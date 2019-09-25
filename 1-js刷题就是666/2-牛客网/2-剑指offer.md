地址：https://www.nowcoder.com/ta/coding-interviews

1. 二维数组中的查找
注：迷之c plus plus
```C++
class Solution {
public:
    bool Find(int target, vector<vector<int> > array) {
        int row = array.size();
        if(row==0)return false;
        int col = array[0].size();
        if(col==0)return false;
        
        int i=0,j=col-1;
        while(i<row&&j>=0)
            {
            if(target==array[i][j])
                return true;
            else if(target>array[i][j]) i++;
            else j--;    
        }
        if(i==row||j<0) return false;
        return true ;
        
    }
};
```

2. 替换空格
```js
function replaceSpace(str)
{
    return str.replace(/\s/g,'%20')
}
```

3. 从尾到头打印链表
```js
function printListFromTailToHead(head)
{
    const res = []
    let p = head
    while (p !== null) {
        res.unshift(p.val)
        p = p.next
    }
    return res
}
```
4. 重建二叉树
```js
function reConstructBinaryTree(pre, vin)
{
    if(pre.length === 0 || vin.length === 0) {
        return null
    }
    const index = vin.indexOf(pre[0]),
          left = vin.slice(0,index),
          right = vin.slice(index+1)
    return {
        val: pre[0],
        left:reConstructBinaryTree(pre.slice(1,index+1), left),
        right:reConstructBinaryTree(pre.slice(index+1), right)
    }
}
```
5. 两个栈实现队列
```js
const outStack = [],
      inStack = []

function push(node)
{
    // write code here
    inStack.push(node)
}
function pop()
{
    // write code here
    if(!outStack.length){
        while(inStack.length) {
            outStack.push(inStack.pop())
        }
    }
    return outStack.pop();
}
```
6. 旋转数组到最小数字
```js
function minNumberInRotateArray(rotateArray)
{
    // write code here
    if(rotateArray.length === 0) return 0
    if(rotateArray.length === 1) return rotateArray[0]
    for(let i=0;i<rotateArray.length-1;i++){
         if(rotateArray[i]>rotateArray[i+1]) return rotateArray[i+1]
    }
    return rotateArray[0]
}
```
7. 斐波拉契数
```js
function Fibonacci(n)
{
    // write code here
    if(n===0) return 0;
    if(n===1 || n===2) return 1
    let a = 1, b = 1, i = 2, temp;
    while(i<n){
        temp = a;
        a=b;
        b=temp+a;
        i++
    }
    return b
}
```
8. 跳台阶
```js
function jumpFloor(number)
{
    // write code here
    let n = number
        if(n===2) return 2;
    if(n===1) return 1
    let a = 1, b = 2, i = 2, temp;
    while(i<n){
        temp = a;
        a=b;
        b=temp+a;
        i++
    }
    return b
}
```
9. 变态跳台阶
```js
function jumpFloorII(number)
{
    // write code here
    if(number == 1) return 1
    if(number == 2) return 2
    let res = 0
    for(let i=1;i<number;i++){
        res += jumpFloorII(number-i)
    }
    return res+1
}
```
10. 矩形覆盖
```js
function rectCover(number)
{
    // write code here
    if(number==0) return 0
    if(number==1) return 1
    if(number==2) return 2
    return rectCover(number-1)+rectCover(number-2)
}
```
11. 二进制中1的个数
```js
function NumberOf1(n)
{
    if(n<0) n = n>>>0
    return n.toString(2).split('1').length-1
}
```
12. 数值的整数次方
```js
function Power(base, exponent)
{
    return Math.pow(base, exponent);
}
```
13. 调整数组顺序使奇数位于偶数前面
```js
function reOrderArray(array)
{
    let odd = []
    let even = []
    array.forEach(x=>{
        if(x%2){
            odd.push(x)
        }else{
            even.push(x)
        }
    })
    return([...odd,...even])
}
```
14. 链表中倒数第k个结点
```js
function FindKthToTail(head, k)
{
    let p1=head
    if(p1===null || k<=0) return null
    for(let i=0;i<k-1;i++){
          if(p1.next===null) return null
        p1=p1.next
    }
    let p2=head
    while(p1.next !== null){
        p1=p1.next
        p2=p2.next
    }
    return p2
}
```
15. 反转链表
```js
function ReverseList(pHead)
{
    if(pHead === null) return null
    let p = pHead
    let pre = null
    let nex = pHead.next
    
    while(p !== null){
        nex = p.next
        p.next = pre
        pre = p
        p = nex
    }
    return pre
}
```
16. 合并两个排序的链表
```js
function Merge(pHead1, pHead2)
{
    if(pHead1===null) return pHead2
    if(pHead2===null) return pHead1
    let res = null
    if(pHead1.val<pHead2.val){
        res = pHead1
        res.next = Merge(pHead1.next,pHead2)
    } else {
        res = pHead2
        res.next = Merge(pHead2.next,pHead1) 
    }
    return res
}
```