## computed(计算属性)和methods的区别
1.  使用方式：
```html
<!-- 计算属性里方法的调用 -->
<div id="app">
    总价： {{ prices }} <br/>
    test:{{ tests }}
</div>

<!-- methods里方法的调用 -->
<div id="app">
    总价： {{ prices() }} <br/>
    test:{{ tests() }}
</div>
```

2. 执行机制  
computed里的方法在初始化执行过后，只要任何值有更新，那么所有在computed计算属性里和其相关的值都会更新。
methods只有在调用的时候才会执行对应的方法，不会自动同步数据。
computed计算属性跟methods在内部的函数写起来没有什么区别，只是在调用的时候不一样。

总结：computed计算属性的缓存原理在我们处理大量数据的时候使用可以大大提高效率，不必在数据没有发生改变的时候重新获取数据的值，可直接获取到结果，并且只执行绑定依赖的方法。methods里方法在依赖的值改变后，只有设置触发才会重新执行methods里相关的方法。