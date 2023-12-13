# UI((User Interface)
用户界面（User Interface，简称 UI，亦称使用者界面）是系统和用户之间进行交互和信息交换的媒介，它实现信息的内部形式与人类可以接受形式之间的转换。用户界面是介于用户与硬件而设计彼此之间交互沟通相关软件，目的在使得用户能够方便有效率地去操作硬件以达成双向之交互，完成所希望借助硬件完成之工作，用户界面定义广泛，包含了人机交互与图形用户接口，凡参与人类与机械的信息交流的领域都存在着用户界面。

>百度百科

什么是 UI？您可能把它定义成您按下的按钮、打字的地址栏 、打开和关闭的窗口，等等，这些都是 UI 的元素，但是除了在屏幕上看到的这些之外，还有更多都是 UI 元素。比如鼠标、键盘、音量、屏幕颜色、使用的字体，以及一个对象相对于另一个对象的位置，这些都包含在 UI 之中。实际上，在计算机和用户的交互之中扮演角色的任何对象都是 UI 的组成部分。

>原文链接：https://blog.csdn.net/dlycmsmoses/article/details/7254222

# Swing 的角色

Swing 是 Java 平台的 UI —— 它充当处理用户和计算机之间全部交互的软件。它实际上充当用户和计算机内部之间的中间人。Swing 到底是如何做这项工作的呢？它提供了处理前面一节中描述的 UI 各方面内容的机制：

- 键盘：Swing 提供了捕捉用户输入的方法。
- 颜色：Swing 提供改变在屏幕上看到的颜色的方法。
- 打字的地址栏：Swing 提供了文本组件，处理所有普通任务。
- 音量：Swing 不太擅长。

无论如何，Swing 为您提供了创建自己的 UI 所需要的所有工具

# Swing UI组件
组件类与描述
- JApplet Java.applet.Applet类的扩展，它含有JRootPane的一个实例
- JButton 能显示文本和图形的按钮，它是AWT按钮组件的替代组件
- JCheckBox 能显示文本和图形的复选框，它是AWT选择组件的替代组件
- JCheckBoxMenuItem 一个复选框菜单项，它是AWT的复选框菜单项组件的替代组件
- JComboBox 带下拉列表的文本框，它是AWT选择组件的替代组件
- JComponent 所有轻量J组件的基类
- JDesktopPane 内部窗体的容器
- JDialog　Swing对话框的基类，它扩展了AWT Dialot类
- JEditorPane 用于编辑文本的文本窗格
- JFrame 扩展java.awt.Frame的外部窗体
- JInternalFrame 在JDesktopPane中出现的内部窗体
- JLabel 可显示文本和图标的标签，它是AWT标签组件的替代组件
- JLayeredPane 能够在不同层上显示组件的容器
- JList 显示选项列表的组件，它是AWT列表组件的替代组件
- JMenu 菜单条中显示的一个菜单，它是AWT菜单组件的替代组件
- JMenuBar 用于显示菜单的菜单条，它是AWT菜单条组件的替代组件
- JMenuItem 菜单项，它是AWT菜单项组件的替代组件
- JOptionPane 显示标准的对话框，如：消息和问题对话框
- JPanel 通用容器，它是AWT面板和画布组件的替代组件
- JPasswordfield JTextField的扩展，使输入的字符不可见
- JPopupMenu 弹出式菜单，它是AWT弹出式菜单组件的替代组件
- JProgressBar 进度指示器
- JRadioButton 单选按钮，它是AWT复选框组件的替代组件
- JRootPane 顶层容器，它包含一个玻璃窗格，一个层窗格，一个内容窗格和一个可选的菜单条
- JScrollBar 滚动条，它是AWT滚动条组件的替代组件
- JScrollPane 滚动窗格，它是AWT滚动窗格组件的替代组件
- JSeparator 水平或垂直分隔条
- JSlider 滑杆
- JSplitPane 有两个分隔区的容器，这两个分隔区可以水平排列或者垂直排列且分隔区的大小能自动调整
- JTabbedPane 带选项卡的窗格
- JTable 表格
- JTableHeader 表格头
- JTextArea 用于输入多行文本的文本域，它是AWT文本域组件的替代组件
- JTestComponent 文本组件的基类，它替代AWT的TextComponent类
- JTextField 单行文本域，它替代AWT的单行文本域组件
- JTextPane 简单的文本编辑器
- JToggleButton 两种状态的按钮，它是JCheckBox和JRadioButton组件的基类
- JToolBar 工具条
- JToolTip 当光标停留在一个组件上时，该组件上显示的一行文字
- JTree 用于按钮层次组织数据的结构控件
- JViesport 用于浏览可滚动组件的视口
- JWindow 外部窗口，它是java.awt.Window的扩展

# AWT和Swing的区别

AWT是Abstract Window ToolKit (抽象窗口工具包)的缩写，这个工具包提供了一套与本地图形界面进行交互的接口。AWT 中的图形函数与操作系统所提供的图形函数之间有着一一对应的关系，我们把它称为peers。 也就是说，当我们利用 AWT 来构件图形用户界面的时候，我们实际上是在利用操作系统所提供的图形库。由于不同操作系统的图形库所提供的功能是不一样的，在一个平台上存在的功能在另外一个平台上则可能不存在。为了实现Java语言所宣称的"一次编译，到处运行"的概念，AWT 不得不通过牺牲功能来实现其平台无关性，也就是说，AWT 所提供的图形功能是各种通用型操作系统所提供的图形功能的交集。由于AWT 是依靠本地方法来实现其功能的，我们通常把AWT控件称为重量级控件。

Swing 是在AWT的基础上构建的一套新的图形界面系统，它提供了AWT所能够提供的所有功能，并且用纯粹的Java代码对AWT 的功能进行了大幅度的扩充。例如说并不是所有的操作系统都提供了对树形控件的支持， Swing 利用了AWT 中所提供的基本作图方法对树形控件进行模拟。由于 Swing 控件是用100%的Java代码来实现的，因此在一个平台上设计的树形控件可以在其他平台上使用。由于在Swing 中没有使用本地方法来实现图形功能，我们通常把Swing控件称为轻量级控件。

AWT和Swing之间的基本区别：AWT 是基于本地方法的C/C++程序，其运行速度比较快；Swing是基于AWT 的Java程序，其运行速度比较慢。对于一个嵌入式应用来说，目标平台的硬件资源往往非常有限，而应用程序的运行速度又是项目中至关重要的因素。在这种矛盾的情况下，简单而高效的AWT 当然成了嵌入式Java的第一选择。而在普通的基于PC或者是工作站的标准Java应用中，硬件资源对应用程序所造成的限制往往不是项目中的关键因素，所以在标准版的Java中则提倡使用Swing，也就是通过牺牲速度来实现应用程序的功能。

`简要的讲:`

>AWT 是抽象窗口组件工具包，是 java 最早的用于编写图形节目应用程序的开发包。

>Swing 是为了解决 AWT 存在的问题而新开发的包，它以 AWT 为基础的。

# MVC

Swing 甚至走得更远一步，在基本的 UI 原则之上又放上了一个公共的设计模式。这个设计模式叫做模型-视图-控制器（Model-View-Controller，MVC），它试图“把角色分开”。MVC 让负责显示的代码、处理数据的代码、对交互进行响应并驱动变化的代码彼此分离。

用可视组件显示数据，同时让其他类操纵数据。


# 图形化设计步骤

用java编程的相关设计步骤来分解上面的的程序运行过程如下所示：

1. 创建顶层容器

    对应于程序的初始显现窗口，窗口中放入其它菜单、工具栏、文本框、按钮等组件

    顶层容器图形化界面显示的基础，其它所有的组件（控件）都是直接或间接显示在顶层容器中的。在java中顶层容器有三种，分别是JFrame（框架窗口，即通常的窗口）、JDialog（对话框）、JApplet（用于设计嵌入在网页中的java小程序）。

2. 创建中间容器、组件

    对应于程序中出现的菜单、工具栏（中间容器）、文本框、按钮、单选框、复选框等控件。

    有很多Swing组件可以使用，见前面的Swing UI组件表。

3. 将组件加入容器

    在java中创建组件后，还需要将组件放入相应的容器，才能在顶层容器，如窗口中显示出组件。

4. 设置容器内组件的位置

    组件添加到容器中，还必须设置好组件的显示位置，一般有两种方法来设置组建的显示位置，一是按照与容器的相对距离（以像素为单位），精确固定控件的位置；二是用布局管理器来管理组件在容器内的位置。

5. 处理组件所产生的事件

    即用户执行选择菜单、单击按钮等操作时，就要执行相应的命令，进行相关的程序处理，这就需要设置组件的事件。

# 组件容器的使用

Java中组件容器包含顶层容器和中间容器。

    在java中顶层容器有三种，分别是JFrame（框架窗口，即通常的窗口）、JDialog（对话框）、JApplet（用于设计嵌入在网页中的java小程序），顶层容器是容纳其它组件的基础，即设计图形化程序必须要有顶层容器。

Java中间容器是可以包含其它相应组件的容器，但是中间容器和组件一样，不能单独存在，必须依附于顶层容器。

常见的中间容器有：

- JPanel：最灵活、最常用的中间容器。
- JScrollPane：与 JPanel 类似，但还可在大的组件或可扩展组件周围提供滚动条。
- JTabbedPane：包含多个组件，但一次只显示一个组件。用户可在组件之间方便地切换。
- JToolBar：按行或列排列一组组件（通常是按钮）。

```java
// JFrameDemo1.java

import javax.swing.*;     //使用Swing类，必须引入Swing包

public class JFrameDemo1{

  public staticvoid main( String args[]) {

         //定义一个窗体对象f，窗体名称为"一个简单窗口"        

         Jframe  f = new JFrame("一个简单窗口");

         /*设置窗体左上角与显示屏左上角的坐标，

离显示屏上边缘300像素，离显示屏左边缘300像素     */

         f.setLocation(300, 300);      
         
         f.setLocationRelativeTo(null); //本语句实现窗口居屏幕中央

         f.setSize(300,200);            //设置窗体的大小为300*200像素大小

         f.setResizable(false);       //设置窗体是否可以调整大小，参数为布尔值

         f.setVisible( true);   //设置窗体可见，没有该语句，窗体将不可见，此语句必须有，否则没有界面就没有如何意义了

         f.setDefaultCloseOperation(f.EXIT_ON_CLOSE);   //用户单击窗口的关闭按钮时程序执行的操作
 }

}
```

# JComponent

Swing 的整个可视组件库的基础构造块是 JComponent。它是所有组件的父类。它是一个抽象类，所以不能创建 JComponent，但是作为类层次结构的结果，从字面意义来说它包含了数百个函数，Swing 中的每个组件都可以使用这些函数。显然，有些概念要比其他概念重要，所以对于本教程，需要学习的重要的东西是：

JComponent 不仅是 Swing 组件的基类，还是定制组件的基类（有关的更多信息在“中级 Swing”教程中）。
它为所有组件提供了绘制的基础架构 —— 一些方便进行组件定制的东西（同样，在“中级 Swing”中，有关于这个主题的更多信息）。
它知道如何处理所有的键盘按键。所以类只需要侦听特定的键。
它包含 add() 方法，可以添加其他 JComponent。换种方式来看，可以把任意 Swing 组件添加到其他任何 Swing 组件，从而构造嵌套组件（例如，JPanel 包含 JButton，甚至包含一些古怪的组合，例如 JMenu 包含 JButton）。

简单的swing小部件

## JLabel

Swing 库中最基础的组件是 JLabel。它所做的正是您所期望的：呆在那儿，看起来很漂亮，描述其他组件。下图显示了的 JLabel 实际应用：

### **JLabel**

不太吸引人，但是仍然有用。实际上，在整个应用程序中，不仅把 JLabel 用作文本描述，还将它用作图片描述。每当在 Swing 应用程序中看到图片的时候，它就有可能是 JLabel。JLabel 对于 Swing 初学者来说没有许多意料之外的方法。基本的方法包括设置文本、图片、对齐以及标签描述的其他组件：

- get/setText(): 获取/设置标签的文本。
- get/seticon(): 获取/设置标签的图片。
- get/setHorizontalAlignment(): 获取/设置文本的水平位置。
- get/setVerticalAlignment(): 获取/设置文本的垂直位置。
- get/setDisplayedMnemonic(): 获取/设置标签的访问键（下划线文字）。
- get/setLableFor(): 获取/设置这个标签附着的组件，所以当用户按下 Alt+访问键时，焦点转移到指定的组件。

## JButton

Swing 中的基本动作组件 JButton，是与每个窗口中都能看到的 OK 和 Cancel 一样的按钮；这些按钮所做的正是您希望它们做的工作 —— 在单击它们之后，将发生一些事情。到底会发生什么呢？您必须定义发生的内容（请参阅事件，以获得更多信息）。一个 JButton 实例看起来如下所示：

### **JButton**

用来改变 JButton 属性的方法与 JLabel 的方法类似（您可能发现，在大多数 Swing 组件中，这些属性都类似）。它们控制文本、图片和方向：

- get/setText(): 获取/设置标签的文本。
- get/seticon(): 获取/设置标签的图片。
- get/setHorizontalAlignment(): 获取/设置文本的水平位置。
- get/setVerticalAlignment(): 获取/设置文本的垂直位置。
- get/setDisplayedMnemonic(): 获取/设置访问键（下划线字符），与 Alt 按钮组合时，造成按钮单击。

除了这些方法，我还要介绍 JButton 包含的另外一组方法。这些方法利用了按钮的所有不同状态。状态是对组件进行描述的一个属性，通常采用真/假设置。在 JButton 中，可以包含以下可能状态：活动/不活动、选中/没选中、鼠标经过/鼠标离开、按下/没按下，等等。另外，可以组合这些状态，例如按钮可以在鼠标经过的同时被选中。现在您可能会问自己用这些状态到底要做什么。作为示例，请看看您的浏览器上的后退按钮。请注意在鼠标经过它的时候，图片是如何变化的，在按下该按钮时，图片又是如何变化的。这个按钮利用了不同的状态。每个状态采用不同的图片，这是提示用户交互正在进行的一种普遍并且有效的方式。JButton 上的状态方法是：

- get/setDisabledIcon()
- get/setDisableSelectedIcon()
- get/setIcon()
- get/setPressedIcon()
- get/setRolloverIcon()
- get/setRolloverSelectedIcon()
- get/setSelectedIcon()

## JTextField

Swing 中的基本文本组件是 JTextField，它允许用户在 UI 中输入文本。我肯定您熟悉文本字段：要掌握本教程，则必须使用一个文本字段输入用户名和口令。您输入文本、删除文本、选中文本、把文字四处移动 —— Swing 替您负责所有这些工作。作为 UI 开发人员，利用 JJTextField 时，实际上并不需要做什么。

在任何情况下，这是 JTextField 实际使用时看起来的样子：

### **JTextField**

在处理 JTextField 时，只需要关注一个方法 —— 这应当是很明显的，这个方法就是设置文本的方法： get/setText()，用于获取/设置 JTextField 中的文本。

## JFrame

迄今为止，我介绍了 Swing 的三个基本构造块：标签、按钮和文本字段；但是现在需要个地方放它们，希望用户知道如何处理它们。JFrame 类就是做这个的——它是一个容器，允许您把其他组件添加到它里面，把它们组织起来，并把它们呈现给用户。它有许多其他好处，但是我认为先看看它的图片最简单：

### **JFrame**

JFrame 实际上不仅仅让您把组件放入其中并呈现给用户。比起它表面上的简单性，它实际上是 Swing 包中最复杂的组件。为了最大程度地简化组件，在独立于操作系统的 Swing 组件与实际运行这些组件的操作系统之间，JFrame 起着桥梁的作用。JFrame 在本机操作系统中是以窗口的形式注册的，这么做之后，就可以得到许多熟悉的操作系统窗口的特性：最小化/最大化、改变大小、移动。但是对于本教程的目标来说，把 JFrame 当作放置组件的调色板就足够了。可以在 JFrame 上调用的一些修改属性的方法是：

- get/setTitle(): 获取/设置帧的标题。
- get/setState(): 获取/设置帧的最小化、最大化等状态。
- is/setVisible(): 获取/设置帧的可视状态，换句话说，是否在屏幕上显示。
- get/setLocation(): 获取/设置帧在屏幕上应当出现的位置。
- get/setsize(): 获取/设置帧的大小。
- add(): 将组件添加到帧中。

# SwingWorker

https://blog.csdn.net/vking_wang/article/details/8994882

Swing 应用程序员常见的错误是误用 Swing 事件调度线程（Event DispatchThread，EDT)。他们要么**从非UI线程访问UI组**件；要么不考虑事件执行顺序；要么不**使用独立任务线程而在EDT线程上执行耗时任务**，结果使编写的应用程序变得响应迟钝、速度很慢。`耗时计算和输入/输出(IO)密集型任务不应放在SwingEDT上运行`。发现这种问题的代码并不容易，但 Java SE6 提供 了javax.swing.SwingWorker 类，使修正这种代码变得更容易。

`使用SwingWorker，程序能启动一个任务线程来异步查询，并马上返回EDT线程，允许EDT继续执行后续的UI事件。`

**SwingWorker类帮你管理任务线程和EDT之间的交互**，尽管 SwingWorker 不能解决并发线程中遇到的所有问题，但的确有助于分离 SwingEDT 和任务线程，使它们各负其责：对于 EDT 来说，就是绘制和更新界面，并响应用户输入；对于任务线程来说，就是执行和界面无直接关系的耗时任务和 I/O 密集型操作。

## SwingWorker结构

SwingWoker实现了java.util.concurrent.RunnableFuture接口。RunnableFuture接口是Runnable和Future两个接口的简单封装。

因为实现了Runnable，所以有run方法，调用FutureTask.run()

![Future接口结构](\img\Future接口结构.png)

```java
public abstract class SwingWorker<T, V> implements RunnableFuture<T> {
    //FutureTask
    private final FutureTask<T> future;
    public final void run() {
        future.run();
    }
 
    public SwingWorker() {
        Callable<T> callable = 
                new Callable<T>() {
//1. 任务线程一创建就处于PENDING状态
                    public T call() throws Exception {
//2. 当doInBackground方法开始时，任务线程就进入STARTED状态
                    setState(StateValue.STARTED);  
                        return doInBackground();
                    }
                };
 
        //FutureTask
        future = new FutureTask<T>(callable) {
 
                       @Override
                       protected void done() {
                           doneEDT();
//3. 当doInBackground方法完成后，任务线程就处于DONE状态
                           setState(StateValue.DONE); 
                       }
                   };
 
       state = StateValue.PENDING;
       propertyChangeSupport = new SwingWorkerPropertyChangeSupport(this);
       doProcess = null;
       doNotifyProgressChange = null;
    }
 
}

```

SwingWorker有两个**类型参数：T及V**。**T**是 doInBackground 和 get 方法的返回类型；**V**是 publish 和 process 方法要处理的数据类型

`SwingWorker实例不可复用，每次执行任务必须生成新的实例。`

## doInBackground 和 get 和 done

```java
//1、doInBackground
    protected abstract T doInBackground() throws Exception ;
    //2、get --不可重写
    public final T get() throws InterruptedException, ExecutionException {
        return future.get();
    }
    //3、done
    protected void done() {
    }
 
 
    /**
     * Invokes {@code done} on the EDT.
     */
    private void doneEDT() {
        Runnable doDone = 
            new Runnable() {
                public void run() {
                    done();
                }
            }; 
        //SwingWorker在EDT上激活done()
        if (SwingUtilities.isEventDispatchThread()) { 
            doDone.run();
        } else {
            doSubmit.add(doDone);
        }
    }
```

**doInBackground** 方法作为任务线程的一部分执行，它负责完成线程的基本任务，并以**返回值来作为线程的执行结果**。继承类须覆盖该方法并确保包含或代理任务线程的基本任务。`不要直接调用该方法，应使用任务对象的execute方法来调度执行。`

在获得执行结果后应使用 SwingWorker 的 **get** 方法获取doInBackground方法的结果。`可以在EDT上调用get方法，但该方法将一直处于阻塞状态，直到任务线程完成。最好只有在知道结果时才调用get方法，这样用户便不用等待。`为防止阻塞，可以使用isDone方法来检验doInBackground是否完成。另外调用方法get(longtimeout, TimeUnitunit)将会一直阻塞直到任务线程结束或超时。**get获取任务结果的最好地方是在done方法内。**

在 doInBackground 方法完成之后，SwingWorker 调用 **done** 方法。如果任务需要在完成后使用线程结果更新GUI组件或者做些清理工作，可覆盖done方法来完成它们。这儿是调用get方法的最好地方，因为此时已知道线程任务完成了，**SwingWorker在EDT上激活done方法，因此可以在此方法内安全地和任何GUI组件交互。**

```java
SwingWorker testWorker = new SwingWorker<Icon , Void>(){
      @Override
       protected Icon doInBackground() throws Exception {
		Icon icon = retrieveImage(strImageUrl); 
       		return icon; 
       } 
 
       protected void done(){ 
       //没有必要用invokeLater！因为done()本身是在EDT中执行的 
           SwingUtilities.invokeLater(new Runnable(){ 
       		@Override 
       		public void run() {
			Icon icon= get();
                        lblImage.setIcon(icon); //lblImage可通过构造函数传入
                }			
}
//execute方法是异步执行，它立即返回到调用者。在execute方法执行后，EDT立即继续执行
testWorker.execute();

```

- 指定Icon作为doInBackground和get方法的返回类型
- 因为并不产生任何中间数据，所以指定Void类型作为中间结果类型。

## publish 和 process

SwingWorker 在 doInBackground 方法结束后才产生最后结果，但任务线程也可以产生和公布中间数据。有时没必要等到线程完成就可以获得中间结果。

中间结果是任务线程在产生最后结果之前就能产生的数据。当任务线程执行时，它可以发布类型为**V**的中间结果，通过覆盖 process 方法来处理中间结果。

任务对象的父类会在EDT线程上激活 process 方法，`因此在process方法中程序可以安全的更新UI组件。`

```java

//SwingWorker.publish
   protected final void publish(V... chunks) {
        synchronized (this) {
            if (doProcess == null) {
                doProcess = new AccumulativeRunnable<V>() {
                    @Override
                    public void run(List<V> args) {
                        //调用process
                        process(args); 
                    }
                    @Override
                    protected void submit() {
                        doSubmit.add(this);
                    }
                };
            }
        }
        doProcess.add(chunks);
    }
 
    //SwingWorker.process 在EDT中调用
    protected void process(List<V> chunks) {
    }

```

当从任务线程调用 publish 方法时， SwingWorker 类调度 process 方法。有意思的是 process 方法是在 EDT 上面执行，这意味着可以同 Swing 组件和其模型直接交互。

例如可让 publish 处理 Icon 类型的数据；则 doInBackground 对应应该返回`List<Icon>`类型

使用 publish 方法来发布要处理的中间数据，当 ImageSearcher 线程下载缩略图时，它会随着下载而更新图片信息列表，还会发布每一批图像信息，以便UI 能在图片数据到达时显示这些图片。

如果 SwingWorker 通过 publish 发布了一些数据，那么也应该实现  process 方法来处理这些中间结果，任务对象的父类会在 EDT 线程上激活 process 方法，因此在此方法中程序可以安全的更新 UI 组件。

```java

private void retrieveAndProcessThumbnails(List<ImageInfo> infoList) {
  for (int x=0; x <infoList.size() && !isCancelled(); ++x) {           
    ImageInfo info = infoList.get(x);
    String strImageUrl = String.format("%s/%s/%s_%s_s.jpg",
    IMAGE_URL, info.getServer(), info.getId(), info.getSecret());
    Icon thumbNail = retrieveThumbNail(strImageUrl);
    info.setThumbnail(thumbNail);
    //发布中间结果
    publish(info); 
    setProgress(100 * (x+1)/infoList.size());
  }
}   
/**
 * Process is called as a result of this worker thread's calling the
 * publish method. This method runs on the event dispatch thread.
 *
 * As image thumbnails are retrieved, the worker adds them to the
 * list model.
 *
 */
@Override
protected void process(List<ImageInfo> infoList) {
  for(ImageInfo info: infoList) {
    if (isCancelled()) { //见下节
      break;
    }
    //处理中间结果
    model.addElement(info);
  }     
}

```

## cancel 和 isCancelled 
```java

    public final boolean cancel(boolean mayInterruptIfRunning) {
        return future.cancel(mayInterruptIfRunning);
    }
 
    /**
     * {@inheritDoc}
     */
    public final boolean isCancelled() {
        return future.isCancelled();
    }

```

如果想允许程序用户取消任务，实现代码要在 SwingWorker 子类中周期性地检查取消请求。调用isCancelled方法来检查是否有取消请求。检查的时机主要是：
- doInBackground方法的子任务在获取每个缩略图之前
- process方法中在更新GUI列表模型之前
- done方法中在更新GUI列表模型最终结果之前

可以通过调用其 cancel 方法取消 SwingWorker 线程
```java

private void searchImages(String strSearchText, int page) {
 
  if (searcher != null && !searcher.isDone()) {
    // Cancel current search to begin a new one.
    // You want only one image search at a time.
    //检查现有线程是否正在运行，如果正在运行则调用cancel来取消
    searcher.cancel(true);
    searcher = null;
  }
  ...
  // Provide the list model so that the ImageSearcher can publish
  // images to the list immediately as they are available.
  searcher = new ImageSearcher(listModel, API_KEY, strEncodedText, page);
  searcher.addPropertyChangeListener(listenerMatchedImages);
  progressMatchedImages.setIndeterminate(true);
  // Start the search!
  searcher.execute();
  // This event thread continues immediately here without blocking.
} 
```

## setProgress 和 getProgress

任务对象有一个进度属性，随着任务进展时，可以将这个属性从 0 更新到 100 标识任务进度。当你在任务实例内处理这些信息时，你可以调用 setProgress 方法来更新这个属性。

当该属性发生变化时，任务通知处理器进行处理。（？）

```java

//javax.imageio.ImageReader reader
 
reader.addIIOReadProgressListener(new IIOReadProgressListener() {
  ...           
  public void imageProgress(ImageReader source, float percentageDone) {
    setProgress((int) percentageDone);
  }
  public void imageComplete(ImageReader source) {
    setProgress(100);
  }
});
```

客户端调用1、更新进度条事件处理

```java
/**
 * ProgressListener listens to "progress" property changes 
   in the SwingWorkers that search and load images.
 */
class ProgressListener implements PropertyChangeListener {
  // Prevent creation without providing a progress bar.
  private ProgressListener() {}  
  ProgressListener(JProgressBar progressBar) {
    this.progressBar = progressBar;
    this.progressBar.setValue(0);
  }  
  public void propertyChange(PropertyChangeEvent evt) {
    String strPropertyName = evt.getPropertyName();
    if ("progress".equals(strPropertyName)) {
      progressBar.setIndeterminate(false);
      int progress = (Integer)evt.getNewValue();
      progressBar.setValue(progress);
    }
  }  
  private JProgressBar progressBar;
} 
```

客户端调用2、添加监听
```java

private void listImagesValueChanged(ListSelectionEvent evt) {
  ...
  ImageInfo info = (ImageInfo) listImages.getSelectedValue();
  String id = info.getId();
  String server = info.getServer();
  String secret = info.getSecret();
  // No need to search an invalid thumbnail image
  if (id == null || server == null || secret == null) {
    return;
  }
  String strImageUrl = String.format(IMAGE_URL_FORMAT, server, id, secret);
  retrieveImage(strImageUrl);
  ...
}    
private void retrieveImage(String imageUrl) {
  // SwingWorker，不可复用
  ImageRetriever imgRetriever = new ImageRetriever(lblImage, imageUrl);
  progressSelectedImage.setValue(0);
  // Listen for changes in the "progress" property.
  // You can reuse the listener even though the worker thread will be a new SwingWorker.
  imgRetriever.addPropertyChangeListener(listenerSelectedImage);  
  progressSelectedImage.setIndeterminate(true);  
  // Tell the worker thread to begin with this asynchronous method.
  imgRetriever.execute();
  // This event thread continues immediately here without blocking.  
}     

```

# SwingWorker应用详解
https://www.cnblogs.com/mhzhou-whyj/p/7832840.html

前续知识，一个swing程序有三个类型的线程

- 初始化线程：就是main函数，用来启动GUI
- 用户事件调度线程EDT：负责对GUI组件的渲染和刷新，它只有一个，一定要注意这个问题，它处理的就是事件队列里的事情，他通过调用事件处理器来响应用户交互。所有的事件处理都是在EDT上进行的。
- 任务线程：响应时具体的数据处理。

Swing 框架负责管理组件绘制、更新以及 EDT 上的线程处理。可以想象，该线程的事件队列很繁忙，几乎每一次 GUI 交互和事件都是通过它完成。

事件队列的上任务必须非常快，否则就会阻塞其他任务的执行，使队列里阻塞了很多等待执行的事件，造成界面响应不灵活，让用户感觉到界面响应速度很慢，使他们失去兴趣。理想情况下，任何需时超过30到100毫秒的任务不应放在EDT上执行，否则用户就会觉察到输入和界面响应之间的延迟。

在这里一定注意：

 1. 其他线程上访问UI组件和事件处理器都是不安全的，都有可能导致界面的更新和绘制错误。
 2. 在EDT上执行耗时性任务会发生阻塞队列，会让你觉得界面很卡，所以，要尽可能的不要在EDT上编写耗时性的代码。
 3. 应当使用独立的任务线程来执行耗时性的任务。

 `所以到现在一句话，所有耗时性的任务（即任何干扰或延迟UI的任务）都应该放在任务线程中去解决。在初始化线程和任务线程中与UI组件或其缺省数据模型进行的交互都是非线程安全的。`

 既然是非线程安全怎么办呢？这时候一个非常强大的类就出现了，神一般的 SwingWorker 工具类，它帮助任务线程与 EDT 进行交互，虽然不能实现完全的线程安全，但是解决了大部分的非线程安全的问题。通过它使任务线程和 EDT 各负其责， EDT 实现绘制和刷新，任务线程实现与界面无关的耗时性的操作。将 EDT 线程仅用于 GUI 任务。

同步与异步：

- 同步是程序在发起请求后开始处理事件并等待处理的结果或等待请求执行完毕，在此之前程序被block住直到请求完成。
- 异步是当前程序发起请求后立即返回，当前程序不会立即处理该事件并等待处理的结果，请求是在稍后的某一时间才被处理。

 串行与并行：

- 串行是指多个要处理请求顺序执行，处理完一个再处理下一个；容易阻塞。
- 并行可以理解为并发，是同时处理多个请求（实际上我们只能理解为是这样，特别是CPU数目少于线程数的机器而言，真正意义的并发是不存在的，各个线程只是断断续续地交替地执行）。

## SwingWorker类介绍

Class SwingWorker<T,V>

参数类型

- T - 该 SwingWorker's doInBackground和 get方法返回的结果类型，就是最终结果的类型
- V - 用于执行中间结果的类型 SwingWorker's publish和 process方法的处理的数据类型 ，就是中间结果的类型

`All Implemented Interfaces:Runnable, Future<T>, RunnableFuture<T>`

最重要的几个方法：

1. `protected abstract T doInBackground​() `

计算一个结果，如果不能这样做，就会抛出一个异常。 
首先，这个方法一定要重写，因为这里是处理一个swingworker实例的最后计算结果，当这个函数被执行完后，说明这个线程的所有顺序执行的程序已经执行完了。

其次，想要获取doinbackground方法的返回值要使用get方法，get方法是同步的，所以一般使用时在done方法中调用或者在判断isdone后执行。
最后，因为，当doinbackground执行完后，在EDT中会自动执行done方法。

2. `protected void done​()`

 　　doInBackground方法完成后，在EDT中被执行。 

3. `void execute​()`

 　　计划这个 SwingWorker在 工作线程上执行。用它来开启这个进程，就是说一旦执行这个方法，swingworker就进入了工作线程。

4. `T get​()`

 　　等待doInBackground​计算完成，返回doInBackground​的返回值。 

5. `boolean isDone​()`

 　　判断是否完成整个计算过程，如果此任务完成，则返回 true 。 

6. `protected void process​(List<V> chunks)`

 　　在 事件调度线程上异步接收来自 publish方法的数据块。即中间结果。中间结果是任务线程在产生最后结果之前就能产生的数据。当任务线程执行时，它可以发布类型为V的中间结果，通过覆盖process方法来处理中间结果。任务对象的父类会在EDT线程上激活process方法，因此在process方法中程序可以安全的更新UI组件。这个方法线程安全的实现了DET与任务线程之间的交互。过程是这样的，当从任务线程调用publish方法时，在DET上自动执行process方法。

7. `protected void publish​(V chunks)`

 　　发送数据chunks到 process(java.util.List<V>)方法中的list列表中。这个方法是自动在DET上被调用的。是由任务对象的父类将其激活的。
 
# java中AWT和SWing的区别与联系
https://blog.csdn.net/iamluole/article/details/8142257

AWT和Swing都是java中的包。

AWT(Abstract Window Toolkit)：抽象窗口工具包，早期编写图形界面应用程序的包。

Swing ：为解决 AWT 存在的问题而新开发的图形界面包。Swing是对AWT的改良和扩展。   

AWT和Swing的实现原理不同：
       AWT的图形函数与操作系统提供的图形函数有着一一对应的关系。也就是说，当我们利用 AWT构件图形用户界面的时候，实际上是在利用操作系统的图形库。
       不同的操作系统其图形库的功能可能不一样，在一个平台上存在的功能在另外一个平台上则可能不存在。为了实现Java语言所宣称的"一次编译，到处运行"的概念，AWT不得不通过牺牲功能来实现平台无关性。因此，AWT 的图形功能是各操作系统图形功能的“交集”。
        因为AWT是依靠本地方法来实现功能的，所以AWT控件称为“重量级控件”。

       而Swing ，不仅提供了AWT 的所有功能，还用纯粹的Java代码对AWT的功能进行了大幅度的扩充。
       例如：并不是所有的操作系统都提供了对树形控件的支持， Swing则利用了AWT中所提供的基本作图方法模拟了一个树形控件。
       由于 Swing是用纯粹的Java代码来实现的，因此Swing控件在各平台通用。
       因为Swing不使用本地方法，故Swing控件称为“轻量级控件”。

       AWT和Swing之间的区别：
       1)AWT 是基于本地方法的C/C++程序，其运行速度比较快；Swing是基于AWT的Java程序，其运行速度比较慢。
       2)AWT的控件在不同的平台可能表现不同，而Swing在所有平台表现一致。

       在实际应用中，应该使用AWT还是Swing取决于应用程序所部署的平台类型。例如：
       1)对于一个嵌入式应用，目标平台的硬件资源往往非常有限，而应用程序的运行速度又是项目中至关重要的因素。在这种矛盾的情况下，简单而高效的AWT当然成了嵌入式Java的第一选择。
       2)在普通的基于PC或者是工作站的标准Java应用中，硬件资源对应用程序所造成的限制往往不是项目中的关键因素。所以在标准版的Java中则提倡使用Swing， 也就是通过牺牲速度来实现应用程序的功能。

在java中，AWT包的名称是java.awt，Swing包的名称是javax.swing。
java.awt和javax.swing两个包的层次关系如下：

![](../img\AWT包结构.gif)

Container类是java.awt.Component类的子类，JComponent类又继承自Container类。因此，JComponent类是AWT和Swing的联系之一。
除了Swing顶层容器类(top level containers)以外，其余所有的Swing组件类都继承自JComponent类，如前所述，JComponent类是Container类的子类，因此，所有的Swing组件都可作为容器使用。
Swing顶层容器类包括了JFrame、JDialog、JApplet、JWindow，它们为其他的Swing组件提供了绘制自身的场所。

![](../img\Swing包结构.gif)
　　
Swing组件按功能可分为如下几类:
　　1、顶层容器:JFrame, JApplet, JDialog和JWindow。
　　2、中间容器:JPanel, JScrollPane, JSplitPane, JTooIBar等。
　　3、特殊容器:在用户界面上具有特殊作用的中间容器，如JlnternalFrame、JRootPane、JLayeredPane和JDestopPane等。
　　4、基本组件:实现人机交互的组件，如Button、 JComboBox、Just, Menu、Mider等。
　　5、不可编辑信息的显示组件:向用户显示不可编辑信息的组件，如JLabel、JProgressBar和JTooITip等。
　　6、可编辑信息的显示组件:向用户显示能被编辑的格式化信息的组件，如JTable、JTextArea和JTextField等。
　　7、特殊对话框组件:可以直接产生特殊对话框的组件，如JColorChoosor和JFileChooser等。

Swing的4个顶层容器类直接继承了AWT组件，而不是从JComponent派生出来的，它们分别是：JFrame、JDialog、JApplet和JWindow。
顶层容器类并不是轻量级组件，而是重量级组件(需要部分委托给运行平台上GUI组件的对等体)。


顶层容器中：
1.JApplet可作为java小应用程序的窗体，但通常使用java.applet.Applet类来创建小应用程序。
2.JFrame集成自AWTFrame类，通常作为主窗体使用。
3.JDialog用于创建对话框的窗体。
4.JWindow与AWT中的Window相似，但几乎不用，因为没有太大的实用价值。

Swing组件的类名和对应AWT组件的类名基本一致，只要在原来的AWT组件类名前添加“J”即可，但有如下几个例外：
　　1、JComboBox:对应于AWT里的Choice组件，但比Choice组件功能更丰富。
　　2、JFileChooser:对位于AWT里的FileDialog组件。
　　3、JSrcoIIBar:对应AWT里的Scrollbar。注意两个组件类名中b字母的大小写差别。
　　4、JCheckBox:对应于AWT里的Checkbox。注意两个组件类名中b字母的大小写差别。
　　5、JCheckBoxMenuItem:对应于AWT里的CheckboxMenuItem，注意两个组件类名中b字母的大小写差别。

　　上面JCheckBox和JCheckBoxMenuItem与Checkbox和CheckboxMenuItem字母B的大小写差别，主要是因为早期Java命名不太规范造成的。