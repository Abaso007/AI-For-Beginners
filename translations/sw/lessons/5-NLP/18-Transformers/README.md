<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "7e617f0b8de85a43957a853aba09bfeb",
  "translation_date": "2025-08-25T21:59:17+00:00",
  "source_file": "lessons/5-NLP/18-Transformers/README.md",
  "language_code": "sw"
}
-->
# Mbinu za Uangalizi na Transformers

## [Jaribio la awali ya somo](https://ff-quizzes.netlify.app/en/ai/quiz/35)

Moja ya matatizo muhimu zaidi katika uwanja wa NLP ni **tafsiri ya mashine**, kazi muhimu inayotumika katika zana kama Google Translate. Katika sehemu hii, tutazingatia tafsiri ya mashine, au kwa ujumla zaidi, kazi yoyote ya *mlolongo-kwa-mlolongo* (ambayo pia inaitwa **sentence transduction**).

Kwa kutumia RNNs, mlolongo-kwa-mlolongo unatekelezwa na mitandao miwili ya kurudia, ambapo mtandao mmoja, **encoder**, unafupisha mlolongo wa pembejeo katika hali ya siri, wakati mtandao mwingine, **decoder**, unafungua hali hiyo ya siri kuwa matokeo yaliyotafsiriwa. Kuna matatizo kadhaa na mbinu hii:

* Hali ya mwisho ya mtandao wa encoder ina ugumu wa kukumbuka mwanzo wa sentensi, hivyo kusababisha ubora duni wa modeli kwa sentensi ndefu.
* Maneno yote katika mlolongo yana athari sawa kwenye matokeo. Kwa kweli, hata hivyo, maneno maalum katika mlolongo wa pembejeo mara nyingi yana athari kubwa zaidi kwenye matokeo ya mlolongo kuliko mengine.

**Mbinu za Uangalizi** zinatoa njia ya kupima athari ya muktadha wa kila vector ya pembejeo kwenye kila utabiri wa matokeo wa RNN. Njia inavyotekelezwa ni kwa kuunda njia za mkato kati ya hali za kati za RNN ya pembejeo na RNN ya matokeo. Kwa njia hii, tunapozalisha alama ya matokeo y<sub>t</sub>, tutazingatia hali zote za siri za pembejeo h<sub>i</sub>, kwa kutumia viwango tofauti vya uzito α<sub>t,i</sub>.

![Picha inayoonyesha modeli ya encoder/decoder na safu ya uangalizi wa kuongeza](../../../../../translated_images/encoder-decoder-attention.7a726296894fb567aa2898c94b17b3289087f6705c11907df8301df9e5eeb3de.sw.png)

> Modeli ya encoder-decoder na mbinu ya uangalizi wa kuongeza katika [Bahdanau et al., 2015](https://arxiv.org/pdf/1409.0473.pdf), iliyotajwa kutoka [blogu hii](https://lilianweng.github.io/lil-log/2018/06/24/attention-attention.html)

Matriki ya uangalizi {α<sub>i,j</sub>} ingeonyesha kiwango ambacho maneno fulani ya pembejeo yanachangia katika uzalishaji wa neno fulani katika mlolongo wa matokeo. Hapa chini kuna mfano wa matriki kama hiyo:

![Picha inayoonyesha mpangilio wa mfano uliopatikana na RNNsearch-50, iliyochukuliwa kutoka Bahdanau - arviz.org](../../../../../translated_images/bahdanau-fig3.09ba2d37f202a6af11de6c82d2d197830ba5f4528d9ea430eb65fd3a75065973.sw.png)

> Mchoro kutoka [Bahdanau et al., 2015](https://arxiv.org/pdf/1409.0473.pdf) (Fig.3)

Mbinu za uangalizi zinahusika na sehemu kubwa ya hali ya sanaa ya sasa au karibu ya sasa katika NLP. Hata hivyo, kuongeza uangalizi huongeza sana idadi ya vigezo vya modeli, jambo ambalo lilisababisha changamoto za kupanua RNNs. Kizuizi kikuu cha kupanua RNNs ni kwamba asili ya kurudia ya modeli inafanya iwe changamoto kuunda vikundi na kuendesha mafunzo kwa sambamba. Katika RNN, kila kipengele cha mlolongo kinahitaji kusindika kwa mpangilio wa mlolongo, jambo ambalo lina maana kuwa haliwezi kuendesha kwa urahisi kwa sambamba.

![Encoder Decoder na Uangalizi](../../../../../lessons/5-NLP/18-Transformers/images/EncDecAttention.gif)

> Mchoro kutoka [Blogu ya Google](https://research.googleblog.com/2016/09/a-neural-network-for-machine.html)

Kupitishwa kwa mbinu za uangalizi pamoja na kizuizi hiki kulisababisha kuundwa kwa modeli za Transformer za hali ya sanaa tunazozijua na kuzitumia leo kama BERT hadi Open-GPT3.

## Modeli za Transformer

Moja ya mawazo makuu nyuma ya transformers ni kuepuka asili ya mlolongo ya RNNs na kuunda modeli inayoweza kuendesha kwa sambamba wakati wa mafunzo. Hii inafanikiwa kwa kutekeleza mawazo mawili:

* usimbaji wa nafasi
* kutumia mbinu ya uangalizi wa kibinafsi ili kunasa mifumo badala ya RNNs (au CNNs) (ndiyo sababu karatasi inayotambulisha transformers inaitwa *[Attention is all you need](https://arxiv.org/abs/1706.03762)*)

### Usimbaji/Embedding wa Nafasi

Wazo la usimbaji wa nafasi ni kama ifuatavyo.  
1. Wakati wa kutumia RNNs, nafasi ya jamaa ya tokeni inawakilishwa na idadi ya hatua, na hivyo haitaji kuwakilishwa wazi.  
2. Hata hivyo, mara tu tunapobadilisha kwenda uangalizi, tunahitaji kujua nafasi za jamaa za tokeni ndani ya mlolongo.  
3. Ili kupata usimbaji wa nafasi, tunaongeza mlolongo wetu wa tokeni na mlolongo wa nafasi za tokeni katika mlolongo (yaani, mlolongo wa namba 0,1, ...).  
4. Kisha tunachanganya nafasi ya tokeni na vector ya embedding ya tokeni. Ili kubadilisha nafasi (namba kamili) kuwa vector, tunaweza kutumia mbinu tofauti:

* Embedding inayoweza kufundishwa, sawa na embedding ya tokeni. Hii ndiyo mbinu tunayoangalia hapa. Tunatumia safu za embedding juu ya tokeni na nafasi zao, na kusababisha vector za embedding za vipimo sawa, ambazo tunaziongeza pamoja.  
* Kazi ya usimbaji wa nafasi isiyobadilika, kama ilivyopendekezwa katika karatasi ya awali.

<img src="images/pos-embedding.png" width="50%"/>

> Picha na mwandishi

Matokeo tunayopata na embedding ya nafasi yanajumuisha tokeni asili na nafasi yake ndani ya mlolongo.

### Uangalizi wa Kibinafsi wa Vichwa Vingi

Kisha, tunahitaji kunasa mifumo fulani ndani ya mlolongo wetu. Ili kufanya hivyo, transformers hutumia mbinu ya **uangalizi wa kibinafsi**, ambayo kimsingi ni uangalizi unaotumika kwa mlolongo huo huo kama pembejeo na matokeo. Kutumia uangalizi wa kibinafsi kunatuwezesha kuzingatia **muktadha** ndani ya sentensi, na kuona ni maneno gani yanayohusiana. Kwa mfano, inatuwezesha kuona ni maneno gani yanayorejelewa na marejeleo, kama *it*, na pia kuzingatia muktadha:

![](../../../../../translated_images/CoreferenceResolution.861924d6d384a7d68d8d0039d06a71a151f18a796b8b1330239d3590bd4947eb.sw.png)

> Picha kutoka [Blogu ya Google](https://research.googleblog.com/2017/08/transformer-novel-neural-network.html)

Katika transformers, tunatumia **Uangalizi wa Vichwa Vingi** ili kutoa nguvu kwa mtandao kunasa aina tofauti za utegemezi, mfano uhusiano wa maneno wa muda mrefu dhidi ya wa muda mfupi, marejeleo dhidi ya kitu kingine, n.k.

[Notebook ya TensorFlow](../../../../../lessons/5-NLP/18-Transformers/TransformersTF.ipynb) ina maelezo zaidi juu ya utekelezaji wa safu za transformer.

### Uangalizi wa Encoder-Decoder

Katika transformers, uangalizi hutumika katika sehemu mbili:

* Kunasa mifumo ndani ya maandishi ya pembejeo kwa kutumia uangalizi wa kibinafsi.
* Kufanya tafsiri ya mlolongo - ni safu ya uangalizi kati ya encoder na decoder.

Uangalizi wa encoder-decoder ni sawa sana na mbinu ya uangalizi inayotumika katika RNNs, kama ilivyoelezwa mwanzoni mwa sehemu hii. Mchoro huu wa uhuishaji unaelezea jukumu la uangalizi wa encoder-decoder.

![GIF ya uhuishaji inayoonyesha jinsi tathmini zinavyofanywa katika modeli za transformer.](../../../../../lessons/5-NLP/18-Transformers/images/transformer-animated-explanation.gif)

Kwa kuwa kila nafasi ya pembejeo inalinganishwa kwa uhuru na kila nafasi ya matokeo, transformers zinaweza kuendesha kwa sambamba vizuri zaidi kuliko RNNs, jambo ambalo linawezesha modeli kubwa zaidi na zenye kuelezea zaidi za lugha. Kila kichwa cha uangalizi kinaweza kutumika kujifunza uhusiano tofauti kati ya maneno, jambo ambalo linaboresha kazi za usindikaji wa lugha asilia.

## BERT

**BERT** (Bidirectional Encoder Representations from Transformers) ni mtandao mkubwa wa transformer wenye tabaka nyingi, na tabaka 12 kwa *BERT-base*, na 24 kwa *BERT-large*. Modeli hii kwanza inafundishwa awali kwenye hifadhidata kubwa ya maandishi (WikiPedia + vitabu) kwa kutumia mafunzo yasiyo ya kusimamiwa (kutabiri maneno yaliyofichwa katika sentensi). Wakati wa mafunzo ya awali, modeli inachukua viwango vikubwa vya uelewa wa lugha ambavyo vinaweza kutumika na hifadhidata nyingine kwa kutumia marekebisho. Mchakato huu unaitwa **transfer learning**.

![picha kutoka http://jalammar.github.io/illustrated-bert/](../../../../../translated_images/jalammarBERT-language-modeling-masked-lm.34f113ea5fec4362e39ee4381aab7cad06b5465a0b5f053a0f2aa05fbe14e746.sw.png)

> Picha [chanzo](http://jalammar.github.io/illustrated-bert/)

## ✍️ Mazoezi: Transformers

Endelea kujifunza katika vitabu vya mazoezi vifuatavyo:

* [Transformers katika PyTorch](../../../../../lessons/5-NLP/18-Transformers/TransformersPyTorch.ipynb)
* [Transformers katika TensorFlow](../../../../../lessons/5-NLP/18-Transformers/TransformersTF.ipynb)

## Hitimisho

Katika somo hili umejifunza kuhusu Transformers na Mbinu za Uangalizi, zana muhimu katika kisanduku cha zana cha NLP. Kuna tofauti nyingi za usanifu wa Transformer ikiwa ni pamoja na BERT, DistilBERT, BigBird, OpenGPT3 na zaidi ambazo zinaweza kurekebishwa. [Kifurushi cha HuggingFace](https://github.com/huggingface/) kinatoa hifadhi ya mafunzo ya usanifu nyingi hizi kwa kutumia PyTorch na TensorFlow.

## 🚀 Changamoto

## [Jaribio la baada ya somo](https://ff-quizzes.netlify.app/en/ai/quiz/36)

## Mapitio na Kujisomea

* [Blogu ya maelezo](https://mchromiak.github.io/articles/2017/Sep/12/Transformer-Attention-is-all-you-need/), inayoelezea karatasi ya kawaida [Attention is all you need](https://arxiv.org/abs/1706.03762) kuhusu transformers.
* [Mfululizo wa blogu](https://towardsdatascience.com/transformers-explained-visually-part-1-overview-of-functionality-95a6dd460452) kuhusu transformers, unaoelezea usanifu kwa undani.

## [Kazi ya nyumbani](assignment.md)

**Kanusho**:  
Hati hii imetafsiriwa kwa kutumia huduma ya tafsiri ya AI [Co-op Translator](https://github.com/Azure/co-op-translator). Ingawa tunajitahidi kuhakikisha usahihi, tafadhali fahamu kuwa tafsiri za kiotomatiki zinaweza kuwa na makosa au kutokuwa sahihi. Hati ya asili katika lugha yake ya awali inapaswa kuzingatiwa kama chanzo cha mamlaka. Kwa taarifa muhimu, tafsiri ya kitaalamu ya binadamu inapendekezwa. Hatutawajibika kwa kutoelewana au tafsiri zisizo sahihi zinazotokana na matumizi ya tafsiri hii.