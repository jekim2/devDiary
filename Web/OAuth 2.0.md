# OAuth 2.0

타사 서비스 (google, facebook) 의 이메일 정보에 우리가 만든 서비스의 접근을 허락하여 사용자를 인증   
  
### 용어

용어 | 의미 
---|---
`Client` | 사용자가 사용하려는 우리가 만든 서비스
`Resouce Server` | 서비스에 자신의 API를 제공하는 타사 서비스 (ex. 구글, 네이버) |
`Resouce Owner` |  타사 서비스 API의 정보의 주인. 우리가 만든 서비스를 타사 서비스를 통해 이용하려는 사용자  




  
### OAuth2.0 권한 획득 과정  
  
1. Client는 Resource Server에 특정 API를 사용할 것이라고 등록한다.  
2. Resource server는 Client ID와 Client Secret을 부여  
3. Resouce Owner가 Resouce server에게 구글 계정으로 로그인을 통해 로그인을 요청  
4. Client는 Resource Owner에게 Resouce server 로그인창을 띄워줌  
5. Resource Owner가 Client에게 Resouce server에 있는 자신의 ㅈ어보에 접근을 허락한다면, Resource Server는 Client에게 일련의 암호화된 코드를 제공하고  
이 코드와 함께 해당 정보의 사용 등록 여부의 Client ID와 Client Secret을 함께 보내 일치한다면 최종 접근 권한 부여의 암호인 Access Token을 발급하게된다.  




### JWT 란?
JWT는 `Json Web Token`의 약자로, 데이터가 JSON으로 이루어져있는 토큰을 의미한다.

**세션기반인증** 
1. 사용자가 로그인을 한다.
2. 서버에서 사용자 정보를 조회한 후, 세션 id를 발급해 준다.
3. 발급된 id를 저장 (주로 브라우저의 쿠키)
4. 사용자가 요청을 보낼 때마다 세션 저장소(DB, 메모리)를 조회한 후 응답해 준다.


**토큰기반인증**
1. 사용자가 로그인을 한다
2. 서버에서 토큰을 발급해 준다
3. 사용자가 발급받은 토큰과 함께 서버에 요청한다
4. 서버는 토큰의 유효성을 검사한 후, 응답해 준다.
