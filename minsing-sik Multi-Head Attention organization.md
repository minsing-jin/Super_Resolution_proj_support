# Minsing-sik Multi-head attention 정리

## 결론
##### multi-head self attention
![image](https://user-images.githubusercontent.com/60510718/178751619-28f6574a-efa5-40a6-978c-3c816fe83f5c.png)

multi-head self attention은 single-head self attention을 여러개 이용하는것으로, 하나의 attention value를 이용하는 대신 여러 개의 attention value를 이용하면 서로다른 subspace에 있는 representation을 추출할 수 있을 것이라는 아이디어를 직접 구현한것이다. 
여러개의 attention을 사용함으로써 transformer에서 강조하는 GPU를 통한 연산속도를 높이고자 한것이다.



참고:https://tigris-data-science.tistory.com/entry/%EC%B0%A8%EA%B7%BC%EC%B0%A8%EA%B7%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EB%8A%94-Transformer3-Multi-Head-Attention%EA%B3%BC-Encoder




이미지 처리 분야에서 attention 활용

## 선행지식(prior knowledge)
### 1. Attention이란 무엇인가

잘 이해가 되지 않는다면 아래 SEQ2SEQ model참고
```

```


### 2. SEQ2SEQ model
* structure

![image](https://user-images.githubusercontent.com/60510718/178134568-aaab9f67-69dd-4f32-943c-4314e0db3406.png)
```
인코더와 디코더라는 두개의 RNN 아키텍처로 구성된 모듈로 I am a student라는 입력
문장들을 압축해서 하나의 백터(context vector)로 만든후 디코더에서 번역된 단어를
순차적으로 출력
```
![image](https://user-images.githubusercontent.com/60510718/178134643-f9cf6a0d-8f9a-4aa1-84a4-b1092b33c32f.png)
```
인코더 아키텍처랑 디코더 아키텍처는 LSTM셀 또는 GPU 셀로 이루어져 있다. 입력 문장은
단어 토큰화를 통해서 단어 단위로 쪼개고 단어 토큰은 각각 RNN 셀의 각 시점에 입력된다.
인코더 RNN셀의 마지막 시점의 hidden layer를 디코더 RNN셀로 넘겨주는데 이걸 context
vector라고 불림. 

```

```
디코더는 기본적으로 다음에 올 단어를 예측하고, 그 예측한 단어를 다음 시점의 RNN 셀의 입력으로 넣는 행위를 반복합니다. 이 행위는 문장의 끝을 의미하는 심볼인 <eos>가 다음 단어로 예측될 때까지 반복된다. 지금 설명하는 것은 테스트 과정 동안의 이야기이다. 조금더 자세한 설명은 아래 링크를 참고해주십셔
```
링크: https://wikidocs.net/24996

#### 어텐션 메커니즘
![image](https://user-images.githubusercontent.com/60510718/178749382-4b9bc2d5-b129-4b3f-b182-e7a33bdea464.png)
```
어텐션 함수를 표현하면 다음과 같다.
Attention(Q, K, V) = Attention Value

어텐션 함수는 주어진 Query에 대해서 모든 key의 유사도를 각각 구한다. 그리고 이 유사도를 키와 맵핑되어있는 각각의 value에 반영해준다. 그리고 유사도에 반영된 value를 모두 더해 attention value를 리턴한다.
```
즉 어텐션을 통해서 그냥 rnn에서 다음단어를 예측할거 중요도를 attention value로 정한다음에 그 value를 예측에 참고자료로 사용하여 정확도를 높이는것이다. 이는 이미지 super resolution의 원리로도 사용된다.
->좀더 리서치하기 


여기서 보는 seq2seq + 어텐션 모델에서 Q, K, V에 해당되는 각각의 query, keys, values는 각각 다음과 같다.
```
Q = Query : t 시점의 디코더 셀에서의 은닉 상태
K = Keys : 모든 시점의 인코더 셀의 은닉 상태들
V = Values : 모든 시점의 인코더 셀의 은닉 상태들
```
수식의 차이로 다양한 attention종류가 있으며 우리가 여기서 알아볼것은 super resolution에 관련된 Multi-head self-attention(이하 MHSA)기법과 multi-head cross-attention(이하 MHCA)를 알아볼것이다.


### 2. 용어 설명
```
1. embedding이란?
   NLP에서 embedding은 사람이 쓰는 자연어를 기계가 이해할 수 있는 숫자 형태인 
   vector로 바꾼 결과/ 일련의 과정 전체
   
2. NLP(Natural Language Processing)
   자연어 처리
   
3. LSTM(Long short term memory)
   장기/단기 기억을 가능하게 설계한 신경망 구조. 기존 RNN이 출력과 먼위치에 
   있는 정보를 기억할 수 없고, 장기간의 패턴을 학습하는데에 제한되는 단점 보완 
   자세한 설명은 아래 설명 참조
```
Reference: http://www.incodom.kr/LSTM



https://gist.github.com/ihoneymon/652be052a0727ad59601

https://www.grainpowder.net/posts/dl/nlp/vaswani2017/
https://wikidocs.net/22893
https://tigris-data-science.tistory.com/entry/%EC%B0%A8%EA%B7%BC%EC%B0%A8%EA%B7%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EB%8A%94-Transformer3-Multi-Head-Attention%EA%B3%BC-Encoder
