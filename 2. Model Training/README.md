Multi-Speaker Emotional Tacotron2 + BERT 감성분석 시스템
=====

아이들을 위한 ABC는 자연어의 감성분석 기술과 TTS 음성합성 기술을 융합한 개인 오디오북 제작 시스템입니다.   

## 1. Multi-Speaker Emotional Tacotron2
Tacotron2 모델에 각 emotion의 Embedding을 주어 감정 별 melspetrogram을 만들 수 있게 하는 모델 + WaveGlow vocoder

![Tacotron2-1](https://user-images.githubusercontent.com/52599330/131189517-61e88e87-14fe-4723-8f76-5a8ea81dabb7.png)

#### 1. Text normalization 한글이 아닌 텍스트를 한글로 변환 
오늘은 8월 28일 -> 오늘은 팔월 이십팔일
#### 2. 모델이 읽을 수 있게 Tokenize, 영문으로 발음 변환
#### 3. Spectrogram 생성
Tacotron2 모델 안 쪽에서 Embedding (text, emotion, speaker) 을 encoder / decoder 사이에서 concatenate 해줘서 감정, 스피커 별 특성을 포함한 Mel을 생성해줍니다.
#### 4. Vocoder 사용해서 wav 파일 생성
Griffin-Lim 같은 통계적인 기존 기법의 성능이 좋지 않아 뉴럴 보코더인 WaveGlow를 사용하였습니다.

## 2. BERT 기반 감정 인식
Transformer을 기반으로 한 사전 훈련 언어모델 => Transfer learning을 통해 custom dataset을 효과적으로 분류할 수 있도록 함(label이 있는 supervised learning)

![Untitled (11)](https://user-images.githubusercontent.com/80621384/131187205-437cd5ab-c4aa-4fed-9bb2-50deb0f13765.png)

### 구조 설명
#### 1. Positional Encoding

![Untitled (12)](https://user-images.githubusercontent.com/80621384/131187593-40cd1ef1-35c9-42d2-be58-c053698e9d92.png)

- 트랜스포머 인코더 디코더 부분에 모두 포함
- Attention layer에 들어가기 전, 입력값으로 주어질 단어 vector 안에 **단어의 위치 정보를 포함**시키는 방법
: 각 단어의 임베딩 벡터에 위치 정보들을 더하여 모델의 입력으로 사용
- how? → sin, cos값의 조합으로 순서값 표현

#### 2. Add & Norm
인코더와 디코더 각 서브층 연결점에 있음

- 잔차 연결*residual connection* : 서브층의 입력과 서브층의 출력을 f(x)+x의 구조처럼 더해주는 부분 → 모델의 학습을 돕는 기법 (뒤쪽까지 학습이 잘 전달되지 않는 것을 방지)

- 층 정규화*layer normalization* : 텐서의 마지막 차원에 대해서 평균과 분산을 구하고, 이를 가지고 수식을 통해 값을 정규화하는 방식

#### 3. Multi-head Self-Attention

![Untitled (13)](https://user-images.githubusercontent.com/80621384/131188970-9fe4d82d-2e2b-476c-add7-d2dbdaad04c9.png)

내적 셀프 어텐션 구조가 중첩된 형태
- 단어 벡터끼리의 내적 연산*dot product* : <a href="https://www.codecogs.com/eqnedit.php?latex=QK^T" target="_blank"><img src="https://latex.codecogs.com/gif.latex?QK^T" title="QK^T" /></a>
- attention weights를 구하는 수식 - ![이미지 24](https://user-images.githubusercontent.com/80621384/131188888-ef27321d-8a50-4c26-bb10-49a1ee41bbd9.png)
- 순방향 마스크 어텐션으로 관계 정보 masking : Query값보다 뒤에 나오는 Key 정보를 참조하지 못하도록 행렬의 아래쪽 삼각형 부분을 제외한 값에 매우 작은 값(-1e9) 넣어주기

#### 4. Position-wise FFNN

multi-head attention으로 나온 다양한 정보들을 합쳐주는 역할

- 한 문장에 있는 단어 토큰 벡터 각각에 대해 연산해주기 때문에 position-wise라고 함
- 두 개의 linear layer와 활성화 함수(relu) 활용


### Transfer Learning

- BERT의 언어 모델의 출력에 추가적인 모델을 쌓아 만듦

- 일반적으로 복잡한 CNN, LSTM, Attention을 쌓지 않고 간단한 DNN만 쌓아도 성능이 잘 나오며 별 차이가 없다고 알려져 있음

![다운로드](https://user-images.githubusercontent.com/80621384/131189200-689dd70f-cfd5-4855-b4ed-0457b3427426.png)
