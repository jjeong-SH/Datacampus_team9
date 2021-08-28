# Multi-Speaker Emotional Tacotron2

**original github: https://github.com/hash2430/emotion_tts**

- NLP model(사용하지 않았음, 추가 학습하는 과정에서 initialize 이후 학습되지 않음) - https://drive.google.com/drive/folders/1-NXUTPzwPwZHXoQ5-AgE2d1hHc4B6kB3?usp=sharing
- tts model - https://drive.google.com/file/d/1MHhog5ykYfaeD69ALrghQa9ZQs1MjNdV/view?usp=sharing
- waveglow model - https://drive.google.com/file/d/1y12oOOQm8T5LaqFXdv24cJiPJU58X2Nd/view?usp=sharing

## Fine-tuning TTS model with custom data
조원 박지현(고려대)의 목소리 데이터 약 1시간을 추가로 학습 - /jvoice 폴더 확인

### 1. Prepare dataset
TTS 모델에 추가로 학습시키기 위해서는 다음과 같은 포맷으로 저장해야 함 'custom_wav경로|텍스트|감정|감정' -> 데이터 양이 적어 2 channel=>mono로 바꾸면서 똑같은 wav파일 두개씩 생성
```
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
```

### 2. directory path
화자, 스크립트, 설정파일, checkpoint, output 음원의 경로를 설정
**inference_with_guide.py는 수정하지 않아도 됨. .ipynb파일 이용**

### 3. train model
```
cd /content/drive/MyDrive/emotion-tts/emotion_tts
python train.py -o './train_test/outdir' -c './train_test/outdir/checkpoint_195500' -l './logdir'
```

기존에 있던 checkpoint_180000에서 지현님 목소리로 16500iteration 추가학습

### 4. run inference
코랩 환경에서 cd /emotion-tts/emotion-tts 경로로 이동 후 해당 코랩파일 실행 [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1wNfnVOlhctE8VK1bAV6n0fT5Onq4Dtf9?usp=sharing)

### 5. check outputs
First_Inference 폴더에서 결과 확인
- redhat_nes = emotion-tts 모델의 체크포인트에서의 화자의 목소리
- redhat_final, redhat_196, redhat_195 = 지현님 목소리로 읽어본 빨간모자 동화 오디오(문장별, 뒤 숫자는 iteration 앞자리)
