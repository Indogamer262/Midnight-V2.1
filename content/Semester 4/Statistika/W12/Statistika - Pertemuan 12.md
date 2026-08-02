# Simple Linear Regression & Correlation
Regresi Linear --> satu teknik dalam statistika (sekarang *Machine Learning*) kita mencari sebuah trend berupa garis lurus dari sekumpulan data yang hampir berbentuk garis

Regresi Linear digunakan untuk memprediksi masa depan (*forecast*) dalam bentuk kuantitas (angka)

Regresi linear adalah "AI" paling sederhana
$$
y = \beta_0 + \beta_1 x_1
$$
Ini adalah regresi paling sederhana karena tidak ada banyak parameter ($\beta_n x_n$), korelasi sebaiknya mendekati nol antara masing-masing parameter

y = variabel dependant
sisanya = variabel independent, makannya korelasi sebaiknya mendekati nol antara mereka

Misal: Seorang pedagang penjual beras
x = waktu (bulan)
y = omset

| No  | x (bulan) | y (kg) |
| :-: | :-------: | :----: |
|  1  |     3     |  1100  |
|  2  |     4     |  1250  |
|  3  |     5     |  1400  |
|  4  |     6     |  1300  |
|  5  |     7     |  1450  |
|  6  |     8     |  1700  |
|  7  |     9     |  2000  |
|  8  |    10     |  1950  |
|  9  |    11     |  2100  |
Ada 9 data point (9 pasangan data)

| No  | x (bulan) | y (kg) |
| :-: | :-------: | :----: |
| 10  |    12     |   ?    |
Gimana ke bulan 12? Lakukan regresi linear!
![[Document20260518_1.jpg]]
Tambahan: $r^2$ = Determination Coefficient

Correlation Coefficient:
![[20260518_133412.jpg|480]]
![[Pasted image 20260518133359.png|480]]

Mengerjakan kasus beras dengan Microsoft Excel:
![[Document20260518_2.jpg]]

