# Ensemble Learning
Ensemble
* Arti kata: Serangkaian, Keseluruhan, Kelompok, Keroyokan --> namun intinya "Berkelompok"
* "Banyak" model
* Bagging, Busting, Pasting, Stacking
* Kita membuat machine learning yang berkelompok

# Ensemble Learning & Random Forest
![[Pasted image 20260602094834.png|680]]
Hasil akhir sebuah model berasal dari berbagai model, lalu dilakukan voting, seperti kasus pada gambar diatas

Bisa dilakukan untuk *Decision Tree* juga, karena cenderung overfitting, kita membuat berbagai *tree*
## Voting pada Esemble Learning
* Default Ensemble Learning: *Hard Voting* --> Memilih berdasarkan suara terbanyak
* Ada juga *Soft Voting* --> Memilih model yang memiliki probabilitas yang paling tinggi yang akan menentukan keputusan akhir, seperti investor yang modalnya paling tinggi, dia yang akan menentukan (jadi bukan yang paling banyak investornya, tapi dari investor yang paling kaya)

## Bagging, and Pasting
Bagging & Pastig in Sckit-Learn, Out-of-Bag evaluation
Itu adalah variasi untuk pengacakan data

Model itu terpengaruh dari keteracakan data

Misal kita punya Training dan Testing = 80% : 20%
keteracakan data dari Training dan Testing itu berasal dari algoritma randomisasi yang digunakan

> [!tip] Pesan Moral
> Meski terdiri dari berbagai model, kita tetap perlu perhatikan nilai keteracakan saat melakukan training dan testing

### Bagging vs Pasting
Bagging (Bootstrap aggregating):
![[Pasted image 20260602095855.png|520]]
1 Training set dapat digunakan untuk digunakan ke dalam banyak model, ketika kita menggunakan *bagging*, maka dalam 1 pelatihan, 1 data yang sama bisa digunakan berkali-kali

Berbeda dengan *Pasting*, 1 data hanya boleh digunakan untuk 1 model

Mana yang kira-kira memiliki performa yang lebih baik? Bootstrap or Pasting?
* Ini terkait dengan variasi, variasinya menjadi terbatas untuk tiap model jika menggunakan konsep pasting, sehingga potensi keberhasilannya dapat menurun
* Secara default saat melakukan *ensemble learning*, kita menggunakan konsep Bootstrap (Bagging)

## Random Forest
Keuntungan menggunakan random forest selain mewakili banyak kebutuhan adalah kita juga bisa menentukan nilai kepentingan dari fitur yang kita miliki dalam dataset

Dalam konsep kecerdasan buatan sekarang, ada konsep yang namanya *Exaplainable AI*, menjelaskan mengapa suatu keputusan itu diambil, salah satu caranya adalah dengan mengetahui *Feature Importance* (nilai kepentingan dari fitur)

![[Pasted image 20260602101306.png|520]]
Dengan kita mengetahui feature importance, kita mengetahui fitur mana yang paling mempengaruhi keputusan

## Boosting, Adaboost, Gradient Boosting, Stacking
Untuk bentuk-bentuk yang sifatnya regresi (menebak nilai, menebak angka)

Algoritma ini melakukan secara incremental, untuk menurunkan RMSE/MAE
![[Pasted image 20260602101109.png|540]]
Perbaikan fungsi yang memprediksi data training, karena itu, konsep Boosting ini cenderung hanya digunakan untuk regresi

Intinya: Memperbaiki fungsi agar mendekati ketersebaran data
### Stacking/Blending
* Stacking: Tahapan training menggunakan *Cross Validation*
* Blending: Bisa menggunakan *Hold Out* biasa

![[Pasted image 20260602101527.png|640]]
Blending itu semacam mengagregasi, menyatukan, tahap yang ada sebelumnya

Istilah Blending juga suka disebut *meta-learning*, model yang ada di atas model lainnya

Ketika kita ingin menggunakan Blending, maka kita perlu mempersiapkan dataset kita agar nantinya itu bisa digunakan di 2 tahap

![[Pasted image 20260602101800.png|640]]
Misal kita ingin melatih 1 Blender, misal kita gunakan
* SVM
* Linear Regression
* Neural Network

Kemudian blending menggunakan algortima lain lagi, misal *Random Forest Regressor*
Jadi komposisi model-modelnya bisa kita asumsikan sendiri

Contoh:
* Subset nomor 2 dipakai untuk melatih yang bagian dasarnya, hasil dari tahap dasar, hasil prediksinya digunakan untuk training model yang diatasnya, ini disebut dengan meta-learning (stacking)
* Intinya: Model mempelajari hasil dari model lain
* Hasilnya tergantung dari pada model yang sebelumnya, jadi jika model sebelumnya ngaco, hasil blending bisa ngaco, tapi jika hasil model sebelumnya sudah baik, maka hasil blendingnya bisa menjadi lebih baik lagi
* Model blending mungkin jadi bisa mempelajari hal yang mungkin sempat terlewat oleh model-model sebelumnya

Jadi dengan demikian, secara teoritis, dengan Blending/Stacking/Meta-Learning, hasilnya menjadi semakin baik

Blending mempelajari target value, yang diberikan oleh prediksi model di lapisan pertama

![[Pasted image 20260602102642.png|600]]
Setiap lapisan *transformer* (ini mirip seperti Neural Model), berdiri sendiri, dan mereka memprediksi hal yang berbeda-beda, lalu mereka disatukan dan menghasilkan keputusan akhir yang menyatukan semua

ChatGPT versi 2 (sekarang tahun 2026 sudah ada versi 5), memiliki sekitar 12 lapisan *transformer*

> [!tip] State of the art
> Meta learning: Model mempelajari hasil dari model lain
> 
> Pendekatan subtil untuk mendapatkan hasil yang baik --> model belajar dari model yang lain

