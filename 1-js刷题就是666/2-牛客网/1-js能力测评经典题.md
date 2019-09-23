https://www.nowcoder.com/ta/js-assessment
50个很简单的题目，一年前刷的，第一遍还很吃力，现在看起来简单到不行，复习总结一下
1、查找数组元素位置
注：es6有find和findIndex方法，可以传函数。
```
function indexOf(arr, item) {
  return arr.indexOf(item)
}
```
2、数组求和
注：可以用箭头函数；reduce注意初值。
```
function sum(arr) {
    return arr.reduce(function(sum,x){
        return sum+x
    })
}
```
3、移除数组中的元素，返回新数组
考：filter用法
```
function remove(arr, item) {
    return arr.filter(function(x){
        return x !== item
    })
}
```
4、移除数组中的元素，直接操作数组
考：splice直接操作数组
附：常见的直接操作数组的方法pop,push,shift,unshift,splice,reverse,sort
```
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
```
function append(arr, item) {
    var arr1=arr.slice(0);
    arr1.push(item);
    return arr1;
}
```
6、删除数组最后一个元素
```
function truncate(arr) {
    return arr.slice(0,arr.length-1)
}
```
7、添加元素，从头
```
function prepend(arr, item) {
	var arr1=arr.slice(0);
    arr1.unshift(item);
    return arr1;
}
```
8、删除数组第一个元素
注：可以用shift
```
function curtail(arr) {
	var arr1=arr.slice(0);
    arr1.splice(0,1);
    return arr1;
}
```
9、数组合并
注：es6，[...arr1,...arr2]
```
function concat(arr1, arr2) {
	return arr1.concat(arr2);
}
```
10、添加元素，index处，返回新数组
```
function insert(arr, item, index) {
	var arr1=arr.slice(0);
    arr1.splice(index,0,item);
    return arr1;
}
```