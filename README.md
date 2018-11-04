# Vue(读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架,只关注视图层， 采用自底向上增量开发的设计,其目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件。
# 一、vue 起步
    1、创建一个.html文件
    2、引包；（从官网下载 vue.min.js 通过 <script> 标签引入/使用 CDN 方法/npm命令行）；
    3、留坑<div id="app"></div> 这里id也可以起其他名，与new Vue()实例中的配置对象中el相同
    4、启动vue，通过new Vue({el:'目的地',template:'模板',data: function(){return {要使用的key: 数据}} }})；
    5、配置options选项对象；页面中存在的该目的地，目的地字符串描述，同jQuery方式相同；
话不多说直接上代码：

    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Vue.js</title>
      <!-- 2、引包 -->
      <script src="https://unpkg.com/vue/dist/vue.js"></script>
    </head>
    <body><!-- 3、留坑 -->
      <div id="app"></div>
      <script>
        // 4、创建Vue的对象，并把数据绑定到上面创建好的div上去。
        // 5、配置option
        new Vue({
          //el: '#app', 在Vue内部运行机制中，需要根据你传递的字符串进行判断，如：'#app'/'.XXX'/'div'.....等等(占据内存)
          // el: document.getElementById('app'),//el:发生行为的目的地，更为优化，将元素直接找到，也可以用标签名、类名
          template: '<div><h2>Hello Vue.js！{{text}}</h2></div>',//装载模板
            data: function(){
              return {
                  text : '我是你要绑定得数据'//template 中用到的数据
              }
            }
        })
    </script>
    </body>
    </html> 
 运行结果如下图：
 <img src="https://github.com/sophianbj/Vue.js-learning/blob/master/asset/1-1.png" alt="运行结果">   
        
    Hello Vue.js！我是你要绑定得数据

# 二、指令（以v-xxx表示的特殊属性）
# 在Vue中提供了一些对于页面+数据的更为方便的操作，这些操作叫做指令。指令封装了一些Dom行为（在表达式的值改变时）

# 常用的指令：
1、v-html：相当于JavaScript的innerHTML属性。
2、v-text：相当于JavaScript的innerText属性，主要用来更新textContent。
    
    注意：v-html和v-text指令只要存在与标签中，那么该标签内部其他内容便不会显示，
    <div v-html="txt_html">444<p>123{{txt_html}}</p></div>，div中的内容仅显示txt_html数据中的内容。
    <div v-text="txt"></div> <====> <div>{{txt}}</div>

3、v-if(v-else-if,v-else)：条件渲染。是否插入元素，v-if系列指令的使用，必须是相邻的DOM元素。如：<div v-if="flag"></div>中flag为true，则      渲染，否则，便不会渲染这个元素；
4、v-show：是否隐藏元素，和v-if不同的是，若v-if的值为false，那么该元素被销毁，不在dom中。而v-show则是对于css中         display值的改变"none"/"block"；

    v-if和v-show的异同：
    相同点：都是通过属性值的真假动态控制元素的显示与隐藏；
    不同点：v-if将整个dom元素移除或添加（类似于removeChild()，appendChild()方法，高度切换场景下更消耗性能）；
    v-show切换css中的display值“none”和“block”而dom元素一直存在于页面中。
5、v-for：列表渲染，对一组数组的选项列表进行遍历渲染。<ul><li v-for="(item,index) in list">{{index}},{{item}}</li></ul>其中index表示选项索引，item选项内容，这里的in也可以换成of，list可以是object也可以是array；
6、v-bind：属性绑定，动态地绑定一个或者多个特性，或一个组件 prop 到表达式。常用于动态绑定class和style，以及href等。在绑定 class或style特性时，支持其它类型的值，如数组或对象。当内存中的值发生改变时会触发重新渲染。简写为:属性名="属性值" <div v-bind:原属性名="变量"></div>☜☜☞☞<div :属性名="变量"></div>。
7、v-model：双向数据绑定。双向数据流 v-model="变量" 当元素的value值被改变以后，就会给Vue中的属性赋值
   v-model 只能给具备value属性的元素进行双向数据绑定（必须使用的是有value属性的元素）。（Vue☞☞页面☞☞Vue）
8、v-bind 可以给任何属性赋值，是从Vue到页面的单向数据流。（Vue☞☞页面）
9、v-on：事件绑定。<div v-on:原生事件名="对变量进行操作||表达式/函数名"></div>☜☜☞☞<div @原生事件名="对变量进行操作||表达式/函数名"></div>
10、v-once：关联的实例，只会渲染一次。之后的重新渲染，实例极其所有的子节点将被视为静态内容跳过，这可以用于优化更新性能。
11、v-pre：主要用来跳过这个元素和它的子元素编译过程。可以用来显示原始的Mustache标签。跳过大量没有指令的节点加快编译。<div v-pre>{{msg}}</div>//这个标签以及字节点会直接跳过。
12、v-cloak：指令是用来保持在元素上直到关联实例结束时进行编译。
接下来我们step by step 上代码
