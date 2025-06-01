OAuth2를 활용한 SSO 패턴을 구현하기 위해서는 URL에 대한 명확한 이해와 설계가 필요하다. 이에 따라 URL을 어떻게 설계하는지에 대한 패턴 공부가 필요하다.

제안받은 것은 REST API 패턴이다. 현업에서도 자주 사용되고 있고, 프론트-백 엔드간 협업에 유리한 구조라고 한다.

#RESTful API란?

약어인 REST는 'Representational State Transfer' 를 줄인 것이라고 한다. 아래의 특징을 가지고 있다.

```
A. 자원(얻고자 하는 정보) 중심의 URI 설계
B. 행위(HTTP Method - GET/POST/PUT/PATCH/DELETE)로 동작을 구분한다. << 다른 행위라면 같은 URL이라도 따로 작동시킬 수 있다.
C. URL의 구조가 일관적이며, 계층적 구조를 강조한다.
```

