# BERT Finetuning - 동화책 감정 태깅 모델

https://github.com/SKTBrain/KoBERT 에서 공개한 koBERT에 데이터를 추가학습시켜 동화책의 감정을 분류할 수 있도록 만든 classification 모델

**감정 4분류: neutral, happy, sad, angry**

- Full code for training nlp_checkpoint.pt --> [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1UjGE84sDTyVxKvtEiYfolRwzRyQ-Dv9V?usp=sharing)

- download nlp_checkpoint.pt --> https://drive.google.com/file/d/1ErLIhldgSchaKF3iNpG5O1C7eFWc8Maq/view?usp=sharing

### load nlp_checkpoint.pt to predict sentiment & make txt file for tts
for_custom_clf.ipynb 다운로드 후 주석처리 된 파일 경로를 원하는 동화책 텍스트 파일 경로로 변경


## 추가학습을 위한 data
Data collection 폴더

- 감정 분류를 위한 음성 데이터셋의 scripts: 5차년도.csv + 5차년도_2차.csv
- 카이스트 오디오북 scripts: kaist_scripts.xlsx에서 동화1, 동화2 sheet 추출 -> 각 약 600줄에 감정 직접 태깅

=> 통합 후 data_onlytales.csv 생성

#### samples:
![sentiment_id](https://user-images.githubusercontent.com/80621384/131179599-da884379-2184-42be-bae8-71195eaa91ed.png)

#### 감정 distribution:
![image](https://user-images.githubusercontent.com/78553384/130914104-df4020fc-5811-4d3e-a757-7be296d46d36.png)

총 17,929개의 데이터 추가학습

## Finetuning model
Pretrained Language Model - BERT

: 관련 대량 코퍼스 -> BERT -> 분류를 원하는 데이터(위의 새롭게 구성한 dataset) -> LSTM, CNN 등의 머신러닝 모델 -> 분류

<p align="center"><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcEoPYe%2FbtqBW0v9pJo%2FxM7PQl9BL0XAKX9fYuphw1%2Fimg.png"></p>

SKT에서 공개한 [코랩 환경에서의 튜토리얼](https://colab.research.google.com/github/SKTBrain/KoBERT/blob/master/scripts/NSMC/naver_review_classifications_pytorch_kobert.ipynb)을 기반으로 한 다중분류 모델(튜토리얼은 이중분류)

### requirements
```
Python >= 3.6
PyTorch >= 1.7.0
MXNet >= 1.4.0
gluonnlp >= 0.6.0
sentencepiece >= 0.1.6
onnxruntime >= 0.3.0
transformers >= 3.5.0
```
**특이사항** :
transformers 패키지를 pip로 설치 시 최신 버전과 튜토리얼 코드 사이에 에러가 발생해 
```
!pip install transformers==3.3.0
```
으로 버전을 특정해주었음
> Input: must be Tensor, not str

### model parameters
```
## Setting parameters
max_len = int(np.percentile(sents_length, 85))
batch_size = 32
warmup_ratio = 0.1
num_epochs = 20
max_grad_norm = 1
log_interval = 200
learning_rate = 3e-5
patience = 3
```
- max_len은 문장 길이 제3사분위보다 살짝 높은 값을 적용
- early stopping 적용을 위한 patience 변수 설정

## Output 예시(중간단계) - for_custom_clf.ipynb
크롤링한 동화책 중 빨간모자 텍스트를 문장별로 분리해, 최종 학습을 마친 모델로 감정 태깅

보다 정확한 문장 분리를 위해 kss 패키지 설치 필요
```
!pip install kss
```

**label_dict = {'neutral':0, 'happy':1, 'sad':2, 'angry':3 }**

![labeled](https://user-images.githubusercontent.com/80621384/131179566-e3a22f3f-67dd-4817-8b1e-9b5cf51ed70a.png)

## Output 예시(최종단계) - for_custom_clf.ipynb
emotion transplant가 완료된 Tacotron2 모델에 넣어 화자의 목소리로 읽을 수 있도록 하기 위해 txt 데이터로 변환 
-> 'reference_wav|텍스트|speaker_id|emotion|emotion'
- reference_wav의 경우 화자의 어떤 음성파일 경로를 넣어도 상관없음. 본 프로젝트에서는 jvoice폴더의 jvoice_3_L.wav로 통일

![redhat_text](https://user-images.githubusercontent.com/80621384/131178939-bee67537-9996-410a-9138-e9c76241537b.png)
