---
layout: post
title:  "2019/08/26 ELK(ElasticSearch,Logstash,Kibana) 스택으로 데이터 분석하기 (1)"
subtitle: "2019/08/26 ELK(ElasticSearch,Logstash,Kibana) 스택으로 데이터 분석하기 (1)"
categories: til
tags: til
comments: true

---

- 인프런 [Elastic Search 강의](https://www.inflearn.com/course/elk-스택-데이터-분석) 정리 (1)
  - 엘라스틱 서치 (Elastic Search)

------

# Elastic Search 강의 (1) (190826)

### 1강 데이터 과학 소개

> ELK 스택
>
> - Ubuntu 18.04 LTS
> - Elastic Search (7.3.1ver) (데이터 Search)
> - Logstash (데이터 수집)
> - Kibana (Data Visualization)

![elk-stack](https://drive.google.com/uc?id=1NOc6m4v--4u_cKt6kZ2t8VrkcWBFfigf)

---



### 2강 우분투에 엘라스틱 서치 설치하기

- Supports most OS including yours! https://www.elastic.co/kr/support/matrix

- Install on Ubuntu 18.04 

  - Install JDK

    - 설치 도움 사이트 
    - [Ubuntu 18.04 LTS 자바 설치 및 톰캣 설치](https://bokyundev.tistory.com/14)  (이걸로 jdk 8버전 설치했다. openjdk)
    - [우분투 18.04 자바 8 설치하기](https://developerhive.tistory.com/16) (oracle jdk)

  - Download and Install ElasticSearch

    - [ElasticSearch Down](https://www.elastic.co/kr/downloads/elasticsearch) 버전 7.3.1 .deb 파일 다운로드 및 설치

    ```
    Install at     : /usr/share/elasticsearch
    Config file at : /etc/elasticsearch
    Init script at : /etc/init.d/elasticsearch
    ```

    - Automatic start and stop when server starts and stop

    ```
    $ sudo systemctl enable elasticsearch.service
    ```

  - Start & Stop & Check

    ```
    $ sudo service elasticsearch start  # start
    $ sudo service elasticsearch stop   # stop
    $ sudo curl -XGET 'localhost:9200'  # check if elasticsearch run
    
    # 실행결과
    {
      "name" : "playground",
      "cluster_name" : "elasticsearch",
      "cluster_uuid" : "----",
      "version" : {
        "number" : "7.3.1",
        "build_flavor" : "default",
        "build_type" : "deb",
        "build_hash" : "4749ba6",
        "build_date" : "2019-08-19T20:19:25.651794Z",
        "build_snapshot" : false,
        "lucene_version" : "8.1.0",
        "minimum_wire_compatibility_version" : "6.8.0",
        "minimum_index_compatibility_version" : "6.0.0-beta1"
      },
      "tagline" : "You Know, for Search"
    }
    ```



---



### 3강 ElesticSearch 기본 개념 정리

- DataFlow

![data-flow](https://drive.google.com/uc?id=1UFR9NezY3Gb4llMr2UbsNb6Wurbe1_gx)

- ElasticSearch vs. Relation DB

![es-vs-rdb](https://drive.google.com/uc?id=14fZ-GsegCb0WWr3RoNbqiB4f0aYjeiXq)

> ES사용시에 Indexing 방법이 다르기 때문에 검색시에 속도가 매우 빠른 장점이 있다.

<img src="https://drive.google.com/uc?id=1iensKFH1fQHPQDgy3lX1xRvuc-o1k_Gm" width="500">

```
# ElasticSearch Rest API를 사용한다.

Elastic Search  Relational DB
   GET 				Select
   PUT				Update
   Post				Insert
  DELETE			Delete
```

- Elastic Search사용시 , Rest API 사용

![RestAPI](https://drive.google.com/uc?id=1jgV7Le_M4M3xJj7tCCrGsku2PzWTT_If)



---



### 4강 엘라스틱 서치 데이터 입력, 조회, 삭제 (GET, POST, PUT, DELETE)

```
# ES는 RestAPI를 사용한다.

Elastic Search  Relational DB
   GET 				Select
   PUT				Update
   Post				Insert
  DELETE			Delete
```



- GET(조회), PUT(인덱스 생성), DELETE(삭제), POST(Document 생성)

```
# GET
$ curl -XGET http://localhost:9200/classes
$ curl -XGET http://localhost:9200/classes?pretty  # JSON 포멧으로 깔끔하게 CLI에 출력됨

# PUT # 새로운 인덱스(클래스) 생성
$ curl -XPUT http://localhost:9200/classes  

# DELETE
$ curl -XDELETE http://localhost:9200/classes

# POST # 새로운 Document 생성
	Document생성 시 인덱스명이 있는 상태에서 만들어도 되고, 아니면 POST사용시에 인덱스명과 타입명을 동시에 	명시하면 새로운 인덱스와 Document가 생성된다. url 표기법, IPAddr:port/인덱스/타입/아이디
$ curl -XPOST http://localhost:9200/classes/class/1/ -d '{"title": "Algorithm", "professor": "John"}' -H 'Content-Type:application/json'
$ curl -XGET http://localhost:9200/classes/class/1/?pretty 

# GET방식으로 POST된 결과 확인
{
  "_index" : "classes",
  "_type" : "class",
  "_id" : "1",
  "_version" : 1,
  "_seq_no" : 0,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "title" : "Algorithm",
    "professor" : "John"
  }
}
```



- CREATE INDEX, TYPE, DOCUMENT FROM **FILE**

```json
# JSON 파일 구성 oneclass.json

{
    "title" : "ML",
    "Prof." : "John Ahn",
    "major" : "Computer Science",
    "semester" : ["spring", "fall"],
    "student_count" : 100,
    "unit" : 3,
    "rating" : 5
}
```



```
$ curl -XPOST http://localhost:9200/classes/class/1/ -d @oneclass.json -H 'Content-Type:application/json'

$ curl -XGET http://localhost:9200/classes/class/1/?pretty # 조회

{
  "_index" : "classes",
  "_type" : "class",
  "_id" : "1",
  "_version" : 2,
  "_seq_no" : 1,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "title" : "ML",
    "Prof." : "John Ahn",
    "major" : "Computer Science",
    "semester" : [
      "spring",
      "fall"
    ],
    "student_count" : 100,
    "unit" : 3,
    "rating" : 5
  }
}
```



---



### 5강 엘라스틱 서치 업데이트 (Update)

- curl을 이용해서 Document 생성

```
$ curl -XPOST http://localhost:9200/classes/class/1/ -d '{"title": "Algorithm", "professor": "John"}' -H 'Content-Type:application/json'
```

- **file structure**

  <img src="https://drive.google.com/uc?id=12bZLJepkbWqL8m9kBmXNLbi901iY-T9K">

- 생성된 데이터 확인

```
$ curl -XGET http://localhost:9200/classes/class/1/?pretty

{
  "_index" : "classes",
  "_type" : "class",
  "_id" : "1",
  "_version" : 1,
  "_seq_no" : 0,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "title" : "Algorithm",
    "professor" : "John"
  }
}
```



- 데이터 업데이트 (Update)

```
$ curl -XPOST http://localhost:9200/classes/class/1/_update?pretty -d '{"doc": {"unit":1}}' -H 'Content-Type:application/json'

$ curl -XGET http://localhost:9200/classes/class/1/?pretty # 업데이트 된 데이터 확인

{
  "_index" : "classes",
  "_type" : "class",
  "_id" : "1",
  "_version" : 2,
  "_seq_no" : 1,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "title" : "Algorithm",
    "professor" : "John",
    "unit" : 1
  }
}
```



- 기존 데이터 unit : 1 -> unit : 2 업데이트

```
$ curl -XPOST http://localhost:9200/classes/class/1/_update?pretty -d '{"doc": {"unit":2}}' -H 'Content-Type:application/json'

$ curl -XGET http://localhost:9200/classes/class/1/?pretty # 업데이트 된 데이터 확인

{
  "_index" : "classes",
  "_type" : "class",
  "_id" : "1",
  "_version" : 2,
  "_seq_no" : 1,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "title" : "Algorithm",
    "professor" : "John",
    "unit" : 2
  }
}
```



- Updata One filed with Script

```
$ curl -XPOST http://localhost:9200/classes/class/1/_update -d '{"script" : "ctx._source.unit += 5"}' -H 'Content-type:application/json'

$ curl -XGET http://localhost:9200/classes/class/1/?pretty # 업데이트 된 데이터 확인

{
  "_index" : "classes",
  "_type" : "class",
  "_id" : "1",
  "_version" : 2,
  "_seq_no" : 1,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "title" : "Algorithm",
    "professor" : "John",
    "unit" : 7
  }
}
```



---



### 6강 BULK POST 

> 여러 개의 Document를 한 번에  Elastic Search로 삽입하는 방법
>
> (study folder에 elk / ch2에 있는 json 파일 사용)

```
$ curl -XPOST http://localhost:9200/_bulk?pretty --data-binary @classes.json -H 'Content-type:application/x-ndjson'

$ curl -XGET localhost:9200/classes/class/2?pretty   # id를 바꿔가면서 bulk로 삽입된 결과확인
```



---



### 7강 MAPPING (관계형 데이터 베이스의 Schema)

> WE CAN ADD DOCUMENT WITHOUT MAPPING?

Yes, but be careful, date field may stored as sting and you cannot visualize it on Kibana. Value may stored as string while you expect it is number. Elasticsearch do its best, but not smart enough as much as you think

> 데이터를 관리할 땐 꼭 MAPPING 사용!!!

- Example,

<img src="https://drive.google.com/uc?id=1DrLnhbzJRnxTM_Z3CKEsvEQwPWlPDhbQ" height="500">

- 학습을 위한 클래스 생성 및 확인

```
# 클래스 생성
$ curl -XPUT http://localhost:9200/classes

# 결과확인
curl -XGET http://localhost:9200/classes?pretty
{
  "classes" : {
    "aliases" : { },
    "mappings" : { },
    "settings" : {
      "index" : {
        "creation_date" : "1566785883842",
        "number_of_shards" : "1",
        "number_of_replicas" : "1",
        "uuid" : "BnL_5lQ8Qsaz_0TdhrGxSg",
        "version" : {
          "created" : "7030199"
        },
        "provided_name" : "classes"
      }
    }
  }
}

-> mapping이 비어이는 상황이다.
```

- mapping 만들기

```
# 매핑 만들기
$ curl -XPUT 'http://localhost:9200/classes/class/_mapping?include_type_name=true&pretty' -d @classesRating_mapping.json -H 'Content-Type:application/json'

# 결과 확인
$ curl -XGET http://localhost:9200/classes/?pretty

{
  "classes" : {
    "aliases" : { },
    "mappings" : {
      "properties" : {
        "major" : {
          "type" : "text"
        },
        "professor" : {
          "type" : "text"
        },
        "rating" : {
          "type" : "integer"
        },
        "school_location" : {
          "type" : "geo_point"
        },
        "semester" : {
          "type" : "text"
        },
        "student_count" : {
          "type" : "integer"
        },
        "submit_date" : {
          "type" : "date",
          "format" : "yyyy-MM-dd"
        },
        "title" : {
          "type" : "text"
        },
        "unit" : {
          "type" : "integer"
        }
      }
    },
    "settings" : {
      "index" : {
        "creation_date" : "1566785883842",
        "number_of_shards" : "1",
        "number_of_replicas" : "1",
        "uuid" : "BnL_5lQ8Qsaz_0TdhrGxSg",
        "version" : {
          "created" : "7030199"
        },
        "provided_name" : "classes"
      }
    }
  }
}
```

매핑에 기존 json파일로 명시해둔 내용이 들어와있음을 확인할 수 있다.

agg 혹은 시각화 진행시 데이터를 잘 다룰 수 있다.



- 데이터 기입

```
# 벌크 데이터 삽입
$ curl -XPOST 'http://localhost:9200/_bulk?pretty' --data-binary @classes.json -H 'Content-Type:application/x-ndjson'

# 삽입된 데이터 확인
$ curl -XGET 'http://localhost:9200/classes/class/1/?pretty'
{
  "_index" : "classes",
  "_type" : "class",
  "_id" : "1",
  "_version" : 1,
  "_seq_no" : 0,
  "_primary_term" : 1,
  "found" : true,
  "_source" : {
    "title" : "Machine Learning",
    "Professor" : "Minsuk Heo",
    "major" : "Computer Science",
    "semester" : [
      "spring",
      "fall"
    ],
    "student_count" : 100,
    "unit" : 3,
    "rating" : 5,
    "submit_date" : "2016-01-02",
    "school_location" : {
      "lat" : 36.0,
      "lon" : -120.0
    }
  }
}
```



---



### 8강 엘라스틱 서치 데이터 조회 (Search)

> 사용되는 데이터는 Simple_basketball.json파일이고, ch3에 있다.

- 실습에 사용되는 데이터 삽입

```
$ curl -XPOST 'http://localhost:9200/_bulk?pretty' --data-binary @simple_basketball.json -H 'Content-Type:application/x-ndjson'
```

- 조회 (Search)

```
$ curl -XGET 'http://localhost:9200/basketball/record/_search?pretty'

{
  "took" : 24,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 2,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    "hits" : [
      {
        "_index" : "basketball",
        "_type" : "record",
        "_id" : "1",
        "_score" : 1.0,
        "_source" : {
          "team" : "Chicago Bulls",
          "name" : "Michael Jordan",
          "points" : 30,
          "rebounds" : 3,
          "assists" : 4,
          "submit_date" : "1996-10-11"
        }
      },
      {
        "_index" : "basketball",
        "_type" : "record",
        "_id" : "2",
        "_score" : 1.0,
        "_source" : {
          "team" : "Chicago Bulls",
          "name" : "Michael Jordan",
          "points" : 20,
          "rebounds" : 5,
          "assists" : 8,
          "submit_date" : "1996-10-11"
        }
      }
    ]
  }
}
```

- 조건 조회 (query string 이용)

```
$ curl -XGET 'http://localhost:9200/basketball/record/_search?q=points:30&pretty'

{
  "took" : 11,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    "hits" : [
      {
        "_index" : "basketball",
        "_type" : "record",
        "_id" : "1",
        "_score" : 1.0,
        "_source" : {
          "team" : "Chicago Bulls",
          "name" : "Michael Jordan",
          "points" : 30,
          "rebounds" : 3,
          "assists" : 4,
          "submit_date" : "1996-10-11"
        }
      }
    ]
  }
}
```

- 조건 조회 (request body이용)

```
$ curl -XGET 'localhost:9200/basketball/record/_search?pretty' -d '{"query":{"term":{"points": 30}}}' -H 'Content-Type:application/json'

{
  "took" : 1,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    "hits" : [
      {
        "_index" : "basketball",
        "_type" : "record",
        "_id" : "1",
        "_score" : 1.0,
        "_source" : {
          "team" : "Chicago Bulls",
          "name" : "Michael Jordan",
          "points" : 30,
          "rebounds" : 3,
          "assists" : 4,
          "submit_date" : "1996-10-11"
        }
      }
    ]
  }
}
```



---



### 9강 엘라스틱 서치 메트릭 어그리게이션 (Metric Aggregation)

> AGGREGATIONS?

The aggregations framework helps provide aggregated data based on a search query. It is based on simple building blocks called aggregations, that can be composed in order to build complex summaries of the data.

> Metric Aggregations?

Aggregations that keep track and compute metrics over a set of documents. (산술적인 연산시 필요)

- Aggregation structure

<img src="https://drive.google.com/uc?id=1EuFPkEotQy3j5op2EF2t88Ozzv0QMBgi" height="300">

- ElasticSearch에 bulk 데이터 기입

```
$ curl -XPOST 'localhost:9200/_bulk' --data-binary @simple_basketball.json -H 'Content-Type:application/x-ndjson'

$ curl -XGET 'localhost:9200/basketball?pretty' # 조회
```

- Aggregation json 파일 확인 **평균 값 구하기** (avg_points_aggs.json @ ch3)

```json
{
	"size" : 0,
	"aggs" : {
		"avg_score" : {
			"avg" : {
				"field" : "points"
			}
		}
	}
}
```

- Aggregation을 ElasticSearch를 이용해서 돌린다. (**평균 값**)

```
$ curl -XGET localhost:9200/_search?pretty --data-binary @avg_points_aggs.json -H 'Content-Type:application/json'

{
  "took" : 772,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 2,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "avg_score" : {
      "value" : 25.0
    }
  }
}
```

- Aggregation json 파일 확인 **최대 값 구하기** (max_points_aggs.json @ ch3)

```json
{
	"size" : 0,
	"aggs" : {
		"max_score" : {
			"max" : {
				"field" : "points"
			}
		}
	}
}
```

- Aggregation을 ElasticSearch를 이용해서 돌린다. (**최댓 값**)

```
$ curl -XGET localhost:9200/_search?pretty --data-binary @max_points_aggs.json -H 'Content-Type:application/json'

{
  "took" : 3,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 2,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "max_score" : {
      "value" : 30.0
    }
  }
}
```



- Stats (연산 집계) 구하기 (**count, max, min, sum, avg**)

```
# json 파일
{
	"size" : 0,
	"aggs" : {
		"stats_score" : {
			"stats" : {
				"field" : "points"
			}
		}
	}
}

$ curl -XGET localhost:9200/_search?pretty --data-binary @stats_points_aggs.json -H 'Content-Type:application/json'

{
  "took" : 1,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 2,
      "relation" : "eq"
    },
    "max_score" : null,
    "hits" : [ ]
  },
  "aggregations" : {
    "stats_score" : {
      "count" : 2,
      "min" : 20.0,
      "max" : 30.0,
      "avg" : 25.0,
      "sum" : 50.0
    }
  }
}
```



---



### 10강 엘라스틱서치 버켓 어그리게이션 (Bucket Aggregation)

> BUCKET AGGREGATIONS

Bucket aggregation create buckets of documents. (**group by**)

Bucket aggregations can hold sub-aggregations.

- Aggregation structure

<img src="https://drive.google.com/uc?id=1EuFPkEotQy3j5op2EF2t88Ozzv0QMBgi" height="300">

- aggregation 예제 삽입



---



#### 1강부터 10강까지 진행된 내용

**ElasticSearch에 대한**

1. 설치
2. 기본 개념 정리 
3. 데이터 다루는 방법 (RestAPI PUT, GET, DELETE POST)
4. 벌크 데이터 파일로부터 불러오기
5. 맵핑 (RDB에서 Schema)
6. 데이터 조회
7. 데이터 집계 (단순 document & group by)