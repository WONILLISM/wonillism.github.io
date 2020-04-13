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
config.auth 패키지 생성  
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
src/main/java/com/freehyun/book/springboot/config/auth/CustomOAuth2UserService  
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
  
config.auth.dto 패키지 생성  
[![그림 1-16](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img16.png)](/assets/Web/AWS/2020-04-10-SpringBoot-AWS-05-img16.png)  
  
OAuthAttributes 클래스 생성후 코드 작성  
src/main/java/com/freehyun/book/springboot/config/auth/dto/OAuthAttributes  
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
  
config.auth.dto 패키지에 SessionUser 클래스를 추가  
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






















'mustache'를 검색해서 해당 플러그인 설치
[![그림 1-1](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img01.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img01.png)  
  
## 기본 페이지 만들기  
머스테치 스타터 의존성을 `build.gradle` 에 등록
```  
compile('org.springframework.boot:spring-boot-starter-mustache')
```  
머스테치는 __스프링 부트에서 공식 지원하는 템플릿 엔진__  
머스테치의 파일 위치는 기본적으로 __src/main/resources/templates__ 이다. 이 위치에 머스테치 파일을 두면 스프링 부트에서 자동으로 로딩한다.  
  
`src/main/resources/templates` 에 `index.mustache` 생성  
[![그림 1-2](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img02.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img02.png)  
  
`index.mustache` 코드 작성  
```javascript  
<!DOCTYPE HTML>
<html>
<head>
    <title>스프링 부트 웹서비스</title>
    <meta http-equiv="Content-Type" content="text/html"; charset="UTF-8" />
    
</head>
<body>
    <h1>스프링 부트로 시작하는 웹 서비스</h1>
</body>
</html>
```  
머스테치에 URL을 매핑해보자. URL 매핑은 당연하게 Controller에서 진행한다. `web` 패키지 안에 IndexController를 생성  
[![그림 1-3](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img03.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img03.png)  

```java  
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class IndexController {

    @GetMapping("/")
    public String index() {
        return "index";
    }
}
```  
머스테치 스타터 덕분에 컨트롤러에서 문자열을 반환할 때 __앞의 경로와 뒤의 파일 확장자는 자동으로 지정__ 된다. 앞의 경로는 `src/main/resources/templates`로, 뒤의 파일 확장자는 `.mustache`가 붙은 것이다. 즉 여기선 "index"을 반환하므로, `src/main/resources/templates/index.mustache` 로 전환되어 View Resolver가 처리하게 된다.  
  
테스트 코드 검증  
`test` 패키지에 IndexControllerTest 클래스를 생성  
[![그림 1-4](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img04.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img04.png)  

`src/test/java/com/freehyun/book/springboot/web/IndexControllerTest`
```java  
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.web.client.TestRestTemplate;
import org.springframework.test.context.junit4.SpringRunner;

import static org.assertj.core.api.Assertions.assertThat;
import static org.springframework.boot.test.context.SpringBootTest.WebEnvironment.RANDOM_PORT;

@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = RANDOM_PORT)
public class IndexControllerTest {

    @Autowired
    private TestRestTemplate restTemplate;

    @Test
    public void 메인페이지_로딩() {
        //when
        String body = this.restTemplate.getForObject("/", String.class);

        //then
        assertThat(body).contains("스프링 부트로 시작하는 웹서비스");
    }
}
```  
TestRestTemplate를 통해 "/"로 호출했을 때 `index.mustache`에 포함된 코드들이 있는지 확인  
저체 코드를 다 검증할 필요는 없으니, "스프링 부트로 시작하는 웹 서비스" 문자열이 포함되어 있는지만 비교  
[![그림 1-5](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img05.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img05.png)  
  
`Application.java`의 main 메소드 실행하고 [http://localhost:8080](http://localhost:8080) 으로 접속해서 확인  
[![그림 1-6](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img06.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img06.png)  
  
## 게시글 등록 화면 만들기  
`src/main/resources/templates` 디렉토리에 `layout` 디렉토리를 추가 생성  
`footer.mustache`, `header.mustache` 파일 생성  
[![그림 1-7](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img07.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img07.png)  
  
header.mustache  
```javascript  
<!DOCTYPE HTML>
<html>
<head>
    <title>스프링부트 웹서비스</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />

    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
</head>
<body>
```  
footer.mustache  
```javascript  
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>

</body>
</html>
```  
<!-- 코드를 보면 css와 js의 위치가 서로 다르다. 페이지 로딩속도를 높이기 위해 css는 header에, js는 footer에 둔다. HTML은 위에서부터 코드가 실행되기 때문에 head가 다 실행되고서야 body가 실행된다. 즉, head가 다 불러지지 않으면 사용자 쪽에선 백지 화면만 노출된다. 특히 js의 용량이 크면 클수록 body 부분의 실행이 늦어지기 때문에 js는 body 하단에 두어 화면이 다 그려진 뒤에 호출하는 것이 좋다. 반면 css는 화면을 그리는 역할이므로 head에서 불러오는 것이 좋다. 그허지 않으면 css가 적용되지 않은 깨진 화면을 사용자가 볼 수 있기 때문이다. 추가로, bootstrap.js가 제이쿼리에 의존한다고 한다. -->
`index.mustache` 코드 변경, 글 등록 버튼 추가  
[![그림 1-8](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img08.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img08.png)  
  
IndexController /posts/save 추가  
```java  
@RequiredArgsConstructor
@Controller
public class IndexController {

    ...

    @GetMapping("/posts/save")
    public String postsSave() {
        return "posts-save";
    }
}
```  
`posts-save.mustache` 파일 생성  
파일 위치는 index.mustache와 같다.  
[![그림 1-9](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img09.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img09.png)  
  
프로젝트를 실행하고 [http://localhost:8080/](http://localhost:8080/) 로 접근해서 '글 등록' 버튼을 클릭하면 글 등록 화면으로 이동한다.  
[![그림 1-10](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img10.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img10.png)  
  
아직 등록 버튼의 기능이 없다. API를 호출하는 JS가 없기 때문이다. 그래서 `src/main/resources` 에 `static/js/app` 디렉토리를 생성해준다.
[![그림 1-11](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img11.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img11.png)  
  
index.js 생성  
[![그림 1-12](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img12.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img12.png)  
  
index.js 코드 작성  
```javascript  
var main = {
    init : function () {
        var _this = this;
        $('#btn-save').on('click', function () {
            _this.save();
        });
    },
    save : function () {
        var data = {
            title: $('#title').val(),
            author: $('#author').val(),
            content: $('#content').val()
        };

        $.ajax({
            type: 'POST',
            url: '/api/v1/posts',
            dataType: 'json',
            contentType:'application/json; charset=utf-8',
            data: JSON.stringify(data)
        }).done(function () {
            alert('글이 등록되었습니다.');
            window.location.href = '/'; //1. 
        }).fail(function (error) {
            alert(JSON.stringify(error));
        });
    }
};

main.init();
```  
1. window.location.href = '/'  
+ 글 등록이 성공하면 메인페이지(/)로 이동  
  
<!-- index.mustache에서 a.js가 추가되어 a.js도 a.js만의 init과 save function이 있다면 어떻게 될까? 브라우저의 scope는 공용 공간으로 쓰이기 때문에 나중에 로딩된 js의 init, save가 먼저 로딩된 js의 function을 덮어쓰게 된다. 여러 사람이 참여하는 프로젝트에서는 중복된 function이름은 자주 발생할 수 있다. 모든 function 이름을 확인하면서 만들 수는 없다. 그러다 보니 이런 문제를 피하려고 index.js만의 유효범위 scope를 만들어 사용한다. 방법은 var index이란 객체를 만들어 해당 객체에서 필요한 모든 function을 선언하는 것이다. 이렇게 하면 index객체 안에서만 function이 유효하기 때문에 다른 JS와 겹칠 위험이 사라진다. -->
footer.mustache 추가  
```javascript  
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>

<!--index.js 추가-->
<script src="/js/app/index.js"></script>
</body>
</html>
```  
스프링 부트는 기본적으로 `src/main/resources/static` 에 위치한 자바스크립트, CSS, 이미지 등 정적 파일들은 URL에서 /로 설정 된다.
+ src/main/resources/static/js/...(http://도메인/js/...)
+ src/main/resources/static/css/...(http://도메인/css/...)
+ src/main/resources/static/image/...(http://도메인/image/...)
  
등록 기능을 브라우저에서 직접 테스트해보자  
[![그림 1-13](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img13.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img13.png)  
  
[![그림 1-14](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img14.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img14.png)  
  
[http://localhost:8080/h2-console](http://localhost:8080/h2-console) 에 접속해서 실제로 DB에 데이터가 등록되었는지 확인해보자  
[![그림 1-15](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img15.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img15.png)  
  
## 전체 조회 화면 만들기  
전체 조회를 위해 index.mustache의 UI를 변경  
[![그림 1-16](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img16.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img16.png)  
  
Controller, Service, Repository 코드를 작성  
PostsRepository 인터페이스에 쿼리 추가  
```java  
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;

import java.util.List;

public interface PostsRepository extends JpaRepository<Posts, Long> {

    @Query("SELECT p FROM Posts p ORDER BY p.id DESC")
    List<Posts> findAllDesc();
}
```  
<!-- SpringDataJpa에서 제공하지 않는 메소드는 위처럼 쿼리로 작성해도 되는 것을 보여주기위해 @Query를 사용했다. 실제로 앞의 코드는 SpringDataJpa에서 제공하는 기본 메소드만으로 해결할 수 있다. 다만 @Query가 훨씬 가독성이 좋으니 선택해서 사용 하면된다. -->
PostsService 코드 추가  
```java  
...
import java.util.List;
import java.util.stream.Collectors;

@RequiredArgsConstructor
@Service
public class PostsService {
    private final PostsRepository postsRepository;

    ...

    @Transactional(readOnly = true) //1.
    public List<PostsListResponseDto> findAllDesc() {
        return postsRepository.findAllDesc().stream()
                .map(PostsListResponseDto:: new) //2.
                .collect(Collectors.toList());
    }
}
```  
1. @Transactional(readOnly = true)  
+ (readOnly = true) 를 주면 트랜잭션 범위는 유지하되, 조회 기능만 남겨두어 조회 속도가 개선되기 때문에 등록, 수정, 삭제 기능이 전혀 없는 서비스 메소드에서 사용하는 것을 추천  
2. .map(PostsListResponseDto:: new)  
+ .map(posts -> new PostsListResponseDto(posts))  
+ postsRepository 결과로 넘어온 Posts 의 Stream 을 map 을 통해 PostsListResponseDto 변환 -> List 로 반환하는 메소드  
  
PostsListResponseDto 클래스 생성  
[![그림 1-17](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img17.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img17.png)  
  
PostsListResponseDto 코드 작성  
`src/main/java/com/freehyun/book/springboot/web/dto/PostsListResponseDto`
```java  
import lombok.Getter;
import java.time.LocalDateTime;

@Getter
public class PostsListResponseDto {
    private Long id;
    private String title;
    private String author;
    private LocalDateTime modifiedDate;

    public  PostsListResponseDto(Posts entity) {
        this.id = entity.getId();
        this.title = entity.getTitle();
        this.author = entity.getAuthor();
        this.modifiedDate = entity.getModifiedDate();
    }
}
```  
IndexController 변경  
```java  
import org.springframework.ui.Model;

@RequiredArgsConstructor
@Controller
public class IndexController {
    private final PostsService postsService;

    @GetMapping("/")
    public String index(Model model) { //1.
        model.addAttribute("posts", postsService.findAllDesc());
        return "index";
    }
}
```  
1. Model  
+ 서버 템플릿 엔진에서 사용할 수 있는 객체를 저장  
+ 여기서는 postsService.findAllDesc()로 가져온 결과를 posts 로 index.mustache 에 전달  
  
[http://localhost:8080/](http://localhost:8080/) 로 접속한 뒤 정상 작동하는지 확인  
[![그림 1-18](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img18.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img18.png)  
  
## 게시글 수정, 삭제 화면 만들기  
게시글 수정 화면 머스테치 파일을 생성  
`src/main/resources/templates/posts-update.mustache`  
[![그림 1-19](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img19.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img19.png)  
  
그리고 btn-update 버튼을 클릭하면 update 기능을 호출할 수 있게 index.js 파일에도 update function 을 추가  
```javascript  
var main = {
    init : function () {
        var _this = this;
        $('#btn-save').on('click', function () {
            _this.save();
        });

        $('#btn-update').on('click', function () { //1. 
            _this.update();
        });
    },
    save : function () {
        var data = {
            title: $('#title').val(),
            author: $('#author').val(),
            content: $('#content').val()
        };

        $.ajax({
            type: 'POST',
            url: '/api/v1/posts',
            dataType: 'json',
            contentType:'application/json; charset=utf-8',
            data: JSON.stringify(data)
        }).done(function () {
            alert('글이 등록되었습니다.');
            window.location.href = '/';
        }).fail(function (error) {
            alert(JSON.stringify(error));
        });
    },

    update : function () { //2. 
        var data = {
            title: $('#title').val(),
            content: $('#content').val()
        };

        var id = $('#id').val();

        $.ajax({
            type: 'PUT', //3. 
            url: '/api/v1/posts/'+id, //4. 
            dataType: 'json',
            contentType:'application/json; charset=utf-8',
            data: JSON.stringify(data)
        }).done(function () {
            alert('글이 수정되었습니다.');
            window.location.href = '/';
        }).fail(function (error) {
            alert(JSON.stringify(error));
        });
    }
};

main.init();
```  
1. $('#btn-update').on('click')  
+ btn-update 란 id를 가진 HTML 엘리먼트에 click 이벤트가 발생할 때 update function 을 실행하도록 이벤트를 등록  
2. update : function ()  
+ 신규로 추가될 update function  
3. type: 'PUT'  
+ 여러 HTTP Method 중 PUT 메소드를 선택  
+ PostsApiController 에 있는 API 에서 이미 @PutMapping 으로 선언했기 때문에 PUT 을 사용  
+ REST 에서 CRUD 는 HTTP Method 에 매핑, 생성(create)-POST, 읽기(Read)-GET, 수정(Update)-PUT, 삭제(Delete)-DELETE  
4. url: '/api/v1/posts/'+id
+ 어느 게시글을 수정할지 URL Path 로 구분하기 위해 Path 에 id 를 추가  
  
수정 페이지로 이동할 수 있게 페이지 이동 기능 추가  
index.mustache 코드 수정  
[![그림 1-20](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img20.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img20.png)  
  
수정 화면을 연결할 Controller 코드 작업  
IndexController 메소드 추가  
```java  
.....
  
public class IndexController {
    ...

    @GetMapping("/posts/update/{id}")
    public String postsUpdate(@PathVariable Long id, Model model) {
        PostsResponseDto dto = postsService.findById(id);
        model.addAttribute("post", dto);

        return "posts-update";
    }
}
```  
`Application.java`의 main 메소드 실행하고 [http://localhost:8080](http://localhost:8080) 으로 접속해서 확인  
[![그림 1-21](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img21.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img21.png)  
[![그림 1-22](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img22.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img22.png)  
[![그림 1-23](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img23.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img23.png)  
[![그림 1-24](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img24.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img24.png)  
  
게시글 삭제  
posts-update.mustache 코드 추가  
```javascript  
...
<div class="col-md-12">
    <div class="col-md-4">
        <a href="/" role="button" class="btn btn-secondary">취소</a>
        <button type="button" class="btn btn-primary" id="btn-update">수정 완료</button>
        <button type="button" class="btn btn-danger" id="btn-delete">삭제</button>//1.
    </div>
</div>
...
```  
1. btn-delete  
+ 삭제 버튼을 수정 완료 버튼 옆에 추가  
+ 해당 버튼 클릭시 JS 에서 이벤트를 수신  
  
삭제 이벤트를 진행할 JS 코드 추가  
```javascript  
var main = {
    init : function () {
        ...

        $('#btn-delete').on('click', function () {
            _this.delete();
        });
    },

    ...

    delete : function () {
        var id = $('#id').val();

        $.ajax({
            type: 'DELETE',
            url: '/api/v1/posts/'+id, 
            dataType: 'json',
            contentType:'application/json; charset=utf-8',
        }).done(function () {
            alert('글이 삭제되었습니다.');
            window.location.href = '/'; 
        }).fail(function (error) {
            alert(JSON.stringify(error));
        });
    }
};

main.init();
```  
  
PostsService 메소드 추가  
```java  
...
public class PostsService {
    private final PostsRepository postsRepository;
    
    ...
    
    @Transactional
    public void delete (Long id) {
        Posts posts = postsRepository.findById(id).orElseThrow(() -> new IllegalArgumentException("해당 게시글이 없습니다. id=" + id));
        postsRepository.delete(posts); //1. JpaRepository 에서 이미 delete 메소드를 지원하고 있으니 이를 활용, 엔티티를 파라미터로 삭제할 수도 있고, deleteById 메소드를 이용하면 id 로 삭제할 수도 있다. 존재하는 Posts 인지 확인을 위해 엔티티 조회 후 그대로 삭제.
    }
}
```  
1. postsRepository.delete(posts)
+ JpaRepository 에서 이미 delete 메소드를 지원하고 있으니 이를 활용  
+ 엔티티를 파라미터로 삭제할 수도 있고, deleteById 메소드를 이용하면 id 로 삭제할 수도 있다.  
+ 존재하는 Posts 인지 확인을 위해 엔티티 조회 후 그대로 삭제  
  
PostsApiController 코드 추가  
```java  
public class PostsApiController {

    ...

    @DeleteMapping("/api/v1/posts/{id}")
    public Long delete(@PathVariable Long id) {
        postsService.delete(id);
        return id;
    }
}
```  
`Application.java`의 main 메소드 실행하고 [http://localhost:8080](http://localhost:8080) 으로 접속해서 확인  
[![그림 1-25](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img25.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img25.png)  
[![그림 1-26](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img26.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img26.png)  
[![그림 1-27](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img27.png)](/assets/Web/AWS/2020-04-09-SpringBoot-AWS-04-img27.png)  
  