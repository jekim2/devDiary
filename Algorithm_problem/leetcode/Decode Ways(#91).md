# 62. Unique Paths


##### Share  
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

 

##### Example 1:
![image](https://user-images.githubusercontent.com/71614519/97643674-bbe42700-1a8b-11eb-8329-1e990a441b52.png)
Input: m = 3, n = 7
Output: 28


##### Example 2:
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down


##### Example 3:
Input: m = 7, n = 3
Output: 28

##### Example 4:
Input: m = 3, n = 3
Output: 6

### 1. DP 

1. m, n 0이나 1인 경우 예외처리 

2. m+1, n+1 의 2차원 배열의 1로 채워준 값을 초기 값으로 설정

3. DP는 반복되는 값을 찾아 점화식을 만들어 줘야한다. 

하단의 그림을 통해 반복되는 값을 확인해 본 결과
dp[1][1] = dp[0][1] + dp[1][0]  
dp[1][2] = dp[0][2] + dp[1][1]  
dp[1][3] = dp[0][3] + [1][2]
 ..... 
 
 
이름 점화식으로 만들어 주면 dp[i][j] = dp[i-1][j] + dp[i][j-1]; 결과가 된다.

4. dp배열의 맨 마지막 값이 m,n이 가는 경우의 수.

![image](https://user-images.githubusercontent.com/71614519/97645168-83464c80-1a8f-11eb-85e5-3895dddce764.png)  
     

~~~javascript
/**
 * @param {number} m
 * @param {number} n
 * @return {number}
 */
var uniquePaths = function(m, n) {

    if(m == 0 || n == 0) return 0;
    if(m == 1 || n == 1) return 1;

    let dp = new Array(n+1).fill(1).map((x) => new Array(m+1).fill(1));

    for(let i=1; i< n; i++) {
        for(let j=1; j< m; j++) {
          // console.log(i,j)
            dp[i][j] = dp[i-1][j] + dp[i][j-1];
        }
    }
    return dp[n-1][m-1];
};
~~~


### 2. RECUSIVE
>> 반복되는 경우를 생각해보면 오른쪽으로 갈 수 있는지, 아래로 내려갈 수 있는지 여부이다.
>> 오른쪽, 아래로 갈 수 없다면 함수를 빠져나간다고 생각하면 된다.
ex. "2263"
1. 1개를 잘라서 decoding 가능한가, 2개를 잘라서 decoding가능한가 2가지 경우의 수 고려.
2. 1개의 숫자를 잘라서 decoding가능한 경우 0이상인 경우
3. 2개의 숫자를 잘라서 decoding가능한 경우 10이상 26이하인 경우


![image](https://user-images.githubusercontent.com/35910264/97376530-7ff76900-18b5-11eb-9193-3a7511753c85.png)

숫자 "2"까지 잘라서 가능한 경우 dp배열의 index 1에 저장
숫자 "22"까지 잘라서 decoding 가능한 경우 dp 배열의 index 2에 저장
"2263"의 총 경우 "226" 까지 decoding가능한 경우 + "3"추가 했을 때 가능한 경우의 수 => dp[dp.length-1]



~~~javascript
/**
 * @param {string} s
 * @return {number}
 */
var numDecodings = function(s) {
    const dp = Array(s.length+1).fill(0);
    dp[0] = 1;
    
    for(let i = 1; i <= s.length; i++) {
        const oneChar = +s.slice(i-1, i);
        const twoChar = +s.slice(i-2, i);

        if(oneChar > 0) dp[i] = dp[i-1];
        if(twoChar >= 10 && twoChar <= 26) dp[i] += dp[i-2]
    }    

    return dp[s.length];
};

~~~


