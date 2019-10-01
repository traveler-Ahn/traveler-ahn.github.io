---
layout: post
title:  "2019/10/01 [이미지변환-GAN #1] GAN 기본 지식"
subtitle: "2019/10/01 [이미지변환-GAN #1] GAN 기본 지식"
categories: deeplearning
tags: Imagetranslation
comments: true
---

- 이미지변환-GAN
	- 이미지 변환 기술 정리
	- 특히 GAN을 활용한 이미지 변환기술 정리
	- 이곳을 [참조]()하였습니다.

---

# [이미지변환-GAN #1] GAN 기본 지식
- GAN(Generative Adversarial Network)을 활용한 이미지 변환을 위한 첫 걸음으로 기본 GAN 기술에 대해서 간략하게 정리함

- 최윤제님 [강의 자료](https://www.slideshare.net/NaverEngineering/1-gangenerative-adversarial-network?from_action=save)와 [강의](https://www.youtube.com/watch?v=odpjk7_tGY0)를 바탕으로 정리합니다.

#### 1. Intuition in GAN

<img src="https://drive.google.com/uc?id=1ccybl7a531SDZ6lh1sNx0PtwaGcfBGwU">



**(Vanila) GAN Network는 두 가지 관점으로 접근하면 된다.**

1) Discriminator (감별자)

 - 입력 이미지가 들어왔을 때, 입력된 이미지가 거짓인지(0) , 진짜인지(1) 판단한다.

 - Discriminator는 입력된 이미지가 진짜인지 가짜인지 "잘"구분하기 위해서 학습이 진행된다.

 - 감별자는 진짜 이미지(real image)가 들어왔을 때, 이를 진짜 이미지라고 구분(sigmoid output -> 1) 해야하고,

 - 감별자는 가짜 이미지(fake image)가 들어왔을 때, 이를 가짜 이미지라고 구분(sigmoid output -> 0) 해야한다.

   

   <img src="https://drive.google.com/uc?id=1-gk49YeqMpHztZ4-Cc3h_EieCrHzUx75">



2) Generator (생성자)

- 입력  Latent Code가 들어왔을 때, Fake image를 생성한다.

- Generators는 Latent Code가 들어왔을 때, Discriminator를 "잘" 속이기 위해서 학습이 진행된다.

- 생성자는 가짜 이미지(fake image)를 만들어서, 이를 감별자가 진짜 이미지라고 착각(sigmoid output -> 1)하게 만들어야 한다.

  

  <img src="https://drive.google.com/uc?id=1gTaU2I3WJEDk1hiQvpRv1qWlHY_JFh82">



#### [pytorch 구현 참조](https://github.com/traveler-Ahn/image-translation-gan-1)

