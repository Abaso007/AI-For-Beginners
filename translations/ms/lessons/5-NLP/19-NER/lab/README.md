<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "032bda5068f543d6c1fcb30c34231461",
  "translation_date": "2025-08-29T11:59:43+00:00",
  "source_file": "lessons/5-NLP/19-NER/lab/README.md",
  "language_code": "ms"
}
-->
# NER

Tugasan Makmal daripada [Kurikulum AI untuk Pemula](https://github.com/microsoft/ai-for-beginners).

## Tugasan

Dalam makmal ini, anda perlu melatih model pengenalan entiti bernama untuk istilah perubatan.

## Dataset

Untuk melatih model NER, kita memerlukan dataset yang dilabel dengan betul yang mengandungi entiti perubatan. [Dataset BC5CDR](https://biocreative.bioinformatics.udel.edu/tasks/biocreative-v/track-3-cdr/) mengandungi entiti penyakit dan bahan kimia yang dilabel daripada lebih 1500 kertas kajian. Anda boleh memuat turun dataset ini selepas mendaftar di laman web mereka.

Dataset BC5CDR kelihatan seperti ini:

```
6794356|t|Tricuspid valve regurgitation and lithium carbonate toxicity in a newborn infant.
6794356|a|A newborn with massive tricuspid regurgitation, atrial flutter, congestive heart failure, and a high serum lithium level is described. This is the first patient to initially manifest tricuspid regurgitation and atrial flutter, and the 11th described patient with cardiac disease among infants exposed to lithium compounds in the first trimester of pregnancy. Sixty-three percent of these infants had tricuspid valve involvement. Lithium carbonate may be a factor in the increasing incidence of congenital heart disease when taken during early pregnancy. It also causes neurologic depression, cyanosis, and cardiac arrhythmia when consumed prior to delivery.
6794356	0	29	Tricuspid valve regurgitation	Disease	D014262
6794356	34	51	lithium carbonate	Chemical	D016651
6794356	52	60	toxicity	Disease	D064420
...
```

Dalam dataset ini, terdapat tajuk kertas kajian dan abstrak pada dua baris pertama, dan kemudian terdapat entiti individu, dengan posisi permulaan dan akhir dalam blok tajuk+abstrak. Selain jenis entiti, anda juga mendapat ID ontologi entiti ini dalam beberapa ontologi perubatan.

Anda perlu menulis beberapa kod Python untuk menukar ini kepada pengekodan BIO.

## Rangkaian

Percubaan pertama untuk NER boleh dilakukan dengan menggunakan rangkaian LSTM, seperti dalam contoh yang telah anda lihat semasa pelajaran. Walau bagaimanapun, dalam tugas NLP, [transformer architecture](https://en.wikipedia.org/wiki/Transformer_(machine_learning_model)), dan khususnya [model bahasa BERT](https://en.wikipedia.org/wiki/BERT_(language_model)) menunjukkan hasil yang jauh lebih baik. Model BERT yang telah dilatih memahami struktur umum bahasa, dan boleh disesuaikan untuk tugas tertentu dengan dataset yang agak kecil dan kos pengiraan yang rendah.

Oleh kerana kita merancang untuk menggunakan NER dalam senario perubatan, adalah masuk akal untuk menggunakan model BERT yang dilatih pada teks perubatan. Microsoft Research telah mengeluarkan model pra-latih yang dipanggil [PubMedBERT][PubMedBERT] ([publikasi][PubMedBERT-Pub]), yang telah disesuaikan menggunakan teks daripada repositori [PubMed](https://pubmed.ncbi.nlm.nih.gov/).

Standard *de facto* untuk melatih model transformer ialah perpustakaan [Hugging Face Transformers](https://huggingface.co/). Ia juga mengandungi repositori model pra-latih yang diselenggara oleh komuniti, termasuk PubMedBERT. Untuk memuat dan menggunakan model ini, kita hanya memerlukan beberapa baris kod:

```python
model_name = "microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract"
classes = ... # number of classes: 2*entities+1
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = BertForTokenClassification.from_pretrained(model_name, classes)
```

Ini memberikan kita `model` itu sendiri, yang dibina untuk tugas klasifikasi token menggunakan `classes` bilangan kelas, serta objek `tokenizer` yang boleh memecahkan teks input kepada token. Anda perlu menukar dataset kepada format BIO, dengan mengambil kira tokenisasi PubMedBERT. Anda boleh menggunakan [bahagian kod Python ini](https://gist.github.com/shwars/580b55684be3328eb39ecf01b9cbbd88) sebagai inspirasi.

## Pengajaran

Tugasan ini sangat dekat dengan tugas sebenar yang mungkin anda hadapi jika anda ingin mendapatkan lebih banyak wawasan daripada sejumlah besar teks bahasa semula jadi. Dalam kes kita, kita boleh menggunakan model yang telah dilatih untuk [dataset kertas kajian berkaitan COVID](https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge) dan melihat wawasan apa yang boleh kita peroleh. [Blog post ini](https://soshnikov.com/science/analyzing-medical-papers-with-azure-and-text-analytics-for-health/) dan [kertas kajian ini](https://www.mdpi.com/2504-2289/6/1/4) menerangkan penyelidikan yang boleh dilakukan pada korpus kertas kajian ini menggunakan NER.

---

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan perkhidmatan terjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Walaupun kami berusaha untuk memastikan ketepatan, sila ambil perhatian bahawa terjemahan automatik mungkin mengandungi kesilapan atau ketidaktepatan. Dokumen asal dalam bahasa asalnya harus dianggap sebagai sumber yang berwibawa. Untuk maklumat penting, terjemahan manusia profesional adalah disyorkan. Kami tidak bertanggungjawab atas sebarang salah faham atau salah tafsir yang timbul daripada penggunaan terjemahan ini.