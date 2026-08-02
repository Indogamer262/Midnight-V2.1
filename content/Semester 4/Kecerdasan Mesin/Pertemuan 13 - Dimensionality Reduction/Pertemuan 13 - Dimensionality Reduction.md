Kata-kata itu tidak terhitung, dari ribuan kata atau jutaan kata, mana kata-kata yang bisa kita anggap penting tapi tidak harus kita pilih katanya?

Misal dari 10.000 kata, kita proyeksikan ke dalam suatu ruang fitur tertentu --> Mereduksi ruang dimensi

![[Pasted image 20260602103714.png|540]]
PCA (Principal Component Analysis) adalah suatu algoritma pereduksi ruang dimensi yang populer dan sering digunakan
* Konsep aljabar linear yang digunakan dalam PCA adalah `Eigen Problem`

> [!info] Visualizing PCA
> ![](https://youtu.be/nEvKduLXFvk?si=qMj4ThVKaLXaMWNF)
> [View on YouTube](https://youtu.be/nEvKduLXFvk?si=qMj4ThVKaLXaMWNF)

Bagaimana kita memproyeksikan data 2 dimensi ke dalam suatu ruang vektor baru 1 dimensi, martriks echelon pasti tegak lurus dengan nilai matriks awal

Kita dapat memiliki sangat banyak Principal Component, sebanyak yang kita inginkan, meski biasanya hanya 2
## Hyperparameter
![[Pasted image 20260602104852.png|540]]
Hyperparameter utama: `n_components`, semakin banyak komponen, semakin mendekati realita (`n_components` menentukan rasio persebaran yang mau dipertahankan)

> [!tip] Inti
> Inti dari Reduksi Dimensi yang akan kita pelajari adalah algoritma PCA.
> gambaran dari proses PCA dapat dilihat dari video yang tersedia

*Dimensionality Reduction* digunakan agar data itu tidak terlalu besar, untuk memperingkas proses learningnya
* Jadi, bagi yang memiliki data Image atau data tabular dengan fitur yang sangat banyak, reduksi dimensi dapat digunakan agar proses learning menjadi lebih cepat

