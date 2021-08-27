# Emotion TTS Model


## 1. Multi-Speaker Emotional Tacotron2
Tacotron2 모델에 각 emotion의 Embedding을 주어 감정 별 melspetrogram을 만들 수 있게 하는 모델 + WaveGlow vocoder

!!!!모델 아키텍쳐!!!!

#### 1. Text normalization 한글이 아닌 텍스트를 한글로 변환 
오늘은 8월 28일 -> 팔월 이십팔일
#### 2. 모델이 읽을 수 있게 Tokenize, 영문으로 발음 변환
#### 3. Spectrogram 생성
Tacotron2 모델 안 쪽에서 Embedding (text, emotion, speaker) 을 encoder / decoder 사이에서 concatenate 해줘서 감정, 스피커 별 특성을 포함한 Mel을 생성해줍니다.
#### 4. Vocoder 사용해서 wav 파일 생성
Griffin-Lim 같은 통계적인 기존 기법의 성능이 좋지 않아 뉴럴 보코더인 WaveGlow를 사용하였습니다.



### further issus
- WaveGlow 학습 속도가 너무 느리고 epoch도 많이 돌아야 함 -> 다른 pretrained vocoder를 가져와(+추가학습) melspectrogram eval하는 후에 붙여보면 어떨까?
- 
https://github.com/chldkato/Tacotron-MelGAN-Korean, https://github.com/HGU-DLLAB/Korean-FastSpeech2-Pytorch

WaveGan이나 VocGan, (아직 영어 데이터셋에서만 돌아가기는 하지만) ParallelWaveGan 등 논문 상 훨씬 적은 시간이 걸린다고 함


## 2.gst-tacotron

추가바람

-----
## 3. Vocoder 
실험중인 모델은 원래 보코더로 WaveGlow를 사용
하지만 WaveGlow도 새로 학습해줘야하고 보코더 학습에 시간이 오래 걸리기 때문에 pre-trained 모델인 MelGAN 을 VAE의 보코더로 사용하고자 시도 중.

https://github.com/chldkato/Tacotron-MelGAN-Korean -> 시도 중인 코드 

### Issues
1. [Solved] VAE의 mel-spectrogram이 MelGAN의 input으로 들어갈 수 있어야 한다.
-> a. VAE의 Decoder와 b. inference.py 코드를 수정하여 Tacotron2-VAE의 중간 단계 아웃풋인 mel-spectrogram이 
WaveGlow의 infer로 바로 들어가지 않고, tacotron-output이라는 폴더 안에 바로 저장되는 방향으로 바꾸었다. 

<img src = "https://user-images.githubusercontent.com/83811753/129574900-8c29ddda-0992-4d66-a4f9-70bc6190e65c.png" : width = 500 height = 100>

2. (8/16 시도중) 생성한 mel-spectrogram이 MelGAN의 input으로 들어갔는데, padding 개수가 안맞다는 오류가 떴다.

<img src = "https://user-images.githubusercontent.com/83811753/129575182-87688b6d-9d35-4966-a876-5ad8916b7f15.png" : width = 700 height = 300>

<img src = "https://user-images.githubusercontent.com/83811753/129576076-c081d405-b531-4f70-a05a-00d0fe9896ec.png" : width = 450 height = 500>
-> 현재 gan.py 의 파란색 하이라이트 부분 확인 중임
