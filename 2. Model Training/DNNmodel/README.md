# Emotion TTS Model


## 1.tacotron2
Tacotron2 모델에 각 emotion의 Embedding을 주어 감정 별 melspetrogram을 만들 수 있게 하는 모델 + WaveGlow vocoder

!!!!모델 아키텍쳐!!!!


#### model testing을 위해 disgust emotion dataset으로만 돌려보는 중(계속 학습중임!!) 
#### --> https://drive.google.com/drive/folders/1tMJgUUvb0NACwtaNgnuIFxhzLos3PPdv?usp=sharing

  - tacotron2-vae 안에 filelists 폴더 체크(train, valid, test)
  - (0816.note) 현재 0816_testing_vae_dis 코랩 파일로 계속 학습중 **건들지말기**

### issuses
- [SOLVED] requirements 버전 호환의 문제
```
# 다른 건 몰라도 이거 세개는 꼭 맞춰줘야함
tensorflow==1.14
tensorboardX==1.8
numpy<1.17
torch==0.4.1.post2 (0.4.1도 가능한지는 확인 중)
```
이후 발생하는 tensorboard-plugin-wit 에러는 pip freeze 이후 해당 패키지 uninstall 해줘야함 --> 후에 tensorboard로 학습 상황 확인 가능

- [SOLVED] "IndexError: Caught IndexError in DataLoader worker process 0." : train, valid 데이터셋 확인, 형식에 맞지 않는 문자열 수정

- [SOLVED] DataLoader의 num_worker=1 crashes : num_worker=0으로 바꿔주기

- [검토중] SHUTDOWN ERROR 오류 없이 프로그램 종료 -> 아마 GPU out-of-memory인듯?

![KakaoTalk_20210815_184737867](https://user-images.githubusercontent.com/80621384/129483347-523976ff-98ea-48eb-b63f-524c7a040206.png)

(0815note) 지금은 batch_size=4로 줄이고 데이터셋도 절반만 가지고 돌리는 중.. **대책 필요**


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
