---
layout: post
title:  "2019/08/17 python 예외처리"
subtitle: "2019/08/17 python 예외처리"
categories: development
tags: python
comments: true
---

- 파이썬에서 예외처리하는 방법을 다룹니다. ([Ref](https://wayhome25.github.io/python/2017/02/26/py-12-exception/))
  - try / except
  - 예외 이름을 모르는 경우
  - 직접 예외를 부르는 raise

------

## 파이썬 예외처리

### <span style="color:#FF0033">1. try / except</span>

- 파이썬으로 프로그래밍 중에 만나는 에러를 유연하게 다룰 수 있게 도와주는 도구



### 에러 예시

```python
# IndexError
>>> list = []
>>> list[0]
IndexError: list index out of range

# ValueError
>>> text = 'abc'
>>> number = int(text)
ValueError: invalid literal for int() with base 10: 'abc'
```



### try / except문의 사용예시

- 미리 에러가 발생할만한 부분을 try / except문으로 감싸준다면 프로그램 동작중에 에러가 발생할 시 `프로그램이 멈추지 않고` 별도 처리가 가능해진다.

![alt try_excep_use_case](https://drive.google.com/uc?id=1kkD9bSibhWRNUm8gtxDmmqDQcaJAE7qb)



```python
text = '100%'

try :
    number = int(text) # 에러가 발생할 가능성이 있는 코드
except ValueError :  # 에러 종류
    print('{}는 숫자가 아닙니다.'.format(text))  #에러가 발생 했을 경우 처리할 코드
```

- 경우에 따라 예외 처리 대신 if/else 문을 사용할 수 있다. 더 간결한 표현은 if문을 사용하는 것이 좋다.

```python
# try-except 문
def safe_pop_print(list, index):
    try:
        print(list.pop(index))
    except IndexError:
        print('{} index의 값을 가져올 수 없습니다.'.format(index))

safe_pop_print([1,2,3], 5) # 5 index의 값을 가져올 수 없습니다.

# if 문
def safe_pop_print(list, index):
    if index < len(list):
        print(list.pop(index))
    else:
        print('{} index의 값을 가져올 수 없습니다.'.format(index))

safe_pop_print([1,2,3], 5) # 5 index의 값을 가져올 수 없습니다.
```

- try 문으로만 해결이 가능한 문제도 있다.

```python
try:
    import your_module
except ImportError:
    print('모듈이 없습니다.')
```



---

### <span style="color:#FF0033">2. 예외 이름을 모르는 경우</span>

```python
# 모든 에러 처리
try:
    list = []
    print(list[0])  # 에러가 발생할 가능성이 있는 코드

    text = 'abc'
    number = int(text)
except:
    print('에러발생')

# 에러 이름 확인
try:
    list = []
    print(list[0])  # 에러가 발생할 가능성이 있는 코드

except Exception as ex: # 에러 종류
    print('에러가 발생 했습니다', ex) # ex는 발생한 에러의 이름을 받아오는 변수
    # 에러가 발생 했습니다 list index out of range
```

- 모든 에러를 받을 수 있도록 Exception을 추가하여 코드를 동작시킬 수 있고, 이를 출력함으로써 어떤 에러인지 확인 할 수 있다.



---

### <span style="color:#FF0033">3. 에러를 직접 일으키는 방법 raise</span>

- 특정 상황에서 사용자가 직접 에러를 발생시키는 기능 (사용자가 원치않는 입력이 들어올 때 처리하곤 한다.)
- 잦은 사용은 코드를 읽기 어렵게 한다.

```python
# 올바른 값을 넣지 않으면 에러를 발생시키고 적당한 문구를 표시한다.
def rsp(mine, yours):
    allowed = ['가위','바위', '보']
    if mine not in allowed:
        raise ValueError
    if yours not in allowed:
        raise ValueError

try:
    rsp('가위', '바')
except ValueError:
    print('잘못된 값을 넣었습니다!')
```

```python
# 190이 넘는 학생을 발견하면 반복을 종료한다.
school = {'1반' : [150, 156, 179, 191, 199], '2반' : [150, 195, 179, 191, 199]}

try:
    for class_number, students in school.items():
        for student in students:
            if student > 190:
                print(class_number, '190을 넘는 학생이 있습니다.')
                # break # 바로 상위 for문은 종료되지만 최고 상위 for문은 종료되지 않는다.
                raise StopIteration
                # 예외가 try 문 안에 있지 않으면 에러 발생시 프로그램이 멈춘다.
except StopIteration:
    print('정상종료')                
```



---



### Reference

- [여기서](https://wayhome25.github.io/python/2017/02/26/py-12-exception/) 거의 모든것을 퍼왔습니다.