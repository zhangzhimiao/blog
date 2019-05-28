重点在input的绑定属性value上，如果写成
```js
 <tr v-for="(item,index) in list">
    <td>
        <input type="checkbox" :id="index" value="item.id" v-model="checkedItem">
    </td>
    <td>{{ index + 1 }}</td>
</tr>
```
那么就会出现选一个选项而所有选项全部被选中的问题，下列写法不会出现上述问题
```js
<tr v-for="(item,index) in list">
    <td>
        <input type="checkbox" :id="index" :value="item.id" v-model="checkedItem">
    </td>
    <td>{{ index + 1 }}</td>
</tr>
```
>PS:一定不要忘了v-bind，bind是绑定了动态数据，否则数据就是静态的,注意看两段代码的value部分