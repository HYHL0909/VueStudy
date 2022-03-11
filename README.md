# VueStudy 
## day01 vue小实例 
### 第一次提交
首先进入vue官网加载vue.js文件，将其添加到项目内。<br/>利用script在head里引入，这样子能够防止抖屏。<br/>新创建的vue对象也需要在script中。
### 第二次提交
挂载点，模板，实例之间的关系
el所指向的标签就是vue对象的挂载点，实例只会处理挂载点下的内容<br/>
模板：挂载点里的内容都叫模板；模板可以放在挂载点里，也可以放在vue对象的template里。<br/>
放在对象的模板里的优先级更高.
### 第三次提交 数据，事件，和方法
{{插值}}
v-text和v-html都可以显示，但是text会进行转义，而html不会进行转义，会当作html代码执行。<br/>
- 给模板上的标签绑定事件，比如点击标签后内容发生改变<br/>
  v-on:click="函数"，函数定义在vue对象的methods属性里，修改内容的方法直接修改this.msg<br/>
  
### 第4次提交，模板指令实现属性绑定
div在title里可以用模板指令 `v-bind :title ="title"`,在模板指令中的字符串已经不再是字符串而是js的表达式 ` v-bind: `缩写成`:` <br/>

- 单向绑定：数据可以改变页面里的内容，页面里的改变不了数据中的内容 `:value="number"`
- 双向数据绑定 
双向绑定 input可以双向绑定，`v-model:value="number"`中修改number的值那么value的值会改变，而修改value，number的值也会改变。
