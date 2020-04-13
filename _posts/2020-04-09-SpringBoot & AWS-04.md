---
title: "Ⅳ. 머스테치로 화면 구성하기"
excerpt: "서버 템플릿 엔진과 클라이언트 템플릿 엔진"

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
  
  
<!-- MyBatis, iBatis는 ORM(Object Relational Mapping)이 아니다. ORM은 객체를 매핑하는 것이고, SQL Mapper는 쿼리를 매핑한다. -->
## 머스테치 플러그인 설치  
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
  