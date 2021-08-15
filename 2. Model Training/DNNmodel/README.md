# Speech Synthesis Model
**실험 중인 model**
1. tacotron2-vae(https://github.com/jinhan/tacotron2-vae): Tacotron2 + WaveGlow
2. gst-tacotron(https://github.com/syang1993/gst-tacotron): Tacotron으로 melspectogram 생성과 audio 변환을 한번에(End-to-End)
3. only vocoders:
   - WaveGlow
   - WaveGan
   - VocGan(https://arxiv.org/pdf/2007.15256.pdf)

[EDIT] 각자 돌려보고 돌아가는지 보고하기

------


## 1.tacotron2-vae
Tacotron2 모델에 각 emotion의 Embedding을 주어 감정 별 melspetrogram을 만들 수 있게 하는 모델 + WaveGlow vocoder

![vae1](https://user-images.githubusercontent.com/80621384/129482786-dbe8a1c9-feb4-4da3-a6f5-58e8d0c54f7c.png)

["Learning Latent Representations for Style Control and Transfer in End-to-end Speech Synthesis"](https://arxiv.org/pdf/1812.04342.pdf)

 -> 해당 논문과 유사하지만 vocoder가 WaveNet이 아님
 
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

