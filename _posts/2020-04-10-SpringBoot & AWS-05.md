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






















