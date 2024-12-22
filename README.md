# final-project

실험 환경
- Google Colab pro+ : A100
- transformer: 4.39.2
- peft : 0.10.0
- trl : 0.8.6
- bitsandbytes : 0.43.0
- accelerate : 0.29.0

***

## 모델 선정 배경
Mistral, LLaMa, BERT, GPT 등 다양한 모델 중에 OT 환경의 특성과 개발 환경에 초점을 맞춰서 모델을 선정했습니다. OT 환경은 기본적으로 외부 네트워크와 연결을 하지 않는다는 것을 전제로 네트워크 구성이 진행됩니다. 또한, 사이qj보안 목적 상 조직의 데이터가 외부에 유출 및 노출되는 것을 막아야하며 조직 내부에서만 사용이 가능해야 합니다. 따라서, GPU가 부족하고 On-primise 환경에서 사용할 수 있는 LLaMa 3 8B 모델을 선정했습니다.!


***

## 프로젝트 목적
기존의 기계 학습 기반의 침입 탐지 시스템은 오탐율이 높고 실제 환경에서 발생하는 많은 양의 데이터를 효율적이고 효과적으로 분석할 수 있는 기술이 부족하다. 또한, IT 네트워크와 OT 네트워크에서 사용하는 프로토콜이 다르며 사용되는 장치가 다르다. OT 장치는 기존의 IT 장치와 다르게 한 번 세션이 연결될 경우 짧게는 7일 길게는 30일 동안 세션 종료를 하지 않고 통신을 지속하며, 환경의 특성 상 한 번의 연결 종료가 막대한 경제적 피해와 인명 피해를 초래할 수 있다. 현재 침입 탐지 시스템 연구는 IT 네트워크에서 진행되고 있으며 공개 데이터 세트(DARAPA IDS Data, KDDCup99, NSL-KDD, UNSW-NB 15 등)은 OT 네트워크에서 적용할 수 없는 데이터이다. 따라서, 본 프로젝트에서는 대규모 언어 모델에게 학습시킬 수 있는 OT 네트워크 데이터를 개발하고 침입 탐지 시스템으로 적용하는 것이다.

***
## 실험 과정
![image](https://github.com/user-attachments/assets/8ee9d2dd-9d6c-4b83-9145-b1768b5947de)

### 데이터 수집 단계(Data Collection)
데이터 수집 단계에서는 MITRE ATT&CK와 다른 오픈소스 등을 이용해 OT/ICS 환경에서 실제로 발생한 공격에 대한 정보들을 수집하며 실제 공격들이 발생했을 때, 사용된 TTPs를 중점적으로 수집한다. 데이터 수집 단계에서는 APT Reports, Ransom Reports 등의 보고서의 자연어에서 TTP를 추출하는 것이 중요하다. 지속적으로 TTP를 수집해야 하기 때문에 “TRAM:Threat Report ATT&CK Mapper, MITRE ENGENUITY”에서 2021년에 공개한 것을 적용해 향후 발생하는 TTP를 수집하려고 한다.

### 전처리 단계(Data pre-processing)
데이터 전처리 단계에서는 실제 공격사례 기반의 데이터를 ATT&CK for ICS Matrix를 기반으로 정리할 수 있다. 이러한 정보들을 통해, 각 공격들이 사용한 전술과 기법들을 알 수 있으며, OT/ICS 환경에서 자주 사용되는 전술과 기법을 파악할 수 있다. 그림과 같이 수집한 데이터를 기반으로 OT/ICS 환경에서 실제로 발생한 Stuxnet을 MITRE ATT&CK for ICS Matrix 기반으로 정리한 것이다. 해당 정보들을 OpenAI GPT, Facebook LLaMa, Google BERT의 모델 학습 방법에 맞게 학습시켜야 한다. 
![Uploading image.png…]()



### 모델링 단계(Modeling)
 모델링 단계에서는 pre-trained된 LLaMa 3 8B 모델을 파인튜닝(Fine tuning)을 진행한다. 모델은 전술과 기법이 포함된 데이터를 통해 공격자의 패턴과 구조를 파악하여 다음에 일어날 공격에 대해 예측할 수 있도록 한다. 이러한 결과로 방어자(사용자)는 예측의 결과를 통해 다음에 일어날 공격에 대해 방어할 수 있으며, 공격자의 의도를 파악하고 공격에 대한 피해를 최소화할 수 있다. 다음은 방어자와 모델의 질문 및 답변의 예시이다.
- User: Please tell me about techniques that may occur in PLC.
- Model : Techniques that can occur in PLC are as follows. Replication Through Removable Media, Supply Chain Compromise, Rogue Master, etc.
 
