# Recursion

**문제 풀이시 고려사항**
1. 조건에 맞지 않는 경우 (불가능한 경우)  => return

2. 정답을 찾은 경우  

3. 재귀 호출을 하는 경우 (다음의 경우를 실행하는 경우)  



#### baekjoon #9095
1. sum < 0 작으면 불가능한 경우 => return

2. sum == 0 조건을 찾은 경우 count ++

3. 재귀를 해야하는 경우
[1,2,3] 배열이 for문을 돌면서 0이 될때까지 해당 조건을 찾아간다.

~~~javascript
function solution (n) {

    let count = 0;
    let array = [1,2,3];
    let recur = (sum) => {
        console.log("sum >> " , sum);
        if(sum < 0) return;
        if(sum == 0) {
            count ++;
            return;
        }

        for(let i =0; i< array.length; i++) {
            recur(sum-array[i])
        }

    };
    recur(n);

    console.log("count >> " , count);

    return count;
};

solution(7);
~~~

