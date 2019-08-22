---
layout: post
title:  "2019/08/22 JSP-Servlet 인프런 강의"
subtitle: "2019/08/22 JSP-Servlet 인프런 강의"
categories: til
tags: til
comments: true
---

- 인프런 [JSP-Servlet 강의](https://www.inflearn.com/course/실전-jsp_renew) 정리 입니다.

---

# JSP (Java Server Page) 프로그래밍 (190821)
**인프런 강의**

[실전 JSP](https://www.inflearn.com/course/실전-jsp_renew)

### 1강 웹 프로그램 개요

> 웹 프로그램의 개요와 동작에 대해서 학습한다.

- 1-1 웹 프로그래밍이란?
  - 웹 프로그램이란, 인터넷 서비스를 이용해서 서로 다른 구성요소들(PC등)이 통신할 수 있는 프로그램이다.
- 1-2 프로토콜(Protocol)과 IP
  - 프로토콜: 통신을 하기위한 규약으로 HTTP, FTP, SMTP, POP 등이 있다.

![webprogramming1](https://drive.google.com/uc?id=120epycf3bAp4iM-dnv_Ca5x4IJnOLBhc)

- 1-3 웹 프로그래밍의 동작 원리

![webprogramming2](https://drive.google.com/uc?id=14wXGLsBOEIX1wJpPViv829qbl3pVf-jg)

- NAT (Network Address Translation)

![NAT](https://drive.google.com/uc?id=1rK7seeLcU320P_CcYnLK9rBYOHqY132D)

**NAT의 두 가지 기능**

1. private IP addr로부터 router로 신호가 들어왔을 때 발신자의 정보를 기록해둔다.
2. 발신자의 내부 private IP addr을 외부로 보낼 때 public IP addr로 변경해서 보내준다.

> 사설 IP를 사용하는 사용자가 외부 IP를 사용할 수 있게 도와주는 기술이 NAT이다.

```
공유기 (router)
: WAN과 LAN을 이어주는 매개체 기능을 구현한다. (교환원)
WAN: Wide Area Network, LAN: Local Area Network

Gateway addr, Router addr: 공유기의 IP
```

**Port**

- 하나의 컴퓨터에 여러개의 서버를 설치할 수 있는데, 클라이언트가 서버에 접속할 때여러 서버를 구분해서 접속할 수 있는 구분자를 Port라고 한다.
- IP 주소가 컴퓨터에 접속하는 주소라면, Port는 컴퓨터 안에 설치된 서버에 접속하는 주소라고 할 수 있다.

**Port forwading**

- 공유기 외부에서 공유기 내부의 컴퓨터에 접속하기 위해서는 공유기 몇 번 포트에 접속한 정보를 공유기 내의 몇 번 포트로 연결해 줄 것인지를 공유기에게 알려주어야 한다. 이 때 사용되는 기술명이 Port forwading이다. 
- 공유기 외부에서 들어오는 특정  Port를 공유기 내부의 특정 사설 IP와 Port로 매칭시켜서 보내주는 일을 한다.

![port forwading](https://drive.google.com/uc?id=1NYkmSDWlZlBs8lN36q5YpUO97YyZG15w)

**DNS server**

```
채워넣어야 한다!!!
```



------



### 2강 개발 환경 설정

> 웹 프로그램 개발을 위한 기본 개발 환경 설정 방법에 대해 학습한다.

- 2-1 JDK 설치
- 2-2 Path 설정
- 2-3 이클립스 다운로드
- 2-4 웹 컨테이너 (Apache Tomcat 8.5) 설치



------



### 3강 JSP 맛보기

> JSP 파일을 간단하게 만들어 보고, 실제로 웹 컨테이너에서 어떤 작업이 이루어지는지 학습한다.

- 3-1 웹 컨테이너 구조

![webcontainer](https://drive.google.com/uc?id=1aDuEbxIxc0YRwzaKXRUBonyq3tsSE0Pz)

> 개발자는 jsp 파일 만드는 일 까지만 진행하고, 웹 컨테이너(WAS에 내장되어있다.)에서 .java 파일 -> .class 파일 (컴파일) -> .obj파일 (링크) 까지 만들어준다.

- 3-2 JSP 파일 작성
- 3-3 .java 파일 확인

![javafile](https://drive.google.com/uc?id=1ytKlSJG2XA7lkx2Sd6zMxy5L_5i69k9g)

- jsp 파일은 기존 html 파일에 jsp 코드를 가미해서 (이를 통해서 사용자의 요청에 대해 반응하는 동적인 활동이 가능해진다) 만들게 되고, 이를 웹 컨테이너가 컴파일 및 링킹 과정을 통해 사용자의 요청에 응답할 수 있는 html 파일로 response해주게 된다.



------



### 4강 Servelet 맛보기

> java 파일을 간단하게 만들어 보고, 실제로 웹 컨테이너에서 어떤 작업이 이루어지는지 학습한다.

​       **jsp는 html 코드안에 jsp코드를 넣는 반면에, Servlet은 순수 java 파일로 구성된다.**

- 4-1 웹 컨테이너 구조

![Servlet web container](https://drive.google.com/uc?id=1rGIgeMsCah3E4ben5eseELfFOo7PH7H2)

> 개발자는 java 파일만 만들고, 웹 컨테이너가 컴파일 및 링킹 과정을 진행한다.

- 4-2 Servlet 파일 작성
- 4-3 .class 파일 확인

![classfile](https://drive.google.com/uc?id=1RCq1sYdui3OC2blpOLXT5hLieuI8Gmoi)



------

### jsp? Servlet?

```
jsp는 html 기반에 jsp 코드를 넣어서 만든 서버사이드(server side) 파일이고, 이 파일을 웹 컨테이너가 java파일로 만들고, 컴파일 및 링킹 과정을 통해 웹 프로그램으로 사용자에게 서비스 된다.

Servlet은 순수 java 코드로 구성되고, 이러한 서버사이드(server side) 파일을 웹컨테이너가 컴파일 및 링킹 과정을 진행하고, 웹 프로그램으로 사용자에게 서비스 된다.

결국 두 과정의 목적은 사용자에게 java라는 언어를 통해 동적인 환경을 제공하고자 한다는 것이다.
```



> 주로 jsp와 Servlet은 동시에 사용해서 웹 프로그램을 구현하는데, 
>
> jsp는 주로 view function을 위해서 스크립트를 구현하고,
>
> Servlet은 실질적인 동작(Controller, Model)을 위해서 구현되곤 한다.



------



### 5강 Servlet 맵핑

> Servlet을 외부에서 요청하기 쉽도록 특정 문자를 이용해서 맵핑하는 방법에 대해서 학습한다.

- 5-1 Servlet 맵핑이란?

![SM1](https://drive.google.com/uc?id=1Hn01VkYTLH2ikLN3sa_uDALLNbA4vfAh)

**Servlet mapping ?** `각 서블릿마다 구분할 수 있는 간결한 별칭을 지어주는 과정`

1. web.xml을 이용하는 방법
2. Java annotation을 이용하는 방법



- 5-2 web.xml 파일을 이용한 맵핑 (상대적으로 고전적인 방법)

![SM2](https://drive.google.com/uc?id=1aqwW6F09gza5I00XHjjJUg71dXmaQ4V1)

- 5-3 Java Annotation을 이용한 맵핑 (상대적으로 최신방법)

![SM3](https://drive.google.com/uc?id=1KTWWs4-aiPTH5CRP-Ij8QYrBIPcqr4e4)



------



### 6강 Servlet request, response

> 사용자의 요청(Request)과 web-server의 응답(response)을 담당하는 객체에 대해서 학습한다.

- 6-1 HttpServlet

![httpServlet](https://drive.google.com/uc?id=1F1lwne9xYKANJ79glJmokzHTm1VQPxYZ)

`HttpServlet만 상속받아서 필요한 기능만 구현해준다.`

- 6-2 HttpServletRequest
  - Client에 의한 요청 객체
- 6-3 HttpServletResponse
  - Server에 의한 응답객체



------



### 7강 Servlet Life Cycle

> 사용자의 요청에 의해서 생성된 servlet의 생명주기 (생성, 실행, 종료)

- 7-1 Servlet의 생명주기

![ServletLC](https://drive.google.com/uc?id=1UIEWe_6rah8KE858a37CP45mgueDetmT)

- 7-2 Servlet의 생명주기 관련 메소드

![ServletLC_method](https://drive.google.com/uc?id=1KUNVMT4oltnOMXZR_9rWqdvUNRvucv4j)

> 각 단계 별 콜백 메소드를 제공 및 호출(웹 컨테이너가 호출함)됨으로써 Servlet의 Life-Cycle을 구현한다.



------



### 8강 form 데이터 처리

> 사용자의 form 데이터를 Servlet에서 처리하는 방법에 대해서 학습한다.

- 8-1 form 태그

![form](https://drive.google.com/uc?id=1dxs2qWKkJnejA01ODnWe8bRCaBjRnvp9)

- 8-2 doGet

![formGet](https://drive.google.com/uc?id=1l4JPSIIQBWFH9Tnv6ONWkUny856kSYvA)

> 데이터가 웹 브라우저 URL에 노출되어 웹 서버로 전송된다. 

- 8-3 doPost

![formPost](https://drive.google.com/uc?id=1j1l4CRGgUy89QkOFA_hcNfLEFl97pmKC)

> 데이터가 HTTP Request에 암호화 되어 웹서버로 전송되기 때문에 상대적으로 보안에 강하다



------



### 9강 JSP 스크립트

> html 파일에 java 관련 코드를 삽입하여 jsp 파일을 만드는 방법에 대해서 학습한다.

- 9-1 Servelet vs. JSP

![servlet_jsp](https://drive.google.com/uc?id=1urospyR_amaSSe8T-s00qdpixRXOTmdt)

- 9-2 JSP 파일 HTML5 포멧 설정
- 9-3 JSP 주요 스크립트

![servlet_jsp_script1](https://drive.google.com/uc?id=1KxL4bN3Qj_cBG7mbwmg9Ce-h7bCVB4El)

![servlet_jsp_script2](https://drive.google.com/uc?id=1QxVtnVOcEAMOyMEpmoDIzFd8WhpU-BbV)

![servlet_jsp_script3](https://drive.google.com/uc?id=1Tku8BIon-kBWi0iG3uh3beZjAlfviDKJ)



------



### 10강 JSP request, response

> 사용자의 요청(Request)과 web-server의 응답(response)을 담당하는 객체에 대해서 학습한다.

- 10-1 request 객체

![request](https://drive.google.com/uc?id=1QcpcVdPKL-8qfEBlOY7pYiIqKLgZyW_d)

- 10-2 response 객체

![response](https://drive.google.com/uc?id=1QF1ARM71UmpzmjIpq9A0duMmM5XdLyer)



------



### 11강 JSP 내장객체

> request, responsedhl JSP 에서 기본적으로 제공하는 객체에 대해서 학습한다.

- 11-1 config 객체
- 11-2 application 객체
- 11-3 out 객체
- 11-4 exception 객체



------



### 12강 Servlet 데이터 공유

> Servlet에서 데이터를 공유하는 방법에 대해서 학습한다.

- 12-1 servlet parameter
- 12-2 context parameter
- 12-3 context attribute



------



### 13강 Cookie

> 클라이언트와 서버의 연결을 유지시키는 방법 중 하나인 Cookie에 대해서 학습한다.

- 13-1 Cookie 란?

> http 프로토콜은 Stateless라는 특징이 있다. 한 번 요청에 대한 응답을 한다면 연결을 해제한다.(관계해제) 수 많은 클라이언트에 대한 요청을 과부하되지 않고 처리하기 위해서 이와 같은 특징을 유지한다.

> 온라인 쇼핑몰 같은 곳에서 장바구니를 사용할 때 데이터 연결을 유지할 필요가 있는데, 이를 위해서 cookie라는 방법을 사용한다. 클라이언트 쪽에 기존 연결 정보를 저장한다.

> 쿠키는 클라이언트가 만들고, 클라이언트쪽에 정보를 저장한다.

![cookie](https://drive.google.com/uc?id=1OTu5ulYwEf2pluDHmCuoSXHQgglPT00P)

- 13-2 Cookie 구현

> 쿠키는 하나의 정보만 있는 것이 아니기 때문에 배열로 관리한다.

> 쿠키는 정말 많이 사용되지만, 사용자 정보가 본인의 pc에 저장된다는 관점에서 데이터 유출 보안에 취약할 수 있다. (그래서 간단한 데이터만 저장한다. )

> 서버사이드에 유저정보를 저장해서 유저의 정보를 유지시키는 (보안 강화) session이라는 기술이 있다.

![cookie2](https://drive.google.com/uc?id=1s8OYh4hf2bAGEEDrrqLVy0M63ACTj3zu)



------



### 14 강 Session

> 클라이언트와 서버의 연결을 유지시키는 방법 중 하나인 session에 대해서 학습한다.

- 14-1 Session이란?

> 클라이언트와 서버의 연결을 유지시키기 위한 벙법으로 유저에 대한 정보를 서버사이드에 저장한다.

> Session은 Web container가 만들게 되고, 서버쪽에 정보가 저장된다.

> http 프로토콜을 사용한다면 cookie를 사용하든 session을 사용하든 서버와의 연결은 한 번의 request와 response 이후 끊기게 된다.

![session1](https://drive.google.com/uc?id=1D6LUfMwpPXdjUX-rkxIxyRhZxnSIB5ri)

- 14-2 Session 구현

![session2](https://drive.google.com/uc?id=1uqzCNKn8U6szrLJdT9Fid_dGKDAV5ER_)



------



### 15강 한글처리

> 한글이 정상적으로 출력될 수 있는 방법에 대해서 학습한다.

- 15-1 한글처리

![han1](https://drive.google.com/uc?id=1lb1hvDkY7XC9vdyE-CgxDtoMunpe9z_l)

- 15-2 Filter

![han2](https://drive.google.com/uc?id=1kzFzwri5sJogrjJXmy46sUx1L4UyzMQM)



------



### 16강 오라클 설치

> 오라클 데이터 베이스 설치하는 방법에 대해서 학습한다.

[오라클 설치 참조](https://wikidocs.net/3900) , [Oracle developer 설치 참조](https://all-record.tistory.com/76)

- 16-1 오라클 다운로드
- 16-2 오라클 설치
- 16-3 계정 생성
- 16-4 SQL developer

![ocrl](https://drive.google.com/uc?id=15Ic6JAjQ3s4QIYCWXnHZe0UM0g8RHs0u)

> 처음 데이터 베이스 접속 선택 시, SID 관련 오류가 발생하였는데, SID를 xe가 아닌orcl로 설정하니 해결되었다. 자세한 설치 및 초기 s/u과정은 위의 링크 참조



------



### 17강 SQL

> 데이터 베이스의 데이터를 다루기 위한 SQL 문에 대해 학습한다.

- 17-1 테이블 생성 및  삭제

![sql_1](https://drive.google.com/uc?id=1e2ptzIs_V4jwk2pM0FVVdUtmKUShPS22)

- 17-2 데이터 추가, 수정, 삭제

![sql_2](https://drive.google.com/uc?id=1DhkAKXs8gu5l-F34SNmxOMxYm0ePPCAM)

- 17-3 데이터 검색

![sql_3](https://drive.google.com/uc?id=1PtS-0IbYtWYWoqI5FBP9etLfdw4tpzDH)



------



### 18강 JDBC

> Java와 오라클이 통신할 수 있는 방법에 대해서 학습한다.

- 18-1 JDBC 설정

![jdbc1](https://drive.google.com/uc?id=1oAFJJkWXTnOlycLJndaTZOd1MHSKqw_S)

![jdbc2](https://drive.google.com/uc?id=19PZFvojwV0hotya3hgjYLt5geCEyKn2b)

> 현재 내가 사용하는 jre version이 9.0.4라서 따로 lib\ext 폴더가 없었다. 그래서 그냥 이클립스 내에서 project의 properties에서 직접 Add External Jars를 선택하여 jar 파일(ojdbc6.jar)을 연동시켰는데,    'java.lang.ClassNotFoundException: oracle.jdbc.driver.OracleDriver' 이와 같은 에러가 발생하였다.
>
> 결국 하기의 해당 사이트를 참조하여 문제를 해결하였는데, Java Build Path Entries를 설정하지 않았던게 원인이였다.

[해당 사이트 참조](https://febdy.tistory.com/39)

- 18-2 JDBC를 이용한 데이터 관리

![jdbc3](https://drive.google.com/uc?id=17C654xOeQ4hl3-2jWMw6I3XBnahXE9gw)

- 18-3 PreparedStatement

> sql문을 간결하게 쓸 수 있게끔 도와주는 객체이다. (human error를 줄인다.)

![jdbc4](https://drive.google.com/uc?id=1kIIM3ClmqZcZA-Pn46BhirdGHvOLc0Dy)



------



### 19강 DAO와 DTO

> 데이터 베이스와 통신하기 위한 기능을 모듈화하는 방법에 대해서 학습한다.

- 19-1 DAO, DTO란?

> DAO: 18강에서는 servlet에서 데이터 베이스에 접근하고 데이터를 받아오는 역할을 다 수행했지만, DAO라는 객체를 통해서 데이터 베이스에 접근하고, 데이터를 받아오는 역할을 따로 객체화 해서 분리한 것
>
> DTO: 데이터 베이스에 저장된 데이터의 타입과 servlet에서 사용되는 java형식의 데이터 타입이 다르기 때문에 이를 java형식으로 바꿔주는 객체를 만든 것

![DAO_DTO](https://drive.google.com/uc?id=1dvQkUEEv2YVjp36vfrWgB20aCQcVuZXL)

- 19-2 DAO, DTO 구현

> 18강에서는 하나의 servlet파일(bookServlet)에서 데이터 베이스에 접근 및 데이터를 표현하는 역할을 도맡아 했지만, 이를 DAO와 DTO를 따로 떼어내어서 데이터 베이스를 담당하는 객체를 만들어준다.

![DAO_DTO2](https://drive.google.com/uc?id=1Lnte2s3M0tbPn-iijQZt_u3ju4QOBZza)



------



### 20강 Connection Pool

> 데이터 베이스와 통신하는 자원을 효율적으로 관리하기 위한 방법을 학습한다.

- 20-1 커넥션 풀 이란?

> 기존에 웹서버와 DB가 데이터를 주고 받을 땐, DB con/handling/close와 같은 과정을 겪었는데, 접속하는 사용자가 많아질 수록 DB를 열고 닫는 과정에서 서버에 많은 부하가 걸릴 수 있다.

> 이러한 서버의 부하를 낮추기 위해서 미리 Connection을 웹서버(ex. 톰캣)에 만들어 두었다가 웹 서버가 필요로할 때마다 이를 사용하는 방식으로 서버의 부하를 낮추는 방법을 connection pool 이라고 한다.

![connectionpool1](https://drive.google.com/uc?id=1vjf8SESqEkS8NfXHWWlwxepjHp3NOgyS)

- 20-2 커넥션 풀 설정

> 톰캣 컨테이너에 미리 DB에 대한 정보를 알려줌으로써 Connection Pool을 미리 생성하게 된다.

![connectionpool2](https://drive.google.com/uc?id=19qckZmRHRzbsLKWAjriXdhL0pJ5wfToO)

- 20-3 커넥션 풀 구현

> 커넥션 풀을 사용한다면, 먼저 DB로 연결/종료에 대한 서버의 부하를 줄일 수 있고, 19강에서 진행되었던 DB를 연결하여 connection객체를 갖고오는 과정에 비해 코드가 심플해짐을 확인할 수 있다.

![connectionpool3](https://drive.google.com/uc?id=16MHwYDh3QB3Pip6rOYHGe0UFhWYKKgEC)