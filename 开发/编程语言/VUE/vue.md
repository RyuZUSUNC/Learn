## 第一个Vue程序
【说明】IDEA可以安装Vue的插件!
  注意：Vue不支持IE 8及以下版本， 因为Vue使用了IE 8无法模拟的ECMAScript 5特性。但它支持所有兼容ECMAScript 5的浏览器。

**（1）下载地址**
- CDN
```
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.min.js"></script>
```
**（2）代码编写**

Vue.js的核心是实现了MVVM模式， 她扮演的角色就是View Model层， 那么所谓的第一个应用程序就是展示她的数据绑定功能，操作流程如下：
1、创建一个HTML文件
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

</body>
</html>
```
2、引入Vue.js
```
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
3、创建一个Vue实例
```
<script type="text/javascript">
    var vm = new Vue({
        el:"#app",
        /*Model：数据*/
        data:{
            message:"hello,vue!"
        }
    });
</script>
```
说明：
- el: '#app'：绑定元素的ID
- data:{message:'Hello Vue!'}：数据对象中有一个名为message的属性，并设置了初始值 Hello Vue！

4、将数据绑定到页面元素
```
<!--view层，模板-->
<div id="app">
    {{message}}
</div>
```
说明：只需要在绑定的元素中使用双花括号将Vue创建的名为message属性包裹起来， 即可实现数据绑定功能， 也就实现了View Model层所需的效果， 是不是和EL表达式非常像?

5、测试
为了能够更直观的体验Vue带来的数据绑定功能， 我们需要在浏览器测试一番， 操作流程如下：
  1、在浏览器上运行第一个Vue应用程序， 进入开发者工具
  2、在控制台输入vm.message=‘HelloWorld’， 然后回车， 你会发现浏览器中显示的内容会直接变成HelloWorld
  此时就可以在控制台直接输入vm.message来修改值， 中间是可以省略data的， 在这个操作中， 我并没有主动操作DOM， 就让页面的内容发生了变化， 这就是借助了Vue的数据绑定功能实现的； MV VM模式中要求View Model层就是使用观察者模式来实现数据的监听与绑定， 以做到数据与视图的快速响应。

## 基础语法指令
### v-text
v-text指令（相当于原生js中的innerText）
用于将数据填充到标签中，作用于插值表达式类似，但是没有闪动问题 （如果数据中有HTML标签会将html标签一并输出 ）

注意：此处为单向绑定，数据对象上的值改变，插值会发生变化；但是当插值发生变化并不会影响数据对象的值
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>v-text指令</title>
</head>

<body>
    <div id="app">
        <h2 v-text="message+'!'">深圳</h2>
        <h2 v-text="info+'!'">深圳</h2>
        <h2>{{ message +'!'}}深圳</h2>
    </div>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                message:"测试!!!",
                info:"前端与移动教研部"
            }
        })
    </script>
</body>

</html>
```
### v-html
v-html指令(相当于原生js中的innerHTML)
用法和v-text 相似 但是它可以将HTML片段填充到标签中

可能有安全问题, 一般只在可信任内容上使用 v-html，永不用在用户提交的内容上

它与v-text区别在于v-text输出的是纯文本，浏览器不会对其再进行html解析，但v-html会将其当html标签解析后输出。
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>v-html指令</title>
</head>

<body>
    <div id="app">
		<p>{{message}}</p> 
		<p v-text="message"></p>
		<p v-html="message"></p>
	</div>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                message: "<span>通过双括号绑定</span>"
            }
        })
    </script>
</body>

</html>
```
### v-on
v-on监听事件
事件有Vue的事件、和前端页面本身的一些事件!我们这里的click是vue的事件， 可以绑定到Vue中的methods中的方法事件!
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>v-on补充</title>
</head>

<body>
    <div id="app">
        <input type="button" value="点击" v-on:click="doIt(666,'老铁')">
        <input type="text" v-on:keyup.enter="sayHi">
    </div>
    <!-- 1.开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            methods: {
                doIt:function(p1,p2){
                    console.log("做it");
                    console.log(p1);
                    console.log(p2);
                },
                sayHi:function(){
                    alert("吃了没");
                }
            },
        })
    </script>
</body>

</html>
```
### v-bind
我们已经成功创建了第一个Vue应用!看起来这跟渲染一个字符串模板非常类似， 但是Vue在背后做了大量工作。现在数据和DOM已经被建立了关联， 所有东西都是响应式的。我们在控制台操作对象属性，界面可以实时更新!
  我们还可以使用v-bind来绑定元素特性!
```
<!DOCTYPE html>
<html lang="en">

	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title>v-bind指令</title>
		<style>
			.active {
				border: 1px solid red;
			}
		</style>
	</head>

	<body>
		<div id="app">
			<span v-bind:title="message" v-bind:class="active">
			    鼠标悬停几秒钟查看此处动态绑定的提示信息！
			  </span>
		</div>
		<!-- 开发环境版本，包含了有帮助的命令行警告 -->
		<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
		<script>
			var app = new Vue({
				el: "#app",
				/*Model：数据*/
				data: {
					message: '页面加载于 ' + new Date().toLocaleString()
				}
			})
		</script>
	</body>

</html>
```
你看到的v-bind等被称为指令。指令带有前缀v以表示它们是Vue提供的特殊特性。可能你已经猜到了， 它们会在渲染的DOM上应用特殊的响应式行为在这里，该指令的意思是：“将这个元素节点的title特性和Vue实例的message属性保持一致”。
  如果你再次打开浏览器的JavaScript控制台， 输入app， message=‘新消息’，就会再一次看到这个绑定了title特性的HTML已经进行了更新。

### v-show
v-show 指令通过改变元素的 css 属性（display）来决定元素是显示还是隐藏。
```
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<meta http-equiv="X-UA-Compatible" content="ie=edge" />
		<title>v-show指令</title>
	</head>
	<body>
		<div id="app">
			<input type="button" value="切换显示状态" @click="changeIsShow">
			<input type="button" value="累加年龄" @click="addAge">
			<span>liumou</span>
			<span v-show="isShow">{{age}}</span>

		</div>
		<!-- 1.开发环境版本，包含了有帮助的命令行警告 -->
		<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
		<script>
			var app = new Vue({
				el: "#app",
				data: {
					isShow: false,
					age: 17
				},
				methods: {
					changeIsShow: function() {
						this.isShow = !this.isShow;
					},
					addAge: function() {
						this.age++;
					}
				},
			})
		</script>
	</body>
</html>
```
### v-if， v-else
什么是条件判断语句，就不需要我说明了吧，以下两个属性!

- v-if
- v-else
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>v-if指令</title>
</head>
<body>
    <div id="app">
        <input type="button" value="切换显示" @click="toggleIsShow">
        <p v-if="isShow">测试</p>
        <p v-show="isShow">测试 - v-show修饰</p>
        <h2 v-if="temperature>=35">热死啦</h2>
    </div>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                isShow:false,
                temperature:20
            },
            methods: {
                toggleIsShow:function(){
                    this.isShow = !this.isShow;
                }
            },
        })
    </script>
</body>

</html>
```
测试：
1.在浏览器上运行，打开控制台!
2.在控制台输入app.isShow=false然后回车，你会发现浏览器中显示的内容会直接变成NO
  注：使用v-*属性绑定数据是不需要双花括号包裹的

### v-else-if

- v-if
- v-else-if
- v-else

注：
v-show 指令的功能与 v-if 指令相似。不过 v-if 指令会根据表达式重建或销毁元素或组件以及它们所绑定的事件。v-show 指令只是简单地设置 css 属性。
因为 v-if 指令开销较大，所以更适合条件不经常改变的场景。而 v-show 指令适合条件频繁切换的场景。

### v-for
- v-for
格式说明
```
<div id="app">
    <li v-for="(item,index) in items">
        {{item.message}}---{{index}}
    </li>

</div>
```
注：items是数组，item是数组元素迭代的别名。我们之后学习的Thymeleaf模板引擎的语法和这个十分的相似！
  上代码：
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>v-for指令</title>
</head>

<body>
    <div id="app">
        <input type="button" value="添加数据" @click="add">
        <input type="button" value="移除数据" @click="remove">

        <ul>
            <li v-for="(it,index) in arr">
                {{ index+1 }}测试:{{ it }}
            </li>
        </ul>
        <h2 v-for="item in vegetables" v-bind:title="item.name">
            {{ item.name }}
        </h2>
    </div>
    <!-- 1.开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                arr:["北京","上海","广州","深圳"],
                vegetables:[
                    {name:"西兰花炒蛋"},
                    {name:"蛋炒西蓝花"}
                ]
            },
            methods: {
                add:function(){
                    this.vegetables.push({ name:"花菜炒蛋" });
                },
                remove:function(){
                    this.vegetables.shift();
                }
            },
        })
    </script>
</body>

</html>
```
## 表单双绑、组件
### 什么是双向数据绑定
Vue.js是一个MV VM框架， 即数据双向绑定， 即当数据发生变化的时候， 视图也就发生变化， 当视图发生变化的时候，数据也会跟着同步变化。这也算是Vue.js的精髓之处了。
  值得注意的是，我们所说的数据双向绑定，一定是对于UI控件来说的非UI控件不会涉及到数据双向绑定。单向数据绑定是使用状态管理工具的前提。如果我们使用vue x那么数据流也是单项的，这时就会和双向数据绑定有冲突。

### 为什么要实现数据的双向绑定
在Vue.js中，如果使用vuex， 实际上数据还是单向的， 之所以说是数据双向绑定，这是用的UI控件来说， 对于我们处理表单， Vue.js的双向数据绑定用起来就特别舒服了。即两者并不互斥，在全局性数据流使用单项，方便跟踪；局部性数据流使用双向，简单易操作。
### 在表单中使用双向数据绑定
你可以用v-model指令在表单、及元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇， 但v-model本质上不过是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。
  注意：v-model会忽略所有表单元素的value、checked、selected特性的初始值而总是将Vue实例的数据作为数据来源。你应该通过JavaScript在组件的data选项中声明初始值!
### v-model
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>v-model指令</title>
</head>

<body>
    <div id="app">
        <input type="button" value="修改message" @click="setM">
        <input type="text" v-model="message" @keyup.enter="getM">
        <h2>{{ message }}</h2>
		 <h2 v-text="message">{{ message }}</h2>
    </div>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app = new Vue({
            el:"#app",
            data:{
                message:"测试"
            },
            methods: {
                getM:function(){
                    alert(this.message);
                },
                setM:function(){
                    this.message ="酷丁鱼";
                }
            },
        })
    </script>
</body>

</html>
```

## 什么是组件
组件是可复用的Vue实例， 说白了就是一组可以重复使用的模板， 跟JSTL的自定义标签、Thymeleal的th:fragment等框架有着异曲同工之妙，通常一个应用会以一棵嵌套的组件树的形式来组织：
### 第一个Vue组件
注意：在实际开发中，我们并不会用以下方式开发组件，而是采用vue-cli创建，vue模板文件的方式开发，以下方法只是为了让大家理解什么是组件。
  使用Vue.component()方法注册组件，格式如下：
```
<div id="app">
  <pan></pan>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script type="text/javascript">
    //先注册组件
    Vue.component("pan",{
        
        template:'<li>Hello</li>'

    });
    //再实例化Vue
    var vm = new Vue({
        el:"#app",
    });
</script>

```
说明：

- Vue.component()：注册组件
- pan：自定义组件的名字
- template：组件的模板

### 使用props属性传递参数
像上面那样用组件没有任何意义，所以我们是需要传递参数到组件的，此时就需要使用props属性了！
  注意：默认规则下props属性里的值不能为大写；
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<div id="app">
    <!--组件：传递给组件中的值：props-->
  <pan v-for="item in items" v-bind:panh="item"></pan>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.min.js"></script>
<script type="text/javascript">
    //定义组件
    Vue.component("pan",{
        props:['panh'],
        template:'<li>{{panh}}</li>'

    });
    var vm = new Vue({
        el:"#app",
        data:{
            items:["java","Linux","前端"]
        }
    });
</script>
</body>
</html>
```
说明：

v-for="item in items"：遍历Vue实例中定义的名为items的数组，并创建同等数量的组件
v-bind:panh="item"：将遍历的item项绑定到组件中props定义名为item属性上；= 号左边的panh为props定义的属性名，右边的为item in items 中遍历的item项的值

## Axios异步通信
### 什么是Axios
Axios是一个开源的可以用在浏览器端和Node JS的异步通信框架， 她的主要作用就是实现AJAX异步通信，其功能特点如下：
- 从浏览器中创建XMLHttpRequests
- 从node.js创建http请求
- 支持Promise API[JS中链式编程]
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防御XSRF(跨站请求伪造)
GitHub：https://github.com/axios/axios
中文文档：http://www.axios-js.com/

### 为什么要使用Axios
由于Vue.js是一个视图层框架并且作者(尤雨溪) 严格准守SoC(关注度分离原则)所以Vue.js并不包含AJAX的通信功能， 为了解决通信问题， 作者单独开发了一个名为vue-resource的插件， 不过在进入2.0版本以后停止了对该插件的维护并推荐了Axios框架。少用jQuery， 因为它操作Dom太频繁!

### 第一个Axios应用程序
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>axios+vue</title>
</head>

<body>
    <div id="app">
        <input type="button" value="获取笑话" @click="getJoke">
        <p> {{ joke }}</p>
    </div>
    <!-- 官网提供的 axios 在线地址 -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        /*
            接口:随机获取一条笑话
            请求地址:https://autumnfish.cn/api/joke
            请求方法:get
            请求参数:无
            响应内容:随机笑话
        */
        var app = new Vue({
            el:"#app",
            data:{
                joke:"很好笑的笑话"
            },
            methods: {
                getJoke:function(){
                    // console.log(this.joke);
                    var that = this;
                    axios.get("https://autumnfish.cn/api/joke").then(function(response){
                        // console.log(response)
                        console.log(response.data);
                        // console.log(this.joke);
                        that.joke = response.data;
                    },function (err) {  })
                }
            },
        })

    </script>
</body>

</html>
```