<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "bd10f434e444bce61b7f97eeb1ff6a55",
  "translation_date": "2025-08-28T02:43:25+00:00",
  "source_file": "lessons/5-NLP/19-NER/README.md",
  "language_code": "tl"
}
-->
# Named Entity Recognition

Hanggang ngayon, karamihan sa ating pokus ay nasa isang NLP task - ang classification. Gayunpaman, may iba pang mga NLP task na maaaring magawa gamit ang neural networks. Isa sa mga task na ito ay ang **[Named Entity Recognition](https://wikipedia.org/wiki/Named-entity_recognition)** (NER), na tumutukoy sa pagkilala ng mga partikular na entidad sa loob ng teksto, tulad ng mga lugar, pangalan ng tao, mga petsa, chemical formula, at iba pa.

## [Pre-lecture quiz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/119)

## Halimbawa ng Paggamit ng NER

Halimbawa, nais mong gumawa ng natural language chat bot, katulad ng Amazon Alexa o Google Assistant. Ang paraan ng paggana ng mga intelligent chat bot ay ang *pag-unawa* sa nais ng user sa pamamagitan ng text classification sa input na pangungusap. Ang resulta ng classification na ito ay tinatawag na **intent**, na tumutukoy kung ano ang dapat gawin ng chat bot.

<img alt="Bot NER" src="images/bot-ner.png" width="50%"/>

> Larawan mula sa may-akda

Gayunpaman, maaaring magbigay ang user ng ilang mga parameter bilang bahagi ng parirala. Halimbawa, kapag nagtatanong tungkol sa panahon, maaaring tukuyin niya ang lokasyon o petsa. Dapat maunawaan ng bot ang mga entidad na ito, at punan ang mga parameter slots nang naaayon bago isagawa ang aksyon. Dito pumapasok ang NER.

> ✅ Isa pang halimbawa ay [ang pagsusuri ng mga siyentipikong medikal na papel](https://soshnikov.com/science/analyzing-medical-papers-with-azure-and-text-analytics-for-health/). Isa sa mga pangunahing bagay na kailangang hanapin ay ang mga partikular na medikal na termino, tulad ng mga sakit at medikal na sangkap. Habang ang maliit na bilang ng mga sakit ay maaaring makuha gamit ang substring search, ang mas kumplikadong mga entidad, tulad ng mga chemical compound at pangalan ng gamot, ay nangangailangan ng mas masalimuot na paraan.

## NER bilang Token Classification

Ang mga NER model ay mahalagang **token classification models**, dahil para sa bawat input token, kailangan nating tukuyin kung ito ay kabilang sa isang entidad o hindi, at kung oo - sa anong klase ng entidad.

Isaalang-alang ang pamagat ng papel na ito:

**Tricuspid valve regurgitation** at **lithium carbonate** **toxicity** sa isang bagong-silang na sanggol.

Ang mga entidad dito ay:

* Ang Tricuspid valve regurgitation ay isang sakit (`DIS`)
* Ang Lithium carbonate ay isang chemical substance (`CHEM`)
* Ang Toxicity ay isa ring sakit (`DIS`)

Pansinin na ang isang entidad ay maaaring binubuo ng ilang mga token. At, tulad ng sa kasong ito, kailangan nating tukuyin ang pagitan ng dalawang magkasunod na entidad. Kaya't karaniwan ang paggamit ng dalawang klase para sa bawat entidad - isa na tumutukoy sa unang token ng entidad (madalas ginagamit ang prefix na `B-` para sa **b**eginning), at isa pa - ang pagpapatuloy ng entidad (`I-`, para sa **i**nner token). Ginagamit din natin ang `O` bilang klase upang kumatawan sa lahat ng **o**ther tokens. Ang ganitong token tagging ay tinatawag na [BIO tagging](https://en.wikipedia.org/wiki/Inside%E2%80%93outside%E2%80%93beginning_(tagging)) (o IOB). Kapag na-tag, ganito ang magiging hitsura ng pamagat:

Token | Tag
------|-----
Tricuspid | B-DIS
valve | I-DIS
regurgitation | I-DIS
and | O
lithium | B-CHEM
carbonate | I-CHEM
toxicity | B-DIS
in | O
a | O
newborn | O
infant | O
. | O

Dahil kailangan nating bumuo ng one-to-one na kaugnayan sa pagitan ng mga token at klase, maaari tayong mag-train ng isang **many-to-many** neural network model mula sa larawang ito:

![Image showing common recurrent neural network patterns.](../../../../../translated_images/unreasonable-effectiveness-of-rnn.541ead816778f42dce6c42d8a56c184729aa2378d059b851be4ce12b993033df.tl.jpg)

> *Larawan mula sa [blog post na ito](http://karpathy.github.io/2015/05/21/rnn-effectiveness/) ni [Andrej Karpathy](http://karpathy.github.io/). Ang mga NER token classification models ay tumutugma sa pinakakanan na network architecture sa larawang ito.*

## Pagsasanay ng NER Models

Dahil ang isang NER model ay mahalagang isang token classification model, maaari nating gamitin ang RNNs na pamilyar na tayo para sa task na ito. Sa kasong ito, ang bawat block ng recurrent network ay magbabalik ng token ID. Ang sumusunod na notebook ay nagpapakita kung paano mag-train ng LSTM para sa token classification.

## ✍️ Mga Halimbawa ng Notebook: NER

Ipagpatuloy ang iyong pag-aaral sa sumusunod na notebook:

* [NER gamit ang TensorFlow](NER-TF.ipynb)

## Konklusyon

Ang isang NER model ay isang **token classification model**, na nangangahulugang maaari itong gamitin upang magsagawa ng token classification. Ito ay isang karaniwang task sa NLP, na tumutulong sa pagkilala ng mga partikular na entidad sa loob ng teksto kabilang ang mga lugar, pangalan, petsa, at iba pa.

## 🚀 Hamon

Kumpletuhin ang assignment na naka-link sa ibaba upang mag-train ng named entity recognition model para sa mga medikal na termino, pagkatapos subukan ito sa ibang dataset.

## [Post-lecture quiz](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/219)

## Review & Self Study

Basahin ang blog na [The Unreasonable Effectiveness of Recurrent Neural Networks](http://karpathy.github.io/2015/05/21/rnn-effectiveness/) at sundan ang Further Reading section sa artikulong iyon upang palalimin ang iyong kaalaman.

## [Assignment](lab/README.md)

Sa assignment para sa araling ito, kailangan mong mag-train ng medical entity recognition model. Maaari kang magsimula sa pag-train ng LSTM model tulad ng inilarawan sa araling ito, at magpatuloy sa paggamit ng BERT transformer model. Basahin ang [mga instruksyon](lab/README.md) upang makuha ang lahat ng detalye.

---

**Paunawa**:  
Ang dokumentong ito ay isinalin gamit ang AI translation service na [Co-op Translator](https://github.com/Azure/co-op-translator). Bagama't sinisikap naming maging tumpak, tandaan na ang mga awtomatikong pagsasalin ay maaaring maglaman ng mga pagkakamali o hindi pagkakatugma. Ang orihinal na dokumento sa kanyang katutubong wika ang dapat ituring na opisyal na sanggunian. Para sa mahalagang impormasyon, inirerekomenda ang propesyonal na pagsasalin ng tao. Hindi kami mananagot sa anumang hindi pagkakaunawaan o maling interpretasyon na maaaring magmula sa paggamit ng pagsasaling ito.