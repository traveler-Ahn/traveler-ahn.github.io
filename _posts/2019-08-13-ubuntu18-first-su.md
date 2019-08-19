---
layout: post
title:  "2019/08/13 Ubuntu 18.04 내컴퓨터 초기 s/u"
subtitle: "2019/08/13 Ubuntu 18.04 내컴퓨터 초기 s/u"
categories: til
tags: til
comments: true

---

- 오늘 3시간 가량 우분투를 포멧하고 다시 설치하면서 삽질했던 기록들을 남깁니다.
- 앞으로 계속 업데이트 될 페이지 입니다. (190813)



---

# Ubuntu 18.04 내 컴퓨터 초기 s/u (190813)

- 이 모든 것들은 포멧을 반복하는 불쌍한 나 같은 사람들을 위한 recipe?
  - 우분투 초기 필수 프로그램
    - zip, 크롬, 그놈트윅, typora(마크다운 편집기), 팀뷰어, VS, git
  - 가상환경(virtualenv) Tensorflow gpu (1.14.0 with CUDA/cuDNN)
  - Pycharm IDE
  - 지킬(jykell) 깃허브 홈페이지 관리를 위한 환경 s/u (Ruby & RubyGem)

---

- 설치 순서는 제가 편한 순서입니다...ㅎㅎ
- 간단한건 기록하지만 다른 곳에서 얻은 것들은 웬만하면 링크를 그대로 걸어두었습니다.
- 혹시나, 문제 생기면 언제든 답글 남겨주세요. 미리 감사합니다 :)

---

### 1. Software updater

- 컴터 실행시 자동으로 업데이트 되는 파일 업데이트
- 그냥 next 클릭하면서 쭉 설치한다. (주로 update 관련내용들이다.)

### 2. zip 파일 설치

```
$ apt-get update
$ apt-get install zip unzip
```

### 3. 우분투 한글입력 (Eng. 설치)

- [링크]([https://gabii.tistory.com/entry/Ubuntu-1804-LTS-%ED%95%9C%EA%B8%80-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%84%A4%EC%A0%95](https://gabii.tistory.com/entry/Ubuntu-1804-LTS-한글-설치-및-설정)) 사이트에 잘 나와있습니다 :) 감사함당

### 4. 크롬 설치

- [링크](https://webnautes.tistory.com/1184) 사이트에 잘 나와있습니다 :) 감사함당

### 5. 저장소 업데이트, 그놈 [트윅](https://wnw1005.tistory.com/44) 설치

```
$ sudo apt update
$ sudo apt-get install gnome-tweak-tool
```

### 6. pip & python3 설치

```
$ sudo apt update
$ sudo apt install python3-pip
$ sudo apt install build-essential python3-dev  python3-setuptools
$ pip3 --version               # 설치 버전 확인
```

### 7. Tensorflow gpu s/u

- 기존에 갖고있는 GPU 1080Ti를 딥러닝용으로 사용하기 위해서,

  - NVIDIA graphic driver: `v410.104`
  - CUDA [v10.0](https://developer.nvidia.com/cuda-10.0-download-archive) compatible with NVIDIA `v410.104`
  - cuDNN [v7.6.2](https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.6.2.24/prod/10.0_20190719/cudnn-10.0-linux-x64-v7.6.2.24.tgz) compatible with CUDA `v10.0`
  - Tensorflow gpu `v1.14.0`

  으로 각각을 설치하였습니다. 

#### [NVIDIA 그래픽 드라이버 설치]

- GUI 상에서 설치가 간단하기 됩니다 :) ([ref](https://eungbean.github.io/2018/08/08/Ubuntu-Installation1/) 참조하였습니다.)

1. apt를 update 해주어야 합니다.

```
# PPA 추가하기
sudo apt-add-repository ppa:graphics-drivers/ppa -y
sudo apt update
```

2. 이후는 다음 [링크](https://www.linuxbabe.com/ubuntu/install-nvidia-driver-ubuntu-18-04)참조하시면 정말 쉽게 설명되어있습니다. (영어가 어려워도.. 그냥 그림만 보면서 클릭만 하시면 됩니다 ㅎㅎ)

#### [CUDA 드라이버 설치]

1. 해당 그래픽 카드에 맞는 CUDA 드라이버의 호환성을 [확인](https://docs.nvidia.com/deploy/cuda-compatibility/index.html)하고 맞는 CUDA 를 다운 받습니다.
2. 이후의 설치는 해당 [링크](https://eungbean.github.io/2018/08/08/Ubuntu-Installation2-1/) 확인하시면 됩니다. 

#### [cuDNN 설치]

1. 해당 CUDA 버전에 맞는 cuDNN을 [다운](https://developer.nvidia.com/cuda-toolkit-archive) 받습니다.
2. 이후의 설치는 해당 [링크](https://eungbean.github.io/2018/08/08/Ubuntu-Installation2-1/) 확인하시면 됩니다. 

#### [Tensorflow gpu 설치]

---

#### (Optional) virtualenv활용해서 설치

```
$ sudo apt install python3-venv

### Create project directory
$ mkdir tensorflow_gpu
$ cd tensorflow_gpu
```

##### Create venv

```
~/tensorflow_gpu$ python3 -m venv ./venv
```

##### Activate the environment

```
~/tensorflow_gpu$ source venv/bin/activate
```

- 이후부터는 가상환경 내부라고 가정하고 진행하겠습니다 :)

---

##### Tensorflow-gpu 설치 (v1.14.0)

```
(venv) ~/tensorflow_gpu$ pip install tensorflow-gpu==1.14.0
```

##### Tensorflow-gpu 장비확인

```
(venv) ~/tensorflow_gpu$ python3

>>> from tensorflow.python.client import device_lib
>>> device_lib.list_local_devices()
```

### 8. pycharm (python IDE) 설치

1. pycharm 프로그램을 (free opensource community) [다운](https://www.jetbrains.com/pycharm/download/#section=linux) 받는다.

2. 설치는 간단하다. 압축파일 풀고 해당 폴더내의 bin 폴더 내로 이동해서,

```
(venv) ~/pycharm/bin$ sh pycharm.sh
```

3. 나머지는 대부분 Default로 설치하면 된다.

### 9. typora 설치 (마크다운 편집기)

- 마크다운 편집기로 typora 설치한다.

#### [Install Typora on Linux Debian/Ubuntu]

```
$ wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add -

## add Typora's repository
$ sudo add-apt-repository 'deb https://typora.io/linux ./'
$ sudo apt-get update

## install typora
$ sudo apt-get install typora

## upgrade all packages include Typora
$ sudo apt-get upgrade
```

### 10. FileZilla 설치

- 편한 ftp 프로그램~

```
$ sudo apt install filezilla
```

### 11. Teamviewer

- 공식홈페이지에서 [다운](https://www.teamviewer.com/ko/download/linux/)받아서 설치하면 된다. (.deb 패키지 다운받아서 gui로 클릭만하면 설치 완료된다.)

### 12. Visualstudio Code

- 공식홈페이지에서 [다운](https://code.visualstudio.com/docs/?dv=linux64_deb)받아서 설치하면 된다. (.deb 패키지 다운받아서 gui로 클릭만하면 설치 완료된다.)

### 13. git 설치

```
$ sudo apt install git
```

### 14. [지킬](https://jekyllrb-ko.github.io/)페이지 관리를 위한 [루비](https://www.ruby-lang.org/ko/documentation/installation/) 설치

- 기존에 갖고있던 깃헙 페이지를 새로 싹 깨끗하게 민 데스크탑에 다운받아서 로컬에서 관리하기 위해 루비환경을 셋팅한다. (`시간 오래걸린다...ㅠㅠ`)

##### - 기존에 설치되어있는지 확인

```
$ ruby -v
```

##### - apt를 사용한 Debian이나 Ubuntu용 환경에서 [ruby 설치](https://www.ruby-lang.org/ko/documentation/installation/#apt)

```
$ sudo apt-get install ruby-full
```

##### - RubyGems 설치 ([자세한건...](https://rubygems.org/pages/download))

```
$ gem update --system          # may need to be administrator or root
$ gem install rubygems-update  # again, might need to be admin/root
$ update_rubygems              # ... here too
```

##### - github에서 지킬 github 페이지 cloning

###### - [지킬 페이지](https://jekyllrb-ko.github.io/docs/quickstart/) 참조하여 빠른 설치 진행 

#### 로컬에서 지킬페이지 실행되는지 확인

```
## RubyGems 를 통해 Jekyll 과 Bundler 를 설치한다
$ sudo gem install jekyll bundler

## 2.에서 다운받은 깃헙 페이지를 테스트해보기 위해 미리보기 서버로 사이트를 빌드한다
~/test.github.io$ bundle exec jekyll serve

# 이제 브라우저로 http://localhost:4000에 접속하여 확인한다.
```

### 15. tree 설치

- 폴더 구조 파악하기 편하다.

```
$ sudo apt install tree
```

#### 16. Ubuntu sticker note 설치 (Ref from [here](https://itsfoss.com/indicator-stickynotes-windows-like-sticky-note-app-for-ubuntu/))

```
$ sudo add-apt-repository ppa:umang/indicator-stickynotes
$ sudo apt-get update
$ sudo apt-get install indicator-stickynotes
```

![stickynote](https://drive.google.com/uc?id=1wzAse6hoygpzSy1OJOhibWcKTEbnpKI1)



---

#### [Trouble shooting]

- 모르겠다... 나만 그런지 다들 그랬을지....

```
Could not find jekyll-sitemap-1.2.0 in any of the sources
Run `bundle install` to install missing gems.
```

- 위와 같은 에러가 나올 때는 그냥 파일 설치를 계속했다...ㅎㅎㅎ 그러다 보니 되더라

```
$ sudo gem install jekyll-sitemap --version 1.2.0
```

---
