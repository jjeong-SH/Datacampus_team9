Multi-Speaker Emotional Tacotron2 + BERT 감성분석 시스템
=====

아이들을 위한 ABC는 자연어의 감성분석 기술과 TTS 음성합성 기술을 융합한 개인 오디오북 제작 시스템입니다.   

## 1. Multi-Speaker Emotional Tacotron2
Tacotron2 모델에 각 emotion의 Embedding을 주어 감정 별 melspetrogram을 만들 수 있게 하는 모델 + WaveGlow vocoder

![Tacotron2](https://user-images.githubusercontent.com/52599330/131188384-68382e57-6e51-4a33-9695-662b5dbd498f.png)

#### 1. Text normalization 한글이 아닌 텍스트를 한글로 변환 
오늘은 8월 28일 -> 오늘은 팔월 이십팔일
#### 2. 모델이 읽을 수 있게 Tokenize, 영문으로 발음 변환
#### 3. Spectrogram 생성
Tacotron2 모델 안 쪽에서 Embedding (text, emotion, speaker) 을 encoder / decoder 사이에서 concatenate 해줘서 감정, 스피커 별 특성을 포함한 Mel을 생성해줍니다.
#### 4. Vocoder 사용해서 wav 파일 생성
Griffin-Lim 같은 통계적인 기존 기법의 성능이 좋지 않아 뉴럴 보코더인 WaveGlow를 사용하였습니다.

## 2. BERT 기반 감정 인식
