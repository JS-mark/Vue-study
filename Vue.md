# Vue 框架
- {{}} 这种语法叫做“Mustache”语法 (双大括号)
- 1.数据驱动页面的改变，数据改变，页面也改变，这vue的特性
- 2.我们向vue对象中传递的参数，被vue内部直接挂载到了vue对象中，所以当你使用this时，this虽然指向的是vue对象，但是因为我们传递进去的参数都已经被挂载到了对象上，所以我们是可以使用对象.你自己定义的属性名去获取；
- 3.vue 内置方法和属性前面都带一个$
- 一、语法
  - 1.{{变量}}插值运算符，undefined以及null在插值表达式中展现不了,其他数据类型都可以转换，但是都是转换成字符串，展现在页面上
    - 可以在插值表达式中放置js语法；
    - 只能使用不改变原数组的方法
    - 插值表达式，在先加载html结构时，会暴露插值表达式语法（当然处于网络请求中，本地是不会出现闪现原始语法的效果）；而使用v-text时不会出现这种情况。因为其内部使用了未加载就隐藏机制；
  - 2.内部指令
    - v-once //用于渲染文本数据，会把任何字符渲染为字符串，然后显示在页面，但是该指令只渲染一次数据，不是数据驱动页面型
    - v-text //用于渲染文本数据，会把任何字符渲染为字符串，然后显示在页面
    - v-html //用于渲染数据含有html代码的数据
    - v-cloak //通常用来防止{{}}表达式闪烁问题；v-cloak指令保持在元素上直到关联实例结束编译后自动移除，v-cloak和 CSS 规则如 [v-cloak] { display：none } 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。
    - v-on:事件名='执行的方法，括号可加可不加' //用于绑定事件
      - 简写@事件名='执行的方法，括号可加可不加' //用于绑定事件
    - v-bind:要绑定的属性名  绑定属性时使用；将data中的数据注入到标签的属性上
      - 想要v-bind直接赋值一个字符串嵌套兑现规定格式，对象的key是属性名，value与vue对象中data中的变量相互对应
      - 要绑定多个属性值，使用数组[]
      - 缩写写法 :要绑定的属性名
  - 3.vue对象参数
    - data 存放数据
    - methods 定义方法
    - el 元素作用域  用于定义在哪个元素中去实例化vue对象(可以使用# . 标签 选择器，但是标签选择器，类选择器，属性选择器，只会选中一个)

  - 4.v-on绑定事件 事件修饰符（修饰符可以连写也叫串联）
    - .stop 阻止事件冒泡
    - .prevent 阻止默认事件
    - .(keycode键盘安检码)
  - 5.Vue.config.keyCodes.自定义键名   自定义按键事件修饰符
  - 6.数据绑定
    - 单项数据绑定：只给其他人赋值，却不能修改自己的
      - v-bind:html原生属性 单项数据绑定，只影响页面，不影响data数据；如果有多个参数 ，可以以数组形式添加
        - v-bind:class="['box','box1']" ; 给某一个标签的class添加两个样式表；（v-bind指令会内部，会去遍历你添加的值，然后在把值附加给属性）当然你也可以存放一个数组变量，或者对象
    - 双向数据绑定：既给别人赋值数据，同时把别人修改的数据更新自己本身
    - v-model（只有value属性的标签才能使用这个指令）双向数据绑定，既影响页面，页面也能影响data数据
    - v-model修饰符（修饰符可以连写也叫串联）
      - .lazy  延迟双向绑定（当光标移除文本框时，才实施双向绑定）
      - .number 把value的值转换成number类型
      - .trim 去除valu    e空格
  - 7.数据遍历语法
    - v-for="自定义变量（代表对象或者数组中的每一项） in data中的要遍历的对象"
    - 操作数组： v-for="(item,index) in arr" v-bind:key="index" key就是利用了这个算法，当你添加了新数据时，可以就至渲染最新数据，之前数据不进行渲染，大大加强了dom操作效率；
      - diff算法vue为了提高数据渲染（dom操作）效率，
    - 操作对象 v-for="(value,key,index)  in obj"
  - 8.v-if=‘一个布尔表达式’用来控制标签的显示隐藏（本质是直接删掉元素）。true显示 false 隐藏 
    - v-else-if="一个布尔表达式"
    - v-else 必须配合v-if来使用
    - v-show=‘一个布尔表达式’ 只能控制单个元素的显示，隐藏；不能控制多个 不支持template包裹标签的使用（本质是动态添加display：none）
  - 9.Vue-DevTools安装使用方法：
    - 在使用插件时，必须使用vue开发版本，才能启用该插件
  - 10.key
~~~
  当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用“就地复用”策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序， 而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。这个类似 Vue 1.x 的 track-by="$index" 。
  
  这个默认的模式是高效的，但是只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出。
  
  为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 key 属性。理想的 key 值是每项都有的且唯一的 id。这个特殊的属性相当于 Vue 1.x 的 track-by ，但它的工作方式类似于一个属性，所以你需要用 v-bind 来绑定动态值 (在这里使用简写)：
  
  <div v-for="item in items" :key="item.id">
    <!-- 内容 -->
  </div>
  建议尽可能在使用 v-for 时提供 key，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。
  
  因为它是 Vue 识别节点的一个通用机制，key 并不与 v-for 特别关联，key 还具有其他用途，我们将在后面的指南中看到其他用途。
~~~
  - 11.数组更新检测
    - 变异方法
      - Vue 包含一组观察数组的变异方法，所以它们也将会触发视图更新。这些方法如下：
          - push()
          - pop()
          - shift()
          - unshift()
          - splice()
          - sort()
          - reverse()
      - 你打开控制台，然后用前面例子的 items 数组调用变异方法：example1.items.push({ message: 'Baz' }) 。
    
    - 替换数组
      - 变异方法 (mutation method)，顾名思义，会改变被这些方法调用的原始数组。相比之下，也有非变异 (non-mutating method) 方法，例如：filter(), concat() 和 slice() 。这些不会改变原始数组，但总是返回一个新数组。当使用非变异方法时，可以用新数组替换旧数组：
~~~
    example1.items = example1.items.filter(function (item) {
      return item.message.match(/Foo/)
    })
~~~
- 你可能认为这将导致 Vue 丢弃现有 DOM 并重新渲染整个列表。幸运的是，事实并非如此。Vue 为了使得 DOM 元素得到最大范围的重用而实现了一些智能的、启发式的方法，所以用一个含有相同元素的数组去替换原来的数组是非常高效的操作。
- 注意事项
  - 由于 JavaScript 的限制，Vue 不能检测以下变动的数组：
    - 当你利用索引直接设置一个项时，例如：vm.items[indexOfItem] = newValue
    - 当你修改数组的长度时，例如：vm.items.length = newLength
    - 为了解决第一类问题，以下两种方式都可以实现和 vm.items[indexOfItem] = newValue 相同的效果，同时也将触发状态更新：
    
    // Vue.set
    Vue.set(example1.items, indexOfItem, newValue)
    // Array.prototype.splice
    example1.items.splice(indexOfItem, 1, newValue)
    为了解决第二类问题，你可以使用 splice：
    
    example1.items.splice(newLength)
    对象更改检测注意事项
    还是由于 JavaScript 的限制，Vue 不能检测对象属性的添加或删除：
    
    var vm = new Vue({
      data: {
        a: 1
      }
    })
    // `vm.a` 现在是响应式的
    
    vm.b = 2
    // `vm.b` 不是响应式的
    对于已经创建的实例，Vue 不能动态添加根级别的响应式属性。但是，可以使用 Vue.set(object, key, value) 方法向嵌套对象添加响应式属性。例如，对于：
    
    var vm = new Vue({
      data: {
        userProfile: {
          name: 'Anika'
        }
      }
    })
    你可以添加一个新的 age 属性到嵌套的 userProfile 对象：
    
    Vue.set(vm.userProfile, 'age', 27)
    你还可以使用 vm.$set 实例方法，它只是全局 Vue.set 的别名：
    
    this.$set(this.userProfile, 'age', 27)
    有时你可能需要为已有对象赋予多个新属性，比如使用 Object.assign() 或 _.extend()。在这种情况下，你应该用两个对象的属性创建一个新的对象。所以，如果你想添加新的响应式属性，不要像这样：
    
    Object.assign(this.userProfile, {
      age: 27,
      favoriteColor: 'Vue Green'
    })
    你应该这样做：
    
    this.userProfile = Object.assign({}, this.userProfile, {
      age: 27,
      favoriteColor: 'Vue Green'
    })
    显示过滤/排序结果
    有时，我们想要显示一个数组的过滤或排序副本，而不实际改变或重置原始数据。在这种情况下，可以创建返回过滤或排序数组的计算属性。
    
    例如：
    
    <li v-for="n in evenNumbers">{{ n }}</li>
    data: {
      numbers: [ 1, 2, 3, 4, 5 ]
    },
    computed: {
      evenNumbers: function () {
        return this.numbers.filter(function (number) {
          return number % 2 === 0
        })
      }
    }
 
    在计算属性不适用的情况下 (例如，在嵌套 v-for 循环中) 你可以使用一个 method 方法：
    
    <li v-for="n in even(numbers)">{{ n }}</li>
    data: {
      numbers: [ 1, 2, 3, 4, 5 ]
    },
    methods: {
      even: function (numbers) {
        return numbers.filter(function (number) {
          return number % 2 === 0
        })
      }
    }
    一段取值范围的 v-for
    v-for 也可以取整数。在这种情况下，它将重复多次模板。
    
    <div>
      <span v-for="n in 10">{{ n }} </span>
    </div>
    结果：
    
    v-for on a <template>
    类似于 v-if，你也可以利用带有 v-for 的 <template> 渲染多个元素。比如：
    
    <ul>
      <template v-for="item in items">
        <li>{{ item.msg }}</li>
        <li class="divider"></li>
      </template>
    </ul>
    v-for with v-if
    当它们处于同一节点，v-for 的优先级比 v-if 更高，这意味着 v-if 将分别重复运行于每个 v-for 循环中。当你想为仅有的一些项渲染节点时，这种优先级的机制会十分有用，如下：
    
    <li v-for="todo in todos" v-if="!todo.isComplete">
      {{ todo }}
    </li>
    上面的代码只传递了未 complete 的 todos。
    
    而如果你的目的是有条件地跳过循环的执行，那么可以将 v-if 置于外层元素 (或 <template>)上。如：
    
    <ul v-if="todos.length">
      <li v-for="todo in todos">
        {{ todo }}
      </li>
    </ul>
    <p v-else>No todos left!</p>
    一个组件的 v-for
    了解组件相关知识，查看 组件。完全可以先跳过它，以后再回来查看。
    
    在自定义组件里，你可以像任何普通元素一样用 v-for 。
    
    <my-component v-for="item in items" :key="item.id"></my-component>
    2.2.0+ 的版本里，当在组件中使用 v-for 时，key 现在是必须的。
    
    然而，任何数据都不会被自动传递到组件里，因为组件有自己独立的作用域。为了把迭代数据传递到组件里，我们要用 props ：
    
    <my-component
      v-for="(item, index) in items"
      v-bind:item="item"
      v-bind:index="index"
      v-bind:key="item.id"
    ></my-component>
    不自动将 item 注入到组件里的原因是，这会使得组件与 v-for 的运作紧密耦合。明确组件数据的来源能够使组件在其他场合重复使用。
    
    下面是一个简单的 todo list 的完整例子：
~~~
    <div id="todo-list-example">
      <input
        v-model="newTodoText"
        v-on:keyup.enter="addNewTodo"
        placeholder="Add a todo"
      >
      <ul>
        <li
          is="todo-item"
          v-for="(todo, index) in todos"
          v-bind:key="todo.id"
          v-bind:title="todo.title"
          v-on:remove="todos.splice(index, 1)"
        ></li>
      </ul>
    </div>
~~~
- 注意这里的 is="todo-item" 属性。这种做法在使用 DOM 模板时是十分必要的，因为在 <ul> 元素内只有 <li> 元素会被看作有效内容。这样做实现的效果与 <todo-item> 相同，但是可以避开一些潜在的浏览器解析错误。查看 DOM 模板解析说明 来了解更多信息。
~~~
    Vue.component('todo-item', {
      template: '\
        <li>\
          {{ title }}\
          <button v-on:click="$emit(\'remove\')">X</button>\
        </li>\
      ',
      props: ['title']
    })
    
    new Vue({
      el: '#todo-list-example',
      data: {
        newTodoText: '',
        todos: [
          {
            id: 1,
            title: 'Do the dishes',
          },
          {
            id: 2,
            title: 'Take out the trash',
          },
          {
            id: 3,
            title: 'Mow the lawn'
          }
        ],
        nextTodoId: 4
      },
      methods: {
        addNewTodo: function () {
          this.todos.push({
            id: this.nextTodoId++,
            title: this.newTodoText
          })
          this.newTodoText = ''
        }
      }
    })
~~~
- 12.Vue过滤器（其实就是我们自己定义的一个函数而已。可以在插值表达式以及v-bind中调用）
  - ‘|’ ，管道符号，{{原数剧 | 过滤器}}
  - 过滤器：1.全局定义 2.局部定义
  - 1.自定义全局过滤器：使用vue.filter（），在vue的构造函数上使用filter方法，自定义一个过滤器；
  - 例：Vue,filter('自定义的过滤器名称'，回调函数)；回调函数的第一个参数是原数剧，第二个是在过滤器中接收的参数参数1，如果多个就相应的在增加
  - 使用构造函数定义过滤器时，必须写在实例对象的前边，否则无法使用！
  - 2.局部自定义过滤器，在vue对象中，配置filters配置参数项，局部的过滤器，只能在作用域的第一层使用；
    filters：{
      '过滤器名称'：回调函数；回调函数的参数和全局的一样
      }
  - 注：多个过滤可以连用，在使用‘|’连接；

- 13.自定义指令
 - 注：如果指令输入错误，不存在，会报error diirective 这个时候，你就需要检查下你的指令是不是写错了！
 - 1.全局定义：是在Vue构造函数上使用directive方法定义一个自定义指令；自定义指令名，不能带v-,当你使用指令时在加上v-
~~~
       Vue.directive('自定义指令名'，{
        inserted：function（element,binding）{//这是在编译结束后，插入到真实dom时使用
            书写自定义指令的一些逻辑
          }
       })
       Vue.directive('自定义指令名'，{
        bind：function（element,binding）{//这是在编译虚拟dom时使用；
            书写自定义指令的一些逻辑
          }
       })
       - 2.局部定义：是在Vue构造函数上使用directive方法定义一个自定义指令；自定义指令名，不能带v-,当你使用指令时在加上v-

       directives：{
       '自定义指令名'：{
          inserted：function（element,binding）{//这是在编译结束后，插入到真实dom时使用
              书写自定义指令的一些逻辑
            }，
          bind：function（element,binding）{//这是在编译虚拟dom时使用；
            书写自定义指令的一些逻辑
          }
       }
~~~
- 14.计算属性（类似于data可以直接 绑定到vue对象实例上）computed使用该方法，替换掉{{}}插值表达式中的复杂方法；
  - 1.computed和methods区别，前者性能高，只计算一次，值存在缓存中（当然要是值改变，也会重新计算）；而后者是使用到就从新调用，比较消耗性能；
  - 2.filter和computed区别
    - 
  - getter 代表获取类函数
  - setter 代表设置类函数 
  - #计算属性中定义的键名可以在插值表达式中直接调用，也就类似调用一个函数处理一些复杂逻辑
  - 例：
  - 定义一个计算属性
~~~
      var vm = new Vue({//computed不能和data中定义的重复，否则无法调用
          el: '#example',
          data: {
            message: 'Hello'
          },
          computed: {
            // 计算属性的 getter
            reversedMessage: function () {
              // `this` 指向 vm 实例
              // return this.message.split('').reverse().join('')
              return "我是computed输出的值"
            }
          }
        })
   调用：{{msg1}}
~~~
- 15.生命周期
   - 就是类似于onload的事件，因为要等待数据获取完毕才能去渲染东西的时候，使用！
     - 其中一种是created属性：function                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              （）{ 要执行的逻辑 }
- 16.vue中调用XHR，使用`vue-resource` vue扩展插件或者使用axios扩展插件，该扩展在Vue构造函数上，定义了一个$http对象方法
  - 两个回调函数，第一个是成功后返回的数据，第二个是失败后返回的信息；返回的数据绑定在body上
  - 例：$htt.get('请求地址').then((respones)=>{},(error)=>{})


- axios 插件用法（既可以在服务端使用，也可以在前端页面中使用）
  - 引用axios插件（模块）,因为不是vue组件，所以不需要进行注册，返回的数据绑定在data中
  - 例：$htt.get('请求地址').then((respones)=>{}).catch((error)=>{})
- 可以在vue的实例上都挂载一个公用的方法或者属性，也就是Vue.prototype


- 17.Vue组件(创建组件必须有一个根节点，也就是在组件内部有一个大标签把多个组件包裹起来)（组件其实就是把，所有功能，样式等等写成一个标签）
  - 注：如果创建的组件名是驼峰命名法则需要把view层的标签名每个单词之间改成中划线连接的形式

  - 例：命名时的注意点:使用驼峰形式命名时,需要把view层的标签改成中划线连接的形式
~~~
    <template id='p2'>
      <login-to-to></login-to-to>
    </template>
    Vue.component('loginToTo', {//vue默认把所有标签名都转换成了小写
        template: "#p2"
    });
      DOM 模板解析注意事项
  当使用 DOM 作为模板时 (例如，使用 el 选项来把 Vue 实例挂载到一个已有内容的元素上)，你会受到 HTML 本身的一些限制，因为 Vue 只有在浏览器解析、规范化模板之后才能获取其内容。尤其要注意，像 <ul>、<ol>、<table>、<select> 这样的元素里允许包含的元素有限制，而另一些像 <option> 这样的元素只能出现在某些特定元素的内部。
  
  在自定义组件中使用这些受限制的元素时会导致一些问题，例如：
  
  <table>
    <my-row>...</my-row>
  </table>
  自定义组件 <my-row> 会被当作无效的内容，因此会导致错误的渲染结果。变通的方案是使用特殊的 is 特性：
  
  <table>
    <tr is="my-row"></tr>
  </table>
  应当注意，如果使用来自以下来源之一的字符串模板，则没有这些限制：
  
  <script type="text/x-template">
  JavaScript 内联模板字符串
  .vue 组件
  因此，请尽可能使用字符串模板。
~~~
- 1.创建组件第一种
  - 1.先定义模板
  - 2.注册组件(component)
  - 3.把模板写到html结构中
  - 4.实例化一个vue对象
~~~
    var tmpl1 = Vue.extend({
    //1.组件模板必须有个根节点
        template: "
          <div>
            <button>点我啊</button>
            <p>1111111111111111</p>
          </div>"
    });
    //2.注册组件
    要注册一个全局组件，可以使用 Vue.component(tagName, options)
    Vue.component('tmpl1', tmpl1);
    //component('组件名称（标签名称）'，创建好的组件)
    //3.实例化一个vue对象
    new Vue({
        el: "#app"
    })
~~~
- 2.第二种
~~~
    // 注册一个全局组件
    // Vue.component(tagName,option)
    Vue.component('my-component', {
      template: '<div>A custom component!</div>'
    });
    //实例化vue对象
    new Vue({
      el:'#app'
    })
    new Vue({
      el:'#app1'
    })
~~~
- 3.第三种
~~~
<!--第三种定义模板的方式,放到body的内部,作用域的外部,使用template标签-->
<!--template不算根节点,必须在内部设置一个根节点-->
<template id="p1">
    <div>
        <p>33333333333333333</p>
        <p>33333333333333333</p>
        <p>33333333333333333</p>
        <p>33333333333333333</p>
    </div>
</template>
    //注册全局组件
    Vue.component('my-component', {
        template: "#p1"
    });
    new Vue({
        el: "#app"
    })
    new Vue({
        el: "#app1"
    })
~~~
- 4.第四种，字符串模板
~~~
  <script type='text/x-template' id='p2'>
    <div>
      <p>sdssssss</p>
      <p>sdssssss</p>
      <p>sdssssss</p>
      <p>sdssssss</p>
      <p>sdssssss</p>
      <p>sdssssss</p>
    </div>
  </script>
//第四种，使用script标签模板，创建组件
    //注册全局组件
    Vue.component('my-component', {
        template: "#p2"
    });
    new Vue({
        el: "#app"
    })
    new Vue({
        el: "#app1"
    })
~~~
  - 注意：子组件，在什么地方定义的，就只能在那个地方用；组件中的template相当于vue对象中的el，也就是选择组件的作用域
    - 每个组件，以及子组件只能作用域该组件，外部是访问不到组件内部的东西；

- 父子组件传值
		- vue实例对象属于父组件，
		- 传值：在自定义标签中使用v-bind接收父组件传的值以及props接收
	- 钩子函数： 当发生事件时，干预它的事件
	- 自定义指令：里边除了inserted 还有其他钩子函数，binding这个好好看 
	- 命名路由 ： 其实就是给创建的路由规则，起个名字
	- onhashchange window下的一个事件，单页面路由（锚点连接）
	
	- 注意点：使用router-link时，注意渲染的router-view所放置的位置，如果位置不正确，可能导致页面渲染的不正常； 
	 
- 路由传参 
		- 1.创建组件，
		- 2.定义路由模式
		- 3.使用this.$route.params.传递的参数（获取/：id这种类型的传参）
		- 3.1 另外一种获取参数的方法就是在创建路由时，配置props：true，在创建组件时使用props接收参数值
~~~
<div id="app">
    <!-- 路由链接 通过to来设置路由链接-,会渲染成1个a标签-->
    <router-link to='/you'>dddd</router-link> //是为了切换路由使用，使用to属性会自动在渲染的a标签href中，添加一个#
    <router-link to='/me'>eeee</router-link>

    <!-- 配置的路由都会渲染router-view标签中，这个标签就是为了渲染vue组件的，它是为了给路由切换的组件占位用的 -->
    <router-view></router-view>
  </div>
  <script>
    // 创建路由
    const router = new VueRouter({
      //routes // （缩写）相当于 routes: routes
      // 定义路由
      routes:[
        {name:'you',path:'/you/:id',component:{
          template:'<div>sss{{id}}</div>',
          props:['id']
        },props:true},
        {name:'me',path:'/me',component:{
          template:'<div>mmmm</div>'
        }}
      ]
    });
    let vm = new Vue({
      el:'#app',
      router
    })
    
    //配置props：true是为了解决父子组件传值的耦合性
    在组件中使用$route会使之与其对应路由形成高度耦合，从而使组件只能在某些特定的url上使用，限制了其灵活性。使用props将组件和路由解耦：
~~~
- 4.使用this.$route.query.传递的参数（获取/?id=1这种类型的传参）
    - 过滤器：filter格式化字符串   不能监视数据变化（也就是数据变化后，不会触发这个过滤器）
    - 计算属性：computed  （监视数据的变化，只要变化就会触发计算属性）
    - 1.监视data中的属性变化
    2.计算属性对应的函数没有参数
    3.计算属性会缓存的属性值
    调用computed  定义的计算属性名，
    {{ reverse }}，不在使用data中定义的属性名
    - 侦听器：watch；不会返回数据，只是监听数据的改变，并触发指定函数
    - 监听data中定义的属性
    - 监听路由对象$route
    - 例：
      watch:{
        'msg':function(){
          console.log(111);
        }
      }
	- params 查询：id类型传参
	- query 查询？传参的参数
spa ： single page application 单页面应用
mvvm：model view viewmodel
mvc：model view controller（是一个调度者，把model数据给view展示）

## Vue的生命周期
- [官网生命周期地址](https://cn.vuejs.org/v2/guide/instance.html#%E5%AE%9E%E4%BE%8B%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)
- beforeCreated这类函数方法是生命周期中的钩子函数；
![s](lifecycle.png)
- Vue单文件组件
 - 创建一个.vue文件，这个就是以恶搞单文件组件，这个单文件组件，如果使用build构建工具，需要使用vue-loader来解析，vue-loader 又需要vue-template-compiler来使用；
 - tempalte中必须有且仅有一个根标签；

<style scoped> 这个属性只在和vue组件配合时，才有作用域的概念
  //scoped 是H5提供的一个属性，类似与css中的作用域，限定样式的使用范围（其根本是使用属性选择器去控制作用域的）
</style>

## vue执行顺序：先编译虚拟dom（bind阶段），编译完成后把编译好的dom节点替换真实节点当中（inserted阶段编译阶段）

## vue UI组件
- 饿了么前端，出了两款基于vue的UI组件，桌面端element UI，移动端Mint UI
## 使用console.error(打印错误信息)；这个能帮我更快的查找到错误；
## 如果是vue的插件，那么使用vue.use注册插件
## node中app.use是注册中间件
组件化开发，就是为了解决模块之间的依赖关系，强制我们分开书写各个模块
app.vue相当于父组件
## 代码重构（也就是代码重新构建下，整理下结构）
每一个模块都是独立的作用域，不能使用其他模块的属性和功能，要使用，就要把文件导入进来，才能使用！
## axios拦截器，在请求和响应时，先拦截，再去做请求和响应
## 定义导出模块时，如果定义方法或者属性，都可以进行调用，使用this就可指向该函数的调用者，也就可以去使用导出模块的方法和属性；
## 浏览器在发送请求时，会预先发送一次请求，如果请求成功过，那么就是用这个请求头，如果不成功就会报错不支持当前预请求的请求头类型，
- cors跨域解决方案，请求类型分为
  - 1.普通请求
  - 2.非普通请求