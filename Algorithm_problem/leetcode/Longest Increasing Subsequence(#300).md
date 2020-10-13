# 300. Longest Increasing Subsequence


##### Share  
Given an unsorted array of integers, find the length of longest increasing subsequence.

##### Example 1:
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.




### 1. DP (bottom-up)

> 1. dp s의 길이 + 1 만큼 false초기값으로 만든다.
> 2. 증가수열이라는 의미는 ex. 10,9,2,5 에서 (2,5) 가 해당된다. 
     따라서 nums[i] > nums[j] 라는 의미는 nums[i]가 5일 때 nums[j] 10,9,2가 돌면서 nums[i] > nums[j]가 되는 경우가 증가하는 수열이 된다.
> 3.  dp[i] = Math.max(dp[j] + 1, dp[i]) 점화식은 아래 표로 인해 변할 수 있다.

| index 	| 0  	| 1 	| 2 	| 3 	| 4 	| 5 	| 6   	| 7  	|
|-------	|----	|---	|---	|---	|---	|---	|-----	|----	|
| nums  	| 10 	| 9 	| 2 	| 5 	| 3 	| 7 	| 101 	| 18 	|
| DP    	| 1  	| 1 	| 1 	| 2 	| 2 	| 4 	|  4  	| 3  	|

> 4. 가장 긴 길이라고 했으므로 dp배열의 가장 큰 값을 리턴해준다.


~~~javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var lengthOfLIS = function(nums) {
  
  if(nums == null || nums.length == 0) return 0;  // 예외처리

    let dp = new Array(nums.length).fill(1);

    for(let i= 0; i< nums.length; i++) {
        for(let j =0; j < i; j++) {
          if(nums[i] > nums[j]) {
            dp[i] = Math.max(dp[j] + 1, dp[i]);
          }
        }
    }
    return Math.max(...dp);
  };
~~~


