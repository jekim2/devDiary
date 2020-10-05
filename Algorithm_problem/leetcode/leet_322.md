# 322. Coin change


Share
You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. 
If that amount of money cannot be made up by any combination of the coins, return -1. You may assume that you have an infinite number of each kind of coin.



##### Example 1:
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1

##### Example 2:
Input: coins = [2], amount = 3
Output: -1

##### Example 3:
Input: coins = [1], amount = 0
Output: 0

##### Example 4:
Input: coins = [1], amount = 1
Output: 1

##### Example 5:
Input: coins = [1], amount = 2
Output: 2



### 1. DP (bottom-up)

> 1. dp는 i원을 만들기 위한 동전의 최소 갯수를 amount+1만큼 만들어준다.
> 2. dp[0] = 0 초기값 생성
> 3. dp배열의 길이만큼 coin을 돌려준다.
> 4. 가지고 있는 동전으로 만들 수 있는 경우, 점화식을 만들어준다.  
     ex. dp[1]= 1, dp[2] = 2, dp[3] = Math.min(dp[2] + 1, dp[3]), Math.min(dp[1] + 1, dp[3])

~~~javascript

/**
 * @param {number[]} coins
 * @param {number} amount
 * @return {number}
 */
var coinChange = function(coins, amount) {

  if (amount == 0) return 0;
  
  let dp = new Array(amount + 1).fill(Infinity);  // dp는 i원을 만들기 위한 동전의 최소 갯수를 저장
  
  dp[0] = 0;
  
  for(let i=1 i< dp.length; i++) {
    for(const coin of coins)  {
      // 가지고 있는 동전으로 만들 수 있는 경우
      if(coin <= i) {
        // dp[6] = Math.min(dp[5] + 현재코인(coin) 1개, dp[6])
        dp[i] = Math.min(dp[i-coin] + 1 , dp[i]);
      }
    } 

  }
  
  return dp[dp.length-1] !== Infinity ? dp[dp.length-1] : -1
   
};
~~~



