## 目录
  1. [moveZeroes](#movezeroes)
  1. [Convert Sorted Array to Binary Search Tree](#convert-sorted-array-to-binary-search-tree)
  1. [Remove Duplicates from Sorted Array](#remove-duplicates-from-sorted-array)
  1. [First Bad Version](#first-bad-version)
  1. [Valid Anagram](#valid-anagram)
  1. [Maximum Depth of Binary Tree](#maximum-depth-of-binary-tree)
  1. [Delete Node in a Linked List](#delete-node-in-a-linked-list)
  1. [Same Tree](#same-tree)
  1. [Invert Binary Tree](#invert-binary-tree)
  1. [Lowest Common Ancestor of a Binary Search Tree](#lowest-common-ancestor-of-a-binary-search-tree)
  1. [Number of 1 Bits](#number-of-1-bits)
  1. [Contains Duplicate](#contains-duplicate)


## moveZeroes
> Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

> For example, 
>> given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].
>
> Note:
> 1. You must do this in-place without making a copy of the array.
> 2. Minimize the total number of operations.

```javascript
/**
* @param {number[]} nums
* @return {void} Do not return anything, modify nums in-place instead.
*/
var moveZeroes = function(nums) {
  for (var i = 0, k = 0; k < nums.length; k++) {
     if (nums[i] === 0) {
        nums.push(nums.splice(i,1)[0])
        continue;
     } else {
       i++;
     }
  }
};
```
***


## Convert Sorted Array to Binary Search Tree
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {number[]} nums
 * @return {TreeNode}
 */
var sortedArrayToBST = function(nums) {
    return Buildtree(nums, 0, nums.length-1)
};


function Buildtree(nums, start, end) {
  if( start=== end) return new TreeNode(nums[start]);
  if (start > end) return null;
  var mid = Math.floor((start + end) / 2);
  var node = new TreeNode(nums[mid]);
  node.left = Buildtree(nums, start, mid-1);
  node.right = Buildtree(nums, mid+1, end)
  return node;
}
```


***

## Remove Duplicates from Sorted Array
> Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length. 

> Do not allocate extra space for another array, you must do this in place with constant memory. 

> For example,
>> Given input array nums = [1,1,2], Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn’t matter what you leave beyond the new length.

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    var k = 1;
    for (var i = 1; i < nums.length; ++i) {
        if(nums[i] !== nums[i-1]) {
            nums[k++] = nums[i]
        }
    }
    return k;
};
```
***


## First Bad Version
> You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

> Suppose you have n versions [1, 2, …, n] and you want to find out the first bad one, which causes all the following ones to be bad.

> You are given an API bool isBadVersion(version) which will return whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

```javascript
 /**
 * Definition for isBadVersion()
 * 
 * @param {integer} version number
 * @return {boolean} whether the version is bad
 * isBadVersion = function(version) {
 *     ...
 * };
 */

/**
 * @param {function} isBadVersion()
 * @return {function}
 */
var solution = function(isBadVersion) {
    /**
     * @param {integer} n Total versions
     * @return {integer} The first bad version
     */
    return function(n) {
        var left = 0;
        var right = n;
        while (right-left !== 1) {
            var mid = parseInt((left + right) / 2);
            if (isBadVersion(mid)) {
                right = mid;
            } else {
                left = mid;
            }
        }
        return right;
    };
};
```
***


## Valid Anagram
> Given two strings s and t, write a function to determine if t is an anagram of s.

> For example,
>> s = “anagram”, t = “nagaram”, return true. 
>> s = “rat”, t = “car”, return false.

> Note: 
> You may assume the string contains only lowercase alphabets.

```javascript
  /**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function(s, t) {
    if (s.length !== t.length) return false;
    s = s.split("").sort().join("");
    t = t.split("").sort().join("");
    return s === t;
};
```


## Maximum Depth of Binary Tree

> Given a binary tree, find its maximum depth.

> The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
  return root ? Math.max(maxDepth(root.left), maxDepth(root.right))+1 : 0;
};
```

## Delete Node in a Linked List
> Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

> Supposed the linked list is 1 -> 2 -> 3 -> 4 and you are given the third node with value 3, the linked list should become 1 -> 2 -> 4 after calling your function.

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} node
 * @return {void} Do not return anything, modify node in-place instead.
 */
var deleteNode = function(node) {
    var nextNode = node.next;
    node.val = nextNode.val;
    node.next = nextNode.next;
};
```

## Same Tree
> Given two binary trees, write a function to check if they are equal or not.

> Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

```
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function(p, q) {
    if (p===null && q===null) return true;
    if (p===null || q===null ) return false;
    return p.val === q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right); 
};
```



## Invert Binary Tree 
> Invert a binary tree.
>> 
           4
         /   \
        2     7
       / \   / \
      1  3  6   9
>
> to
>> 
             4
           /   \
          7     2
         / \   / \
        9  6  3   1
>
> Trivia:
    This problem was inspired by this original tweet by Max Howell:
>> Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so fuck off.

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {TreeNode}
 */
var invertTree = function(root) {
    if (root === null ) return root;
    var tmp = root.left;
    root.left = invertTree(root.right);
    root.right = invertTree(tmp);
    return root;
};
```


## Lowest Common Ancestor of a Binary Search Tree
>Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

>According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”
>>```
>>        _______6______
>>       /              \
>>    ___2__          ___8__
>>   /      \        /      \
>>   0      _4_     7        9
>>         /   \
>>         3   5
>>```
>
>For example, the lowest common ancestor (LCA) of nodes 2 and 8 is 6. Another example is LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */
var lowestCommonAncestor = function(root, p, q) {
    if (p.val>root.val && q.val>root.val)
       return lowestCommonAncestor(root.right, p, q);
    
    if (p.val<root.val && q.val<root.val)
       return lowestCommonAncestor(root.left, p, q);
    
    return root;
};
```


## Number of 1 Bits

> Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

> For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.


```javascript
/**
 * @param {number} n - a positive integer
 * @return {number}
 */
var hammingWeight = function(n) {
    var count = 0;
    n = n.toString(2);
    for (var i = 0; i < n.length; i++) {
        if(n[i] === "1") count++;
    }
    return count;
};
```

## Contains Duplicate 

> Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
    var tpl = {};
    for (var i = 0; i < nums.length; i++) {
        tpl[nums[i]] = tpl[nums[i]] + 1 || 1;
        if (tpl[nums[i]] > 1) return true;
    }
    return false;
};
```