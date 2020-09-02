# CORE_JAVASCRIPT
javascript 기본 문법과 반드시 알아야 할 기본개념을 정리하는 세션입니다.  



&#128525;   목차  


[1.객체](#객체)     
[2.가비지 컬렉션](#gabage-collection)  
[3.자료구조와 자료형](#자료구조와-자료형)
- 자료형(#§-원시형)  
- 숫자형  
- 문자열(#§-)  



## 객체


**§ 심볼형**  
심볼형은 ES6에서 도입한 새로운 데이터 타입이다. 객체의 프로퍼티는 문자열 또는 심볼로 구성된다. 심볼은 **고유한 식별자**를 만들고 싶을 때 사용한다.  
심볼은 `Symbol()`생성자로 만들 수 있다. 

~~~javascript

const test = Symbol('Hi~!!!');
const test2 = Symbol('Hi~!!!');
test === test2 // false

~~~

#### § 숨김 프로퍼티
숨김 프로퍼티는 외부에서 사용할 수 없는 프로퍼티를 의미한다. 
~~~javascript

let test = {
  grade : 100
};

let name = Symbol('name');

test[name] = 'jogo';

~~~

#### § `{}` => []통해 심볼형 키를 만들어야 한다.
~~~javascript

let name = Symbol('name');
let test = {
  grade : 100,
  [name] : 'jojo'
 };
 
~~~

#### § for...in 에서 배제
키가 심볼인 프로퍼티는 for...in 반복문에서 배제된다.
but , Object.assign 프로퍼티는 배제하지 않는다.

~~~javascript

let name = Symbol('name');
let test = {
  grade : 100,
  [name] : 'jojo'
 };
 
let obj = Object.assign({}, test);
console.log(obj);		// { grade : 100, Symbol(name) : 'jojo' };
 
~~~



#### § 전역 심볼
심볼은 이름이 같더라도 모두 별개로 취급한다. 이름이 같은 심볼 프로퍼티를 찾을 때 전역 심볼을 사용하면 된다.  
`Symbol.for(key)` 는 심볼이 없는 경우 새로운 심볼을 생성하거나 심볼을 찾을 때 사용된다.  
반면에 `Symbol.keyFor(sym)` 은 심볼을 통해 이름을 찾을 때 사용된다.

전역심볼이 아닌 모든 심볼은 `description` 프로퍼티에 있다.


~~~javascript

let test = Symbol.for('name');
let test2 = Symbol.for('name');
let test3 = Symbol.for('password');
let test4 = Symbol('email');

test === test2   	// true

Symbol.keyFor(test)	// name
Symbol.keyFor(test3)	// password

// description 프로퍼티
test4.description 	// email

~~~





## 자료구조와 자료형

#### § 원시형
원시형(기본값) - `문자` , `숫자`, `bigint`, `boolean`, `symbol`, `null`, `undefined`  

참조형 - `객체`(Array, fucntion, Date, RegExp, Map, Set)

`null` 과 `undefined`를 제외한 제외한 원시형에는 다양한 메소드를 호출할 수 있다.


#### § 숫자형
자바스크립트의 숫자형은 두가지 자료형을 지원하는데, 하나는 일반적인 숫자(IEEE-764 부동소수점 숫자 형식) , BigInt 지원한다.

- 0이 많이 붙은 숫자는 0의 갯수 뒤에 `e`를 추가해준다. e뒤의 숫자는 0의 갯수를 의미한다.
~~~javascript

123e6	// 123000000
123e-6	// 0.000123

~~~


- 16진수는 `0x`, 2진수는 `0b`, 8진수는 `0o` 를 사용해 표현하며 대소문자를 가리지 않는다.
~~~javascript
 
 /** 16진수 **/
 0x0000ff	// 255
 0x0000FF	// 255
 
 /** 2진수, 8진수 **/
 let x = 0b11111111	// 255의 2진수
 let y = 0o377		// 255의 8진수
 x == y 		// true
 
~~~

#### § toString() 
toString() 괄호안에 변환하고자 하는 진법을 넣어주면 된다. default는 10진수이다.
~~~javascript

 let num = 255;
 num.toString(16)	// ff
 num.toString(2)	// 11111111

~~~
  
    
    
#### § 어림수

`Math.floor()` - 첫째자리에서 버림

`Math.ceil()`  - 첫째자리에서 올림

`Math.round()` - 첫째자리에서 반올림    

`toFixed(n)` - n번째자리까지 표현 n+1자리에서 반올림하여 문자형을 반환  

`Math.trunc()` - 소수점 아래 버림 (internet explorer 지원 X)   
 
 *cf. 기타 Math 함수 *
 `Math.random()` - 0 ~ 1 사이의 난수를 반환    
 `Math.max(a,b,c)` - 인수 중 최대 값 반환    
 `Math.min(a,b,c)` - 인수 중 최솟 값 반환   
 `Math.pow(n,power` - n을 power번 거듭제곱한 수를 반환 ex. Math.pow(2,10)	// 1024  
    
      
  
#### § isNaN && isFinite
Infinity, -Infinity, NaN 모두 숫자형에 속하지만 정상적인 숫자는 아니다. 따라서 이를 구분하기 위해 isNaN, isFinite가 있어야 한다.

`isNaN()` - 인수를 숫자로 변환한 후 NaN인지 체크  
`isFinite()` - 인수를 숫자로 변환한 후 숫자가 NaN , Infinity, -Infinity 인지 체크 (일반숫자인 경우 true반환)

~~~javascript

  isNaN(NaN)	// true 
  isNaN("test")	// true
  isFinite(NaN)	// false
  isFinite(3)	// true
  
~~~

   
     
     
#### § parseInt ** parseFloat  

숫자와 문자열이 혼용해서 쓰여졌을 때 ex. `40px` , `12pt` 등과 같은 숫자와 단위가 함께 쓰여졌을 때 숫자를 읽는 도중 숫자가 아니라는 판단이
되었을 때 , `숫자까지 반환` 해 준다.  
parseInt는 정수, parseFloat는 부동 소수점 숫자를 반환해 준다. parseInt 두번째 인수를 받을 수 있는데, 진수 문자열을 파싱해준다.  


~~~javascript

 parseInt('100px')	// 100
 parseInt('12.5pt')	// 12.5
 parseInt('0xff', 16)	// 255
 parseInt(11, 2);	// 3	(11의 2진수로 변환)
~~~



#### § 문자열


🖌 **템플릿 리터럴**
`${...}` 이러한 표현식을 템플릿 리터럴이라고 한다. 백틱을 사용하면 문자열을 여러줄에 걸쳐서 작성 할 수 있다.

  
  ~~~javascript
  
    let a = 3 + 5;
    console.log(`a 는  => ${a} `);
    
    let b = ` list : 
    		1,
		2,
		3,
		4
	     `
    
  ~~~
    
  🖌 **이스케이프 문자**  
  모든 특수문자는 역슬래시 `\` 로 시작한다. 

~~~javascript
  
console.log('\\');
console.log('\*');
	
~~~

 🖌 **특정문자에 접근**    
    
 #### § str.charAt(index)

~~~javascript

  let str = "abcde";
  str.charAt(0);	// a
  str.charAt(1);	// b
  str.charAt(str.length-1)	// 마지막 문자
  str[str.length-1]		// 마지막 문자
  
~~~

🖌 **문자열 찾기**  

 #### § str.indexOf(findStr, index)   findStr 은 찾을 문자 , index는 몇번째 인덱스부터 찾을 것을 찾아 index를 반환해 준다.  
 #### § str.lastIndexOf(findStr, index)   lastIndexOf은 뒤에서 부터 해당 문자열을 찾아 index를 반환해 준다.  
 #### § str.includes(findStr,index)   findStr 은 찾을 문자 , index는 몇번째 인덱스부터 찾을 것을 찾아 해당 문자가 있으면 true, 없으면 false를 반환해준다.  
 #### § str.startsWith(findStr)    findStr 해당 문자열로 시작하는지   
 #### § str.endsWith(findStr)       findStr 해당 문자열로 끝나는지  
    
  
  
  🖌 **부분 문자열 찾기**  
    
 #### § str.slice(start, [end])  
   
   문자열을 `start`부터 `end`까지를 반환된다.  end가 생략됬다면 start부터 끝까지 반환된다. 음수라면 끝에서 부터 센다.
   
   ~~~ javascript
   
     let test = "javascript";
     test.slice(0,5)	// javas
     test.slice(0,1)	// j
     test.slice(2)	// vascript
     test.slice(-2, -1)	// p
     
   ~~~

 #### § str.substring(start, [end])  
  
  start와 end사이의 문자열을 반환한다. slice와 달리 end보다 start가 더 커도 상관없다.
  
  
    ~~~ javascript
   
     let test = "javascript";
     test.substring(0,5)	// javas
     test.substring(3,2)	// va
     
    ~~~
     
     
     
 
 
 
 
 #### § str.substr(start, [length])   
 
   start 부터 시작해 length길이만큼 반환해 준다.
   
    ~~~ javascript
   
     let test = "javascript";
     test.substr(2,4)	// vasc
     test.substr(-4,2)	// ri (뒤에서 부터 2
     
    ~~~
     
  

  




  
















객체는 중괄호 {} 를 통해 '키(key) : 값(value)' 쌍으로 구성된 프로퍼티를 여러개 넣을 수 있다.

~~~javascript

let test = new Object();      // '객체 생성자' 문법
let test = {};                // '객체 리터럴' 문법

~~~




**§ delete 연산자**

프로퍼티 삭제하는 delete 연사자는 다음과 같이 표현할 수 있다.

```
delete user.age;
```

**§ 대괄호 표기법**

키 값이 없어도 \[""\] 넣으면 객체의 프로퍼티를 표현할 수 있다.

```
test["user"] = "abc";
```

****§ **계산된 프로퍼티**

객체를 만들 떄 리터럴 안의 프로퍼티가 대괄호로 둘러쌓여 있는 경우, 이를 계산된 프로퍼티라고 한다.

```
let name = "lola";
let obj = {
	[name] : "1"
}
```

**§ 프로퍼티 존재 여부 확인**

in 을 사용하면 프로퍼티 존재 여부를 확인 할 수 있다.

```
"key" in obj
```

**§ 참조에 의한 객체 복사**

객체는 참조에의한 복사를 한다.  예를 들어 설명하면 exam이라는 객체가 있다.  이 댸 exam 객체를 test 객체에  저장해 본다. 그러면 exam 이라는 두 독립된 변수에 exam 과 test가 생긴다. 그러면 두 상자에 각각 math, english의 값이 저장된다. 

객체가 할당된 변수를 복사할 경우, 객체는 복사되지 않고 객체의 참조 값이 복사된다. 따라서 test.math = 100 이라고 할당하고 exam.math를 출력해 보면 exam.math 또한 100이 된다.

```
let exam = {
   math : 50,
   english : 70
};

let test = exam;
```

<table style="border-collapse: collapse; width: 28.0563%; height: 142px;" border="1" data-ke-style="style12"><tbody><tr style="height: 23px;"><td style="width: 100%; height: 23px; text-align: left;"><span style="font-family: AppleSDGothicNeo-Regular, 'Malgun Gothic', '맑은 고딕', dotum, 돋움, sans-serif; color: #000000;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;exam</span></td></tr></tbody></table>

<table style="border-collapse: collapse; width: 100%;" border="1"><tbody><tr><td style="width: 100%; text-align: center;"><span style="font-family: AppleSDGothicNeo-Regular, 'Malgun Gothic', '맑은 고딕', dotum, 돋움, sans-serif; color: #000000;">&nbsp; &nbsp; &nbsp; &nbsp;math : 50 , english : 70<span style="background-color: #f3c000;"></span></span></td></tr></tbody></table>

<table style="border-collapse: collapse; width: 28.1396%; height: 135px;" border="1" data-ke-style="style12"><tbody><tr><td style="width: 100%; text-align: left;"><span style="font-family: AppleSDGothicNeo-Regular, 'Malgun Gothic', '맑은 고딕', dotum, 돋움, sans-serif; color: #000000;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; test</span></td></tr></tbody></table>

**§ 참조에 의한 객체 비교**

두 객체가 동일한 경우, 참을 반환하게 되는데 만약 두 객체가 비워져 있다면 같은 객체라고 볼 수 있을까?

```
let a = {};
let b = {};

console.log( a == b );
```

결과는 false, 두 객체가 모두 비워있다는 점은 같지만 둘은 각각 독립된 객체이므로 같은 값이라고 볼 수 없다.

**§ Object.assign**

독립적인 객체로써, 객체를 복제하고 싶을 때는 Object.assign을 사용하면 된다. 

동작방식은 destination\_obj는 복사하고 싶은 대상인 객체 , test1, test2, test3 은 복사하려는 객체로 나타낸다. 따라서

Object.assign을 사용하면 반복문 없이 객체를 복사할 수 있다.

```
Object.assign(destination_obj , test1, test2, test3)


//Object.assign example
let tester = { name : "sara" };
let tester1 = { per1  : 1 };
let tester2 = { per2 : 2 };

// tester1, tester2 프로퍼티를 복사
Object.assign(tester, tester1, tester2);		// tester = { name : "sara" , per1 : 1, per2 : 2 }

```

만약 tester과 동일한 객체가 있는 경우 기존 값에 덮여씌워 진다.

```
let asg_temp = {
	age : 10,
    name : 'jake'
};

Object.assign(asg_temp, {age : 20 , name : 'jay' });
```

반복문 없이 복사하는 경우

```
let asg_temp = {
	age : 10,
    name : 'jake'
};

let copy = Object.assign({}, asg_temp);
```

## Gabage Collection
한마디로 얘기하자면 **메모리를 관리하는 것** 우리가 함수를 생성하거나 객체등을 만들 때 메모리를 사용합니다. <br> 하지만 우리가 쓰지 않는 데이터는 어떻게 처리할까요?
쓰지 않는 데이터 즉 쓰레기는 삭제한다 라는 것이 기본 원리입니다. 그렇다면 쓰지 않는 데이터는 어떤 기준으로 분리할까요?
바로 도달 가능성(reachability) 입니다. (ex. 전역변수 , 현재 함수의 매개변수나 지역변수 등)

`
let data = { 'name' : 1 };
`  
  
data라는 객체가 있습니다. data는 `name : 1` 이라는 객체를 참조합니다.   
그런데 이때  `data = null` 로 만들어버리면  `name : 1` 이라는 객체에 도달할 수 없게되므로 가비지 컬렉터는 이에 대한 데이터를 메모리에서 삭제합니다.

그렇다면 참조가 2개라면?

`let data = { 'name' :  1 } ;
let copy = data;
data = null; `  
이는 copy를 통해 data에 접근할 수 있으므로 data는 메모리에 남아있습니다.

즉, **데이터가 도달 가능한 상태면 메모리에 남습니다.**

