1. 删除链表中的节点（237）
```js
var deleteNode = function(node) {
   node.val = node.next.val;
  node.next = node.next.next;
};
```
2. 二叉树最大深度（104）
```js
var maxDepth = function(root) {
    if(root === null) return 0
    return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1
};
```
3. Nim游戏(292)
```js
var canWinNim = function(n) {
    if(n%4===0) return false
    return true
};
```
4. 反转字符串中的单词 III(557)
```js
var reverseWords = function(s) {
    return s.split(' ').map(x=>x.split('').reverse().join('')).join(' ')
};
```
5. 反转字符串(344)
```js
var reverseString = function(s) {
    let len = s.length
    let temp
    for(let i=0;i<len/2;i++){
        temp = s[len-i-1]
        s[len-i-1]=s[i]
        s[i]=temp
    }
};
```
6. 反转链表(206)
注：用了n的额外空间
其它：1原地修改双指针加临时变量，2递归
```js
// 原地反转
temp = p.next
p.next = pre
pre = p
p = temp
// 递归
HEAD = reverseList(head->next);
head->next->next = head;
head->next = NULL;
return HEAD;
```
```js
var reverseList = function(head) {
    let p = head
    let arr = []
    if(head === null) return head
    while(p !== null){
        arr.push(p.val)
        p=p.next
    }
    arr.reverse()
    let res = new ListNode(arr[0])
    let p2 = res
    for(let i=1;i<arr.length;i++){
      p2.next = new ListNode(arr[i]) 
        p2 = p2.next
    }
    p2.next = null
    return res
};
```
7. 只出现一次的数字(136)
注：用了异或
```js
var singleNumber = function(nums) {
    let res = 0
    nums.forEach(x=>{
        res = res ^ x
    })
    return res
};
```
8. 二叉搜索树的最近公共祖先(235)
```js
var lowestCommonAncestor = function(root, p, q) {
          if(p===null||q===null||root===null){
            return null;
        }
    if(root.val>=p.val&&root.val<=q.val) return root
    if(root.val>p.val&&root.val>q.val) {
        return lowestCommonAncestor(root.left,p,q)
    }
    if(root.val<p.val&&root.val<q.val) {
        return lowestCommonAncestor(root.right,p,q)
    }
    return root
};
```
9. 求众数(169)
```js
var majorityElement = function(nums) {
    nums.sort((a,b)=>a-b)
    return nums[Math.floor(nums.length/2)]
};
```
10. 合并两个有序链表
```js
var mergeTwoLists = function(l1, l2) {
    if (l1 === null) return l2
    if (l2 === null) return l1
    l3 = new ListNode(4)
    p3 = l3
    p1 = l1
    p2 = l2
    while(p1 !== null && p2 !==null){
        if(p1.val <= p2.val){
            p3.next = p1
            p3 = p3.next
            p1 = p1.next
        } else {
            p3.next = p2
            p3 = p3.next
            p2 = p2.next
        }
    }
    if(p1 === null) {
        p3.next = p2
    } else {
        p3.next = p1
    }
  return l3.next
};
```