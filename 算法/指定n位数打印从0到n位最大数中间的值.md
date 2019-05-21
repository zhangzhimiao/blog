题目的具体描述：**输入数字n，按顺序打印出从0到最大的n位十进制数。比如输入3，则打印出0、1、2一直到最大的3位数999。**

题目思路：首先，最后一位是从0到9一直循环，直到前面所有位的数都变成9；其次，各个位从右到左都是从0增加到9。

* 只有一位的时候，可以考虑直接从0到9
* 当两位的时候，可以考虑个位数从0到9，然后在十位数从0到9的时候，每个十位数都会让个位数从0到9循环一次
* 三位数依次类推，百位每次在从0到9改变的时候，十位数就要从0到9循环一次。。。

这样，n位数就可以知道第n位从0到9的时候，第n-1位每次都会从0到9循环一次，于是可以使用减治法，让n位数变成n-1位。。。最后变成1位，每个位十次循环。于是得出下列代码：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <input  id="input" type="text" name="">
    <button onclick="print()">打印</button>
    <script type="text/javascript">
        var input = document.getElementById('input');
        var value;
        //运用数组可以存储任意长的数字
        var str = [];

        function print () {
            value = input.value;
            for(var i = 0; i < value; i++){
                str.push("0");
            }
            add(0);
        }

        function add (index) {
            //当到达个位数的时候，输出对应数组中的数字
            if (index == str.length - 1) {
                for (var i = 0; i < 10; i++) {
                    str[index] = i;
                    console.log(str.join(""));
                }
            }else if (index > str.length -1) {
                //防止出现下标越界，虽然不大可能
                return;
            }else {
                //让每一位数都能从0到9
                for (var i = 0; i < 10; i++) {
                    str[index] = i;
                    //递归，减治，数组下标增加，数的规模减小
                    add(index+1); 
                }
            }
        }
    </script>
</body>
</html>
```