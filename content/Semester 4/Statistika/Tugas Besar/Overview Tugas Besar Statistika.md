# Identitas
**Anggota Kelompok**
1. Richard Vincentius Christian Dinata - 2472007 
2. Christian Anthony Hermawan - 2472008 
3. Miracle Steven Gerrald - 2472019 

Link Canva: [https://canva.link/arpnx7te2itrwnz](https://canva.link/arpnx7te2itrwnz)

---
# Gambaran Umum
**Judul:** Faktor Penentu Penyerapan Tenaga Kerja di Indonesia Tahun 2013-2023

**Latar Belakang:**
* Dinamika pasar tenaga kerja di Indonesia terus berubah seiring dengan perkembangan zaman dan ekonomi
* Terdapat indikasi adanya ketimpangan penyerapan tenaga kerja berdasarkan Gender (laki-laki vs perempuan) dan Tingkat Keahlian (Rendah, Menengah, Tinggi)
* Diperlukan sebuah pembuktian matematis untuk melihat seberapa besar pengaruh variabel-variabel tersebut secara nyata terhadap total pekerja, bukan sekadar asumsi

**Rumusan Masalah:**
* Apakah terdapat diskriminasi penyerapan tenaga kerja berdasarkan gender di Indonesia?
* Seberapa besar pengaruh tingkat keahlian (skill level) terhadap jumlah tenaga kerja yang terserap?
* Bagaimana tren penyerapan tenaga kerja secara keseluruhan dari tahun 2013 hingga 2023

**Tujuan:**
* Mengukur pengaruh rill variabel gender dan tingkat keahlian terhadap penyerapan tenaga kerja.
* Membangun model prediksi statistik yang akurat untuk melihat tren tenaga kerja di masa depan
* Memberikan kesimpulan berbasis data rill (faktual) menggunakan metode statistika inferensi

---
# Direktori:
* [Google Drive Tugas Besar Statistika](https://drive.google.com/drive/folders/12jTQ-fSHeUcRqvhVvmAYHLbWpzUlAbHc)
* [Canva - Presentation](https://canva.link/93m2plt198o9m8n)
* [Dataset Mentah](https://rshiny.ilo.org/dataexplorer43/?lang=en&segment=indicator&id=EMP_TEMP_SEX_AGE_OCU_NB_A&channel=ilostat)

---
# Penjelasan Data:
Dataset: `Employment by sex, age and occupation (thousands) - Annual`
![[Pasted image 20260607214049.png]]

![[WhatsApp Ptt 2026-06-07 at 21.15.40.ogg]]

> [!info] Transcript
> 
> (0:00) Itu tuh maksudnya kalau yang di reference area apa, reference area aja. (0:06) Kalau yang source ini aku kurang tahu sih, soalnya kurang paham. (0:09) Yang pasti tuh kayaknya itu si National Labour Force survey-nya gitu.
> 
> (0:14) Terus kalau yang bagian kolom sekitar itu maksudnya, aku kurang tahu ya itu total. (0:19) Kayak harusnya ada male female-nya gitu kamu bisa sorting gitu. (0:24) Maksudnya ada male, female atau apa gitu lupa.
> 
> (0:28) Kalau yang age itu milihnya, kategori kita anggapnya tuh yang udah cukup umur. (0:36) Sama occupation itu buat sih nilai skill level, pekerjanya dari level 1, 2, 3, 4. (0:45) Atau yang sampe not elsewhere classified gitu, sama ada totalnya. (0:50) Cuman kita ngambilnya cuma 1-4, ngambil total sama not-nya.
> 
> (0:54) Jadi gak dianggap kalau tahunnya tahun, sama itu value sih jumlah pekerjanya.
## Skema dataset
Nested data schema:
```
Year
    Sex
        Not Classified
        1 - Low
        2 - Medium
        3 and 4 - High
```

---
# Pengerjaan Tugas Besar
## Statistik Deskriptif
## Regresi

