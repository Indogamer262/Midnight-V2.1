Referensi soal:
![[Kuis2Strategi Algoritmik-C.pdf#height=400]]

# Materi 1: Program Dinamis
![[Pasted image 20260610182614.png|600]]
Daftar Item:

| N   | Weight | Profit |
| :-- | :----: | :----: |
| 1   |   2    |   15   |
| 2   |   3    |   12   |
| 3   |   2    |   8    |
| 4   |   2    |   10   |
Kapasitas Knapsack W = 6

Item 1 - Weight = 2, Profit = 15

| y   | f0(y) | 15 + f0(y-2) | f1(y) | (x1, x2, x3, x4) |
| --- | ----- | ------------ | ----- | ---------------- |
| 0   | 0     | $-\infty$    | 0     | (0,0,0,0)        |
| 1   | 0     | $-\infty$    | 0     | (0,0,0,0)        |
| 2   | 0     | 15           | 15    | (1,0,0,0)        |
| 3   | 0     | 15           | 15    | (1,0,0,0)        |
| 4   | 0     | 15           | 15    | (1,0,0,0)        |
| 5   | 0     | 15           | 15    | (1,0,0,0)        |
| 6   | 0     | 15           | 15    | (1,0,0,0)        |
Item 2 - Weight = 3, Profit = 12

| y   | f1(y) | 15 + f0(y-3) | f2(y) | (x1, x2, x3, x4) |
| --- | ----- | ------------ | ----- | ---------------- |
| 0   | 0     | $-\infty$    | 0     | (0,0,0,0)        |
| 1   | 0     | $-\infty$    | 0     | (0,0,0,0)        |
| 2   | 15    | $-\infty$    | 15    | (1,0,0,0)        |
| 3   | 15    | 12           | 15    | (1,0,0,0)        |
| 4   | 15    | 12           | 15    | (1,0,0,0)        |
| 5   | 15    | 12 + 15      | 27    | (1,1,0,0)        |
| 6   | 15    | 12 + 15      | 27    | (1,1,0,0)        |
dst...
# Materi 2: Algoritma Backtracking
![[Pasted image 20260610182719.png|600]]

a. gambarkan graf dari peta di atas
![[Pasted image 20260610184608.png|240]]
b. Gunakan algoritma backtracking, m=4
```mermaid
---
config:
  theme: redux
---
flowchart TB
    A(("1")) -- "x1 = 1" --> B(("2"))
    B -- "x2 = 1" --> C(("3"))
    B -- "x2 = 2" --> D(("4"))
    C --> n1["B"]
    D -- "x3 = 1" --> n2(("5"))
    n2 --> n3["B"]
    D -- "x3 = 2" --> n4(("6"))
    n4 -- "x4 = 1" --> n5(("7"))
    n4 -- "x4 = 2" --> n6(("8"))
    n4 -- "x4 = 3" --> n7(("9"))
    n5 --> n8["B"]
    n6 --> n9["B"]
    n7 -- "x5 = 1" --> n10(("10"))
    n7 -- "x5 = 2" --> n11(("11"))
    n10 --> n12["B"]
    n11 --> n13["B"]
    n7 -- "x5 = 3" --> n14(("12"))
    n14 -- "x6 = 1" --> n15(("13"))
    n15 --> n16["B"]
    n14 -- "x6 = 2" --> n17(("14"))
    n17 --> n18["B"]
    n14 -- "x6 = 3" --> n19(("15"))
    n19 --> n20["B"]
    n14 -- "x6 = 4" --> n21(("16"))
    n21 -- "x7 = 1" --> n22(("17"))

    n1@{ shape: text}
    n3@{ shape: text}
    n8@{ shape: text}
    n9@{ shape: text}
    n12@{ shape: text}
    n13@{ shape: text}
    n16@{ shape: text}
    n18@{ shape: text}
    n20@{ shape: text}
```
# Materi 3: Branch & Bounds
![[Pasted image 20260610190331.png|600]]

| $\infty$ |    9     | $\infty$ |    8     |     | -8  |     | $\infty$ |    1     | $\infty$ |    0     |         |
| :------: | :------: | :------: | :------: | --- | --- | --- | :------: | :------: | :------: | :------: | ------: |
|    10    | $\infty$ |    14    | $\infty$ |     | -10 |     |    0     | $\infty$ |    4     | $\infty$ |         |
|    8     |    15    | $\infty$ |    9     |     | -8  |     |    0     |    7     | $\infty$ |    1     |         |
|    12    |    11    |    10    | $\infty$ |     | -10 |     |    2     |    1     |    0     | $\infty$ |         |
|          |          |          |          |     |     |     |          |          |          |          |         |
|          |          |          |          |     |     |     |    0     |    -1    |    0     |    0     | Total R |
|          |          |          |          |     |     |     |          |          |          |          |      37 |
|          |          |          |          |     |     |     | $\infty$ |    0     | $\infty$ |    0     |         |
|          |          |          |          |     |     |     |    0     | $\infty$ |    4     | $\infty$ |         |
|          |          |          |          |     |     |     |    0     |    6     | $\infty$ |    1     |         |
|          |          |          |          |     |     |     |    2     |    0     |    0     | $\infty$ |         |
Dengan demikian, mulai

|       |    A     |    B     |    C     |    D     |
| ----- | :------: | :------: | :------: | :------: |
| **A** | $\infty$ |    0     | $\infty$ |    0     |
| **B** |    0     | $\infty$ |    4     | $\infty$ |
| **C** |    0     |    6     | $\infty$ |    1     |
| **D** |    2     |    0     |    0     | $\infty$ |
dari A, cari terkecil, ditemukan ke B atau D terkecil, lakukan reduksi sub-matrix A-B

|       |      A       |      B       |      C       |      D       |     |       |     |       |      A       |      B       |      C       |      D       |
| ----- | :----------: | :----------: | :----------: | :----------: | --- | ----- | --- | ----- | :----------: | :----------: | :----------: | :----------: |
| **A** | ==$\infty$== | ==$\infty$== | ==$\infty$== | ==$\infty$== |     |       |     | **A** | ==$\infty$== | ==$\infty$== | ==$\infty$== | ==$\infty$== |
| **B** |      0       | ==$\infty$== |      4       |   $\infty$   |     | -0    |     | **B** |      0       | ==$\infty$== |      4       |   $\infty$   |
| **C** |      0       | ==$\infty$== |   $\infty$   |      1       |     | -0    |     | **C** |      0       | ==$\infty$== |   $\infty$   |      1       |
| **D** |      2       | ==$\infty$== |      0       |   $\infty$   |     | -0    |     | **D** |      2       | ==$\infty$== |      0       |   $\infty$   |
|       |              |              |              |              |     |       |     |       |              |              |              |              |
|       |              |              |              |              |     | Total |     |       |      -0      |      -0      |      -0      |      -1      |
|       |              |              |              |              |     | R =   |     |       |              |              |              |              |
|       |              |              |              |              |     | 38    |     |       |      A       |      B       |      C       |      D       |
|       |              |              |              |              |     |       |     | **A** | ==$\infty$== | ==$\infty$== | ==$\infty$== | ==$\infty$== |
|       |              |              |              |              |     |       |     | **B** |      0       | ==$\infty$== |      4       |   $\infty$   |
|       |              |              |              |              |     |       |     | **C** |      0       | ==$\infty$== |   $\infty$   |      0       |
|       |              |              |              |              |     |       |     | **D** |      2       | ==$\infty$== |      0       |   $\infty$   |
dari A, coba ke D

|       |      A       |      B       |      C       |      D       |
| ----- | :----------: | :----------: | :----------: | :----------: |
| **A** | ==$\infty$== | ==$\infty$== | ==$\infty$== | ==$\infty$== |
| **B** |      0       |   $\infty$   |      4       | ==$\infty$== |
| **C** |      0       |      6       |   $\infty$   | ==$\infty$== |
| **D** |      2       |      0       |      0       | ==$\infty$== |
Tidak ada reduksi baris dan kolom, sehingga R = 37, artinya ke D lebih baik daripada B

dari A-D, cari terkecil, ditemukan B dan C terkecil, langsung aja ke C

|       |      A       |      B       |      C       |      D       |
| ----- | :----------: | :----------: | :----------: | :----------: |
| **A** |   $\infty$   |   $\infty$   | ==$\infty$== |   $\infty$   |
| **B** |      0       |   $\infty$   | ==$\infty$== |   $\infty$   |
| **C** |      0       |      6       | ==$\infty$== |   $\infty$   |
| **D** | ==$\infty$== | ==$\infty$== | ==$\infty$== | ==$\infty$== |
Tidak ada reduksi baris dan kolom, sehingga R = 37, artinya ke C lebih baik daripada ke B

dari A-D-C, cari terkecil, tinggal B doang

|       |    A     |      B       |      C       |      D       |
| ----- | :------: | :----------: | :----------: | :----------: |
| **A** | $\infty$ | ==$\infty$== |   $\infty$   |   $\infty$   |
| **B** |    0     | ==$\infty$== |   $\infty$   |   $\infty$   |
| **C** |  ==0==   | ==$\infty$== | ==$\infty$== | ==$\infty$== |
| **D** | $\infty$ | ==$\infty$== |   $\infty$   |   $\infty$   |
Tidak ada reduksi baris dan kolom, sehingga R = 37
Jalur selesai A-D-C-B, sekarang balik ke A lagi

|       |      A       |      B       |      C       |      D       |
| ----- | :----------: | :----------: | :----------: | :----------: |
| **A** | ==$\infty$== |   $\infty$   |   $\infty$   |   $\infty$   |
| **B** | ==$\infty$== | ==$\infty$== | ==$\infty$== | ==$\infty$== |
| **C** | ==$\infty$== |   $\infty$   |   $\infty$   |   $\infty$   |
| **D** | ==$\infty$== |   $\infty$   |   $\infty$   |   $\infty$   |
ok, pokoknya R = 37, dah gitu aja
# Materi 4: String Matching
![[Pasted image 20260610195214.png|600]]
Fungsi Lo (Last Occurence)???
P = abaca
T = cabadaecdabacadca

Gunakan algoritma Boyer Moore