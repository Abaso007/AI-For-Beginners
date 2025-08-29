<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "893aa368cb485da704b466a0f3775587",
  "translation_date": "2025-08-29T12:12:33+00:00",
  "source_file": "lessons/6-Other/21-GeneticAlgorithms/README.md",
  "language_code": "id"
}
-->
# Algoritma Genetika

## [Kuis sebelum kuliah](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/121)

**Algoritma Genetika** (GA) didasarkan pada pendekatan **evolusioner** dalam AI, di mana metode evolusi populasi digunakan untuk mendapatkan solusi optimal untuk suatu masalah tertentu. Algoritma ini diusulkan pada tahun 1975 oleh [John Henry Holland](https://wikipedia.org/wiki/John_Henry_Holland).

Algoritma Genetika didasarkan pada ide-ide berikut:

* Solusi yang valid untuk masalah dapat direpresentasikan sebagai **gen**
* **Crossover** memungkinkan kita menggabungkan dua solusi untuk mendapatkan solusi valid baru
* **Seleksi** digunakan untuk memilih solusi yang lebih optimal menggunakan beberapa **fungsi kebugaran**
* **Mutasi** diperkenalkan untuk mengganggu optimasi dan menghindari jebakan pada minimum lokal

Jika Anda ingin mengimplementasikan Algoritma Genetika, Anda memerlukan hal-hal berikut:

* Menemukan metode untuk mengkodekan solusi masalah menggunakan **gen** g∈Γ
* Pada himpunan gen Γ, kita perlu mendefinisikan **fungsi kebugaran** fit: Γ→**R**. Nilai fungsi yang lebih kecil menunjukkan solusi yang lebih baik.
* Mendefinisikan mekanisme **crossover** untuk menggabungkan dua gen menjadi solusi valid baru crossover: Γ<sup>2</sup>→Γ.
* Mendefinisikan mekanisme **mutasi** mutate: Γ→Γ.

Dalam banyak kasus, crossover dan mutasi adalah algoritma sederhana untuk memanipulasi gen sebagai urutan numerik atau vektor bit.

Implementasi spesifik dari algoritma genetika dapat bervariasi dari satu kasus ke kasus lainnya, tetapi struktur umumnya adalah sebagai berikut:

1. Pilih populasi awal G⊂Γ
2. Secara acak pilih salah satu operasi yang akan dilakukan pada langkah ini: crossover atau mutasi
3. **Crossover**:
   * Pilih secara acak dua gen g<sub>1</sub>, g<sub>2</sub> ∈ G
   * Hitung crossover g=crossover(g<sub>1</sub>,g<sub>2</sub>)
   * Jika fit(g)<fit(g<sub>1</sub>) atau fit(g)<fit(g<sub>2</sub>) - ganti gen yang sesuai dalam populasi dengan g.
4. **Mutasi** - pilih gen acak g∈G dan ganti dengan mutate(g)
5. Ulangi dari langkah 2, hingga kita mendapatkan nilai fit yang cukup kecil, atau hingga batas jumlah langkah tercapai.

## Tugas-Tugas Umum

Tugas-tugas yang biasanya diselesaikan dengan Algoritma Genetika meliputi:

1. Optimasi jadwal
1. Pengemasan optimal
1. Pemotongan optimal
1. Mempercepat pencarian menyeluruh

## ✍️ Latihan: Algoritma Genetika

Lanjutkan pembelajaran Anda di notebook berikut:

Kunjungi [notebook ini](Genetic.ipynb) untuk melihat dua contoh penggunaan Algoritma Genetika:

1. Pembagian harta yang adil
1. Masalah 8 Ratu

## Kesimpulan

Algoritma Genetika digunakan untuk menyelesaikan banyak masalah, termasuk logistik dan masalah pencarian. Bidang ini terinspirasi oleh penelitian yang menggabungkan topik dalam Psikologi dan Ilmu Komputer.

## 🚀 Tantangan

"Algoritma genetika mudah diimplementasikan, tetapi perilakunya sulit dipahami." [sumber](https://wikipedia.org/wiki/Genetic_algorithm) Lakukan penelitian untuk menemukan implementasi algoritma genetika seperti menyelesaikan teka-teki Sudoku, dan jelaskan cara kerjanya dalam bentuk sketsa atau diagram alur.

## [Kuis setelah kuliah](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/221)

## Tinjauan & Studi Mandiri

Tonton [video hebat ini](https://www.youtube.com/watch?v=qv6UVOQ0F44) yang membahas bagaimana komputer dapat belajar memainkan Super Mario menggunakan jaringan saraf yang dilatih oleh algoritma genetika. Kita akan mempelajari lebih lanjut tentang komputer yang belajar memainkan permainan seperti itu [di bagian berikutnya](../22-DeepRL/README.md).

## [Tugas: Persamaan Diophantine](Diophantine.ipynb)

Tujuan Anda adalah menyelesaikan apa yang disebut **persamaan Diophantine** - persamaan dengan akar bilangan bulat. Sebagai contoh, pertimbangkan persamaan a+2b+3c+4d=30. Anda perlu menemukan akar bilangan bulat yang memenuhi persamaan ini.

*Tugas ini terinspirasi oleh [postingan ini](https://habr.com/post/128704/).*

Petunjuk:

1. Anda dapat mempertimbangkan akar berada dalam interval [0;30]
1. Sebagai gen, pertimbangkan untuk menggunakan daftar nilai akar

Gunakan [Diophantine.ipynb](Diophantine.ipynb) sebagai titik awal.

---

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan layanan penerjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Meskipun kami berupaya untuk memberikan hasil yang akurat, harap diperhatikan bahwa terjemahan otomatis mungkin mengandung kesalahan atau ketidakakuratan. Dokumen asli dalam bahasa aslinya harus dianggap sebagai sumber yang berwenang. Untuk informasi yang bersifat kritis, disarankan menggunakan jasa penerjemahan manusia profesional. Kami tidak bertanggung jawab atas kesalahpahaman atau penafsiran yang keliru yang timbul dari penggunaan terjemahan ini.