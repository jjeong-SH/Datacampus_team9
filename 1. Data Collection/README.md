# 사용할 데이터 정리 및 수집

## 1. 모델 훈련용
### Selvas AI 감정 화자 데이터 (https://github.com/emotiontts/emotiontts_open_db/tree/master/Dataset/SpeechCorpus)

**(주)셀바스AI가 '구축한 로봇의 감정 및 개성을 표현할 수 있는 대화형 음성코퍼스 DB'로, Tacotron2 모델의 감정 학습을 위해 사용하였음**

- 감정 표현 기술 연구를 위한 연구용 DB (감정 대본) : 여성 5인, 남성 5인  
		: 감정 대본을 사용하여 녹음  
		: 일반, 기쁨, 화남, 슬픔  
    : 400문장(감정별 100문장) x 10명  
    : 음성데이터, 녹음 대본, 대본 철자전사  

### 감성 대화 말뭉치 데이터 (https://aihub.or.kr/aidata/7978)
**텍스트와 음성 데이터 둘 다 사용 예정**
  - 텍스트: 동화책 문장의 감성 판단을 위한 학습 자료로 사용 (각 문장 별 id와 화자의 성별, 감성 대분류, 내용만을 뽑아서 사용)
  
  ![feature그림](https://user-images.githubusercontent.com/80621384/126633249-dbbde35d-0f23-4ab3-9ea5-8790c9718ef0.png)

  - 음성: 감성에 따른 음성 변조의 특성을 잡아내기 위해 사용 (대본은 텍스트 파일 문장과 동일 / 확장명 wav)
  
  ![음성사진1](https://user-images.githubusercontent.com/80621384/126633992-656ce39e-997c-4af5-bd54-75e808375b00.png)


### KSS audio dataset (https://www.kaggle.com/bryanpark/korean-single-speaker-speech-dataset) 
**한국어 음성과 대본만을 사용**

음성 모사 시 transfer 학습을 위해 사용. KSS dataset으로 모델을 먼저 학습시킨 이후 개인의 음성을 추가 학습시킬 계획 

<p align="center"><img src="https://user-images.githubusercontent.com/80621384/126634266-cbeb4c56-07db-4937-9ace-3e793b85a357.png"></p>

## 2. 시연용 (모델이 잘 돌아가는지 확인해보기 위한 데이터)

### 동화책 텍스트 데이터(https://www.grimmstories.com/ko/grimm_donghwa/ppalgan_moja)
**텍스트로만 이루어져 있음**

automated 감성 태깅 시스템이 잘 작동하는지 확인하기 위해 사용할, 감성이 분류되어 있지 않은 raw 동화책 텍스트 데이터

<p align="center"><img src="https://user-images.githubusercontent.com/80621384/126634820-89deea72-28db-4f5b-9d51-0dba6d0ee49f.png", width="400"></p>

### 카이스트 오디오 북 데이터셋 (https://aihub.or.kr/opendata/kaist-audiobook) 
**동화책 음성과 대본만을 사용**

speech synthesis 모델 완성 후, 추가학습을 통해 특정 사람의 목소리를 잘 모사할 수 있는지 판단할 때 사용 (감성 태깅은 되어있지 않음)

<img src="https://user-images.githubusercontent.com/80621384/126635356-86b3f30a-d34d-44ef-a3ca-0f4f24653302.png" width="500">![오디오대본1](https://user-images.githubusercontent.com/80621384/126635379-18183d97-4c8f-4c76-9f19-757f430128a9.png)

## 3. 최종 동화책 합성

### 조원 박지현 음성 데이터
**직접 녹음하여 사용**

조원 박지현님이 직접 수능 국어 비문학 지문을 녹음하여 그 음성파일로 Tacotron2 모델을 추가 학습했습니다.

이미지 추가필요
