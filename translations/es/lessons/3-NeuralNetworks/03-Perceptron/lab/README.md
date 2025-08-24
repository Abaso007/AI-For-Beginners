<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7336583e4630220c835335da640016db",
  "translation_date": "2025-08-24T09:23:19+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/lab/README.md",
  "language_code": "es"
}
-->
# Clasificación Multiclase con Perceptrón

Asignación de laboratorio del [Currículo de IA para Principiantes](https://github.com/microsoft/ai-for-beginners).

## Tarea

Usando el código que hemos desarrollado en esta lección para la clasificación binaria de los dígitos manuscritos de MNIST, crea un clasificador multiclase que sea capaz de reconocer cualquier dígito. Calcula la precisión de clasificación en los conjuntos de datos de entrenamiento y prueba, y muestra la matriz de confusión.

## Pistas

1. Para cada dígito, crea un conjunto de datos para un clasificador binario de "este dígito vs. todos los demás dígitos".
1. Entrena 10 perceptrones diferentes para la clasificación binaria (uno para cada dígito).
1. Define una función que clasifique un dígito de entrada.

> **Pista**: Si combinamos los pesos de los 10 perceptrones en una sola matriz, deberíamos poder aplicar los 10 perceptrones a los dígitos de entrada mediante una sola multiplicación de matrices. El dígito más probable se puede encontrar simplemente aplicando la operación `argmax` en la salida.

## Notebook Inicial

Comienza el laboratorio abriendo [PerceptronMultiClass.ipynb](../../../../../../lessons/3-NeuralNetworks/03-Perceptron/lab/PerceptronMultiClass.ipynb)

**Descargo de responsabilidad**:  
Este documento ha sido traducido utilizando el servicio de traducción automática [Co-op Translator](https://github.com/Azure/co-op-translator). Si bien nos esforzamos por lograr precisión, tenga en cuenta que las traducciones automáticas pueden contener errores o imprecisiones. El documento original en su idioma nativo debe considerarse como la fuente autorizada. Para información crítica, se recomienda una traducción profesional realizada por humanos. No nos hacemos responsables de malentendidos o interpretaciones erróneas que puedan surgir del uso de esta traducción.