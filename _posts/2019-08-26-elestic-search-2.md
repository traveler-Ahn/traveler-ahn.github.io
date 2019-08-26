---
layout: post
title:  "2019/08/26 ELK(ElasticSearch,Logstash,Kibana) 스택으로 데이터 분석하기 (2)"
subtitle: "2019/08/26 ELK(ElasticSearch,Logstash,Kibana) 스택으로 데이터 분석하기 (2)"
categories: til
tags: til
comments: true

---

- 인프런 [Elastic Search 강의](https://www.inflearn.com/course/elk-스택-데이터-분석) 정리 (2)
  - 키바나 (Kibana) & 로그 스태쉬 (Logstash)
  - 실전 데이터 다루기

------

# Elastic Search 강의 (2) (190826)

#### 1강부터 10강까지 진행된 내용

**ElasticSearch에 대한**

1. 설치
2. 기본 개념 정리 
3. 데이터 다루는 방법 (RestAPI PUT, GET, DELETE POST)
4. 벌크 데이터 파일로부터 불러오기
5. 맵핑 (RDB에서 Schema)
6. 데이터 조회
7. 데이터 집계 (단순 document & group by)



---



### 11강 키바나 설치 및 실행

> 데이터 시각화 툴

- Install KIBANA (7.3.1 ver)
  
- 다운로드 https://www.elastic.co/kr/downloads/kibana deb 파일 및 설치
  
- Config KIBANA (/etc/kibana/kibana.yml)

  ```
  $ sudo nano /etc/kibana/kibana.yml
  
  server.host: "localhost"
  elasticsearch.hosts: ["http://localhost:9200"]
  
  1. elasticsearch.hosts: YOUR_ELASTICSEARCH_URL (http://localhost:9200)
  2. server.host: the address to which the kibana server will bind (localhost)
  ```

- START KIBANA

  ```
  $ sudo /usr/share/kibana/bin/kibana --allow-root
  
  localhost:5601
  ```



---



### 12강 키바나 매니지먼트

- Elastic Search 데이터 (Document) 넣기

  ```
  # 기존 데이터 삭제
  $ curl -XDELETE localhost:9200/basketball
  
  # 인덱스 생성
  $ curl -XPUT localhost:9200/basketball
  
  # 맵핑 (ch05 폴더)
  $ curl -XPUT 'http://localhost:9200/basketball/record/_mapping?include_type_name=true&pretty' -d @basketball_mapping.json -H 'Content-Type:application/json'
  
  # 데이터 삽입
  $ curl -XPOST 'http://localhost:9200/_bulk?pretty' --data-binary @bulk_basketball.json -H 'Content-Type:application/x-ndjson'
  
  # 데이터 확인
  $ curl -XGET localhost:9200/basketball/record/1/?pretty
  ```

- KIBANA 브라우저 실행 및 ElasticSearch Index Pattern 연결

1. <img src="https://drive.google.com/uc?id=1thoCclSQyh8rHrLvsBaWwzGcvrcmGtQy">

   > 우 하단에 있는 Index Patterns 클릭

2. <img src="https://drive.google.com/uc?id=1oI9daZTKDVMNSCf3bHCL5RpXBjlyo0Qf">

   > Create index pattern 클릭

3. <img src="https://drive.google.com/uc?id=1dllCV8iEa3usSE10R_6CGTbsOZMDErkT">

   > Index pattern에 기존에 기입해둔 Elastic Search의 index값을 기입한다. & Next step

4. <img src="https://drive.google.com/uc?id=1yj_KeaLNevW7BpgFGBLNcqd0IYKOAiBn">

   > Time Filter에 submit_date 찾아서 체크 & Create index pattern

5. <img src="https://drive.google.com/uc?id=1lWZx1m2r7-zpH-VmcHFx80KiPmBpyNbX">

   > Elastic Search에 입력해둔 데이터 확인



---



### 13강 키바나 디스커버 (discover)

> 디스커버라는 탭에서 간단하게 필터링 기능을 통해 데이터를 시각화 할 수 있다. (Graph and Table data) 

<img src="https://drive.google.com/uc?id=15AUm05uhX1H4rrxuQcmIScw80eeIF1Zw">

<img src="https://drive.google.com/uc?id=1est7RRYWb-suJQZI-mQ61Ci3_knnoAlF">



---



### 14강 키바나 비주얼라이즈 (Visualize) - 막대그래프, 파이차트

> 왼쪽의 Visualize tab에서 vertical graph 선택 후, Y-axis / X-axis 선택하여 그래프를 plot한다.

- 선수 별 평균 득점 Vertical graph plot (Y-axis의 Aggregation필드 값을 바꾸어 다양한 통계값을 그린다.)

<img src="https://drive.google.com/uc?id=1qbNUBe9AvJYj3S_oNdQSgPPK8tk0u3aN">

<img src="https://drive.google.com/uc?id=15nrsokzWs1ToTn_XsKqdk3IBU4y73TRB" height="500">

>  왼쪽의 Visualize tab에서 pi graph 선택 후, 각 축을 선택하여 그래프를 plot한다.

<img src="https://drive.google.com/uc?id=1niBL4U4xRPqxsElTGlJutNYDXVdkbWEA">

<img src="https://drive.google.com/uc?id=1Euntfc2JtcC05SgJe3RptfDoiL3Uo_Pm" height="550">



---



### 15강 키바나 비주얼라이즈 (Visualize) - 타일맵, 지도에 표시

> 키바나를 활용하여 ElasticSearch에 있는 document를 지도에 표시

- Document 생성

  ```
  # @ch2 폴더
  # 인덱스 생성
  $ curl -XGET localhost:9200/basketball/record/2/?pretty
  
  # 맵핑
  $ curl -XPUT 'http://localhost:9200/classes/class/_mapping?include_type_name=true&pretty' -d @classesRating_mapping.json -H 'Content-Type:application/json'
  
  # 데이터 삽입
  $ curl -XPOST 'http://localhost:9200/_bulk?pretty' --data-binary @classes.json -H 'Content-Type:application/x-ndjson'
  
  # 데이터 확인
  $ curl -XGET localhost:9200/classes/class/1/?pretty
  ```

- 12강 내용 참조하여 ElasticSearch에 삽입한 classes를 index pattern 연결

- Visualize에서 coordinate map(tile map)을 선택
  - Buckets에서 Geo coordinates를 선택
  - Aggregation Geohash 선택

- **결과화면**

  <img src="https://drive.google.com/uc?id=18bmBgx4XbefeQpWPtIFQZpYV0xgHKlyL">

  <img src="https://drive.google.com/uc?id=1dYkCy3oumzVwGuXFriNdyZyZuHK_eR9Y">



---



### 16강 키바나 대시보드 (Dashboard)

- Classes index가 선택된 상황에서 vertical chart를 average-rating vs. prof.를 그려서 save한다.

  - Visualize chart에서 save된 차트는 dashboard에서 재활용될 수 있다.

  <img src="https://drive.google.com/uc?id=1tQijcK87ROXU_wTHwETtDkQ_8HS6jFZZ">

- DashBoard에서  save한 graph를 불러온다.

  <img src="https://drive.google.com/uc?id=1tJWF9hOvyJ-tt_yIL5VxG8u8l9UkLtSz">

> Dash Board에선 그래프가 한 화면에서 어떻게 보일지를 설정할 수 있다.
>
> 예를들어, 데이터는 계속바뀌는 중에 한 화면에서 모든 데이터의 변화를 살펴보기 위해선 Kibana의 dashboard 기능을 이용하면 된다.



---



### 17강 로그스태시 인스톨 셋업 (logstash install)

> elk 스택에서 logstash는 input에 해당하고, 여기서 받은 입력은 변환되어 ElasticSearch로 들어간다.

- **Inputs**

  - Data is often scattered across many systems in many format. Logstash supports a variety of inputs that pull in events from a Multitude of common sources

- **Filter**

  - Logstash filters parse each event, identify named fields to build structure, and transform, Converge on a common format for easier Analysis and business value

- **Outputs**

  - Logstash has a variety of outputs that let you route data where you want, ehre tutorial, We focus on elasticsearch

  <img src="https://drive.google.com/uc?id=140GCGIogQhWsN4v6GHwd4qlBFqa4h-q5">

  <img src="https://drive.google.com/uc?id=1RE2lt6rJjrhB6fB3Atbn7emNaT38PF_G">

- **Install Logstash** (ver 7.3.1)

  - Logstash 설치 전에 Java 설치되어있어야 한다.

    ```
    $ java -version
    ```

  - .deb 파일 [다운로드](https://www.elastic.co/kr/downloads/logstash) 및 설치

  

- **Configuration Logstash**
  
  - logstash-simple.conf 파일 참조 (ch06)



- **Execution**

  ```
  $ sudo /usr/share/logstash/bin/logstash -f ~/study/elk-stack/BigData/ch06/logstash-simple.conf
  ```

  

---



#### 실전 데이터 셋 분석 첫 번째 시간 (인구 데이터 변화)

- 데이터 셋 다운로드 https://catalog.data.gov/dataset/population-by-country-1980-2010

(github에서 다운로드 받은 파일들 중에 정제된 csv 파일이 있다.)



- Check if elasticsearch, kibana working

```
$ ps -ef | grep kibana
$ ps -ef | grep elasticsearch
```



- Logstash file transfer into ElasticSearch

```
# conf 파일내에 경로 절대경로로 수정필요

$ sudo /usr/share/logstash/bin/logstash -f ~/study/elk-stack/BigData/ch06/logstash.conf
```



- Kibana Visualization
  - Management & Index Pattern에서 Log Stash를 통해 입력한 데이터를 찾아서 등록



---



#### 실전 데이터 셋 분석 두 번째 시간 (주식 데이터 변화)

- 데이터 수집
  - [FaceBookData 5Y](https://finance.yahoo.com/quote/FB/history?period1=1408978800&period2=1566745200&interval=1d&filter=history&frequency=1d) csv 파일 다운로드



- Check if elasticsearch, kibana working

```
$ ps -ef | grep kibana
$ ps -ef | grep elasticsearch
```



- Logstash file transfer into ElasticSearch

```
# conf 파일내에 경로 절대경로로 수정필요

$ sudo /usr/share/logstash/bin/logstash -f ~/study/elk-stack/BigData/ch06/logstash_stock.conf
```



- Kibana Visualization
  - Management & Index Pattern에서 Log Stash를 통해 입력한 데이터를 찾아서 등록

![stock-analysis](https://drive.google.com/uc?id=1JwwHKQsdwP9O15Euwpr0DfGi37KBlLME)