# Minsing-sik Multi-head attention 정리

## 결론
##### multi-head attention

이미지 처리 분야에서 attention 활용

## 선행지식(prior knowledge)
```
### 1. Attention이란 무엇인가

### 2. SEQ2SEQ model
* structure
![image](https://user-images.githubusercontent.com/60510718/178134568-aaab9f67-69dd-4f32-943c-4314e0db3406.png)

인코더와 디코더라는 두개의 RNN 아키텍처로 구성된 모듈로 I am a student라는 입력
문장들을 압축해서 하나의 백터(context vector)로 만든후 디코더에서 번역된 단어를
순차적으로 출력

![image](https://user-images.githubusercontent.com/60510718/178134643-f9cf6a0d-8f9a-4aa1-84a4-b1092b33c32f.png)

인코더 아키텍처랑 디코더 아키텍처는 LSTM셀 또는 GPU 셀로 이루어져 있다. 입력 문장은
단어 토큰화를 통해서 단어 단위로 쪼개고 단어 토큰은 각각 RNN 셀의 각 시점에 입력된다.
인코더 RNN셀의 마지막 시점의 hidden layer를 디코더 RNN셀로 넘겨주는데 이걸 context
vector라고 불림. 

```
#### 어텐션 메커니즘


### 2. 용어 설명
```
1. embedding이란?<br>
   NLP에서 embedding은 사람이 쓰는 자연어를 기계가 이해할 수 있는 숫자 형태인 
   vector로 바꾼 결과/ 일련의 과정 전체<br>
   
2. NLP(Natural Language Processing)
   자연어 처리
   
3. LSTM(Long short term memory)
   장기/단기 기억을 가능하게 설계한 신경망 구조. 기존 RNN이 출력과 먼위치에 
   있는 정보를 기억할 수 없고, 장기간의 패턴을 학습하는데에 제한되는 단점 보완 
   자세한 설명은 아래 설명 참조
```
Reference: http://www.incodom.kr/LSTM




https://wikidocs.net/22893
https://www.grainpowder.net/posts/dl/nlp/vaswani2017/
https://gist.github.com/ihoneymon/652be052a0727ad59601
https://gist.github.com/ihoneymon/652be052a0727ad59601
https://heung-bae-lee.github.io/2020/01/16/NLP_01/
https://wikidocs.net/24996
https://wikidocs.net/22886
