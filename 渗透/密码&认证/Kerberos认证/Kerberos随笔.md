# 极简化认证流程
## 仅C端 和 S端知道 一个相同的`KServer-Client`
## C端请求时发送两份文件
- `不加密的身份(Identity)`
- 用`KServer-Client`当做公钥(Public Key)`加密的身份(Identity)`
## S端认证(Authentication)时使用`KServer-Client`解密C端发送的`加密的身份(Identity)` 并与`不加密的身份(Identity)`对比

# 简化认证流程
 1. 首先Client向KDC发送一个对SServer-Client的申请。这个申请的内容可以简单概括为“我是某个Client，我需要一个`Session Key`用于访问某个Server ”。

 2. KDC在接收到这个请求的时候，生成一个`Session Key`，为了保证这个`Session Key`仅仅限于发送请求的Client和他希望访问的Server知晓，KDC会为这个`Session Key`生成两个Copy，分别被Client和Server使用。然后从Account database中提取Client和Server的Master Key分别对这两个Copy进行对称加密。对于后者，和`Session Key`一起被加密的还包含关于Client的一些信息。

 3. KDC现在有了两个分别被Client和Server 的Master Key加密过的`Session Key`，随后将这两个被加密的Copy一并发送给Client，属于Server的那份由Client发送给Server

# 名词列表

>- `Long-term Key(长期秘钥)`：长期内保持不变的key
>
>- `Master Key(万能钥匙)`：密码是证明身份的凭据，必须通过基于密码的派生的信息来证明用户的真实身份，一般将密码进行Hash运算得到一个Hash code,这样得到的Hash Code叫做Master Key
>
>- `Short-term Key(短期秘钥)`：`Long-term Key(长期秘钥)`加密的数据包不安全，不能在网络上传输，所以使用`Short-term Key(短期秘钥)`加密需要传输的的数据，这种Key只在一定时间内有效。
>
>- `Session Key(会话密钥)`:保证用户跟其它计算机或者两台计算机之间安全通信会话而随机产生的加密和解密密钥。会话密钥有时称对称密钥，因为同一密钥用于加密和解密。在本认证中也称为SServer-Client
>
>- `Timestamp(时间戳)`:一个能表示一份数据在某个特定时间之前已经存在的、 完整的、 可验证的数据,通常是一个字符序列，唯一地标识某一刻的时间。

# KDC(Kerberos分发中心)
`Kerberos Distribution Center-KDC`:KDC在整个`Kerberos 认证(Authentication)`中作为Client和Server共同信任的第三方起着重要的作用。

对于一个`Windows Domain`来说，`Domain Controller`扮演着`KDC`的角色。

`KDC`维护着一个存储着该Domain中所有帐户的`Account Database（一般地，这个Account Database由AD来维护）`，他知道属于每个Account的名称和派生于该Account Password的`Master Key`。而用于Client和Server相互认证的`SServer-Client`就是由KDC分发。

# Authenticator(证明者)
在Kerberos的Authenticator实际上就是关于Client的一些信息和当前时间的一个`Timestamp`

## `Time Synchronization(时间同步)`的重要性

基于Timestamp的认证机制只有在Client和Server端的时间保持同步的情况才有意义。所以保持`Time Synchronization`在整个认证过程中显得尤为重要。在一个`Domain`中，一般通过访问同一个`Time Service`获得当前时间的方式来实现时间的同步。

# `双向认证（Mutual Authentication）`

Kerberos一个重要的优势在于它能够提供双向认证：不但Server可以对Client 进行认证，Client也能对Server进行认证。

1. 如果Client需要对他访问的Server进行认证，会在它向Server发送的`Credential(提供证明书)`中设置一个是否需要认证的`Flag`。
2. Server在对Client认证成功之后，会把`Authenticator`中的`Timestamp`提出出来，通过`Session Key`进行加密并发送。
3. 当Client接收到并使用`Session Key`进行解密之后，如果确认`Timestamp`和原来的完全一致，那么他可以认定Server正式他试图访问的Server。

>不直接发送`Authenticator`的原因是为了防止盗用者假冒Server

# `Ticket Granting Service`
`Ticket`必须从一个合法的`Ticket颁发机构`获得，这个颁发机构就是Client和Server双方信任的`KDC`， 同时这张Ticket具有超强的防伪标识：`它是被Server的Master Key加密的`。

# 认证过程
## 1. `Authentication Service Exchange`

通过这个`Sub-protocol`，`KDC`（`确切地说是KDC中的Authentication Service`）实现对Client身份的确认，并颁发给该Client一个`TGT`。

Client向`KDC`的`Authentication Service`发送`Authentication Service Request（KRB_AS_REQ）`, 为了确保`KRB_AS_REQ`仅限于`自己`和`KDC`知道，Client使用自己的`Master Key`对`KRB_AS_REQ`的`主体部分进行加密`（`KDC可以通过Domain 的Account Database获得该Client的Master Key`）。

KRB_AS_REQ的大体包含以下的内容：

- `Pre-authentication data`：包含用以证明自己`身份的信息`。说白了，就是证明自己知道自己声称的那个account的Password。一般地，它的内容是一个`被Client的Master key加密过的Timestamp`。
- `Client name & realm`: 简单地说就是`Domain name\Client`
- `Server Name`：注意这里的`Server Name并不是Client真正要访问的Server的名称`，而我们也说了`TGT`是和`Server`无关的（`Client`只能使用`Ticket`，而不是`TGT`去访问`Server`）。`这里的Server Name实际上是KDC的Ticket Granting Service的Server Name`。

`AS（Authentication Service）`通过它接收到的`KRB_AS_REQ`验证发送方的是否是在`Client name & realm`中声称的那个人，也就是说要验证发送放是否知道Client的Password。所以`AS`只需从`Account Database`中提取Client对应的`Master Key`对`Pre-authentication data`进行解密，如果是一个合法的`Timestamp`，则可以证明发送放提供的是正确无误的密码。验证通过之后，`AS`将一份`Authentication Service Response（KRB_AS_REP）`发送给Client。`KRB_AS_REQ`主要包含两个部分：`本Client的Master Key加密过的Session Key（SKDC-Client：Logon Session Key）`和`被自己（KDC）加密的TGT`。

`TGT`大体又包含以下的内容：

- `Session Key`: `SKDC-Client`：`Logon Session Key`
- `Client name & realm`: 简单地说就是`Domain name\Client`
- `End time`: `TGT到期的时间`。

Client通过自己的`Master Key`对第一部分解密获得`Session Key（SKDC-Client：Logon Session Key）`之后，携带着`TGT`便可以进入下一步：`TGS（Ticket Granting Service）Exchange`。

## 2. `TGS（Ticket Granting Service）Exchange`

`TGS（Ticket Granting Service）Exchange`通过Client向`KDC`中的`TGS（Ticket Granting Service）`发送`Ticket Granting Service Request（KRB_TGS_REQ）`开始

`KRB_TGS_REQ`大体包含以下的内容：

- `TGT`：Client通过`AS Exchange`获得的`Ticket Granting Ticket`，`TGT`被`KDC`的`Master Key`进行加密。
- `Authenticator`：用以证明当初`TGT`的拥有者是否就是自己，所以它必须以`TGT`的办法方和自己的`Session Key（SKDC-Client：Logon Session Key）`来进行加密。
- `Client name & realm`: 简单地说就是`Domain name\Client`。
- `Server name & realm`: 简单地说就是`Domain name\Server`，这回是`Client试图访问的那个Server`。

`TGS`收到`KRB_TGS_REQ`在发给Client真正的`Ticket`之前，先得整个Client提供的那个`TGT`是否是`AS`颁发给它的。于是它不得不通过Client提供的`Authenticator`来证明。但是`认证(Authentication)`是通过`Logon Session Key（SKDC-Client）`进行加密的，而自己并没有保存这个`Session Key`。所以`TGS`先得通过自己的`Master Key`对Client提供的`TGT`进行解密，从而获得这个`Logon Session Key（SKDC-Client）`，再通过这个L`ogon Session Key（SKDC-Client）`解密`Authenticator`进行验证。验证通过向对方发送`Ticket Granting Service Response（KRB_TGS_REP）`。

这个`KRB_TGS_REP`有两部分组成：

- 使用`Logon Session Key（SKDC-Client）`加密过用于Client和Server的`Session Key（SServer-Client）`
- 使用Server的`Master Key`进行加密的`Ticket`。

    该Ticket大体包含以下一些内容：

    - `Session Key`：`SServer-Client`。
    - `Client name & realm`: 简单地说就是`Domain name\Client`。
    - `End time`: `Ticket的到期时间`。

Client收到`KRB_TGS_REP`，使用`Logon Session Key（SKDC-Client）`解密第一部分后获得`Session Key（SServer-Client）`。有了`Session Key`和`Ticket`，Client就可以之间和Server进行交互，而无须在通过`KDC`作中间人了。所以我们说`Kerberos是一种高效的认证方式`，它可以`直接通过Client和Server双方来完成`，不像Windows NT 4下的NTLM认证方式，每次认证都要通过一个双方信任的第3方来完成。

## 3. `CS（Client/Server ）Exchange`

Client通过`TGS Exchange`获得Client和Server的`Session Key（SServer-Client）`，随后创建用于证明自己就是`Ticket`的真正所有者的`Authenticator`，并使用`Session Key（SServer-Client）`进行加密。最后将这个被加密过的`Authenticator`和`Ticket`作为`Application Service Request（KRB_AP_REQ）`发送给Server。除了上述两项内容之外，`KRB_AP_REQ`还包含一个`Flag`用于表示Client是否需要进行`双向验证（Mutual Authentication）`。

Server接收到`KRB_AP_REQ`之后，通过自己的`Master Key`解密`Ticket`，从而获得`Session Key（SServer-Client）`。通过`Session Key（SServer-Client）`解密`Authenticator`，进而验证对方的身份。验证成功，让Client访问需要访问的资源，否则直接拒绝对方的请求。

对于需要进行双向验证，Server从`Authenticator`提取`Timestamp`，使用`Session Key（SServer-Client）`进行加密，并将其发送给Client用于Client验证Server的身份。

# 4. `User2User Protocol`

以某个`Entity(实体?)`的`Long-term Key`加密的数据不应该在网络中传递。

原因很简单，所有的加密算法都不能保证100%的安全，对加密的数据进行解密只是一个时间的过程，最大限度地提供安全保障的做法就是：使用一个`Short-term key`（`Session Key`）代替`Long-term Key`对数据进行加密，使得恶意用户对其解密获得加密的Key时，该Key早已失效。但是对于`3个Sub-Protocol的C/S Exchange`，Client携带的`Ticket`却是被`Server Master Key`进行加密的，这显现不符合我们提出的原则，降低Server的安全系数。

所以我们必须寻求一种解决方案来解决上面的问题。这个解决方案很明显：就是采用一个`Short-term`的`Session Key`，而不是`Server Master Key`对`Ticket`进行加密。这就是我们今天要介绍的`Kerberos的第4个Sub-protocol`：`User2User Protocol`。我们知道，既然是`Session Key`，仅必然涉及到两方，而在Kerberos整个认证过程涉及到3方：`Client、Server和KDC`，所以用于加密`Ticket`的只可能是Server和`KDC`之间的`Session Key（SKDC-Server）`。

我们知道Client通过在`AS Exchange阶段`获得的`TGT`从`KDC`那么获得访问Server的`Ticket`。原来的`Ticket`是通过Server的`Master Key`进行加密的，而这个`Master Key`可以通过`Account Database`获得。但是现在`KDC`需要使用Server和`KDC`之间的`SKDC-Server`进行加密，而`KDC`是不会维护这个`Session Key`，所以这个`Session Key`只能靠申请`Ticket`的Client提供。所以在`AS Exchange`和`TGS Exchange`之间，Client还得对Server进行请求已获得Server和`KDC`之间的`Session Key（SKDC-Server）`。而对于Server来说，它可以像Client一样通过`AS Exchange`获得他和`KDC`之间的`Session Key（SKDC-Server）`和一个封装了这个`Session Key`并被`KDC`的`Master Key`进行加密的`TGT`，一旦获得这个`TGT`，Server会缓存它，以待Client对它的请求。我们现在来详细地讨论这一过程。

# 完整简易过程（4步
1. **AS Exchange**：Client通过此过程获得了属于自己的`TGT`，有了此`TGT`，Client可凭此向`KDC`申请用于访问某个Server的`Ticket`。

2. 这一步的主要任务是获得封装了Server和`KDC`的`Session Key（SKDC-Server）`的属于Server的`TGT`。如果该`TGT`存在于Server的缓存中，则Server会直接将其返回给Client。否则通过`AS Exchange`从`KDC`获取。

3. **TGS Exchange**：Client通过向`KDC`提供自己的`TGT`，Server的`TGT`以及`Authenticator`向`KDC`申请用于访问Server的`Ticket`。`KDC`使用先用自己的`Master Key`解密Client的`TGT`获得`SKDC-Client`，通过`SKDC-Client`解密A`uthenticator`验证发送者是否是`TGT`的真正拥有者，验证通过再用自己的`Master Key`解密Server的`TGT`获得`KDC`和Server 的`Session Key（SKDC-Server）`，并用该`Session Key`加密`Ticket`返回给Client。

4. **C/S Exchange**：Client携带者通过`KDC`和Server 的`Session Key（SKDC-Server）`进行加密的`Ticket`和通过Client和Server的`Session Key（SServer-Client`）的`Authenticator`访问Server，Server通过`SKDC-Server`解密`Ticket`获得`SServer-Client`，通过`SServer-Client`解密`Authenticator`实现对Client的验证。

# Kerberos的优点

分析整个Kerberos的认证过程之后，我们来总结一下Kerberos都有哪些优点：

1. 较高的Performance(性能)

    虽然我们一再地说Kerberos是一个涉及到3方的认证过程：Client、Server、KDC。但是一旦Client获得用过访问某个Server的Ticket，该Server就能根据这个Ticket实现对Client的验证，而无须KDC的再次参与。和传统的基于Windows NT 4.0的每个完全依赖Trusted Third Party的NTLM比较，具有较大的性能提升。

2. 实现了双向验证（Mutual Authentication）

    传统的NTLM认证基于这样一个前提：Client访问的远程的Service是可信的、无需对于进行验证，所以NTLM不曾提供双向验证的功能。这显然有点理想主义，为此Kerberos弥补了这个不足：Client在访问Server的资源之前，可以要求对Server的身份执行认证。

3. 对Delegation的支持

    Impersonation和Delegation是一个分布式环境中两个重要的功能。Impersonation允许Server在本地使用Logon 的Account执行某些操作，Delegation需用Server将logon的Account带入到另过一个Context执行相应的操作。NTLM仅对Impersonation提供支持，而Kerberos通过一种双向的、可传递的（Mutual 、Transitive）信任模式实现了对Delegation的支持。

4. 互操作性（Interoperability）

    Kerberos最初由MIT首创，现在已经成为一行被广泛接受的标准。所以对于不同的平台可以进行广泛的互操作。