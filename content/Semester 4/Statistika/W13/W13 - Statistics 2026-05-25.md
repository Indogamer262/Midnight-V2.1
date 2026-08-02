> [!info] Author
> Notes By 2472008
# Non Linear Regression (simple), linearization
Tidak semua hal linear, misalnya:
* Pembelahan bakteri/amoeba
* Stem cell
* Peluruhan radioaktif
  C14 --> C12 dalam setiap 2500 tahun, menjadi setengahnya (decay radioactive)

Banyak hal di alam yang tidak linear, bagaimana cara kita meng-handle itu?
Dengan melakukan linearisasi

Arti Bentuk Sederhana: hanya ada 2 parameter, yaitu: A, B

![[Pasted image 20260525130615.png|500]]

Bilangan irasional euler ($e$) dan pi ($\pi$) berasal dari alam semesta, kita manusia menggunakan sistem desimal, mungkin karena hal itu bilangannya jadi irasional 🙂

> [!tip] Insight
> Kalo kita pake sistem bilangannya Tuhan, mungkin angkanya jadi bagus? :D

Sebelum melakukan regresi, Pelajari dulu proses Linearisasi
![[Pasted image 20260525133355.png|480]]
## Correlation Coefficient (r):
![[Pasted image 20260525220640.png|480]]
* Tipe I: antara X dan Y --> seberapa linear hubungan X dan Y
* Tipe II: antara y dan $\hat{y}$ (y_prediction) --> seberapa linear hasil prediksi ($\hat{y}$) dengan data kita (y)

Jika ingin menggunakan Tipe II, ubah $\sum X_i$ dan $\sum Y_i$ pada rumus menjadi $\sum y_i$ dan $\sum \hat{y}_i$

> [!warning] Perhatian!
> Microsoft Excel dan kalkulator ilmiah *Casio* memberikan tipe *Correlation Coefficient* (r) yang berbeda! 

> [!summary] Hal yang akan dibahas
> Tipe-tipe regresi yang akan di bahas adalah:
> * Regresi Eksponensial $\hat{y} = Ae^{Bx}$
> * Regresi Power (kuadrat) $\hat{y} = Ax^B$
> * Tipe Regresi Lainnya

Misal jumlah bakteri membelah diri, dengan x = jam, y = jumlah bakteri

| No  | x<br>(jam) | y<br>(jumlah) |
| --- | :--------: | :-----------: |
| 1   |     4      |     50000     |
| 2   |     5      |     95000     |
| 3   |     6      |    175000     |
| 4   |     7      |    360000     |
| 5   |     9      |    1150000    |
| 6   |     10     |    2200000    |
| 7   |     11     |    4500000    |
| 8   |     12     |    8800000    |
## Regresi Eksponensial:
$$
\begin{aligned}
y &= Ae^{Bx} \\
ln \space y &= ln(Ae^{Bx}) \\
ln \space y &= ln \space A + ln \space e^{Bx} \\
ln \space y &= ln \space A + B \times x \\
\end{aligned}
$$
Lalu kita lakukan permisalan sebagai berikut:
$$
\begin{aligned}
ln \space y &= ln \space A + B \times x \\
Y &= C + DX \\
\end{aligned}
$$
Dengan demikian, kita dapat menentukan A dan B dengan cara sebagai berikut:
$$
\begin{aligned}
\text{karena: } C &= ln \space A \\ 
\text{maka: } A &= e^C \\
\\
\text{dan} \\
\\
B &= D \\
\end{aligned}
$$
> [!note] Dengan
> ln = logaritma natural, artinya logaritma yang basisnya adalah $e$
> $ln (x) = e \space log \space x = C$
> 
> Dengan kata lain, $x = e^C$
> * $log \space 100 = 2$
> * $log \space 10^2 = 2$
> * $log \space 10^😛 = 😛$
> * $ln \space e^😛 = 😛$
### Contoh Regresi Eksponensial
Contoh tabel

| No  | x<br>(jam) | y<br>(jumlah) | X = x  |    Y = ln y    |  $X^2$  |     $Y^2$      |       XY       |  $\hat{y}$  |
| --- | :--------: | :-----------: | :----: | :------------: | :-----: | :------------: | :------------: | :---------: |
| 1   |     4      |     50000     |   4    |   10,8197783   |   16    |   117,067602   |   43,2791131   | 49601,41888 |
| 2   |     5      |     95000     |   5    |   11,4616322   |   25    |   131,369012   |   57,3081609   | 94193,75999 |
| 3   |     6      |    175000     |   6    |   12,0725413   |   36    |   145,746252   |   72,4352475   | 178875,2141 |
| 4   |     7      |    360000     |   7    |   12,7938593   |   49    |   163,682836   |   89,5570152   | 339686,4317 |
| 5   |     9      |    1150000    |   9    |   13,9552725   |   81    |   194,749631   |   125,597453   | 1224994,861 |
| 6   |     10     |    2200000    |   10   |   14,6039679   |   100   |   213,275879   |   146,039679   | 2326281,677 |
| 7   |     11     |    4500000    |   11   |   15,319588    |   121   |   234,689775   |   168,515468   | 4417640,118 |
| 8   |     12     |    8800000    |   12   |   15,9902623   |   144   |   255,688488   |   191,883147   | 8389157,86  |
| SUM |            |               | **64** | **107,016902** | **572** | **1456,26947** | **894,615283** |             |
Dengan proses Linearisasi, didapatkan C dan D sebagai berikut:

D = 4,688083712
C = 3,932960169

Setelah C dan D ditemukan, carilah A dan B

B = D = 4,688083712
A = $e^C$ = $e^{3,932960169}$ = 51,05789419

Setelah itu carilah r dan $r^2$ tipe I dan tipe II

Tipe I (X & Y):
* r = 0,988449533
* $r^2$ = 0,977032479

Tipe II (y & $\hat{y}$):
* r = 0,97882048
* $r^2$ = 0,958089532

## Regresi Power:
$$
\begin{aligned}
y &= Ax^B \\
ln \space y &= ln(Ax^B) \\
ln \space y &= ln \space A + ln \space x^B \\
ln \space y &= ln \space A + B \times ln \space x \\
Y &= C + DX
\end{aligned}
$$
Dengan demikian, akan ada perubahan pada tabel menjadi seperti ini:

| No  | x<br>(jam) | y<br>(jumlah) | X = ln x | Y = ln y | $X^2$ | $Y^2$ | XY  | $\hat{y}$ |
| --- | :--------: | :-----------: | :------: | :------: | :---: | :---: | :-: | :-------: |
perhatikan bahwa sekarang
* $X = ln \space x$
* D = B
* C = ln A
* A = $e^C$

## Tipe Regresi Lainnya
![[Pasted image 20260525222642.png|480]]

![[Pasted image 20260525222427.png|480]]

![[Pasted image 20260525222447.png|480]]

![[Pasted image 20260525222530.png|480]]

![[Pasted image 20260525222612.png|480]]

> [!info] Informasi PR
> Khusus PR Case 12, boleh kumpulin excel yang dijadikan PDF

