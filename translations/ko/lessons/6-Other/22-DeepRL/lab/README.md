<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7bd8dc72040e98e35e7225e34058cd4e",
  "translation_date": "2025-08-24T21:33:23+00:00",
  "source_file": "lessons/6-Other/22-DeepRL/lab/README.md",
  "language_code": "ko"
}
-->
## 환경

Mountain Car 환경은 자동차가 계곡 안에 갇혀 있는 상황으로 구성됩니다. 목표는 계곡을 뛰어넘어 깃발에 도달하는 것입니다. 수행할 수 있는 행동은 왼쪽으로 가속, 오른쪽으로 가속, 또는 아무것도 하지 않는 것입니다. 자동차의 x축 위치와 속도를 관찰할 수 있습니다.

## 시작 노트북

[MountainCar.ipynb](../../../../../../lessons/6-Other/22-DeepRL/lab/MountainCar.ipynb)를 열어 실습을 시작하세요.

## 주요 학습 내용

이 실습을 통해 RL 알고리즘을 새로운 환경에 적용하는 것이 종종 매우 간단하다는 것을 배우게 될 것입니다. 이는 OpenAI Gym이 모든 환경에 대해 동일한 인터페이스를 제공하며, 알고리즘 자체가 환경의 특성에 크게 의존하지 않기 때문입니다. Python 코드를 재구성하여 RL 알고리즘에 어떤 환경이든 매개변수로 전달할 수 있도록 할 수도 있습니다.

**면책 조항**:  
이 문서는 AI 번역 서비스 [Co-op Translator](https://github.com/Azure/co-op-translator)를 사용하여 번역되었습니다. 정확성을 위해 최선을 다하고 있지만, 자동 번역에는 오류나 부정확성이 포함될 수 있습니다. 원본 문서의 원어 버전을 권위 있는 출처로 간주해야 합니다. 중요한 정보에 대해서는 전문적인 인간 번역을 권장합니다. 이 번역을 사용함으로 인해 발생하는 오해나 잘못된 해석에 대해 당사는 책임을 지지 않습니다.