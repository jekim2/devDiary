# 1. Two Sum
Share
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.



#### Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]
Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]

### 1. brute-force
~~~javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let answer = [];
    for(let i =0; i< nums.length; i++) {
        for(let j = i+1; j< nums.length; j++) {
            if(nums[i] + nums[j] == target) {
                return [i, j];
            }
        }
    }
    
    return answer;
};
twoSum([3,2,3], 6);
~~~
### 2. hash-table    

> 1. hash table 형식으로 만든다 { 3 : 0, 2 : 1, 3 : 2 }
> 2. target - nums = hashTable에 있는지 확인한다.

~~~javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */

var twoSum = function(nums, target) {
    let answer = [];
    let obj = {};
    if (nums.length === 2) return [0, 1];
  
    for(let i =0; i< nums.length; i++) {
      obj[nums[i]] = i;
    }

  
  for(let j =0; j< nums.length; j++) {
   let findTarget =  target - nums[j];
    if(obj.hasOwnProperty(findTarget) && j != obj[findTarget]) {
      return [j, obj[findTarget]];
    }
  }
  return [0,0];
};
~~~
