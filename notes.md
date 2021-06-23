#### Date 2021/6/21

1. defineComponent中`inheritAttrs`选项

   在父组件中给子组件传递的props没有被子组件接收时，会作为普通属性出现在子组件HTML根标签上

   `inheritAttrs: false`可以禁止这些默认行为

   https://www.jianshu.com/p/ce8ca875c337

2. 实例属性 `$attrs`

   a. 当设置了`inheritAttrs: false`后，可以通过setup选项传入第二个参数`context`使用`context.attrs`，或者直接用解构写法`setup(props, { attrs }) {}`接收未被props接收的值

   b. 可以使用`v-bind="$attrs"`搭桥实现跨组件传值（父---孙）。比如通过父组件传递props，子组件（中间层）不接收，可以通过子组件里的孙组件绑定`v-bind="$attrs"`，将父组件的props传递至孙组件中。注意孙组件接收的将是除了子组件接收以外的值，也就是说如果有的值已经被子组件接收了，孙组件将无法接收这些值。

   https://www.freesion.com/article/35591118141/

   https://www.jianshu.com/p/ce8ca875c337



#### Date 2021/6/22

1. 在 Vue 3.x 的虚拟 DOM 中，事件监听器只是以`on`为前缀的属性。因此，监听器被归纳为`$attrs` 的一部分，从而移除了`$listerners`

   ```vue
   <template>
     <label>
       <input type="text" v-bind="$attrs" />
     </label>
   </template>
   <script>
   export default {
     inheritAttrs: false
   }
   </script>
   ```

   如果这个组件接收到一个 `id` 属性和一个 `v-on: close` 监听器，`$attrs`对象现在看起来如下

   ```json
   {
     id: 'my-input',
     onClose: () => console.log('close Event triggered')
   }
   ```

   https://www.cnblogs.com/yinyuxing/p/14558492.html

2. 具名插槽`slot`

   例如对于一个带有如下模板的 `<base-layout>` 组件：

   ```html
   <div class="container">
     <header>
       <slot name="header"></slot>
     </header>
     <main>
       <slot></slot>
     </main>
     <footer>
       <slot name="footer"></slot>
     </footer>
   </div>
   ```

   一个不带 `name` 的 `<slot>` 出口会带有隐含的名字“default”。

   在向具名插槽提供内容的时候，我们可以在一个 `<template>` 元素上使用 `v-slot` 指令，并以 `v-slot` 的参数的形式提供其名称：

   ```html
   <base-layout>
     <template v-slot:header>
       <h1>Here might be a page title</h1>
     </template>
   
     <template v-slot:default>
       <p>A paragraph for the main content.</p>
       <p>And another one.</p>
     </template>
   
     <template v-slot:footer>
       <p>Here's some contact info</p>
     </template>
   </base-layout>
   ```

   现在 `<template>` 元素中的所有内容都将会被传入相应的插槽。

   渲染的 HTML 将会是：

   ```html
   <div class="container">
     <header>
       <h1>Here might be a page title</h1>
     </header>
     <main>
       <p>A paragraph for the main content.</p>
       <p>And another one.</p>
     </main>
     <footer>
       <p>Here's some contact info</p>
     </footer>
   </div>
   ```

   注意，`v-slot` 只能添加在 `<template>` 上（只有一种特殊情况，可以先忽略）



#### Date 2021/6/23

1. 

