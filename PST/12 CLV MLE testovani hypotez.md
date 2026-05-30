# 12 CLV, maximální věrohodnost a testování hypotéz

**Otázka:** Centrální limitní věta. Metoda maximální věrohodnosti. Základní principy statistického testování hypotéz, testy střední hodnoty. Chí-kvadrát test dobré shody.

## Centrální limitní věta

Centrální limitní věta říká, že součet velkého počtu vzájemně nezávislých náhodných veličin má za obecných podmínek přibližně normální rozdělení. V podkladu je uvedena Lévyho-Lindebergova verze CLV.

Nechť $X_1,X_2,\dots$ jsou nezávislé stejně rozdělené náhodné veličiny se střední hodnotou $\mu$ a konečným rozptylem $\sigma^2$. Označme

$$
Z_n=\frac{\sum_{k=1}^{n}X_k-n\mu}{\sqrt{n\sigma^2}}.
$$

Je-li $F_n$ distribuční funkce veličiny $Z_n$, potom

$$
\lim_{n\to\infty}F_n(x)=\Phi(x)
$$

pro všechna $x\in\mathbb R$, kde $\Phi$ je distribuční funkce normovaného normálního rozdělení $N(0,1)$.

Zkratka i.i.d. znamená, že veličiny jsou nezávislé a stejně rozdělené. Praktický význam CLV je v tom, že pro velké $n$ lze součty a průměry aproximovat normálním rozdělením. To se používá v intervalových odhadech a testech.

Zdroj: [[01PST_zapisky.pdf#page=23|PST, s. 23]]

## Náhodný výběr a výběrové charakteristiky

Náhodný výběr je náhodný vektor

$$
X=(X_1,\dots,X_n)^T,
$$

jehož složky jsou nezávislé stejně rozdělené náhodné veličiny s distribuční funkcí $F_\theta$ závislou na parametru $\theta$. Číslo $n$ je rozsah výběru.

Výběrový průměr je

$$
\overline X_n=\frac1n\sum_{i=1}^n X_i
$$

a výběrový rozptyl je

$$
S_n^2=\frac1{n-1}\sum_{i=1}^n (X_i-\overline X_n)^2.
$$

Tyto veličiny jsou základ pro [[11 Nahodna velicina vektor rozdeleni charakteristiky#Odhady střední hodnoty a rozptylu|odhady střední hodnoty a rozptylu]] a pro t-testy.

Zdroj: [[01PST_zapisky.pdf#page=25|PST, s. 25]]

## Bodový odhad

Bodový odhad parametru $\theta$ je funkce náhodného výběru

$$
\theta^*(X),
$$

jejíž předpis nezávisí na $\theta$. Odhad je nestranný, jestliže

$$
E\theta^*(X)=\theta.
$$

V praktickém výpočtu se po dosazení naměřených dat obvykle pracuje s konkrétním číslem $\widehat\theta$, které má co nejlépe popsat neznámý parametr.

Zdroj: [[01PST_zapisky.pdf#page=28|PST, s. 28]]

## Metoda momentů

Metoda momentů vychází ze srovnání teoretických momentů rozdělení s výběrovými momenty. Máme-li parametry $\theta_1,\dots,\theta_k$ a existují momenty $EX_1^i$ pro $i=1,\dots,k$, položíme

$$
EX_1^i=m_i,
$$

kde

$$
m_i=\frac1n\sum_{j=1}^{n}x_j^i.
$$

Vznikne soustava $k$ rovnic pro $k$ neznámých parametrů. Pro dva parametry lze místo prvních dvou momentů použít rovnice

$$
EX_1=\overline X_n, \qquad \operatorname{var}X_1=S_n^2.
$$

Podklad upozorňuje, že nevýhodou této metody může být velký rozptyl odhadu.

Zdroj: [[01PST_zapisky.pdf#page=28|PST, s. 28]]

## Metoda maximální věrohodnosti

Metoda maximální věrohodnosti volí takový parametr, při kterém jsou pozorovaná data nejpravděpodobnější podle daného modelu.

V diskrétním případě je věrohodnostní funkce

$$
L(\theta)=\prod_{i=1}^{n}P_\theta(X_1=x_i).
$$

V absolutně spojitém případě je

$$
L(\theta)=\prod_{i=1}^{n}f_\theta(x_i).
$$

Maximálně věrohodný odhad $\widehat\theta$ splňuje

$$
L(\widehat\theta)=\max_{\theta\in\Theta}L(\theta).
$$

V praxi se často maximalizuje logaritmická věrohodnost

$$
l(\theta)=\log L(\theta),
$$

protože součin se změní na součet. Typický postup je:

1. Sestavit $L(\theta)$.
2. Spočítat $l(\theta)=\log L(\theta)$.
3. Položit

$$
\frac{\partial l(\theta)}{\partial \theta}=0.
$$

4. Vyřešit rovnici a ověřit, že nalezená hodnota dává maximum.

Zdroj: [[01PST_zapisky.pdf#page=28|PST, s. 28-29]]

## Princip testování hypotéz

Nechť náhodný výběr pochází z rozdělení závislého na parametru $\theta\in\Theta$. Nulová hypotéza je tvrzení

$$
H_0:\theta\in\Theta_0,
$$

testované proti alternativě

$$
H_A:\theta\in\Theta\setminus\Theta_0.
$$

Typicky se testuje

$$
H_0:\theta=\theta_0
$$

proti oboustranné alternativě $H_A:\theta\ne\theta_0$ nebo jednostranným alternativám $H_A:\theta>\theta_0$, případně $H_A:\theta<\theta_0$.

Test je určen kritickou oblastí $W$: pokud pozorovaný výběr spadne do $W$, hypotézu $H_0$ zamítáme.

Mohou nastat čtyři situace:

- $H_0$ platí a test ji nezamítne.
- $H_0$ neplatí a test ji zamítne.
- $H_0$ platí, ale test ji zamítne: chyba prvního druhu.
- $H_0$ neplatí, ale test ji nezamítne: chyba druhého druhu.

Hladina testu $\alpha$ se volí tak, aby pravděpodobnost chyby prvního druhu nebyla větší než $\alpha$. Nejmenší hladina $\alpha$, pro kterou test zamítá $H_0$ ve prospěch $H_A$, se nazývá p-hodnota.

Zdroj: [[01PST_zapisky.pdf#page=32|PST, s. 32]]

## Testování pomocí intervalových odhadů

Intervalové odhady lze použít k testování střední hodnoty. Máme-li intervalový odhad pro $\mu$ o spolehlivosti $1-\alpha$

$$
(\mu_L,\mu_U),
$$

potom při testu

$$
H_0:\mu=\mu_0, \qquad H_A:\mu\ne\mu_0
$$

zamítáme $H_0$, pokud

$$
\mu_0\notin (\mu_L,\mu_U).
$$

U jednostranných alternativ se používají jednostranné intervalové odhady.

Zdroj: [[01PST_zapisky.pdf#page=32|PST, s. 32]]

## Testy střední hodnoty

### Jednovýběrový t-test

Nechť $X_1,\dots,X_n$ je náhodný výběr z normálního rozdělení $N(\mu,\sigma^2)$, kde $\sigma^2$ není známé. Pro test

$$
H_0:\mu=\mu_0, \qquad H_A:\mu\ne\mu_0
$$

se počítá testová statistika

$$
T_0=\frac{\overline X_n-\mu_0}{S_n}\sqrt n.
$$

Hypotézu $H_0$ zamítáme, pokud

$$
|T_0|\ge t_{1-\alpha/2,n-1}.
$$

Pro jednostrannou alternativu $H_A:\mu>\mu_0$ zamítáme, pokud

$$
T_0\ge t_{1-\alpha,n-1}.
$$

Pro alternativu $H_A:\mu<\mu_0$ zamítáme, pokud

$$
T_0\le t_{\alpha,n-1}.
$$

### Párový t-test

U párových dat $(Y_i,Z_i)$ se vytvoří rozdíly

$$
X_i=Y_i-Z_i
$$

a na tyto rozdíly se použije jednovýběrový t-test, pokud pocházejí z normálního rozdělení.

### Dvouvýběrový t-test

Mějme nezávislé výběry z $N(\mu_1,\sigma^2)$ a $N(\mu_2,\sigma^2)$ se společným neznámým rozptylem. Pro test

$$
H_0:\mu_1-\mu_2=\mu_0, \qquad H_A:\mu_1-\mu_2\ne\mu_0
$$

se počítá

$$
T_0=\frac{\overline X-\overline Y-\mu_0}
{\sqrt{(m-1)S_X^2+(n-1)S_Y^2}}
\sqrt{\frac{mn(m+n-2)}{m+n}}.
$$

Hypotézu $H_0$ zamítáme, pokud

$$
|T_0|\ge t_{1-\alpha/2,m+n-2}.
$$

Základní předpoklad t-testů je normalita dat. Podklad zmiňuje ověřování normality graficky pomocí histogramu nebo Q-Q plotu.

Zdroj: [[01PST_zapisky.pdf#page=33|PST, s. 33-35]]

## Chí-kvadrát test dobré shody

Chí-kvadrát test dobré shody testuje, zda skutečné pravděpodobnosti kategorií odpovídají předem zadaným hodnotám $p_1,\dots,p_k$.

Předpokládejme, že v jednom pokusu může nastat právě jeden z jevů $A_1,\dots,A_k$ a $p_i=P(A_i)$, kde

$$
\sum_{i=1}^{k}p_i=1.
$$

Pokus opakujeme $n$-krát a $X_i$ označuje počet výskytů jevu $A_i$. Testujeme

$$
H_0:\text{ skutečné pravděpodobnosti jsou }p_1,\dots,p_k
$$

proti alternativě, že aspoň jedna pravděpodobnost je jiná.

Testová statistika je

$$
\chi^2=\sum_{i=1}^{k}\frac{(X_i-np_i)^2}{np_i}.
$$

Hypotézu $H_0$ zamítáme, pokud

$$
\chi^2>\chi^2_{1-\alpha,k-1}.
$$

Jinak $H_0$ nezamítáme. Vzorec porovnává pozorované četnosti $X_i$ s očekávanými četnostmi $np_i$.

Zdroj: [[01PST_zapisky.pdf#page=35|PST, s. 35-36]]

## Test nezávislosti v kontingenční tabulce

Podklad po testu dobré shody uvádí také test nezávislosti dvou diskrétních veličin. Pro výběr dvojic $(Y_i,Z_i)$ se vytvoří kontingenční tabulka se sdruženými četnostmi $n_{ij}$ a marginálními četnostmi

$$
n_{i\cdot}=\sum_j n_{ij}, \qquad n_{\cdot j}=\sum_i n_{ij}.
$$

Testuje se

$$
H_0:\text{$Y$ a $Z$ jsou nezávislé}
$$

proti alternativě, že nezávislé nejsou. Testová statistika je

$$
\chi^2=\sum_{i=1}^{r}\sum_{j=1}^{c}
\frac{\left(n_{ij}-\frac{n_{i\cdot}n_{\cdot j}}{n}\right)^2}
{\frac{n_{i\cdot}n_{\cdot j}}{n}}.
$$

Hypotézu $H_0$ zamítáme, pokud

$$
\chi^2\ge \chi^2_{1-\alpha,(r-1)(c-1)}.
$$

Tento test souvisí s pojmem [[11 Nahodna velicina vektor rozdeleni charakteristiky#Nezávislost náhodných veličin|nezávislosti náhodných veličin]].

Zdroj: [[01PST_zapisky.pdf#page=36|PST, s. 36]]
