Supervised (Diawasi) --> Classification Label
Unsupervised learning --> Clustering

Vector
* Teks
* Gambar
* Video

Embeddings

> [!info] Info
> Machine learning tidak dapat melakukan apa-apa jika datanya tidak berubah ke dalam bentuk angka. Semua data akan dijadikan angka terlebih dahulu, baik teks maupun gambar, akan diubah menjadi angka, pada gambar setiap pikselnya menjadi angka

Setelah data berbentuk angka, barulah supervised atau unsupervised learning dapat dilakukan

Unsupervised learning bukan benar-benar "belajar", tetapi mengelompokkan

Saat kita melakukan unsupervised learning, kita mencoba untuk menganalisis ciri dari setiap cluster tersebut, sehingga dataset yang kita miliki bisa saja memiliki kecenderungan terhadap hal-hal yang mungkin luput dari pengamatan kia kalau kita sekedar hanya mengamati deretan angka-angka

Anggaplah kita punya 30 atribut, jika kita amati itu satu-satu yah cape, jadi agar kita bisa mengamati bagaimana karakteristik data itu terjadi, kita bisa melakukan *clustering*

Dengan begitu kita dapat menganalisis cluster tersebut, bisa saja kita gunakan untuk kita memperbaiki label

Karena kadang manusia itu tidak konsisten dalam memberikan label, manusia mudah lelah, bisa saja kelasnya tidak konsisten karena lelah itu (digunakan untuk memvalidasi label, apakah karakteristik data itu apakah sudah sesuai denga label yang diberikan atau belum)

Hal-hal lain yang dapat dilakukan dengan **Unsupervised Learning** adalah
* Anomaly detection
  Kita bisa mendeteksi data yang akan menimbulkan problem saat kita ingin membangun model klasifikasi, salah satunya data yang berada di *boundary*/perbatasan
* Density estimation
# Semi-Supervised Learning
Unsupervised learning juga dapat digunakan apabila dataset kita labelnya tidak penuh, jadi andaikata hanya ada 800 label pada dataset 1000 data, jadi ada 200 data yang belum berlabel, nah, dengan clustering, data tanpa label tersebut bisa masuk ke dalam salah satu cluster tersebut, dan dengan begitu data dapat diberi label dengan ciri dari cluster tersebut. Sehinga data yang tadinya tidak ada label, kita bisa propagasikan dengan cluster yanga ada, dengan demikian data itu akan memiliki label --> ini disebut **semi-supervised learning**

# Clustering
![[Pasted image 20260609095740.png|600]]
Ketika kita melihat bahwa ada data yang sangat beririsan antara satu cluster dengan cluster lainnya, yang datanya ada di *boundary*/perbatasan itu, tentu akan perlu manusia yang "expert" untuk menentukan data itu sebaiknya masuk ke dalam *class* yang mana

Ada berbagai macam algoritma yang dapat dimanfaatkan untuk melakukan clustering adalah
# K-Means (Kluster - Rata-Rata)
![[Pasted image 20260609100023.png|600]]
Pembentukan cluster ini tentu saja akan tergantung sekali dengan asumsi kita, kenapa `K=5`, kenapa tidak 7 kenapa tidak 3? kita harus mengira-ngira kira-kira ada berapa cluster yang diperlukan untuk merepresentasikan data kita
 
Bagaimana jika ternyata ada area yang kita perlu lakukan analisis lebih dalam di daerah perbatasan/*boundary*, dengan begitu, kita dapat mencoba untuk menurunkan nilai K misalnya menjadi 4, dengan begitu clusternya akan berbeda, akan ada yang menyatu, atau kita coba menaikan nilai K-nya jadinya akan terbentuk cluster baru, jadi dengan begitu, harapannya irisan cluster bisa menjadi lebih kecil
  
Saat melakukan *clustering*, cluster yang lebih baik adalah cluster yang lebih padat (datanya makin menyatu) atau yang lebih longgar (lebih tersebar), untuk memastikan cluster kita baik, maka mana yang lebih baik densitasnya? yang **kerapatannya tinggi**, yang hubungannya erat, dengan begitu karakteristiknya semakin kuat.
  
Semakin menyebar datanya, lebih tinggi juga kemungkinan errornya. Semakin tinggi nilai kerapatan, semakin kuat karakteristik data di dataset. Jadi dengan nilai density kita dapat mengetahui apakah modelnya sudah baik atau belum

![[Pasted image 20260609100945.png|600]]

Setiap cluster akan memiliki *core*/titik pusat, dengan begitu kita dapat menghitung nilai titik terjauh ke pusat, *max distance* itu, semakin 1 cluster itu memiliki anomali, maka kita dapat memprediksi densitas, di mana densitas itu akan semakin rendah apabila *max distance*-nya besar

![[Pasted image 20260609101811.png|600]]

Ini adalah problem kedua setelah kita menentukan jumlah K, jadi kita harusnya menentukan juga centroid/titik awal, jadi selain mengatur nilai K, kita juga mengubah nilai inisiasi Centroid apabila perlu, nilai random state juga perlu ditentukan agar keteracakan data awalnya sama meski algoritma dijalankan di waktu yang berbeda atau di tempat lain

Semakin besar nilai K, asumsinya data kita akan semakin detail pengelempokannya, tetapi tidak masuk akal juga apabila nilai K sesuai dengan jumlah fitur kita

Beberapa cara untuk menentukan nilai K adalah dengan cara berikut
## Finding the optimal number of cluster
### Elbow Method
![[Pasted image 20260609102345.png|600]]
![[Pasted image 20260609102357.png|600]]
Kita dapat menggunakan Elbow method untuk menentukan nilai optimal dari K, saat siku tersebut memiliki perbedaan sudut yang paling besar terhadap yang sebelumnya, mana yang paling tinggi, itu menjadi titik sikunya, titik asumsi jumlah K yang optimal
### Silhouette score
![[Pasted image 20260609102553.png|600]]
Dengan silhouette score yang paling tinggi, itu adalah asumsi nilai K kita

![[Pasted image 20260609102736.png|600]]
Kita dapat menggunakan *silhouette coefficcient* untuk memastikan lebih jauh apakah K yang tadi kita tentukan sudah merupakan nilai K yang terbaik atau belum.

Kita melihat perbandingan *density* dari masing-masing nilai K tersebut
## Limits of K-Means
K-Means punya batasan atau kelemahan bagi data yang bentuknya tidak bulat, contohnya apabila datanya itu terlihat pipih/elips, K-Means tidak akan cocok, makannya penting untuk melihat EDA, untuk menentukan apakah datanya sudah pas atau belum

![[Pasted image 20260609103410.png|600]]
## Cara kerja K-Means
PDF: [[Chapter09-k-means-example.pdf]]
![[Chapter09-k-means-example.pdf]]

Dengan cara kerja yang demikian, maka `K-Means` akan memiliki nilai kompleksitas yang sangat tinggi

Ini adalah kelemahan utama `K-Means`, yaitu kita boleh bebas berasumsi berapa nilai `K` yang menurut kita baik, meski ada cara efektifnya yaitu dengan sihloutte score tadi atau elbow method tadi.

Kita telah mengasumsikan bahwa `K=3`, dengan begitu ditentukan seed (nilai centroid awal)

Jika kita tidak menentukan titik awal centroid, maka resikonya, setiap perbedaan titik awal, dapat membentuk cluster yang berbeda

Algoritma DBSCAN untuk menentukan posisi Centroid
[See Article](https://www.kdnuggets.com/2020/04/dbscan-clustering-algorithm-machine-learning.html)
<iframe src="https://www.kdnuggets.com/2020/04/dbscan-clustering-algorithm-machine-learning.html" width="600px" height="500px"></iframe>

GIF:
![Figure|400](https://miro.medium.com/proxy/1*tc8UF-h0nQqUfLC8-0uInQ.gif)
Mengambil tetangga yang paling dekat, jika melebihi ambang batas, maka pindah ke cluster lain

Andaikata kita tidak ingin membangun cluster baru, kita bisa membuat *sub-cluster*, ini disebut dengan hierrarchical-clustering, kita dapat membuat sub-cluster dari cluster besar
* Pada dasarnya menentukan K-Means dulu
* Lalu menentukan jarak untuk hierarkinya

Ketika kita tau bahwa dataset kita hierarkis, maka kita juga dapat menggunakan metode ini untuk memvisualisasikan hierarki yang ada

## Contoh bagaimana Clustering dapat digunakan
View PDF: [[1570924690 stamped.pdf]] 
![[1570924690 stamped.pdf#height=500]]

> [!info] Info
> "Kami menggunakan clustering untuk menemukan bagian mana yang salah"
> * Kami berasumsi bahwa karena ada 9 gerakan, maka ada 9 cluster, ternyata dalam semua gerakan itu malah ada gerakan yang dominan, malah ciri-ciri utama yang menjadi fitur utama yang dominan dari salah satu gerakan itu kurang jelas, nilainya tidak berbeda jauh dari antara gerakan dan gerakan yang lain (dari cluster ke cluster yang lain)
> * Meskipun tidak ada fitur yang dominan dalam suatu cluster/gerakan, tetapi kita dapat memberikan bobot untuk setiap fitur yang dominan dalam suatu gerakan/cluster tertentu
> 
> Karena tidak adanya fitur yang dominan dari suatu gerakan/cluster, jadinya model tidak dapat mendeteksi secara akurat, tetapi ada suatu fitur yang berbobot lebih berat yang mencirikan suatu cluster/gerakan tertentu


