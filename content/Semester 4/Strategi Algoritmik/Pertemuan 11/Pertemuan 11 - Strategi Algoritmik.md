# String Matching
View PDF: [[Strago_StringMatching_2022.pdf]]
![[Strago_StringMatching_2022.pdf]]

Definisi:
* Teks T --> n karaketer
* Pola/Pattern (P) -> m karakter

> [!summary] Intinya
> Kita mencari Pola (P) pada Teks (T)

Contoh:
* T: "the rain in spain stays <span style="color:red"><b>main</b></span>ly on the plain"
* P: "main"

## Konsep String
String `S`:

|  a  |  n  |  d  |  r  |  e  |  w  |
| :-: | :-: | :-: | :-: | :-: | :-: |
|  0  |  1  |  2  |  3  |  4  |  5  |
Substring: S\[i...j] (dari indeks i sampai j)
Prefix: S\[0...i] (dari indeks 0 sampai i)
Suffix: S\[i...m-1] (dari indeks i sampai akhir)

## Algoritma yang digunakan
Untuk melakukan string matching
### 1. Algoritma Brute Force
Geser satu indeks, lalu coba cocokan, geser lagi jika belum cocok sampai akhir
![[Pasted image 20260521152539.png]]

Kasus terburuk dari algoritma **Brute Force**: O(mn), algoritma **Brute Force** berjalan cepat jika jumlah karakter uniknya besar (banyak karakter yang unik)

Jika jumlah karakter uniknya kecil, malah memperlambat algoritma **Brute Force**, karena bisa saja pencocokan sampai indeks akhir baru salah, ini memperlambat!!

Contoh worst case:
* T: aaaaaaaaaaah
* P: aaah

Setiap kali iterasi, maka algoritma akan memerika `aaa`, lalu `h` tidak match, ini memperlambat!
### 2. Algoritma Boyer-Moore
Berdasarkan 2 teknik:
* looking-glass
* character-jump

**Langkah-langkah**
0. Membuat tabel *Last Occurence* (tabel yang berisi indeks terakhir dari masing-masing karakter unik T pada P)
1. Lakukan matching dengan indeks terakhir P sampai awal, juga mundur pada T

Kasus 1: `x` pada T lebih kiri di P
Kasus 2: `x` pada T lebih kanan di P
Kasus 3: `x` pada T tidak ada di P

![[Document20260521_1.jpg]]

**Booyer-Moore** worst case running time: O(nm + A)
Berjalan lambat jika `A` (jumlah karakter unik) kecil, tetapi cepat jika `A` besar

### 3. Algoritma KMP (Knuth-Morris-Pratt)
Mulainya dari ke 0, berbeda dengan BM yang dari belakang

KMP akan menggunakan *prefix* dan *suffix*

Berbeda dengan BM, KMP menjadi $j_{\text{new}}$, sedangkan BM mencari $i_\text{new}$

![[Document20260521_2.jpg]]

Lalu, karena yang terpanjang sama adalah 2 karakter, maka $j_\text{new}$ = 2
![[Pasted image 20260521161258.png|640]]

> [!info] Insight
> Jika salah/*mismatch* di j = 0, maka geser 1 saja

Contoh:
![[Document20260521_3.jpg]]
Dengan:
![[Document20260521_4.jpg|480]]

KMP memiliki kompleksitas O(m+n) --> sangat cepat

KMP bekerja kurang baik jika A (jumlah karakter unik) meningkat, karena ketidakcocokan akan meningkat, KMP berjalan cepat jika mismatch terjadi di akhir P (pola)