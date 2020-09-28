# 169. Majority Element


Share
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.
You may assume that the array is non-empty and the majority element always exist in the array.



##### Example 1:

Input: [3,2,3]  
Output: 3

##### Example 2:
Input: [2,2,1,1,1,2,2]  
Output: 2


### 1. hash-table

> 1. hash table 형식으로 만든다 { 3 : 0, 2 : 1, 3 : 2 }
> 2. obj의 최댓값을 구한 후 해당 key를 리턴해준다.

~~~javascript

/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {

    let obj = {};
    let answer = 0;
    for(let i=0; i< nums.length; i++) {
        if(obj.hasOwnProperty(nums[i])) {
            obj[nums[i]] += 1;
        } else {
            obj[nums[i]] = 1;
        }
    }

    for(let el in obj) {
        if(obj[el] == Math.max(...Object.values(obj))) {
            answer = el;
        }
    }

    return answer;

};
~~~




### 2. sort     


~~~javascript   

/**
 * @param {number[]} nums
 * @return {number}
 */

var majorityElement = function(nums) {
    nums.sort((a,b) => a - b);
    return nums[Math.floor(nums.length/2)];
}; 

~~~
