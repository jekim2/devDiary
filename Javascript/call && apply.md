# call/apply/bind
`this`를 지정하는 3가지 방법이 있다. `call`, `apply`, `bind`이다. 

📌 **call**  
call(this로 사용할 값, 매개변수)
call함수는 모든 함수에서 쓰일 수 있으며 this를 지정할 수 있다.





~~~javascript
  const bruce = {name:"Bruce"};
  const jake = {name : "jake"};
  
  function greet(){
    return `Hello, I'm ${this.name}~!!!`;
  }
  
  greet.call(bruce);        // Hello, I'm bruce~!!!
  greet.call(jake);         // Hello, I'm jake~!!!
~~~


📌 **apply**  
매개변수를 처리하는 방법이 call과 다른데 apply는 매개변수를 배열로 받는다.
~~~javascript

update.apply(bruce,[1995,"actor"];
update.apply(jake,[1996,"testor"];

~~~

~~~javascript

const arr = [1,2,3,4,5];
Math.min.apply(null,arr); // 1
Math.max.apply(null,arr); // 5

~~~
null을 쓴 이유는 Math.min, Math.max가 객체와 관계없이 동작하기 때문이다.

📌 **bind**  
bind를 사용하면 함수의 this값을 영구히 바꿀 수 있다. 
~~~javascript

const updateBruce = update.bind(bruce);
updateBruce(1904,"actor");
updateBruce.call(jake,1274,"testor");

~~~
updateBruce.call 함수가 변하지 않는다는 것을 볼 수 있다.



