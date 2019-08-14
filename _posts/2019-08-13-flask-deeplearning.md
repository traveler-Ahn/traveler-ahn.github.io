---
layout: post
title:  "2019/08/13 플라스크(flask) 딥러닝 서버, 얼굴인식(Face Recognition)/물체인식(Object detection)"
subtitle: "2019/08/13 플라스크(flask) 딥러닝 서버, 얼굴인식(Face Recognition)/물체인식(Object detection)"
categories: til
tags: til
comments: true
---

- 얼굴인식 및 감지된 얼굴에서
  - 1) 나이예측 & 성별 예측 (Multi-task CNN)
  - 2) 감정예측
  - 3) 특징점 추출 (mtcnn API사용)
- 물체인식 (Object detection, SSD)
- Javescript + JQuery + Bootstrap + Flask video streaming deeplearning Web Server 구현
- 앞으로 계속 업데이트 될 페이지 입니다. (190813)

---

# Flask deeplearning

- 주로 학습된 딥러닝 모델에 대해 Flask 서버 구현 과정에 대한 글을 작성합니다.
- 모델은 구현하면서 직접 학습시키기도 했지만, 이와 관련해서는 나중에 기회가 된다면 따로 글을 작성하겠습니다.
- 혹시나, 문제 생기면 언제든 답글 남겨주세요. 미리 감사합니다 :)

---

### 0. 초기 셋업

- 모든건 [여기](https://traveler-ahn.github.io/til/2019/08/13/ubuntu18-first-su/)에서 셋업한 환경을 갖췄다는 전제하에 진행합니다. (at least `Tensorflow GPU (or CPU) v1.14.0`)

### 1. 가상환경 s/u 및 실행하기

```
#### 가상환경 s/u
$ mkdir flask_deeplearning
$ cd flask_deeplearning
~/flask_deeplearning$ python3 -m venv flask

### 가상환경 실행
~/flask_deeplearning$ source flask/bin/activate
```

### 2. 플라스크 및 필요파일 설치하기

```
#### pip 최신버전 업그레이드
(flask) ~$ python3 -m pip install --upgrade pip

#### flask 설치
(flask) ~$ pip install flask

#### Keras 설치
(flask) ~$ pip intall keras

#### mtcnn 설치 (Face detection, Landmark detection)
(flask) ~$ pip install mtcnn

### opencv 설치
(flask) ~$ pip install opencv-python
```

### 3. 관련 파일 전체 다운로드

- [저의 github](https://github.com/traveler-Ahn/flask_deeplearning)에서 관련 전체 파일을 cloning하시면 됩니다.

```
(flask) ~$ cd flask_deeplearning
(flask) ~/flask_deeplearning$ git clone https://github.com/traveler-Ahn/flask_deeplearning.git
```

#### 모델 파일 추가하기

- 해당 [경로](https://drive.google.com/drive/folders/1vBnoOsVKDmy55-6Ky9CtEwrr3SYkD7pJ)에서 모델 파일을 다운받아서 models폴더 안에 넣어줍니다.

### 4. 실행!

```
# Web cam 실행 
(flask) ~/flask_deeplearning/flask_deeplearning$ python3 app.py -i cam
(flask) ~/flask_deeplearning/flask_deeplearning$ python3 app.py -i VIDEO_PATH  (Video file)

and Web browser(Firefox & Chrome supported)
http://localhost:5000
```
- [깃허브](https://github.com/traveler-Ahn/flask_deeplearning)에서 구현된 결과와 코드를 확인하세요:)



