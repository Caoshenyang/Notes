# Vue 3.0 学习笔记

## Vue 3.0 六大亮点

- **Performance：性能比vue2.x 快1.2^2倍**
- **Tree shaking support：按需编译，体积比vue2.x 更小**
- **Composition API：组合API /  注入API （类似React Hooks）**
- **Better TypeScript support：更好的 Ts 支持**
- **Custom Renderer API：暴漏了自定义渲染API**
- **Fragment，Teleport(Protal)，Suspense：更先进的组件**

## Vue 3.0 性能提升

1. **diff方法优化**：https://vue-next-template-explorer.netlify.app/

   - **vue2中的虚拟dom树是进行全量的对比**

   - **vue3增加了静态标记（PatchFlag）**

     > 在与上次虚拟dom树进行对比的时候，不再全部一一比较，只针对带有patch flag的节点进行比较，并且可以通过flag的信息得知当  前节点要对比的具体内容。

![1](https://notes-page.oss-cn-beijing.aliyuncs.com/vue3.0/1.png)



2. hoistStatic **静态提升**
   - **vue2元素是否参与更新，每次都会重新创建，然后再渲染**
   - **vue3对于不参与更新的元素，会做静态提升，只会被创建一次，在渲染的时候直接复用**

![2](https://notes-page.oss-cn-beijing.aliyuncs.com/vue3.0/2.png)



3. cacheHandlers **事件侦听器缓存**
   - **默认情况下onClick会被视为动态绑定，所以每次都会追踪它的变化，但是因为是同一个函数，所以没有追踪变化，直接缓存起来复用**

![3](https://notes-page.oss-cn-beijing.aliyuncs.com/vue3.0/3.png)

![4](https://notes-page.oss-cn-beijing.aliyuncs.com/vue3.0/4.png)

>  **开启事件监听缓存之后，不存在 静态标记了， 在vue3的 diff 算法 中，只有静态标记的才会进行比较，才会追踪**



4. ssr 渲染