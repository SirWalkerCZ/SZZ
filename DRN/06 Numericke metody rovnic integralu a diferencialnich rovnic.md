---
aliases:
  - DRN 06
  - Numerické metody řešení rovnic, integrálů a diferenciálních rovnic
predmet: DRN
okruh: 6
---

# Numerické metody řešení rovnic, integrálů a diferenciálních rovnic

> [!info] Zdroje
> Hlavní podklad: [[dnbook.pdf]], kapitoly 5, 11-13, 18-20 a 23-25. Originální text je anglicky, poznámky jsou přeložené a zestručněné česky.

## Chyby a řád metody

Numerická metoda obvykle nepočítá přesný výsledek, ale aproximaci. Sledují se hlavně dvě složky chyby:

- chyba metody, tedy chyba z nahrazení přesného postupu konečným algoritmem,
- zaokrouhlovací chyba, která vzniká výpočtem v konečné přesnosti.

U iteračních metod se navíc sleduje stabilita a šíření chyb. Metoda je prakticky užitečná jen tehdy, když dává dostatečně přesný výsledek v rozumném čase.

Zdroj: [[dnbook.pdf#page=10|dnbook, kap. 2, str. 10]], [[dnbook.pdf#page=11|dnbook, kap. 2, str. 11]]

Metoda řádu $p$ má chybu řádově
$$
O(h^p),
$$
kde $h$ je krok dělení. Vyšší řád znamená, že při zmenšování kroku chyba mizí rychleji, ale obvykle za cenu větší složitosti nebo silnějších předpokladů na hladkost funkce.

Zdroj: [[dnbook.pdf#page=43|dnbook, definice 5a.5, str. 43]]

## Numerická kvadratura

Cílem numerické kvadratury je aproximovat určitý integrál
$$
I=\int_a^b f(x)\,dx.
$$
Interval $[a,b]$ se rozdělí ekvidistantně na body
$$
x_i=a+ih,
\qquad
h=\frac{b-a}{n}.
$$
Hodnoty $f(x_i)$ se použijí k aproximaci obsahu pod grafem.

Zdroj: [[dnbook.pdf#page=40|dnbook, kap. 5, str. 40]]

### Obdélníková pravidla

Levé obdélníkové pravidlo:
$$
R_l(n)=h\sum_{i=0}^{n-1}f(x_i).
$$
Pravé obdélníkové pravidlo:
$$
R_r(n)=h\sum_{i=1}^{n}f(x_i).
$$
Pokud $M_1=\max_{[a,b]}|f'(x)|$, pak pro obdélníková pravidla platí odhad chyby
$$
|I-R(n)|\le \frac12 (b-a)^2M_1\frac1n.
$$
Jde tedy o metodu prvního řádu.

Zdroj: [[dnbook.pdf#page=41|dnbook, definice 5a.1, str. 41]], [[dnbook.pdf#page=42|dnbook, věta 5a.3, str. 42]]

### Lichoběžníkové pravidlo

Lichoběžníkové pravidlo používá lineární aproximaci grafu na každém dílku:
$$
T(n)=\frac{h}{2}\left(f(x_0)+2\sum_{i=1}^{n-1}f(x_i)+f(x_n)\right).
$$
Pokud $M_2=\max_{[a,b]}|f''(x)|$, pak
$$
|I-T(n)|\le \frac{1}{12}(b-a)^3M_2\frac{1}{n^2}.
$$
Jde o metodu druhého řádu.

Zdroj: [[dnbook.pdf#page=46|dnbook, definice 5b.1, str. 46]], [[dnbook.pdf#page=47|dnbook, věta 5b.3, str. 47]]

### Simpsonovo pravidlo

Simpsonovo pravidlo používá parabolickou aproximaci přes dvojice dílků, proto vyžaduje sudé $n$:
$$
S(n)=\frac{h}{3}\left(f(x_0)+4\sum_{i=1}^{n/2}f(x_{2i-1})+2\sum_{i=1}^{n/2-1}f(x_{2i})+f(x_n)\right).
$$
Lokální chyba má řád $h^5$, globální chyba má řád $h^4$. Simpsonovo pravidlo je proto výrazně přesnější než obdélníky a lichoběžníky, pokud je funkce dostatečně hladká.

Zdroj: [[dnbook.pdf#page=49|dnbook, definice 5b.4 a fakt 5b.5, str. 49]], [[dnbook.pdf#page=51|dnbook, kap. 5b, str. 51]]

Související: určitý integrál a jeho význam jsou shrnuty v [[04 Primitivni funkce a integraly#Riemannův určitý integrál|MA1A - Riemannův určitý integrál]].

## Nelineární rovnice: hledání kořenů

Nelineární rovnici lze převést na tvar
$$
f(x)=0.
$$
Číslo $r$ je kořen funkce $f$, pokud $f(r)=0$. V numerice obvykle nehledáme přesný kořen, ale aproximaci $\hat r$ s chybou menší než zadaná tolerance.

Zdroj: [[dnbook.pdf#page=197|dnbook, definice 19.1, str. 197]]

Pokud je $f$ spojitá na $[a,b]$ a $f(a)$, $f(b)$ mají opačná znaménka, pak existuje kořen v $(a,b)$. Tato věta je základ pro metody, které kořen uzavírají do intervalu.

Zdroj: [[dnbook.pdf#page=198|dnbook, věta 19.2, str. 198]]

### Metoda půlení intervalu

Metoda půlení intervalu drží interval $[a_k,b_k]$, ve kterém je kořen. V každém kroku vezme střed
$$
m_k=\frac{a_k+b_k}{2}
$$
a ponechá tu polovinu, na jejíchž koncích se mění znaménko funkce. Chyba aproximace středem je nejvýše
$$
\frac12|b_k-a_k|.
$$
Metoda je spolehlivá a má kontrolu chyby, ale je pomalá; chyba se v každém kroku zmenší zhruba na polovinu.

Zdroj: [[dnbook.pdf#page=199|dnbook, algoritmus 19a.1, str. 199]], [[dnbook.pdf#page=200|dnbook, kap. 19a, str. 200]]

### Newtonova metoda

Newtonova metoda nahrazuje graf funkce tečnou v bodě $x_k$. Iterační vzorec je
$$
x_{k+1}=x_k-\frac{f(x_k)}{f'(x_k)}.
$$
Je rychlá, pro jednoduchý kořen má řád konvergence $2$, ale není obecně spolehlivá: může selhat při $f'(x_k)=0$, může oscilovat nebo utéct daleko od kořene. Funguje nejlépe, když už je počáteční odhad dostatečně blízko kořenu.

Zdroj: [[dnbook.pdf#page=204|dnbook, algoritmus 19b.1, str. 204]], [[dnbook.pdf#page=205|dnbook, vlastnosti Newtonovy metody, str. 205]], [[dnbook.pdf#page=213|dnbook, věta 19d.6, str. 213]]

### Metoda sečen

Metoda sečen nahrazuje derivaci v Newtonově metodě diferenčním podílem ze dvou posledních bodů:
$$
x_{k+1}=\frac{x_{k-1}f(x_k)-x_kf(x_{k-1})}{f(x_k)-f(x_{k-1})}.
$$
Potřebuje dva počáteční odhady a nevyžaduje derivaci. Je méně spolehlivá než půlení, ale často rychlejší; její řád konvergence je
$$
\varphi=\frac{1+\sqrt{5}}{2}.
$$

Zdroj: [[dnbook.pdf#page=214|dnbook, algoritmus 19e.1, str. 214]], [[dnbook.pdf#page=215|dnbook, vlastnosti metody sečen, str. 215]]

### Pevný bod

Rovnici lze také přepsat na tvar
$$
\varphi(x)=x.
$$
Řešení se pak hledá iterací
$$
x_{k+1}=\varphi(x_k).
$$
Pokud je $\varphi$ kontrakce na uzavřeném intervalu $I$ a $\varphi[I]\subset I$, pak má právě jeden pevný bod a iterace k němu konverguje pro libovolné $x_0\in I$.

Zdroj: [[dnbook.pdf#page=219|dnbook, definice 20.1, str. 219]], [[dnbook.pdf#page=221|dnbook, algoritmus 20a.1, str. 221]], [[dnbook.pdf#page=225|dnbook, Banachova věta, str. 225]]

Relaxace používá vážený kompromis mezi původní iterací a identitou:
$$
\varphi_\lambda(x)=\lambda\varphi(x)+(1-\lambda)x.
$$
Správná volba $\lambda$ může zrychlit konvergenci nebo zachránit iteraci, která bez relaxace diverguje.

Zdroj: [[dnbook.pdf#page=229|dnbook, kap. 20b, str. 229]]

## Numerické řešení diferenciálních rovnic

U počáteční úlohy
$$
y'=f(x,y),
\qquad
 y(x_0)=y_0
$$
se zvolí krok
$$
h=\frac{T}{n},
\qquad
x_i=x_0+ih,
$$
a hledají se aproximace $y_i\approx y(x_i)$.

Zdroj: [[dnbook.pdf#page=118|dnbook, kap. 11, str. 118]]

### Eulerova metoda

Eulerova metoda použije tečnu v aktuálním bodě:
$$
y_{i+1}=y_i+h f(x_i,y_i).
$$
Je explicitní, jednoduchá a názorná, ale má nízkou přesnost. Lokální chyba je řádu $h^2$ a globální chyba řádu $h$, takže jde o metodu prvního řádu.

Zdroj: [[dnbook.pdf#page=119|dnbook, Eulerova metoda, str. 119]], [[dnbook.pdf#page=124|dnbook, chyba Eulerovy metody, str. 124]]

### Základní metody pro ODE

Obecná jednokroková metoda má tvar
$$
y_{i+1}=y_i+h\Phi_f(x_i,y_i,h),
$$
kde $\Phi_f$ odhaduje vhodný sklon na kroku. Eulerova metoda používá jen sklon na začátku intervalu. Přesnější metody se snaží získat lepší odhad sklonu uvnitř kroku nebo průměr sklonů.

Zdroj: [[dnbook.pdf#page=128|dnbook, kap. 12, str. 128]]

Rungeovy-Kuttovy metody používají několik vyhodnocení pravé strany $f$ v rámci jednoho kroku. Klasické metody vyššího řádu jsou prakticky důležité, protože dávají lepší přesnost při rozumné velikosti kroku.

Zdroj: [[dnbook.pdf#page=130|dnbook, kap. 12, str. 130]]

Taylorova metoda používá Taylorův polynom řešení. Pro rovnici $y'=f(x,y)$ se derivace vyšších řádů získávají opakovaným derivováním vztahu $y'=f(x,y(x))$. Taylorova metoda s polynomem stupně $p$ je metodou řádu $p$.

Zdroj: [[dnbook.pdf#page=133|dnbook, kap. 13a, str. 133]], [[dnbook.pdf#page=136|dnbook, věta 13a.2, str. 136]]

Vícekrokové metody používají více předchozích hodnot. Typicky se derivace nahradí diferenční formulí, například centrální diferencí, takže nový bod závisí na více bodech z minulosti.

Zdroj: [[dnbook.pdf#page=138|dnbook, kap. 13c, str. 138]]

U rovnic vyššího řádu se často nepoužívá přímo tečnový postup. Standardní trik je převést rovnici vyššího řádu na soustavu prvního řádu a použít metody pro soustavy. Tento převod je stejný jako v [[05 Linearni diferencialni rovnice a soustavy#Převod rovnice vyššího řádu na soustavu|otázce 5]].

Zdroj: [[dnbook.pdf#page=194|dnbook, kap. 18, str. 194]], [[dnbook.pdf#page=270|dnbook, algoritmus 26.4, str. 270]]

## Soustavy lineárních rovnic: přímé metody

Soustavu lineárních rovnic zapisujeme jako
$$
A\mathbf{x}=\mathbf{b}.
$$
Přímé metody se snaží v konečném počtu kroků převést soustavu na jednodušší tvar.

Zdroj: [[dnbook.pdf#page=236|dnbook, kap. 23, str. 236]]

Gaussova eliminace používá řádkové úpravy k převodu matice na horní trojúhelníkový tvar. Poté se použije zpětná substituce. Prakticky je důležité pivotování: jako pivot se vybírá vhodný nenulový a pokud možno velký prvek, aby se omezilo dělení malými čísly a růst zaokrouhlovacích chyb.

Zdroj: [[dnbook.pdf#page=237|dnbook, kap. 23a, str. 237]], [[dnbook.pdf#page=258|dnbook, kap. 24d, str. 258]]

LUP faktorizace rozkládá matici s případným přehazováním řádků na součin
$$
PA=LU,
$$
kde $P$ je permutační matice, $L$ dolní trojúhelníková matice a $U$ horní trojúhelníková matice. Výhoda je, že pro stejnou matici $A$ a různé pravé strany lze faktorizaci použít opakovaně.

Zdroj: [[dnbook.pdf#page=241|dnbook, kap. 23b, str. 241]]

## Podmíněnost a stabilita maticových výpočtů

Podmíněnost popisuje citlivost výsledku na změny vstupu. U soustav lineárních rovnic hraje roli číslo podmíněnosti
$$
\operatorname{cond}(A)=\|A\|\,\|A^{-1}\|.
$$
Velké číslo podmíněnosti znamená, že i malá chyba ve vstupu nebo zaokrouhlení může způsobit velkou chybu v řešení.

Zdroj: [[dnbook.pdf#page=250|dnbook, kap. 24, str. 250]]

Pivotování při eliminaci zlepšuje numerickou stabilitu. Bez pivotování může malý pivot výrazně zvětšit chyby nebo vést k úplně špatnému výsledku ve výpočtu s konečnou přesností.

Zdroj: [[dnbook.pdf#page=258|dnbook, příklad 24d.a, str. 258]]

## Soustavy lineárních rovnic: iterační metody

Iterační metody převádějí soustavu na tvar
$$
\mathbf{x}_{k+1}=B\mathbf{x}_k+\mathbf{c}.
$$
Taková iterace konverguje právě tehdy, když spektrální poloměr matice $B$ splňuje
$$
\rho(B)<1.
$$
Praktičtější postačující podmínka je $\|B\|<1$ pro nějakou kompatibilní maticovou normu.

Zdroj: [[dnbook.pdf#page=260|dnbook, věta 25a.1 a 25a.3, str. 260]]

Jacobiho metoda rozdělí matici
$$
A=D+L+U,
$$
kde $D$ je diagonála, $L$ dolní část a $U$ horní část. Iterace má tvar
$$
\mathbf{x}_{k+1}=D^{-1}\mathbf{b}-D^{-1}(L+U)\mathbf{x}_k.
$$
Souřadnicově se každá nová složka počítá ze starých hodnot ostatních složek.

Zdroj: [[dnbook.pdf#page=261|dnbook, algoritmus 25b.1, str. 261]]

Gaussova-Seidelova metoda používá v rámci jednoho kroku už nově spočítané složky:
$$
\mathbf{x}_{k+1}=-(D+L)^{-1}U\mathbf{x}_k+(D+L)^{-1}\mathbf{b}.
$$
Často konverguje rychleji než Jacobiho metoda, ale je citlivější na pořadí rovnic.

Zdroj: [[dnbook.pdf#page=262|dnbook, algoritmus 25b.2, str. 262]]

Pokud je matice $A$ ostře diagonálně dominantní, konvergují Jacobiho i Gaussova-Seidelova metoda. Pokud je $A$ symetrická a pozitivně definitní, konverguje Gaussova-Seidelova metoda.

Zdroj: [[dnbook.pdf#page=263|dnbook, definice 25b.3 a věta 25b.4, str. 263]]

SOR metoda zavádí relaxační parametr $\lambda$ a upravuje Gaussovu-Seidelovu metodu. Pro $\lambda=1$ dostaneme Gaussovu-Seidelovu metodu. Vhodné $\lambda$ může urychlit konvergenci; obvykle se hledá experimentálně.

Zdroj: [[dnbook.pdf#page=264|dnbook, algoritmus 25b.5, str. 264]], [[dnbook.pdf#page=265|dnbook, věta 25b.6, str. 265]]

## Kdy použít přímé a kdy iterační metody

Gaussova eliminace je univerzální a vhodná pro menší a střední soustavy. Iterační metody jsou výhodné pro velmi velké řídké matice, kde jeden krok stojí málo operací a počet kroků je výrazně menší než rozměr soustavy. Pokud je matice špatně podmíněná, je potřeba být opatrný i u přímých metod.

Zdroj: [[dnbook.pdf#page=264|dnbook, srovnání iterací a eliminace, str. 264]], [[dnbook.pdf#page=265|dnbook, doporučení pro iterace, str. 265]]

## Minimum ke zkoušce

Je potřeba umět vysvětlit rozdíl mezi spolehlivostí a rychlostí metody. Půlení intervalu je pomalé, ale kontroluje chybu; Newtonova metoda je rychlá, ale může selhat; metoda sečen nepotřebuje derivaci. U kvadratury znát obdélníky, lichoběžníky a Simpsonovo pravidlo. U lineárních soustav znát Gaussovu eliminaci, pivotování, podmíněnost, Jacobiho a Gaussovu-Seidelovu iteraci. U ODE znát Eulerovu metodu, obecnou jednokrokovou ideu a důvod převodu vyššího řádu na soustavu prvního řádu.

Zdroj: souhrn podle [[dnbook.pdf#page=40|dnbook, kap. 5]], [[dnbook.pdf#page=118|dnbook, kap. 11]], [[dnbook.pdf#page=197|dnbook, kap. 19]], [[dnbook.pdf#page=236|dnbook, kap. 23]], [[dnbook.pdf#page=260|dnbook, kap. 25]]
