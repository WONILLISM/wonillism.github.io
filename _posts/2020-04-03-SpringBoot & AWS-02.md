---
title: "테스트 코드 작성과 롬복 전환하기"
excerpt: "Hello Controller 테스트 코드"

categories:
    - SpringBoot & AWS
tags:
    - SpringBoot
    - Amazon Web Services
    - IntelliJ IDEA 
    - Gradle
    - Git
use_math: true;
last_modified_at: 2020-04-07

# published : false
--- 
> 개발 언어 : __Java 8(JDK 1.8)__  
> 개발 환경 : __Gradle 4.8 ~ Gradle 4.10.2__  
> 참조 :  
> [기억보단 기록을](https://jojoldu.tistory.com/)  
> [스프링 부트와 AWS로 혼자 구현하는 웹서비스 (프리렉, 이동욱 지음)](https://jojoldu.tistory.com/463)  
> [예제 코드 내려받기](http://bit.ly/fr-springboot)
  
  
## Hello Controller 테스트 코드 작성하기  
[New -> Package]
[![그림 1-1](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img01.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img01.png)  
  
패키지명 작성  
[![그림 1-2](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img02.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img02.png)  
  
[New -> Java class]  
[![그림 1-3](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img03.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img03.png)  
  
[![그림 1-4](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img04.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img04.png)  
  
클래스 코드 작성  
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```  
  
[Alt+Enter] Import 등록  
[![그림 1-5](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img05.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img05.png)  
  
Application 클래스는 프로젝트의 __메인 클래스__  
__@SpringBootApplication__ 으로 인해 스프링 부트의 자동 설정, 스프링 Bean 읽기와 생성을 모두 자동으로 설정  
__@SpringBootApplication이 있는 위치부터 설정을 읽어__ 가기 때문에 클래스는 항상 __프로젝트의 최상단에 위치__  
main 메소드에서 실행하는 __SpringApplication.run__ 으로 인해 내장 __WAS__(Web Application Server)를 실행  
서버에 __Tomcat을 설치할 필요가 없게되고,__ 스프링 부트로 만들어진 __Jar__ 파일(실행 가능한 Java 패키징 파일)로 실행  
  
  
web 패키지 생성  
[![그림 1-6](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img06.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img06.png)  
  
[![그림 1-7](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img07.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img07.png)  
  
컨트롤러와 관련된 클래스들은 모두 이 패키지에  
  
컨트롤러 클래스 생성  
[![그림 1-8](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img08.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img08.png)  
  
[![그림 1-9](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img09.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img09.png)  
  
src/main/java/com/freehyun/book/springboot/web/HelloController
```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController //1.
public class HelloController {

    @GetMapping("/hello") //2.  
    public String hello() {
        return  "hello";
    }
}
```  
1. @RestController
+ 컨트롤러를 JSON을 반환하는 컨트롤러로 만들어 준다.  
+ @ResponseBody를 각 메소드마다 선언했던 것을 한번에 사용할 수 있게 해준다.  
2. @GetMapping
+ HTTP Method 인 Get 의 요청을 받을 수 있는 API 를 만들어 준다.  
+ 예전에는 @RequestMapping(method = RequestMethod.GET)으로 사용되었다. 이제 이프로젝트는 /hello 로 요청이 오면 문자열 hello 를 반환하는 기능을 가지게 된다.  
  
__테스트 코드로 검증__ src/test/java 디렉토리에 앞에서 생성했던 패키지를 그대로 다시 생성  
[![그림 1-10](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img10.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img10.png)  
  
[![그림 1-11](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img11.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img11.png)  
  
HelloControllerTest 클래스 생성
/src/test/java/com/freehyun/book/springboot/web/HelloControllerTest
```java
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;

import static org.hamcrest.Matchers.is;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@RunWith(SpringRunner.class) //1.
@WebMvcTest(controllers = HelloController.class) //2.
public class HelloControllerTest {

    @Autowired //3.
    private MockMvc mvc; //4.

    @Test
    public void hello가_리턴된다() throws Exception {
        String hello = "hello";

        mvc.perform(get("/hello")) //5.
                .andExpect(status().isOk()) //6.
                .andExpect(content().string(hello)); //7.
    }
}
```  
1. @RunWith(SpringRunner.class)
+ 테스트를 진행할 때 JUnit 에 내장된 실행자 외에 다른 실행자를 실행  
+ 여기서는 SringRunner 라는 스프링 실행자를 사용  
+ 즉, 스프링 부트 테스트와 JUnit 사이에 연결자 역할을 한다.  
2. @WebMvcTest
+ 여러 스프링 테스트 어노테이션 중, Web(Spring MVC)에 집중할 수 있는 어노테이션  
+ 선언할 경우 @Controller, @ControllerAdvice 등을 사용할 수 있다.  
+ 단, @Service, @Component, @Repository 등은 사용할 수 없다.  
+ 여기서는 컨트롤러만 사용하기 때문에 선언  
3. @Autowired
+ 스프링이 관리하는 빈(Bean)을 주입받는다.  
4. private MockMvc mvc
+ 웹 API 를 테스트할 때 사용  
+ 스프링 MVC 테스트의 시작점  
+ 이 클래스를 통해 HTTP GET, POST 등에 대한 API 테스트를 할 수 있다.  
5. mvc.perform(get("/hello"))
+ MockMvc 를 통해 /hello 주소로 HTTP GET 요청을 한다.  
+ 체이닝이 지원되어 아래와 같이 여러 검증 기능을 이어서 선언할 수 있다.  
6. .andExpect(status().isOk())
+ mvc.perform 의 결과를 검증  
+ HTTP Header 의 Status 를 검증  
+ 우리가 흔히 알고 있는 200, 404, 500 등의 상태를 검증  
+ 여기선 OK 즉, 200인지 아닌지 검증  
7. .andExpect(content().string(hello))
+ mvc.perform 의 결과를 검증  
+ 응답 본문의 내용을 검증  
+ Controller 에서 "hello"를 리턴하기 때문에 이 값이 맞는지 검증  
  
테스트 코드 실행  
[![그림 1-12](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img12.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img12.png)  
  
테스트 메소드 실행 결과  
[![그림 1-13](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img13.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img13.png)  
  
Application.java 파일로 이동 __main 메소드 Run 'Application.main()' 버튼 클릭__  
[![그림 1-14](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img14.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img14.png)  
  
메인 메소드 실행 로그  
[![그림 1-15](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img15.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img15.png)  
  
브라우저 결과 확인  
[![그림 1-16](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img16.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img16.png)  
  
## 롬복 소개 및 설치하기  
롬복은 자바 개발할 때 자주 사용하는 코드 Getter, Setter, 기본생성자, toString 등을 어노테이션으로 자동 생성 해준다.  
  
build.gradle 의존성 추가  
[![그림 1-17](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img17.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img17.png)  
  
롬복 플러그인 설치 [Ctrl+Shift+A]  
[![그림 1-18](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img18.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img18.png)  
  
[![그림 1-18](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img18.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img18.png)  
  
롬복 설정 [Ctrl+Alt+S] -> Build, Execution, Deployment -> Annotation Processors -> Enable annotation processing 체크  
[![그림 1-22](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img22.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img22.png)  
  
## Hello Controller 코드를 롬복으로 전환하기  
web 패키지에 dto 패키지를 추가, HelloResponseDto 생성  
[![그림 1-19](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img19.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img19.png)  
  
HelloResponseDto 코드 작성
/src/main/java/com/freehyun/book/springboot/web/dto/HelloResponseDto
```java
import lombok.Getter;
import lombok.RequiredArgsConstructor;

@Getter //1.
@RequiredArgsConstructor //2. 
public class HelloResponseDto {

    private final String name;
    private final int amount;
}
```  
1. @Getter
+ 선언된 모든 필드의 get 메소드를 생성해 준다.  
2. @RequiredArgsConstructor
+ 선언된 모든 final 필드가 포함된 생성자를 생성해 준다.  
+ final 이 없는 필드는 생성자에 포함되지 않는다.  
  
dto 테스트 패키지와 클래스  
[![그림 1-20](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img20.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img20.png)  
  
HelloResponseDtoTest 코드 작성  
/src/test/java/com/freehyun/book/springboot/web/dto/HelloResponseDtoTest
```java
import org.junit.Test;
import static org.assertj.core.api.Assertions.assertThat;

public class HelloResponseDtoTest {

    @Test
    public void 롬복_기능_테스트() {
        //given
        String name = "test";
        int amount = 1000;

        //when
        HelloResponseDto dto = new HelloResponseDto(name, amount);

        //then
        assertThat(dto.getName()).isEqualTo(name); //1,2
        assertThat(dto.getAmount()).isEqualTo(amount);
    }
}
```  
1. assertThat
+ assertj 라는 테스트 검증 라이브러리의 검증 메소드  
+ 검증하고 싶은 대상을 메소드 인자로 받는다.  
+ 메소드 체이닝이 지원되어 isEqualTo와 같이 메소드를 이어서 사용할 수 있다.  
2. isEqualTo
+ assertj 의 동등 비교 메소드  
+ assertThat 에 있는 값과 isEqualTo 의 값을 비교해서 같을 때만 성공  
  
dto 테스트 메소드 결과  
[![그림 1-21](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img21.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img21.png)  
  
만약 다음 그림 처럼 테스트 실패 했을 경우  
[![그림 1-23](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img23.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img23.png)  
  
```
dependencies {
	compileOnly 'org.projectlombok:lombok:1.18.12'
	annotationProcessor 'org.projectlombok:lombok:1.18.12'
	
	testCompileOnly 'org.projectlombok:lombok:1.18.12'
	testAnnotationProcessor 'org.projectlombok:lombok:1.18.12'
}
```  
build.gradle 의 dependencies를 수정하거나 `gradle/wrapper/gradle-wrapper.properties` 에서 distributionUrl의 값을 `https\://services.gradle.org/distributions/gradle-4.10.2-bin.zip` 와 같이 바꿔주고 gradle을 downgrade한다.  
[![그림 1-24](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img24.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img24.png)  
  
gradle 5부터는 어노테이션을 구별해서 추가해줘야 한다고 한다. 전자의 경우 계속해서 추가 대응이 필요하기 때문에 개인적으로는 처음 실습은 gradle 4로 권장한다.  
  
__HelloController__ 에도 새로 만든 ResponseDto를 사용하도록 코드를 추가  
```java
    @GetMapping("/hello/dto")
    public HelloResponseDto helloDto(@RequestParam("name") String name, @RequestParam("amount") int amount) { //1.
        return new HelloResponseDto(name, amount);
    }
```  
1. @RequestParam
+ 외부에서 API 로 넘긴 파라미터를 가져오는 어노테이션  
+ 여기서는 외부에서 name(@RequestParam("name")) 이란 이름으로 넘긴 파라미터를 메소드 파라미터 name(String name)에 저장하게 된다.  
  
__HelloControllerTest__ 코드 추가  
```java
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;

import static org.hamcrest.Matchers.is;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;

@RunWith(SpringRunner.class)
@WebMvcTest(controllers = HelloController.class)
public class HelloControllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    public void hello가_리턴된다() throws Exception {
        String hello = "hello";

        mvc.perform(get("/hello"))
                .andExpect(status().isOk())
                .andExpect(content().string(hello));
    }

    @Test
    public void helloDto가_리턴된다() throws Exception {
        String name = "hello";
        int amount = 1000;

        mvc.perform(
                get("/hello/dto")
                        .param("name", name) //1.
                        .param("amount",String.valueOf(amount)))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.name", is(name))) //2.
                .andExpect(jsonPath("$.amount", is(amount)));
    }
}
```  
1. param
+ API 테스트할 때 사용될 요청 파라미터를 설정  
+ 단, 값은 String 만 허용  
+ 그래서 숫자/날짜 등의 데이터도 등록할 때는 문자열로 변경해야만 가능  
2. jsonPath
+ JSON 응답값을 필드별로 검증할 수 있는 메소드  
+ $를 기준으로 필드명을 명시  
+ 여기서는 name 과 amount 를 검증하니 $.name, $.amount 로 검증  
  
HelloControllerTest.helloDto가_리턴된다 dto API 테스트 결과
[![그림 1-25](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img25.png)](/assets/Web/AWS/2020-04-07-SpringBoot-AWS-02-img25.png)  