---

---

# VueStudy 

减少了DOM操作，只需要修改vue实例里面的数据。面向数据编程。

当一个 Vue 实例被创建时，它将 `data` 对象中的所有的 property 加入到 Vue 的**响应式系统**中。当这些 property 的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

## 一、Vue的基础语法
### 第一次提交
首先进入vue官网加载vue.js文件,开发版本，将其添加到项目内。<br/>

![image-20220404233412815](C:\Users\Elvira\AppData\Roaming\Typora\typora-user-images\image-20220404233412815.png)

利用script在head里引入，这样子能够防止抖屏。<br/>新创建的vue对象也需要在script中。

~~~html
<head>
    <script src='./vue.js'></script>
</head>
<body>
    <div id='root'>
        {{msg}}
    </div>
    <script>
        new Vue({
            el:"#root",
            data:{
                msg:"hello world"
            }
        })
    </script>
</body>
~~~

或者通过cdn引入

~~~html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
~~~



### 第二次提交：挂载点，模板，实例之间的关系

el所指向的标签就是vue对象的挂载点，实例只会处理挂载点下(包括孙子元素，只要在挂载点里，都能用data的内容<br/>

~~~html
<head>
    <script src='./vue.js'></script>
</head>
<body>
    <div id='root'>
       <h1>
            {{msg}}  可以用
        </h1>
    </div>
    <div>
        
    {{msg}} 不可用
    </div>
    <script>
        new Vue({
            el:"#root",
            data:{
                msg:"hello world"
            }
        })
    </script>
</body>
~~~

模板：挂载点里的内容都叫模板；模板可以放在挂载点里，也可以放在vue对象的template里。<br/>
放在对象的模板里的优先级更高.

~~~html
<head>
    <script src='./vue.js'></script>
</head>
<body>
    <div id='root'>

    </div>
    <div>
        
    {{msg}} 不可用
    </div>
    <script>
        new Vue({
            el:"#root",
            <!--   根据template和data构造一个dom，然后挂载el上-->
            template:"  <h1>{{msg}}  </h1>"
            data:{
                msg:"hello world"
            }
        })
    </script>
</body>
~~~



### 第三次提交 数据，事件，和方法
<<<<<<< HEAD
1. 数据：

   - {{插值表达式}}  

   - v-text和v-html都可以显示，但是text会进行转义，而html不会进行转义，会当作html代码执行，会加粗。<br/>

     ~~~html
     <div v-text='content'>
         
     </div>
     ~~~

2. 给模板上的标签绑定事件，比如点击标签后内容发生改变<br/>
   v-on:click="函数"，函数定义在vue对象的methods属性里，修改内容的方法直接修改this.content<br/>

   

   ~~~html
   <head>
       <script src='./vue.js'></script>
   </head>
   <body>
       <div id='root'>
          
           <div v-on:click="handleClick">
               {{content}}
           </div>
            <!--v-on:@-->
           <div @click="handleClick">
               {{content}}
           </div>
   
       </div>
   
       <script>
           new Vue({
               el:"#root",
               data:{
                   content:"hello world"
               },
               methods:{
                   handleClick:function(){
                       this.content='world';
                   }
               }
           })
       </script>
   </body>
   ~~~

   

### 第四次提交：属性绑定和双向数据绑定

1. 属性绑定 v-bind

   Mustache 语法不能作用在 HTML attribute 上，遇到这种情况应该使用 [`v-bind` 指令]  缩写：

   ~~~html
   <head>
       <script src='./vue.js'></script>
   </head>
   <body>
       <div id='root'>
           <!--上面显示的是title字符串-->
           <div title="title">hello world</div>
           
            <!--上面显示的是title里的内容，它指的的是vue实例中的title-->
            <div v-bind:title="title">hello world</div>
           <div :title="title">hello world</div>
           
       </div>
   
       <script>
           new Vue({
               el:"#root",
               data:{
                   title:"hello world"
               }
           })
       </script>
   </body>
   ~~~

   

2. 双向属性绑定。

   单向是，data决定页面的显示。

   v-model 实现表单数据的双向绑定，可以理解为直接修改了对象里的data。

   ~~~html
   <head>
       <script src='./vue.js'></script>
   </head>
   <body>
       <div id='root'>
           <div :title="title">hello world</div>
           
           <input v-model="content"/>
           <div>
               {{content}}
           </div>
           
       </div>
   
       <script>
           new Vue({
               el:"#root",
               data:{
                   title:"hello world",
                   content:"this is content"
               }
           })
       </script>
   </body>
   ~~~

   

### 第五次提交：计算属性和侦听器

1. 计算属性

   一个属性通过其他两个及以上属性计算而成。

   有个好处是如果实例内的属性值均没有改变的话，那么这个属性只会到缓存中寻找不会重新计算。但是一旦，实例内的属性值发生了改变，则会重新计算，此时包括着非实例内的属性一起计算。监听实例内的属性。

2. 侦听watch，修改次数等，就是计数器。

   一般是一个变量

   ~~~html
   <body>  
       <div id="root">
           姓：<input v-model="firstName"/>
           名：<input v-model="lastName"/>
           <div>{{fullName}}</div>
           <div>
               {{count}}
           </div>
         
    
         </div>
       <script>
           new Vue({
               el:"#root",
               data:{
                   firstName:"",
                   lastName:'',
                   count:0
   
               },
               computed:{
                   fullName:function(){
                       return this.firstName+" "+this.lastName;
                   }
               },
               /*监听fullName变量*/
               watch:{
                   fullName:function(){
                       this.count++;
                   }
               }
    
           })
       </script>
   </body>
   ~~~

   



### 第六次提交：（条件渲染）v-if，v-show，与（列表渲染）v-for指令

1. v-if 为false的时候，会直接将该节点从dom树上删除。如果很频繁，使用这种方法是很不合理的，要一直创建dom树。

   v-else-if  v-else

   v-show为false的时候，会给该节点添加display：none，这个节点依然没有删除。

   ~~~html
   <body>  
       <div id="root">
         <div v-if="seen">hello world!</div>
          <!--可有可无-->
           <div v-else>
               hello Vue!
           </div>
         <div v-show="seen">hello Vue</div>
         <button @click="switcher">toggle</button>
   
       </div> 
       <script>
           new Vue({
               el:"#root",
               data:{
                   seen:true,     
               },
               methods:{
                   switcher:function(){
                       this.seen = !this.seen;
                   }
               }
           })
       </script>
   </body>
   ~~~

2. v-for :循环显示

   ~~~html
   <body>  
       <div id="root">
         <ol>
             <li v-for="item of list" >{{item}}</li>
         </ol>
   
       </div> 
       <script>
           new Vue({
               el:"#root",
               data:{
                   list:['apple','banana','orange']
               },
   
           })
       </script>
   </body>
   ~~~

     ~~~html
     <!--循环打印对象内容-->
      <div v-for="item of list" >
       <div v-if="item.age>20">
           {{item.age}}
          </div>   </div>
     ~~~

   

## 二、 Vue中的组件

### 1. todolist功能开发

点击提交，将内容显示在`li`里面。

~~~html
<div id="root">
        <div>
            <input v-model="inputValue">
            <button @click="add">submit</button>
        </div>
        <ul>
            <li v-for="(item,key) of list" :key="index">{{item}}</li>
        </ul>
    </div> 
    <script>
        new Vue({
            el:"#root",
            data:{
                inputValue:"",
                list:[]
            },
            methods:{
                add:function(){
                    this.list.push(this.inputValue);
                    this.inputValue='';
                  
                }
            }
        })
    </script>
~~~



### 2.todolist组件拆分

组件就是页面里的部分。组件拆分的原则就是要复用性高

组件的定义与组件之间的通信。

全局组件：哪里都能用。局部组件只能在部分。

~~~html
<div id="root">
        <div>
            <input v-model="inputValue">
            <button @click="add">submit</button>
        </div>
        <ul>
            <todo-item v-for='item of list'
            :content="item" ></todo-item>

        </ul>
    </div> 
    <script>
        /*全局组件，它们在注册之后可以用在任何新创建的 Vue 根实例 (new Vue) 的模板中,props用于接受来自todo-item里面的content，父组件Vue，通过属性传递的方式，向子组件传递值*/
        Vue.component('todo-item',{
            props:['content'],
            template: '<li>{{content}}</li>' 
        })
        
        new Vue({
            el:"#root",
            data:{
                inputValue:"",
                list:[]
            },
            methods:{
                add:function(){
                    this.list.push(this.inputValue);
                    this.inputValue='';
                  
                }
            }
        })
    </script>
~~~

~~~html
<div id="root">
        <div>
            <input v-model="inputValue">
            <button @click="add">submit</button>
        </div>
        <ul>
            <todo-item v-for='item of list'
                       :content='item'></todo-item>

        </ul>
    </div> 
    <script>    
        /*你可以通过一个普通的 JavaScript 对象来定义组件：*/
        var TodoItem={
            props:['content'],
            template:'<li>{{content}}</li>'
        }
        new Vue({
            el:"#root",
            /*然后在 components 选项中定义你想要使用的组件，如果没有定义则使用不了，因为局部注册的组件在其子组件中不可用*/
            components:{ 'todo-item': TodoItem
        },
            
            
            data:{
                inputValue:"",
                list:[]
            },
            methods:{
                add:function(){
                    this.list.push(this.inputValue);
                    this.inputValue='';
                  
                }
            }
        })
    </script>
~~~

### 3.组件和实例的关系

组件本身也是一个vue实例。

Vue实例的模板是挂载在实例下的dom里的所有内容。

### 4.实现todolist的删除功能。

==父子组件交互。==

添加，是在父组件中添加，然后将值传递给子组件，让子组件显示。

props用于接受来自todo-item里面的content，父组件Vue，通过属性传递的方式，向子组件传递值。所有的 prop 都使得其父子 prop 之间形成了一个**单向下行绑定**：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外变更父级组件的状态，从而导致你的应用的数据流向难以理解。

删除，比如点击删除，是在子组件里点击触发事件名，然后父组件监听到事件名被触发，然后父组件点击事件将父组件中渲染子组件的那条数据删除。

因此最重要的就是让父组件和子组件进行通信。

~~~html
<div id="root">
        <div>
            <input v-model="inputValue">
            <button @click="add">submit</button>
        </div>
        <ul>
            <todo-item v-for='(item,index) of list'
            :content="item"
            :key="index"
            :index="index" 
            @delete="handleDelete"></todo-item>
<!--父组件监听子组件是否有-->
        </ul>
    </div> 
    <script>
        Vue.component('todo-item',{
            props:['content','index'],
            template: '<li @click="handleClick">{{content}}</li>' ,
            methods:{
                handleClick:function(){
                    /*组件被点击会触发一个事件，事件叫delete，会传递this.index这个值*/
                    this.$emit('delete',this.index)

                }
            }
        })
        
        new Vue({
            el:"#root",
            data:{
                inputValue:"",
                list:[]
            },
            methods:{
                add:function(){
                    this.list.push(this.inputValue);
                    this.inputValue='';
                  
                },
                handleDelete:function(index){
                    this.list.splice(index,1);

                }
            }
        })
    </script>
~~~

## 三、 Vue-cli的简介与使用

Vue-cli自带webpack的

安装vue-cli

~~~npm
npm i -g vue-cli
vue init webpack my-project
cd my-project
npm run dev
~~~

主要是编写src的代码。

main.js

![image-20220404210259369](C:\Users\Elvira\AppData\Roaming\Typora\typora-user-images\image-20220404210259369.png)

主要的Vue

~~~vue
<template>
</template>
<script>
   export default {
       /*导入子组件*/
       import TodoItem from './components/TodoItem.vue'
       components:{
           /*子组件*/
       },
       data () {
           return {}
       },
       method : {
           
       }
   } 
</script>
<style>
</style>
~~~

利用vue-cli实现todolist。

缕一缕

![image-20220404211407940](C:\Users\Elvira\AppData\Roaming\Typora\typora-user-images\image-20220404211407940.png)

首先父组件的模板是：

~~~vue
<div>
  <div>
    <input >
    <button >submit</button>
  </div>
  <ul>
    <todo-item ></todo-item>
  </ul>
</div>
~~~

input的v-model inputValue，因为要双向绑定啊，相当于直接修改在父组件里的数据  inputValue

然后点击button时inputValue传递到list中。

然后显示list的东西，此时已经将li看成子组件。

父组件要使用子组件，要import，要定义components

然后父组件要把list上的数据传递给子组件，通过属性绑定。

：content=’item‘，然后子组件要利用props接受

。如果要通过点击子组件删除数据。

要在子组件绑定click事件，然后事件触发$emit发送函数 名和参数给父组件

父组件在子组件上绑定了监听事件，一旦监听到子组件发送，就调用删除元素的函数。





style scoped

局部样式，局部有效，这样很好，因为这样最大程度的保持了各个组件之间的解耦
=======
{{插值}}
v-text和v-html都可以显示，但是text会进行转义，而html不会进行转义，会当作html代码执行。<br/>
- 给模板上的标签绑定事件，比如点击标签后内容发生改变<br/>
  v-on:click="函数"，函数定义在vue对象的methods属性里，修改内容的方法直接修改this.msg<br/>
  
### 第4次提交，模板指令实现属性绑定
div在title里可以用模板指令 `v-bind :title ="title"`,在模板指令中的字符串已经不再是字符串而是js的表达式 ` v-bind: `缩写成`:` <br/>

- 单向绑定：数据可以改变页面里的内容，页面里的改变不了数据中的内容 `:value="number"`
- 双向数据绑定 
双向绑定 input可以双向绑定，`v-model:value="number"`中修改number的值那么value的值会改变，而修改value，number的值也会改变。
>>>>>>> 5991e4cd9284e2ec841fa6d38d987cabf479dfd4
