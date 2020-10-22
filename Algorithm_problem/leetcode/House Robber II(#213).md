# 213. House Robber II


##### Share  
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

 

##### Example 1:
Input: nums = [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.

##### Example 2:
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.


### 1. DP (bottom-up) 
>> ex. [4,2,2,4] 이라고 했을 때 처음과 끝이 이어져있는 원형 하우스라고 생각하면 된다.   
위의 배열은 0번째 요소 배열과 마지막요소 배열을 합한값이 제일 큰 값이지만, 처음과 끝이 이어져있다고 하였으므로  
옆집이라고 볼 수 있다. 따라서 처음요소 제거 [2,2,4] 와 마지막 요소 제거 [4,2,2] 의 DP값 중 가장 큰 값을 리턴해 주면된다.   

> 1. 배열 길이 0,1,2에 대한 예외   
> 2. 첫번째 요소를 뺀 배열 num1 마지막요소를 뺀 배열 nums2의 dp 값을 구해준다.  
> 3. dp1 = [0,2,0,0] 첫번째 요소에는 0을 두번째 요소에는 nums1의 0번째 값을 넣어준다.  
> 4. nums1 = [2,2,4]  
     dp1[2] = Math.max(dp1[0]+nums1[1], dp1[1])   -> dp1 = [0,2,2,0]   
     dp1[3] = Math.max(dp1[1]+nums1[2], dp1[2])   -> dp1 = [0,2,2,6]  
          
> 5. nums2 = [4,2,2]  
     dp2 = [0,4,0,0] 첫번째 요소에는 0을 두번째 요소에는 nums2의 0번째 값을 넣어준다.  
     dp2 = Math.max(dp2[0]+nums2[2], dp2[1])      -> dp2 = [0,4,4,0]  
     dp3 = Math.max(dp2[1]+nums2[2], dp2[2])      -> dp2 = [0,4,4,6]  
따라서 6의 값이 리턴되는 원리.  


~~~javascript
/**
 * @param {number[]} nums
 * @return {number}
 */

var rob = function(nums) {
  
  if(nums.length == 0) return 0;
  
  if(nums.length == 1) return nums[0];
  
  if(nums.length == 2) return Math.max(...nums);
  
  
  let nums1= nums.slice(1, nums.length);
  
  let nums2 = nums.slice(0,nums.length-1);
  
  let dp1 = [];
  dp1[0] = 0;
  dp1[1] = nums1[0];
  
  let dp2 = [];
  dp2[0] = 0;
  dp2[1] = nums2[0];
 
  for(let i=2; i<= nums1.length; i++) {
      dp1[i] = Math.max(dp1[i-1], nums1[i-1] + dp1[i-2]);
  }
  
  for(let i=2; i<= nums2.length; i++) {
      dp2[i] = Math.max(dp2[i-1], nums2[i-1] + dp2[i-2]);
  }
  
  return Math.max(dp1[dp1.length-1], dp2[dp2.length-1]);
};

~~~


<<다른 풀이>>

