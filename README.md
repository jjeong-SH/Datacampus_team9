





# 아이들을 위한 ABC 오디오북 제작 시스템

**자연어 감성분석 기술과 음성합성 기술을 융합한 개인 오디오북 제작 시스템**

자연어 감성분석 기술과 음성합성 기술을 이용하여 부모가 직접 읽어주는 실감나는 오디오북 제작 서비스를 개발했습니다.

2021 데이터청년캠퍼스 고려대 과정 9조 / 박지현 서지혜 이승준 정상희 한유연


#### 이론 공부용 스터디노션: <https://www.notion.so/60eb7f4dc83845b397d2bae416d552f9?v=199c09d2679e4ded8f7fe05845c5a2fd>




## ABC는 두단계를 거처 개인 오디오북을 제작합니다. 

1 단계 - 감성분석 단계 : BERT

2 단계 - 음성합성 단계 : TACOTRON2 + Waveglow

![슬라이드15](https://user-images.githubusercontent.com/78553384/131202212-62802bc7-e3ce-44e0-bfc2-63c929e376aa.PNG)

사용자의 음성으로 추가 학습된 모델에 동화책 대본을 input으로 넣어주면 BERT 모델이 문장 별로 감정 태깅을 하고 그 텍스트를 Tacotron2 모델에 넣어 Mel-spectrogram을 생성해줍니다. 

그 Mel-Spectrogram을 waveglow에 주면 ‘감정이 들어간 사용자의 목소리로 들려주는 동화책’ 즉 저희 모델의 최종 output이 생성됩니다. 



#### 학습 전 모노톤하고 감정이 없는 AI voice: 

https://user-images.githubusercontent.com/78553384/131202589-345a624f-0566-48a1-8b77-d93325925abf.mov



#### 학습 후 감정이 들어간 박지현의 목소리:

https://user-images.githubusercontent.com/78553384/131202586-e8a442e2-d2b9-47b2-bf79-e7d212e6af4b.mov







