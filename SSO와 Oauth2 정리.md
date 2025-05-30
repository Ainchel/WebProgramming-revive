# 1. SSO란 무엇인가?

SSO란 Single Sign-On의 줄임말로, 한 번의 로그인으로 여러 서비스에 접근할 수 있도록 해주는 인증 방식이다.

예시) 구글 계정으로 로그인한 상태에서 메일, 유튜브, 구글 드라이브 등 여러 서비스에 접근 가능

장점 : 사용자가 한 번의 로그인에서 다양한 서비스에 접근할 수 있으므로 편의성이 올라가고, 로그인 횟수가 감소한다.

한 번의 로그인 인증 상태를 공유하며 다양한 서비스로 연계할 수 있으므로, 카카오/네이버 등 타 플랫폼을 통해 로그인하면 해당 인증을 유지하면서 우리 서비스로 바로 연계할 수 있게 되는 것이다.

** SSO는 특정 기술이 아닌 패턴이자 설계에 가깝다. 이 설계를 구현하기 위한 도구가 Oauth2인 것이다.

# 2. 그렇다면 Oauth2란 무엇인가?

Oauth2.0이란 사용자의 비밀번호를 노출하지 않고, 제3자 서비스가 사용자 자원(정보)에 접근할 수 있게 해주는 표준 프로토콜이다. 이 프로토콜을 거치면 사용자의 비밀번호는 전혀 사용하지 않고, 접근 권한(Access Token)을 통해 다른 서비스의 정보를 허용된 만큼만 볼 수 있게 해준다.
Oauth2를 이용하면 비밀번호라는 중요 정보 없이, 사용자가 직접 허용한 범위 내에서, 시간 제한과 범위 제한을 가진 안전한 권한을 이용해 서비스 간 정보를 주고받을 수 있다.

예시) 사용자가 우리의 서비스에 로그인하려고 할 때, 우리 측에 정보를 제공하여 회원가입을 하지 않고도 카카오로 로그인할 수 있다.

```
1. 우리의 서비스에서 카카오 쪽에 사용자 인증을 요청한다.
2. 사용자에게 카카오 측의 동의 화면을 제공
3. 사용자가 동의했을 경우, Access Token을 발행
4. Access Token을 이용해 사용자의 이메일과 이름 등을 카카오 측에 요청
5. 받아온 정보로 우리 서비스의 회원 가입과 로그인 등을 처리한다.
```

** 프로토콜이란? 사람이 서로 의사소통을 하기 위해 언어와 문법이 필요한 것처럼, 컴퓨터나 시스템도 서로 정보를 주고 받기 위해 정해진 방식이 필요하다. 이를 프로토콜이라고 한다. 대표적인 것이 웹페이지를 주고받기 위한 규칙인 HTTP, 인터넷 상에서 데이터를 주고 받기 위한 TCP/IP가 있다. Oauth2 역시 인증을 주고 받기 위한 규칙이므로 프로토콜이라고 할 수 있다.

Oauth2라는 프로토콜은 인증을 주고 받기 위해 아래 절차를 거친다.

```
A. 클라이언트가 인증을 요청한다.
B. 사용자의 선택을 통해 권한을 부여한다. (인증 해도 돼라고 OK 사인을 준다)
C. 액세스 토큰이 발급된다.
D. API가 호출된다.
```

또한 Oauth2는 안전성을 위한 보안 규칙도 가지고 있다.

```
A. 토큰 기반 인증
B. 사용자 정보 보호
C. 범위(scope라고 한다) 설정
```

Oauth2를 구성하는 핵심 요소들은 아래와 같다.

```
A. 우선 특정 서비스에 특정 정보를 넘긴 상태의 사용자가 있어야 한다. -> Resource Owner
B. 사용자가 이용하고 있는 서비스가 있어야 한다. -> Client
C. 지금 이용하는 서비스 외에, 인증을 요청할 서버가 있어야 한다. -> Authorization Server
D. 사용자가 정보를 가지고 있는 서버가 있어야 한다.
E. 해당 정보에 접근하기 위한 인증 수단이 있어야 한다.
```

위 요소들을 가지고 Oauth2가 담당하는 기능인 '인증' 의 흐름을 아래와 같이 정리할 수 있다.

```
A. 사용자 우리의 서비스에서 로그인 요청을 하고, 카카오 인증 서버에서 인증에 동의를 한다.
B. Autorization Token을 발행한다.
C. Access Token을 요청한다.
D. 사용자 정보를 요청한다.
E. 받아온 정보를 가지고 로그인을 처리한다.
```

# 3. 그래서 Oauth2를 사용하려면 뭐가 필요한데?

스프링부트를 사용한다고 하면 아래 기술 스택이 필요하다.

```
A. spring-boot_starter-oauth2-client
B. spring-security-oauth2-client
C. application.yml 혹은 properties 설정
```

1. spring-boot_starter-oauth2-client은 Spring Security 기반 라이브러리이다. 사용하려면 build.gradle이나 application.yml 혹은 application.properties를 설정해야 한다.

``` spring-boot_starter-oauth2-client 설정 코드(일단 챗GPT 통해서 빠르게 수집함)
아래 코드는 YAML(Ain't Markup Language)이라는 양식으로, 들여쓰기로 계층 구조를 표현하는 파일 설정 형식이라고 한다. 즉 내려갈 수록 하위 계층이라고 생각하면 된다.
들여쓰기를 할 때, tab 키가 아닌 space 2번을 반드시 적어야 한다.

spring: << 모든 스프링 관련 설정은 이 아래로 들어간다.
  security: << Spring Security라는 보안 프레임워크이다. 로그인/로그아웃, 권한 부여, 인증/인가 등의 기능 구현을 돕는 라이브러리이다.
    oauth2: << Oauth2 관련 설정 영역을 가리킨다. 소셜 로그인, 외부 인증 등을 사용할 때 필요하다.
      client: << 이 앱이 Oauth2 구조에서 클라이언트(요청자) 역할을 한다는 의미이다. 외부 서비스에 로그인해 정보를 받아올 것이다.
        registration: << 여기 하위부터 어떤 인증 제공자에 대해 로그인을 요청할지 등록해야 한다. 구체적인 서비스명 및 코드가 시작된다.
          google: << 구글 설정 블록. Spring이 기본적으로 이해할 수 있는 키워드이다. 내부적으로 구글 Oauth2 제공자에 연결해준다.
            client-id: [클라이언트 ID] 구글 API 콘솔에서 발급받은 OAuth2 클라이언트 ID를 적는다. 저기로 가서 앱 등록을 해야 한다.
            client-secret: [클라이언트 시크릿] << 같은 방식으로 발급받는 클라이언트 비밀번호. 위 id랑 같이 github에 노출되면 안됨.
            scope: << 사용자가 OAuth2를 통해 어떤 정보를 제공받을지 하위에 적는다. 동의 화면에 아래 정보들 수집한다고 뜬다고 함.
              - email << 이메일. 구글은 기본으로 제공한다고 함
              - profile << 프로필. 구글은 기본으로 제공한다고 함
        provider: << OAuth2 제공자에 대한 추가 설정이 필요할 때 사용한다. 자동으로 설정하는 주소 말고 다른 주소를 명시할 수 있음
          google: << 어느 서비스에 대한 것인지. 위 registration에 명시된 서비스명과 일치해야 한다.
            authorization-uri: https://accounts.google.com/o/oauth2/v2/auth << 사용자 로그인할 때 이동하게 될 인증 URL(리디렉션)
            token-uri: https://oauth2.googleapis.com/token << 로그인 후(인증 마친 후), 서버가 액세스 토큰을 받기 위해 요청할 주소
            user-info-uri: https://www.googleapis.com/oauth2/v3/userinfo << 필요한 정보 요청할 주소. 이 API를 통해 받아온다고 함
```

2. spring-security-oauth2-client는 OAuth2의 핵심 기능(클라이언트 인증 기능) 을 실제로 구현하는 JAVA의 클래스이자 라이브러리이다.

``` spring-security-oauth2-client를 활용한 소셜로그인 기본 코드(어떻게 사용하는지 뜯어봐야 하며, 우리 서비스에는 코드 변형해서 넣어야겠지..?)

@Configuration << 스프링 설정 클래스임을 명시하는 어노테이션이다. Spring이 자동으로 스캔하여 스프링 컨테이너에 자동 등록시킴
@EnableWebSecurity << 스프링 시큐리티 수동 설정을 활성화하겠다는 의미. 보안 관련 설정을 하겠다는 의미이기도 하다.
public class SecurityConfig { << 보안 설정 담당 클래스 선언

    @Bean << 스프링이 관리하게 할 빈 객체를 등록하는 어노테이션
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception { << 스프링 시큐리티의 보안 설정을 구성하는 메소드. HttpSecurity 패러미터는 해당 웹 요청에서 어떤 보안 규칙을 적용할지 설정하는 물건이다.
        http << 스프링 시큐리티에서 사용하는 보안 설정 객체. 이 객체를 통해 URL 별 인증, 로그인 방식 등을 설정할 수 있다.
            .authorizeHttpRequests(authorize -> authorize << 요청을 허용 혹은 제한하겠다는 설정. URL별로 바로 접근시킬지, 로그인을 해야 할지 등의 규칙을 다음에 적는다.
                .requestMatchers("/", "/login", "/css/**").permitAll() << 이 URL에는 아무나 접근할 수 있도록 허용한다는 의미. 각 패러미터들은 메인 페이지에서의 이후 URL들이다. 예시) www.example.com/, www.example.com/login, www.example.com/css/... 등.
                .anyRequest().authenticated() << 위에 적어넣은 URL이 아닌 모든 요청을 로그인한 사용자만 접근 가능하도록 설정한다.
            )
            .oauth2Login(); << OAuth2의 외부 로그인 서비스와의 연동을 활성화한다.

        return http.build(); << 메소드의 마지막으로 위 설정을 마친 결과물을 만들어 반환시킨다.
    }
}
```

# 2-1. 위 메소드를 실제 호출하는 흐름 정리

만약에 사용자가 www.example.com/mypage라는 URL에 접근하다고 치자.

1. 스프링 시큐리티에서 로그인 상태를 체크한다. 로그인이 안 되어 있으면 카카오로 리디렉션 시킨다. 로그인이 되어 있다면 컨트롤러에서 실제 페이지를 반환한다.

2. 컨트롤러에서의 예시 (코드는 챗GPT에게 요청)

```
@Controller
public class MainController {

    @GetMapping("/")
    public String home() {
        return "home";  // 누구나 접근 가능
    }

    @GetMapping("/mypage")
    public String myPage(Principal principal, Model model) {
        // principal 객체는 인증된 사용자 정보
        model.addAttribute("username", principal.getName());
        return "mypage";  // 인증된 사용자만 접근 가능
    }
}
```
