# computed与watch的区别

## computed

1. 支持缓存，默认走缓存。计算属性是基于它们的响应式依赖进行缓存的，也就是基于data中声明过或者父组件传递的props中的数据通过计算得到的值。
2. 依赖其他属性，只有当依赖的数据发生改变，才会进行重新计算。
3. 不支持异步，当computed内有异步操作时无效，无法监听数据的变化。
4. 如果computed属性值是函数，那么默认会走get方法；函数的返回值就是属性的属性值；在computed中的，属性都有一个get和一个set方法，当数据变化时，调用set方法。

## watch

1. 不支持缓存，一旦数据变化，会直接触发相应的操作。

2. 支持异步。

3. 接收两个参数，第一个是新值，第二个是旧值。

   