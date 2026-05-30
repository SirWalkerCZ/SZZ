---
aliases:
  - MA1A 04
  - Primitivní funkce a integrály
predmet: MA1A
okruh: 4
---

# Primitivní funkce a integrály

> [!info] Zdroje
> Hlavní podklady: [[ma1a-23k7.pdf]], [[ma1a-23k8.pdf]], [[ma1a-23k9.pdf]], [[ma1a-23k10.pdf]].

## Primitivní funkce a neurčitý integrál

Funkce $F$ je primitivní funkcí k funkci $f$ na intervalu $I$, pokud pro každé $x\in I$ existuje derivace $F'(x)$ a platí
$$
F'(x)=f(x).
$$
V krajních bodech intervalu se případně bere příslušná jednostranná derivace. Každá primitivní funkce je na intervalu spojitá, protože má vlastní derivaci.

Zdroj: [[ma1a-23k7.pdf#page=1|MA1A k7, P7.1]]

Pokud je $F$ primitivní funkcí k $f$ na intervalu $I$, pak pro libovolnou konstantu $c\in\mathbb{R}$ je $F+c$ také primitivní funkcí. Naopak dvě primitivní funkce ke stejné funkci na intervalu se liší o konstantu:
$$
G=F+c.
$$
Neurčitý integrál je množina všech primitivních funkcí:
$$
\int f(x)\,dx = F(x)+c.
$$

Zdroj: [[ma1a-23k7.pdf#page=1|MA1A k7, P7.1]]

Pokud je $f$ spojitá na intervalu $I$, pak k ní na tomto intervalu existuje primitivní funkce. Ne každá primitivní funkce ale musí jít vyjádřit pomocí elementárních funkcí v konečném tvaru.

Zdroj: [[ma1a-23k7.pdf#page=1|MA1A k7, P7.1]]

Související: [[03 Funkce jedne promenne, limita, derivace, prubeh#Derivace a její význam|derivace]] je operace opačná k hledání primitivní funkce.

## Základní tabulkové integrály

Z tabulkových integrálů je potřeba umět hlavně ty, které odpovídají základním derivacím:
$$
\int x^\alpha\,dx=\frac{x^{\alpha+1}}{\alpha+1}+c \quad (\alpha\ne -1),
$$
$$
\int \frac{1}{x}\,dx=\ln|x|+c,
$$
$$
\int e^x\,dx=e^x+c,
\qquad
\int a^x\,dx=\frac{a^x}{\ln a}+c,
$$
$$
\int \sin x\,dx=-\cos x+c,
\qquad
\int \cos x\,dx=\sin x+c,
$$
$$
\int \frac{1}{1+x^2}\,dx=\arctan x+c.
$$
Vždy je nutné hlídat interval, na kterém se primitivní funkce hledá.

Zdroj: [[ma1a-23k7.pdf#page=2|MA1A k7, P7.2]]

## Základní metody výpočtu neurčitých integrálů

Linearita říká, že pokud existují příslušné primitivní funkce, pak
$$
\int (f+g)\,dx=\int f\,dx+\int g\,dx,
$$
$$
\int \alpha f\,dx=\alpha\int f\,dx.
$$

Zdroj: [[ma1a-23k7.pdf#page=3|MA1A k7, P7.3]]

Integrace per partes vychází z derivace součinu. Pokud mají $u,v$ vlastní derivace a existuje primitivní funkce k $u'v$, pak
$$
\int u v'\,dx = uv-\int u'v\,dx.
$$
Používá se například pro integrály typu $\int \ln x\,dx$, $\int x e^x\,dx$ nebo kombinace polynomu s goniometrickou či exponenciální funkcí.

Zdroj: [[ma1a-23k7.pdf#page=3|MA1A k7, P7.3]]

Substituce převádí složený výraz na jednodušší proměnnou. Pokud $F$ je primitivní funkce k $f$ na $J$, $\varphi(I)\subset J$ a $\varphi$ má derivaci na $I$, pak
$$
\int f(\varphi(t))\varphi'(t)\,dt = F(\varphi(t))+c.
$$
Obráceně se dá psát symbolicky
$$
\int f(x)\,dx=\int f(\varphi(t))\varphi'(t)\,dt,
\qquad x=\varphi(t),
$$
pokud je substituce na daném intervalu vhodná.

Zdroj: [[ma1a-23k7.pdf#page=3|MA1A k7, P7.3]]

Častý vzor je
$$
\int \frac{f'(x)}{f(x)}\,dx=\ln|f(x)|+c,
$$
a pro $k>1$
$$
\int \frac{f'(x)}{(f(x))^k}\,dx=\frac{(f(x))^{-k+1}}{-k+1}+c.
$$

Zdroj: [[ma1a-23k7.pdf#page=4|MA1A k7, P7.4]]

## Integrace racionálních funkcí

Racionální funkce má tvar
$$
R(x)=\frac{P(x)}{Q(x)},
$$
kde $P,Q$ jsou polynomy a $Q$ není nulový polynom. Pokud $\deg P\ge \deg Q$, nejprve se provede dělení polynomů:
$$
\frac{P(x)}{Q(x)}=Y(x)+\frac{Z(x)}{Q(x)}, \qquad \deg Z<\deg Q.
$$
Polynom se integruje přímo a ryze lomená část se rozkládá na parciální zlomky.

Zdroj: [[ma1a-23k7.pdf#page=5|MA1A k7, P7.5]]

Jednoduché zlomky mají základní tvary
$$
\frac{A}{(x-\alpha)^k}
$$
a
$$
\frac{Bx+C}{(x^2+px+q)^l}, \qquad p^2-4q<0.
$$
Každou ryze lomenou racionální funkci lze jednoznačně zapsat jako součet jednoduchých zlomků, až na pořadí sčítanců. Integrace racionální funkce se tím redukuje na integraci polynomu a jednoduchých zlomků.

Zdroj: [[ma1a-23k7.pdf#page=6|MA1A k7, P7.6]], [[ma1a-23k7.pdf#page=8|MA1A k7, P7.8]]

## Goniometrické a odmocninové substituce

U výrazů typu
$$
\int R(\sin x,\cos x)\,dx
$$
se volí substituce podle symetrie racionální funkce $R$. Typicky:

- lichost v $\sin x$ vede k substituci $t=\cos x$,
- lichost v $\cos x$ vede k substituci $t=\sin x$,
- současná změna znamének často vede k $t=\tan x$,
- univerzální možnost je $t=\tan\frac{x}{2}$.

Univerzální substituce dává
$$
\sin x=\frac{2t}{1+t^2},
\qquad
\cos x=\frac{1-t^2}{1+t^2},
\qquad
 dx=\frac{2}{1+t^2}\,dt.
$$
Je obecná, ale často vede ke složitější racionální funkci než jednodušší cílená substituce.

Zdroj: [[ma1a-23k7.pdf#page=12|MA1A k7, P7.12]], [[ma1a-23k7.pdf#page=13|MA1A k7, P7.13]]

U integrálů s odmocninami se používají substituce přizpůsobené tvaru odmocniny, například pro výrazy s
$$
\sqrt[n]{\frac{ax+b}{cx+d}}
$$
se bere
$$
y=\sqrt[n]{\frac{ax+b}{cx+d}}.
$$
U výrazů $R(x,\sqrt{ax^2+bx+c})$ se nejprve doplní na čtverec a poté se volí goniometrická nebo hyperbolická substituce podle výsledného tvaru.

Zdroj: [[ma1a-23k7.pdf#page=18|MA1A k7, P7.18]]

## Riemannův určitý integrál

Určitý integrál je motivován obsahem plochy pod grafem. Pro omezenou funkci $f$ na $[a,b]$ vezmeme dělení
$$
D=\{x_0,x_1,\dots,x_n\}, \qquad a=x_0<x_1<\dots<x_n=b.
$$
Na každém dílku definujeme
$$
m_{i,D}=\inf_{x\in[x_{i-1},x_i]}f(x),
\qquad
M_{i,D}=\sup_{x\in[x_{i-1},x_i]}f(x).
$$
Dolní a horní Riemannův součet označíme v poznámkách jako $s(f,D)$ a $S(f,D)$:
$$
s(f,D)=\sum_{i=1}^{n}m_{i,D}(x_i-x_{i-1}),
$$
$$
S(f,D)=\sum_{i=1}^{n}M_{i,D}(x_i-x_{i-1}).
$$

Zdroj: [[ma1a-23k8.pdf#page=1|MA1A k8, P8.1]]

Riemannův integrál existuje, pokud se horní hranice dolních součtů rovná dolní hranici horních součtů:
$$
\sup\{s(f,D)\mid D\text{ je dělení }[a,b]\}
\;=\;
\inf\{S(f,D)\mid D\text{ je dělení }[a,b]\}=I.
$$
Pak píšeme
$$
\int_a^b f(x)\,dx=I.
$$
Riemannův integrál je definován pro omezené funkce. Změna hodnoty funkce v konečně mnoha bodech nemění existenci ani hodnotu integrálu.

Zdroj: [[ma1a-23k8.pdf#page=2|MA1A k8, P8.2]], [[ma1a-23k8.pdf#page=4|MA1A k8, P8.4]]

Důležitá existence: je-li funkce na $[a,b]$ spojitá nebo monotónní, pak Riemannův integrál existuje.

Zdroj: [[ma1a-23k8.pdf#page=3|MA1A k8, P8.3]]

## Vlastnosti určitého integrálu

Aditivita podle intervalu:
$$
\int_a^c f(x)\,dx=\int_a^b f(x)\,dx+\int_b^c f(x)\,dx.
$$
Pro obrácené meze platí
$$
\int_b^a f(x)\,dx=-\int_a^b f(x)\,dx,
$$
a
$$
\int_a^a f(x)\,dx=0.
$$

Zdroj: [[ma1a-23k8.pdf#page=3|MA1A k8, P8.3]]

Linearita a monotonie:
$$
\int_a^b (f+g)(x)\,dx=\int_a^b f(x)\,dx+\int_a^b g(x)\,dx,
$$
$$
\int_a^b c f(x)\,dx=c\int_a^b f(x)\,dx.
$$
Je-li $f\ge 0$ na $[a,b]$, pak
$$
\int_a^b f(x)\,dx\ge 0.
$$
Je-li $f\le g$, pak
$$
\int_a^b f(x)\,dx\le \int_a^b g(x)\,dx.
$$
Platí také odhad
$$
\left|\int_a^b f(x)\,dx\right|\le \int_a^b |f(x)|\,dx.
$$

Zdroj: [[ma1a-23k8.pdf#page=4|MA1A k8, P8.4]]

Integrál jako funkce horní meze:
$$
F_c(x)=\int_c^x f(t)\,dt.
$$
Je-li $f$ spojitá v $x_0$, pak
$$
F_c'(x_0)=f(x_0).
$$
Tím se propojuje určitý integrál s primitivní funkcí.

Zdroj: [[ma1a-23k8.pdf#page=5|MA1A k8, P8.5]]

## Newtonova-Leibnizova formule

Pokud existuje $\int_a^b f(x)\,dx$ a $F$ je primitivní funkce k $f$ na $(a,b)$, pak
$$
\int_a^b f(x)\,dx=F(b-)-F(a+).
$$
Píšeme také
$$
\int_a^b f(x)\,dx=[F(x)]_a^b.
$$
Na volbě primitivní funkce nezáleží, protože primitivní funkce se liší o konstantu.

Zdroj: [[ma1a-23k8.pdf#page=5|MA1A k8, P8.5]]

Pro spojité funkce na uzavřeném intervalu tedy výpočet určitého integrálu obvykle probíhá takto: najít primitivní funkci, dosadit horní mez a odečíst hodnotu v dolní mezi. U substituce v určitém integrálu je nutné přepočítat meze.

Zdroj: [[ma1a-23k8.pdf#page=6|MA1A k8, P8.6]]

Pro sudé a liché funkce platí na symetrickém intervalu:
$$
\int_{-a}^{a} f(x)\,dx=0 \quad \text{pro lichou } f,
$$
$$
\int_{-a}^{a} f(x)\,dx=2\int_0^a f(x)\,dx \quad \text{pro sudou } f.
$$

Zdroj: [[ma1a-23k8.pdf#page=6|MA1A k8, P8.6]]

Věta o střední hodnotě: je-li $f$ spojitá na $[a,b]$, existuje $c\in(a,b)$ tak, že
$$
\int_a^b f(x)\,dx=f(c)(b-a).
$$

Zdroj: [[ma1a-23k8.pdf#page=7|MA1A k8, P8.7]]

## Nevlastní integrál

Nevlastní integrál vzniká, pokud je interval neomezený nebo pokud funkce není omezená v některém bodě intervalu. Singulární bod integrace může být krajní bod $\pm\infty$ nebo bod, kde je funkce neomezená v každém prstencovém okolí.

Zdroj: [[ma1a-23k9.pdf#page=1|MA1A k9, P9.1]]

Pokud je singulární horní mez $b$, definuje se
$$
\int_a^b f(x)\,dx=\lim_{\beta\to b-}\int_a^\beta f(x)\,dx.
$$
Pokud je singulární dolní mez $a$, definuje se
$$
\int_a^b f(x)\,dx=\lim_{\alpha\to a+}\int_\alpha^b f(x)\,dx.
$$
Integrál konverguje, pokud je příslušná limita konečná. Diverguje k $+\infty$ nebo $-\infty$, pokud je limita nevlastní.

Zdroj: [[ma1a-23k9.pdf#page=1|MA1A k9, P9.1]]

Je-li více singulárních bodů, interval se rozdělí přípustným dělením a všechny dílčí nevlastní integrály musejí existovat tak, aby byl definován jejich součet. Nesmí se například mechanicky odečítat dva integrály, které divergují k nekonečnu.

Zdroj: [[ma1a-23k9.pdf#page=2|MA1A k9, P9.2]]

Srovnávací kritérium: pokud $|f|\le g$, funkce $f$ je po částech spojitá a $\int_a^b g$ konverguje, pak konverguje také $\int_a^b f$. Pro dokazování divergence se používají opačné odhady na funkce s kladným integrálem divergujícím k $+\infty$.

Zdroj: [[ma1a-23k9.pdf#page=4|MA1A k9, P9.4]]

Základní testovací integrály:
$$
\int_0^1 x^\alpha\,dx \text{ konverguje právě tehdy, když } \alpha>-1,
$$
$$
\int_1^\infty x^\alpha\,dx \text{ konverguje právě tehdy, když } \alpha<-1,
$$
$$
\int_0^\infty e^{\alpha x}\,dx \text{ konverguje právě tehdy, když } \alpha<0.
$$

Zdroj: [[ma1a-23k9.pdf#page=4|MA1A k9, P9.4]]

## Aplikace určitého integrálu

Obsah plochy mezi grafy spojitých funkcí $f\le g$ na $[a,b]$ je
$$
S=\int_a^b (g(x)-f(x))\,dx.
$$

Zdroj: [[ma1a-23k10.pdf#page=1|MA1A k10, P10.1]]

Délka grafu funkce s kontinuální derivací na $[a,b]$ je
$$
\ell=\int_a^b \sqrt{1+(f'(x))^2}\,dx.
$$

Zdroj: [[ma1a-23k10.pdf#page=1|MA1A k10, P10.1]]

Pro kladnou spojitou funkci $f$ je objem rotačního tělesa kolem osy $x$
$$
V=\pi\int_a^b (f(x))^2\,dx,
$$
a obsah rotační plochy je
$$
Q=2\pi\int_a^b f(x)\sqrt{1+(f'(x))^2}\,dx.
$$

Zdroj: [[ma1a-23k10.pdf#page=2|MA1A k10, P10.2]]

## Minimum ke zkoušce

U neurčitého integrálu se hledá celá třída primitivních funkcí $F+c$. U určitého integrálu jde o číslo, které je definované přes Riemannovy součty a prakticky se často počítá Newtonovou-Leibnizovou formulí. U nevlastního integrálu je hlavní chyba zapomenout na limitu v singulárním bodě nebo nerozdělit interval při více singularitách.

Zdroj: souhrn podle [[ma1a-23k7.pdf]], [[ma1a-23k8.pdf]], [[ma1a-23k9.pdf]]
