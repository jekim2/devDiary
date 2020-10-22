# 💡 mongoose를 이용한 MongoDB 연동

[1.MongoDB](#mongodb)     
[2.mongoose](#mongoose)  
[3. 데이터베이스의 스키마와 모델](#데이터베이스의-스키마와-모델)

##  💡MongoDB
noSQL 데이터 베이스이다. 새로 등록된 데이터 형식이 바뀌더라도 기존 데이터를 수정 할 필요가 없다.   
다른 스키마를 가진 문서들이 한 컬렉션에서 공존할 수 있다.

`스키마`는 컬렉션에 들어가는 필드가 어떤 형식인지 정의하는 것이며 `컬렌션`은 여러문서가 들어잇는 곳을 의미한다.    

ex. 데이터 형식이 바뀌더라도 기존 데이터를 수정X

~~~javascript

{
  "_id":"5f7c942199a06037348dcdf8",
  "email":"test@gmail.com",
}
{
  "_id":"5f7c942199a06037348dcdf8",
  "email":"test@gmail.com",
  "password" : "1234"
}

~~~
**MongoDB 구조**  

<img src="https://user-images.githubusercontent.com/35910264/96869580-9c0c9c00-14aa-11eb-80a5-a3fdd2d187ae.jpg" width="300" height="300">


## 💡mongoose
mongoose란 nodejs 환경에서 사용하는 MongoDB기반의 라이브러리이다.

**mongoose 설치 및 적용**

`yarn add mongoose dotenv`

**mongoose && MongoDB 연동**
~~~javascript

mongoose.connect( mongoUri,{ useNewUrlParser: true,useUnifiedTopology: true, useCreateIndex: true,useFindAndModify: false})
.then(() => {
  console.log('Connected to Mongo DB');
})
.catch((e=> {
  console.error(e);
 });
~~~


**dotenv**   
환경별로 달라질 수 있는 값을 넣어줄 때 쓰이는데 환경변수 파일을 넣고 사용할 수 있는 개발도구이다.  

.env (file)
```bash
PORT=4000
MONGO_URL=mongodb://localhost:27029/user
```

**esm**   

es모듈(import/exprt) 는 nodejs에서 정의되어 있지 않는데 정의 할 수 있도록 도와주는 라이브러리

`yarn add esm`

## 💡데이터베이스의 스키마와 모델
mongoose 에는 `스키마` 와 `모델`이라는 개념이 있다.

**스키마와 모델 구조**  
<img src="https://user-images.githubusercontent.com/35910264/96872229-50f48800-14ae-11eb-8d1e-98ebcacd77a7.jpg" width="500" height="400">


~~~javascript

/** 스키마 생성 **/

const { Schema } = mongoose;

const UserSchema = new Schema({
  email: String,
  password: String,
  nickName: String,
  reg_date: Date,
  last_login: Date,
  role_id: String,
});

~~~

~~~javascript

/** 모델 생성 **/

const { Schema } = mongoose;

const UserSchema = new Schema({
  email: String,
  password: String,
  nickName: String,
  reg_date: Date,
  last_login: Date,
  role_id: String,
});

const User = mongoose.model('User', UserSchema);  // 'User' : 스키마 이름, UserSchema : 스키마 객체
export default User;

~~~

데이터베이스는 스키마 이름을 정해주면 그 이름의 복수 형태로 데이터베이스에 컬렉션 이름을 만든다.   
예를들어 스키마이름이 User인 경우 컬렉션이름은 users 
