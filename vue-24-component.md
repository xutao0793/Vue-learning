# component 组件

1. **组件的概念**
    Vue 组件同时也都是 Vue 实例，可接受相同的选项对象`option` (除了一些根级特有的选项) 和使用相同的生命周期钩子，以及模板调用方式。
1. **组件的构建和注册**
    - 构建：`com = Vue.extend(option)`
    - 注册：
        - 全局注册：`Vue.component('my-com', com)`
        - 局部注册：`vm.components: {'my-com': com}`
    - 语法糖： `Vue.component('my-com',option)`   `vm.components('my-com': option)`
    - 组件命名规范

1. **组件三大API： `prop`  /  `event`  /  `slot`**
    **prop**

    - 字符串数组形式： `props: ['prop1', 'prop2', ...]`
    - 对象形式： 
        ```js
        props: {prop1: Number}
        props: {
            prop1: {
                type: [Number, String],
                required: true,
                default: 100,  //当默认值是对象或数组时，必须从函数返回值获取 () => { return value }
                validator: (value) => {
                    // do somethings  return Boolean
                    return result
                }
            }
        }
        ```
    - 动态prop（除字符串外，其它类型传入都需要使用动态prop，即v-bind绑定）
    - 非prop特性（被替换或合并、禁用继承）
    - `$attr`
    - 其它：单向数据流的特性，以及prop的大小写

    **event**
    - `v-on  /  $on` 监听事件
    - `$once`  一次性事件
    - `$emit` 触发事件
    - `$off`  卸载事件监听
    - `.native` 原生事件修饰符
    - `.sync`  双向绑定修饰符
    - `model` 属性
    - `$listeners` 监听器集合（除原生监听事件）

    **slot**
    - 普通插槽 
        ```html
        <slot></slot>
        ```
    - 插槽提供默认值 
        ```html
        <slot>default content</slot>
        ```
    - 具名插槽 
        ```html
        <slot name="someName"></slot>
        <!-- 组件调用 -->
        <my-com>
            <template v-slot:somName></template>
        <my-com>
        ```
    - 作用域插槽 
        ```html
        <slot :prop="value"></slot>
        <!--组件调用 -->
        <my-com>
            <template v-slot='childValue'>{{ cilidValue.value}}</template>
        </my-com>
        ```
    - 独占默认插槽的写法
        ```html
        <some-component v-slot="childValue"> {{ childValue.value }}</some-component>
        <some-component v-slot:default="childValue"> {{ childValue.value }}</some-component>
        ```
    - 解构插槽prop
        ```html
        <my-com v-slot="{value}">{{ value }}</my-com>
        <!-- 重命名 -->
        <my-com v-slot="{value: otherName}">{{ otherName }}</my-com>
        <!-- 重命名并提供默认值 -->
        <my-com v-slot="{value: {otherName: defaultValue}}">{{ otherName }}</my-com> 
        ```
    - 动态插槽名
        ```html
        <my-com>
            <template v-slot:[dynamicSlotName]></template>
        </my-com>
        ```
    - `v-slot` 的简写 `#`
        ```html
        <my-com>
            <template #:somName></template>
        <my-com>
        ```
    - 模板编译作用域 和 插槽作用域

1. **动态组件**
1. **异步组件**
1. **内置组件**

1. **组件实例的调用**
    - `ref`
    - `$root`
    - `$parent`
    - `$children`

1. **组件间的通信**
    - 父子组件通信 `prop / $emit`
    - 后代组件通信 `provide / inject`
    - 事件总线 `const Bus = new Vue()`
    - 状态管理器 `Vuex`

1. **其它**
    - 组件的递归调用
    - 组件的循环引用
    - `v-once`创建静态组件
