---
title: "Ⅴ. 스프링 시큐리티와 OAuth2.0"
excerpt: "스프링 시큐리티와 OAuth2.0으로 로그인 기능 구현하기"

categories:
    - SpringBoot & AWS
tags:
    - SpringBoot
    - Amazon Web Services
    - IntelliJ IDEA 
    - Gradle
    - JPA
    - Git
use_math: true;
last_modified_at: 2020-04-09

# published : false
--- 
> 개발 언어 : __Java 8(JDK 1.8)__  
> 개발 환경 : __Gradle 4.8 ~ Gradle 4.10.2__  
> 참조 :  
> [기억보단 기록을](https://jojoldu.tistory.com/)  
> [스프링 부트와 AWS로 혼자 구현하는 웹서비스 (프리렉, 이동욱 지음)](https://jojoldu.tistory.com/463)  
> [예제 코드 내려받기](http://bit.ly/fr-springboot)
  
## 구글서비스 등록
먼저 구글 서비스에 신규 서비스를 생성 해야한다. 여기서 발급된 인증 정보(clientId와 dlientSecret)를 통해서 로그인 기능과 소셜 서비스 기능을 사용 할 수 있다.  
구글 클라우드 플랫폼 주소 [http://console.cloud.google.com](http://console.cloud.google.com) 로 이동  
[프로젝트 선택] 탭 클릭  
[![그림 1-1](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img01.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img01.png)  
  
[새 프로젝트] 버튼 클릭  
[![그림 1-2](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img02.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img02.png)  
  
등록될 서비스 이름 입력  
[![그림 1-3](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img03.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img03.png)  
  
왼쪽 메뉴 탭 클릭 -> API 및 서비스 카테고리 이동  
[![그림 1-4](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img04.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img04.png)  
  
[사용자 인증 정보] 클릭 -> [사용자 인증 정보 만들기] 버튼 클릭  
[![그림 1-5](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img05.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img05.png)  
  
[OAuth 클라이언트 ID] 항목 클릭  
[![그림 1-6](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img06.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img06.png)  
  
[동의 화면 구성] 버튼 클릭  
[![그림 1-7](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img07.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img07.png)  
  
User Type 외부 체크후 만들기 클릭  
[![그림 1-8](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img08.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img08.png)  
  
OAuth 동의 화면에서 각 항목 작성  
[![그림 1-9](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img09.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img09.png)  
1. __애플리케이션 이름__  
+ 구글 로그인 시 사용자에게 노출될 애플리케이션 이름을 이야기한다.  
2. __지원 이메일__  
+ 사용자 동의 화면에서 노출될 이메일 주소이다. 보통은 서비스의 help 이메일 주소를 사용하지만, 여기서는 독자의 이메일 주소를 사용하면된다.  
3. __Google API의 범위__  
+ 이번에 등록할 구글 서비스에서 사용할 범위 목록이다. 기본값은 email/profile/openid 이며, 여기서는 딱 기본 범위만 사용한다. 이외 다른 정보들도 사용하고 싶다면 범위 추가 버튼으로 추가하면 된다.  
  
OAuth 동의 화면 제일 아래에 저장 버튼 클릭후 다시 [사용자 인증 정보] 클릭 -> [사용자 인증 정보 만들기] 버튼 클릭하여 OAuth 클라이언트 ID 화면으로 이동  
  
OAuth 클라이언트 ID 만들기  
[![그림 1-10](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img10.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img10.png)  
  
__승인된 리디렉션 URL__
+ 서비스에서 파라미터로 인증 정보를 주었을 때 인증이 성공하면 구글에서 리다이렉트할 URL이다.
+ 스프링 부트 2 버전의 시큐리티에서는 기본적으로 {도메인}/login/oauth2/code/{소셜서비스코드}로 리다이렉트 URL을 지원하고 있다.
+ 사용자가 별도로 리다이렉트 URL을 지원하는 Controller를 만들 필요가 없다. 시큐리티에서 이미 구현해 놓은 상태이다.
+ 현재는 개발 단계이므로 http://localhost:8080/login/oauth2/code/google 로만 등록한다.
+ AWS 서버에 배포하게 되면 localhost 외에 주소를 추가해야한다.
  
생성 버튼 클릭 하면 인증 정보를 볼 수 있다.  
[![그림 1-11](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img11.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img11.png)  
  
클라이언트 ID와 클라이언트 보안 비밀 코드를 프로젝트에서 설정  
`src/main/resources` 디렉토리에 __application-oauth.properties__ 파일 생성  
[![그림 1-12](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img12.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img12.png)  
  
```  
spring.security.oauth2.client.registration.google.client-id=클라이언트 ID
spring.security.oauth2.client.registration.google.client-secret=클라이언트 보안 비밀
spring.security.oauth2.client.registration.google.scope=profile,email
```  
  
스프링 부트에서는 properties의 이름을 `application-xxx.properties` 로 만들면 xxx라는 이름의 profile이 생성되어 이를 통해 관리할 수 있다. 즉, profile=xxx라는 식으로 호출하면 __해당 properties의 설정들을 가져올__ 수 있다. `application.properties` 에서 `application-oauth.properties` 를 포함하도록 구성  
application.properties 코드 추가  
```  
spring.profiles.include=oauth
```  
  
__.gitignore 등록__
구글 로그인을 위한 클라이언트 ID와 클라이언트 보안 비밀은 보안이 중요한 정보들이다. 외부에 노출될 경우 언제든 개인정보를 가져갈 수 있는 취약점이 될 수 있다.  
application-oauth.properties 파일이 깃허브에 올라갈 수 있다. 보안을 위해 깃허브에 application-oauth.properties 파일이 올라가는 것을 방지해야한다.  
.gitignore 에 코드 추가  
```  
application-oauth.properties
```  
추가한 뒤 커밋했을 때 커밋 파일 목록에 application-oauth.properties가 나오지 않으면 성공  
[![그림 1-13](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img13.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img13.png)  
__만약 .gitignore 에 추가했음에도 커밋 목록에 노출된다면 git의 캐시문제 때문이다. git명령어로 캐시 내용을 전부 삭제후 다시 add ALL해서 커밋해보자__  
```  
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
```  
## 구글 로그인 연동하기  
사용자 정보를 담당할 도메인인 User 클래스를 생성.  
패키지는 domain 아래에 user 패키지 생성.  
`src/main/java/com/freehyun/book/springboot/domain/user/User`  
```java  
import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.EnumType;
import javax.persistence.Enumerated;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Getter
@NoArgsConstructor
@Entity
public class User extends BaseTimeEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    @Column(nullable = false)
    private String email;

    @Column
    private String picture;

    @Enumerated(EnumType.STRING) //1.
    @Column(nullable = false)
    private Role role;

    @Builder
    public User(String name, String email, String picture, Role role) {
        this.name = name;
        this.email = email;
        this.picture = picture;
        this.role = role;
    }

    public User update(String name, String picture) {
        this.name = name;
        this.picture = picture;

        return this;
    }

    public String getRoleKey() {
        return this.role.getKey();
    }
}
```  
1. @Enumerated(EnumType.STRING)
+ JPA 로 데이터베이스로 저장할 때 Enum 값을 어떤 형태로 저장할지를 결정
+ 기본적으로 int 로 된 숫자가 저장
+ 숫자로 저장되면 데이터베이스로 확인할 때 그 값이 무슨 코드를 의미하는지 알 수가 없다.
+ 그래서 문자열 (EnumType.STRING)로 저장될 수 있도록 선언.
  
각 사용자의 권한을 관리할 Enum 클래스 Role을 생성  
`src/main/java/com/freehyun/book/springboot/domain/user/Role`  
```java  
import lombok.Getter;
import lombok.RequiredArgsConstructor;

@Getter
@RequiredArgsConstructor
public enum Role {

    GUEST("ROLE_GUEST", "손님"),
    USER("ROLE_USER", "일반 사용자");

    private final String key;
    private final String title;
}
```  
스프링 시큐리티에서는 권한 코드에 항상 __ROLE_ 이 앞에 있어야만__ 한다. 그래서 코드별 키 값을 ROLE_GUEST, ROLE_USER 등으로 지정.  
  
User의 CRUD를 책임질 UserRepository 인터페이스 생성  
`src/main/java/com/freehyun/book/springboot/domain/user/Role`  
```java  
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.Optional;

public interface UserRepository extends JpaRepository<User,Long> {
    Optional<User> findByEmail(String email); //1.
}
```  
1. findByEmail
+ 소셜 로그인으로 반환되는 값 중 email 을 통해 이미 생성된 사용자인지 처음 가입하는 사용자인지 판단하기 위한 메소드
  
__스프링 시큐리티 설정__
`build.gradle` 스프링 시큐리티 관련 의존성 추가  
```  
    compile('org.springframework.boot:spring-boot-starter-oauth2-client') //1.
```  
1. spring-boot-starter-oauth2-client
+ 소셜 로그인 등 클라이언트 입장에서 소셜 기능 구현 시 필요한 의존성
+ spring-security-oauth2-client 와 spring-security-oauth2-jose 를 기본으로 관리
  
OAuth 라이브러리를 이용한 소셜 로그인 설정 코드 작성  
`config.auth` 패키지 생성  
__시큐리티 관련 클래스는 모두 이곳에 담는다__  
[![그림 1-14](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img14.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img14.png)  
  
SecurityConfig 클래스 생성과 코드 작성  
```java  
import lombok.RequiredArgsConstructor;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@RequiredArgsConstructor
@EnableWebSecurity //1.
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    private final CustomOAuth2UserService customOAuth2UserService;

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
                .csrf().disable()
                .headers().frameOptions().disable() //2.
            .and()
                .authorizeRequests() //3.
                .antMatchers("/", "/css/**", "/images/**", "/js/**", "/h2-console/**").permitAll()
                .antMatchers("/api/v1/**").hasRole(Role.USER.name()) //4.
                .anyRequest().authenticated() //5.
            .and()
                .logout()
                    .logoutSuccessUrl("/") //6.
            .and()
                .oauth2Login() //7.
                    .userInfoEndpoint() //8.
                        .userService(customOAuth2UserService); //9.
    }
}
```  
1. @EnableWebSecurity  
+ Spring Security 설정들을 활성화 시켜 준다.  
2. .csrf().disable().headers().frameOptions().disable()  
+ h2-console 화면을 사용하기 위해 해당 옵션들을 disable 한다.  
3. authorizeRequests  
+ URL 별 권한 관리를 설정하는 옵션의 시작점  
+ authorizeRequests 가 선언되어야만 antMatchers 옵션을 사용할 수 있다.  
4. antMatchers  
+ 권한 관리 대상을 지정하는 옵션  
+ URL, HTTP 메소드별로 관리가 가능  
+ "/"등 지정된 URL 들은 permitAll() 옵션을 통해 전체 열람 권한을 준다.  
+ "/api/v1/**" 주소를 가진 API 는 USER 권한을 가진 사람만 가능.  
5. anyRequest  
+ 설정된 값들 이외 나머지 URL 들을 나타낸다.  
+ 여기서는 authenticated()을 추가하여 나머지 URL 들은 모두 인증된 사용자들에게만 허용  
+ 인증된 사용자 즉, 로그인한 사용자들을 이야기한다.  
6. .logout().logoutSuccessUrl("/")  
+ 로그아웃 기능에 대한 여러 설정의 진입점  
+ 로그아웃 성공시 / 주소로 이동  
7. oauth2Login  
+ OAuth2 로그인 기능에 대한 여러 설정의 진입점  
8. userInfoEndpoint
+ OAuth2 로그인 성공 이후 사용자 정보를 가져올 때의 설정들을 담당  
9. userService
+ 소셜 로그인 성공 시 후속 조치를 진행할 UserService 인터페이스의 구현체를 등록  
+ 리소스 서버(즉, 소셜 서비스들)에서 사용자 정보를 가져온 상태에서 추가로 진행하고자 하는 기능을 명시할 수 있다.
  
CustomOAuth2UserService 클래스 생성
[![그림 1-15](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img15.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img15.png)  
  
이 클래스에서는 구글 로그인 이후 가져온 사용자의 정보(email, name, picture 등) 들을 기반으로 가입 및 정보수정, 세션 저장 등의 기능을 지원한다.  
  
CustomOAuth2UserService 코드 작성  
`src/main/java/com/freehyun/book/springboot/config/auth/CustomOAuth2UserService`  
```java  
import lombok.RequiredArgsConstructor;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.oauth2.client.userinfo.DefaultOAuth2UserService;
import org.springframework.security.oauth2.client.userinfo.OAuth2UserRequest;
import org.springframework.security.oauth2.client.userinfo.OAuth2UserService;
import org.springframework.security.oauth2.core.OAuth2AuthenticationException;
import org.springframework.security.oauth2.core.user.DefaultOAuth2User;
import org.springframework.security.oauth2.core.user.OAuth2User;
import org.springframework.stereotype.Service;

import javax.servlet.http.HttpSession;
import java.util.Collections;

@RequiredArgsConstructor
@Service
public class CustomOAuth2UserService implements OAuth2UserService<OAuth2UserRequest, OAuth2User> {
    private final UserRepository userRepository;
    private final HttpSession httpSession;

    @Override
    public OAuth2User loadUser(OAuth2UserRequest userRequest) throws OAuth2AuthenticationException {
        OAuth2UserService delegate = new DefaultOAuth2UserService();
        OAuth2User oAuth2User = delegate.loadUser(userRequest);

        String registrationId = userRequest.getClientRegistration().getRegistrationId(); //1.
        String userNameAttributeName = userRequest.getClientRegistration().getProviderDetails().getUserInfoEndpoint().getUserNameAttributeName(); //2.

        OAuthAttributes attributes = OAuthAttributes.of(registrationId, userNameAttributeName, oAuth2User.getAttributes()); //3.

        User user = saveOrUpdate(attributes);
        httpSession.setAttribute("user", new SessionUser(user)); //4.

        return new DefaultOAuth2User(
                Collections.singleton(new SimpleGrantedAuthority(user.getRoleKey())),
                attributes.getAttributes(),
                attributes.getNameAttributeKey());
    }

    private User saveOrUpdate(OAuthAttributes attributes) {
        User user = userRepository.findByEmail(attributes.getEmail())
                .map(entity -> entity.update(attributes.getName(), attributes.getPicture()))
                .orElse(attributes.toEntity());

        return userRepository.save(user);
    }
}
```  
1. registrationId  
+ 현재 로그인 진행 중인 서비스를 구분하는 코드  
+ 지금은 구글만 사용하는 불필요한 값이지만, 이후 네이버 로그인 연동 시에 네이버 로그인인지, 구글 로그인인지 구분하기 위해 사용  
2. userNameAttributeName  
+ OAuth2 로그인 진행 시 키가 되는 필드값  
+ Primary Key 와 같은 의미  
+ 구글의 경우 기본적으로 코드를 지원하지만, 네이버 카카오 등은 기본 지원하지 않는다. 구글의 기본 코드는 "sub" 이다.  
+ 이후 네이버 로그인과 구글 로그인을 동시 지원할 때 사용  
3. OAuthAttributes  
+ OAuth2UserService 를 통해 가져온 OAuth2User 의 attribute 를 담을 클래스  
+ 이후 네이버 등 다른 소셜 로그인도 이 클래스를 사용  
4. SessionUser  
+ 세션에 사용자 정보를 저장하기 위한 Dto 클래스  
  
구글 사용자 정보가 업데이트 되었을 때를 대비하여 update 기능도 같이 구현되었다. 사용자의 이름이나 프로필 사진이 변경되면 User 엔티티에도 반영된다.  
  
`config.auth.dto` 패키지 생성  
[![그림 1-16](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img16.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img16.png)  
  
OAuthAttributes 클래스 생성후 코드 작성  
`src/main/java/com/freehyun/book/springboot/config/auth/dto/OAuthAttributes`  
```java  
import lombok.Builder;
import lombok.Getter;

import java.util.Map;

@Getter
public class OAuthAttributes {
    private Map<String, Object> attributes;
    private String nameAttributeKey;
    private String name;
    private String email;
    private String picture;

    @Builder
    public OAuthAttributes(Map<String, Object> attributes, String nameAttributeKey, String name, String email, String picture) {
        this.attributes = attributes;
        this.nameAttributeKey = nameAttributeKey;
        this.name = name;
        this.email = email;
        this.picture = picture;
    }

    //1.
    public static OAuthAttributes of(String registrationId, String userNameAttributeName, Map<String, Object> attributes) {
        return ofGoogle(userNameAttributeName, attributes);
    }

    private static OAuthAttributes ofGoogle(String userNameAttributeName, Map<String, Object> attributes) {
        return OAuthAttributes.builder()
                .name((String) attributes.get("name"))
                .email((String) attributes.get("email"))
                .picture((String) attributes.get("picture"))
                .attributes(attributes)
                .nameAttributeKey(userNameAttributeName)
                .build();
    }

    //2.
    public User toEntity() {
        return User.builder()
                .name(name)
                .email(email)
                .picture(picture)
                .role(Role.GUEST)
                .build();
    }
}

```  
1. of()  
+ OAuth2User 에서 반환하는 사용자 정보는 Map 이기 때문에 값 하나하나를 변환해야만 한다.  
2. toEntity()  
+ User 엔티티를 생성  
+ OAuthAttributes 에서 엔티티를 생성하는 시점은 처음 가입할 때  
+ 가입할 때의 기본 권한을 GUEST 로 주기 위해서 role 빌더값에는 Role.GUEST 를 사용  
  
`config.auth.dto` 패키지에 SessionUser 클래스를 추가  
[![그림 1-17](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img17.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img17.png)  
  
SessionUser에는 인증된 사용자 정보만 필요하다. 그외에 필요한 정보들은 없으니 name, email, picture만 필드로 선언한다.  
  
__로그인 테스트__  
index.mustache 추가  
[![그림 1-18](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img18.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img18.png)  
  
1. #userName  
+ 머스테치는 다른 언어와 같은 if문(if userName !=null 등)을 제공하지 않는다.  
+ true/false 여부만 판단할 뿐이다.  
+ 그래서 머스테치에서는 항상 최종값을 넘겨줘야 한다.  
+ 여기서도 역시 userName 이 있다면 userName 을 노출시키도록 구성하였다.
2. a href="/logout"  
+ 스프링 시큐리티에서 기본적으로 제공하는 로그아웃 URL  
+ 즉, 개발자가 별도로 저 url 에 해당하는 컨트롤러를 만들 필요가 없다.  
+ SecurityConfig 클래스에서 URL 을 변경할 순 있지만 기본 URL 을 사용해도 충분하니 여기서는 그대로 사용한다.  
3. ^userName  
+ 머스테치에서 해당 값이 존재하지 않는 경우에는 ^를 사용  
+ 여기서는 userName 이 없다면 로그인 버튼을 노출시키도록 구성  
4. a href="/oauth2/authorization/google"  
+ 스프링 시큐리티에서 기본적으로 제공하는 로그인 URL  
+ 로그아웃 URL 과 마찬가지로 개발자가 별도의 컨트롤러를 생성할 필요가 없다.  
  
index.mustache에서 userName을 사용할 수 있게 __IndexController__ 에서 userName을 model에 저장하는 코드를 추가  
```java  
...
import javax.servlet.http.HttpSession;

@RequiredArgsConstructor
@Controller
public class IndexController {
    private final PostsService postsService;
    private final HttpSession httpSession;

    @GetMapping("/")
    public String index(Model model) {
        model.addAttribute("posts", postsService.findAllDesc());
        SessionUser user = (SessionUser) httpSession.getAttribute("user"); //1.

        if (user != null) { //2. 
            model.addAttribute("userName", user.getName());
        }
        return "index";
    }
    ...
```  
1. (SessionUser) httpSession.getAttribute("user")  
+ 앞서 작성된 CustomOAuth2UserService 에서 로그인 성공 시 세션에 SessionUser 를 저장  
+ 즉, 로그인 성공 시 httpSession.getAttribute("user") 에서 값을 가져올 수 있다.  
2. if (user != null)  
+ 세션에 저장된 값이 있을 때만 model 에 userName 으로 등록  
+ 세션에 저장된 값이 없으면 model 엔 아무런 값이 없는 상태이니 로그인 버튼이 보이게 된다.  
  
`Application.java`의 main 메소드 실행하고 [http://localhost:8080](http://localhost:8080) 으로 접속해서 확인  
[![그림 1-19](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img19.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img19.png)  
  
[![그림 1-20](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img20.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img20.png)  
  
[http://localhost:8080/h2-console](http://localhost:8080/h2-console)에 접속해서 user테이블 확인  
[![그림 1-21](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img21.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img21.png)  
  
현재 로그인된 사용자의 권한은 GUEST이다. 이 상태에서는 posts 기능을 쓸 수 없다. 글 등록 기능을 사용하도록 해보자  
[![그림 1-22](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img22.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img22.png)  
  
실제 테스트를 위한 글쓰기를 진행하면 __403(권한 거부)__ 에러가 발생한다.
[![그림 1-23](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img23.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img23.png)  
  
권한을 변경해서 다시 시도 해보자  
h2-console로 가서 사용자의 role을 USER로 변경  
[![그림 1-24](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img24.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img24.png)  
  
세션에는 이미 GUEST인 정보로 저장되어있으니 로그아웃한 후 다시 로그인하여 세션 정보를 최신 정보로 갱신한 후에 글 등록을 해보자  
[![그림 1-25](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img25.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img25.png)  
  
## 어노테이션 기반으로 개선하기  
코드의 중복을 피하기 위해 IndexController에서 세션값을 가져오는 부분(SessionUser user = (SessionUser) httpSession.getAttribute("user");) 을 메소드 인자로 세션값을 바로 받을 수 있도록 변경한다.  
`config.auth` 패키지에 @LoginUser 어노테이션을 생성  
[![그림 1-26](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img26.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img26.png)  
  
```java  
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target(ElementType.PARAMETER) //1.
@Retention(RetentionPolicy.RUNTIME)
public @interface LoginUser { //2.
}
```  
1. @Target(ElementType.PARAMETER)  
+ 어노테이션이 생성될 수 있는 위치를 지정  
+ PARAMETER 로 지정했으니 메소드의 파라미터로 선언된 객체에서만 사용  
+ 이 외에도 클래스 선언문에 쓸 수 있는 TYPE 등이 있다.  
2. @interface  
+ 파일을 어노테이션 클래스로 지정  
+ LoginUser 라는 이름을 가진 어노테이션이 생성되었다고 보면 된다.
  
`config.auth` 패키지에 LoginUserArgumentResolver 클래스 생성  
LoginUserArgumentResolver라는 HandlerMethodArgumentResolver 인터페이스를 구현한 클래스이다.  
HandlerMethodArgumentResolver는 한가지 기능을 지원, 바로 조건에 맞는 경우 메소드가 있다면 HandlerMethodArgumentResolver의 구현체가 지정한 값으로 해당 메소드의 파라미터로 넘길 수 있다.  
`src/main/java/com/freehyun/book/springboot/config/auth/LoginUserArgumentResolver`  
```java  
import lombok.RequiredArgsConstructor;
import org.springframework.core.MethodParameter;
import org.springframework.stereotype.Component;
import org.springframework.web.bind.support.WebDataBinderFactory;
import org.springframework.web.context.request.NativeWebRequest;
import org.springframework.web.method.support.HandlerMethodArgumentResolver;
import org.springframework.web.method.support.ModelAndViewContainer;

import javax.servlet.http.HttpSession;

@RequiredArgsConstructor
@Component
public class LoginUserArgumentResolver implements HandlerMethodArgumentResolver {

    private final HttpSession httpSession;

    @Override
    public boolean supportsParameter(MethodParameter parameter) { //1.
        boolean isLoginUserAnnotation = parameter.getParameterAnnotation(LoginUser.class) != null;
        boolean isUserClass = SessionUser.class.equals(parameter.getParameterType());

        return isLoginUserAnnotation && isUserClass;
    }

    @Override //2.
    public Object resolveArgument(MethodParameter parameter, ModelAndViewContainer mavContainer, NativeWebRequest webRequest, WebDataBinderFactory binderFactory) throws Exception {
        return httpSession.getAttribute("user");
    }
}

```  
1. supportsParameter()  
+ 컨트롤러 메서드의 특정 파라미터를 지원하는지 판단  
+ 여기서는 파라미터에 @LoginUser 어노테이션이 붙어 있고, 파라미터 클래스 타입이 SessionUser.class 인 경우 true 를 반환  
2. resolveArgument()  
+  파라미터에 전달할 객체를 생성
+ 여기서는 세션에서 객체를 가져온다.
  
LoginUserArgumentResolver를 __스프링에서 인식될 수 있도록__ WebMvcConfigurer에 추가  
config 패키지에 WebConfig 클래스 생성, 설정 추가  
[![그림 1-27](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img27.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img27.png)  
  
`src/main/java/com/freehyun/book/springboot/config/WebConfig`  
```java  
import lombok.RequiredArgsConstructor;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.method.support.HandlerMethodArgumentResolver;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

import java.util.List;

//LoginUserArgumentResolver 를 스프링에서 인식될 수 있도록 WebMvcConfigurer 에 추가
//HandlerMethodArgumentResolver 는 항상 WebMvcConfigurer 의 addArgumentResolvers() 를 통해 추가. 다른 HandlerMethodArgumentResolver 가 필요하다면 같은 방식으로 추가.
@RequiredArgsConstructor
@Configuration
public class WebConfig implements WebMvcConfigurer {
    private final LoginUserArgumentResolver loginUserArgumentResolver;

    @Override
    public void addArgumentResolvers(List<HandlerMethodArgumentResolver> argumentResolvers) {
        argumentResolvers.add(loginUserArgumentResolver);
    }
}
```  
IndexController의 코드에서 반복되는 부분들을 모두 @LoginUser로 개선  
```java  
...
import javax.servlet.http.HttpSession;

@RequiredArgsConstructor
@Controller
public class IndexController {
    private final PostsService postsService;
    private final HttpSession httpSession;

    @GetMapping("/")
    public String index(Model model, @LoginUser SessionUser user) {//1.
        model.addAttribute("posts", postsService.findAllDesc());
        //SessionUser user = (SessionUser) httpSession.getAttribute("user");

        if (user != null) {
            model.addAttribute("userName", user.getName());
        }
        return "index";
    }
    ...
```  
1. @LoginUser SessionUser user  
+ 기존에 (User) httpSession.getAttribute("user") 로 가져오던 세션 정보 값이 개선  
+ 이제는 어느 컨트롤러든지 @LoginUser 만 사용하면 세션 정보를 가져올 수 있게 되었다.  
  
애플리케이션을 실행해 로그인 기능이 정상적으로 작동하는지 확인.
  
## 세션 저장소로 데이터베이스 사용하기  
세션이 내장 톰캣의 메모리에 저장되기 때문에 애플리케이션을 재 실행 하면 로그인이 풀린다. 기본적으로 세션은 실행되는 WAS(Web Application Server)의 메모리에서 저장되고 호출된다. 메모리에 저장되다 보니 내장 톰캣처럼 애플리케이션 실행 시 실행되는 구조에선 항상 초기화가 된다. 즉, 배포할 때마다 톰캣이 재시작되는 것이다.  
세션 저장소에 대해 3가지(톰캣 세션을 사용한다, MySQL과 같은 데이터베이스를 세션 저장소로 사용한다, Redis, Memcached와 같은 메모리 DB를 세션 저장소로 사용한다.) 중 데이터베이스를 세션 저장소로 사용하는 방식을 선택해서 진행하겠다.  
  
`build.gradle` 에 의존성 등록  
```  
compile('org.springframework.session:spring-session-jdbc')
```  
그리고 `application.properties` 에 세션 저장소를 jdbc로 선택하도록 코드 추가  
```  
spring.session.store-type=jdbc
```  
변경한 후 다시 애플리케이션을 실행해서 로그인을 테스트한 뒤, h2-console로 접속  
h2-console을 보면 세션을 위한 테이블2개(SPRING_SESSION, SPRING_SESSION_ATTRIBUTES)가 생성된 것을 볼 수 있다.  
[![그림 1-28](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img28.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img28.png)  
  
H2 기반으로 스프링이 재실행될 때 H2도 재시작되기 때문에 기존과 동일하게 스프링을 재시작하면 세션이 풀리게 된다. 이후 AWS로 배포하게 되면 AWS의 데이터베이스 서비스인 RDS(Relational Database Service)를 사용하게 되니 이때부터는 세션이 풀리지 않게된다.  
  
## 네이버 로그인  
__네이버 API 등록__  
[https://developers.naver.com/apps/#/register?api=nvlogin](https://developers.naver.com/apps/#/register?api=nvlogin)  
  
[![그림 1-29](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img29.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img29.png)  
  
[![그림 1-30](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img30.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img30.png)  
  
서비스 URL은 필수이다. 여기서 localhost:8080 으로 등록한다. Callback URL은 구글에서 등록한 리디렉션 URL과 같은 역할을 한다. /login/oauth2/code/naver로 등록한다. 등록을 완료하면 ClientID와 ClientSecret가 생성된다.  
[![그림 1-31](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img31.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img31.png)  
  
해당 키값들을 `application-oauth.properties` 에 등록한다. 네이버에서는 스프링 시큐리티를 공식 지원하지 않기 때문에 그동안 Common-OAuth2Provider에서 해주던 값들도 전부 수동으로 입력한다.  
```  
# registration
spring.security.oauth2.client.registration.naver.client-id=클라이언트 ID
spring.security.oauth2.client.registration.naver.client-secret=클라이언트 비밀
spring.security.oauth2.client.registration.naver.redirect-uri={baseUrl}/{action}/oauth2/code/{registrationId}
spring.security.oauth2.client.registration.naver.authorization-grant-type=authorization_code
spring.security.oauth2.client.registration.naver.scope=name,email,profile_image
spring.security.oauth2.client.registration.naver.client-name=Naver

# provider
spring.security.oauth2.client.provider.naver.authorization-uri=https://nid.naver.com/oauth2.0/authorize
spring.security.oauth2.client.provider.naver.token-uri=https://nid.naver.com/oauth2.0/token
spring.security.oauth2.client.provider.naver.user-info-uri=https://openapi.naver.com/v1/nid/me
spring.security.oauth2.client.provider.naver.user-name-attribute=response  //1.
```  
1. user-name-attribute=response  
+ 기준이 되는 user-name 의 이름을 네이버에서는 response 로 해야한다.  
+ 이유는 네이버의 회원 조회 시 반환되는 JSON 형태 때문이다.  
  
__스프링 시큐리티 설정 등록__
OAuthAttributes에 네이버인지 판단하는 코드와 네이버 생성자 추가  
```java  
@Getter
public class OAuthAttributes {
    ...

    public static OAuthAttributes of(String registrationId, String userNameAttributeName, Map<String, Object> attributes) {
        if("naver".equals(registrationId)) {
            return ofNaver("id", attributes);
        }

        return ofGoogle(userNameAttributeName, attributes);
    }

    ...

    private static OAuthAttributes ofNaver(String userNameAttributeName, Map<String, Object> attributes) {
        Map<String, Object> response = (Map<String, Object>) attributes.get("response");

        return OAuthAttributes.builder()
                .name((String) response.get("name"))
                .email((String) response.get("email"))
                .picture((String) response.get("profile_image"))
                .attributes(response)
                .nameAttributeKey(userNameAttributeName)
                .build();
    }

    ...
}
```  
index.mustache 네이버 로그인 버튼 추가  
```javascript  
<a href="/oauth2/authorization/naver" class="btn btn-secondary active" role="button">Naver Login</a>
```
1. /oauth2/authorization/naver  
+ 네이버 로그인 URL 은 application-oauth.properties 에 등록한 redirect-uri 값에 맞춰 자동으로 등록  
+ /oauth2/authorization/ 까지 고정이고 마지막 Path 만 각 소셜 로그인 코드를 사용  
+ 여기서는 naver 가 마지막 Path  
`Application.java`의 main 메소드 실행하고 [http://localhost:8080](http://localhost:8080) 으로 접속해서 네이버 로그인 버튼 활성화 확인  
[![그림 1-32](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img32.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img32.png)  
  
## 기존 테스트에 시큐리티 적용하기  
기존 테스트에 시큐리티 적용으로 문제가 되는 부분이 있다. 기존에는 바로 API를 호출 할 수 있어 테스트 코드 역시 바로 API를 호출하도록 구성하였다. 하지만, 시큐리티 옵션이 활성화되면 인증된 사용자만 API를 호출할 수 있다. 기존의 API 테스트 코드들이 모두 인증에 대한 권한을 받지 못하였으므로, 테스트 코드마다 인증한 사용자가 호출한 것처럼 작동하도록 수정하겠다.  
IntelliJ 오른쪽 위에 [Gradle] 탭을 클릭  
[Tasks -> verification -> test] 전체 테스트 수행  
[![그림 1-33](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img33.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img33.png)  
  
test를 실행해 보면 롬복을 이용한 테스트 외에 스프링을 이용한 테스트는 모두 실패  
[![그림 1-34](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img34.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img34.png)  
  
첫번째 실패 테스트인 "hello가 리턴된다"의 메시지를 보면 "No qualifying bean of type 'com.freehyun.book.springboot.config.auth.CustomOAuth2UserService'" 라는 메시지가 등장한다.  
[![그림 1-35](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img35.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img35.png)  
  
이는 CustomOAuth2UserService를 생성하는데 필요한 소셜 로그인 관련 설정값들이 없기 때문에 발생한다.  
우리가 `src/main` 환경에서 `application-oauth.properties`에 설정값들을 추가하였지만 이는 `src/test` 환경과는 다르다. 둘은 본인만의 환경 구성을 가진다. 다만, `src/main/resources/application.properties`가 테스트 코드를 수행할 때도 적용되는 이유는 __test에 application.properties가 없으면 main의 설정을 그대로 가져오기 때문__ 이다. 다만, 자동으로 가져오는 옵션의 범위는 `application.properties` 파일까지이다. 즉, `application-oauth.properties`는 __test에 파일이 없다고 가져오는 파일은 아니라는 점__ 이다.  
문제를 해결하기 위해 테스트 환경을 위한 `application.properties`를 만들어보자  
실제로 구글 연동까지 진행할 것은 아니므로 가짜 설정값을 등록한다.  
[![그림 1-36](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img36.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img36.png)  
  
`application.properties` 코드작성  
src/test/resources/application.properties  
```  
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect
spring.h2.console.enabled=true
spring.session.store-type=jdbc

# Test OAuth

spring.security.oauth2.client.registration.google.client-id=test
spring.security.oauth2.client.registration.google.client-secret=test
spring.security.oauth2.client.registration.google.scope=profile,email
```
두 번째 "Posts_등록된다" 테스트 로그를 확인하자  
[![그림 1-37](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img37.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img37.png)  
  
응답의 결과로 200(정상 응답) Status Code를 원했는데 결과는 302(리다이렉션 응답) Status Code가 와서 실패했다. 이는 스프링 시큐리티 설정 때문에 __인증되지 않은 사용자의 요청은 이동__ 시키기 때문이다. 임의로 인증된 사용자를 추가하여 API만 테스트해 볼 수 있게 하자  
스프링 시큐리티 테스트를 위한 여러 도구를 지원하는 spring-security-test를 `build.gradle`에 추가  
```  
testCompile("org.springframework.security:spring-security-test")
```
그리고 PostsApiControllerTest 의 2개 테스트 메소드에 임의 사용자 인증을 추가  
```java  
@Test
@WithMockUser(roles = "USER") //1. 인증된 모의(가짜) 사용자를 만들어서 사용, roles 에 권한을 추가할 수 있다. 즉, 이 어노테이션으로 인해 ROLE_USER 권한을 가진 사용자가 API 를 요청하는 것과 동일한 효과를 가지게 된다.
public void Posts_등록된다() throws Exception {
...
  
@WithMockUser(roles = "USER")
public void Posts_수정된다() throws Exception {
...
```  
1. @WithMockUser(roles = "USER")  
+ 인증된 모의(가짜) 사용자를 만들어서 사용  
+ roles 에 권한을 추가할 수 있다.  
+ 즉, 이 어노테이션으로 인해 ROLE_USER 권한을 가진 사용자가 API 를 요청하는 것과 동일한 효과를 가지게 된다.  
  
__@WithMockUser가 MockMvc에서만 작동하기 때문__ 에 테스트가 작동하지 않는다. 현재 PostsApiControllerTest는 @SpringBootTest로만 되어있으며 MockMvc를 전혀 사용하지 않는다. 그래서 __@SpringBootTest에서 MockMvc를 사용하는방법__ 으로 코드를 변경하겠다.  
```java  
//1.
import com.fasterxml.jackson.databind.ObjectMapper;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.web.client.TestRestTemplate;
import org.springframework.boot.web.server.LocalServerPort;
import org.springframework.http.*;
import org.springframework.security.test.context.support.WithMockUser;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import org.springframework.web.context.WebApplicationContext;

import java.util.List;

import static org.assertj.core.api.Assertions.assertThat;
import static org.springframework.security.test.web.servlet.setup.SecurityMockMvcConfigurers.springSecurity;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.post;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.put;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class PostsApiControllerTest {
    ...

    @Autowired
    private WebApplicationContext context;

    private MockMvc mvc;

    @Before //2. 매번 테스트가 시작되기 전에 MockMvc 인스턴스를 생성
    public void setup() {
        mvc = MockMvcBuilders
                .webAppContextSetup(context)
                .apply(springSecurity())
                .build();
    }

    ...

    @Test
    @WithMockUser(roles = "USER")
    public void Posts_등록된다() throws Exception {

        ...

        //when
        mvc.perform(post(url) //3. 생성된 MockMvc 를 통해 API 를 테스트, 본문(Body)영역은 문자열로 표현하기 위해 ObjectMapper 를 통해 문자열 JSON 으로 변환
                .contentType(MediaType.APPLICATION_JSON_UTF8)
                .content(new ObjectMapper().writeValueAsString(requestDto)))
                .andExpect(status().isOk());

        //then
        List<Posts> all = postsRepository.findAll();
        assertThat(all.get(0).getTitle()).isEqualTo(title);
        assertThat(all.get(0).getContent()).isEqualTo(content);
    }

    @Test
    @WithMockUser(roles = "USER")
    public void Posts_수정된다() throws Exception {

        ...

        //when
        mvc.perform(put(url)
                .contentType(MediaType.APPLICATION_JSON_UTF8)
                .content(new ObjectMapper().writeValueAsString(requestDto)))
                .andExpect(status().isOk());
        //then
        List<Posts> all = postsRepository.findAll();
        assertThat(all.get(0).getTitle()).isEqualTo(expectedTitle);
        assertThat(all.get(0).getContent()).isEqualTo(expectedContent);
    }
}
```  
1. import...
+ 새로 추가되는 import  
2. @Before  
+ 매번 테스트가 시작되기 전에 MockMvc 인스턴스를 생성  
3. mvc.perform  
+ 생성된 MockMvc 를 통해 API 를 테스트  
+ 본문(Body)영역은 문자열로 표현하기 위해 ObjectMapper 를 통해 문자열 JSON 으로 변환  
  
다시 전체 테스트를 수행해 보면 Posts 테스트가 정상적으로 수행되었다.  
[![그림 1-38](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img38.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img38.png)  
  
세 번째로 "Hello가 리턴된다" 테스트인데 HelloControllerTest는 @WebMvcTest를 사용하고 있다. 첫번째 테스트로 스프링 시큐리티 설정은 잘 작동했지만, @WebMvcTest는 CustomOAuth2UserService를 스캔하지 않기 때문이다. @WebMvcTest는 WebSecurityConfigurerAdapter, WebMvcConfigurer를 비롯한 @ControllerAdvice, @Controller를 읽는다. 즉, @Repository, @Service, @Component는 스캔 대상이 아니다. 그러니 SecurityConfig는 읽었지만, SecurityConfig를 생성하기 위해 필요한 CustomOAuth2UserService는 읽을수가 없어 앞에서와 같이 에러가 발생한 것이다. 이문제를 해결하기 위해서는 스캔 대상에서 SecurityConfig를 제거한다.  
  
```java  
@WebMvcTest(controllers = HelloController.class, 
        excludeFilters = {
        @ComponentScan.Filter(type = FilterType.ASSIGNABLE_TYPE, classes = SecurityConfig.class)
        }
)
```  
여기서도 마찬가지로 @WithMockUser를 사용해서 가짜로 인증된 사용자를 생성한다.  
```  
java.lang.IllegalArgumentException: JPA metamodel must not be empty!
```  
이 에러는 `Application.java`에 @EnableJpaAuditing로 인해 발생한다. @EnableJpaAuditing를 사용하기 위해선 최소 하나의 @Entity 클래스가 필요하다. @WebMvcTest이다 보니 당연히 없다.  
@EnableJpaAuditing가 @SpringBootApplication와 함께 있다보니 @WebMvcTest에서도 스캔하게 되었다. 그래서 @EnableJpaAuditing과 @SpringBootApplication 둘을 분리하겠다. `Application.java`에서 @EnableJpaAuditing를 제거한다.  
```java  
//@EnableJpaAuditing //따로분리 config/JpaConfig 선언
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```  
그리고 config 패키지에 JpaConfig를 생성하여 @EnableJpaAuditing를 추가  
[![그림 1-39](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img39.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img39.png)  
  
src/main/java/com/freehyun/book/springboot/config/JpaConfig  
```java  
import org.springframework.context.annotation.Configuration;
import org.springframework.data.jpa.repository.config.EnableJpaAuditing;

@Configuration
@EnableJpaAuditing //JPA Auditing 활성화
public class JpaConfig {
}
```  
@WebMvcTest는 일반적인 @Configuration은 스캔하지 않는다.  
다시 전체 테스트를 수행해 보자  
[![그림 1-40](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img40.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img40.png)  