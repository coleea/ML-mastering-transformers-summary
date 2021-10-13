# mastering transformers 요약
저자 : Savaş Yıldırım, Meysam Asgari-Chenaghlu  
출간일 : 2021/09  

이 책은 크게 아래로 분류된다  
1장 : NLP의 역사  
2장 : 개발환경 셋팅하기  
3,4장 : 인코더와 디코더를 이론 중심으로 설명  
5,6장 : fine-tune 방법을 설명  
7장 : Text Representation  
8, 9장 : 빠르고 효율적인 모델 만들기  
9장 : 다언어 모델  
10, 11장 : 일종의 번외편  

# 1장. NLP의 역사

## 1.1 transformers 까지의 역사

### 1.1.1 bag of word
bag of word는 워드 임베딩이다. 워드 임베딩이란 단어에 숫자를 레이블링하는 작업이다.  
워드 임베딩의 단점 : 단어와 단어간에 아무런 관계도 부여되지 않는다. 따라서 단어가 맥락에서 사용되었는지 알수없다  
워드 임베딩을 개선하여 단어와 단어간에 맥락(context)을 부여하는 방법이 고안되었다  
### 1.1.2 word2vec(2013)
word2vec은 단어와 단어 사이에 맥락(context)을 부여한다.  
예를 들어 `학교`라는 단어가 있으면 그 단어에 대한 배열을 생성해서 그 단어와 인접한 순으로  단어를 순서대로 적는다. 예를들어 `['공부', '학생', '선생님', '시험']` 와 같은 배열이 생성된다  

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

### 1.1.3 transformers 모델

문장내 단어간 관계를 학습하는 모델을 `self-attention`이라고 한다  

word2vec과 마찬가지로 문장내 인접한 단어끼리 관계도가 높다  

transformers는 문장 전체에 대한 배열을 만든다. 배열은 N차원 좌표평면상의 특정 좌표를    의미한다. 이 문장의 배열에는 특정 단어의 좌표는 포함되어 있지 않다.  
이 과정을 language model이라고 한다. 여기까지의 작업이 pre-train이다.  
그리고 이 language model을 가져와서 sentiment analysis를 하거나 언어 번역을 하고싶을때는 fine-tuning으로 테스크에 특성화된 작업을 수행한다.  
이 일련의 과정을 합쳐서  transfer learning, 한국어로 전이 학습이라고 한다.  

이 과정을 여러번 반복해서 평균을 내기 때문에 ‘multi’라는 단어를 붙여서 `multi-head selt-attention`이라고 한다

#### 1.1.3.1 인코더 & 디코더
인코더를 autoencoder라고 한다.  
디코더를 regressive 모델이라고 한다.  

인코더는 양방향(bi-directional) 토큰을 이용해서 중간에 위치한 토큰을 생성한다. 이를 양방향 트랜스포머라고 한다.  
디코더는 한쪽방향 토큰을 이용해서 다음 토큰을 생성하는 생성자이다  
`주의 ! : BERT와 BART는 다른 개념이다. BERT는 인코더 모델이며 BART는 인코더와 디코더가 결합된 seq2seq 모델이다  `

## 1.2 distributional semantics

###	1.2.1 bow 구현하기

### 1.2.2 차원 문제

###	1.2.3 언어 모델링

## 1.3 레버리징 DL

### 1.3.1 워드 임베딩

### 1.3.2 RNN
RNN기반의 번역 모델은 인코더-디코더 기반 모델이다. 먼저 인코더는 입력으로 문장을 구성하는 각 단어를 순차적으로 입력받는다. 각 단어를 입력받을 때 마다 컨텍스트 벡터를 출력한다. 문장의 마지막 단어까지 입력받으면 최종적인 컨텍스트 벡터(context vector)가 완성된다. 이 컨텍스트 벡터는 입력 문장의 처음부터 끝까지 모든 컨텍스트 정보를 벡터로 표현한 자료구조이다. 디코더는 이 컨텍스트 벡터를 입력으로 받아 입력에 대응되는 단어를 하나씩 생성하여 최종적으로 하나의 문장을 생성한다. 컨텍스트 벡터는 인코더와 디코더 사이에 위치하기 때문에 이를 중간 표현값(intermediate representation)이라고 부른다.
디코더가 문장을 생성할 때는 1개 단어씩 순차적으로 생성하는데 이 작업은 end 토큰을 만날때 까지 반복된다. 하지만 이런 메커니즘에는 문제가 있다. 최종 컨텍스트 벡터가 생성된 시점에서 초기에 입력된 토큰의 정보가 점점 소실된다는 점이다. 따라서 RNN기반의 인코더는 `긴 문장이 입력으로 들어왔을 때 상당량의 정보가 소실되는 문제가 있다.`  
두번째 문제, 컨텍스트 벡터는 처음부터 고정된 사이즈이다. 입력의 길이를 예측할 수 없는 상황에서 고정 사이즈의 배열을 활용한다는 건 최적화에 문제가 있다.  

###### 어텐션은 어떻게 이 문제를 해결했는가 ?
하나의 컨텍스트 벡터만을 사용하는 것이 아니라 각 단어가 입력으로 들어갈 때 마다 생성되는 모든 컨텍스트 벡터를 사용하는 것이다. 이렇게 되면 각 단어의 정보가 소실되지 않은 상황, 다시말해 단어의 컨텍스트 정보가 전혀 소실되지 않은 컨텍스트 벡터와 전체적인 문장의 컨텍스트 정보를 동시에 참고하여 문장을 생성할 수 있다. 즉 입력 단어가 3개라면 중간과정에 생성되는 컨텍스트 벡터와 최종적으로 생성되는 벡터를 합쳐 총 3가지의 벡터가 생성된다. 이 3가지의 정보를 모두 다 이용하여 문장을 생성하는 것이 어텐션 메커니즘이다. 어텐션의 대략적인 공식은 다음과 같다
`어떤함수(생성된 모든 컨텍스트 벡터) + 어떤함수(가장 최근에 생성된 컨텍스트 벡터)`
이 어텐션은 fully-connected neural network에서 작동하며 최종 레이어에서는 입력단어의 갯수만큼의 weight를 출력한다. 이 최종 레이어의 weight들에 softmax함수를 적용하면 모든 weight의 총합이 1이 되는 확률분포가 생성된다. 이 weight를 어텐션 weight라고 부른다. 이 어텐션 weight는 입력 단어들 중 어느 단어에 비중을 두어야 하는지에 대한 정보를 담고 있다. 이 어텐션 weight의 정보를 활용하여 최종적으로 단어 생성에 사용할 컨텍스트 벡터를 생성한다. 이 최종 생성된 컨텍스트 벡터를 입력으로 단어를 생성한다.

상세 내용은 유튜브 강의 (https://www.youtube.com/watch?v=WsQLdu2JMgI) 를 참조할 것  
### 1.3.3 LSTM & GRU

### 1.3.4 LSTM 구현하기

### 1.3.5 CNN 오버뷰

## 1.4 트랜스포머 아키텍처
트랜스포머로 대부분의 NLP문제를 처리할 수 있다. 어텐션 메카니즘은 트랜스포머의 핵심이다. 트랜스 포머 이전에도 어텐션은 존재했다. 과거 LSTM모델에서 어텐션은 성능 향상을 위한 옵션으로 존재했다. 하지만 트랜스포머에서는 어텐션이 핵심 메커니즘이다  

### 1.4.1 어텐션  
어텐션은 2015년 Bahdanau등에 의해 제안되었다. LSTM은 자연어 번역 과정에서 정보 보틀넥이 있었다. 이들 인코더-디코더 기반 모델은 입력을 받아 인코더에서 recurrent기반으로 프로세싱한다. 후에 이 중간 값(intermediate representation)은 다른 recurrent unit인 디코더로 이송된다. 이것은 모든 정보를 소비한 후에 롤링아웃하는 과정은 디코더에게 더버거웠다 왜냐하면 디코더는 모든 의존성들을 볼 수 없기 때문이고 `오직 중간 과정만을 입력으로서 참조`하기 때문이다.
이 문제를 해결하려 어텐션이 고안되었는데 어텐션에서는 weight들을 중간 숨겨진 값들로 이용한다. 이들 어텐션의 양을 조율한 weight들은 각 디코딩 스탭별로 입력을 지불해야한다. 이는 모델이 자연어 번역같은 모델을 돕는다.


### 1.4.2 멀티헤드 어텐션

## 1.5 TL을 트랜스포머와 같이쓰기  
TL은 AI의 분야이다.  
TL은 pre-trained model이다.  
TL은 shallow model과 deep model로 나뉜다  
shallow model은 pre-trained vector이다.  
deep model은 language model이다.  


# 2장. introduction (도입)
## 2.1 아나콘다와 transformers 설치
### 2.1.1 colab에서 설치하는 방법
`!pip install Transformer`

!(느낌표)는 shell에서 실행하도록 해준다. 파이썬에서의 실행이 아니다  

## 2.2 언어모델과 토크나이저 불러오기
transformers 사용법 : 모델함수 안에 인코딩된 토큰을 집어넣으면 끝.  

## 2.3 커뮤니티에서 제공하는 모델 불러오기
결론 : pipeline()함수로 불러오시오  

## 2.4 벤치마킹 함수와 데이터셋 불러오기
### 2.4.1 중요한 벤치마킹 함수  

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

# 3.1 BERT
BERT는 다중레이어 모델이다.  
BERT의 핵심 : provide better language modeling. 즉 더나은 fine-tune 학습을 제공한다.  
BERT를 이해하기 전에 먼저 GPT-1을 이해하는 것이 좋다. BERT는 GPT-1 공개 이후 GPT-1의 단점을 지적하면서 등장했다. GPT-1은 `문장을 출력할 때 단방향으로 출력하는 단점이 있다`. 이러한 단방향 접근법은 문맥 이해에 어려움이 있을 수 있다.

### 3.1.1 pre-train
BERT의 마스크 모델을 제대로 이해하려면 마스크 모델을 왜 쓰는지를 알아야 한다  
마스크 모델을 왜 쓰는가 ? 마스크 모델이 cloze 테스트가 가능하면 언어의 일반적인 이해가 가능하기 때문이다.
따라서 cloze 테스트가 뭔지를 이해해야 한다.  
cloze 테스트는 마스크된 문장을 평가하는 방법이다. 마스크된 토큰에 단어가 생성되면 그 단어가 문장에 적합한지를 평가하는게 cloze 테스트이다.

### 3.1.2 BERT 깊이 파보기
BERT는 WordPiece 토큰화를 제공한다.  

## 3.2 training for any language

## 3.3 모델 공유하기

## 3.4 다른 모델들
### 3.4.1 ALBERT
### 3.4.2 RoBERTa
### 3.4.3 ELECTRA (2020)
ELECTRA is a masked language model.  
마스크 언어 모델의 학습이 비효율적이다. 그래서 더 빠른 처리속도를 도입했다.  

참고 : GAN은 임의의 IMAGE를 생성하는 모델이다. 생성된 이미지를 분류기가 TRUE OR FALSE로 구분하는데 만일 생성된 이미지가 원본과 유사하다고 판별하면 true를 출력한다. 이같은 경우 generator가 제대로 이미지를 생성했다고 학습한다. 이 경우는 loss함수를 통한 튜닝이 필요가 없다.

## 3.5 토크나이징

### 3.5.1 byte-pair 인코딩

### 3.5.2 wordPiece 토큰화

### 3.5.3 sentence piece 토큰화

### 3.5.4 토크나이저 라이브러리

## 3.6 요약

# 4장. 디코더
GPT-2는 디코더이다.  
이번장에서 배울 내용은 아래의 5가지다  
1. 인코더와 디코더 함께쓰기  
1. seq2seq 모델 만들기  
1. 인코더 모델을 학습하기  
1. 인코더 모델을 써서 NLG하기  
1. SIMPLE TRANSFORMERS사용하여 요약하기  

## 4.1 AR 언어모델과 디코더 함께쓰기

### 4.1.1 GPT란?
문장을 입력하면 다음 단어를 예측하는데 이때 전체 단어에 대한 확률을 출력하는 모델이 GPT이다.  
이들은 2단계로 나뉜다  
첫단계는 PRE-TRAIN이다. 이는 비지도 pre-train이다.  
두번째는 fine-tune이다. 이는 supervised fine-tune이다. 이는 상대적으로 작은양의 데이터만을 사용한다.  

GPT-2와 GPT-3의 아키텍처는 비슷하다. 다만 파라메터 수가 100배 증가되었다.
GPT-3는 그라디언트 기반의 파인튜닝 없이 pre-train만으로 더나은 결과를 출력했다.

### 4.1.2 Transformer-XL
segment-레벨의 recurrence 메커니즘  
not limited to two consecutive segments  

The recurrence mechanism works between  
every two consecutive segments, leading to spanning the several segments to a certain
degree.  

### 4.1.3 XLNet
마스크 모델은 pre-train단계를 장악했다.  
하지만 마스크된 토큰은 pre-train단계에는 있지만 fine-tune단계에는 없다. 따라서 pre-train과 fine-tune 사이에는 불일치가 존재한다. 이 불일치 때문에 pre-train에서 학습한 모든 정보를 사용할 수 있는 것은 아니다.
XLNet은 마스크 모델을 permuted 모델로 대체한다 (순화 언어 모형). 이는 입력 토큰들의 랜덤 퍼뮤테이션이다.  토큰의 위치가 문맥적 정보를 이용할수 있도록 해준다.  
XLNet은 AR과 AE의 모든 장점을 활용한다. 이는 일반화된 AR모델이다.  

## 4.2 seq2seq
T5, BART, PEGASUS등은 유명한 seq2seq 모델이다  

### 4.2.1.T5
T5는 인코더와 디코더를 결합한 unifying framework이다. 입력값에 prefix를 집어넣어 의도를 나타낸다. prefix의 예로는 ‘요약’, ‘영어로 번역’ 같은 것들이 있다.  

### 4.2.2 BART란?
BART역시 AR과 AE모델을 둘다 이용하는 프레임워크의 일종이다. 페이스북에서 개발했다

## 4.3 학습하기  

## 4.4 AR모델을 사용해서 NLG(Natural Language Generate)하기

# 5장. fine-tune for classifier (분류용 파인튠)
이번장은 다음을 다룬다  
1. BERT로 이진분류 fine-tune하기  
2. 분류모델을 학습하기  
3. BERT로 다중분류하기  
4. BERT로 문장-쌍을 regression하기  

# 6장. fine-tune for token classification

# 7장. text representation (워드 임베딩 or 문장 임베딩)
text representation은 비지도 학습에서 중요하다. 이 작업은 Representing sentences라고 한다. 이 작업은 특수한 엔코더로 수행한다. 예를들어 Siamese BERT등이다. text representation으로 제로샷 러닝도 가능하다. few-shot 러닝도 가능하다. one-shot 러닝도 가능하다.  

## 7.1 sentence embedding 소개
BERT는 효율적인 임베딩을 할수없다. 항상 fine-tune을 요구한다. 왜냐하면 pre-trained BERT는 분리불가능한 전체이고 시멘틱은 모든 딥러닝 레이어에 걸쳐있기 때문이다. 그리고 비지도학습이 어렵다. 왜냐하면 많은 문장 쌍을 평가해야 하기 때문이다. 경우의 수가 너무많아  실질적으로는 연산이 불가능하다.  
BERT의 변형인 Sentence BERT는 의미론적으로 유의미하고 독립적인 문장 임베딩이다 (이해불가).
벡터공간에서 문장간의 유의미성을 평가할때는 코사인 함수를 쓰고 불일치성을 평가할때는 유클리디안 거리를 쓴다.  

text representation이란 sentence embeddings이다.

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


# 10장. 실전에서 써먹기
tensorflow extended는 디플로이에 사용한다.  
또한 fast api를 사용해서 api를 쓰는 방법도 배운다.  
도커도 배운다.  
locust로 속도 테스트 하는 방법도 배운다  

pydantic으로 입력값의 데이터 모델링을 수행한다  
예를들어 Q&A모델을 쓸때 입력으로 질문이 들어올게 아닌가? 그 입력을 어떻게 만드냐면 클라이언트 요청 패킷에서 가져온다. 가져온 정보를 pydantic으로 정규화한다  

# 11장. 어텐션 시각화 & 실험적 트래킹

## 11.1 어텐션 헤드를 해석하기
### 11.1.1 어텐션을 시각화하기
### 11.1.2 어텐션 헤드를 Multiscale 시각화
### 11.1.3 BERT의 내부를 이해하기

## 11.2 모델 메트릭을 트래킹하기

## 11.3 요약


