# 139. Word Break


##### Share  
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words,
determine if s can be segmented into a space-separated sequence of one or more dictionary words.

- The same word in the dictionary may be reused multiple times in the segmentation.
- You may assume the dictionary does not contain duplicate words.

##### Example 1:
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".

##### Example 2:
Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.

##### Example 3:
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false



### 1. DP (bottom-up)

> 1. dp s의 길이 + 1 만큼 false초기값으로 만든다.
> 2. dp[0] = true 초기값 생성
> 3. wordDict 배열은 {'leet', 'code'} 형식으로 변환한다.
> 4. s의 길이를 잘라 비교해준다. 
     ex. l, (le, e), (lee, ee, e), (leet, eet, et, t) ....
> 5. 해당 단어가 있는 경우 dp[end]를 true로 바꿔주고 다음 단어를 찾아 준다.
> 6. 마지막 dp가 true인지 false인지 return.
> <img src="https://user-images.githubusercontent.com/35910264/95743811-49bec480-0ccd-11eb-8558-0d9a0db5c3ce.jpg" width="300" height="200">




~~~javascript
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {boolean}
 */
var wordBreak = function(s, wordDict) {
  
  if(wordDict == null || wordDict.length == 0) return false;
  
  let dp = new Array(s.length + 1).fill(false);
  dp[0] = true;
  
  let wordSet = new Set(wordDict);
  
  // console.log("wordSet >> " , wordSet);
  
  for(let start = 1; start <= s.length; start ++) {
    for(let end = 0; end < start; end ++) {
      let word = s.substring(start, end);
      
      // console.log("word >> " , start, end, word);
      
      if(dp[end] && wordSet.has(word)){
        dp[start] = true;
        break;
      }
    }
  }
  
  // console.log(dp);
  return dp[s.length];
};
~~~


