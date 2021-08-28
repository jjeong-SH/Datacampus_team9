# 사용할 데이터 정리 및 수집
모델 학습을 위한 데이터셋과, 모델이 완성된 후 여러 동화책 텍스트를 잘 읽을 수 있는지 확인하는 시연용 데이터셋으로 나뉨.

## 1. For Training

### 감정 분류를 위한 대화 음성 데이터셋 (https://aihub.or.kr/opendata/keti-data/recognition-laguage/KETI-02-002)
**텍스트 데이터만 사용**

  - 동화책 문장의 감성 판단을 위한 학습 자료로 사용 (wav_id와 발화문, 상황만을 뽑아서 사용): 5차년도와 5차년도_2차
  
  ![csv_image](https://user-images.githubusercontent.com/80621384/131170880-dcbfc692-222c-4f04-9131-82e484db3ee4.png)
  
### 카이스트 오디오북 데이터셋 (https://aihub.or.kr/opendata/kaist-audiobook)
**텍스트 데이터만 사용**

 - 동화책 문장의 감성 판단을 위한 학습 자료로 사용 (index와 대사만을 뽑아서 사용): 동화1과 동화2 sheet
 
![kaist](https://user-images.githubusercontent.com/80621384/131172282-07ce7e14-8c53-4e9b-b907-1b2a4e89e4be.png)


### Selvas AI 감정 화자 데이터 (https://github.com/emotiontts/emotiontts_open_db/tree/master/Dataset/SpeechCorpus)

**(주)셀바스AI가 '구축한 로봇의 감정 및 개성을 표현할 수 있는 대화형 음성코퍼스 DB'로, Tacotron2 모델의 감정 학습을 위해 사용**

- 감정 표현 기술 연구를 위한 연구용 DB (감정 대본) : 여성 5인, 남성 5인  
		: 감정 대본을 사용하여 녹음  
		: 일반, 기쁨, 화남, 슬픔  
    : 400문장(감정별 100문장) x 10명  
    : 음성데이터, 녹음 대본, 대본 철자전사  


### 조원 박지현 음성 데이터
**직접 녹음하여 사용**

 - 음성 모사 시 transfer 학습을 위해 사용. 조원 박지현님이 직접 수능 국어 비문학 지문을 녹음하여 그 음성파일로 Tacotron2 모델을 추가 학습함.
 
 - 한 문장씩 나눠진 음성 데이터, 총 약 1시간 10분의 분량 -> 데이터가 부족해 하나의 2 channel wav 파일을 2개의 mono channel로 바꿔 증강 후 학습.

 - 본 프로젝트의 목적은 감정이 실리지 않은 monotone voice를 emotion transplant를 통해 생생하게 만들어주는 것이므로, 화자의 음성은 최대한 monotonous하게 녹음되었음.

 - 추후 Tacotron2 모델의 학습 input으로 쓰기 위해 'wav파일경로|텍스트|speaker_id|감정|감정' 형식으로 텍스트 파일을 저장함.
```
##텍스트 파일 예시
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_1_L.wav|과학적 지식은 어떻게 생성될까?|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_1_R.wav|과학적 지식은 어떻게 생성될까?|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_2_L.wav|이에 대한 설명은 과학 철학적 관점에 따라 달라질 수 있다.|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_2_R.wav|이에 대한 설명은 과학 철학적 관점에 따라 달라질 수 있다.|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_3_L.wav|그 중 하나가 경험적 검증 가능성에 의해 과학적 진술의 의미를 판가름하는 논리 실증주의적 관점이다.|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_3_R.wav|그 중 하나가 경험적 검증 가능성에 의해 과학적 진술의 의미를 판가름하는 논리 실증주의적 관점이다.|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_4_L.wav|연어의 회귀에 대한 연구 과정을 통해 과학적 지식의 생성 과정을 논리 실증주의적 관점에서 살펴보기로 하자.|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_4_R.wav|연어의 회귀에 대한 연구 과정을 통해 과학적 지식의 생성 과정을 논리 실증주의적 관점에서 살펴보기로 하자.|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_5_L.wav|과학자들은 연어가 어떻게 태어난 곳으로 돌아오는지 알고 싶었다.|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_5_R.wav|과학자들은 연어가 어떻게 태어난 곳으로 돌아오는지 알고 싶었다.|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_6_L.wav|인디언들은 초자연적인 힘에 의해 연어가 회귀한다고 믿고 있었는데, 과학자들은 이러한 설명이 경험적으로 검증될 수 없기 때문에 과학적 의미가 없다고 생각했다.|pjh|0|0
/content/drive/MyDrive/emotion-tts/jvoice/jvoice_6_R.wav|인디언들은 초자연적인 힘에 의해 연어가 회귀한다고 믿고 있었는데, 과학자들은 이러한 설명이 경험적으로 검증될 수 없기 때문에 과학적 의미가 없다고 생각했다.|pjh|0|0
```

## 2. For Inference

### 동화책 텍스트 데이터(https://www.grimmstories.com/ko/grimm_donghwa/ppalgan_moja)

감정이 분류되어 있지 않은 동화책 텍스트로, BERT 감정 태깅 시스템을 사용해 자동 태깅을 진행했습니다.

이후 조원 박지현님의 음성을 학습하여 감정있는 오디오북을 생성했습니다.

<p align="center"><img src="https://user-images.githubusercontent.com/80621384/126634820-89deea72-28db-4f5b-9d51-0dba6d0ee49f.png", width="400"></p>
