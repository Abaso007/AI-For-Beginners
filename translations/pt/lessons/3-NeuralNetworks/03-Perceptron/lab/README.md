<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7336583e4630220c835335da640016db",
  "translation_date": "2025-08-24T09:05:15+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/lab/README.md",
  "language_code": "pt"
}
-->
# Classificação Multi-Classe com Perceptron

Trabalho prático do [Currículo de IA para Iniciantes](https://github.com/microsoft/ai-for-beginners).

## Tarefa

Utilizando o código que desenvolvemos nesta lição para classificação binária de dígitos manuscritos do MNIST, crie um classificador multi-classe que seja capaz de reconhecer qualquer dígito. Calcule a precisão da classificação nos conjuntos de treino e teste, e apresente a matriz de confusão.

## Dicas

1. Para cada dígito, crie um conjunto de dados para o classificador binário de "este dígito vs. todos os outros dígitos".
1. Treine 10 perceptrons diferentes para classificação binária (um para cada dígito).
1. Defina uma função que classifique um dígito de entrada.

> **Dica**: Se combinarmos os pesos de todos os 10 perceptrons numa única matriz, deveremos ser capazes de aplicar todos os 10 perceptrons aos dígitos de entrada através de uma única multiplicação de matrizes. O dígito mais provável pode então ser encontrado simplesmente aplicando a operação `argmax` ao resultado.

## Notebook Inicial

Comece o trabalho prático abrindo [PerceptronMultiClass.ipynb](../../../../../../lessons/3-NeuralNetworks/03-Perceptron/lab/PerceptronMultiClass.ipynb)

**Aviso Legal**:  
Este documento foi traduzido utilizando o serviço de tradução por IA [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos pela precisão, esteja ciente de que traduções automáticas podem conter erros ou imprecisões. O documento original na sua língua nativa deve ser considerado a fonte autoritária. Para informações críticas, recomenda-se a tradução profissional realizada por humanos. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações incorretas decorrentes do uso desta tradução.