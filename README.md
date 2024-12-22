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


