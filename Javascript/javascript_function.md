## Javascript 함수 정리

### splice (start, deleteCount, item1, item2): 배열, 문자열 원소 삭제, 잘려진 배열을 반환
- array (start, deleteCount, item1, item2);: 배열 원소 삭제

~~~javascript
var array = [0, 1, 2, 3, 4, 5 ];
// 2인덱스부터 3개제거
var resullt = array.splice(2, 3);
// array : [0, 1, 5]
// result : [2, 3, 4]
~~~
### slice (start, deleteCount, item1, item2) : 기존 배열은 변하지 않고, 잘려진 배열을 반환

: 배열, 문자열 원소 삭제
~~~javascript
var array = [0, 1, 2, 3, 4, 5 ];
// 2인덱스부터 3개제거
var resullt = array.plice(2, 3);
// array : [0, 1, 5]
// result : [2, 3, 4]
~~~
