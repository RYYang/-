https://www.nowcoder.com/ta/js-assessment

45个很简单的题目，一年前刷的，第一遍还很吃力，现在看起来简单到不行，复习总结一下

1、查找数组元素位置
注：es6有find和findIndex方法，可以传函数。
```javascript
function indexOf(arr, item) {
  return arr.indexOf(item)
}
```
2、数组求和
注：可以用箭头函数；reduce注意初值。
```js
function sum(arr) {
    return arr.reduce(function(sum,x){
        return sum+x
    })
}
```
3、移除数组中的元素，返回新数组
考：filter用法
```js
function remove(arr, item) {
    return arr.filter(function(x){
        return x !== item
    })
}
```
4、移除数组中的元素，直接操作数组
考：splice直接操作数组
附：常见的直接操作数组的方法pop,push,shift,unshift,splice,reverse,sort
```js
function removeWithoutCopy(arr, item) {
	for(var i=0;i<arr.length;i++){
    	if(arr[i]===item){
            arr.splice(i,1);
            i--;
        }
}
    return arr;
}
```
5、添加元素，不改变原数组
考：先复制，再操作
注：es6，任何操作原数组的方法都可以这样操作，[...arr].push(item)
```js
function append(arr, item) {
    var arr1=arr.slice(0);
    arr1.push(item);
    return arr1;
}
```
6、删除数组最后一个元素
```js
function truncate(arr) {
    return arr.slice(0,arr.length-1)
}
```
7、添加元素，从头
```js
function prepend(arr, item) {
	var arr1=arr.slice(0);
    arr1.unshift(item);
    return arr1;
}
```
8、删除数组第一个元素
注：可以用shift
```js
function curtail(arr) {
	var arr1=arr.slice(0);
    arr1.splice(0,1);
    return arr1;
}
```
9、数组合并
注：es6，[...arr1,...arr2]
```js
function concat(arr1, arr2) {
	return arr1.concat(arr2);
}
```
10、添加元素，index处，返回新数组
```js
function insert(arr, item, index) {
	var arr1=arr.slice(0);
    arr1.splice(index,0,item);
    return arr1;
}
```
11、计数
注：可以用str可以用match全局
```js
function count(arr, item) {
    var j=0;
	for(var i=0;i<arr.length;i++){
        if(arr[i]===item) j++;
    }
    return j;
}
```
12、查找重复元素
```js
function duplicates(arr) {
    var arr1 = arr.filter(function(x, index){
        return arr.indexOf(x) !== index
    })
    return arr1.filter(function(x,index){
        return arr1.indexOf(x) === index
    })
}
```
13、求二次方
注：最好用map
```js
function square(arr) {
	var arr1=[];
    for(var i=0;i<arr.length;i++){
        arr1[i]=arr[i]*arr[i];
    }
    return arr1;
}
```
14、查找元素位置
注：match直接返回数组
```js
function findAllOccurrences(arr, target) {
	arr1=[];
   for(var i=0;i<arr.length;i++){
       if(arr[i]===target) arr1.push(i);
   }
    return arr1;
}
```
15、避免全局变量
注：函数作用域
```js
// 错误，没有用var定义，myObject会到全局变量，成为window的对象
function globals() {
    myObject = {
      name : 'Jory'
    };

    return myObject;
}
// 正确
function globals() {
    var myObject = {
      name : 'Jory'
    };
    return myObject;
}
```
16、正确函数定义
```js
// 错误 函数声明有变量提升
function functions(flag) {
    if (flag) {
      function getValue() { return 'a'; }
    } else {
      function getValue() { return 'b'; }
    }

    return getValue();
}
// 正确 函数表达式
function functions(flag) {
    if (flag) {
      getValue = function() { return 'a'; }
    } else {
      getValue = function() { return 'b'; }
    }

    return getValue();
}
```
17、正确使用parseInt
```js
function parse2Int(num) {
    return parseInt(num); // 加10进制
}
```
18、完全等同
注：并不是所有的情况都要用完全等同
```js
function identity(val1, val2) {
	return(val1===val2);
}
```
19、计时器
题目：
实现一个打点计时器，要求
1、从 start 到 end（包含 start 和 end），每隔 100 毫秒 console.log 一个数字，每次数字增幅为 1
2、返回的对象中需要包含一个 cancel 方法，用于停止定时操作
3、第一个数需要立即输出
```js
function count(start, end) {
    console.log(start++);
    var timer=setInterval(function(){
        if(start<=end){
        	console.log(start);
        	start++;
    	}
        else
        clearInterval(timer);
    },100);
    return {cancel:function(){clearInterval(timer);}};   
}
```
20、流程控制
注：可以用switch case
```js
function fizzBuzz(num) {
	if(num%3==0&&num%5==0) 
        return "fizzbuzz";
    else if(num%3==0) 
        return "fizz";
    else if(num%5==0) 
        return "buzz";
    else if(num==null||typeof num!="number")
        return false;
    else return num;
}
```
21、函数传参
题目：将数组 arr 中的元素作为调用函数 fn 的参数
```js
function argsAsArray(fn, arr) {
    return fn.apply(this, arr);
}
```
22、函数的上下文
题目：将函数 fn 的执行上下文改为 obj 对象
注：bind要加(),call传一个个参数,apply传数组
```js
function speak(fn, obj) {
	return fn.bind(obj)();
}
```
23、返回函数
注：高阶函数，至少传一个函数或者返回一个函数
```js
function functionFunction(str) {
    return function f(a){ return str+', '+a};
}
```
24、使用闭包（有点难）
注：内部函数的变量还在被外部函数引用，没有被销毁
```js
// 用map
function makeClosures(arr, fn) {
 return arr.map(function(item){
        return function(){
            return fn(item);
        }
    })
}
// forEach
function makeClosures(arr, fn) {
  var result = [];
     arr.forEach(function(e){
         result.push(function(num){
             return function(){
                 return fn(num);
             };
         }(e));
     });
     return result;
 }
```
25、二次封装函数
```js
function partial(fn, str1, str2) {
    return function(str3){return fn.call(this,str1,str2,str3);};
}
```
26、使用arguments
注：arguments是类数组，可以先转换成真正的数组
```js
function useArguments() {
	var sum=0;
    for(var i=0;i<arguments.length;i++){
        sum+=arguments[i];
    }
    return sum;
}
```
27、使用apply调用函数
```js
function callIt(fn) {
    var arr=Array.prototype.slice.call(arguments,1);
    return fn.apply(this,arr);
}
```
28、二次封装函数
```js
    function partialUsingArguments(fn) {
        var arr=Array.prototype.slice.call(arguments,1);
        return function(){
            return fn.apply(null,arr.concat(Array.prototype.slice.call(arguments)));};                   
    }
```
29、柯里化
```js
function curryIt(fn) {
	var n=fn.length;
    var args=[];
    return function(arg){
        args.push(arg);
        if(args.length<n){
            return arguments.callee;
        }
        else return fn.apply(null,args);
    };
}
```
30、或运算
```js
function or(a, b) {
	return a||b;
}
```
31、且运算
```js
function and(a, b) {
	return a&&b;
}
```
32、模块
```js
function createModule(str1, str2) {
    return obj={
        greeting:str1,
        name:str2,
        sayIt:function(){
        return this.greeting + ', ' +this.name;
    }
    }
}
```
33、二进制转换
注：toString也还行
```js
function valueAtBit(num, bit) {
    return num & (1 << (bit-1)) ? 1 : 0;
}
```
34、二进制转换（2转10）
```js
function base10(str) {
    var sum=0;
	for(var i=0;i<str.length;i++){
        sum=sum*2;
        sum=sum+(str[i]-0);
    }
    return sum;
}
```
35、二进制转换（补位）
注：循环也还行
```js
function convertToBinary(num) {
	var a=num.toString(2);
    return '00000000'.slice(a.length)+a;
}
```
36、乘法
```js
function multiply(a, b) {
	return a*b;
}
```
37、改变上下文
```js
function alterContext(fn, obj) {
	return fn.bind(obj)();
}
```
38、批量改变对象属性
```js
function alterObjects(constructor, greeting) {
	constructor.prototype.greeting=greeting;
}
```
39、遍历属性(找出不在原型链上的)
注：Object.keys(obj),Object.getOwnPropertyNames(obj),for...of
```js
function iterate(obj) {
    var res = [];
	for (p in obj) {
        if (obj.hasOwnProperty(p)) {
            res.push(p.toString() + ": " + obj[p]);
        }
    }
    return res;
}
```
40、判断是否包含数字
```js
function containsNumber(str) {
	return /\d/.test(str);
}
```
41、检查重复字符串
```js
function containsRepeatingLetter(str) {
	return /([a-zA-Z])\1/.test(str);
}
```
42、是否以元音字母结尾
```js
function endsWithVowel(str) {
	return /[aeiou]$/i.test(str);
}
```
43、获取指定字符串（连续三个数字）
```js
function captureThreeNumbers(str) {
    var reg=str.match(/\d{3}/);
    if(reg){
        return reg[0];
    }
    else
        return false;
}
```
44、判断是否符合指定格式(XXX-XXX-XXXX)
```js
function matchesPattern(str) {
    return /^\d{3}\-\d{3}\-\d{4}$/.test(str);
}
```
45、判断是否符合USD格式
```js
function isUSD(str) {
    return /^\$\d{1,3}(,\d{3})*(\.\d{2})?$/.test(str);
}
```