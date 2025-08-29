<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "2efbb183384a50f0fc0cde02534d912f",
  "translation_date": "2025-08-29T12:45:45+00:00",
  "source_file": "lessons/5-NLP/20-LangModels/README.md",
  "language_code": "id"
}
-->
# Model Bahasa Berukuran Besar yang Telah Dilatih Sebelumnya

Dalam semua tugas sebelumnya, kita melatih jaringan neural untuk melakukan tugas tertentu menggunakan dataset berlabel. Dengan model transformer besar, seperti BERT, kita menggunakan pemodelan bahasa secara self-supervised untuk membangun model bahasa, yang kemudian disesuaikan untuk tugas spesifik dengan pelatihan lebih lanjut yang berfokus pada domain tertentu. Namun, telah terbukti bahwa model bahasa besar juga dapat menyelesaikan banyak tugas tanpa pelatihan spesifik domain. Keluarga model yang mampu melakukan hal tersebut disebut **GPT**: Generative Pre-Trained Transformer.

## [Kuis Pra-Kuliah](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/120)

## Generasi Teks dan Perplexity

Gagasan bahwa jaringan neural dapat melakukan tugas umum tanpa pelatihan lanjutan diperkenalkan dalam makalah [Language Models are Unsupervised Multitask Learners](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf). Ide utamanya adalah bahwa banyak tugas lain dapat dimodelkan menggunakan **generasi teks**, karena memahami teks pada dasarnya berarti mampu memproduksinya. Karena model dilatih pada sejumlah besar teks yang mencakup pengetahuan manusia, model ini juga menjadi berpengetahuan luas tentang berbagai subjek.

> Memahami dan mampu memproduksi teks juga berarti mengetahui sesuatu tentang dunia di sekitar kita. Orang juga belajar dengan membaca dalam skala besar, dan jaringan GPT serupa dalam hal ini.

Jaringan generasi teks bekerja dengan memprediksi probabilitas kata berikutnya $$P(w_N)$$. Namun, probabilitas tanpa syarat dari kata berikutnya sama dengan frekuensi kata tersebut dalam korpus teks. GPT mampu memberikan **probabilitas bersyarat** dari kata berikutnya, berdasarkan kata-kata sebelumnya: $$P(w_N | w_{n-1}, ..., w_0)$$

> Anda dapat membaca lebih lanjut tentang probabilitas dalam [Kurikulum Data Science untuk Pemula](https://github.com/microsoft/Data-Science-For-Beginners/tree/main/1-Introduction/04-stats-and-probability).

Kualitas model generasi bahasa dapat didefinisikan menggunakan **perplexity**. Ini adalah metrik intrinsik yang memungkinkan kita mengukur kualitas model tanpa dataset spesifik tugas. Metrik ini didasarkan pada konsep *probabilitas sebuah kalimat* - model memberikan probabilitas tinggi pada kalimat yang kemungkinan besar nyata (yaitu model tidak **bingung** olehnya), dan probabilitas rendah pada kalimat yang kurang masuk akal (misalnya, *Bisakah itu melakukan apa?*). Ketika kita memberikan model kita kalimat dari korpus teks nyata, kita mengharapkan mereka memiliki probabilitas tinggi, dan **perplexity** rendah. Secara matematis, ini didefinisikan sebagai probabilitas terbalik yang dinormalisasi dari set pengujian:
$$
\mathrm{Perplexity}(W) = \sqrt[N]{1\over P(W_1,...,W_N)}
$$ 

**Anda dapat bereksperimen dengan generasi teks menggunakan [editor teks berbasis GPT dari Hugging Face](https://transformer.huggingface.co/doc/gpt2-large)**. Dalam editor ini, Anda mulai menulis teks Anda, dan menekan **[TAB]** akan menawarkan beberapa opsi pelengkapan. Jika opsi tersebut terlalu pendek, atau Anda tidak puas dengannya - tekan [TAB] lagi, dan Anda akan mendapatkan lebih banyak opsi, termasuk potongan teks yang lebih panjang.

## GPT adalah Sebuah Keluarga

GPT bukanlah satu model tunggal, melainkan kumpulan model yang dikembangkan dan dilatih oleh [OpenAI](https://openai.com). 

Di bawah model GPT, kita memiliki:

| [GPT-2](https://huggingface.co/docs/transformers/model_doc/gpt2#openai-gpt2) | [GPT-3](https://openai.com/research/language-models-are-few-shot-learners) | [GPT-4](https://openai.com/gpt-4) |
| -- | -- | -- |
|Model bahasa dengan hingga 1,5 miliar parameter. | Model bahasa dengan hingga 175 miliar parameter | 100T parameter dan menerima input berupa gambar dan teks serta menghasilkan output berupa teks. |

Model GPT-3 dan GPT-4 tersedia [sebagai layanan kognitif dari Microsoft Azure](https://azure.microsoft.com/en-us/services/cognitive-services/openai-service/#overview?WT.mc_id=academic-77998-cacaste), dan sebagai [API OpenAI](https://openai.com/api/).

## Rekayasa Prompt

Karena GPT telah dilatih pada volume data yang sangat besar untuk memahami bahasa dan kode, model ini memberikan output sebagai respons terhadap input (prompt). Prompt adalah input atau kueri untuk GPT di mana seseorang memberikan instruksi kepada model tentang tugas yang akan diselesaikan berikutnya. Untuk mendapatkan hasil yang diinginkan, Anda memerlukan prompt yang paling efektif, yang melibatkan pemilihan kata, format, frasa, atau bahkan simbol yang tepat. Pendekatan ini disebut [Rekayasa Prompt](https://learn.microsoft.com/en-us/shows/ai-show/the-basics-of-prompt-engineering-with-azure-openai-service?WT.mc_id=academic-77998-bethanycheum).

[Dokumentasi ini](https://learn.microsoft.com/en-us/semantic-kernel/prompt-engineering/?WT.mc_id=academic-77998-bethanycheum) memberikan informasi lebih lanjut tentang rekayasa prompt.

## ✍️ Notebook Contoh: [Bermain dengan OpenAI-GPT](GPT-PyTorch.ipynb)

Lanjutkan pembelajaran Anda di notebook berikut:

* [Menghasilkan teks dengan OpenAI-GPT dan Hugging Face Transformers](GPT-PyTorch.ipynb)

## Kesimpulan

Model bahasa umum yang telah dilatih sebelumnya tidak hanya memodelkan struktur bahasa, tetapi juga mengandung sejumlah besar bahasa alami. Oleh karena itu, model ini dapat digunakan secara efektif untuk menyelesaikan beberapa tugas NLP dalam pengaturan zero-shot atau few-shot.

## [Kuis Pasca-Kuliah](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/220)

---

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan layanan penerjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Meskipun kami berusaha untuk memberikan hasil yang akurat, harap diingat bahwa terjemahan otomatis mungkin mengandung kesalahan atau ketidakakuratan. Dokumen asli dalam bahasa aslinya harus dianggap sebagai sumber yang otoritatif. Untuk informasi yang bersifat kritis, disarankan menggunakan jasa penerjemahan profesional oleh manusia. Kami tidak bertanggung jawab atas kesalahpahaman atau penafsiran yang timbul dari penggunaan terjemahan ini.