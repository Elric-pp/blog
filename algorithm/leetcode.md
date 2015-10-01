## 目录
  1. [moveZeroes](#movezeroes)
  1. [Convert Sorted Array to Binary Search Tree](#convert-sorted-array-to-binary-search-tree)
  1. [Remove Duplicates from Sorted Array](#remove-duplicates-from-sorted-array)
  1. [First Bad Version](#first-bad-version)
  1. [Valid Anagram](#valid-anagram)



## moveZeroes
&nbsp;&nbsp;Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

- For example, 
>&nbsp;&nbsp;given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

- Note:
1. You must do this in-place without making a copy of the array.
2. Minimize the total number of operations.
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
&nbsp;&nbsp;Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length. 

&nbsp;&nbsp;Do not allocate extra space for another array, you must do this in place with constant memory. 
- For example,
> Given input array nums = [1,1,2], Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn’t matter what you leave beyond the new length.

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
&nbsp;&nbsp;You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

&nbsp;&nbsp;Suppose you have n versions [1, 2, …, n] and you want to find out the first bad one, which causes all the following ones to be bad.

&nbsp;&nbsp;You are given an API bool isBadVersion(version) which will return whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

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
&nbsp;&nbsp;Given two strings s and t, write a function to determine if t is an anagram of s.

- For example,
> s = “anagram”, t = “nagaram”, return true. 
> s = “rat”, t = “car”, return false.

- Note: 
  You may assume the string contains only lowercase alphabets.

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
