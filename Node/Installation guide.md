
## ⛏installation

**✔ express / express-session**
- express :  Node JS의 `Express framework`를 사용하여 Node JS 서버를 구축  [(express공식사이트)](https://www.notion.so/server-53b3fa486740425b83d42f9ebe93af4c)
- express-session 


 ```txt
npm install express
npm install express-session
```
  
<br>

**✔ mongoose / dotenv** 
- mongoose : nodejs 환경에서 사용하는 MongoDB기반 라이브러리
- dotenv : 환경변수를 파일에 넣고 사용할 수 있는 개발도구


 ```txt
npm install mongoose
npm install dotenv
```

<br>

**✔ nodemon**
- nodemon : 코드를 변경할 때마다 서버를 자동으로 재시작하게 해주는 도구


 ```txt
npm install nodemon
```

<br>

**✔ Cors**  
- cors (cross-origin-resource-sharing) : 도메인이나 포트가 다르기 때문에 발생한다. (네트워크 요청을 할 때 주소가 다른 경우)  
- 서버, 클라이언트가 분리되어 있는 앱에서는 cross-orgin Http 요청을 서버에서 승인해 주는 것이 좋다.  

```txt
npm install cors
```
<br>

**✔ bcrypt**
- 비밀번호를 데이터 베이스에 저장할 때 아무런 가공되지 않는 텍스트로 저장하면 보안상 위험하므로 단방향 해시함수를 지원해주는 bcrypt를 사용.  
- bcrypt는 의존성이 많아, 그것보다 가벼운 `bcryptjs`를 설치 [https://velog.io/@nomadhash/TIL-bcrypt.-비밀번호를-암호화-해봅시다-feat.Node-JS](https://velog.io/@nomadhash/TIL-bcrypt.-%EB%B9%84%EB%B0%80%EB%B2%88%ED%98%B8%EB%A5%BC-%EC%95%94%ED%98%B8%ED%99%94-%ED%95%B4%EB%B4%85%EC%8B%9C%EB%8B%A4-feat.Node-JS)
```txt
npm install bcryptjs
```
<br>

**✔ joi**
- 객체 검증을 위한 라이브러리이며 유효성 검사를 위한 express 미들웨어.
```txt
npm install joi
```

<br>

**✔ jsonwebtoken**
- 클라이언트가 사용자 로그인 정보를 지닐 수 있도록 서버에서 토큰 발급을 해야 하는데 JWT토큰을 발급하기
위해서 jsonwebtoken이라는 모듈이 필요.
JWT란 JSON 포맷을 이용해서 사용자 정보를 저장하는 web token
JWT = header + payload + signature로 이루어져있다. 
```txt
npm install jsonwebtoken
```
<br>


**✔ jwt-decode**
- jwt가 암호화 되어있는 것을 풀어주는 모듈
```txt
npm install jwt-token
```

<br>
<br>
## 📕 References
📌 [project guide-line](https://github.com/elsewhencode/project-guidelines/blob/master/README-ko.md)  

📌 [JWT_ex1](https://velopert.com/2389) [JWT_ex2](https://meetup.toast.com/posts/239)

📌 [Schema](https://www.zerocho.com/category/MongoDB/post/59a1870210b942001853e250)

[Passport_naver](https://github.com/naver/passport-naver)
