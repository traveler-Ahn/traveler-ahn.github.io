---
layout: post
title:  "2019/08/28 스프링 프레임워크 (인프런 강좌 정리)"
subtitle: "2019/08/28 스프링 프레임워크 (인프런 강좌 정리)"
categories: til
tags: til
comments: true
---

- 인프런 [스프링 프레임워크 강좌](https://www.inflearn.com/course/스프링-프레임워크_renew) (자바 스프링 프레임워크) 정리본 입니다. 
	- 중간 중간 다른곳에서 잘 쓰인 글들을 참조하여 정리한 곳도 있습니다.
	- 스프링에 대한 개념을 차츰차츰 추가하여 꾸준히 업데이트 할 예정이고, 더 시간이 지난다면 각 파트별로 쪼갤 예정입니다.

---

# Spring Framework (190828)
**인프런 강의**

[자바 스프링 프레임워크](https://www.inflearn.com/course/스프링-프레임워크_renew)

---

`Framework 관련 다른 곳에 쓰인 글을 참조한 내용입니다. 출처는 밑에 있습니다.:)`

### 프레임워크(Framework)란

"소프트웨어의 구체적인 부분에 해당하는 설계와 구현을 재사용이 가능하게끔 일련의 협업화된 형태로 클래스들을 제공하는 것" - *랄프 존슨 (Ralph Johnson)*

1. <span style="color:#FF0033">**프레임 워크는 구조 품질을 보장한다.**</span>
   - 구조 품질: "Great Software is well-designed, well-coded, and easy to maintain, reuse, and extend"
   - Framework  = Design Pattern + class Library
   - 구체적이며 확장 가능한 기반 코드를 갖고 있다.
     - 소프트웨어의 구조 및 기반이 되는 클래스를 제공한다.
   - 설계자가 의도하는 여러 디자인 패턴의 집합으로 구성되어 있다.
2. <span style="color:#FF0033">**Framework는 반제품이다.**</span>
   - Application의 틀과 구조를 결정한다.
   - Application 코드의 상당 부분을 제공한다.
     - Application 코드는 Framework에 설계되어 있는 제어 흐름에 따라 동작한다.
     - 즉, Framework 코드가 그 위에 개발된 개발자의 User 코드를 호출하고 제어한다.
   - 개발자는 Application의 핵심 로직에만 집중할 수 있다.
3. <span style="color:#FF0033">**Framework의 장점**</span>
   - 생산성
     - business logic에만 집중할 수 있어 생산성이 증대
   - 코드 품질
     - 코드의 재사용 및 유지보수 용이
     - 확장성을 가진 코드 설계 가능

`프레임워크 vs. 라이브러리`

- 프레임워크란,
  - 소프트웨어의 구체적인 부분에 해당하는 설계와 구현을 재사용이 가능하게끔 일련의 협업화되 형태로 클래스들을 제공하는 것
  - Ex) 자동차의 프레임, 즉 기본적으로 구성하고 있는 뼈대
- 라이브러리란,
  - 자주 사용되는 로직을 재사용하기 편리하도록 잘 정리한 일련의 코드들의 집합
  - Ex) 자동차의 기능을 하는 부품

### 스프링 프레임워크(Framework)란

#### 스프링(Spring)의 개념

자바 엔터프라이즈 개발을 편하게 해주는 경량급 오픈소스 애플리케이션 프레임워크

- Lightweight Java Application Framework
  - 목표: POJO 기반의 Enterprise Application 개발을 쉽고 편하게 할 수 있도록 한다.
  - Java Application을 개발하는데 필요한 하부구조(Infrastructure)를 포괄적으로 제공한다.
  - Spring이 하부구조를 처리하기 때문에 개발자는 Application 개발에 집중할 수 있다.
- 자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크
- 동적인 웹사이트를 개발하기 위한 여러가지 서비스를 제공한다.
- 대한민국 공공기관의 웹 서비스 개발 시 사용을 권장하고 있는 전자 정부 표준 프레임워크의 기반기술

`POJO와 EJB`

- POJO
  - Plain Old Java Object
  - 상속, 인터페이스가 필요없는 아주 단순하고 가벼운 객체를 의미한다.
  - 원하는 business logic만 넣을 수 있도록 돕는다.
- EJB
  - Enterprise JavaBeans
  - 기업 환경의 시스템을 구현하기 위한 서버 측 컴포넌트 모델이다.
  - 즉, EJB는 애플리케이션의 업무 로직을 갖고 있는 서버 애플리케이션으로 특정 환경에 종속적이고 무겁다.

#### 스프링(Spring)의 주요 특징

![spring](https://drive.google.com/uc?id=1fstDF1ErqVH3-6HpVsPv7Skma0st_vaS)

1. <span style="color:#FF0033">**DI(Dependency Injection)**</span>
   - **의존 관계 주입**
   - 각각의 계층이나 서비스들 간에 의존성이 존재할 경우 Spring이 서로 연결시켜 준다.
   - POJO 객체들 사이의 의존관계를 Spring이 알아서 연관성을 맺어준다.
   - Ex) 다양한 DB 사용이 가능
2. <span style="color:#FF0033">**AOP(Aspect Orientated Programming)**</span>
   - **관점 중심 프로그래밍**
   - Spring은 핵심적인 비즈니스 로직과 관련이 없으나 여러 곳에서 공통적으로 쓰이는 기능들을 분리 (공통 관심사를 분리)하여 개발하고 실행 시에 서로 조합할 수 있는 AOP를 지원한다.
   - 이를 통해 코드를 단순하고 깔끔하게 작성할 수 있다.
   - ![AOP](https://drive.google.com/uc?id=1Vi8us1FU89fiefieWrrYbGgb91PIPF6A)
   - 횡단 관심을 수행하는 코드 (Logging, Security, Transaction 등)는 aspect라는 특별한 객체로 모듈화하고 weaving이라는 작업을 통해 모듈화한 코드를 핵심 기능에 끼워넣을 수 있다.
3. <span style="color:#FF0033">**Portable Service Abstraction**</span>
   - **이식 가능한 서비스 추상화**
   - Spring은 완성도가 높은 라이브러리와 연결할 수 있는 인터페이스를 제공한다.
   - 즉, 다른 프레임워크들과의 통합을 지원한다.
   - ![PortableServiceAbstraction](https://drive.google.com/uc?id=1dj5WhGPRHocs7OiLONWY9ZhFhjy3bQNJ)

#### 스프링(Spring)의 구성요소

![spring-structure](https://drive.google.com/uc?id=1fmmFm1SAM-u4fl2nWtdSkYn9bMuAhzWg)

- Core Container 중 Bean Container는 POJO라는 객체를 관리한다.
- Spring에서 제공하는 다양한 기능 중 필요한 것을 선택적으로 사용한다. 

------

#### [스프링(Spring) 관련 Reference]

> - https://gmlwjd9405.github.io/2018/10/26/spring-framework.html

------



### 1. Java 프로그래밍

> 스프링 프레임워크가 무엇인지에 대해서 학습한다.

- **<span style="color:#FF0033">1-1 스프링 프레임워크 (Spring Framework)</span>**

  - 프레임워크 : 개발을 위해 추상적으로 정의해둔 틀 (작업의 효율성을 위해 만든다.) `개발자가 개발 본연의 업무에만 집중할 수 있는 구조`를 만든다.
  - 스프링 프레임워크는 주요기능으로 DI, AOP, MVC, JDBC 등을 제공한다.
  - Java 기반 프레임워크
    - 웹개발 -> Spring Framework
    - 모바일개발 -> Android Framework

  

<img src="https://drive.google.com/uc?id=1CMa3rkCuMSl__Tlqfxqu55wH3_qvUVCB">



- **<span style="color:#FF0033">1-2 스프링 프레임워크 모듈</span>**
  - 모듈? 코드로 구성된 라이브러리 (기능이 추상적으로 정의되어 있다.)
  - 스프링의 모든 기능은 모듈화 되어있고, 개발자의 필요에 따라 필요한 모듈을 설정(조립)하여 가져다쓴다.

<img src="https://drive.google.com/uc?id=1vJJgEWnOdNzf2oqwgI2odpiPOcOtzOtj">

- **<span style="color:#FF0033">1-3 스프링 컨테이너 (IoC)</span>**
  - 스프링 설정파일(.xml 혹은 .java)을 만들어서 객체(Bean)들을 모아놓은 큰 메모리 공간

<img src="https://drive.google.com/uc?id=1XCnwPUw_YeUIcyqChouf9XR8uy16viMO">



------



### 2강 개발환경 구축

> 스프링을 이용한 애플리케이션 구축에 필요한 개발환경에 대해 학습한다.

- **<span style="color:#FF0033">2-1 Java 설치</span>**
  - JDK 설치 (java 1.8 ver사용) 오라클 홈페이지에서 다운받아서 설치한다.
- **<span style="color:#FF0033">2-2 환경변수 설정</span>**
  - javac.exe, java.exe 파일 환경변수 설정
- **<span style="color:#FF0033">2-3 IDE (이클립스) 다운로드</span>**
  - 그냥 홈페이지에서 다운받는다.



------



### 3강 스프링 프로젝트 생성

> Maven builder tool을 이용해서 스프링 프로젝트를 생성하는 방법에 대해서 학습합니다.

> Build? 개발자가 소스코드를 짜고, 컴파일 과정 및 빌드 과정을 통해 실행파일을 생성하게 된다. 이때 build 과정을 거친다. 이때 Spring에선 빌드하는 툴로 Maven을 사용하게 된다. (안드로이드는 gradle)

- **<span style="color:#FF0033">3-1 프로젝트 생성</span>**
  - Group id: 전체적인 프로젝트의 id를 적는 것
  - Artifact Id: 현재 해당하는 프로젝트의 id를 적는 것

![p1](https://drive.google.com/uc?id=1Y809JOu_CmMxxYZPIIueBdUdHxq5ANgN)

![p2](https://drive.google.com/uc?id=1NigNxH3NGwd7Q65lbsmNCWa8P5xBD7lp)

- **<span style="color:#FF0033">3-2 pom.xml 작성</span>**
  - 스프링에서 사용하게 될 필요한 모듈을 가져오기 위해 셋팅하는 곳
  - 필요한 모듈을 해당 xml파일에 기입하면 자동으로 스프링으로 해당 모듈(라이브러리)이 불러와진다.

![p3](https://drive.google.com/uc?id=1M9CqAh37GhjPf0y7hWLM7MOixDfxUBFL)



![p4](https://drive.google.com/uc?id=1oawYfQobJKGS_ocm4YYyOeh-OUtnmL_H)

- **<span style="color:#FF0033">3-3 폴터 및 pom.xml 파일의 이해</span>**
  - pom.xml 파일 ? 스프링에서 사용하게 될 필요한 모듈을 가져오기 위해 셋팅하는 곳
  - 프로젝트가 여러 개가 있을 때 각 pom.xml 파일에 의해서 필요한 라이브러리만 다운로드 하여 사용하게 된다.
  - 한 번 라이브러리를 다운 받으면, 다른 프로젝트를 위해서 다시 다운 받을 필요없고, 다른 프로젝트에서도 공유하여 사용된다.
  - pom.xml 파일의 build 태그는 실제 maven빌드를 할 때 필요한 설정파일 구성

![p5](https://drive.google.com/uc?id=1dVs2_pS_kaI0ZbnKY6DIGcuA0zQPpTYg)

![p6](https://drive.google.com/uc?id=1Qd79X3nBh0d3VfX-2oWaL-MGZuXG9ypJ)



------



### 4강 처음 해보는 스프링 프로젝트

> 스프링을 이용해서 간단한 프로그램을 만들어본다.

- **<span style="color:#FF0033">4-1 Java 파일을 이용한 프로젝트 실행</span>**
  - Spring framework에선 기존 Java프로젝트와는 다르게 pom.xml을 통해서 spring에서 제공하는 다양한 모듈을 이용할 수 있다.

<img src="https://drive.google.com/uc?id=1r9FQOCa2Vbci-_fMYNkcagcWjuM9rZnC">

<img src="https://drive.google.com/uc?id=1i84GTqlXJcFjBqnOWpGV1tIqV5j_8wi0">

- <span style="color:#FF0033">**4-2 우선 따라 해보는 스프링 프로젝트**</span>
  - 스프링 방식의 '의존'을 이용하기 위해서는 Main에서 TransportationWalk 객체를 직접 생성하지 않고, 스프링 설정파일(.xml)을 이용해 보기로 한다. 가장 큰 차이점은 Java파일에서 이용한 new 연산자를 이용하지 않고 스프링 설정파일(.xml)을 이용하는 것이다.
  - 실제 new라는 키워드를 사용하지 않아도 applicationContext.xml파일 내의 설정에 의해 자동으로 bean 객체가 생성(메모리에 로딩)된다.
  - applicationContext.xml(컨테이너)에 의해 미리 메모리에 만들어진 객체를 MainClass에서 가져다 쓰면된다.
  - 가져다 쓸 때 스프링 컨테이너에 접근(ctx)해서 미리 생성된 bean 객체에 접근(getBean())하게 된다.

<img src="https://drive.google.com/uc?id=1zhOleP9DBGL45WZEWJX65ZV5Ykc7lmMc">



<img src="https://drive.google.com/uc?id=1e4GbXs-bJXG0qW2hrPPgiRYGYdCgixJy">



------



### 5강 또 다른 프로젝트 생성 방법

> 폴더(java.resources)와 파일(pom.xml)을 직접 만들어 프로젝트를 생성하는 방법에 대해서 학습합니다.

> 이클립스에서 프로젝트를 생성하는 것이 아니라, 직접 폴더생성과 함께 project를 만들고, eclipse에서 import하는 방법으로 프로젝트를 생성한다.

- <span style="color:#FF0033">**5-1 폴더(java.resources)와 파일(pom.xml) 만들기**</span>

![project](https://drive.google.com/uc?id=1PnK1wpSPgIA3xsk1g8bNNpsRKS06ihdV)

- <span style="color:#FF0033">**5-2 이클립스에서 import 하기**</span>

![project2](https://drive.google.com/uc?id=1aZumZrgB3LPCB0aqsPtvaFheZLArt6xp)

![project3](https://drive.google.com/uc?id=1c2FWMzF2rwNHvs-j6tNFA8zuQ8bAWsiy)



------



### 6강 DI(Dependency injection)

> DI를 이용한 프로그래밍 방법과 스프링에서의 DI에 대해서 학습한다.

> Spring에서는 spring 설정파일(.xml 혹은 java파일)을 이용해서 객체를 생성(메모리에 로딩됨)하고, 생성된 객체를 생성된 컨테이너에 접근하여 getBean 메소드를 통해 객체를 사용하게 된다.

- <span style="color:#FF0033">**6-1 DI (Dependency Injection이란?)**</span>
  - OOP 프로그래밍의 하나의 방법론 ( `객체들이 서로 의존관계를 갖는다.`)
  - 배터리 일체형 (내부적으로 new 생성자를 통한 배터리(객체) 생성)
  - 배터리 분리형 1 (배터리가 떨어지면 교체한다. 이 과정에서 배터리를 주입할 때 생성자를 통해 주입한다.)
  - 배터리 분리형 2 (배터리가 떨어지면 교체한다. 이 과정에서 배터리를 주입할 때 setter메소드를 통해 주입한다.)
  - DI 관점에서 필요에 의해 일체형이든 분리형이든 사용할 수 있다.

![di1](https://drive.google.com/uc?id=1THrKTV1wp2hz1eXC-tzwKRpPIB_Sf6Pe)



![di2](https://drive.google.com/uc?id=1KN_AhBj9BEsVw8ZgTyUTBOOroqN99yhy)

- <span style="color:#FF0033">**6-2 스프링 DI 설정방법**</span>
  - 스프링 설정파일(applicationContext.xml)을 이용해서 Spring container를 만들고, 이러한 과정에서 메모리에 객체(Bean)가 로딩된다.
  - 이러한 객체를 가져다 쓰기위해 각 컨테이너에 접근하여 getBean 메소드를 사용한다.
  - 컨테이너 내에서 객체끼리 의존관계를 맺게 되는데, 이를 스프링 설정파일에서 미리 정의한다.
  - 맨 처음 studentDao객체를 bean객체 생성, 나머지 서비스객체에서 생성자 태그를 통해 dao객체를 참조하게 된다. 이를 통해 의존객체 구현

![di3](https://drive.google.com/uc?id=1iTUuJn5moA9cuddYGGovnB61KY3zzl9t)



![di4](https://drive.google.com/uc?id=1YqSpNwBSBksHKfGqVt0nXods0joQejiV)

- 위의 스프링 설정파일(.xml) 수정을 통해 assembler 클래스가 따로 필요로 하지 않게 된다. 기존에 assembler 클래스의 주된 목적은 studentDao객체를 new연산자를 통해 생성해서 각 서비스 객체에 주입해주는 역할이였음 (아래의 6강 소스코드 참조)
- 위에서 studentDao Bean객체는 default로 singleton 범위가 지정되기 때문에 모든 서비스 bean객체는 하나의 studentDao bean 객체를 공유하게 된다.
- Main함수에서도 따로 assembler 객체를 사용하지 않고, 컨테이너에서 getBean 메소드를 통해 원하는 서비스에 해당하는 객체를 가져다가 사용하게 된다. 



------

------



#### [6강에서 나온 소스코드]

- 하나의 Dao를 모든 서비스 객체가 주입해서 공유한다. `의존객체 주입!`
- 이를 통해 하나의 데이터 베이스를 모든 서비스가 공유하게 된다. 
- 여기서 구현된 코드는 Java source 코드를 통한 DI 구현 (lec06Pjt002 코드 참조)

<img src="https://drive.google.com/uc?id=1U2eOtx9ArhIlbI5GeB79pJT3jFBwSrMq">



------

------



### 7강 다양한 의존 객체 주입

> 스프링에서 의존객체를 주입하는 다양한 방법에 대해서 학습한다.

- <span style="color:#FF0033">**7-1 생성자를 이용한 의존 객체 주입**</span>
  - 스프링 설정파일(.xml)에서 의존 객체(studentDao)를 각 서비스 객체의 생성자 parameter에 주입하게 된다.

![di1](https://drive.google.com/uc?id=1YlLUVDIem8fZ5ZsDaEnUkbeliNJFGuFq)

- <span style="color:#FF0033">**7-2 setter를 이용한 의존 객체 주입**</span>
  - setter메소드를 사용해서 따로 해당 value를 주입하지 않고, 컨테이너가 생성될 시 의존 객체의 값을 주입한다.
  - 스프링 설정파일(.xml)에서 setter에서 set을 빼고 나머지 이름을 property tag의 name 속성 값으로 넣어준다. 여기서 첫 번째 문자는 소문자로 기입한다.

![di2](https://drive.google.com/uc?id=17exZLWVIsN11ei2m2D06CF7HuTaudMPN)

- <span style="color:#FF0033">**7-3 List타입 의존 객체 주입**</span>
  - 아래에서 개발자(developers)에 대한 value값이 list로 들어오기 때문에 이에 대해서 list 태그를 활용한다.

![ di3](https://drive.google.com/uc?id=150cmj0ncjITYYOWm9HiCYDbXWwEnXk7V)

- <span style="color:#FF0033">**7-4 Map타입 의존 객체 주입**</span>
  - entry와 key 태그를 활용하여 의존객체를 주입한다.

![di4](https://drive.google.com/uc?id=1iESdoVqalzIq3NrcacWDFLg8CEpKFutY)



------



### 8강 스프링 설정 파일 분리

> 스프링 설정파일을 효율적으로 관리하기 위해서 설정파일을 분리하는 방법에 대해 학습한다.

> 스프링 설정파일에서 Bean 태그를 이용해서 Bean 객체를 만든다. -> 여기서 모든 Bean객체(메모리 로드)를 만들게 된다.
>
> - 생성자를 통한 의존객체 주입 -> Constructor 태그
> - setter를 통한 의존객체 주입 -> Parameter를 통한 의존객체 주입

=> 하나의 스프링 설정파일에서 모든 내용을 관리하게 된다면 가독성과 개발의 편의성이 낮아지기 때문에 기능별 스프링 설정파일을 관리하게 된다. 어떻게하면 효율적으로 분리할 수 있을까?



- <span style="color:#FF0033">**8-1 스프링 설정 파일 분리**</span>

  - 분리하기위한 명확한 가이드라인은 없지만, 주로 기능별로 스프링 설정파일을 분리하곤한다.

  - 분리한 파일을 사용하기 위해서, 스프링 설정파일을 통해 컨테이너를 만들 때, 

    1. 각 파일들을 하나 씩 class path의 인자로 넣을지, (**주로 이 방법을 선호한다.**)

       <img src="https://drive.google.com/uc?id=1TkwvxqOfN1Uq4aNSt70luQ1oIT9ZfvxN">

    2. 각 파일들을 import를 통해서 하나의 파일처럼 만들어서 class path의 인자로 넣을지 

    선택하면 된다. 성능상의 큰 차이는 없다.

    ​		<img src="https://drive.google.com/uc?id=1NZ-mYqRTy4aPIt38sEXEj_3LqbXoz7BW">

![spring-config](https://drive.google.com/uc?id=1dCmnp-Leu-JHdQgsZMlg-Ft2ndxk01Ad)

> 가독성과 관리의 문제를 위해서 설정파일을 분리하게된다.



- <span style="color:#FF0033">**8-2 빈(Bean) 객체의 범위**</span>
  - Singleton: 레퍼런스는 다르지만, 같은 메모리 공간을 참조한다. (Bean객체 생성시 default 작업)
  - Bean 객체를 정의할 때 scope속성의 값을 변경함에 따라 객체의 범위(singleton, prototype)를 설정할 수 있다.

![spring-config](https://drive.google.com/uc?id=1C50Bl6aimNR7ISZOkDMzsM3L8xJidRMZ)



------



### 9강 의존객체 자동 주입

> 의존객체를 자동으로 주입하는 방법에 대해서 학습한다.

- <span style="color:#FF0033">**9-1 의존객체 자동 주입이란?**</span>
  - 스프링 설정파일에서 의존 객체를 주입할 때 생성자 <constructor-org> 또는 setter <property> 태그로 의존 대상 객체를 명시하지 않아도 스프링 컨테이너가 자동으로 의존 대상 객체를 찾아서 의존 대상 객체가 필요한 객체에 주입해주는 기능이다. 
  - 구현 방법은 `@Autowired`와 `@Resource`어노테이션을 이용해서 쉽게 구현할 수 있다.

![di-injection1](https://drive.google.com/uc?id=1oqwjrH0MLkQCGITLnhlkEYW6cTWnm2Oe)



- <span style="color:#FF0033">**9-2 @Autowired** (lec09Pjt)</span>
  - 주입하려고 하는 `객체의 타입이 일치`하는 객체를 자동으로 주입한다.
  - 생성자, 프로퍼티(속성), 메소드(setter)에 사용될 수 있다.
  - 프로퍼티나 메소드에 자동주입을 위한 어노테이션 선언시에는 디폴트 생성자를 필수로 작성해야한다.

![di-injection-autowired](https://drive.google.com/uc?id=1FnFG1gMk1iD6lbnTnwQWx1myPpcBwcGI)



- <span style="color:#FF0033">**9-3 @Resource** (lec09Pjt)</span>
  - 주입하려고 하는 `객체의 이름이 일치`하는 객체를 자동으로 주입한다.
  - 생성자가 아닌, 프로퍼티(속성)과 메소드(setter)에만 사용될 수 있다. 생성자에는 사용될 수 없다.
  - 프로퍼티나 메소드에 자동주입을 위한 어노테이션 선언시에는 디폴트 생성자를 필수로 작성해야한다.

![di-injection-resource](https://drive.google.com/uc?id=1Ji4o5v16K43SzDS8J18QLax6RaWFLjaC)



------



### 10강 의존객체 선택

> 다수의 빈(Bean)객체 중 의존 객체의 대상이 되는 객체를 선택하는 방법에 대해서 학습한다.

- <span style="color:#FF0033">**10-1 의존객체 선택**</span>
  - 동일한 Bean 객체가  2개 이상인 경우 스프링 컨테이너는 자동 주입 대상 객체를 판단하지 못해서 Exception을 발생시킨다.
  - 그래서 `Qualifier 태그와 어노테이션`을 사용해서 정확하게 어떤 의존객체가 쓰이는지 지정해주어야 한다.

![do-selection](https://drive.google.com/uc?id=1W9gHLqApB1CxugqtvvDagLH3Vf9XhBOc)

- <span style="color:#FF0033">**10-2 의존객체 자동 주입 체크**</span>
  - 의존객체가 자동으로 주입되야하는 상황에서 required라는 속성 값을 true로 정한다.
  - 만약 의존객체가 자동으로 주입되지 않아도 되는 상황이라면 required 속성값을 false로 지정한다.

![di-check](https://drive.google.com/uc?id=1-hoZ7G-JCgM6LV_w6EDNTqXyJBWnAe2A)

- <span style="color:#FF0033">**10-3 @Injection**</span>
  - @Autowired와 유사하게 @Inject 어노테이션을 이용해서 의존객체를 자동으로 주입할 수 있다.
  - Autowired와의 차이점은 required 속성의 유무 차이이다. 
  - Autowired 어노테이션을 사용할 때 `Qualifiler 태그와 어노테이션`을 통해 원하는 객체를 지정할 수 있지만, Inject어노테이션을 사용할때는, @Named(value="id속성값")라는 어노테이션만을 사용해서 의존객체 주입을 지정하면 된다.

![injection](https://drive.google.com/uc?id=1I0lxlDqGEegUtGmFgHSPxbF6zxnZQM3_)



------



### 11강 생명주기 (Life Cycle)

> 스프링 컨테이너와 빈(Bean) 객체의 생명주기(Life Cycle)에 대해 학습한다.

- <span style="color:#FF0033">**11-1 스프링 컨테이너 생명주기**</span>
  - 스프링 컨테이가 어느 시점에 생성되는지, 어느 시점에 소멸되는지
  - GenericXmlApplicationContext Class와 new 키워드를 이용할 때 스프링 컨테이너가 생성된다. (메모리에 스프링 컨테이너가 올라간다.)
  - 스프링 컨테이너의 close 메소드를 호출하여 컨테이너를 종료시킨다. (메모리 해제)()

![lc](https://drive.google.com/uc?id=1p3CRFStcqbFjkGTx0eX9OVfdK1dh78Rp)



- <span style="color:#FF0033">**11-2 빈(Bean)객체 생명주기**</span>
  - 빈 객체가 어느 시점에 생성(메모리에 객체가 올라가고)되는지, 어느 시점에 소멸(메모리에서 객체가 해제는)되는지
  - Bean 객체가 `생성되고 소멸될 때 특정작업(메소드)을 실행`시키는 방법
    - 0. 주로 DB연결이나 인증작업시에 작업이 수행되곤 한다.
    - 1. 빈 객체에서 afterPropertiesSet() / destroy() 메소드 구현 (인터페이스 구현)
    - 2. init-method, destroy-method 속성 이용
  - 스프링 컨테이너가 생성되는 시기와 빈 객체가 생성되는 시점은 같다. 
  - 빈 객체가 생성될 때 의존객체 주입도 동시에 이루어진다.
  - 스프링 컨테이너를 close메소드를 호출할 때 소멸되고, 빈 객체도 소멸된다.

![bean-lc](https://drive.google.com/uc?id=1574aAIVarJjxk-CboAuByguP2SsTF0_m)



- <span style="color:#FF0033">**11-3 init-method, destroy-method 속성**</span>
  - 스프링 설정파일(.xml)에 빈 객체를 기입할 때 해당 속성(init/destroy)과 그에 해당하는 메소드를 구현한다. (이름 맞춰주는 것 중요)

![lc-property](https://drive.google.com/uc?id=1JpaYWDPuniQDMF_cHfBLjCeR_oqsegHI)



------



### 12강 어노테이션을 이용한 스프링 설정

> XML을 이용한 스프링 설정파일 제작을 Java 파일로 제작할 수 있는 방법을 학습한다.

> `자바의 어노테이션`을 이용해서 스프링 설정파일을 만드는 방법을 학습한다.

- <span style="color:#FF0033">**12-1 XML 파일을 Java 파일로 변경하기**</span>

![anotation1](https://drive.google.com/uc?id=1LklW1p73s_kDCye09MIV3psALARz6pij)

- <span style="color:#FF0033">**12-2 Java 파일 분리**</span>
  - 스프링 설정파일로 사용되는 자바파일을 분리해서 관리하고, 이를 하나의 파일처럼 import 하는 방법을 학습했다.
  - 왜 분리하냐? 유지보수 측면에서 분리를 하고, 기본적으로 기술적인 용도로 .java파일을 분리하곤 한다.
  - 비록 나눠서 관리가 된다고 해도, 스프링 컨테이너는 하나로 유지되며 모든 bean 객체가 이 컨테이너 위로 올라가게 된다. (서로 같은 컨테이너를 공유하게 된다. `의존객체 자동 주입시 중요한 내용!` 12-2 코드!)

![anotation2](https://drive.google.com/uc?id=1QY9JfnVsSYh1owlYphAzslCEf6C8Otwa)

- <span style="color:#FF0033">**12-3 @Import 어노테이션**</span>

![anotation3](https://drive.google.com/uc?id=1jbYmKIvd3l4YasoW2c7GX1lM2RmdnBQ_)



------

------



#### [12강 소스코드]

- 스프링 설정파일을 .xml에서 어노테이션을 이용한 스프링 설정
  - @Configuration 어노테이션으로 현 자바 파일이 스프링 설정파일로 사용될 것이라는 것을 명시한다.
  - @Bean 어노테이션을 통해 현 메소드는 각각 Bean 객체 생성한다는 것을 명시해준다.

```java
// 유사한거 다 빼고, 위에서 사용되었던 .xml파일에서 의존객체 주입 설정했던 것들을
// 자바 코드로 바꿔서 입력한다.

@Configuration
public class MemberConfig {
	
	@Bean
	public StudentDao studentDao() {
		return new StudentDao();
	}
	
	@Bean
	public StudentRegisterService registerService() {
		return new StudentRegisterService(studentDao());
	}
	
	...
	
	@Bean
	public DataBaseConnectionInfo dataBaseConnectionInfoDev() {
		DataBaseConnectionInfo inforDev = new DataBaseConnectionInfo();
		inforDev.setJdbcUrl("jdbc:oracle:thin:@localhost:1521:xe");
		inforDev.setUserId("scott");
		inforDev.setUserPw("tiger");
		
		return inforDev;
	}
	
	@Bean
	public DataBaseConnectionInfo dataBaseConnectionInfoReal() {
		DataBaseConnectionInfo inforReal = new DataBaseConnectionInfo();
		inforReal.setJdbcUrl("jdbc:oracle:thin:@192.168.0.1:1521:xe");
		inforReal.setUserId("masterid");
		inforReal.setUserPw("masterid");
		
		return inforReal;
	}
	
	@Bean
	public EMSInformationService informationService() {
		EMSInformationService info = new EMSInformationService();
		info.setInfo("Education Management System program was developed in 2015.");
		info.setCopyRight("COPYRIGHT(C) 2015 EMS CO., LTD. ALL RIGHT RESERVED. CONTACT MASTER FOR MORE INFORMATION.");
		info.setVer("The version is 1.0");
		info.setsYear(2015);
		info.setsMonth(1);
		info.setsDay(1);
		info.seteYear(2015);
		info.seteMonth(2);
		info.seteDay(28);
		
		ArrayList<String> developers = new ArrayList<String>();
		developers.add("Cheney.");
		developers.add("Eloy.");
		developers.add("Jasper.");
		developers.add("Dillon.");
		developers.add("Kian");
		info.setDevelopers(developers);
		
		Map<String, String> administrators = new HashMap<String, String>();
		administrators.put("Cheney", "cheney@springPjt.org");
		administrators.put("Jasper", "jasper@springPjt.org");
		info.setAdministrators(administrators);	
		
		...
		
		return info;
	}
}
```



------

------



### 13강 웹 프로그래밍 설계 모델

> 스프링 MVC 프레임워크 기반의 웹 프로그래밍 구조에 대해서 학습한다.

- <span style="color:#FF0033">**13-1 웹 프로그래밍을 구축하기 위한 설계 모델**</span>
  - **Model1**구조를 사용할 때는, Service & DAO & JSP(view)를 하나의 파일에서 관리하기 때문에 개발속도가 빠르지만, 하나의 파일에서 Logic & View & Data Access 부분이 동시에 관리되기 때문에문서가 장황해지고, 유지보수 관점에서 큰 단점이 존재한다.
  - **Model2** => `MVC; Model, View, Controller` 각 기능을 서로 나눠서 `모듈화`를 통해 전체를 관리한다.  
  - Model2 접근을 통해서 전체적인 프로그램의 유지보수가 쉬워진다. 대부분이 이 모델을 따른다.

![design-model](https://drive.google.com/uc?id=1wQtcN2F_gIFTx6fGVamqbsCR9De0rfRH)

![design-model](https://drive.google.com/uc?id=1phafm5tIYmTEvHGsqe5UbVf0UIeTi-E4)

- <span style="color:#FF0033">**13-2 스프링 MVC 프레임워크 설계구조**</span>
  - `DispatcherServlet => HandlerMapping`: 여러 Controller중에 가장 적합한 Controller를 선택
  - `DispatcherServlet => HandlerAdapter`: 하나의 Controller중 여러 메소드 중에 적합합 메소드를 선택
  - Controller 뒤에는 Service & DAO 기능이 있다.
  - Controller의 메소드에서 얻은 결과를 model 객체(데이터)를 통해 반환한다.
  - Controller를 통해 얻은 결과를 ViewResolver 및 View를 통해서 Jsp => html을 반환한다.

![mvc](https://drive.google.com/uc?id=1Y91KX1-EBrzHqNZ6ZIwFoCllhJScDkFg)

- <span style="color:#FF0033">**13-3 DispatcherServlet 설정**</span>

  - `도로의 신호등과 같은 역할`
  - Dispatcher servlet을 web.xml에 등록 및 처음 url mapping
  - servlet-context.xml => 스프링 설정파일!, Dispatcher servlet이 만들어질 때 컨테이너를 만들게 된다.

  #### (참조) web.xml 이란?  ([참조 사이트](https://gmlwjd9405.github.io/2018/10/29/web-application-structure.html))

  #### 개념

  - web application의 설정을 위한 `deployment descriptor`

  #### 역할

  - Deploy할 때 Servlet의 정보를 설정해준다.
  - 브라우저가 JavaServlet에 접근하기 위해서는 WAS(Ex. Tomcat)에 필요한 정보를 알려줘야 해당하는 Servlet을 호출할 수 있다.
    - 정보 1) 배포할 Servlet이 무엇인지
    - 정보 2) 해당 Servlet이 어떤 URL에 매핑되는지
  - 하기의 이미지에서 1) aliases 설정하는 부분 2) URL 매핑 하는 과정이 이루어진다.

![dispatcher](https://drive.google.com/uc?id=15-itVnFNI3gOn5zXj9mQtTwf4gSBB2gr)

- DispatcherServlet 설정할 때, init-param으로 스프링 설정파일을 지정할 때와 지정하지 않았을 때의 컨테이너 생성 결과는 아래와 같다. (굳이 지정하지 않아도 기본적으로 필요한 객체는 생성하게 된다.)

![dispatcher_2](https://drive.google.com/uc?id=1Izmpjs8ZFYn1A4m4z0-ExZHBo1Hb1Cyj)

- <span style="color:#FF0033">**13-4 Controller 객체 - @Controller**</span>
  - Controller 결과는 Model & View 객체로 반환된다.
  - 생성하는 방법은 스프링 설정파일에 해당 태그(<annotation-driven> 이 태그를 작성함으로써 Controller를 만들어주기 위해 사용될 다양한 빈(Bean) 객체가 컨테이너 위로 올라가게 된다.)를 작성하고, 실제 Controller로 사용하게 될 Class에 @Controller 어노테이션을 사용한다.

![controller](https://drive.google.com/uc?id=1IEXAJCHV3pry3sL4mh0w0Utciythqo_M)

- <span style="color:#FF0033">**13-5 Controller 객체 - @RequestMapping**</span>
  - Controller에는 다양한 메소드가 존재하는데, 사용자가 원하는 메소드를 찾기 위해 필요한 도구가 @RequestMapping 어노테이션이다.
  - URL을 통해 요청한 값에 따라서 미리 명시된 RequestMapping에 의해 해당되는 메소드가 실행된다.

![request-mapping](https://drive.google.com/uc?id=1lJ-ZeDy6eudXYR6z17OnHcKoFpl_GQzG)

- <span style="color:#FF0033">**13-6 Controller 객체 - Model 타입의 파라미터**</span>
  - 개발자는 Controller를 통해 나온 결과를 Model 객체에 데이터를 담아서 DispatcherServlet에 전달하게 된다.
  - DispatcherServlet에 전달된 Model 데이터는 View에서 가공되어 클라이언트에게 응답처리 된다.

![model-parameter](https://drive.google.com/uc?id=1-Myz72CdUFq-dlp-UeUcVWxRLab_wZXU)

- <span style="color:#FF0033">**13- 7 View 객체**</span>
  - ViewResolver 객체에 미리 정의된 내용에 따라서 Controller의 결과가 Jsp 파일로 반환하는 역할을 하게 된다.
  - 

![view](https://drive.google.com/uc?id=1Cj-dMhhRTZDElWCZQy2Zat-Hwx-GU01k)

- <span style="color:#FF0033">**13-8 전체적인 웹 프로그래밍 구조**</span>

![total-architecture](https://drive.google.com/uc?id=1xFpHOro-tGwE30me7nlsHwab96IFOtfc)



------



### 14강  스프링 MVC 웹서비스-1

> 스프링 MVC 프레임워크를 이용한 웹 프로그래밍 구현방법에 대해서 학습한다.

- <span style="color:#FF0033">**14-1 웹 서버(Tomcat) 다운로드**</span>
- <span style="color:#FF0033">**14-2 웹 서버 (Tomcat)와 이클립스 연동**</span>
- <span style="color:#FF0033">**14-3 이클립스에 STS (Spring Tool Suit) 설치** </span>
  - STS 3 standalone 설치
  - 직접 다운받아서 sts4 버전 설치
    - https://tlo-developer.tistory.com/82
- <span style="color:#FF0033">**14-4 STS를 이용한 웹프로젝트 생성**</span>
- <span style="color:#FF0033">**14-5 스프링 MVC 프레임워크를 이용한 웹프로젝트 분석**</span>

> MVC 모델을 스프링으로 쉽게 구현을 하기 위해서 sts plugin을 설치하고 사용하게 된다. 



------



### 15강 스프링 MVC 웹서비스-2

> 스프링 MVC 프레임워크를 이용한 웹 프로그래밍 구현 방법에 대해서 학습한다.

- <span style="color:#FF0033">**15-1 프로젝트 전체 구조**</span>

  - `java 파일`

    : java파일들이 주로 패키지로 묶여서 관리된다. 웹 애플리케이션에서 사용되는 Controller, Service, DAO 객체들이 위치한다.

  - `resources 폴더`

    : JSP 파일을 제외한 html, css, js 파일등이 위치한다. 

  - `webapp 폴더`

    : 웹과 관련된 파일 / 폴더들 (스프링 설정파일, JSP 파일, HTML/CSS/JS 파일등)이 위치한다.

  - `spring 폴더`

    : 스프링 컨테이너를 생성하기 위한 스프링 설정파일(servlet-context.xml)이 위치한다. 

  - `views 폴더`

    : View로 사용될 JSP 파일이 위치한다.

  - `web.xml 파일`

    : DispatcherServlet을 서블릿으로 등록한다. & 이 과정에서 스프링 컨테이너를 생성하게 된다.

  - `pom.xml 파일`

    : 메인 Repository에서 프로젝트에 필요한 라이브러리를 Local Repo.로 내려받기 위한 메이븐 설정파일이다.

<img src="https://drive.google.com/uc?id=1lcv5NvSR4nco2TxSuqpDTB13s7grvRRf">

- <span style="color:#FF0033">**15-2 web.xml**</span>
  - 13강 web.xml 내용 참조 (여기에서 주된 역할은 DispatcherServlet을 서블릿으로 등록하는 것이다.)
  - 웹 어플리케이션에서 최초 사용자의 요청을 DispatcherServlet이 받게되는데, 이를 위해서 URL 매핑을 해주어야 한다.

<img src="https://drive.google.com/uc?id=1Cozt9Zg6_PfcCty_nE4SS17XAmkYavqa">

- <span style="color:#FF0033">**15-3 DispatcherServlet**</span>
  - DispatcherServlet을 통해 사용자가 요청한 정보를 처리하여 알맞는 정보를 응답하는 과정

<img src="https://drive.google.com/uc?id=1u8uxL23zdrH-pWp0vuZsI7C0NgNe4j4J">

- <span style="color:#FF0033">**15-4 servlet-context.xml**</span>

  - DispatcherServlet을 서블릿으로 등록할 때, 스프링 설정파일(servlet-context.xml)도 초기화 파라메터로 지정이 되고 이로인해 스프링 컨테이너가 생성된다. (Spring Container: Controller의 lifecycle 관리) 

  - 스프링 설정파일(servlet-context.xml)에서는,

    1. pre-defined 클래스로부터 `빈(bean) 객체를 생성하고 조립하는 역할`을 한다.

    2. resources로 사용되는 파일들의 위치를 매핑시켜준다.

    3. Controller에서 받은 View정보를 이용해서 사용자에게 어떤 JSP 파일을 보여줄지 설정한다.   

       이러한 작업을 처리해 줄 InternalResourceViewResolver 클래스로부터 Bean 객체 (ViewResolver) 생성

<img src="https://drive.google.com/uc?id=1mGzrg4VsxfYW7UyAqYZW2udnUisgi3CN">



<img src="https://drive.google.com/uc?id=1CUsEMjn5A9deAy7HVLJPzIcLmPlC0gxY">



<img src="https://drive.google.com/uc?id=1_F1DPeTycclbrtCnp6P_hiJh4g9C4oeD">



- <span style="color:#FF0033">**15-5 Controller (컨트롤러)**</span>
  - 사용자의 요청을 실제로 처리하는 객체들이 존재한다.
  - 하기의 코드에서 간단한 Controller의 역할을 확인 할 수 있는데, 
    - 여기서
      1. 어떤 view 파일을 보일건지 (home -> home.jsp (ViewResolver에 의해서))
      2. jsp파일에 어떤 데이터(view에서 활용되는 파일)를 뿌릴건지 (주고 받는 Model 객체에 의해서)

<img src="https://drive.google.com/uc?id=1txym16M-JU7PiEfdGjI_TfEO6c0SU3ZK">

<img src="https://drive.google.com/uc?id=1f234IiXybRNLsSGi-HpIxRNLm8qn3GmD">

- <span style="color:#FF0033">**15-6 View (뷰)**</span>
  - 클라이언트 요청정보(URL 맵핑 값)에 해당하는 JSP 파일을 뿌려준다.

<img src="https://drive.google.com/uc?id=14jscaC2-0ZeMDgm3IBKCzgZUm4NWZJGA">



------



### 16강 STS를 이용하지 않은 웹 프로젝트

> 스프링 MVC 프레임워크를 이용한 웹프로그램 구현 방법에 대해서 학습한다.



**폴더생성** (src -> main -> java, webapp -> resources -> WEB-INF -> spring, views) -> 

**각 설정파일 설정** (pom.xml, web.xml, servlet-context.xml, root-context.xml) -> 

**Java 및 JSP 파일 생성** (컨트롤러와 뷰 작성) -> 

**실행**

- <span style="color:#FF0033">**16-1 스프링 MVC 웹 애플리케이션 제작을 위한 폴더 설정**</span>
- <span style="color:#FF0033">**16-2 pom.xml 및 이클립스 import**</span>
- <span style="color:#FF0033">**16-3 web.xml 작성**</span>
- <span style="color:#FF0033">**16-4 스프링 설정 파일 (servlet-context.xml) 작성**</span>
- <span style="color:#FF0033">**16-5 root-context.xml 작성**</span>
- <span style="color:#FF0033">**16-6 컨트롤러와 뷰 작성**</span>
- <span style="color:#FF0033">**16-7 실행**</span>



------



### 17강 Service & Dao 객체 구현

> 웹 프로그래밍의 구조에서 Service와 DAO 객체의 구현에 대해서 학습한다.
>
> Bean 객체 생성시에 어노테이션을 이용한 자동 객체 생성 및 주입 방법에 대해서 학습한다.

- <span style="color:#FF0033">**17-1 웹 어플리케이션 준비**</span>
  - 웹 어플리케이션의 일반적인 프로그램 구조

<img src="https://drive.google.com/uc?id=1osrUUY7Ky60DVaW3mKXiZ12Yq2BxT_UT">

- <span style="color:#FF0033">**17-2 한글 처리**</span>
  - web.xml파일에서 filter를 설정하여 모든 url에 맵핑하면 한글처리 완료

<img src="https://drive.google.com/uc?id=1iGZpFTQRY0Bu2p7r_AAaNU-ymlknr-84">

- <span style="color:#FF0033">**17-3 Service 객체 구현**</span>

  - 빈(Bean) 객체로 올리는 방법 3가지

    - **방법1** `new 연산자`를 이용해서 service 객체를 생성(메모리에 올리고)하고 참조한다.

    - **방법2** `스프링 설정파일(servlet-context.xml)에 bean 객체를 등록` 하고, @Autowired 어노테이션을 이용해서 의존객체 자동주입을 한다.

    - **방법3** `어노테이션을 활용`하여 자동으로 빈(Bean) 객체에 담고, 이러한 빈 객체를 이용한다.

      #####        객체를 주입하는 쪽 클래스에서,

      1. `@Repository어노테이션`을 이용하거나, 

      2. `@Component 어노테이션`을 이용하거나

      3. `@Service 어노테이션`을 이용한다.

         

         ##### 객체를 주입 당하는 쪽 클래스에서,

      1. `@Resource 어노테이션` 이용한다.
      2. `@Autowired 어노테이션` 이용한다.

<img src="https://drive.google.com/uc?id=1dhLxOxhPe4KEy5R0Zm7LIGiqrjOiqhWc">

- <span style="color:#FF0033">**17-4 DAO 객체 구현**</span>
  - @Repository 어노테이션과 @Autowired 어노테이션을 이용해서 DAO 빈(bean) 객체를 자동으로 생성하고 의존주입을 한다.

<img src="https://drive.google.com/uc?id=1uqDeDR8XNy9s4k86ixM5_YEgzX3_2eoe">



------

 

### 18강 Controller 객체 구현 - I

> 컨트롤러의 URL 맵핑과 파라미터 처리 방법에 대해서 학습한다.

- <span style="color:#FF0033">**18-1 웹 어플리케이션 준비**</span>

<img src="https://drive.google.com/uc?id=1ktorwEXOrGYETXzuzyd2L9hgoBt81N7r">

- <span style="color:#FF0033">**18-2 @RequestMapping을 이용한 URL 맵핑**</span>
  - 클래스와 메소드에 RequestMapping을 적용하여 URL 맵핑을 구현한다.
    - `클래스 RequestMapping` : 기능에 따른 컨트롤러 클래스 제작
    - `메소드 Requestmapping` : 각 컨트롤러안의 세부기능 구현
  - RequestMapping method 속성을 설정하여 HTTP 전송 정보를 처리할 수 있다.

<img src="https://drive.google.com/uc?id=1mjgPsJWeE9y_eTO9ml07ONwXR1xwqqQc">

<img src="https://drive.google.com/uc?id=1sBL4KAwRFvQM43O2ZFsO5j3206SSRrTv">

- <span style="color:#FF0033">**18-3 요청 파라미터**</span>

  > 사용자가 HTTP request를 활용하여 전송한 정보를 서버에서 어떻게 처리할지에 대한 방법론

  - `HttpServletRequest 객체`를 이용한 HTTP 전송 정보 얻기
    - 해당 메소드의 파라미터로 선언된 객체를 이용해서 전송된 HTTP 정보를 얻을 수 있다.

  <img src="https://drive.google.com/uc?id=1lAtr0CzxAPYll2J1uePuR4xggdzyRYf3">

  

  - `@RequestParam 어노테이션`을 이용한 HTTP 전송 정보 얻기
    - 어노테이션을 활용하여 간편한 방법으로 전송된 HTTP 전송 정보를 얻을 수 있다.
    - RequestParam 어노테이션 안에 속성으로 defaultValue를 넣어줄 수 있다. (또한, required=true | false)

  <img src="https://drive.google.com/uc?id=1VZAw_S-j28KohQD4TlViwO7X1i1gI9xm">

  

  - `커맨드 객체`를 이용한 HTTP 전송 정보 얻기 (가장 실무에서 많이 쓰인다.)

    > 커맨드 객체를 사용하면 코드의 양을 줄일 수 있고, 코드가 깔끔해진다.

    - Ex) 하기 이미지에 대한 설명; Member 커맨드 클래스 선언필요 (반드시 with getter/setter 만들어야 함)
    - 또한, 이 클래스에 대한 속성 값은 html form 에서의 name과 이름이 같아야 한다. (커맨드 객체)
    - 사용하기 위한 메소드의 파라미터로 해당 커맨드 객체를 넣고,
    - 뷰에서  커맨드 객체를 사용할 때는,
      1. 전송된 커맨드 객체의 메소드(getter)를 활용한다.
      2. Model 객체를 활용한다.

  <img src="https://drive.google.com/uc?id=1ZbKNNqC1Kx-Sys2lxiFYKzVKsYyKuAIb">

```java
// 커맨드 객체 이용관련 source code
// 커맨드 객체를 뷰에서 활용하기 위해 Model 객체를 사용하고 있다.
@RequestMapping(value="/memJoin", method=RequestMethod.POST)
public String memJoin(Model model, Member member) {

    //      해당 코드가 사라지게 된다.
    //		String memId = request.getParameter("memId");
    //		String memPw = request.getParameter("memPw");
    //		String memMail = request.getParameter("memMail");
    //		String memPhone1 = request.getParameter("memPhone1");
    //		String memPhone2 = request.getParameter("memPhone2");
    //		String memPhone3 = request.getParameter("memPhone3");

    service.memberRegister(member.getMemId(), member.getMemPw(), member.getMemMail(),
                member.getMemPhone1(), member.getMemPhone2(), member.getMemPhone3());

    model.addAttribute("memId", member.getMemId());
    model.addAttribute("memPw", member.getMemPw());
    model.addAttribute("memMail", member.getMemMail());
    model.addAttribute("memPhone", member.getMemPhone1() + " - " + member.getMemPhone2() 
                       + " - " + member.getMemPhone3());

    return "memJoinOk";
}
```



```java
// 커맨드 객체를 사용한다면 Model 파라미터를 사용하지 않아도 된다.
// 뷰(jsp파일)에서 커맨드 객체의 메소드를 호출하여 정보를 사용할 수 있다.
@RequestMapping(value="/memJoin", method=RequestMethod.POST)
public String memJoin(Member member) {

    service.memberRegister(member.getMemId(), member.getMemPw(), member.getMemMail(),
                member.getMemPhone1(), member.getMemPhone2(), member.getMemPhone3());

    return "memJoinOk";
}
```

```jsp
<!-- 위의 파일을 처리하는 memJoinOk.jsp코드 -->
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ page session="false" %>
<html>
<head>
	<title>Home</title>
</head>
<body>
	<h1> MEMBER JOIN OK </h1>
	
    <!-- 커맨드 객체를 이용해서 jsp에서 요청 값을 사용하는 방법 -->
	ID : ${member.memId} <br />
	PW : ${member.memPw} <br />
	Mail : ${member.memMail} <br />
	
	<a href="/"> MAIN </a>
</body>
</html>
```



------



### 19강 Controller 객체 구현 - II

> 컨트롤러의 URL 맵핑과 파라미터 처리 방법에 대해서 학습한다.

- <span style="color:#FF0033">**19-1 @ModelAttribute**</span>
  - @ModelAttribute 어노테이션을 이용하면 `커맨드 객체의 이름을 변경`할 수 있고, 변경된 이름은 `뷰에서 커맨드 객체의 속성을 참조`할 때 사용될 수 있다.
  - @ModelAttribute 어노테이션을 메소드에 적용하면, `어떤 뷰에서든 해당 메소드를 호출할 수 있다.` URL 맵핑에 의해서 어떤 메소드가 실행되든지 ModelAttribute가 붙어있는 메소드는 꼭 실행된다. 그래서 뷰단에서 바로 사용가능하다.

<img src="https://drive.google.com/uc?id=1XOZY5fnkOwhx0r-us1HXeT7Rke0Onc5c">

```java
// Controller 클래스
...
    
@ModelAttribute("serverTime")
public String getServerTime(Locale locale) {

    Date date = new Date();
    DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);

    return dateFormat.format(date);
}
...
```

```jsp
<!--serverTime 메소드를 가져다 쓰는 뷰(.jsp) 파일 -->

<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ page session="false" %>
<html>
    <head>
        <title>Home</title>
    </head>
    <body>
        <h1>
            Hello world!  
        </h1>

        <P>  The time on the server is ${serverTime}. </P>
    </body>
</html>
```



- <span style="color:#FF0033">**19-2 커맨드 객체 프로퍼티 데이터 타입**</span>

  - 커맨드 객체가 다루게 되는 데이터가 `기초데이터 타입`인 경우

  <img src="https://drive.google.com/uc?id=1UYdMuzXW3BnPEIHk_QC-hyPBau9_Xn1V">

  

  - 커맨드 객체가 다루게 되는 데이터가 `중첩 커맨드 객체를 이용한 List 구조`인 경우
    - MemPhone이라는 커맨드 객체를 하나 더 만들어고 각 속성에 대해 getter/setter를 만들어준다.

  <img src="https://drive.google.com/uc?id=1wDl39DptduDfzYfMH5CGCEM0Fe-3GDNt">

  ```java
  // Member.java
  
  public class Member {
  	
  	private String memId;
  	private String memPw;
  	private String memMail;
  	private List<MemPhone> memPhones;
  	private int memAge;
  	private boolean memAdult;
  	private String memGender;
  	private String[] memFSports;
  	
      // 데이터가 기초데이터 타입일 때 커맨드 객체 구현
      public String getMemId() {
  		return memId;
  	}
  	public void setMemId(String memId) {
  		this.memId = memId;
  	}
  	
      ... 
      
      // 데이터가 커맨드 객체를 이용한 List 구조일때 커맨드 객체 구현
  	public List<MemPhone> getMemPhones() {
  		return memPhones;
  	}
  	public void setMemPhones(List<MemPhone> memPhones) {
  		this.memPhones = memPhones;
  	}
  	
      ...
  }
  ```

  

  ```java
  // MemPhone.java
  
  public class MemPhone {
  	
  	private String memPhone1;
  	private String memPhone2;
  	private String memPhone3;
  	
  	public String getMemPhone1() {
  		return memPhone1;
  	}
  	public void setMemPhone1(String memPhone1) {
  		this.memPhone1 = memPhone1;
  	}
  	public String getMemPhone2() {
  		return memPhone2;
  	}
  	public void setMemPhone2(String memPhone2) {
  		this.memPhone2 = memPhone2;
  	}
  	public String getMemPhone3() {
  		return memPhone3;
  	}
  	public void setMemPhone3(String memPhone3) {
  		this.memPhone3 = memPhone3;
  	}
  }
  ```

  

- <span style="color:#FF0033">**19-3 Model & ModelAndView**</span>

  - 컨트롤러에서 뷰에 데이터를 전달하기 위해 사용되는 객체로 `Model`과 `ModelAndView` 객체가 있다.

  - `어떤게 좋고 나쁨은 없다.` 개발자 취향이다.

  - 두 객체의 **차이점**은,

    - `Model`은 뷰에 데이터만을 전달하기 위한 객체이고,
    - `ModelAndView`는 데이터와 뷰의 이름을 함께 전달하는 객체이다.

    

  <img src="https://drive.google.com/uc?id=1r65cqJ4bMgR4gYJyznTup29s6HBE2HQV">

  

  <img src="https://drive.google.com/uc?id=144SsiQ6DWZgJ6_Af4YjpTvmUcpVZGscp">

  

  <img src="https://drive.google.com/uc?id=1Ftxd9mCaL9Ox2fPyVZ2yIB3G6b0R8M7T">



------



### 20강 세션, 쿠키

> 클라이언트와 서버의 연결을 유지하는  방법에 대해서 학습한다.

- <span style="color:#FF0033">**20-1 세션(Session)과 쿠키(Cookie)**</span>
- <span style="color:#FF0033">**20-2 HttpServletRequest를 이용한 세션 사용**</span>
- <span style="color:#FF0033">**20-3 HttpSession을 이용한 세션 사용**</span>
- <span style="color:#FF0033">**20-4 세션 삭제**</span>
- <span style="color:#FF0033">**20-5 세션 주요 메소드 및 플로어**</span>
- <span style="color:#FF0033">**20-6 쿠키(Cookie)**</span>



------



### 21강 리다이렉트, 인터셉트

> 컨트롤러에서 뷰를 분기하는 방법과 컨트롤러 실행 전/후에 특정 작업을 가능하게 하는 방법에 대해서 학습한다.

- <span style="color:#FF0033">**21-1 리다이렉트 (redirect)**</span>
- <span style="color:#FF0033">**21-2 인터셉터 (interceptor)**</span>



------



### 22강 Database

> 오라클 데이터베이스를 설치하고 사용하는 방법에 대해서 학습한다.

- <span style="color:#FF0033">**22-1 오라클 다운로드**</span>
- <span style="color:#FF0033">**22-2 오라클 설치**</span>
- <span style="color:#FF0033">**22-3 계정 생성**</span>
- <span style="color:#FF0033">**22-4 SQL developer**</span>



------



### 23강 JDBC

> Java언어를 사용해서 Database와 통신하기 위한 방법에 대해서 학습한다.

- <span style="color:#FF0033">**23-1 기본 SQL**</span>
- <span style="color:#FF0033">**23-2 JDBC**</span>



------



### 24강 JdbcTemplate

> Java언어를 사용해서 Database와 통신하기 위한 방법에 대해서 학습한다.

- <span style="color:#FF0033">**24-1 JDBC의 단점을 보완한 JdbcTemplate**</span>
- <span style="color:#FF0033">**24-2 DataSource 클래스**</span>



------



### 25강 커넥션 풀

> 데이터베이스 연결을 미리 준비해 놓고 사용하는 방법에 대해서 학습한다.

- <span style="color:#FF0033">**25-1 c3p0 모듈의 ComboPooledDataSource**</span>
- <span style="color:#FF0033">**25-2 스프링 설정파일을 이용한 DataSource 설정**</span>



------

