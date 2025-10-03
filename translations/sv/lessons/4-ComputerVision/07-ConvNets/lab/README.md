<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f3d2cee9cb3c52160419e560c57a690e",
  "translation_date": "2025-08-28T15:14:10+00:00",
  "source_file": "lessons/4-ComputerVision/07-ConvNets/lab/README.md",
  "language_code": "sv"
}
-->
# Klassificering av husdjurs ansikten

Labuppgift från [AI for Beginners Curriculum](https://github.com/microsoft/ai-for-beginners).

## Uppgift

Föreställ dig att du behöver utveckla en applikation för ett djurpensionat för att katalogisera alla husdjur. En fantastisk funktion i en sådan applikation skulle vara att automatiskt identifiera rasen från ett fotografi. Detta kan framgångsrikt göras med hjälp av neurala nätverk.

Du behöver träna ett konvolutionellt neuralt nätverk för att klassificera olika raser av katter och hundar med hjälp av datasetet **Pet Faces**.

## Datasetet

Vi kommer att använda datasetet **Pet Faces**, som är hämtat från [Oxford-IIIT](https://www.robots.ox.ac.uk/~vgg/data/pets/) husdjursdataset. Det innehåller 35 olika raser av hundar och katter.

![Datasetet vi kommer att arbeta med](../../../../../../translated_images/data.50b2a9d5484bdbf0f52f5765b381cec9efe2bd296a98f007f90bedb6ac67f2a8.sv.png)

För att ladda ner datasetet, använd följande kodsnutt:

```python
!wget https://thor.robots.ox.ac.uk/~vgg/data/pets/images.tar.gz
!tar xfz images.tar.gz
!rm images.tar.gz
```

## Starta Notebook

Börja labben genom att öppna [PetFaces.ipynb](PetFaces.ipynb)

## Slutsats

Du har löst ett relativt komplext problem med bildklassificering från grunden! Det fanns ganska många klasser, och du lyckades ändå uppnå rimlig noggrannhet! Det är också vettigt att mäta top-k noggrannhet, eftersom det är lätt att förväxla vissa klasser som inte är tydligt olika, även för människor.

---

**Ansvarsfriskrivning**:  
Detta dokument har översatts med hjälp av AI-översättningstjänsten [Co-op Translator](https://github.com/Azure/co-op-translator). Även om vi strävar efter noggrannhet, bör du vara medveten om att automatiserade översättningar kan innehålla fel eller inexaktheter. Det ursprungliga dokumentet på dess originalspråk bör betraktas som den auktoritativa källan. För kritisk information rekommenderas professionell mänsklig översättning. Vi ansvarar inte för eventuella missförstånd eller feltolkningar som uppstår vid användning av denna översättning.