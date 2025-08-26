<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7336583e4630220c835335da640016db",
  "translation_date": "2025-08-26T00:00:48+00:00",
  "source_file": "lessons/3-NeuralNetworks/03-Perceptron/lab/README.md",
  "language_code": "ro"
}
-->
# Clasificare Multi-Clasă cu Perceptron

Temă de laborator din [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners).

## Sarcină

Folosind codul dezvoltat în această lecție pentru clasificarea binară a cifrelor scrise de mână din MNIST, creați un clasificator multi-clasă care să poată recunoaște orice cifră. Calculați acuratețea clasificării pe setul de date de antrenament și test, și afișați matricea de confuzie.

## Sugestii

1. Pentru fiecare cifră, creați un set de date pentru clasificarea binară „această cifră vs. toate celelalte cifre”.
1. Antrenați 10 perceptroni diferiți pentru clasificarea binară (câte unul pentru fiecare cifră).
1. Definiți o funcție care să clasifice o cifră de intrare.

> **Sugestie**: Dacă combinăm greutățile tuturor celor 10 perceptroni într-o singură matrice, ar trebui să putem aplica toți cei 10 perceptroni asupra cifrelor de intrare printr-o singură înmulțire de matrice. Cifra cea mai probabilă poate fi apoi găsită doar aplicând operația `argmax` pe ieșire.

## Notebook de Pornire

Începeți laboratorul deschizând [PerceptronMultiClass.ipynb](../../../../../../lessons/3-NeuralNetworks/03-Perceptron/lab/PerceptronMultiClass.ipynb)

**Declinare de responsabilitate**:  
Acest document a fost tradus folosind serviciul de traducere AI [Co-op Translator](https://github.com/Azure/co-op-translator). Deși ne străduim să asigurăm acuratețea, vă rugăm să fiți conștienți că traducerile automate pot conține erori sau inexactități. Documentul original în limba sa natală ar trebui considerat sursa autoritară. Pentru informații critice, se recomandă traducerea profesională realizată de un specialist uman. Nu ne asumăm responsabilitatea pentru eventualele neînțelegeri sau interpretări greșite care pot apărea din utilizarea acestei traduceri.