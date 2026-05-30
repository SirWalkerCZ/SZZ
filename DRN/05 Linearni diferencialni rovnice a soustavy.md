---
aliases:
  - DRN 05
  - Lineární diferenciální rovnice vyšších řádů a soustavy
predmet: DRN
okruh: 5
---

# Lineární diferenciální rovnice vyšších řádů a soustavy

> [!info] Zdroje
> Hlavní podklad: [[dnbook.pdf]], kapitoly 15, 16, 26 a 27. Originální text je anglicky, poznámky jsou přeložené a zestručněné česky.

## Lineární diferenciální rovnice řádu $n$

Lineární obyčejná diferenciální rovnice řádu $n$ má tvar
$$
y^{(n)}+a_{n-1}(x)y^{(n-1)}+\dots+a_1(x)y'+a_0(x)y=b(x).
$$
Je homogenní, pokud $b(x)=0$. Neznámá funkce $y$ a její derivace se v rovnici vyskytují jen lineárně; koeficienty $a_i(x)$ mohou záviset na $x$.

Zdroj: [[dnbook.pdf#page=151|dnbook, kap. 15, str. 151]]

Pokud jsou $a_0,\dots,a_{n-1},b$ spojité na otevřeném intervalu $I$, pak pro libovolné $x_0\in I$ a libovolné počáteční hodnoty
$$
y(x_0)=y_0,\quad y'(x_0)=y_1,\quad \dots,\quad y^{(n-1)}(x_0)=y_{n-1}
$$
existuje právě jedno řešení na $I$.

Zdroj: [[dnbook.pdf#page=152|dnbook, věta 15.2, str. 152]]

## Homogenní lineární rovnice

U homogenní rovnice
$$
y^{(n)}+a_{n-1}(x)y^{(n-1)}+\dots+a_0(x)y=0
$$
tvoří množina všech řešení na intervalu $I$ lineární prostor dimenze $n$. Proto stačí najít $n$ lineárně nezávislých řešení; jejich báze se nazývá fundamentální systém řešení.

Zdroj: [[dnbook.pdf#page=152|dnbook, věta 15.3, str. 152]], [[dnbook.pdf#page=155|dnbook, definice 15.5, str. 155]]

Pro test lineární nezávislosti se používá Wronskián
$$
W(y_1,\dots,y_n)(x)=
\det
\begin{pmatrix}
y_1 & y_2 & \dots & y_n\\
y_1' & y_2' & \dots & y_n'\\
\vdots & \vdots & \ddots & \vdots\\
y_1^{(n-1)} & y_2^{(n-1)} & \dots & y_n^{(n-1)}
\end{pmatrix}.
$$
Pro fundamentální systém homogenní lineární rovnice není Wronskián nulový na celém intervalu.

Zdroj: [[dnbook.pdf#page=156|dnbook, definice 15.6, str. 156]]

## Konstantní koeficienty a charakteristická rovnice

Nejdůležitější řešitelný případ je homogenní lineární rovnice s konstantními koeficienty
$$
y^{(n)}+a_{n-1}y^{(n-1)}+\dots+a_1y'+a_0y=0.
$$
Zkouší se řešení $y=e^{\lambda x}$. Po dosazení vznikne charakteristická rovnice
$$
\lambda^n+a_{n-1}\lambda^{n-1}+\dots+a_1\lambda+a_0=0.
$$

Zdroj: [[dnbook.pdf#page=158|dnbook, kap. 15, str. 158]]

Z kořenů charakteristické rovnice se skládá fundamentální systém:

- reálný jednoduchý kořen $\lambda$ dává řešení $e^{\lambda x}$,
- reálný kořen násobnosti $m$ dává řešení
$$
e^{\lambda x},\; xe^{\lambda x},\; \dots,\; x^{m-1}e^{\lambda x},
$$
- komplexní kořeny $\lambda=\alpha\pm i\beta$ dávají reálná řešení
$$
e^{\alpha x}\cos(\beta x),\qquad e^{\alpha x}\sin(\beta x),
$$
a při násobnosti $m$ se násobí ještě mocninami $1,x,\dots,x^{m-1}$.

Zdroj: [[dnbook.pdf#page=160|dnbook, kap. 15, str. 160]], [[dnbook.pdf#page=162|dnbook, kap. 15, str. 162]]

Obecné řešení homogenní rovnice je lineární kombinace řešení z fundamentálního systému:
$$
y_h(x)=c_1u_1(x)+\dots+c_nu_n(x).
$$

Zdroj: [[dnbook.pdf#page=155|dnbook, kap. 15, str. 155]]

## Nehomogenní lineární rovnice

K nehomogenní rovnici
$$
L[y]=b(x)
$$
se přiřazuje homogenní rovnice
$$
L[y]=0.
$$
Pokud $y_p$ je jedno konkrétní řešení nehomogenní rovnice a $y_h$ je obecné řešení přidružené homogenní rovnice, pak obecné řešení nehomogenní rovnice je
$$
y=y_p+y_h.
$$
To je základní strukturální věta pro lineární rovnice.

Zdroj: [[dnbook.pdf#page=167|dnbook, definice 16.1 a věta 16.2, str. 167]]

Související: numerický pohled na úlohy, kde analytický tvar řešení nemáme, je v [[06 Numericke metody rovnic integralu a diferencialnich rovnic#Numerické řešení diferenciálních rovnic|numerickém řešení diferenciálních rovnic]].

## Metoda neurčitých koeficientů

Metoda neurčitých koeficientů se používá pro lineární rovnice s konstantními koeficienty a pravou stranou složenou ze speciálních členů. Typické členy jsou polynom, exponenciála, sinus a kosinus, případně jejich součiny tvaru
$$
p(x)e^{\alpha x}\cos(\beta x)+q(x)e^{\alpha x}\sin(\beta x).
$$

Zdroj: [[dnbook.pdf#page=169|dnbook, kap. 16a, str. 169]], [[dnbook.pdf#page=172|dnbook, kap. 16a, str. 172]]

Postup:

1. Vyřeší se přidružená homogenní rovnice a zjistí se charakteristická čísla.
2. Podle tvaru pravé strany se zvolí odhad $y_p$ se zatím neurčenými koeficienty.
3. Pokud speciální číslo pravé strany odpovídá kořenu charakteristické rovnice násobnosti $m$, odhad se vynásobí $x^m$.
4. Odhad se dosadí do rovnice a porovnáním koeficientů se dopočítají neznámé konstanty.

Zdroj: [[dnbook.pdf#page=181|dnbook, algoritmus 16a.5, str. 181]]

## Variace konstant

Variace konstant je obecnější metoda. Předpokládáme, že známe fundamentální systém $u_1,\dots,u_n$ přidružené homogenní rovnice. Hledáme partikulární řešení ve tvaru
$$
y_p(x)=c_1(x)u_1(x)+\dots+c_n(x)u_n(x).
$$
Funkce $c_i(x)$ se určují ze soustavy
$$
\sum_{i=1}^n c_i'(x)u_i(x)=0,
$$
$$
\sum_{i=1}^n c_i'(x)u_i'(x)=0,
$$
$$
\dots
$$
$$
\sum_{i=1}^n c_i'(x)u_i^{(n-1)}(x)=b(x).
$$
Matice této soustavy je Wronského matice fundamentálního systému, takže je regulární. Po vyřešení pro $c_i'(x)$ se integruje a dosadí zpět.

Zdroj: [[dnbook.pdf#page=188|dnbook, kap. 16b, str. 188]], [[dnbook.pdf#page=189|dnbook, algoritmus 16b.1, str. 189]]

Prakticky: metoda neurčitých koeficientů je rychlá pro „hezké“ pravé strany, variace konstant je systematičtější, ale výpočetně náročnější a závisí na integraci.

Zdroj: [[dnbook.pdf#page=189|dnbook, shrnutí 16c, str. 189]]

## Soustavy lineárních diferenciálních rovnic

Soustava lineárních ODE prvního řádu s konstantními koeficienty má tvar
$$
y_1'=a_{11}y_1+a_{12}y_2+\dots+a_{1n}y_n+b_1(x),
$$
$$
y_2'=a_{21}y_1+a_{22}y_2+\dots+a_{2n}y_n+b_2(x),
$$
$$
\dots
$$
$$
y_n'=a_{n1}y_1+a_{n2}y_2+\dots+a_{nn}y_n+b_n(x).
$$
V maticovém tvaru se píše
$$
\mathbf{y}'=A\mathbf{y}+\mathbf{b}(x).
$$
Je homogenní, pokud $\mathbf{b}(x)=\mathbf{0}$.

Zdroj: [[dnbook.pdf#page=266|dnbook, definice 26.1, str. 266]], [[dnbook.pdf#page=271|dnbook, kap. 26a, str. 271]]

Pro spojité pravé strany $b_i(x)$ existuje pro každé $x_0$ a každou počáteční hodnotu
$$
\mathbf{y}(x_0)=\mathbf{y}_0
$$
právě jedno řešení na daném intervalu.

Zdroj: [[dnbook.pdf#page=271|dnbook, věta 26.6, str. 271]]

## Převod rovnice vyššího řádu na soustavu

Každou lineární ODE řádu $n$ lze převést na soustavu $n$ rovnic prvního řádu. Pro rovnici
$$
y^{(n)}+a_{n-1}(x)y^{(n-1)}+\dots+a_1(x)y'+a_0(x)y=b(x)
$$
se zavede
$$
y_1=y,
\qquad
 y_2=y_1',
\qquad
\dots,
\qquad
 y_n=y_{n-1}'.
$$
Dostaneme soustavu
$$
y_1'=y_2,
$$
$$
y_2'=y_3,
$$
$$
\dots
$$
$$
y_n'=-a_0(x)y_1-a_1(x)y_2-\dots-a_{n-1}(x)y_n+b(x).
$$
Počáteční podmínky pro derivace $y^{(k)}(x_0)$ se přepíšou na počáteční hodnoty složek $y_{k+1}(x_0)$.

Zdroj: [[dnbook.pdf#page=270|dnbook, algoritmus 26.4, str. 270]]

## Homogenní soustavy a vlastní čísla

U homogenní soustavy
$$
\mathbf{y}'=A\mathbf{y}
$$
tvoří řešení lineární prostor dimenze $n$. Pokud má matice $A$ vlastní číslo $\lambda$ a vlastní vektor $\mathbf{v}$, pak
$$
\mathbf{y}(x)=e^{\lambda x}\mathbf{v}
$$
je řešení soustavy.

Zdroj: [[dnbook.pdf#page=272|dnbook, věta 26b.1, str. 272]], [[dnbook.pdf#page=274|dnbook, kap. 26b, str. 274]]

Pro reálná vlastní čísla se řešení skládají přímo z $e^{\lambda x}\mathbf{v}$. Pro komplexní dvojici $\lambda=\alpha\pm i\beta$ se z komplexního řešení vezme reálná a imaginární část; tím vzniknou reálná řešení s faktorem $e^{\alpha x}$ a funkcemi $\cos(\beta x)$, $\sin(\beta x)$.

Zdroj: [[dnbook.pdf#page=276|dnbook, kap. 26b, str. 276]]

## Nehomogenní soustavy

Pro nehomogenní soustavu platí stejná struktura jako u jedné rovnice:
$$
\mathbf{y}=\mathbf{y}_p+\mathbf{y}_h.
$$
Stačí tedy najít jedno partikulární řešení a přičíst obecné řešení přidružené homogenní soustavy.

Zdroj: [[dnbook.pdf#page=279|dnbook, kap. 27, str. 279]]

Variace konstant pro soustavy: pokud $Y(x)$ je fundamentální matice homogenní soustavy, hledá se
$$
\mathbf{y}_p(x)=Y(x)\mathbf{c}(x).
$$
Po dosazení vyjde
$$
Y(x)\mathbf{c}'(x)=\mathbf{b}(x),
$$
tedy
$$
\mathbf{c}'(x)=Y(x)^{-1}\mathbf{b}(x).
$$
Po integraci dostaneme $\mathbf{c}(x)$ a tím partikulární řešení.

Zdroj: [[dnbook.pdf#page=280|dnbook, kap. 27a, str. 280]]

Metoda neurčitých koeficientů pro soustavy funguje podobně jako u jedné rovnice: podle tvarů pravých stran se odhadnou všechny složky $y_i$, dosadí se do soustavy a porovnáním koeficientů vznikne soustava lineárních rovnic pro neznámé konstanty.

Zdroj: [[dnbook.pdf#page=285|dnbook, algoritmus 27b.1, str. 285]]

## Minimum ke zkoušce

Je potřeba umět rozeznat lineární rovnici, sestavit charakteristickou rovnici, z kořenů zapsat homogenní řešení a u nehomogenní rovnice použít princip
$$
y=y_p+y_h.
$$
U soustav je klíčové maticové psaní $\mathbf{y}'=A\mathbf{y}+\mathbf{b}$, vazba na vlastní čísla matice $A$ a převod vyššího řádu na soustavu prvního řádu.

Zdroj: souhrn podle [[dnbook.pdf#page=151|dnbook, kap. 15]], [[dnbook.pdf#page=167|dnbook, kap. 16]], [[dnbook.pdf#page=266|dnbook, kap. 26]], [[dnbook.pdf#page=279|dnbook, kap. 27]]
