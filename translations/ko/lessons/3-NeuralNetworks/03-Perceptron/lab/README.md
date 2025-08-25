<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7336583e4630220c835335da640016db",
  "translation_date": "2025-08-24T21:35:11+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/lab/README.md",
  "language_code": "ko"
}
-->
# 퍼셉트론을 이용한 다중 클래스 분류

[AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners)에서 제공하는 실습 과제입니다.

## 과제

이 강의에서 개발한 MNIST 손글씨 숫자의 이진 분류 코드를 사용하여 모든 숫자를 인식할 수 있는 다중 클래스 분류기를 만드세요. 학습 및 테스트 데이터셋에서 분류 정확도를 계산하고 혼동 행렬(confusion matrix)을 출력하세요.

## 힌트

1. 각 숫자에 대해 "이 숫자 vs. 다른 모든 숫자"의 이진 분류 데이터셋을 만드세요.
1. 이진 분류를 위해 10개의 서로 다른 퍼셉트론을 학습시키세요 (각 숫자마다 하나씩).
1. 입력 숫자를 분류할 수 있는 함수를 정의하세요.

> **힌트**: 10개의 퍼셉트론의 가중치를 하나의 행렬로 결합하면, 입력 숫자에 대해 한 번의 행렬 곱셈으로 모든 퍼셉트론을 적용할 수 있습니다. 가장 가능성이 높은 숫자는 출력값에 `argmax` 연산을 적용하여 찾을 수 있습니다.

## 시작 노트북

[PerceptronMultiClass.ipynb](../../../../../../lessons/3-NeuralNetworks/03-Perceptron/lab/PerceptronMultiClass.ipynb)를 열어 실습을 시작하세요.

**면책 조항**:  
이 문서는 AI 번역 서비스 [Co-op Translator](https://github.com/Azure/co-op-translator)를 사용하여 번역되었습니다. 정확성을 위해 최선을 다하고 있지만, 자동 번역에는 오류나 부정확성이 포함될 수 있습니다. 원본 문서의 원어 버전을 권위 있는 출처로 간주해야 합니다. 중요한 정보의 경우, 전문적인 인간 번역을 권장합니다. 이 번역 사용으로 인해 발생하는 오해나 잘못된 해석에 대해 책임을 지지 않습니다.