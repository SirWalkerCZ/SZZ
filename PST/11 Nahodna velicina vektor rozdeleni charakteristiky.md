# 11 Náhodná veličina, náhodný vektor, rozdělení a charakteristiky

**Otázka:** Náhodná veličina a náhodný vektor. Distribuční funkce, hustota a pravděpodobnostní funkce náhodné veličiny. Střední hodnota a rozptyl náhodné veličiny a jejich odhady. Korelace a nezávislost náhodných veličin.

## Náhodná veličina

Náhodná veličina je reálná funkce $X$ definovaná na pravděpodobnostním prostoru $(\Omega,\mathcal A,P)$, která je měřitelným zobrazením

$$
X:(\Omega,\mathcal A)\to (\mathbb R,\mathcal B),
$$

tedy pro každou borelovskou množinu $B\in\mathcal B$ platí

$$
\{\omega\in\Omega\mid X(\omega)\in B\}\in\mathcal A.
$$

Zjednodušeně se píše například $\{X\in B\}$ nebo $\{X<x\}$. Součty, součiny, podíly, minima, maxima, mocniny a násobky náhodných veličin jsou opět náhodné veličiny.

Zdroj: [[01PST_zapisky.pdf#page=7|PST, s. 7]]

## Distribuční funkce

Distribuční funkce náhodné veličiny $X$ je funkce

$$
F_X(x)=P(X\le x), \qquad x\in\mathbb R.
$$

Má tři základní vlastnosti:

1. Je neklesající.
2. Je zprava spojitá.
3. Platí

$$
\lim_{x\to -\infty}F_X(x)=0, \qquad
\lim_{x\to \infty}F_X(x)=1.
$$

Distribuční funkce jednoznačně určuje rozdělení pravděpodobnosti náhodné veličiny.

Zdroj: [[01PST_zapisky.pdf#page=7|PST, s. 7]], [[01PST_zapisky.pdf#page=9|PST, s. 9]]

## Diskrétní náhodná veličina a pravděpodobnostní funkce

Náhodná veličina $X$ je diskrétní, pokud nabývá konečně nebo spočetně mnoha hodnot $x_1,x_2,\dots$ s pravděpodobnostmi

$$
p_n=P(X=x_n), \qquad p_n\ge 0, \qquad \sum_{n=1}^{\infty}p_n=1.
$$

Funkce $p_X(x_n)=P(X=x_n)$ se běžně chápe jako pravděpodobnostní funkce diskrétní náhodné veličiny. Distribuční funkce má tvar

$$
F_X(x)=P(X\le x)=\sum_{\{n:x_n\le x\}}p_n.
$$

Pro interval $(a,b]$ platí

$$
P(a<X\le b)=F_X(b)-F_X(a)=\sum_{\{n:a<x_n\le b\}}p_n.
$$

Distribuční funkce diskrétní veličiny je schodovitá a velikost skoku v bodě $x_n$ je $p_n$.

Zdroj: [[01PST_zapisky.pdf#page=7|PST, s. 7-8]]

## Absolutně spojitá náhodná veličina a hustota

Náhodná veličina $X$ je absolutně spojitá, pokud existuje nezáporná integrovatelná funkce $f_X$ taková, že

$$
F_X(x)=P(X\le x)=\int_{-\infty}^{x} f_X(t)\,dt.
$$

Funkce $f_X$ se nazývá hustota rozdělení pravděpodobnosti. Platí

$$
\int_{-\infty}^{\infty}f_X(x)\,dx=1
$$

a pro $a\le b$

$$
P(a<X\le b)=\int_a^b f_X(x)\,dx.
$$

Pokud existuje derivace distribuční funkce, pak $f_X(x)=F_X'(x)$ skoro jistě. U spojité náhodné veličiny se pravděpodobnost intervalu počítá integrací hustoty, ne hodnotou hustoty v bodě.

Zdroj: [[01PST_zapisky.pdf#page=8|PST, s. 8]]

## Střední hodnota

Střední hodnota je základní charakteristika polohy rozdělení. Pro diskrétní náhodnou veličinu s hodnotami $x_i$ a pravděpodobnostmi $p_i$ je

$$
EX=\sum_{i=1}^{\infty}x_i p_i,
$$

pokud řada konverguje. Pro absolutně spojitou náhodnou veličinu s hustotou $f_X$ je

$$
EX=\int_{-\infty}^{\infty}x f_X(x)\,dx,
$$

pokud integrál existuje.

Základní vlastnosti:

$$
E(aX+bY)=aEX+bEY,
$$

$$
X_1\le X\le X_2 \text{ skoro jistě } \Rightarrow EX_1\le EX\le EX_2.
$$

Pro funkci náhodné veličiny platí u diskrétního rozdělení

$$
E\varphi(X)=\sum_n \varphi(x_n)p_n
$$

a u spojitého rozdělení

$$
E\varphi(X)=\int_{-\infty}^{\infty}\varphi(x)f_X(x)\,dx.
$$

Zdroj: [[01PST_zapisky.pdf#page=9|PST, s. 9-10]]

## Rozptyl, momenty a kovariance

$n$-tý moment náhodné veličiny je $EX^n$ a $n$-tý centrální moment je $E(X-EX)^n$. Rozptyl je druhý centrální moment:

$$
\operatorname{var}X=E(X-EX)^2.
$$

Pro výpočet je často vhodný vztah

$$
\operatorname{var}X=E(X^2)-(EX)^2.
$$

Pro konstantu $c$ a reálné číslo $a$ platí

$$
\operatorname{var}c=0, \qquad
\operatorname{var}(aX)=a^2\operatorname{var}X, \qquad
\operatorname{var}(X+c)=\operatorname{var}X.
$$

Kovariance veličin $X,Y$ s konečnými druhými momenty je

$$
\operatorname{cov}(X,Y)=E(X-EX)(Y-EY).
$$

Platí

$$
\operatorname{var}(X+Y)=\operatorname{var}X+\operatorname{var}Y+2\operatorname{cov}(X,Y),
$$

$$
\operatorname{cov}(X,Y)=E(XY)-EXEY.
$$

Speciálně $\operatorname{cov}(X,X)=\operatorname{var}X$.

Zdroj: [[01PST_zapisky.pdf#page=11|PST, s. 11]]

## Odhady střední hodnoty a rozptylu
Ve statistice pracujeme s náhodným výběrem

$$
X=(X_1,\dots,X_n)^T,
$$

kde $X_1,\dots,X_n$ jsou nezávislé stejně rozdělené náhodné veličiny. Výběrový průměr

$$
\overline X_n=\frac1n\sum_{i=1}^n X_i
$$

se používá jako odhad střední hodnoty $EX_1$. Výběrový rozptyl je

$$
S_n^2=\frac1{n-1}\sum_{i=1}^n (X_i-\overline X_n)^2
$$

a používá se jako odhad rozptylu. Výběrová směrodatná odchylka je

$$
S_n=\sqrt{S_n^2}.
$$

U normálního rozdělení podklad uvádí, že výběrový průměr a výběrový rozptyl jsou nezávislé, $\overline X_n\sim N(\mu,\sigma^2/n)$ a veličina $(n-1)S_n^2/\sigma^2$ má chí-kvadrát rozdělení o $n-1$ stupních volnosti. Tyto vztahy jsou základem pro intervalové odhady a t-testy v [[12 CLV MLE testovani hypotez#Testy střední hodnoty|testech střední hodnoty]].

Zdroj: [[01PST_zapisky.pdf#page=25|PST, s. 25]]

## Náhodný vektor

Náhodný vektor je vektor náhodných veličin

$$
X=(X_1,\dots,X_n)^T.
$$

Jeho sdružená distribuční funkce je

$$
F_X(x_1,\dots,x_n)=P(X_1\le x_1,\dots,X_n\le x_n).
$$

Diskrétní náhodný vektor má hodnoty $x_k\in\mathbb R^n$ s pravděpodobnostmi $p_k=P(X=x_k)$, kde $\sum_k p_k=1$. Absolutně spojitý náhodný vektor má sdruženou hustotu $f_X$ splňující

$$
F_X(x_1,\dots,x_n)=\int_{-\infty}^{x_1}\cdots\int_{-\infty}^{x_n} f_X(t_1,\dots,t_n)\,dt_1\cdots dt_n.
$$

Marginální rozdělení je rozdělení podvektoru. U spojitého náhodného vektoru se marginální hustota získá integrací sdružené hustoty přes ostatní proměnné.

Zdroj: [[01PST_zapisky.pdf#page=19|PST, s. 19-21]]

## Korelace

Pro náhodný vektor se zavádí varianční matice s prvky

$$
\operatorname{cov}(X_i,X_j)
$$

a korelační matice s prvky

$$
\operatorname{corr}(X_i,X_j)=\frac{\operatorname{cov}(X_i,X_j)}{\sqrt{\operatorname{var}X_i\operatorname{var}X_j}}.
$$

Korelace je normalizovaná kovariance a platí

$$
-1\le \operatorname{corr}(X,Y)\le 1.
$$

Korelace měří lineární vztah mezi veličinami. Pokud je kovariance nulová, veličiny jsou nekorelované.

Zdroj: [[01PST_zapisky.pdf#page=21|PST, s. 21]]

## Nezávislost náhodných veličin

Náhodné veličiny $X_1,\dots,X_n$ jsou vzájemně nezávislé, pokud pro každou volbu podmnožiny indexů a všechna reálná $x_{i_j}$ platí

$$
P\left(\bigcap_{j=1}^{r}\{X_{i_j}<x_{i_j}\}\right)=
\prod_{j=1}^{r}P(X_{i_j}<x_{i_j}).
$$

V praxi se nezávislost ověřuje jednodušeji:

- U diskrétního náhodného vektoru musí být sdružená pravděpodobnost rovna součinu marginálních pravděpodobností.
- U absolutně spojitého náhodného vektoru musí být sdružená hustota součinem marginálních hustot:

$$
f_X(x_1,\dots,x_n)=f_{X_1}(x_1)\cdots f_{X_n}(x_n).
$$

Jsou-li $X,Y$ nezávislé a mají konečné střední hodnoty, pak

$$
E(XY)=EX\,EY.
$$

Pokud mají navíc konečné druhé momenty, pak

$$
\operatorname{cov}(X,Y)=0.
$$

Z nezávislosti tedy plyne nekorelovanost, ale opačně to obecně neplatí.

Zdroj: [[01PST_zapisky.pdf#page=21|PST, s. 21-22]]
