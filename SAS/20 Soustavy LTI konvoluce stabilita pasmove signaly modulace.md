# 20 Soustavy, LTI popis, konvoluce, stabilita a pásmové signály

> [!info] Podklady
> Hlavní zdroj: [[sas_cviceni_v0.96_250225.pdf]]. Soustavy jsou zpracované podle kapitol 7, 8 a 9. Pásmové signály, Hilbertova transformace, komplexní obálka a analogové modulace jsou v dodaném PDF zachyceny hlavně ve znění teoretických otázek, proto je u nich uveden zdroj výskytu otázky.

## Soustava a základní klasifikace

> 🎥 **ALL OF Signals and Systems Explained** (Eric Explains) — souhrnný přehled okruhu

<div style="position:relative;padding-bottom:56.25%;height:0;margin:14px 0;max-width:680px;border-radius:8px;overflow:hidden">
<iframe src="https://www.youtube-nocookie.com/embed/XJw92w5u13c" title="All of Signals and Systems" loading="lazy" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position:absolute;inset:0;width:100%;height:100%;border:0"></iframe>
</div>

**Soustava** je objekt, který pod vlivem vstupního signálu, tedy buzení, produkuje výstupní signál, tedy odezvu. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=100|SAS s. 100]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=1cm]
    \draw[->,thick] (-2,0) -- (-0.7,0) node[midway,above] {$x(t)$ nebo $x[k]$};
    \draw[thick] (-0.7,-0.5) rectangle (0.7,0.5);
    \node at (0,0) {$\mathcal A$};
    \draw[->,thick] (0.7,0) -- (2,0) node[midway,above] {$y(t)$ nebo $y[k]$};
  \end{tikzpicture}
\end{document}
```

**Spojitá soustava** má vstup i výstup ve spojitém čase; **diskrétní soustava** má vstup i výstup v diskrétním čase. Smíšené soustavy obsahují například vzorkovač nebo interpolátor. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=100|SAS s. 100]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.95cm,y=0.8cm]
    \draw[->] (-0.3,0) -- (6.4,0) node[right] {$t,k$};
    \draw[->] (0,-1.3) -- (0,1.5);
    \draw[color=blue,thick,domain=0:3,samples=80] plot (\x,{sin(2*\x r)});
    \foreach \x/\y in {3.5/0.66,4.1/0.94,4.7/0.02,5.3/-0.91,5.9/-0.73}
      {
        \draw[color=red,thick] (\x,0) -- (\x,\y);
        \fill[color=red] (\x,\y) circle (1.5pt);
      }
    \node[color=blue] at (1.5,1.25) {spojitá};
    \node[color=red] at (5.1,1.25) {diskrétní};
  \end{tikzpicture}
\end{document}
```

**Kauzální soustava** má výstup vyvolaný současnými nebo minulými hodnotami vstupu, nikoli budoucností:

$$
x(t)=0\ \forall t<t_0 \Rightarrow y(t)=0\ \forall t<t_0,
$$

respektive diskrétně $x[k]=0\ \forall k<k_0\Rightarrow y[k]=0\ \forall k<k_0$. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=100|SAS s. 100]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.85cm,y=0.8cm]
    \draw[->] (-2.2,0) -- (4.3,0) node[right] {$t$};
    \draw[->] (0,-0.2) -- (0,1.6);
    \draw[color=blue,thick] (-2,0) -- (0,0) -- (0,1) -- (3.5,1);
    \draw[color=red,thick,dashed] (-2,0.65) -- (0,0.65) -- (0,1.25) -- (3.5,1.25);
    \node[color=blue] at (2.5,0.75) {$x$};
    \node[color=red] at (2.5,1.45) {$y$};
    \node at (0,-0.25) {$t_0$};
  \end{tikzpicture}
\end{document}
```

**Soustava bez paměti** závisí jen na aktuální hodnotě vstupu. **Soustava s pamětí** používá i minulé hodnoty vstupu. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=100|SAS s. 100]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=0.9cm]
    \draw[->] (-2.5,0) -- (3.2,0) node[right] {$t$};
    \draw[->] (0,-0.2) -- (0,1.5);
    \draw[color=blue,thick] (-2,0.2) -- (-1,1.0) -- (0,0.4) -- (1,1.2) -- (2,0.5);
    \draw[red,thick] (0,0) circle (0.12);
    \draw[red,thick,dashed] (-1,0) circle (0.12);
    \node[color=red] at (-0.55,1.35) {aktuální a sousední časy};
  \end{tikzpicture}
\end{document}
```

**BIBO stabilní soustava** převádí každý omezený vstup na omezený výstup:

$$
|x(t)|\le M_x<\infty \Rightarrow |y(t)|\le M_y<\infty,
$$

respektive stejně pro diskrétní čas. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=100|SAS s. 100-101]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.8cm,y=0.7cm]
    \draw[->] (-0.2,0) -- (6.5,0) node[right] {$t$};
    \draw[->] (0,-1.5) -- (0,1.7);
    \draw[dashed] (0,1) -- (6,1) node[right] {$M_y$};
    \draw[dashed] (0,-1) -- (6,-1) node[right] {$-M_y$};
    \draw[color=blue,thick] plot coordinates {(0,0.2) (1,0.8) (2,-0.7) (3,0.5) (4,-0.4) (5,0.9) (6,-0.2)};
    \node[color=blue] at (3,1.45) {omezený výstup};
  \end{tikzpicture}
\end{document}
```

**Lineární soustava** splňuje princip superpozice:

$$
\mathcal A\left\{\sum_i\lambda_i x_i(t)\right\}
=\sum_i\lambda_i\mathcal A\{x_i(t)\},
$$

a analogicky v diskrétním čase. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=101|SAS s. 101]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=0.85cm]
    \node at (-2,0.8) {$x_1$};
    \node at (-2,-0.2) {$x_2$};
    \draw[->] (-1.6,0.8) -- (-0.6,0.25);
    \draw[->] (-1.6,-0.2) -- (-0.6,0.25);
    \draw[thick] (-0.6,-0.25) rectangle (0.6,0.75);
    \node at (0,0.25) {$\mathcal A$};
    \draw[->] (0.6,0.25) -- (2.2,0.25) node[right] {$\lambda_1y_1+\lambda_2y_2$};
  \end{tikzpicture}
\end{document}
```

**Časově invariantní soustava** dává na posunutý vstup stejně posunutý výstup:

$$
y(t-t_0)=\mathcal A\{x(t-t_0)\},\qquad
y[k-k_0]=\mathcal A\{x[k-k_0]\}.
$$

Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=101|SAS s. 101]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.9cm,y=0.75cm]
    \draw[->] (-0.2,0) -- (6.4,0) node[right] {$t$};
    \draw[->] (0,-0.2) -- (0,1.5);
    \draw[color=blue,thick] (0.5,0) -- (1,1) -- (1.5,0);
    \draw[color=red,thick,dashed] (3.5,0) -- (4,1) -- (4.5,0);
    \draw[->,gray] (1.6,1.15) -- (3.4,1.15) node[midway,above] {$t_0$};
    \node[color=blue] at (1,1.35) {$y(t)$};
    \node[color=red] at (4,1.35) {$y(t-t_0)$};
  \end{tikzpicture}
\end{document}
```

**LTI soustava** je lineární a časově invariantní. V PDF se označuje také jako LS. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=101|SAS s. 101]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=1cm]
    \draw[thick] (-1.2,-0.6) rectangle (1.2,0.6);
    \node at (0,0.15) {lineární};
    \node at (0,-0.2) {časově invariantní};
    \draw[->,thick] (-2.4,0) -- (-1.2,0) node[midway,above] {$x$};
    \draw[->,thick] (1.2,0) -- (2.4,0) node[midway,above] {$y$};
  \end{tikzpicture}
\end{document}
```

## LTI soustava v časové oblasti

**Impulsová odezva** $h(t)$, respektive $h[k]$, je odezva LTI soustavy na Diracův impuls nebo jednotkový impuls:

$$
h(t)=\mathcal A\{\delta(t)\},\qquad h[k]=\mathcal A\{\delta[k]\}.
$$

Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=107|SAS s. 107]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=0.9cm]
    \draw[->,thick] (-3,0) -- (-1.8,0) node[midway,above] {$\delta$};
    \draw[thick] (-1.8,-0.45) rectangle (-0.6,0.45);
    \node at (-1.2,0) {LTI};
    \draw[->,thick] (-0.6,0) -- (0.4,0);
    \draw[->] (0.5,0) -- (3.2,0) node[right] {$t,k$};
    \draw[->] (0.8,-0.1) -- (0.8,1.3);
    \draw[color=blue,thick,domain=0.8:3,samples=80] plot (\x,{1.1*exp(-1.2*(\x-0.8))});
    \node[color=blue] at (2.3,0.9) {$h$};
  \end{tikzpicture}
\end{document}
```

**Konvoluce** určuje odezvu LTI soustavy ze vstupu a impulsové odezvy:

$$
y(t)=x(t)*h(t)=\int_{-\infty}^{\infty}x(\tau)h(t-\tau)\,d\tau,
$$

$$
y[k]=x[k]*h[k]=\sum_{i=-\infty}^{\infty}x[i]h[k-i].
$$

Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=107|SAS s. 107]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.85cm,y=0.75cm]
    \draw[->] (-3.2,0) -- (4.0,0) node[right] {$\tau$};
    \draw[->] (0,-0.2) -- (0,1.7);
    \draw[color=blue,thick] (-2,0) -- (-1,1.1) -- (0,0);
    \draw[color=red,thick] (0.7,0) -- (1.7,1.0) -- (2.7,0);
    \node[color=blue] at (-1,1.35) {$x(\tau)$};
    \node[color=red] at (1.8,1.3) {$h(t-\tau)$};
    \node at (0.2,-0.35) {součin a integrace};
  \end{tikzpicture}
\end{document}
```

Konvoluce je komutativní, asociativní a distributivní. PDF tyto vlastnosti zapisuje například jako $h_1*h_2=h_2*h_1$ a $(x*h_1)*h_2=x*(h_1*h_2)$. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=107|SAS s. 107]].

**Kauzalita LTI soustavy** je ekvivalentní podmínce

$$
h(t)=0\ \forall t<0,\qquad h[k]=0\ \forall k<0.
$$

Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=107|SAS s. 107]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.9cm,y=0.75cm]
    \draw[->] (-2.3,0) -- (4.3,0) node[right] {$t,k$};
    \draw[->] (0,-0.2) -- (0,1.6) node[above] {$h$};
    \draw[color=blue,thick] (-2,0) -- (0,0);
    \draw[color=blue,thick,domain=0:4,samples=80] plot (\x,{1.2*exp(-0.8*\x)});
    \node[color=blue] at (2.6,1.1) {kauzální $h$};
  \end{tikzpicture}
\end{document}
```

**Stabilita LTI soustavy v časové oblasti** je ekvivalentní absolutní integrovatelnosti nebo absolutní sčitatelnosti impulsové odezvy:

$$
\int_{-\infty}^{\infty}|h(\tau)|\,d\tau<\infty,\qquad
\sum_{i=-\infty}^{\infty}|h[i]|<\infty.
$$

Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=107|SAS s. 107-108]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.9cm,y=0.75cm]
    \draw[->] (-0.3,0) -- (5.2,0) node[right] {$t$};
    \draw[->] (0,-0.2) -- (0,1.6) node[above] {$|h(t)|$};
    \draw[color=blue,thick,domain=0:5,samples=100] plot (\x,{1.25*exp(-0.8*\x)});
    \fill[color=blue,opacity=0.15] (0,0) -- plot[domain=0:5,samples=100] (\x,{1.25*exp(-0.8*\x)}) -- (5,0) -- cycle;
    \node[color=blue] at (3.2,1.0) {konečná plocha};
  \end{tikzpicture}
\end{document}
```

## LTI soustava v transformační oblasti

**Spojitá LTI soustava popsaná diferenciální rovnicí** má tvar

$$
\sum_{i=0}^{m}a_i y^{(i)}(t)=\sum_{i=0}^{M}b_i x^{(i)}(t).
$$

Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=122|SAS s. 122]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.9cm,y=0.8cm]
    \draw[->] (-0.2,0) -- (5.8,0) node[right] {$t$};
    \draw[->] (0,-1.3) -- (0,1.5);
    \draw[color=blue,thick,domain=0:5.5,samples=100] plot (\x,{sin(2*\x r)});
    \draw[color=red,thick,domain=0:5.5,samples=100] plot (\x,{0.7*cos(2*\x r)});
    \node[color=blue] at (4.7,1.2) {$x(t)$};
    \node[color=red] at (4.7,-1.0) {$y(t)$};
  \end{tikzpicture}
\end{document}
```

**Laplaceova systémová funkce** je Laplaceův obraz impulsové odezvy:

$$
H(p)=\mathcal L\{h(t)\}
=\frac{\sum_{i=0}^{M}b_ip^i}{\sum_{i=0}^{m}a_ip^i},
\qquad h(t)=\mathcal L^{-1}\{H(p)\}.
$$

Stabilita kauzální spojité soustavy popsané touto funkcí vyžaduje póly v levé polorovině: $\operatorname{Re}\lambda_n<0$. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=123|SAS s. 123]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.8cm,y=0.8cm]
    \draw[->] (-3.2,0) -- (3.4,0) node[right] {$\operatorname{Re}p$};
    \draw[->] (0,-2.3) -- (0,2.5) node[above] {$\operatorname{Im}p$};
    \fill[color=blue,opacity=0.12] (-3,-2.2) rectangle (0,2.2);
    \foreach \x/\y in {-2/1.2,-1.4/-0.8,-0.7/0.4}
      \draw[color=blue,thick] (\x,\y) node {$\times$};
    \node[color=blue] at (-1.7,2.0) {stabilní oblast pólů};
  \end{tikzpicture}
\end{document}
```

**Diskrétní LTI soustava popsaná diferenční rovnicí** má tvar

$$
\sum_{i=0}^{m}a_i y[k-i]=\sum_{i=0}^{M}b_i x[k-i].
$$

Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=131|SAS s. 131]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.9cm,y=0.75cm]
    \draw[->] (-0.3,0) -- (6.3,0) node[right] {$k$};
    \draw[->] (0,-1.3) -- (0,1.5);
    \foreach \x/\y in {0/0.2,1/1.0,2/0.3,3/-0.8,4/-0.4,5/0.7,6/0.5}
      {
        \draw[color=blue,thick] (\x,0) -- (\x,\y);
        \fill[color=blue] (\x,\y) circle (1.5pt);
      }
    \node[color=blue] at (4.2,1.25) {zpoždění a vážené součty};
  \end{tikzpicture}
\end{document}
```

**Z-transformační systémová funkce** je obraz impulsové odezvy:

$$
H(z)=\mathbb Z\{h[k]\}
=\frac{\sum_{i=0}^{M}b_iz^{-i}}{\sum_{i=0}^{m}a_iz^{-i}},
\qquad h[k]=\mathbb Z^{-1}\{H(z)\}.
$$

Stabilita diskrétní soustavy vyžaduje póly uvnitř jednotkové kružnice: $|\lambda_n|<1$. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=132|SAS s. 132]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=1cm]
    \draw[->] (-1.7,0) -- (1.9,0) node[right] {$\operatorname{Re}z$};
    \draw[->] (0,-1.7) -- (0,1.9) node[above] {$\operatorname{Im}z$};
    \draw[color=blue,thick] (0,0) circle (1);
    \fill[color=blue,opacity=0.12] (0,0) circle (1);
    \foreach \x/\y in {-0.5/0.4,0.3/-0.6,0.7/0.2}
      \draw[color=blue,thick] (\x,\y) node {$\times$};
    \node[color=blue] at (0,-1.35) {uvnitř jednotkové kružnice};
  \end{tikzpicture}
\end{document}
```

## LTI soustava v kmitočtové oblasti

**Přenosová funkce spojité LTI soustavy** je Fourierova transformace impulsové odezvy a splňuje

$$
Y(\omega)=H(\omega)X(\omega),\qquad
H(\omega)=\mathcal F\{h(t)\}.
$$

U kauzální soustavy platí $H_F(\omega)=H_L(j\omega)$, pokud oblast konvergence Laplaceovy transformace obsahuje imaginární osu. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=136|SAS s. 136]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.85cm,y=0.75cm]
    \draw[->] (-0.2,0) -- (6.4,0) node[right] {$\omega$};
    \draw[->] (0,-0.2) -- (0,1.7) node[above] {$|H(\omega)|$};
    \draw[color=blue,thick] (0,1.2) -- (2.2,1.2) -- (3.2,0.2) -- (6,0.2);
    \node[color=blue] at (4.4,1.1) {příklad propusti};
  \end{tikzpicture}
\end{document}
```

**Přenosová funkce diskrétní LTI soustavy** je DtFT impulsové odezvy:

$$
Y(\Omega)=H(\Omega)X(\Omega),\qquad
H(\Omega)=\operatorname{DtFT}\{h[k]\}=\sum_{k=-\infty}^{\infty}h[k]e^{-j\Omega k}.
$$

U kauzální soustavy platí $H_F(\Omega)=H_Z(e^{j\Omega})$, pokud oblast konvergence Z-transformace obsahuje jednotkovou kružnici. Zdroj: [[sas_cviceni_v0.96_250225.pdf#page=142|SAS s. 142]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.85cm,y=0.75cm]
    \draw[->] (-3.4,0) -- (3.6,0) node[right] {$\Omega$};
    \draw[->] (0,-0.2) -- (0,1.7) node[above] {$|H(\Omega)|$};
    \draw[color=blue,thick,domain=-3.14:3.14,samples=120] plot (\x,{0.45+0.75*cos(0.5*\x r)*cos(0.5*\x r)});
    \node at (-3.14,-0.25) {$-\pi$};
    \node at (3.14,-0.25) {$\pi$};
  \end{tikzpicture}
\end{document}
```

## Pásmové signály, Hilbertova transformace a modulace

> 🎥 **Hilbert Transform Tutorial – A Tale of AM, QAM, and SSB** (Florentin Putz)

<div style="position:relative;padding-bottom:56.25%;height:0;margin:14px 0;max-width:680px;border-radius:8px;overflow:hidden">
<iframe src="https://www.youtube-nocookie.com/embed/R6w-47O3-w8" title="Hilbert Transform Tutorial" loading="lazy" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position:absolute;inset:0;width:100%;height:100%;border:0"></iframe>
</div>

> [!note] Rozsah v podkladech
> V textově extrahovaném [[sas_cviceni_v0.96_250225.pdf]] jsou Hilbertova transformace, komplexní obálka, pásmové signály a analogová modulace zachyceny hlavně jako teoretické otázky, nikoli jako samostatná vyložená kapitola. Konkrétní výskyty jsou na [[sas_cviceni_v0.96_250225.pdf#page=188|SAS s. 188-189]] a u AM na [[sas_cviceni_v0.96_250225.pdf#page=191|SAS s. 191]]. `hex_compost.pdf` kontrolně potvrzuje otázky „analogové modulace a jejich spektrum“, „jak získat komplexní obálku“ a „co je pásmový signál“. Zdroj: [[hex_compost.pdf#page=240|HEX s. 240]].

**Pásmový signál** má spektrum soustředěné kolem nenulové nosné úhlové frekvence $\omega_c$. Pro reálný pásmový signál je spektrum sdruženě symetrické, takže obsahuje kladné pásmo okolo $+\omega_c$ a záporné pásmo okolo $-\omega_c$. Pásmový signál lze popsat pomocí komplexní obálky v základním pásmu:

$$
s(t)=\operatorname{Re}\{\tilde s(t)e^{j\omega_c t}\}.
$$

Komplexní obálka $\tilde s(t)$ je pomalu proměnný komplexní signál, který nese informaci o amplitudě i fázi vůči nosné. Zdroj výskytu otázky: [[sas_cviceni_v0.96_250225.pdf#page=188|SAS s. 188-189]], kontrolně [[hex_compost.pdf#page=240|HEX s. 240]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.8cm,y=0.75cm]
    \draw[->] (-4.4,0) -- (4.6,0) node[right] {$\omega$};
    \draw[->] (0,-0.2) -- (0,1.6);
    \draw[color=blue,thick] (-3.4,0) -- (-2.8,1.0) -- (-2.2,0);
    \draw[color=blue,thick] (2.2,0) -- (2.8,1.0) -- (3.4,0);
    \draw[dashed] (-2.8,0) -- (-2.8,1.15);
    \draw[dashed] (2.8,0) -- (2.8,1.15);
    \node at (-2.8,-0.32) {$-\omega_c$};
    \node at (2.8,-0.32) {$\omega_c$};
    \node[color=blue] at (0,1.25) {reálný pásmový signál};
  \end{tikzpicture}
\end{document}
```

**Hilbertova transformace** signálu $s(t)$ se značí $\mathcal H\{s(t)\}$ a lze ji chápat jako průchod LTI soustavou s impulsovou odezvou

$$
h_H(t)=\frac{1}{\pi t}.
$$

Formálně:

$$
\hat s(t)=\mathcal H\{s(t)\}=s(t)*\frac{1}{\pi t}.
$$

V kmitočtové oblasti Hilbertův transformátor nemění amplitudy složek, ale zavádí fázový posun $+\pi/2$ pro záporné kmitočty a $-\pi/2$ pro kladné kmitočty:

$$
H_H(\omega)=-j\,\operatorname{sgn}(\omega)
=
\begin{cases}
j, & \omega<0,\\
0, & \omega=0,\\
-j, & \omega>0.
\end{cases}
$$

Zdroj výskytu otázky: [[sas_cviceni_v0.96_250225.pdf#page=188|SAS s. 188]], [[sas_cviceni_v0.96_250225.pdf#page=191|SAS s. 191]].

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.85cm,y=0.75cm]
    \draw[->] (-3.4,0) -- (3.6,0) node[right] {$\omega$};
    \draw[->] (0,-1.4) -- (0,1.6) node[above] {$H_H(\omega)$};
    \draw[color=gray,dashed] (-3.1,1) -- (3.1,1);
    \draw[color=gray,dashed] (-3.1,-1) -- (3.1,-1);
    \draw[color=blue,thick] (-3.1,1) -- (-0.12,1);
    \draw[color=blue,thick] (0.12,-1) -- (3.1,-1);
    \node[left] at (0,1) {$j$};
    \node[left] at (0,-1) {$-j$};
    \node at (-1.55,1.25) {$\omega<0$};
    \node at (1.55,-1.25) {$\omega>0$};
  \end{tikzpicture}
\end{document}
```

**Analytický signál** vznikne z reálného signálu $s(t)$ a jeho Hilbertovy transformace:

$$
s_a(t)=s(t)+j\hat s(t)=s(t)+j\mathcal H\{s(t)\}.
$$

Jeho spektrum obsahuje jen kladné kmitočty původního reálného signálu. Komplexní obálku pásmového signálu kolem $\omega_c$ získáme posunutím analytického signálu do základního pásma:

$$
\tilde s(t)=s_a(t)e^{-j\omega_c t}.
$$

Zpětný převod z komplexní obálky na reálný pásmový signál je

$$
s(t)=\operatorname{Re}\{\tilde s(t)e^{j\omega_c t}\}.
$$

Filtrační metoda tedy odpovídá postupu: z reálného pásmového signálu se vytvoří analytický signál odstraněním záporné poloviny spektra a výsledek se vynásobí $e^{-j\omega_c t}$. Zdroj výskytu otázky: [[sas_cviceni_v0.96_250225.pdf#page=188|SAS s. 188-189]].

```tikz
\begin{document}
  \begin{tikzpicture}[node distance=1.2cm,>=latex]
    \node[draw,minimum width=1.2cm] (s) {$s(t)$};
    \node[draw,right=of s] (analytic) {$s_a(t)=s(t)+j\mathcal H\{s(t)\}$};
    \node[draw,right=of analytic] (shift) {$\times e^{-j\omega_c t}$};
    \node[draw,right=of shift] (env) {$\tilde s(t)$};
    \draw[->] (s) -- (analytic);
    \draw[->] (analytic) -- (shift);
    \draw[->] (shift) -- (env);
    \node[below=0.35cm of analytic] {odstranění záporné poloviny spektra};
  \end{tikzpicture}
\end{document}
```

**Amplitudová modulace se zachovanou nosnou** mění amplitudu nosné podle modulačního signálu:

$$
s_{AM}(t)=A_c\left[1+m\,s_M(t)\right]\cos(\omega_c t).
$$

Nosná vlna má amplitudu $A_c$ a úhlovou frekvenci $\omega_c$, $s_M(t)$ je modulační signál a $m$ je činitel modulace. Aby obálka neměnila znaménko, běžně se vyžaduje

$$
1+m\,s_M(t)\ge 0.
$$

Ve spektru AM se zachovanou nosnou zůstává čára nosné na $\pm\omega_c$ a vznikají obě postranní pásma posunutá kolem nosné. Pro modulační signál se spektrem $S_M(\omega)$ lze schematicky psát

$$
S_{AM}(\omega)=\pi A_c\left[\delta(\omega-\omega_c)+\delta(\omega+\omega_c)\right]
+\frac{A_c m}{2}\left[S_M(\omega-\omega_c)+S_M(\omega+\omega_c)\right].
$$

Zdroj zadání vztahu a požadavku na spektrum: [[sas_cviceni_v0.96_250225.pdf#page=191|SAS s. 191]].

Časový a spektrální náčrt AM:

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.75cm,y=0.75cm]
    \draw[->] (-0.2,0) -- (8.2,0) node[right] {$t$};
    \draw[->] (0,-1.8) -- (0,1.9);
    \draw[color=gray,thick,domain=0:8,samples=120] plot (\x,{1.1+0.35*sin(0.9*\x r)});
    \draw[color=gray,thick,domain=0:8,samples=120] plot (\x,{-1.1-0.35*sin(0.9*\x r)});
    \draw[color=blue,thick,domain=0:8,samples=300] plot (\x,{(1.1+0.35*sin(0.9*\x r))*sin(7*\x r)});
    \node[color=blue] at (6.0,1.55) {AM náčrt};
  \end{tikzpicture}
\end{document}
```

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.85cm,y=0.75cm]
    \draw[->] (-4.4,0) -- (4.6,0) node[right] {$\omega$};
    \draw[->] (0,-0.2) -- (0,1.9) node[above] {$|S_{AM}|$};
    \draw[color=blue,thick] (-3.5,0) -- (-3.0,0.65) -- (-2.5,0);
    \draw[color=blue,thick] (-1.9,0) -- (-1.4,0.65) -- (-0.9,0);
    \draw[color=blue,thick] (0.9,0) -- (1.4,0.65) -- (1.9,0);
    \draw[color=blue,thick] (2.5,0) -- (3.0,0.65) -- (3.5,0);
    \draw[color=red,very thick,->] (-2.2,0) -- (-2.2,1.55);
    \draw[color=red,very thick,->] (2.2,0) -- (2.2,1.55);
    \node at (-2.2,-0.3) {$-\omega_c$};
    \node at (2.2,-0.3) {$\omega_c$};
    \node[color=red] at (0,1.6) {nosná};
    \node[color=blue] at (0,0.85) {postranní pásma};
  \end{tikzpicture}
\end{document}
```

**Další základní analogové modulace** se liší tím, která vlastnost nosné vlny se mění:

- **DSB-SC**: amplitudová modulace s potlačenou nosnou, typicky $s(t)=A_c s_M(t)\cos(\omega_c t)$; ve spektru jsou postranní pásma bez samostatné čáry nosné.
- **SSB**: jednopásmová modulace; přenáší jen jedno postranní pásmo, takže šetří šířku pásma.
- **PM**: fázová modulace; okamžitá fáze nosné závisí na modulačním signálu.
- **FM**: frekvenční modulace; okamžitá frekvence nosné závisí na modulačním signálu.

Tyto typy jsou uvedeny jako základní orientační přehled k části „typy základních analogových modulací“ ve znění okruhu [[SZZ - Odborné okruhy|odborný okruh 20]].

Pro jednofrekvenční modulační signál $s_M(t)=\cos(\omega_m t)$ lze orientačně psát:

$$
s_{PM}(t)=A_c\cos\left(\omega_c t+k_p s_M(t)\right),
\qquad
s_{FM}(t)=A_c\cos\left(\omega_c t+k_f\int s_M(t)\,\mathrm dt\right).
$$

U PM i FM je amplituda nosné konstantní. Mění se fáze, respektive okamžitá frekvence. Ve spektru úhlových modulací vzniká nosná a postranní čáry na $\omega_c\pm n\omega_m$; u většího modulačního indexu je postranních složek více.

Časový a spektrální náčrt PM:

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.75cm,y=0.75cm]
    \draw[->] (-0.2,0) -- (8.2,0) node[right] {$t$};
    \draw[->] (0,-1.5) -- (0,1.7);
    \draw[color=blue,thick,domain=0:8,samples=350] plot (\x,{sin((7*\x + 0.9*sin(0.9*\x r)) r)});
    \draw[color=gray,dashed] (0,1.05) -- (8,1.05);
    \draw[color=gray,dashed] (0,-1.05) -- (8,-1.05);
    \node[color=blue] at (5.8,1.35) {PM: konstantní amplituda};
  \end{tikzpicture}
\end{document}
```

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.8cm,y=0.75cm]
    \draw[->] (-4.5,0) -- (4.7,0) node[right] {$\omega$};
    \draw[->] (0,-0.2) -- (0,1.8) node[above] {$|S_{PM}|$};
    \foreach \x/\h in {-3.4/0.25,-2.8/0.5,-2.2/1.35,-1.6/0.5,-1.0/0.25,1.0/0.25,1.6/0.5,2.2/1.35,2.8/0.5,3.4/0.25}
      \draw[color=blue,very thick,->] (\x,0) -- (\x,\h);
    \node at (-2.2,-0.3) {$-\omega_c$};
    \node at (2.2,-0.3) {$\omega_c$};
    \node[color=blue] at (0,1.45) {$\omega_c\pm n\omega_m$};
  \end{tikzpicture}
\end{document}
```

Časový a spektrální náčrt FM:

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.75cm,y=0.75cm]
    \draw[->] (-0.2,0) -- (8.2,0) node[right] {$t$};
    \draw[->] (0,-1.5) -- (0,1.7);
    \draw[color=blue,thick,domain=0:8,samples=450] plot (\x,{sin((7*\x - 1.2*cos(0.9*\x r)) r)});
    \draw[color=gray,dashed] (0,1.05) -- (8,1.05);
    \draw[color=gray,dashed] (0,-1.05) -- (8,-1.05);
    \node[color=blue] at (5.8,1.35) {FM: mění se hustota kmitů};
  \end{tikzpicture}
\end{document}
```

```tikz
\begin{document}
  \begin{tikzpicture}[x=0.8cm,y=0.75cm]
    \draw[->] (-4.5,0) -- (4.7,0) node[right] {$\omega$};
    \draw[->] (0,-0.2) -- (0,1.8) node[above] {$|S_{FM}|$};
    \foreach \x/\h in {-4.0/0.15,-3.4/0.35,-2.8/0.7,-2.2/1.2,-1.6/0.7,-1.0/0.35,-0.4/0.15,0.4/0.15,1.0/0.35,1.6/0.7,2.2/1.2,2.8/0.7,3.4/0.35,4.0/0.15}
      \draw[color=blue,very thick,->] (\x,0) -- (\x,\h);
    \node at (-2.2,-0.3) {$-\omega_c$};
    \node at (2.2,-0.3) {$\omega_c$};
    \node[color=blue] at (0,1.45) {více postranních složek};
  \end{tikzpicture}
\end{document}
```

## Kontrolní shrnutí

- Obecná soustava je mapování vstupu na výstup.
- LTI znamená linearita plus časová invariantnost.
- Impulsová odezva úplně popisuje LTI soustavu v časové oblasti.
- Konvoluce dává odezvu LTI soustavy na libovolný vstup.
- BIBO stabilita LTI odpovídá absolutně integrovatelné nebo sčitatelné impulsové odezvě.
- V transformační oblasti se konvoluce mění na násobení.
- Spojitá stabilita podle pólů: levá polorovina; diskrétní stabilita podle pólů: uvnitř jednotkové kružnice.
- Pásmový signál lze popsat komplexní obálkou $\tilde s(t)$: $s(t)=\operatorname{Re}\{\tilde s(t)e^{j\omega_c t}\}$.
- Hilbertův transformátor má charakteristiku $H_H(\omega)=-j\,\operatorname{sgn}(\omega)$.
- AM se zachovanou nosnou má tvar $s_{AM}(t)=A_c[1+m s_M(t)]\cos(\omega_c t)$ a ve spektru zachovává nosnou i obě postranní pásma.
- PM mění okamžitou fázi nosné; FM mění okamžitou frekvenci nosné. Obě mají konstantní amplitudu a u tónové modulace spektrální složky kolem $\omega_c\pm n\omega_m$.
