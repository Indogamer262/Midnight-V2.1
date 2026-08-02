# Suport Vector Machines
Chapter 5 Prosise (2023) & Geron (2023)

---
## Sedikit Review
Tipe keluaran model
* **Regresi**: Angka, cth: Premi (10.500)
* **Klasifikasi**: Kelas/Label (diabetes='1')

Beberapa algoritma yang biasa digunakan
* SVM (Support Vector Machines)
* Tree
* Ensamble
* NN (Neural Network)
* Transformer (yang umum digunakan dalam LLM)

## Support Vector Machines
Jika bentuk suatu dataset tercampur, dengan kelompok yang tidak terpisah, tidak mungkin untuk dilakukan suatu garis "Decision Boundary"
* Akan sulit sekali untuk membuat suatu persamaan yang dapat memisahkan label pada dataset jika posisinya nempel-nempel

### Cara kerja SVM (Support Vector Machines):
![[Pasted image 20260505095451.png]]
Bagaimana juga persamaan garisnya, selama dia memisahkan, dapat kita gunakan
Tapi tujuannya, untuk memisahkan beberapa kelas yang ada **sejauh mungkin**, itulah yang akan menjadi hasil akhir dari fungsi yang akan kita bentuk

> [!Info] Konsep utama SVM
> Mencari persamaan garis/bidang/hal lain yang dapat memisahkan selebar-lebarnya antar kelas

### Apa itu SVM?
Satu satunya algoritma dalam klasifikasi yang hampir **tidak selalu ditentukan oleh banyaknya data** pada saat training

Misalnya jika data kita tidak terlalu banyak, mungkin SVM, juga Logistic Regression(?) adalah algoritma yang bisa kita yakini performanya bisa cukup baik

SVM hanya tergantung pada vektor di bagian yang perbatasan-perbatasan, jadi jika dataset banyak tetapi ngumpul pada bagian yang terpisah, maka tidak akan ada pengaruh performa

Salah satu sisi positif yang bisa kita pertimbangkan, algoritma apa yang baik digunakan untuk klasifikasi, jika kita merasa datanya banyak tercampur, SVM ini bisa jadi algoritma yang mumpuni, dia membedakan data yang beda-beda tipis itu dengan persamaan yang optimal

### SVM Regularization
> Sebagai parameter pertama dalam SVM

Lebar pita pada SVM bergantung pada Reguralisasi
![[Pasted image 20260505100720.png]]Semakin tinggi nilai penalti, maka lebar pitanya semakin kecil
- Penalti --> Mengurangi error
- Semakin kecil error (penalty nambah) --> semakin kecil pitanya

Kita tetap perlu mempertimbangkan mana nilai C (penalty) yang lebih baik, melalui eksperimen, melihat confusion matrix, dsb

### Kernels
> Hal berikutnya yang disebut dengan intisari dari SVM (core)

Hal yang membuat SVM Spesial
![[Pasted image 20260505101207.png]]
Kita bisa seolah mengubah _point of view_, kita membawa ke dimensi yang lebih tinggi (2D --> 3D)

> [!info] Analogi
> *Point of view* pemain dan penonton, pada _point of view_ penonton, lebih tinggi, penonton lebih mudah **membedakan** tim, sedangkan pada perspektif pemain, terlihat tercampur

**Prinsipnya:** *Cover's Theorem*, data yang kelihatannya mungkin tidak dapat dipisahkan secara linear, mungkin dapat dipisahkan secara linear jika dibawa ke dimensi yang lebih tinggi

## Tipe-tipe kernel

![[Pasted image 20260505101801.png]]

Sckit-learn punya beberpa kernel *general-purpose* secara *built-in*, termasuk:
* the Linear kernel
* the RBF kernel
* the polynomial kernel
* the sigmoid kernel

### Kernel Tricks
![[Pasted image 20260505101937.png]]

### Hyperparameter tuning (C)

![[Pasted image 20260505102034.png]]
Semakin tinggi nilai `C`, perbatasan antar kelas semakin tipis, dan ini juga meningkatkan resiko untuk **overfitting**

Tetapi jika nilai `C` terlalu kecil, maka dapat terjadi **underfitting** juga

Sifatnya sangat empiris (perlu uji-coba) secara default nilai `C` adalah 0.1, tapi bisa kita coba misal kalikan 10, dan kita dapat melihat dampaknya terhadap dataset yang kita miliki

### Hyperparameter Tuning (C and Gamma)
> RBF adalah fungsi yang menaikkan dimensi

> [!tip] Parameter kedua
> Ini adalah parameter kedua selain `C`

![[Pasted image 20260505102351.png]]
jika nilai Gamma semakin tinggi, maka dia akan mengambil sedikit data di perbatasan yang digunakan untuk memisahkan, area-nya semakin kecil pula jika Gamma semakin besar

Secara umum, nilai Gamma itu 0-1, meskipun bisa lebih dari 1, tetapi itu sangat jarang

### Bagaimana cara kerja RBF (Radial Basis Function) ?

Basic Idea -- Menentukan agar data tidak berada pada dimensi yang sama
![[Pasted image 20260505102851.png]]

Lalu:
![[Pasted image 20260505103007.png]]

RBF dapat kita manfaatkan untuk data yang masih berantakan atau yang sudah terpisah untuk menaikkan dimensi... data kita mungkin tercampur, tapi dengan POV yang berbeda, itu bisa saja jadi terpisah

![[Pasted image 20260505103301.png]]
Menentukan suatu landmark dimana dia bisa dibawa ke dimensi yang lebih tinggi

**Video**: The Kernel Trick
![](https://youtu.be/Q7vT0--5VII?si=Zu9CdV4zru9WzNLB)

### Contoh Kasus: Face Recognition
SVM memiliki performa yang tidak kalah dengan algoritma-algoritma modern seperti Neural Network (NN), dsb

Muka itu, jika hanya melihat satu bagian wajah (misalnya ambil sepotong-sepotong, mulut saja, mata saja, ujung hidung saja), itu sangat berdekatan, sangat mirip-mirip, bagaimana itu bisa dibedakan?

![[Pasted image 20260505104155.png]]

> [!tip] Pesan moral
> Jika kita punya data yang terbatas, dan itu sangat beririsan sifatnya, contoh wajah orang, SVM jadi algoritma yang dianggap dapat optimal untuk dipakai

Face detection $\neq$ Face recognition
* **Face detection** hanya deteksi itu muka atau bukan
* **Face recognition** mendeteksi identitas juga, tidak hanya itu muka atau bukan

SVM dapat memisahkan dengan tingkatan layer-layer yang berbeda

> [!info] Insight
> SVM memiliki 2 parameter yang harus diatur yaitu `C` dan `Gamma`

---
