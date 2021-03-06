# [Mastering Transformers](https://www.packtpub.com/product/mastering-transformers/9781801077651) 요약
저자 : Savaş Yıldırım, Meysam Asgari-Chenaghlu  
출간일 : 2021/09  (packt publishing)

![책표지](./book_img.jpg)
---

# 챕터별 분류
이 책은 크게 아래로 분류된다  

## 섹션 1: 도입부 (Introduction)
1장부터 2장까지는 도입부이다. 도입부는 다음과 같은 주제를 다룬다\
1. NLP분야의 역사
1. transformers 라이브러리의 설치 후 기본적인 사용방법

### 1장. NLP의 역사 (From Bag-of-Words to the Transformer)
딥러닝 이전 시대부터 트랜스포머까지의 NLP의 역사를 짚어본다
### 2장. introduction (A Hands-On Introduction to the Subject)
transformers 라이브러리의 실습환경 구축 및 기본 사용법을 소개한다

## 섹션 2: 트랜스포머 모델들 소개 (Transformer Models)
From Autoencoding to Autoregressive Models
### 3장. 오토인코딩 모델들 소개 (Autoencoding Language Models)
BERT등의 트랜스포머의 인코더 모델들을 소개한다
### 4장. 디코더 (Autoregressive and Other Language Models)
GPT-1등의 트랜스포머의 디코더 모델들을 소개한다
### 5장. 분류를 위한 파인튠 (fine-tune for classifier)
제목 그대로 분류를 위한 파인튠 방법을 소개한다
### 6장. 토큰 분류를 위한 파인튠 (fine-tune for token classification)
제목 그대로 토큰 분류를 위한 파인튠 방법을 소개한다
### 7장. text representation (워드 임베딩 or 문장 임베딩)
다양한 모델을 사용하여 문장을 표현하는 여러가지 기법을 배운다. 다음과 같은 내용을 다룬다
1. Universal Sentence Encoder (USE) 모델
1. Siamese BERT (Sentence-BERT) 모델
1. BART모델을 사용한 제로샷 학습에 대해 다룬다
1. Few-shot 학습 방법론

## 섹션 3: 심화 주제 (Advanced Topics)
### 8장. 효율적인 트랜스포머 (Working with Efficient Transformers)
빠르고 효율적인 모델을 만드는 테크닉을 소개한다
### 9장. 다른 언어간 번역모델 (Cross-Lingual and Multilingual Language Modeling)
지금까지는 단일 언어에 대한 문제만을 다루었지만 이번 장에서는 서로 다른 언어간 번역 기능을 제공하는 mT5, mBART등의 모델에 대해 살펴본다
### 10장. 트랜스포머를 웹 API로 사용하기 (Serving Transformer Models)
FastAPI등의 서버를 사용하여 트랜스포머 모델을 REST API로 제공하는 기법 등을 소개한다
### 11장. 어텐션 시각화 & 실험적 트래킹 (Attention Visualization and Experiment Tracking)
어텐션을 시각화하여 성능개선 등에 참고하는 기법을 소개한다

---

# 소챕터별 분류
# 1장. NLP의 역사 (From Bag-of-Words to the Transformer)

## 1.1 transformers 까지의 역사 (이론중심으로 설명)

아키텍처와 아키텍처들의 변화는 다음 기술들의 진보로 성공적이었다  
1. 문맥적 워드 임베딩 (BERT등에서 사용한다)
1. 더나은 서브워드 토큰화 알고리즘 (BERT의 토크나이저인 Wordpiece tokenizer.)
1. 입력 토큰을 문장단위로 분리하는 기법 (예 BERT의 CLS토큰 등. 이를 메모리 토큰이라고 한다)
1. 입력 문장의 모든 정보를 같은 우선순위로 두고 디코딩하는 문제 (어텐션 메커니즘으로 해결 )
1. 멀티헤드 셀프 어텐션
1. 포지셔널 인코딩
1. 더 빠른 훈련을 위한 병렬 아키텍처
1. 모델 압축 (distillation, quantization 등)
1. 전이학습 (Transfer Learning)  

기존의 전통적인 모델은 sparsity, unseen words representation,
tracking long-term dependencies 등의 문제가 있었다. 이러한 문제의 대응으로 딥러닝 기반의 접근법이 고안되었다.  
2013년은 word2vec이 등장하여 차원문제를 해결하려 하였다. word2vec은 워드 임베딩이라는 개념을 도입하였다.  
재귀(recurrent) 및 컨볼루션 아키텍처는 인코더와 디코더로 사용되었다. 인코더 및 디코더는 sequence to sequence 문제를 해결하려 고안되었다. 이 초기모델들의 문제점은 다의어의 여러가지 뜻을 해결하지 못하는 문제가 있었다.  뒤이어 고안된 Universal Language Model Finetuning
(ULMFit) and Embeddings from Language Models (ELMo) 등의 모델은 단어를 문장 수준의 정보로 인코딩하여 다의어 문제를 어느정도 해결하였다. 이는 기존의 정적 워드 임베딩에서 한단계 진보된 형태였다. 이들 두 모델은 RNN이 진보된 LSTM 모델 기반이었다. 이 모델은 pre-train과 fine-tune의 개념을 도입하였다. 이 모델은 전통적인 워드 임베딩과 다르게 단어의 뜻을 표현하였는데 이 모델에서는 문장내의 단어가 입력문장 전체의 맥락을 고려하여 임베딩된다. 이것을 문맥적 임베딩이라고 한다.  
그리고 2015년 어텐션 메커니즘이 소개되었다.  
2년후 2017년 트랜스포머 기반의 인코더-디코더 모델이 발표되었다. 이 모델은 기존의 재귀(recurrent) 모델을 버리고 어텐션 메커니즘만을 차용하였다.  

## 1.2 분산 시멘틱스(distributional semantics) 이해하기
분산 시멘틱스는 `단어의 의미를 벡터로 표현하는 수단`이다.  분산 시멘틱스의 구체적인 예로는 워드 임베딩이 있다.  
이 접근법은 사전에 정의된 의미를 찾기보다는 분산적 증거를 찾는것을 선호한다. 분산적 증거라는 말이 어려울 수 있지만 비슷한 위치에 존재하는 단어들은 뜻이 유사할 가능성이 높다는 뜻이다. 같은 문맥에서 함께 등장하는 한쌍의 단어들은 유사한 뜻인 경향이 있다는 것을 암시한다. 일례로 `개`와 `고양이`는 같은 문맥에서 함께 등장할 가능성이 높으므로 유사한 뜻으로 간주된다. 단어는 시간이 흐르거나 도메인이 바뀌면 그 의미가 바뀔 수 있는데 이를 `lexical semantic change problem`이라고 한다. `분산 시멘틱스 (distributional semantics)`는 이러한 문제를 이해하는데 도움을 준다.
고전적인 방법으로 `Bag-of-Words (BoW)`와 `n-gram`이 단어를 표현하는데 사용되었다. BoW에서는 단어와 문장들이 `one-hot 인코딩`으로 표현되었다. `n-gram` 모델은 문장을 구성하는 각각의 단어에 확률을 부여한다. 그래서 이 문장이 코퍼스 내에 속할 확률을 구하거나 랜덤한 문장을 생성하는데 쓰였다.  
### 1.2.1 bag of word
bag of word는 워드 임베딩이다. 워드 임베딩이란 단어에 숫자를 레이블링하는 작업이다.  
워드 임베딩의 단점 : 단어와 단어간에 아무런 관계도 부여되지 않는다. 따라서 단어가 어떤 맥락에서 사용되었는지 알수없다  
워드 임베딩을 개선하여 단어와 단어간에 맥락(context)을 부여하는 방법이 고안되었다  

### 1.2.2 차원 문제를 극복하기
차원 문제를 해결하기 위해 `Latent Semantic Analysis(LSA)`가 사용된다. 이는 저차원 벡터 공간에서 단어의 의미를 파악하는데 쓰인다. LSA기반의 확률모델은 단일 레이어로서 사용을 고려해볼만 하지만 최근의 딥러닝(DL) 모델은 다중 레이어 기반이다.

###	1.2.3 언어 모델과 언어 모델의 생성
기존의 언어 생성 모델은 `n-gram`기반의 모델을 기반으로 했다. 문장을 이루는 각 단어는 이전 단어의 클러스터에 기반하여 생성된다. unigram , bigram, ngram 등이 있다
이후 n-gram을 실습함  

## 1.3 레버리징 딥러닝(DL)
NLP역사를 돌아보며 지금까지의 여러 접근법을 배워본다  

### 1.3.1 워드 임베딩과 word2vec(2013)
`Word2vec` 은 가장 널리 알려진 워드임베딩 솔루션이다.
word2vec은 단어와 단어 사이에 맥락(context)을 부여한다.  
예를 들어 `학교`라는 단어가 있으면 그 단어에 대한 배열을 생성해서 그 단어와 인접한 단어를 순서대로 삽입한다. 예를들어 `['공부', '학생', '선생님', '시험']` 와 같은 배열이 생성된다  

word2vec의 단점은 오직 맥락에 의해서만 단어의 쓰임새를 유추하는데서 온다
예를 들어
```
나는 학교에 갔다  
나는 거기에 갔다  
```
`학교에`와 `거기에`는 정확히 같은 맥락에서 사용되었다. 따라서 이들 두 단어는 유사한 단어로 정의된다. 그러나 실제로 이들 두 단어는 유사한 단어가 아니다.  

또다른 문제로는 동음 이의어를 구분하지 못하는데 있다  
`나는 말을 보며 말을 했다.`  
위와 같은 문장에서 첫번째 말은 horse이고 두번째 말은 speech이지만 word2vec은 동음이의어를 구분하지 못한다  

이런 문제를 해결하려면 `단어 수준의 이해`를 `문장 단위의 이해`로 업그레이드 해야한다  
이 문장 수준의 시도한게 `RNN`이다. `RNN`이 업그레이드 되어 `LSTM`이 되었고 `LSTM`이 개선되어 `transformer` 모델이 되었다  

word2vec은 sklearn라이브러리가 제공하는 `Principal Component Analysis (PCA)` 를 사용하면 시각화도 가능하다  
이후 Word2vec 실습  

### 1.3.2 RNN
RNN기반의 번역 모델은 `인코더-디코더 기반 모델`이다. 인코더와 디코더를 각각의 함수로 놓고 합성함수를 실행하다고 이해해도 좋다. 먼저 인코더는 입력으로 문장을 구성하는 각 단어를 순차적으로 입력받는다. 각 단어를 입력받을 때 마다 `컨텍스트 벡터`를 생성한다. 이 컨텍스트 벡터는 단어를 입력받을 때 마다 문장의 정보를 갱신한 채로 수정된다. 문장의 마지막 단어까지 입력받으면 최종적인 컨텍스트 벡터(context vector)가 완성된다. 이 컨텍스트 벡터는 입력 문장의 처음부터 끝까지 모든 컨텍스트 정보를 벡터로 표현한 자료구조이다. 디코더는 이 컨텍스트 벡터를 입력으로 받아 입력에 대응되는 단어를 하나씩 생성하여 최종적으로 하나의 문장을 생성한다. 컨텍스트 벡터는 인코더와 디코더 사이에 위치하기 때문에 이를 `중간 표현값(intermediate representation)`이라고 부른다.
디코더가 문장을 생성할 때는 1개 단어씩 순차적으로 생성하는데 이 작업은 end 토큰을 만날때 까지 반복된다. 하지만 이런 메커니즘에는 문제가 있다. 컨텍스트 벡터를 갱신할 때마다 초기에 입력받은 단어의 정보가 점차 소실되어 정보가 유실될수도 있다는 점이다. 따라서 RNN기반의 인코더는 `긴 문장이 입력으로 들어왔을 때 상당량의 정보가 소실되는 문제`가 있다.  
두번째 문제, 컨텍스트 벡터는 처음부터 고정된 사이즈이다. 입력의 길이를 예측할 수 없는 상황에서 고정 사이즈의 배열을 활용한다는 건 최적화에 문제가 있다.  

###### 어텐션은 어떻게 이 문제를 해결했는가 ?
하나의 컨텍스트 벡터만을 사용하는 것이 아니라 각 단어가 입력으로 들어갈 때 마다 생성되는 모든 컨텍스트 벡터를 사용하는 것이다. 이렇게 되면 각 단어의 정보가 소실되지 않은 상황, 다시말해 단어의 컨텍스트 정보가 전혀 소실되지 않은 컨텍스트 벡터와 전체적인 문장의 컨텍스트 정보를 동시에 참고하여 문장을 생성할 수 있다. 즉 입력 단어가 3개라면 중간과정에 생성되는 컨텍스트 벡터와 최종적으로 생성되는 벡터를 합쳐 총 3가지의 벡터가 생성된다. 이 3가지의 정보를 모두 다 이용하여 문장을 생성하는 것이 어텐션 메커니즘이다. 어텐션의 대략적인 공식은 다음과 같다
`어떤함수(생성된 모든 컨텍스트 벡터) + 어떤함수(가장 최근에 생성된 컨텍스트 벡터)`
이 어텐션은 fully-connected neural network에서 작동하며 최종 레이어에서는 입력단어의 갯수만큼의 weight를 출력한다. 이 최종 레이어의 weight들에 softmax함수를 적용하면 모든 weight의 총합이 1이 되는 확률분포가 생성된다. 이 weight를 어텐션 weight라고 부른다. 이 어텐션 weight는 입력 단어들 중 어느 단어에 비중을 두어야 하는지에 대한 정보를 담고 있다. 이 어텐션 weight의 정보를 활용하여 최종적으로 단어 생성에 사용할 컨텍스트 벡터를 생성한다. 이 최종 생성된 컨텍스트 벡터를 입력으로 단어를 생성한다.

상세 내용은 유튜브 강의 (https://www.youtube.com/watch?v=WsQLdu2JMgI) 를 참조할 것  

### 1.3.3 LSTM & GRU
LSTM (long-short term memory)는 이름처럼 기억과 관련한 솔루션이다. 긴 문장 내에서 초기에 등장한 단어의 정보가 점차 소실되는 `long-term dependency problem`을 해결하기 위해 고안되었다. 정보의 보존을 위해 `cell state`라는 개념을 도입하였다. 셀은 상태를 저장하는데 이 상태에 어떤 형태의 정보를 담을지 또는 어떤 형태의 정보를 제거할지가 LSTM알고리즘에 의해 자체적으로 결정된다.  
### 1.3.4 LSTM 구현하기
LSTM을 tf, keras를 통해 구현한다  
### 1.3.5 CNN 오버뷰
cnn의 개념을 설명하고 keras로 cnn을 구현한다  

## 1.4 트랜스포머 아키텍처
트랜스포머는 대부분의 NLP문제를 처리할 수 있는 딥러닝 아키텍처다. 트랜스포머의 핵심은 병렬화이다. 트랜스포머는 recurrent모델을 사용하지 않으며 문장의 모든 단어를 한번에 병렬로 인코딩한다  
트랜스포머의 또다른 핵심은 어텐션 메카니즘이다. 트랜스 포머 이전에도 어텐션은 존재했다. 과거 LSTM모델에서 어텐션은 성능 향상을 위한 옵션으로 존재했지만 트랜스포머에서는 어텐션이 핵심 메커니즘이다.

### 1.4.1 어텐션  
어텐션은 2015년 Bahdanau등에 의해 제안되었다. LSTM기반의 인코더-디코더 모델은 먼저 인코더가 문장을 재귀(recurrent) 기반으로 처리하여 컨텍스트 벡터를 생성한다. 처리가 끝나면 최종적으로 하나의 컨텍스트 벡터가 생성되는데 이 컨텍스트 벡터가 다른 재귀유닛(recurrent unit)인 디코더의 입력으로 들어간다. 이처럼 문장의 모든 정보를 소비한 후에 다시 롤링아웃하는 과정은 디코더에게 버거웠다 왜냐하면 디코더는 문장에 관련한 모든 의존성들을 볼 수 없기 때문이고 `오직 최종 생성된 컨텍스트 벡터만을 입력으로서 참조`하기 때문이다.
이 문제를 해결하려 어텐션이 고안되었는데 어텐션에서는 재귀(recurrent) 프로세싱 중간에 생성된 모든 컨텍스트 벡터를 별도의 스테이트로 저장한 후에 이 모든 스테이트가 디코더에 입력된다.
어텐션의 등장 이후 많은 변종들이 생겨났고 그중에서도 트랜스포머는 `멀티헤드 어텐션 (multi-head attention mechanism)`을 사용한다.

문장내 단어간 관계를 학습하는 모델을 `self-attention`이라고 한다  
word2vec과 마찬가지로 문장내 인접한 단어끼리 관계도가 높다  
transformers는 문장 전체에 대한 배열을 만든다. 배열은 N차원 좌표평면상의 특정 좌표를    의미한다. 이 문장의 배열에는 특정 단어의 좌표는 포함되어 있지 않다.  
이 과정을 language model이라고 한다. 여기까지의 작업이 pre-train이다.  
그리고 이 language model을 가져와서 sentiment analysis를 하거나 언어 번역을 하고싶을때는 fine-tuning으로 테스크에 특성화된 작업을 수행한다.  
이 일련의 과정을 합쳐서  transfer learning, 한국어로 전이 학습이라고 한다.  이 과정을 여러번 반복해서 평균을 내기 때문에 ‘multi’라는 단어를 붙여서 `multi-head selt-attention`이라고 한다



### 1.4.2 멀티헤드 어텐션 (Multi-head attention)
멀티헤드의 이해에 앞서 `셀프 어텐션(self-attention, 다른말로 dot-product attention)`을 알아보자. 셀프 어텐션의 핵심은 어텐션 스코어를 입력 문장에 의존해서 `스스로(self)` 생성해서 활용한다는 점이다. 어텐션 스코어란 현재 시점에서 디코더의 상태와 가장 유사한 상태를 인코더의 히든스테이트 중에서 구한다는 개념이다.

셀프 어텐션에서는 각각의 히든스테이트 별로 어텐션 스코어를 구해놓고 이것들을 하나의 벡터로 관리한다. 이 벡터에 소프트맥스 함수를 적용하면 총값이 1이 되는 확률 분포가 생성된다. 이를 `어텐션 분포(Attention Distribution)`라고 하고 각각의 값은 `어텐션 가중치(Attention Weight)`라고 한다. 이 어텐션 가중치들을 (각각에 대응되는 히든스테이트와 곱해서) 모두 더하면, 즉 시그마 연산을 하면 `어텐션 값(Attention Value)` 다른말로 컨텍스트 벡터가 생성된다. 이 컨텍스트 벡터를 가장 최근의 스테이트(latest state)와 결합하여 하나의 벡터를 만든다. 이 최종 연산된 벡터가 디코더의 입력으로 들어가 단어를 출력한다.  

dot-product attention에서의 어텐션 스코어는 Query 행렬과 Key 행렬의 내적(dot-product)을 하여 구한다. 그래서 이름이 `dot-product attention`이다. 이 결과물은 정사각 행렬이다. 이 어텐션 스코어를 입력 문장과 행렬곱을 하여 어텐션 메커니즘의 최종 결과값을 구한다

이와같은 dot-product attention에 scaling을 추가한게 scaled dot-product attention이다.
이 scaled dot-product attention를 병렬로 여러번 실행하여 나온 결과물들을 더하는게 멀티헤드 어텐션이다.

그 외 핵심개념 : positional encoding. 이는 입력값에 사인과 코사인을 적용하여 구한다

#### 1.4.3 인코더 & 디코더
인코더는 양방향(bi-directional) 토큰을 이용해서 중간에 위치한 토큰을 생성한다. 이를 양방향 트랜스포머라고 한다.  
디코더는 한쪽방향 토큰을 이용해서 다음 토큰을 생성하는 생성자이다  

## 1.5 전이학습(tranfer learning, TL)을 트랜스포머와 같이쓰기  
전이학습은 pre-trained model이라고도 불린다.  
전이학습은 shallow model과 deep model로 나뉜다. shallow TL의 예로는 Word2vec이 있다.
얕은 모델(shallow model)은 pre-trained vector 기반이다.  이러한 종류의 전이학습 뒤에는 아무런 모델이 없기 때문에 얕은 모델이라고 불린다. 모델 대신 pre-trained 벡터가 활용된다.
deep model은 language model이다.  
트랜스포머는 비지도 학습 기반으로 전이학습이 가능하다. 마스크 언어 모델(Masked Language Model) 을 활용하면 언어 그자체가 스스로 학습이 가능하다. 특정한 단어를 공백으로 바꾸어 놓고 이 단어를 예측하는 방식으로 학습이 진행된다
트랜스포머를 활용한 최초의 언어 모델은 BERT이다. 이는 트랜스포머의 인코더 파트를 기반으로 한다. BERT는 마스크 언어 모델을 기반으로 스스로 학습한다. 바트는 전이 가능한 언어모델이므로 한번 학습해 놓으면 토큰 분류, Q&A, 문장 분류등 다양한 필드에 적용할 수 있다.  
BERT의 학습에는 2가지 문장이 동시에 입력된다. 이는 다음 문장 예측을 학습하기 위함이다. 이는 문장과 문장관의 관계를 학습함으로서 이루어진다.  
`주의 ! : BERT와 BART는 다른 개념이다. BERT는 인코더 모델이며 BART는 인코더와 디코더가 결합된 seq2seq 모델이다`  

# 2장. introduction (실습환경 구축 및 기본 사용법 소개)
## 2.1 아나콘다와 transformers 설치
읽지 않음  

### 2.1.1 colab에서 설치하는 방법
`!pip install Transformer`

!(느낌표)는 shell에서 실행하도록 해준다. 파이썬에서의 실행이 아니다  

## 2.2 언어모델과 토크나이저 불러오기
transformers 사용법 : 모델함수 안에 인코딩된 토큰을 집어넣으면 끝.  

## 2.3 커뮤니티에서 제공하는 모델 불러오기
결론 : pipeline()함수로 불러오시오  

## 2.4 벤치마킹 함수와 데이터셋 불러오기

## 2.4.1 중요한 벤치마킹 함수  

• GLUE  
• SuperGLUE  
• XTREME  
• XGLUE  
• SQuAD  

### 2.4.2 데이터셋 라이브러리

`pip install dataset`

dataset이란 ? 커뮤니티에서 제공하는 데이터셋을 불러오는 함수.  
예) glue에서 cola라는 데이터를 불러오기  
`the GLUE dataset which is an agregated benchmark comprised of 10 subsets: COLA, SST2, MRPC, QQP, STSB, MNLI, QNLI, RTE, WNLI and the diagnostic subset AX.`  

```
from datasets import load_dataset
cola = load_dataset('glue', 'cola')
cola['train'][25:28]
```

## 2.5 속도 벤치마킹
읽지 않음  

## 2.6 요약
멀티태스킹(GLUE) 및 교차 언어 벤치마킹(XTREME) 을 도입했습니다. 이는 언어모델이 더 강력해지도록 돕는다.  
evaluate 방법을 배웠다. 평가는 연산속도를 기준으로 한다  


# 3장. 오토인코딩 모델들 소개

이번장은 인코더를 트레이닝 하는 방법을 배운다.  
여기서는 단일언어에 대한 학습을 배운다.
이번장은 다음 다섯개를 배운다  
• BERT 모델  
• 모델 학습  
• 커뮤니티에 모델 공유하기  
• 다른 모델들  
• 토큰화 알고리즘 살펴보기  

# 3.1 BERT 모델

BERT를 이해하기 전에 먼저 GPT-1을 이해하는 것이 좋다. BERT는 GPT-1 공개 이후 GPT-1의 단점을 지적하면서 등장했다. 재귀(recurrent)기반 모델인 GPT-1은 `문장을 출력할 때 단방향으로 출력하는 단점`이 있다. 이러한 단방향 접근법은 문맥 이해에 어려움이 있을 수 있다. 그래서 고안된 모델이 `양방향 접근법`이다.
BERT는 최종적으로 컨텍스트 벡터를 생성한다. 이는 기존의 어텐션 메커니즘에서 인코더 모델이 컨텍스트 벡터를 생성한 방식과 유사하다. 다만 이 방식은 RNN처럼 재귀적으로(recurrent) 발생하지 않고 한번에 모든 문장을 읽어들여 컨텍스트 벡터를 생성한다. 컨텍스트 벡터의 생성은 RNN에서의 어텐션 메커니즘과 마찬가지로 fully-connected neural network에서 수행된다. 이 네트워크는 다중레이어 모델이다. 이렇게 생성된 컨텍스트 벡터는 다시 입력으로 들어가 다시 컨텍스트 벡터를 생성하고 이 작업을 문장의 단어갯수 + 1회 만큼 반복한다.

BERT의 핵심 : provide better language modeling. 즉 더나은 fine-tune 학습을 제공한다.  

### 3.1.1 BERT 모델의 pre-train
BERT의 마스크 모델을 제대로 이해하려면 마스크 모델을 왜 사용하는지 알아야 한다\
마스크 모델을 왜 쓰는가 ? 마스크 모델이 cloze 테스트를 성공적으로 수행할 수 있으면 언어의 일반적인 이해가 가능하다고 판단할 수 있기 때문이다.\
cloze 테스트란 문장장에서 특정한 단어를 지워버린 후에 그 지워진 단어에 들어갈 단어를 선택하여 그 선택된 단어가 적합한지 여부를 평가하는 방법이다.\
마스크 모델과 더불어 BERT는 다음 문장 예측 (Next Sentence Prediction, NSP) 작업을 수행하여 학습한다. 이 모델의 학습에는 2개의 입력이 동시에 주어진다. BERT는 두가지 문장을 검사한 후에 두번째 문장이 첫번째 문장의 후속 문장으로 적합한지 여부를 확률로 판단한다. 이 적합성 여부는 두 문장간의 상호 연관성을 측정하여 그 수치값을 기준으로 판단한다
### 3.1.2 BERT 깊이 파보기
BERT는 다음과 같은 특징을 가진다
1. BERT는 WordPiece 토큰화를 기반으로 작동한다.  
1. BERT는 위치적 인코딩(positional encoding)을 사용한다.
1. 시퀀스 분류, 토큰 분류, Q&A 모델 등 문제의 도메인에 따라서 BERT모델의 각기 다른 출력을 사용한다

## 3.2 BERT모델의 학습 실습하기 (Autoencoding language model training for any language)
이번 장에서는 BERT 모델을 이용해 학습하는 과정을 실습한다. 우리는 IMDB 데이터셋에서 감정분석용 영화 리뷰를 가져온 후에 이를 학습할 것이다. 간단한 과정은 다음과 같다
1. 데이터셋을 다운로드한다
1. 토크나이저를 훈련시킨다
1. transformers라이브러리에서 제공하는 trainer클래스를 이용하여 trainer 객체를 생성한다
1. trainer객체의 train메소드를 호출하여 훈련을 시작한다
1. 트레이닝이 종료되면 trainer객체의 save_model 메소드를 이용하여 원하는 이름으로 학습된 모델을 저장한다

## 3.3 리포지토리에 모델 업로드하여 다른사람들과 모델 공유하기
Transformers-cli와 git을 이용하여 리포지토리에 업로드하는 실습을 진행한다  

## 3.4 다른 모델들  
이 장에서는 BERT 모델을 개선한 여러 모델을 소개한다. 모델의 개선은 크게 2가지 파트로 나눌 수 있다.  
첫째는 더 나은 아키텍처이며 또 다른 하나는 pre-train 컨트롤이다
### 3.4.1 ALBERT
대규모 코퍼스를 활용한 모델의 학습은 거대한 메모리 사용량과 오래 걸리는 학습시간이 문제였다.  
Albert (A Lite BERT)는 이러한 문제를 개선하기 위한 BERT의 재구현물이다. BERT대비 18배 더 작은 파라메터로 1.7배 더 빠른 학습이 가능하다.  

ALBERT 모델은 오리지널 BERT대비 다음 3가지 수정사항을 기반으로 한다
• Factorized embedding parameterization (파라메터 갯수 감소용)
• 레이어간 파라메터 공유 (Cross-layer parameter sharing) (파라메터 갯수 감소용)
• Inter-sentence coherence loss
위의 2가지 방법론은 파라메터 갯수를 줄여서 메모리 사용량을 줄인다.\
\
설명이 끝나고 간단한 실습을 수행한다. 이 실습에서는 transformers 라이브러리에서 AlbertTokenizer, AlbertModel를 임포트하여 pre-trained 모델을 불러온다. 그렇게 불러온 모델에 인자로 간단한 영어문장을 입력하고 이에대한 출력이 어떻게 나오는지 확인한다.
### 이 파트는 작성중입니다

### 3.4.2 RoBERTa
RoBERTa (Robustly Optimized BERT pre-training Approach)는 더 나은 pre-train전략을 제공한다.
이후 transformers 라이브러리에서 RobertaTokenizer와 RobertaModel를 불러와서 pre-trained 모델을 이용하여 간단한 실습을 수행한다.


### 3.4.3 ELECTRA (2020)
엘렉트라(ELECTRA)는 BERT에서 파생되었다. 기존의 BERT 모델은 마스크 기반 학습 방법이 비효율적 이었다.\
엘렉트라는 BERT보다 더 빠른 처리속도를 실현했다.\
이후 pipeline 함수로 엘렉트라 제네레이터를 불러오는 매우 간단한 실습을 수행한다\


## 3.5 토크나이징
transformers라이브러리는 BERT모델에 대한 기본 토크나이저로 BertWordPieceTokenizer를 제공한다. 이번 장에서는 토큰화 방법들의 종류와 그 특징을 살펴본다. 일반적인 토큰화 과정은 공백문자 단위로 토큰을 분리하는 접근법을 수행하지만 이는 띄어쓰기가 없는 언어인 일본어 같은 언어에서는 적용할 수 없는 접근 법이다.\
한편 기존의 전통적인 토큰화 방법에서 한단계 진보된 방식이 서브워드 토큰화인데 이는 단어를 더 작은 단어로 분해하는 방식이다. 이렇게 하면 토큰화 대상이 되는 단어가 줄어드는데 이는 두가지 장점이 있다. 첫번째로 워드 임베딩에 사용되는 차원수를 줄일 수 있다. 그리고 학습과정 외에 실제 상황에서 입력받은 단어가 학습때는 본 적이 없는 단어일 가능성이 줄어든다. 미지의 언어가 입력 문장으로 들어오는 현상을(Out-Of-Vocabulary Problem, OOV Problem) 또는 언노운 토큰 문제(Unknown Token Problem) 라고 한다\
transformers 라이브러리에서 사용되는 토큰화 알고리즘은 self-supervised 기반이며 코퍼스에 기반하여 토큰화 룰을 생성한다.\
최근 바이트쌍 인코딩(byte-pair encoding, BPE)이라는 이름의 서브워드 토큰화 알고리즘은 트랜스포머 아키텍처의 일부분이 되었다. 이 `가장 현대적인 토큰화 프로세스`는 두가지 과정으로 분류된다. 첫번째 단계인 pre-tokenization phase는 단순히 공백문자 또는 언어에 기반한 룰을 이용하여 문장을 토큰으로 쪼갠다. 두번째 과정인 tokenization training phase는 토크나이저를 학습하고 그 결과로 기본 단어를 생성한다. 서브워드 토크나이저가 더 작은 단위로 단어를 쪼갤 때 기본 단어를 기준으로 쪼갠다\
이 바이트쌍 인코딩에 기반한 토큰화 알고리즘은 transformers 라이브러리에서 BertTokenizerFast 모듈로 제공된다.

### 3.5.1 바이트쌍 인코딩 (byte-pair encoding)
서브워드 토큰화로 언노운 토큰 문제의 상당수가 해결되었다. 하지만 완전히 문제가 해결된 것은 아니었다. 어떻게 하면 언노운 토큰 문제를 더 개선할 수 있을까?  이는 토크나이저가 이해할 수 있는 베이스 단어를 추가로 늘려주면 해결되는 문제다. 입력으로 주어진 단어들을 조합하여 새로운 단어를 생성하면 이를 달성할 수 있지만 한가지 문제에 봉착한다\
단어를 조합하여 새로운 단어를 만드는 작업은 경우의 수가 거의 무한대로 늘어난다. 이렇게 되면 단어를 담고 있는 워드 임베딩 차원의 수가 증가할 수 밖에 없고 그렇게 되면 메모리 사용량과 학습비용이 늘어난다. 따라서 어떠한 단어가 언노운 워드로 입력될지를 예측하고 그에 맞는 최소한의 단어만 생성하는 전략이 필요하다. 사실 어떠한 단어가 입력으로 들어올지는 확률적 기반에 근거하여 예측하는 것이 가장 합리적이다. 바이트쌍 인코딩 전략은 자주 반복되는 문자를 하나의 쌍으로 묶어 새로운 단어를 생성하는 단순한 전략이다. 이 과정은 n-gram알고리즘에 기반하여 수행된다\
이러한 BPE 토크나이징 방법론은 GPT-2 등의 트랜스포머 모델에서 사용되고 있다.

### 3.5.2 wordPiece 토큰화
워드피스는 BERT, ELECTRA 등에서 사용하는 토큰화 기법이다. 워드피스는 2012년에 나카지마에 의해 고안되었다. 이 솔루션을 제공한 사람이 일본인인 만큼 그는 일본어의 음성 문제를 해결하기 위해 이 토큰화 테크닉을 고안하였다. 많은 아시아 언어에서 단어를 조각화 하는 과정은 어렵다. 일본어처럼 띄어쓰기 자체가 없는 언어도 있고,  띄어쓰기가 있더라도 한국어처럼 잘 지켜지지 않는 경우도 있으며 한국어처럼 은는이가 등의 조사가 붙는경우 그 경우의 수가 너무 많아 일일이 대응하여 토큰화하는 작업은 어렵다. BPE와 유사한 방식으로 워드피스는 대규모 코퍼스를 학습에 이용하고 규칙을 병합한다 (이해가 안됨). BPE가 병합규칙(merging rules)을 학습할 때 co-occurrence 통계에 기반하는 반면 워드피스는 최대가능도 방법(maximum likelihood estimation)에 의존한다

### 3.5.3 Sentence Piece 토큰화
sentence piece 알고리즘은 일본어 등 단어와 단어사이에 공백이 없는 경우에 사용된다. SentencePiece를 사용하는 대표적인 모델로는 XLNet, T5등이 있다.
상세 내용은 [SentencePiece 소개논문](https://arxiv.org/pdf/1808.06226.pdf)을 참조하라
### 3.5.4 토크나이저 라이브러리
허깅페이스 팀은 transformers 라이브러리와는 별개의 토크나이저 라이브러리를 만들었다. 이 모델은 rust로 만들어졌고 랩핑되어 파이썬의 tokenizer 라이브러리로 제공된다
토크나이저의 파이프라인은 총 5스탭으로 이루어진다
1. 정규화 : 알파벳 대문자를 소문자로 바꾸는 등의 정규화 과정을 수행한다
1. pre-tokenizer : 코퍼스를 공백문자 등으로 분리한다.
1. 모델 학습 : BPE등의 서브워드 토큰화 알고리즘을 수행한다
1. 후처리 : 트랜스포머 모델에서 사용할 수 있도록 추가적인 작업이 수행된다. CLS나 SEP토큰을 추가하는 방식으로 이루어진다
1. 디코더 : 디코더는 토큰 아이디를 원래의 문자열로 변환한다. 이는 변환이 제대로 이루어지는지 조사하는 용도로 쓰인다

이후 BPE와 wordpice 토크나이저를 이용한 실습을 수행한다
허깅페이스의 토크나이저 라이브러리에 대한 더 자세한 내용은 [여기](https://huggingface.co/docs/tokenizers/python/latest/)를 참조하라

## 3.6 요약
이번 장은 아래와 같은 내용을 살펴보았다
1. 인코딩 모델을 이론적으로 알아보고 실습을 했다
1. BERT의 기본을 배우고 토크나이저를 훈련했다
1. keras등의 다른 프레임워크와 같이 사용하는 방법을 학습했다
1. BERT의 트레이닝 과정에서 WordPiece 토큰화 알고리즘을 학습했다
1. WordPiece외의 바이트페어 인코딩 등의 기타 다른 토큰화 알고리즘도 살펴보았다.

# 4장. 디코더 (Autoregressive and Other Language Models)
이번장은 트랜스포머에서 디코더 계층으로 사용되는 Auto-regressive (AR)에 대해 다룬다\
AR의 대표적인 예로는 GPT-2모델이 있다\
구체적으로 다루는 내용은 아래의 5가지다  
1. 인코더와 디코더 함께쓰기  
1. seq2seq 모델 사용하기  
1. 인코더 모델을 학습하기  
1. AR모델을 써서 자연어 생성(NLG)하기  
1. simpletransformers 모델을 사용하여 단락요약 테스크 수행하기

## 4.1 AR모델 소개 (Working with AR language models)

### 4.1.1 GPT 모델의 개념과 학습 (Introduction and training models with GPT)
문장을 입력하면 다음 단어를 예측하는데 이때 전체 단어에 대한 확률을 출력하는 모델이 GPT이다.  
이들은 2단계로 나뉜다  
첫단계는 PRE-TRAIN이다. 이는 비지도 pre-train이다.  
두번째는 fine-tune이다. 이는 supervised fine-tune이다. 이는 상대적으로 작은양의 데이터만을 사용한다.  

GPT-2와 GPT-3의 아키텍처는 비슷하다. 다만 파라메터 수가 100배 증가되었다.
GPT-3는 그라디언트 기반의 파인튜닝 없이 pre-train만으로 더나은 결과를 출력했다.

### 4.1.2 Transformer-XL
이 모델은 기존의 트랜스포머 모델들의 입력이 고정길이 기반이라는 문제에서 출발한다. 이들 대부분은 입력을 최대 512개의 세그먼트로 분리하는데 길이가 너무 짦은 탓에 긴 문장의 컨텍스트 정보를 모두 담지 못한다는 태생적 한계를 가진다. 이러한 고정길이 기반의 문장은 절반중 전반을 초반 컨텍스트로 상정하고 절반중 후반을 후반 컨텍스트로 상정하는 불합리한 가정하에 테스크를 수행한다. 다시말해 문장의 바운더리를 합리적으로 생성해 내는 방법이 없는 것이다.\
그래서 어떻게 하면 여러 문장의 컨텍스트 정보를 모두 활용할 수 있을까 고심하여 고안해 낸 것이 재귀(recurrence) 기반의 메커니즘이다. 사실 재귀 기반 메커니즘은 이미 토큰 생성시에 이전 토큰을 참조하는 방식으로 활용하고 있었던 것으로 그렇게 참신한 개념은 아니다. 하지만 이 발상을 조금 더 확대해서 이전에 입력된 문장, 즉 이전에 입력된 세그먼트의 컨텍스트 정보도 참조하는 식으로 개념을 확장한 것이다.\
상세 내용은 더 잘 정리된 [블로그의 기사](http://mlgalaxy.blogspot.com/2019/07/transformer-xl.html)를 참조하라

### 4.1.3 XLNet
마스크 모델은 pre-train단계를 장악했다.\
하지만 마스크된 토큰은 pre-train단계에는 있지만 fine-tune단계에는 없다. 따라서 pre-train과 fine-tune 사이에는 불일치가 존재한다. 이 불일치 때문에 pre-train에서 학습한 모든 정보를 사용할 수 있는 것은 아니다.
이러한 문제점 때문에 XLNet은 기존의 마스크 모델을 개량하여 pre-train단계에서 학습한 모든 정보를 사용할 수 있도록 시도하였다. XLNet은 마스크 모델을 permuted 언어 모델 (Permuted Language Modeling, PLM)로 대체한다. 이는 입력 토큰들을 랜덤하게 재배열하여 입력으로 집어넣는 방식이다. 이렇게 하면 토큰의 위치가 모든 포지션의 문맥적 정보를 이용할수 있게 되는데 그 결과 각 토큰별로 양방향 컨텍스트의 정보를 모두 캡쳐할 수 있게 된다
XLNet은 일반화된 AR모델이지만 AR과 AE의 장점이 결합된 일종의 프레임워크이다. XLNet이 이 두가지 메커니즘을 결합한 이유는 AR과 AE의 모든 장점을 활용하기 위해서이다. AE모델 에서는 2스트림 기반의 어텐션 메커니즘을 도입하였고 AR모델 에서는 Transformer-XL 모델의 세그먼트 레벨 재귀 메커니즘(segment-level recurrence mechanism)을 도입하였다
이렇게 두가지 파트로 구성된 XLNet은 일반화된 AR모델이므로 다양한 수단에 이용할 수 있다.\


## 4.2 seq2seq의 개념과 모델 소개 (Working with Seq2Seq models)
T5, BART, PEGASUS 등은 대표적인 seq2seq 모델이다\
이번 장은 가장 대표적인 seq2seq 모델인 T5와 BART의 개념을 소개하고 실습을 수행한다

### 4.2.1.T5
T5는 인코더와 디코더를 결합한 unifying framework이다. 입력값에 prefix를 집어넣어 의도를 나타낸다.\
prefix의 예로는 ‘요약’, ‘영어로 번역’ 같은 것들이 있다.\
T5모델의 실습은 4.4절의 문장 생성하기에서 진행한다

### 4.2.2 BART란?
BART역시 AR과 AE모델을 둘다 이용하는 프레임워크의 일종이다. 페이스북에서 개발했다\
이번 장은 아래와 같은 내용을 다룬다
1. BART의 개념
1. BART의 간단한 실습. 허깅페이스 리포지토리에서 이미 학습된 BART 모델인 summarization을 불러와  영어 문장을 입력했을 때 요약이 제대로 수행되는지 실습해본다

## 4.3 학습하기  (AR language model training)
GPT-2 모델을 pre-train하는 과정을 실습한다
## 4.4 [실습] AR모델을 사용해서 문장 생성하기 (Natural Language Generate, NLG)
이번 장은 pre-train된 GPT-2모델을 이용하여 문장을 생성해본다

## 4.5 [실습] simpletransformers 라이브러리로 번역하기 (Summarization and MT fine-tuning using simpletransformers)
이번 장은 Simple Transformers라는 이름의 T5 구현체를 이용하여 언어간 번역을 실습한다
학습된 T5모델에 영어 문장을 집어넣으면 터키어로 번역이 제대로 이루어지는지 확인한다
## 4.6 요약 (Summary)

# 5장. fine-tune for classifier (분류용 파인튠)
이번장은 다음을 다룬다  
1. BERT로 이진분류 fine-tune하기  
2. 분류모델을 학습하기  
3. BERT로 다중분류하기  
4. BERT로 문장-쌍을 regression하기  

# 6장. fine-tune for token classification
-

## 6.1 토큰 분류(token classification) 소개
-

## 6.2 fine-tune하기 (NER을 위한)
-

## 6.3 토큰 분류를 통한 Q&A
-

# 7장. text representation (워드 임베딩 or 문장 임베딩)
text representation은 비지도 학습에서 중요하다. 이 작업은 Representing sentences라고 한다. 이 작업은 특수한 엔코더로 수행한다. 예를들어 Siamese BERT등이다. text representation으로 제로샷 러닝도 가능하다. few-shot 러닝도 가능하다. one-shot 러닝도 가능하다.  

## 7.1 sentence embedding 소개
BERT는 효율적인 임베딩을 할수없다. 항상 fine-tune을 요구한다. 왜냐하면 pre-trained BERT는 분리불가능한 전체이고 시멘틱은 모든 딥러닝 레이어에 걸쳐있기 때문이다. 그리고 비지도학습이 어렵다. 왜냐하면 많은 문장 쌍을 평가해야 하기 때문이다. 경우의 수가 너무많아  실질적으로는 연산이 불가능하다.  
BERT의 변형인 Sentence BERT는 의미론적으로 유의미하고 독립적인 문장 임베딩이다 (이해불가).
벡터공간에서 문장간의 유의미성을 평가할때는 코사인 함수를 쓰고 불일치성을 평가할때는 유클리디안 거리를 쓴다.  

text representation이란 sentence embeddings이다.  

## 7.2 문장유사도 실험 (FLAIR를 통한)
-

## 7.3 텍스트 클러스터링 (Sentence-BERT를 통한)
-

## 7.4 시멘틱 검색 (Sentence-BERT를 통한)
-

# 8장. 효율적인 트랜스포머
distillation(증류), pruning(가지치기), quantization(정량화)를 이용하면 효율적인 모델을 만들수 있다  
sparse transformers에 대해 배울것이다.  
sparse transformers에 예로는 BigBird가 있다.  
모델 크기를 줄이는 방법을 배워보자.  
이 장은 성능이 떨어지는 환경에서 학습할때 유용한 정보를 다룬다  
DistilBERT는 distillation된 BERT이다. 증류된 모델은 더욱 가볍다.
attention dot product의 4차원적 복잡성 문제로 긴 문장을 작업하는데 오랜 시간이 걸린다.   BigBird는 복잡성 문제를 해결하여 학습시간을 단축해준다  
이번 장에서 배울 내용  
1. 가볍고 빠른 트랜스포머  
1. 모델 크기 줄이기  
1. 효율적인 self-attention (BigBird같은 모델들)  

## 8.1 도입부 : 효율적이고 빠른 트랜스포머
-

## 8.2 모델 사이즈 감소 구현하기
-

## 8.3 효율적인 셀프어텐션 구현하기
-

# 9장. 이종언어간 모델
다음은 기존 모델의 이종언어판이다  
Multilingual Bidirectional Encoder Representations from Transformers (mBERT)  

Multilingual Text-to-Text Transfer Transformer (mT5)  

Multilingual Bidirectional and Auto-Regressive Transformer (mBART)  

반면 Cross-linual Language 모델은 설계단계부터 이종언어간 모델을 염두하고 제작되었다  

Byte-Pair Encoding (BPE)이 토큰화로 수행된다. 말 그대로 이종언어간의 페어 인코딩이다.  

## 9.1 번역 모델  

언어모델은 크게 3가지로 나뉜다  
MLM : Masked Language Modeling (마스킹)  
CLM : Causal Language Modeling (인과관계)  
CLM은 문장생성기 이다.  

TLM : Translation Language Modeling (번역)  
번역 모델은 Mask 모델의 변형판이다.  
2개의 각각 다른국가 언어의 문장이 주어진다. 각 문장은 랜덤으로 단어가 마스크되어 있다. 마스크 된 토큰을 자국어로 추론한다. 이게 전부다.  

## 9.2 XLM & mBERT
mBERT는 다언어 모델이다. 이는 마스크 모델을 사용했다.  
반면 XLM은 MLM, CLM, TLM등 다양한 모델을 사용했다.  

### 9.2.1 mBERT
104개 다국적 언어로 학습되었다.  
단점 : 언어간 1:1 맵핑이 불가능하다  
언어간 맵핑을 하려면 지도학습을 추가로 해주어야 한다  

### 9.2.2 XLM
B-pair-E 토크나이저를 사용한다. 토큰이 공유되는 이유 : 공유된 토큰은 더 적은수의 토큰을 제공한다 (언어간 토큰을 공유하는 경우에는 그렇다.). 반면 동음이의어도 있다. 운좋게도 self-attention은 이종언어의 같은 음절의 단어의 뜻을 구분해준다.  