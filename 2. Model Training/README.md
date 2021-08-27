Multi-Speaker Emotional Tacotron2 + BERT 감성분석 시스템
=====

아이들을 위한 ABC는 자연어의 감성분석 기술과 TTS 음성합성 기술을 융합한 개인 오디오북 제작 시스템입니다.   



BERT 기반 감성분석 시스템
-----
임의의 텍스트를 input으로 주면 해당 텍스트에 맞는 감정을 output으로 주는 모델입니다.

Multi-Speaker Emotional Tacotron2 : Tacotron2 기반 TTS 시스템
-----
!!!model structure 추가!!!

### 1. Text-to-Mel Prediction
: emotion embedding을 사용한 Tacotron2 모델 사용   

- input : 스피커 id, 감성태그가 있는 텍스트   
- output : 해당 스피커의 목소리에 emotion이 합성된 mel-spectrogram   

### 2. Vocoder
: WaveGlow를 통해 mel-spectrogram을 wav 파일로 변환

