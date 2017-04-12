# 在vue.js的海洋中蒙蔽(一)

> *今天只搞了两个玩意儿，不说精通，可能理解到了，不过还是将自己的感受写出来比较好。*

### 1.vue.js中的父作用域的值传递到子组件

首先贴上代码：

Html:

	<div id="app-7">
		<ol>
			<!-- item是定义的一个变量 然后将这个变量bind在了一个叫todo的变量上-->
			<todo-item v-for="item in todos" v-bind:todo="item"></todo-item>
		</ol>
	</div>
js:

``````
Vue.component('todo-item',{
	props:['todo'],
	template:'<li>{{todo.text}}</li>'
})
var app7 = new Vue({
	el:'#app-7',
	data:{
      	todos:[{text:'desk1'},{text:'desk2'},{text:'desk3'}]
	}
})
``````

运行的结果：

``````
1.desk1
2.dest2
3.desk3
``````

其中‘todo-item’是个自定义组件，item是一个临时变量，而这个变量通过 **v-bind** 绑定在了另一个变量todo上，夫元素app7中的数组就是通过这个todo变量赋值到自定义变量template中的。



###  2.vue.js中的filter

首先先温习几个js常见的函数

> charAt(index):参数：index；可返回指定位置的字符。
>
> slice(start,end):参数：start是必须参数规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。end可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。

先给这俩函数举两个例子

``````
var str = "hello world";
str.charAt(0);    //输出 h
str.slice(0);     //输出 hello world
str.slice(0,5)    //输出 hello
str.slice(-1)     //输出 d
``````

然后继续filter，官方给的文档是：

> *Vue.filter( id, [definition] )*
>
> *参数：*
>
> *{string} id*
> *{Function} [definition]*
> *用法：*
>
> *注册或获取全局过滤器。*
>
> *// 注册*
> *Vue.filter('my-filter', function (value) {*
> *// 返回处理后的值*
> *})*
> *// getter，返回已注册的过滤器*
> *var myFilter = Vue.filter('my-filter')*

所以马上上代码：

html:

``````
<div id="app-8">{{message|strtoup}}</div>
``````

js:

``````
//参考官方文档
//将字符串首字母大写
Vue.filter('strtoup',function(value){
  	//首先判断value是否存在
  	if(value){
  		//将value转换为字符串
      	var str = value.toString();
      	return str.charAt(0).toUpperCase()+str.slice(1);
  	}else{
  		//value不存在返回''
      	return '';
  	}
})

//然后实例化
var app8 = new Vue({
  	el: "#app-8",
  	data: {
      	message: 'hello vue!'
  	}
})
``````

运行之后：

> Hello vue!

