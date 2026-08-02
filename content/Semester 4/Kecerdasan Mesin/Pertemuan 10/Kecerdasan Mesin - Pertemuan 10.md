# Decision Tree
![[20260512_093848.jpg]]
Kelemahan utama dari Decision Tree adalah **overfitting**

![[Pasted image 20260512094534.png]]
Nilai `Gini` besar = Ketidakmurniannya (*Impurity*) besar

Semakin kecil nilai `Gini`, maka peluang untuk memurnikan suatu keputusan itu semakin besar --> Kemampuan pemisahannya akan semakin tinggi

Nilai `Gini` = 0, artinya sangat murni sekali

Nilai Gini harus menurun setiap kali terjadi percabangan

Kedalaman pohon akan berlanjut semakin banyaknya kelas

Pada kasus ini, class `setosa` murni tidak bisa diganggu gugat, jika `petal length (cm)` $\leq$ 2.45 sudah pasti pasti `setosa`

![[Pasted image 20260512095254.png]]

Jika ingin membuat classifier yang dapat menentukan arah keputusan dan mempertanggunjawabakna arah keputusan, `Tree` adalah algoritmanya

Jadi setiap keputusan itu kelihatan langsung alasannya

Ini disebut dengan `White Box`

![[Pasted image 20260512095358.png]]
Kita dapat mengestimasikan probabilitas kelas dengan menggunakan fungsi `predict_proba()`

![[Pasted image 20260512095511.png]]
Dalam `Sckit-Learn`, secara default, algoritma yang digunakan adalah `CART`, yang secara default akan membangun binary-tree

![[Pasted image 20260512100120.png]]
Pemisahan tree, jika misal kita memiliki N1, N2, N3, Decision
maka Tree paling atas akan menggunakan N1, lalu berikutnya menggunakan N2, dst...

![[Pasted image 20260512100240.png]]
Parameter lain: `Entropy`
Sebenarnya mirip dengan `Gini`, secara rumus, hanya berbeda di $log_2$  $P_{i,k}$

![[Pasted image 20260512100540.png|600]]
![[Pasted image 20260512100608.png|600]]
Dari nilai Entropy 0.9911 awalnya, ini artinya mixing datanya sangat besar sekali
Hair Length $\leq$ 5, angka 5 didapat dari nilai median panjang rambut (`Hair Length`)

Lalu berikutnya setelah pemisahan berdasarkan panjang rambut, masih terjadi percampuran, 0.8113 masih cukup besar, masih ada 1 Female yang masuk, dan 0.9710, artinya percampurannya malah lebih parah

Nilai yang penting adalah `Entropy` dan `Gini`

Bagaimana jika atribut yang digunakan adalah `Weight`:
![[Pasted image 20260512101248.png|600]]

Bagaimana jika atribut yang digunakan adalah `Age`?
![[Pasted image 20260512101344.png|600]]

Jadi, parameter terbaik untuk root adalah `Weight`
![[Pasted image 20260512101511.png|600]]

Tree itu sangat sensitif terhadap overfitting, cenderung tidak berlaku lagi jika datanya berubah, dan sangat rentan terhadap perubahan, karena `Gini` dan `Entropy` berubahah, `Treshold` juga berubah jika kita memasukkan data baru misalnya

Tree itu paling jelas, paling transparan, mengapa suatu keputusan itu diambil, meski sangat rentan terhadap overfitting
## Perbedaan Gini vs Entropy:
![[Pasted image 20260512102317.png]]
![[Pasted image 20260512102112.png]]

Tree itu mudah untuk dibentuk dan digunakan, tetapi bahaya yang paling besar dari tree itu adalah overfitting

bagaimana kita menghasilkan pohon yang lebih general? yang lebih bisa digunakan untuk lebih banyak macam kasus?

![[Pasted image 20260512103942.png]]
Sebenarnya Entropy itu sama saja dengan Gini jika Pi dikuadratkan dan log dihapus
# Hyperparameter Regularisasi Decision Tree
Agar pohon kita tidak terlalu overfit (ada errornya), maka caranya adalah dengan kita mengurangi kedalaman pohon
![[Pasted image 20260512102426.png]]

Hyperparameter penting dalam tree:
![[Pasted image 20260512102514.png]]

Jika area tidak diberikan restriction:
![[Pasted image 20260512102818.png]]
Ada area yang sangat eksklusif, pemisahan pada model yang `no_restriction`, itu sampai sangat detail sekali, ini artinya terjadi **overfitting**
## Regression Tree
Tree bukan hanya klasifikasi, tapi bisa juga melakukan regresi

![[Pasted image 20260512103040.png]]
Semakin tidak murni, ia akan menjadi pemisah yang paling bawah

![[Pasted image 20260512103226.png]]
Terlihat jika tidak ada restriction, Tree memisahkan sampai ke detail-detail terkecil, itu adalah ciri-ciri **overfitting**

## Max_depth
![[Pasted image 20260512103119.png]]
Jika terlihat detail-detail kecil, itu kemungkinan besar terjadi **overfitting**

![[Pasted image 20260512103421.png]]
Pilih *Decision Boundaries* yang lebih menguntungkan, pada kasus ini menggunakan garis horizontal/garis vertikal

kita perlu memiliki nilai acuan yang sama saat bereksperimen, misal `random_state=42`, ini perlu sama

> [!info] fun fact
> Angka `random_state` bebas bulat, angka `42` hanya karena pembuatnya suka dengan angka itu

Misalnya untuk membandingkan 2 algoritma, maka agar training dan testingnya sama antar 2 algoritma, maka `random_state` harus sama agar datanya tidak ngacak, jika tidak sama, maka metrik yang dihasilkan tidak fair/tidak seimbang

