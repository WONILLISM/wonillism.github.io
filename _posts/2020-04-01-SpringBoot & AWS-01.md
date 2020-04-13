---
title: "Ⅰ. 인텔리제이로 스프링부트 시작하기"
excerpt: "인텔리제이 커뮤니티에서 프로젝트 생성하기"

categories:
    - SpringBoot & AWS
tags:
    - SpringBoot
    - Amazon Web Services
    - IntelliJ IDEA 
    - Gradle
    - Git
use_math: true;
last_modified_at: 2020-04-01

# published : false
--- 
> 개발 언어 : __Java 8(JDK 1.8)__  
> 개발 환경 : __Gradle 4.8 ~ Gradle 4.10.2__  
> 참조 :  
> [기억보단 기록을](https://jojoldu.tistory.com/)  
> [스프링 부트와 AWS로 혼자 구현하는 웹서비스 (프리렉, 이동욱 지음)](https://jojoldu.tistory.com/463)  
> [예제 코드 내려받기](http://bit.ly/fr-springboot)
  
  
## 인텔리제이 설치하기  
바로 인텔리제이를 내려받지 않고 젯브레인 툴박스를 이용해 보겠습니다. 툴박스는 인텔리제이를 만든 __젯브레인의 제품 전체를 관리해 주는 데스크 톱 앱__ 입니다.
  
[JET BRAINS 내려받기 페이지](https://www.jetbrains.com/toolbox-app/)
[![그림 1-1](/assets/Web/AWS/2020-04-01-SpringBoot-AWS-01-img01.png)](/assets/Web/AWS/2020-04-01-SpringBoot-AWS-01-img01.png)
  
  
화면에서 [DOWNLOAD] 버튼을 클릭해서 바로 설치를 진행하면 됩니다. 설치되었다면 __맥 OS에서는 화면 위쪽에, 윈도우에서는 화면 아래쪽__ 에 아이콘이 생겼을 것입니다.
해당 아이콘을 클릭하여 다음과 같이 툴박스 설정창을 열어 봅니다.
  
본인은 이미 설치된 여러 개발 도구가 있어 해당 도구들이 나오지만, 처음 설치한 분은 빈 화면이 나올 것입니다.
  
[IntelliJ IDEA Community -> Install]를 차례로 클릭해 설치합니다.
  
설치가 끝났다면 [IntelliJ IDEA Community -> 설정[톱니바퀴] -> Settings]를 차례로 클릭하면 인텔리제이에 관한 다양한 설정 기능을 볼 수 있습니다.
  
[![그림 1-2](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img02.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img02.png)
  
  
[![그림 1-3](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img03.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img03.png)
  
  
여기서 Maximum Heap Size가 750MB로 되어있습니다. 이 설정은 __인텔리제이를 실행하는데, 어느 만큼의 메모리를 할당할지를 결정__ 하는 값입니다.
기본값은 개발 PC의 메모리가 4G 이하일 때를 가정하고 설정된 값입니다.
본인의 개발 PC가 이보다 좋은 성능을 갖고 있다면 더 높여서 쾌적하게 사용하면 됩니다. 일반적으로 개발 PC의 메모리가 8G라면 1024~2048을, 16G라면 2048~4096을 선택해서 사용합니다.
  
  
## 인텔리제이 커뮤니티에서 프로젝트 생성하기
프로젝트를 생성해 보겠습니다. 툴박스 앱에서 인텔리제이 커뮤니티 아이콘을 클릭합니다.
  
그럼 다음과 같이 인텔리제이 로딩 화면이 보이며 시작됩니다.
  
  
[![그림 1-4](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img04.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img04.png)
  
  
로딩 화면이 끝나면 다음과 같이 본격적으로 인텔리제이의 기본환경 설정이 시작됩니다.
  
처음 설치할 경우에는 가져올 이전 설정이 없으므로 [Do not import setting -> OK]를 차례로 클릭합니다.
  
  
[![그림 1-5](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img05.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img05.png)
  
  
다음 설정은 테마입니다.
  
이클립스를 사용하는 개발자들이 가장 부러워하는 것이 인텔리제이의 다큘라 테마입니다.
  
`드라큘라가 아닙니다. 다크+드라큘라의 합성 테마라서 다큘라(Darcular)입니다. 다큘라 테마는 별도의 방법으로 설치할 수 있습니다.`
  
  
[![그림 1-6](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img06.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img06.png)
  
  
그다음 설정들은 단축키 설정, 런처 스크립트 설정, 기본 플러그인 선택이 있는데 기본으로 설정하고 넘어가겠습니다. 상세하게 알고싶다면 구글링해서 찾아보시길 바랍니다.
  
모든 설정이 끝나면 인텔리제이의 프로젝트 생성 화면이 나옵니다.
  
새로운 프로젝트를 생성할 것이기 때문에 [Create New Project]버튼을 클릭합니다.
  
  
[![그림 1-7](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img07.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img07.png)
  
  
[![그림 1-8](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img08.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img08.png)
  
JDK 설치가 안되어있는 분들은 Java 프로젝트를 선택하면 SDK(Software Development Kit)가 없다는 메세지가 뜹니다. 아래 Download JDK를 눌러 JDK(Java development Kit)를 설치해주면 됩니다.
  
  
[https://www.oracle.com/technetwork/java/javase/downloads](https://www.oracle.com/technetwork/java/javase/downloads)
  
  
그런데 자바 통합개발환경인 IntelliJ를 설치해줬는데 왜 또 설치를 하라고 하는걸까?
IDE(Integrated Development Environment)는 프로그램 개발을 위한 편집기, 컴파일러, 디버거등 등 실행 모듈개발에 필요한 기능을 통합적으로 모아놓은것이고
SDK(Software Development Kit)는 소프트웨어 개발을 위해 모아놓은 도구 및 라이브러리입니다. JDK는 SDK중 하나라고 보면 됩니다.

프로젝트 유형을 선택해야 하는데, 여기서는 그레이들[Gradle]을 선택해 프로젝트를 생성합니다.
  
[![그림 1-9](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img09.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img09.png)
  
  
다음은 GroupId와 ArtifactId를 등록합니다. 특히 ArtifactId는 프로젝트의 이름이 되기 때문에 원하는 이름을 작성해 주면 됩니다.
  
  
[![그림 1-10](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img10.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img10.png)
  
  
(화면 캡쳐 생략)
다음은 앞에서 선택한 그레이들의 옵션을 선택해야 합니다. 인텔리제이의 기본 설정값으로 그대로 두고 다음으로 넘어갑니다.
  
다음으로 넘어가면 새로 만들 프로젝트의 디렉토리 위치를 선택해야 합니다. 기본적으로는 ArtifactId가 프로젝트 이름이 됩니다. 기본으로 잡혀 있는 위치외에 
원하는 위치가 있다면 Project location에서 수정하면 됩니다.
  
이렇게 모든 설정이 끝나면 그레이들 기반의 자바 프로젝트가 생성됩니다.
  
  
[![그림 1-11](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img11.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img11.png)
  
  
## 그레이들 프로젝트를 스프링 부트 프로젝트로 변경하기
그레이들 프로젝트를 스프링 부트 프로젝트로 변경해 보겠습니다. 인텔리제이에서 __build.gradle__ 파일을 열어 봅니다. 다음과 같은 간단한 코드들만 있습니다.
  
```  
plugins {
    id 'java'
}

group 'com.freehyun.book'
version '1.0-SNAPSHOT'

sourceCompatibility = 1.8

repositories {
    mavenCentral()
}

dependencies {
    testCompile group: 'junit', name: 'junit', version: '4.12'
}
```  
  
앞의 코드들은 자바 개발에 가장 기초적인 설정만 되어있는 상태입니다. 여기에 스프링 부트에 필요한 설정들을 하나씩 추가하겠습니다.
  
먼저 __build.gradle__ 맨 위에 위치할 코드입니다.
  
```  
buildscript {
    ext {
        springBootVersion = '2.1.7.RELEASE'
    }
    repositories {
        mavenCentral()
        jcenter()
    }

    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
    }
}
```  
  
앞의 코드는 이 프로젝트의 플러그인 의존성 관리를 위한 설정입니다.
  
ext라는 키워드는 build.gradle에서 사용하는 전역변수를 설정하겠다는 의미인데, 여기서는 springBootVersion 전역변수를 생성하고 그 값을 '2.1.7.RELEASE'로 하겠다는 의미입니다.
즉, spring-boot-gradle-plugin 라는 스프링 부트 그레이들 플러그인의 2.1.7.RELEASE를 의존성으로 받겠다는 의미입니다.
  
다음은 앞서 선언한 플러그인 의존성들을 적용할 것인지를 결정하는 코드입니다.
  
```  
apply plugin : 'java'
apply plugin : 'eclipse'
apply plugin : 'org.springframework.boot'
apply plugin : 'io.spring.dependency-management'
```  
  
io.spring.dependency-management 플러그인은 스프링 부트의 의존성들을 관리해 주는 플러그인이라 꼭 추가해야만 합니다.  
앞 4개의 플러그인은 자바와 스프링 부트를 사용하기 위해서는 필수 플러그인들이니 항상 추가하면 됩니다. 나머지 코드는 다음과 같습니다.
  
```  
repositories {
    mavenCentral()
    jcenter()
}

dependencies {
    compile('org.springframework.boot:spring-boot-starter-web')
    testCompile('org.springframework.boot:spring-boot-starter-test')
}
```  
  
repositories는 각종 의존성(라이브러리)들을 어떤 원격 저장소에서 받을지를 정합니다. 기본적으로 mavenCentral를 많이 사용하지만, 최근에는 라이브러리 업로드 난이도 때문에 jcenter도 많이 사용합니다.  
jcenter는 라이브러리 업로드를 간단하게 하였습니다. 또한, jcenter에 라이브러리를 업로드하면 mavenCentral에도 업로드 될 수 있도록 자동화를 할 수 있습니다. 여기서는 mavenCentral, jcenter 둘 다 등록해서 사용하겠습니다.  
dependencies는 프로젝트 개발에 필요한 의존성들을 선언하는 곳입니다. 여기서는 org.springframework.boot:spring-boot-starter-web와 org.springframework.boot:spring-boot-starter-test를 받도록 선언되어 있습니다.  
이렇게 관리할 경우 각 라이브러리들의 버전 관리가 한 곳에 집중되고, 버전 충돌 문제도 해결되어 편하게 개발을 진행할 수 있습니다.  
이 코드를 모두 적용한 전체 코드는 다음과 같습니다.
  
```  
buildscript {
    ext {
        springBootVersion = '2.1.7.RELEASE'
    }
    repositories {
        mavenCentral()
        jcenter()
    }

    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
    }
}

apply plugin : 'java'
apply plugin : 'eclipse'
apply plugin : 'org.springframework.boot'
apply plugin : 'io.spring.dependency-management'


group 'com.freehyun.book'
version '1.0-SNAPSHOT'
sourceCompatibility = 1.8

repositories {
    mavenCentral()
    jcenter()
}

dependencies {
    compile('org.springframework.boot:spring-boot-starter-web')
    testCompile('org.springframework.boot:spring-boot-starter-test')
}
```  
  
코드 작성이 다 되었다면 알람 오른쪽의 [Enable Auto-import]를 클릭하면 build.gradle 변경이 있을 때마다 자동으로 반영이 되며, 외쪽[Import Changes] 버튼을 클릭하면 1번만 반영 됩니다.
  
  
[![그림 1-12](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img12.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img12.png)
  
  
spring-boot-starter-web과 spring-boot-starter-test와 관련되 라이브러리들을 받게되면 [Gradle] 탭을 클릭해서 의존성들이 잘 받아졌는지 확인해 봅시다.
  
  
[![그림 1-13](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img13.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img13.png)
  
  
## 인텔리제이에서 깃과 깃허브 사용하기
먼저 [https://github.com/](https://github.com/) 에 계정이 없다면 가입을 먼저 해야 합니다. 깃허브의 계정이 있으면 바로 인텔리제이 화면으로 이동합니다.  
인텔리제이에서 단축키로 윈도우 기준 [Ctrl+Shift+A)를 사용해 Action 검색창을 열어 __share project on GitHub__ 을 검색합니다.
  
  
[![그림 1-14](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img14.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img14.png)
  
  
해당 Action을 선택한 후 엔터를 누르면 깃허브 로그인 화면이 나옵니다.  
본인 깃허브 계정으로 로그인을 하고 [Repository name] 필드에 등록한 이름으로 __깃허브에 저장소가 생성__ 됩니다.
  
  
[![그림 1-15](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img15.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img15.png)
  
  
[Share]버튼을 클릭하면 깃허브 저장소와 동기화를 진행합니다.  
프로젝트의 첫 번째 커밋을 위한 팝업창이 등장합니다.
  
여기서 __.idea 디렉토리는 커밋하지 않습니다.__ 이는 인텔리제이에서 프로젝트 __실행시 자동으로 생성되는 파일들__ 이기 때문에 깃허브에 올리기에는 불필요 합니다.
  
  
[![그림 1-16](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img16.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img16.png)
  
  
커밋과 푸시가 성공했다면 본인의 깃허브 계정으로 이동합니다.
  
  
[![그림 1-17](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img17.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img17.png)
  
  
깃 허브와 동기화가 되었으니 좀 전에 커밋을 하면서 대상에서 제외했던 .idea 폴더를 앞으로의 __모든 커밋 대상에서 제외되도록__ 처리를 해보겠습니다.  
깃에서 특정 파일 혹은 디렉토리를 관리 대상에서 제외할 때는 __.gitignore파일__ 을 사용합니다. 이 파일 안에 기입된 내용들은 모두 깃에서 관리하지 않겠다는 것을 의미합니다.  
인텔리제이에서는 이 .gitignore 파일에 대한 기본적인 지원이 없습니다. 대신 플러그인에서 .gitignore 지원을 하고 있습니다.  
.ignore 플러그인에서 지원하는 기능들은 다음과 같습니다.  
  
+ 파일 위치 자동완성  
+ 이그노어 처리 여부 확인  
+ 다양한 이그노어 파일 지원(.gitignore, .npmignore, .dockerignore 등등)  
  
.ignore 플러그인을 설치해 보겠습니다. 인텔리제이에서 단축키 [Ctrl+Shift+A] 를 사용해 Action 검색창을 열어 __plugins__ 을 검색합니다.
Plugins Action을 선택하면 플러그인 설치 팝업창이 나옵니다.
  
  
[![그림 1-18](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img18.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img18.png)
  
  
.ignore을 검색하거나 목록에서 찾아 다음과 같이 [.ignore] -> [Install] 버튼을 차례로 클릭해서 설치합니다.
  
  
[![그림 1-19](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img19.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img19.png)
  
  
__인텔리제이를 다시 시작해야만 설치한 플러그인이 적용__  
설치가 다 되었다면 이제 ignore파일을 생성해 보겠습니다.  
프로젝트 이름을 선택한 뒤, 마우스 오른쪽 버튼을 누르거나 단축키를 눌러 생성 목록을 열어 봅니다. 단축키는 [Alt+Insert] 입니다.  
  
생성 목록 아래에 [.ignore file -> gitignore file(Git)]을 선택해서 .gitignore파일을 생성하겠습니다.
  
  
[![그림 1-20](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img20.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img20.png)
  
  
.gitignore 생성 화면이 나옵니다.
  
  
[![그림 1-21](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img21.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img21.png)
  
  
생성된 .gitignore 파일에 깃 체크 대상에서 제외하고 싶은 이름을 작성하면 됩니다.  
__인텔리제이에서 자동으로 생성되는 파일__ 들을 모두 이그노어 처리하겠습니다. 다음과 같이 코드를 추가합니다.
  
  
[![그림 1-22](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img22.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img22.png)
  
  
이렇게 이그노어 처리된 것을 깃허브에도 반영해 보겠습니다. 깃 커밋 창을 열어 봅니다. 단축키는 [Ctrl+K] 입니다.
  
  
[![그림 1-23](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img23.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img23.png)
  
  
.gitignore 파일을 선택하고, 메시지를 작성하였다면 [Ctrl+Alt+K] 눌러 Commit합니다.  
커밋하면 푸시 화면이 나오는데 [Alt+P]를 눌러 푸시를 진행합니다.  
  
[![그림 1-24](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img24.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img24.png)
  

푸시가 성공했다면 다시 깃허브의 프로젝트로 이동해서 커밋과 푸시가 성공적으로 반영된 것을 확인합니다.
  
  
[![그림 1-25](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img25.png)](/assets/Web/AWS/2020-04-02-SpringBoot-AWS-01-img25.png)
  
  