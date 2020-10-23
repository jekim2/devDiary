# Closure



```
클로저 = 함수  + 렉시컬 환경(함수를 둘러싼 환경)
```



클로저란 함수와 렉시컬 환경으로 이루어진 것이라고 볼 수 있다. **외부함수에 의해 반환되는 내부함수**를 의미한다. 간단히 말해서 이미 생명주기가 끝난 외부함수의 변수를 참조하는 함수를
클로저라고 한다.




  
~~~javascript
  let name = "Warning";
  function outer() {
    let name = "Closure";
    return function inner() {
      console.log(name);
    }
  }
let callFunc = outer();
callFunc();

~~~
  
  
  
위 코드에서 callFunc를 클로저라고 볼 수 있다. 여기서 찍히는 값은 Warning이 아니라 Closure 라는 값이다.  
즉 outer라는 함수의 context속에 속해있는 변수를 참조하는 것이다.
  
<<면접>>
클로저의 정의를 말하고 자바스크립트에서 왜 모든 함수가 클로저 설명.

  
#### 클로저의 활용
