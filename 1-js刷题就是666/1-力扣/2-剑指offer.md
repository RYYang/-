03. 数组中重复数字
hash,set,indexOf
```js
var findRepeatNumber = function(nums) {
    let hash = {}
    for(let i=0;i<nums.length;i++){
        if(hash[nums[i]] === 1){
            return nums[i]
        } else {
            hash[nums[i]] = 1
        }
    }
};
```
04. 二维数组中的查找
从左下角或者右上角找
```js
var findNumberIn2DArray = function(matrix, target) {
    if(matrix===null||matrix.length===0||matrix[0].length===0){
        return false
    }
    let rows=matrix.length, columns=matrix[0].length
    let row = 0, column=columns-1
    while(row<rows&&column>=0){
        let cur = matrix[row][column]
        if(cur===target){
            return true
        }else if(cur>target){
            column--
        } else {
            row++

        }
    }
    return false
};
```

05. 替换空格
正则
```js
var replaceSpace = function(s) {
    return s.replace(/ /g,'%20')
};
```

06. 从尾到头打印链表
本题返回数组，只要遍历一遍即可
```js
var reversePrint = function(head) {
 let arr = []
 let p = head
 while(p !== null){
     arr.unshift(p.val)
     p=p.next
 }
return arr
};
```

07. 重建二叉书
知道中序和前序，前序是根，找出中序被根切分的左右，并算出长度。递归
```js
var buildTree = function(preorder, inorder) {
    if(preorder.length === 0 || inorder.length === 0) return null
    let root = {
        val: preorder[0],
        left: null,
        right: null
    }
    let i = inorder.indexOf(preorder[0])
    root.left = buildTree(preorder.slice(1,1+i),inorder.slice(0,i))
    root.right = buildTree(preorder.slice(1+i),inorder.slice(1+i))
    return root
};
```

09. 用两个栈实现队列
```js
var CQueue = function() {
    this.inStack = []
    this.outStack = []
};

/** 
 * @param {number} value
 * @return {void}
 */
CQueue.prototype.appendTail = function(value) {
    this.inStack.push(value)
};

/**
 * @return {number}
 */
CQueue.prototype.deleteHead = function() {
    const {inStack, outStack} = this
        if (outStack.length) {
        return outStack.pop();
    } else {
        while (inStack.length) {
            outStack.push(inStack.pop());
        }
        return outStack.pop() || -1;
    }
};
```

10- I. 斐波那契数列 10- II. 青蛙跳台阶问题
```js
var fib = function(n) {
    let arr = [0,1]
    for(i=2;i<=n;i++){
        arr[i]=arr[i-1]+arr[i-2]
        arr[i] %= 1000000007
    }
    return arr[n]
};
```

11. 旋转数组的最小数字
```js
var minArray = function(numbers) {
    let start = 0
    let end = numbers.length - 1
    while(start<end){
        let  mid = Math.floor((end+start)/2)
        if(numbers[mid]>numbers[end]){
            start = mid + 1
        } else if(numbers[mid]<numbers[end]) {
            end = mid
        } else {
            end--
        }
    }
    return numbers[start]
};
```

14- I. 剪绳子
```js
var cuttingRope = function(n) {
    if(n === 2) return 1
    if(n === 3) return 2
    if(n === 4) return 4
    let res = 1
    while(n>4){
        res = res*3
        n = n-3
    }
    return res*n
};
```

14- II. 剪绳子 II
```js
var cuttingRope = function(n) {
    if(n === 2) return 1
    if(n === 3) return 2
    if(n === 4) return 4
    let res = 1
    while(n>4){
        res = res*3
        res %= 1000000007;
        n = n-3
    }
    return (res*n)%1000000007
};
```
15. 二进制中1的个数
```js
var hammingWeight = function(n) {
    return n.toString(2).split('').reduce((s,x)=>s+Number(x),0)
    
};
```
17. 打印从1到最大的n位数
```js
var printNumbers = function(n) {
    let str = ''
    for(i=0;i<n;i++){
        str += 9
    }
    let num = str - 0
    let arr = []
    for(i=1;i<=num;i++){
        arr.push(i)
    }
    return arr
};
```
18. 删除链表节点
```js
var deleteNode = function(head, val) {
    let pre = new ListNode(-1)
    pre.next = head
    let p = pre
    while(p.next){
        if(p.next.val === val){
            p.next = p.next.next
            break
        }
        p = p.next
    }
    return pre.next
};
```
19. 正则表达式匹配
```js
var isMatch = function(s, p) {
    return new RegExp("^" + p + "$", "g").test(s);
};
```

21. 调整数组顺序使奇数位于偶数前面
```js
var exchange = function(nums) {
    let start = 0
    let end = nums.length - 1
    while(start<end){
        if(nums[start]%2 === 0&&(nums[end]%2 === 1)){
            let temp = nums[start]
            nums[start] = nums[end]
            nums[end] = temp
            start++
            end--
        } else {
           if(nums[start]%2 === 1) start++
        if(nums[end]%2 === 0) end-- 
        }
    }
    return nums
};
```

22. 链表中倒数第k个节点
```js
var getKthFromEnd = function(head, k) {
    let p = head
    for(i=0;i<k;i++){
        p = p.next
    }
    let pre = head
    while(p !== null){
        pre = pre.next
        p = p.next
    }
    return pre
};
```

24. 反转链表
```js
var reverseList = function(head) {
    let cur = null
    let pre = head
    while (pre !== null) {
       let p = pre.next 
       pre.next = cur
        cur = pre
        pre = p
    }
    return cur
};
```
25. 合并两个排序的链表
```js
var mergeTwoLists = function(l1, l2) {
    let l = new ListNode(0)
    let p = l
    while(l1 !== null && l2 !== null) {
        if(l1.val<l2.val){
            p.next=l1
            l1=l1.next
        } else {
            p.next = l2
            l2 = l2.next
        }
        p = p.next
    }
    if(l1 === null){
        p.next = l2
    } else {
        p.next = l1
    }
    return l.next
};
```

27. 二叉树的镜像
```js
var mirrorTree = function(root) {
    if(root === null) return root
    if(root.left === null && root.right === null) return root
    let temp = root.left
    root.left = mirrorTree(root.right)
    root.right = mirrorTree(temp)
    return root
};
```

28. 对称的二叉树
```js
var isSymmetric = function(root) {
    if(root === null) return true
    
    function recur(left, right){
        if(left === null && right === null) {
            return true
        } else if(left === null || right === null || left.val!==right.val)  {
             return false
        } else {
                    return recur(left.left,right.right)&&recur(left.right,right.left)
        }
    }
       return recur(root.left, root.right)
};
```

29. 顺时针打印矩阵
```js
var spiralOrder = function(matrix) {
    let n = matrix.length
    if(n===0) return []
    let m = matrix[0].length
    let l = 0, r = m - 1, t = 0, b = n - 1;
    let res = []
    let nums = 1, target = n * m;
    while (nums<=target) {
   for (let i = l; i <= r; i++) {
            res.push(matrix[t][i]) // left to right.
            nums++
        }
        if(nums>target) break;
        t++;
        for (let i = t; i <= b; i++) {
            res.push(matrix[i][r]); // top to bottom.
            nums++
        }
        if(nums>target) break;
        r--;
        for (let i = r; i >= l; i--) {
            res.push(matrix[b][i]); // right to left.
            nums++
        } 
        if(nums>target) break;
        b--;
        for (let i = b; i >= t; i--) {
            res.push(matrix[i][l]); // bottom to top.
            nums++
        }
        l++;
    }
    return res;
};
```

30. 包含min函数的栈
```js
var MinStack = function() {
    this.stack = []
    this.minNum = []
};

/** 
 * @param {number} x
 * @return {void}
 */
MinStack.prototype.push = function(x) {
    this.stack.push(x)
    let len = this.minNum.length
    if(len===0) {
        this.minNum.push(x)
    } else if(this.minNum[len-1]>=x) {
        this.minNum.push(x)
    }
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function() {
    let x = this.stack.pop()
    let len = this.minNum.length
    if(x===this.minNum[len-1]){
        this.minNum.pop()
    }
};

/**
 * @return {number}
 */
MinStack.prototype.top = function() {
    let len = this.stack.length
    if(len>0){
        return this.stack[len-1]
    } else return null
};

/**
 * @return {number}
 */
MinStack.prototype.min = function() {
    let len = this.minNum.length
    if(len>0){
        return this.minNum[len-1]
    } else return null
};
```

32 - I. 从上到下打印二叉树
```js
var levelOrder = function(root) {
    if(root === null) return []
    let queue = [root]
    let res = []
    while(queue.length>0){
        let node = queue.shift()
        res.push(node.val)
        if(node.left !== null) queue.push(node.left)
        if(node.right !== null) queue.push(node.right)
    }
    return res
};
```

32 - II. 从上到下打印二叉树 II
```js
var levelOrder = function(root) {
    if(root === null) return []
    let queue = [root]
    let res = []
    let level = 0
    while(queue.length>0){
        res[level] = []
        let levelNum = queue.length; // 第level层的节点数量
        while (levelNum--) {
            const front = queue.shift();
            res[level].push(front.val);
            if (front.left) queue.push(front.left);
            if (front.right) queue.push(front.right);
        }

        level++;
    }
    return res
};
```
35. 复杂链表的复制
还有点问题，先合并再拆开，链表深克隆，深度优先遍历
```js
var copyRandomList = function(head) {
    const map = {};
    function recur(node){
        if(!node){
            return null
        }
        if(map[node.val]){
            return map[node.val]
        }
        let res = new Node(node.val);
        map[node.val] = res;
        res.next = recur(node.next);
        res.random = recur(node.random)
        return res
    }
    return recur(head)
};
```

39. 数组中出现次数超过一半的数字
```js
var majorityElement = function(nums) {
    nums.sort((m,n)=>m-n)
    return nums[Math.floor(nums.length/2)]
};
```

40. 最小的k个数
```js
var getLeastNumbers = function(arr, k) {
    return arr.sort((m,n)=>m-n).slice(0,k)
};
```

47. 礼物的最大价值
动态规划
```js
var maxValue = function(grid) {
    let m = grid[0].length
    let n = grid.length
    let dp = [[]]
    dp[0][0]=grid[0][0]
    for(let i=1; i<m;i++){
        dp[0][i]=dp[0][i-1]+grid[0][i]
    }
    for(let i=1; i<n;i++){
        dp.push([])
        dp[i][0]=dp[i-1][0]+grid[i][0]
    }
    for(let i=1; i<n;i++){
        for(let j=1; j<m;j++){
            dp[i][j]=Math.max(dp[i-1][j],dp[i][j-1])+grid[i][j]
        }
    }
    return dp[n-1][m-1]
};
```
48. 最长不含重复字符的子字符串
```js
var lengthOfLongestSubstring = function(s) {
    if (s.length === 0) return 0
    let obj = {}
    let cur = [0]
    for (let i = 0; i < s.length; i++) {
        if (s[i] in obj) {
            cur[i + 1] = Math.min(i - obj[s[i]], cur[i] + 1)
        } else {
            cur[i + 1] = cur[i] + 1
        }
        obj[s[i]] = i
    }
    return Math.max(...cur)
};
```

49. 丑数
```js
var nthUglyNumber = function(n) {
        let p2=0,p3=0,p5=0;
        let dp = []
        dp[0]=1;
        for(let i=1;i<n;i++){
            dp[i]=Math.min(dp[p2]*2,dp[p3]*3,dp[p5]*5);
            if(dp[i]==dp[p2]*2) p2++;
            if(dp[i]==dp[p3]*3) p3++;
            if(dp[i]==dp[p5]*5) p5++; 
        }
        return dp[n-1];
};
```
50. 第一个只出现一次的字符
```js
var firstUniqChar = function(s) {
    let arr = s.split('')
  for(let i=0;i<s.length;i++){
      if(arr.indexOf(arr[i])===arr.lastIndexOf(arr[i])){
          return arr[i]
      }
  }
    return " "
};
```

52. 两个链表的第一个公共节点
```js
var getIntersectionNode = function(headA, headB) {
    if(headA === null || headB === null) return null
    let node1 = headA
    let node2 = headB
    let flag = 0
    while(node1 !== node2){
        if(node1.next === null) {
            node1 = headB
            flag++
        }else{
            node1=node1.next
        }
        if(node2.next === null) {
            node2 = headA
        } else {     
            node2=node2.next
        }
        if(flag>1) return null
    }
    return node1
};
```

53 - I. 在排序数组中查找数字 I
```js
var search = function(nums, target) {
    let index = nums.indexOf(target)
    if(index === -1){
        return 0
    }
    return nums.lastIndexOf(target)+1 - index
};
```

53 - II. 0～n-1中缺失的数字
```js
var missingNumber = function(nums) {
    let low = 0
    let high = nums.length - 1
    while(low<high){
        let mid = Math.floor((low+high)/2)
        if(nums[mid] != mid){
            high = mid - 1
        } else {
            low = mid + 1;
        }
    }
     return nums[low] == low ? nums[low]+1 : nums[low]-1;
};
```
54. 二叉搜索树的第k大节点
```js
var kthLargest = function(root, k) {
    let res=0
    let n=0
    dfs(root,k);
    return res;
    function dfs(root,k){
        if(root === null) return 
        if(root.right) dfs(root.right,k);
        n++;
        if(n==k) res=root.val;
        if(root.left) dfs(root.left,k);
        return ;
    }
};
```
55 - I. 二叉树的深度
```js
var maxDepth = function(root) {
    if(root === null) return 0
  if (root.left === null && root.right === null) {
      return 1
  } 
  if (root.left !== null && root.right  === null)  {
      return maxDepth(root.left)+1
  }
  if (root.left === null && root.right !== null)  {
      return maxDepth(root.right)+1
  }
  if (root.left !== null && root.right !== null)  {
      return Math.max(maxDepth(root.left),maxDepth(root.right))+1
  }
};
```
55 - II. 平衡二叉树
```js
var isBalanced = function(root) {
    return recur(root) !== -1
    function recur(root){
          if (root == null) return 0;
        let left = recur(root.left);
        if(left == -1) return -1;
        let right = recur(root.right);
        if(right == -1) return -1;
        return Math.abs(left - right) < 2 ? Math.max(left, right) + 1 : -1;
    }
};
```

56 - I. 数组中数字出现的次数
```js
var singleNumbers = function(nums) {
    let res = 0
    for (let i=0;i<nums.length;i++) {
        res ^= nums[i]
    }
    let flag = res & (-res)
    let res1 = 0
    let res2 = 0
    for (let i=0;i<nums.length;i++) {
        if(nums[i]&flag){
            res1 ^= nums[i]
        } else {
            res2 ^= nums[i]
        }
    }
    return [res1,res2]
};
```
56 - II. 数组中数字出现的次数 II
```js
var singleNumber = function(nums) {
     let a=0,b=0;
        for (let i=0;i<nums.length;i++) {
            b = b ^ nums[i] & ~ a;
            a = a ^ nums[i] & ~ b;
        }
        return b;
};
```

57. 和为s的两个数字
```js
var twoSum = function(nums, target) {
    let obj = {}
    for(let i=0;i<nums.length;i++){
        if(nums[i] in obj){
            return [nums[i], obj[nums[i]]]
        } else {
            obj[target - nums[i]] = nums[i]
        }
    }
};
```

面试题57 - II. 和为s的连续正数序列
```js
var findContinuousSequence = function(target) {
    let start = 1
    let end = 1
    let sum = 0
    let res = []
    while(start<=target/2){
        if(sum<target){
            sum += end
            end++
        } else if(sum > target){
            sum -=start
            start++
        } else {
            let arr = []
            for(let i=start;i<end;i++){
                arr.push(i)
            }
            res.push(arr)
            sum -= start
            start++
        }
    }
    return res
};
```
58 - I. 翻转单词顺序
```js
var reverseWords = function(s) {
  return s.split(' ').reverse().filter(x=>x!='').join(' ')
};
```

58 - II. 左旋转字符串
```js
var reverseLeftWords = function(s, n) {
  return s.substr(n,s.length) + s.substr(0,n)
};
```

59 - I. 滑动窗口的最大值
```js
var maxSlidingWindow = function(nums, k) {
    if (nums.length === 0) return nums
    let arr = []
  arr.push(Math.max(...nums.slice(0,k)))
    for(i=1;i<nums.length-k+1;i++){
        if(nums[i-1]===arr[i-1]){
            arr.push(Math.max(...nums.slice(i,k+i)))
        } else {
            arr.push(Math.max(arr[i-1],nums[i+k-1]))
        }
  }
    return arr
};
```

60. n个骰子的点数
```js
var twoSum = function(n) {
    let dp = []
    dp[1]=[0,1,1,1,1,1,1]
        for (let i = 2; i <= n; i ++) {
            for (let j = i; j <= 6*i; j ++) {
                for (let cur = 1; cur <= 6; cur ++) {
                    if (j - cur <= 0) {
                        break;
                    }
                    if(!dp[i]) dp[i] = []
                    if(!dp[i][j]) dp[i][j] = 0
                    if(!dp[i-1][j-cur]) dp[i-1][j-cur] = 0
                    dp[i][j] += dp[i-1][j-cur];
                }
            }
        }
        let all = 6**n;
        let ret = [];
        for (let i = n; i <= 6 * n; i ++) {
            ret.push(dp[n][i] / all);
        }
        return ret;
};
```
61. 扑克牌中的顺子
```js
var isStraight = function(nums) {
    nums.sort((m,n)=>m-n)
    let res = 0
    for(let i=0;i<4;i++){
        if(nums[i]===0) {
            res++
        } else if((nums[i+1]-nums[i])===0) {
            return false
        } else {
            res = res-(nums[i+1]-nums[i])+1
        }
    }
    return res>=0
};
```
63. 股票的最大利润
```js
var maxProfit = function(prices) {
  let min = prices[0]
  let dp = []
  for(let i=1;i<prices.length;i++){
      dp[i-1] = prices[i]-min
      min = Math.min(min,prices[i])
  }
    let res = Math.max(...dp)
    return res>0?res:0
};
```

64. 求1+2+…+n
```js
var sumNums = function(n) {
    n && (n += sumNums(n-1));
    return n;
};
```
65. 不用加减乘除做加法
```js
var add = function(a, b) {
        if(a == 0) return b;
    if(b == 0) return a;
    return add(( a ^ b ),((a & b) << 1));
};
```

66. 构建乘积数组
```js
var constructArr = function(a) {
    let preArr = []
    let afterArr = []
    let pre = 1
    let after = 1
    for(let i=0;i<a.length;i++){
        preArr.push(pre)
        pre *= a[i]
        afterArr.push(after)
        after *= a[a.length-i-1]
    }
    let res = []
    for(let i=0;i<a.length;i++){
        res.push(preArr[i]*afterArr[a.length-i-1])
    }
    return res
};
```
68 - I. 二叉搜索树的最近公共祖先
此题编辑器不可以选js
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
            while (root!=null){
            if (p.val<root.val && q.val<root.val){
                root=root.left;
            }else if (p.val>root.val && q.val>root.val){
                root=root.right;
            }else{
                break;
            }
        }
        return root;
    }
}
```
68 - II. 二叉树的最近公共祖先
不可选js
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
           if(root==null || root==p || root==q)
        return root;
    
    TreeNode leftNode=lowestCommonAncestor(root.left,p,q);
    TreeNode rightNode=lowestCommonAncestor(root.right,p,q);

    if(leftNode==null)
        return rightNode;
    if(rightNode==null)
        return leftNode;

    return root;

    }
}
```