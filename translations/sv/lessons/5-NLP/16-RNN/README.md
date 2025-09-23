<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "58bf4adb210aab53e8f78c8082040e7c",
  "translation_date": "2025-08-28T15:58:41+00:00",
  "source_file": "lessons/5-NLP/16-RNN/README.md",
  "language_code": "sv"
}
-->
# Rekurrenta neurala nätverk

## [Quiz före föreläsning](https://ff-quizzes.netlify.app/en/ai/quiz/31)

I tidigare avsnitt har vi använt rika semantiska representationer av text och en enkel linjär klassificerare ovanpå inbäddningarna. Vad denna arkitektur gör är att fånga den aggregerade betydelsen av ord i en mening, men den tar inte hänsyn till **ordningen** av orden, eftersom aggregeringsoperationen ovanpå inbäddningarna tog bort denna information från den ursprungliga texten. Eftersom dessa modeller inte kan modellera ordordning, kan de inte lösa mer komplexa eller tvetydiga uppgifter som textgenerering eller frågehantering.

För att fånga betydelsen av textsekvenser behöver vi använda en annan neural nätverksarkitektur, som kallas ett **rekurrent neuralt nätverk**, eller RNN. I ett RNN skickar vi vår mening genom nätverket en symbol i taget, och nätverket producerar ett **tillstånd**, som vi sedan skickar tillbaka till nätverket tillsammans med nästa symbol.

![RNN](../../../../../translated_images/rnn.27f5c29c53d727b546ad3961637a267f0fe9ec5ab01f2a26a853c92fcefbb574.sv.png)

> Bild av författaren

Givet en inmatningssekvens av token X<sub>0</sub>,...,X<sub>n</sub>, skapar RNN en sekvens av neurala nätverksblock och tränar denna sekvens från början till slut med hjälp av backpropagation. Varje nätverksblock tar ett par (X<sub>i</sub>,S<sub>i</sub>) som indata och producerar S<sub>i+1</sub> som resultat. Det slutliga tillståndet S<sub>n</sub> eller (utdata Y<sub>n</sub>) skickas till en linjär klassificerare för att producera resultatet. Alla nätverksblock delar samma vikter och tränas från början till slut med en enda backpropagation-pass.

Eftersom tillståndsvektorerna S<sub>0</sub>,...,S<sub>n</sub> skickas genom nätverket, kan det lära sig sekventiella beroenden mellan ord. Till exempel, när ordet *inte* dyker upp någonstans i sekvensen, kan det lära sig att negera vissa element inom tillståndsvektorn, vilket resulterar i negation.

> ✅ Eftersom vikterna för alla RNN-block i bilden ovan är delade, kan samma bild representeras som ett block (till höger) med en rekurrent återkopplingsslinga, som skickar nätverkets utgångstillstånd tillbaka till indata.

## Anatomi av en RNN-cell

Låt oss se hur en enkel RNN-cell är organiserad. Den tar emot det föregående tillståndet S<sub>i-1</sub> och den aktuella symbolen X<sub>i</sub> som indata och måste producera utgångstillståndet S<sub>i</sub> (och ibland är vi också intresserade av någon annan utdata Y<sub>i</sub>, som i fallet med generativa nätverk).

En enkel RNN-cell har två viktmatriser inuti: en som transformerar en indatasymbol (vi kallar den W) och en annan som transformerar ett indatatillstånd (H). I detta fall beräknas nätverkets utdata som σ(W×X<sub>i</sub>+H×S<sub>i-1</sub>+b), där σ är aktiveringsfunktionen och b är en ytterligare bias.

<img alt="RNN Cell Anatomy" src="images/rnn-anatomy.png" width="50%"/>

> Bild av författaren

I många fall skickas indatatoken genom inbäddningslagret innan de går in i RNN för att minska dimensionen. I detta fall, om dimensionen av indatavektorerna är *emb_size* och tillståndsvektorn är *hid_size* - är storleken på W *emb_size*×*hid_size*, och storleken på H är *hid_size*×*hid_size*.

## Long Short Term Memory (LSTM)

Ett av de största problemen med klassiska RNN är det så kallade **försvinnande gradienter**-problemet. Eftersom RNN tränas från början till slut i en enda backpropagation-pass, har det svårt att sprida fel till de första lagren i nätverket, och därmed kan nätverket inte lära sig relationer mellan avlägsna token. Ett sätt att undvika detta problem är att införa **explicit tillståndshantering** genom att använda så kallade **grindar**. Det finns två välkända arkitekturer av detta slag: **Long Short Term Memory** (LSTM) och **Gated Relay Unit** (GRU).

![Bild som visar ett exempel på en long short term memory-cell](../../../../../lessons/5-NLP/16-RNN/images/long-short-term-memory-cell.svg)

> Bildkälla TBD

LSTM-nätverket är organiserat på ett sätt som liknar RNN, men det finns två tillstånd som skickas från lager till lager: det faktiska tillståndet C och den dolda vektorn H. Vid varje enhet sammanfogas den dolda vektorn H<sub>i</sub> med indata X<sub>i</sub>, och de styr vad som händer med tillståndet C via **grindar**. Varje grind är ett neuralt nätverk med sigmoidaktivering (utdata i intervallet [0,1]), som kan ses som en bitmask när den multipliceras med tillståndsvektorn. Följande grindar finns (från vänster till höger i bilden ovan):

* **Glömskegrinden** tar en dold vektor och avgör vilka komponenter i vektorn C vi behöver glömma och vilka vi ska släppa igenom.
* **Indatagrinden** tar viss information från indata- och dolda vektorer och inför den i tillståndet.
* **Utgångsgrinden** transformerar tillståndet via ett linjärt lager med *tanh*-aktivering och väljer sedan vissa av dess komponenter med hjälp av den dolda vektorn H<sub>i</sub> för att producera ett nytt tillstånd C<sub>i+1</sub>.

Komponenter i tillståndet C kan ses som flaggor som kan slås på och av. Till exempel, när vi stöter på namnet *Alice* i sekvensen, kanske vi vill anta att det hänvisar till en kvinnlig karaktär och höja flaggan i tillståndet att vi har ett kvinnligt substantiv i meningen. När vi senare stöter på frasen *och Tom*, höjer vi flaggan att vi har ett plural substantiv. Genom att manipulera tillståndet kan vi alltså hålla reda på de grammatiska egenskaperna hos meningsdelar.

> ✅ En utmärkt resurs för att förstå LSTM:s interna funktioner är denna fantastiska artikel [Understanding LSTM Networks](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) av Christopher Olah.

## Bidirektionella och flerskikts-RNN

Vi har diskuterat rekurrenta nätverk som arbetar i en riktning, från början av en sekvens till slutet. Det verkar naturligt, eftersom det liknar hur vi läser och lyssnar på tal. Men eftersom vi i många praktiska fall har slumpmässig åtkomst till inmatningssekvensen, kan det vara vettigt att köra rekurrent beräkning i båda riktningarna. Sådana nätverk kallas **bidirektionella** RNN. När vi arbetar med ett bidirektionellt nätverk behöver vi två dolda tillståndsvektorer, en för varje riktning.

Ett rekurrent nätverk, antingen enkelriktat eller bidirektionellt, fångar vissa mönster inom en sekvens och kan lagra dem i en tillståndsvektor eller skicka dem till utdata. Precis som med konvolutionella nätverk kan vi bygga ett annat rekurrent lager ovanpå det första för att fånga högre nivåmönster och bygga från låg-nivåmönster som extraherats av det första lagret. Detta leder oss till begreppet ett **flerskikts-RNN**, som består av två eller fler rekurrenta nätverk, där utdata från det föregående lagret skickas till nästa lager som indata.

![Bild som visar ett flerskikts long-short-term-memory-RNN](../../../../../translated_images/multi-layer-lstm.dd975e29bb2a59fe58b429db833932d734c81f211cad2783797a9608984acb8c.sv.jpg)

*Bild från [detta fantastiska inlägg](https://towardsdatascience.com/from-a-lstm-cell-to-a-multilayer-lstm-network-with-pytorch-2899eb5696f3) av Fernando López*

## ✍️ Övningar: Inbäddningar

Fortsätt ditt lärande i följande anteckningsböcker:

* [RNN med PyTorch](RNNPyTorch.ipynb)
* [RNN med TensorFlow](RNNTF.ipynb)

## Slutsats

I denna enhet har vi sett att RNN kan användas för sekvensklassificering, men de kan faktiskt hantera många fler uppgifter, såsom textgenerering, maskinöversättning och mer. Vi kommer att titta på dessa uppgifter i nästa enhet.

## 🚀 Utmaning

Läs igenom lite litteratur om LSTM och fundera över deras tillämpningar:

- [Grid Long Short-Term Memory](https://arxiv.org/pdf/1507.01526v1.pdf)
- [Show, Attend and Tell: Neural Image Caption
Generation with Visual Attention](https://arxiv.org/pdf/1502.03044v2.pdf)

## [Quiz efter föreläsning](https://ff-quizzes.netlify.app/en/ai/quiz/32)

## Granskning & Självstudier

- [Understanding LSTM Networks](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) av Christopher Olah.

## [Uppgift: Anteckningsböcker](assignment.md)

---

**Ansvarsfriskrivning**:  
Detta dokument har översatts med hjälp av AI-översättningstjänsten [Co-op Translator](https://github.com/Azure/co-op-translator). Även om vi strävar efter noggrannhet, bör du vara medveten om att automatiserade översättningar kan innehålla fel eller felaktigheter. Det ursprungliga dokumentet på dess originalspråk bör betraktas som den auktoritativa källan. För kritisk information rekommenderas professionell mänsklig översättning. Vi ansvarar inte för eventuella missförstånd eller feltolkningar som uppstår vid användning av denna översättning.