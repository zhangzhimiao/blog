
<h1>改变原数组</h1>

1.push()往数组末尾添加元素，可一次添加多个
```js
Array.prototype.push = function(){
    for(var i = 0; i < arguments.length; i++){
        this[this.length] = arguments[i];
    }
    return this.length;
}
```

2.pop()移除数组中的最后一个元素，参数没有效果
```js
Array.prototype.pop = function(){
    var temp = this[this.length - 1];
    this.length = this.length - 1;
    return temp;
}
```

3.shift()移除数组最开始的元素，只能一次移除一个，参数没有效果
```js
Array.prototype.shift = function(){
    var temp = this[0];
    for(var i = 0; i < this.length - 1; i++){
        this[i] = this[i + 1];
    }
    this.length--;
    return temp;
}
```

4.unshift()往数组头部添加元素，可一次添加多个
```js
Array.prototype.unshift = function(){
    var oldLength = this.length - 1;
    var temp = this.length;
    var newLength = arguments.length + this.length - 1;
    for(var i = 0; i < temp; i ++){
        this[newLength--] = this[oldLength--];
    }
    for(var i = 0; i < arguments.length; i ++){
        this[i] = arguments[i];
    }
    return this.length;
}
```

5.sort()//用来排序数组，可自定义
```js
//排序过程：1.将数组中的第一个位置的元素与第二个元素位置比较
//如果第一个元素大于第二个，则将两个元素换位，
//如果第一个元素小于第二个，则元素的位置不变
//此时再将第一个位置的元素与第三个位置的元素比较
//一次遍历以后，第二个位置的元素与第三个位置的元素比较
//规则如上直至第n-1个元素与第n个元素比较完为止，整个过程类似于选择排序
//自定义sort方法如下
function newSort(x, y){
    //顺序
    //return x - y;
    //逆序
    return y - x;
}
//使用自定义sort()
arr.sort(newSort);
//特殊的方法，打乱原数组，每次调用返回的结果都不一样
function mixtureArr(){
    return 0.5 - Math.random();
}
```

6.reverse()//将数组倒置,即按原数组排列顺序的相反顺序排列
```js
Array.prototype.reverse = function(){
    var temp;
    for(var i = 0; i < this.length / 2; i ++){
        temp = this[i];
        this[i] = this[this.length-i-1];
        this[this.length-i-1] = temp;
    }
    return this;
}
```

7.splice()
```js
//用来剪切数组，参数可分三种，一个参数，两个参数，多个参数
//一个参数或两个参数时候的第一个参数代表切的位置，可为负数，真正的位置为该负数加上数组长度代表的位置
//如果代表真正位置的数还是为负数，则从第一个元素开始
//如果第一个参数的值大于数组的长度，则相当于没有切，返回空数组。
//一个参数的时候，该数为真实位置，从该位置开始切，直到数组最后
//两个参数的时候，第一个参数代表切的开始位置，第二个参数代表要切的个数
//如果两个参数的和大于数组从第一个参数开始所示位置到数组最后的长度，则从第一个参数表示的位置开始，截取后面所有的元素
//多个参数的时候，第二个参数往后的所有参数，均为从切口位置要插入的元素
//该方法返回切下的数组，原数组为剩下的部分
Array.prototype.splice = function(){
    var splicePart = [];
    if(arguments[0] >= this.length || arguments[1] < 0){
        if (arguments > 2) {
             for (var i = 2; i < arguments.length; i++) {
                this[length++] = arguments[i];                
            }
        }
        return splicePart;
    }
    var index = arguments[0] >= 0 ? arguments[0] : (arguments[0] + this.length < 0 ? 0 : arguments[0] + this.length);
    var border = index + arguments[1] <= this.length ? arguments[1] : this.length - index;
    var current = 0;
    for(var i = index; i < index + border; i ++){
        splicePart[current++] = this[i];
    }
    if (arguments.length <= 2) {
        for(var i = index; i < this.length; i++){
            this[i] = this[i + border];
        }
        this.length = this.length - border;
    }else{
        var argu_length = arguments.length - 2;
        for(var i = 0; i < this.length - index - border; i++){
            this[i + index + argu_length] = this[i + index + border];
        }
        for(var i = 0; i < argu_length; i++){
            this[i + index] = arguments[i + 2];
        }
        this.length = this.length - border + argu_length;
    }
    this = splicePart;
    return this;
}
```

8.数组去重
```js
Array.prototype.unique = function(){
    var obj = {};
    var arr = [];
    var length = this.length;
    for(var i = 0; i < length; i ++){
        if(!obj[this[i]]){
            obj[this[i]] = this[i];
        }
    }
    this.length = 0;
    for(var x in obj){
        this.push(obj[x]);
    }
    return this;
}
```