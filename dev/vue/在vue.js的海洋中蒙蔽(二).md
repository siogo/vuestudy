# 在vue.js的海洋中蒙蔽(二)

### 计算属性

在模板中绑定表达式是非常便利的，但是它们实际上只用于简单的操作。在模板中放入太多的逻辑会让模板过重且难以维护。

##### 简单例子:

html:

``````
<div id='app-10'>
	<p>{{message}}</p>
    <p>changed message{{changedmessage}}</p>
</div>
``````

js:

``````
var app10 = new Vue({
  	el: '#app-10',
  	data:{
      	message:'hello vue'
  	},
  	computed:{
      	changedmessage:function(){
          	return this.message.split('').reverse().join('');
      	}
  	}
})
``````

返回的结果是：

> hello vue
>
> euv olleh

### Method vs 计算属性

当看到 *computed* 和 *method* 使用起来差不多的时候，会感觉这个属性和 *method* 并没有什么区别，继续看代码

``````
//我们将这个程序改造一下，看看有什么区别
<div id='app-10'>
	<p>{{message}}</p>
	//这是计算属性改变后的值
    <p>changed message：{{changedmessage}}</p>
    //这是Method改变后的值，ps：大括号中是函数调用
    <p>method message：{{methodmessage()}}</p>
</div>

var app10 = new Vue({
  	el: '#app-10',
  	data:{
      	message:'hello vue'
  	},
  	//计算属性方法
  	computed:{
      	changedmessage:function(){
          	return this.message.split('').reverse().join('');
      	}
  	}
  	//method方法
  	//单词是methods
  	methods:{
      	methodmessage:function(){
          	return this.message.split('').reverse().join('');
      	}
  	}
})
``````

运行结果：

> changed message：euv olleh
>
> method message：euv olleh

说明在一定程度上 *method* 和 *computed* 是一样的，然后在改动一下代码

``````
//in component
	//计算属性方法
  	computed:{
      	changedmessage:function(){
          	return Date.now();
      	}
  	}
  	//method方法
  	//单词是methods
  	methods:{
      	methodmessage:function(){
          	return Date.now();
      	}
  	}
``````

然后在chrome中console命令

``````
>app10.changedmessage
<1489498314075
//再次调用
>app10.changedmessage
<1489498314075

//调用method方法
>app10.methodmessage()
<1489498639685
//再次调用
>app10.methodmessage()
<1489498676609
``````

所以**computed**是只执行一次然后存入缓存，多次调用也只会调用缓存的值，而**method**是每次都会执行，多次调用就多次执行，对于有很大的计算量的，应当用**computed**。

