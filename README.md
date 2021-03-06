# 아이들을 위한 ABC 오디오북 제작 시스템

### 자연어 감성분석 기술과 음성합성 기술을 융합한 개인 오디오북 제작 시스템

2021 데이터청년캠퍼스 고려대 과정 9조 / *박지현 서지혜 이승준 정상희 한유연*

![대문사진](https://user-images.githubusercontent.com/80621384/131204004-52bf70e7-863c-48b4-9390-de87ac98a954.jpg)



- 이론 공부용 스터디노션: check this [link](https://www.notion.so/60eb7f4dc83845b397d2bae416d552f9?v=199c09d2679e4ded8f7fe05845c5a2fd)




## 개인 오디오북 제작 시스템 과정 

ABC는 두단계를 거처 개인 오디오북을 제작합니다. 

**1 단계 - 감성분석 단계 : BERT**

**2 단계 - 음성합성 단계 : TACOTRON2 + Waveglow**

![슬라이드15](https://user-images.githubusercontent.com/78553384/131202212-62802bc7-e3ce-44e0-bfc2-63c929e376aa.PNG)

사용자의 음성으로 추가 학습된 모델에 동화책 대본을 input으로 넣어주면 BERT 모델이 문장 별로 감정 태깅을 하고 그 텍스트를 Tacotron2 모델에 넣어 Mel-spectrogram을 생성해줍니다. 

그 Mel-Spectrogram을 waveglow에 주면 ‘감정이 들어간 사용자의 목소리로 들려주는 동화책’ 즉 저희 모델의 최종 output이 생성됩니다. 


아래 빨간 모자 동화책 텍스트를 저희 ABC ( 개인 오디오북 제작 시스템 ) 에 시연해봤습니다. 

먼저, 박지현의 목소리가 학습되기전 AI 목소리와 학습한 후 감정이 들어간 박지현의 목소리는 다음과 같습니다.


## 모델 시연
- Input : 빨간모자 동화책 텍스트 파일, 박지현의 목소리 wav 파일

- Output : 박지현이 감정을 담아 읽은 빨간모자 동화 음성

#### 학습 전 모노톤하고 감정이 없는 AI voice: 

https://user-images.githubusercontent.com/78553384/131202589-345a624f-0566-48a1-8b77-d93325925abf.mov



#### 학습 후 감정이 실리고, 박지현의 목소리를 모사한 AI voice:

https://user-images.githubusercontent.com/78553384/131202586-e8a442e2-d2b9-47b2-bf79-e7d212e6af4b.mov


**빨간모자 텍스트 =**

> 옛날 옛날에 모두의 사랑을 받는 작고 귀여운 소녀가 있었습니다. 하지만 그 소녀를 가장 사랑하는 것은 그녀의 할머니였습니다. 할머니는 소녀에게 무엇을 줘야 할지 몰랐습니다. 한번은 할머니가 소녀에게 붉은 벨벳으로 만들어진 모자를 선물했습니다. 소녀에게 그 모자가 잘 어울렸고, 소녀가 그 모자가 아닌 다른 것은 쓰지 않으려고 했습니다. 그래서 그 소녀는 '빨간 모자'라고 불렸습니다. 어느 날, 소녀의 엄마가 그녀에게 말했습니다. "빨간 모자, 여기로 와보렴. 여기 케이크 한 조각과 와인 한 병을 할머니에게 가져다 주렴. 할머니가 편찮으시니까 네가 가면 기뻐하실 거야. 더워지기 전에 출발하렴. 그리고 할머니 댁에 갈 때, 조심해서 가고 길에서 벗어나지 마렴. 그렇지 않으면 네가 넘어져서 병을 깨뜨릴 거야. 그러면 할머니는 아무것도 받지 못하신단다. 그리고 할머니 방에 가면, 먼저 인사하고 방 안 구석구석을 살펴보는 것을 잊지 말아라!"

....

> 이 이야기도 말해야 합니다. 빨간 모자가 할머니께 다시 케이크를 드리러 갈 때, 또 다른 늑대가 와서 빨간 모자에게 말을 시키고 빨간 모자가 길에서 벗어나게 하려고 했습니다. 하지만 빨간 모자는 늑대를 경계하며 바로 할머니 댁으로 갔습니다. 빨간 모자가 할머니께 자기에게 인사를 했지만 자기를 째려보는 늑대를 만났다고 말했습니다. "내가 사람들이 있는 거리에 있지 않았다면, 늑대가 나를 잡아먹었을 거에요." – "이리 와라" 할머니가 말씀하셨습니다. "우리 늑대가 들어오지 못하게 문을 닫자." 곧 늑대가 와서 문을 두드리며 말했습니다. "할머니, 문 열어주세요. 저에요, 빨간 모자. 제가 할머니께 케이크를 드리러 왔어요." 하지만 할머니는 아무 말도 하지 않고 문을 열어주지 않았습니다. 그랬더니 그 나쁜 늑대가 계속 할머니 집 주위를 걸어 다니더니 마침내 지붕 위로 뛰어 올랐습니다. 늑대는 빨간 모자가 저녁에 집에 갈 때까지 기다려 빨간 모자를 따라가서 어둠 속에서 몰래 잡아먹으려고 했습니다. 하지만 할머니는 늑대가 무엇을 하려고 하는지 알았습니다. 집 앞에 큰 양동이가 있었습니다. 할머니는 빨간 모자에게 말했습니다. "빨간 모자야, 저기서 양동이를 가져와라. 내가 어제 거기에 소시지를 구웠다. 그 양동이에 물을 부어라!" 빨간 모자는 양동이가 완전히 찰 때까지 물을 채웠습니다. 그래서 소시지 냄새가 늑대의 코까지 올라갔습니다. 늑대는 냄새를 맡고 아래를 내려봤습니다. 결국 늑대가 너무 목을 아래로 내린 나머지, 스스로 지탱할 수 없어서 아래로 떨어졌습니다. 늑대는 굴뚝으로 미끄러져 내려와 양동이에 빠져 죽었습니다. 그리고 빨간 모자는 행복하고 안전하게 집에 돌아왔습니다.
