# Final Outputs

Data Collection과 Model training 폴더에도 있지만, 좀 더 원활한 비교를 위해 별도의 폴더에 저장
- /jvoice : 지현님 목소리가 녹음된 원본 wav 파일 (22050Hz, 16bit, mono channel)
- /redhat_nes : 기존 tacotron2 모델의 체크포인트에서 빨간모자 텍스트->오디오를 생성한 inference
- /redhat_infernces : 지현님 목소리로 16500 iteration 추가 학습 후 빨간모자 텍스트를 감정을 실어 읽은 오디오 모음집

## 추후 발전사항
음성 녹음과 휴대의 간편성 측면에서 서비스를 모바일 어플리케이션으로 구현하는 것

![앱개발](https://user-images.githubusercontent.com/80621384/131204446-824b1348-984c-40df-b37c-a47fbd69dfc7.jpg)

1. 사용자의 목소리 학습을 위해 한시간 분량의 음성 파일을 입력받기 - 동화책 두 세권 분량의 텍스트를 제공
2. 해당 텍스트를 BERT 모델로 eval - 감정 태깅
3. Tacotron2 모델의 추가 학습과 동화책 오디오 파일 생성
4. 오디오 파일 concat 및 다른 여러 동화책 텍스트에도 적용
