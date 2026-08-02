Materi Pendukung:
![[Standard_Normal_Table   Inverse t-distribution Table v2.pdf#height=480]]

Soal:
![[Pasted image 20260516105503.png]]
# Nomor 1
$$
\begin{aligned}
\bar{x} &= 7.18 \text{ tahun} \\
\sigma &= 0.89 \text { tahun} \\
n &= 100 \\ 
\end{aligned}
$$
## Bagian A

Buktikanlah bahwa $\mu > 7 \text{ tahun}$ dengan *significance level* 1%

$$
\begin{aligned}
\alpha &= 1\% = 0.01 \\
z_\alpha &= 2.33 \\
z_\bar{x} &= \frac{\bar{x} - \mu}{\sigma / \sqrt{n}} \\
&= \frac{7.18 - 7}{0.89/\sqrt{100}} \\
&= \frac{0.18}{0.89/10} \\
&= 2.022471
\end{aligned}
$$
Dengan demikian, $\mu = 7 \text{ tahun}$ dengan *significance level* 1% dapat diterima karena $z_\alpha > z_\bar{x}$
## Bagian B
Buktikanlah bahwa $\mu > 7 \text{ tahun}$ dengan *significance level* 5%

$$
\begin{aligned}
\alpha &= 5\% = 0.05 \\
z_\alpha &= 1.64 \\
z_\bar{x} &= 2.022471 \\
\end{aligned}
$$

Dengan demikian, $\mu = 7 \text{ tahun}$ dengan *significance level* 5% **tidak** dapat diterima karena $z_\alpha < z_\bar{x}$
## Bagian C
Buktikanlah bahwa $\mu > 7 \text{ tahun}$ dengan *significance level* 10%

$$
\begin{aligned}
\alpha &= 10\% = 0.10 \\
z_\alpha &= 1.28 \\
z_\bar{x} &= 2.022471 \\
\end{aligned}
$$

Dengan demikian, $\mu = 7 \text{ tahun}$ dengan *significance level* 5% **tidak** dapat diterima karena $z_\alpha < z_\bar{x}$

# Nomor 2
![[Pasted image 20260516123430.png]]
dengan:
$$
s^2 = \frac{\sum (\bar{x}-x\tiny{i})^2}{n-1}
$$

$$
\begin{aligned}
n &= 9 \\ 
\bar{x} &= \frac{6 + 7 + 7 + 7 + 6 + 8 + 8 + 7 + 6}{9}= 6.8889 \text { tahun}\\
s^2 &= \frac{3(\bar{x}-6)^2 + 4(\bar{x}-7)^2 + 2(\bar{x}-8)^2}{9-1} = 0.6111 \text { tahun} \\
s &= \sqrt{s^2} = 0.781736
\end{aligned}
$$
## Bagian A
Buktikan bahwa  $\mu \neq 7 \text{ tahun}$ dengan *significance level* 1%
$$
\begin{aligned}
\alpha &= 1\% = 0.01 \\
\frac{\alpha}{2} &= 0.5\% = 0.005\\
t_{\frac{\alpha}{2},8} &= 3.355387 \\
t_\bar{x} &= \frac{\bar{x} - \mu}{s / \sqrt{n}} \\
&= \frac{6.8889 - 7}{0.781736/\sqrt{9}} \\
&= -0.426359
\end{aligned}
$$
Dengan demikian, $\mu \neq 7 \text{ tahun}$ dengan *significance level* 1%, dapat diterima karena $-t_{\frac{\alpha}{2},8} < t_\bar{x} < t_{\frac{\alpha}{2},8}$

## Bagian B
Buktikan bahwa  $\mu \neq 7 \text{ tahun}$ dengan *significance level* 5%

$$
\begin{aligned}
\alpha &= 5\% = 0.05 \\
\frac{\alpha}{2} &= 2.5\% = 0.025\\
t_{\frac{\alpha}{2},8} &= 2.306004 \\
t_\bar{x} &= -0.426359
\end{aligned}
$$
Dengan demikian, $\mu \neq 7 \text{ tahun}$ dengan *significance level* 5%, dapat diterima karena $-t_{\frac{\alpha}{2},8} < t_\bar{x} < t_{\frac{\alpha}{2},8}$

## Bagian C
Buktikan bahwa  $\mu \neq 7 \text{ tahun}$ dengan *significance level* 10%

$$
\begin{aligned}
\alpha &= 10\% = 0.1 \\
\frac{\alpha}{2} &= 5\% = 0.05\\
t_{\frac{\alpha}{2},8} &= 1.859548 \\
t_\bar{x} &= -0.426359
\end{aligned}
$$
Dengan demikian, $\mu \neq 7 \text{ tahun}$ dengan *significance level* 10%, dapat diterima karena $-t_{\frac{\alpha}{2},8} < t_\bar{x} < t_{\frac{\alpha}{2},8}$

# Nomor 3
$$
\begin{aligned}
\bar{x} &= 7.8 \text{ kg} \\
\sigma &= 0.5 \text { kg} \\
n &= 50 \\ 
\end{aligned}
$$
Buktikanlah bahwa $\mu = 8 \text{ kg}$ dengan *significance level* 1%
## Kurang dari 8 kg?
$$
\begin{aligned}
\alpha &= 1\% = 0.01\\
z_\alpha &= -2.33 \\
z_\bar{x} &= \frac{\bar{x} - \mu}{\sigma / \sqrt{n}} \\
&= \frac{7.8 - 8}{0.5/\sqrt{50}} \\
&= -2.8284
\end{aligned}
$$
Dengan demikian, $\mu < 8 \text{ kg}$ tidak dapat diterima karena $z_\alpha > z_\bar{x}$
## Tidak sama dengan 8 kg?
$$
\begin{aligned}
\alpha &= 1\% = 0.01\\
\frac{\alpha}{2} &= 0.5\% = 0.005 \\
z_\frac{\alpha}{2} &= 2.58 \\
z_\bar{x} &= \frac{\bar{x} - \mu}{\sigma / \sqrt{n}} \\
&= \frac{7.8 - 8}{0.5/\sqrt{50}} \\
&= -2.8284
\end{aligned}
$$
 Dengan demikian, $\mu \neq 8 \text{ kg}$ tidak dapat diterima karena $-z_{\frac{\alpha}{2},8} > z_\bar{x}$
# Nomor 4
$$
\begin{aligned}
\bar{x} &= 42 \text{ kWh/tahn} \\
\sigma &= 11.9 \text { kWh/tahun} \\
n &= 12 \\ 
\end{aligned}
$$
Buktikanlah bahwa $\mu < 46 \text{ kWh/tahun}$ dengan *significance level* 5%
$$
\begin{aligned}
\alpha &= 5\% = 0.05\\
t_{\alpha,11} &= -1.795885 \\
t_\bar{x} &= \frac{\bar{x} - \mu}{\alpha / \sqrt{n}} \\
&= \frac{42 - 46}{11.9/\sqrt{12}} \\
&= -1.1644
\end{aligned}
$$
Dengan demikian, $\mu < 46 \text{ kWh/tahun}$ dengan *significance level* 5%, dapat diterima karena $t_\bar{x} > t_{\alpha,11}$
