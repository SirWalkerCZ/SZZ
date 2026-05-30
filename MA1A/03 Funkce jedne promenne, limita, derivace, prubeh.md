---
aliases:
  - MA1A 03
  - Funkce jedné proměnné, limita, derivace a průběh funkce
predmet: MA1A
okruh: 3
---

# Funkce jedné proměnné, limita, derivace, průběh funkce

> [!info] Zdroje
> Hlavní podklady: [[ma1a-23k2.pdf]], [[ma1a-23k3.pdf]], [[ma1a-23k4.pdf]], [[ma1a-23k6.pdf]]. Taylorův polynom je doplněn podle [[hex_compost.pdf#page=22|hex_compost, MA1A - 1, str. 6]], protože v dodané složce MA1A není kapitola 5.

## Funkce jedné proměnné

Reálná funkce reálné proměnné je zobrazení
$$
f:A\to \mathbb{R}, \qquad A\subset \mathbb{R}.
$$
Množina $A$ je definiční obor $D(f)$, hodnota funkce v bodě $x$ je $f(x)$ a obor hodnot je
$$
H(f)=\{f(x)\mid x\in D(f)\}.
$$
Graf funkce je množina bodů
$$
\{(x,f(x))\mid x\in D(f)\}.
$$
Pokud není definiční obor zadán, bere se maximální množina, na které má předpis smysl.

Zdroj: [[ma1a-23k2.pdf#page=1|MA1A k2, P2.1]]

S funkcemi se pracuje bodově. Pro součet, rozdíl a součin se bere průnik definičních oborů; u podílu se navíc vyřadí body, kde je jmenovatel nulový. Složená funkce $h=g\circ f$ je dána předpisem
$$
h(x)=g(f(x)),
$$
a je potřeba, aby hodnoty vnitřní funkce ležely v definičním oboru vnější funkce.

Zdroj: [[ma1a-23k2.pdf#page=2|MA1A k2, P2.2]]

Důležité vlastnosti funkce:

- Funkce je prostá, pokud různým vzorům odpovídají různé obrazy. Pak má inverzní funkci $f^{-1}$ na $H(f)$, kde
$$
f^{-1}(x)=y \iff f(y)=x.
$$
- Funkce je omezená na množině $A$, pokud existuje $S\in\mathbb{R}$ tak, že $|f(x)|\le S$ pro všechna $x\in A$.
- Monotonie se vyjadřuje porovnáním hodnot pro $x_1<x_2$: neklesající, nerostoucí, rostoucí, klesající. Ryze monotónní funkce je prostá.
- Funkce je sudá, pokud $f(-x)=f(x)$, lichá, pokud $f(-x)=-f(x)$.
- Funkce je periodická s periodou $T>0$, pokud $f(x+T)=f(x)$ tam, kde jsou obě hodnoty definovány.

Zdroj: [[ma1a-23k2.pdf#page=3|MA1A k2, P2.3]], [[ma1a-23k2.pdf#page=4|MA1A k2, P2.4]]

Související: [[04 Primitivni funkce a integraly#Primitivní funkce a neurčitý integrál|primitivní funkce]] pracuje opačně k derivaci.

## Limita funkce

Limita popisuje chování funkce v okolí bodu, nikoli nutně přímo v bodě. Zápis
$$
\lim_{x\to x_0} f(x)=a
$$
znamená, že hodnoty $f(x)$ se pro $x$ dostatečně blízká $x_0$, ale $x\ne x_0$, dostávají libovolně blízko k $a$.

Zdroj: [[ma1a-23k3.pdf#page=1|MA1A k3, P3.1]]

Limita může být vlastní nebo nevlastní a bod, ke kterému $x$ míří, může být vlastní bod nebo nekonečno. Jednostranné limity se značí
$$
\lim_{x\to x_0+} f(x), \qquad \lim_{x\to x_0-} f(x).
$$
Oboustranná limita existuje právě tehdy, když existují obě jednostranné limity a jsou si rovny.

Zdroj: [[ma1a-23k3.pdf#page=2|MA1A k3, P3.2]]

Heineho věta převádí limitu funkce na limitu posloupností. Platí
$$
\lim_{x\to x_0} f(x)=a
$$
právě tehdy, když pro každou posloupnost $(y_n)$ z $D(f)\setminus\{x_0\}$ s $y_n\to x_0$ platí $f(y_n)\to a$. Pro vyvrácení existence limity stačí najít dvě posloupnosti jdoucí ke stejnému bodu, na kterých vyjdou různé limity hodnot funkce.

Zdroj: [[ma1a-23k3.pdf#page=2|MA1A k3, P3.2]]

Základní vlastnosti limit:

- limita je jednoznačná,
- vlastní limita zachovává znaménko v prstencovém okolí,
- funkce s vlastní limitou je v okolí bodu omezená,
- limity se sčítají, násobí a dělí podle běžných pravidel, pokud mají výrazy smysl,
- limita složené funkce vyžaduje kontrolu vnitřní limity a spojitosti nebo vynechání problematické hodnoty.

Zdroj: [[ma1a-23k3.pdf#page=4|MA1A k3, P3.4]], [[ma1a-23k3.pdf#page=5|MA1A k3, P3.5]]

Typické důležité limity:
$$
\lim_{x\to 0}\frac{\sin x}{x}=1,
\qquad
\lim_{x\to 0}\frac{e^x-1}{x}=1,
\qquad
\lim_{x\to 0}\frac{\ln(1+x)}{x}=1,
$$
$$
\lim_{x\to \infty}\left(1+\frac{1}{x}\right)^x=e.
$$

Zdroj: [[ma1a-23k3.pdf#page=7|MA1A k3, P3.7]]

## Spojitost

Funkce je spojitá v bodě $x_0\in D(f)$, pokud hodnoty funkce v okolí $x_0$ zůstávají libovolně blízko hodnotě $f(x_0)$. Pokud je funkce definovaná v okolí bodu, je to ekvivalentní podmínce
$$
\lim_{x\to x_0} f(x)=f(x_0).
$$
Na intervalu se požaduje spojitost ve vnitřních bodech a odpovídající jednostranná spojitost v krajních bodech.

Zdroj: [[ma1a-23k3.pdf#page=3|MA1A k3, P3.3]]

Elementární funkce jsou spojité na svých definičních oborech. Součet, součin, podíl se nenulovým jmenovatelem a složení spojitých funkcí jsou opět spojité.

Zdroj: [[ma1a-23k3.pdf#page=6|MA1A k3, P3.6]]

## Derivace a její význam

Derivace funkce $f$ v bodě $x_0$ je limita diferenčního podílu
$$
f'(x_0)=\lim_{x\to x_0}\frac{f(x)-f(x_0)}{x-x_0}
=\lim_{h\to 0}\frac{f(x_0+h)-f(x_0)}{h},
$$
pokud tato limita existuje jako vlastní číslo. Lze definovat i jednostranné derivace a nevlastní derivaci.

Zdroj: [[ma1a-23k4.pdf#page=1|MA1A k4, P4.1]]

Geometricky je derivace směrnice tečny ke grafu. Pokud $f'(x_0)\in\mathbb{R}$, rovnice tečny je
$$
y=f(x_0)+f'(x_0)(x-x_0).
$$
Pro $f'(x_0)\ne 0$ má normála rovnici
$$
y=f(x_0)-\frac{1}{f'(x_0)}(x-x_0).
$$
Je-li $f'(x_0)=0$, tečna je vodorovná a normála svislá; při nevlastní derivaci je tečna svislá.

Zdroj: [[ma1a-23k4.pdf#page=1|MA1A k4, P4.1]]

Pokud má funkce v bodě vlastní derivaci, je v tomto bodě spojitá. Obrácení obecně neplatí: spojitá funkce nemusí mít derivaci.

Zdroj: [[ma1a-23k4.pdf#page=2|MA1A k4, P4.2]]

Pravidla derivování:
$$
(f\pm g)'=f'\pm g',
$$
$$
(fg)'=f'g+fg',
$$
$$
\left(\frac{f}{g}\right)'=\frac{f'g-fg'}{g^2}, \qquad g(x_0)\ne 0,
$$
$$
(g\circ f)'(x_0)=g'(f(x_0))f'(x_0).
$$
Pro inverzní funkci platí při splnění předpokladů spojitosti, prostoty a $f'(x_0)\ne 0$
$$
(f^{-1})'(y_0)=\frac{1}{f'(x_0)}, \qquad y_0=f(x_0).
$$

Zdroj: [[ma1a-23k4.pdf#page=2|MA1A k4, P4.2]], [[ma1a-23k4.pdf#page=3|MA1A k4, P4.3]]

Vyšší derivace se definují induktivně:
$$
f^{(0)}=f, \qquad f^{(n)}=(f^{(n-1)})'.
$$
Pro součin platí Leibnizův vzorec
$$
(fg)^{(n)}=\sum_{k=0}^{n}\binom{n}{k}f^{(k)}g^{(n-k)}.
$$

Zdroj: [[ma1a-23k4.pdf#page=6|MA1A k4, P4.6]]

## Průběh funkce a lokální extrémy

Funkce nabývá globálního maxima na množině $M$ v bodě $x_0$, pokud $x_0\in M$ a pro všechna $x\in M$ platí
$$
f(x)\le f(x_0).
$$
Analogicky se definuje globální minimum. Lokální maximum nebo minimum se definuje stejně, ale jen v nějakém okolí bodu $x_0$.

Zdroj: [[ma1a-23k6.pdf#page=1|MA1A k6, P6.1]]

Nutná podmínka lokálního extrému: pokud má $f$ v bodě $x_0$ lokální extrém a existuje $f'(x_0)$, pak
$$
f'(x_0)=0.
$$
Bod s nulovou derivací se nazývá stacionární bod. Nulová derivace ale sama o sobě extrém nezaručuje.

Zdroj: [[ma1a-23k6.pdf#page=1|MA1A k6, P6.1]]

Derivace určuje monotonií:

- pokud $f'(x_0)>0$, funkce v bodě roste,
- pokud $f'(x_0)<0$, funkce v bodě klesá,
- na intervalu spojitosti platí: $f'\ge 0$ odpovídá neklesání a $f'\le 0$ odpovídá nerostoucí funkci.

Lokální extrém se často ověří změnou znaménka derivace. Pokud $f'$ změní znaménko z $+$ na $-$, jde o lokální maximum; pokud z $-$ na $+$, jde o lokální minimum.

Zdroj: [[ma1a-23k6.pdf#page=2|MA1A k6, P6.2]]

Test druhou derivací: pokud
$$
f'(x_0)=0
$$
a zároveň $f''(x_0)>0$, má funkce v $x_0$ lokální minimum. Pokud $f''(x_0)<0$, má lokální maximum.

Zdroj: [[ma1a-23k6.pdf#page=2|MA1A k6, P6.2]]

Pro konvexitu a konkavitu se používá druhá derivace. Je-li na intervalu $f''>0$, funkce je ryze konvexní; je-li $f''<0$, je ryze konkávní. Inflexní bod je bod, kde se mění konvexita. Pokud v inflexním bodě existuje druhá derivace, platí
$$
f''(x_0)=0.
$$
Jestliže $f''(x_0)=0$ a druhá derivace v bodě mění znaménko, jde o inflexi.

Zdroj: [[ma1a-23k6.pdf#page=3|MA1A k6, P6.3]]

Asymptoty:

- svislá asymptota v bodě $x_0$ existuje, pokud alespoň jedna jednostranná limita v $x_0$ je nevlastní; rovnice je $x=x_0$,
- asymptota v nekonečnu má tvar $y=kx+q$ a platí
$$
\lim_{x\to \pm\infty}\bigl(f(x)-(kx+q)\bigr)=0.
$$
Koeficienty se hledají pomocí
$$
k=\lim_{x\to\pm\infty}\frac{f(x)}{x},
\qquad
q=\lim_{x\to\pm\infty}(f(x)-kx).
$$

Zdroj: [[ma1a-23k6.pdf#page=4|MA1A k6, P6.4]]

Při vyšetřování průběhu funkce se obvykle postupuje takto: definiční obor, průsečíky s osami a znaménko, sudost/lichost/periodicita, limity a spojitost, monotonie a extrémy, konvexita a inflexe, asymptoty.

Zdroj: [[ma1a-23k6.pdf#page=5|MA1A k6, P6.5]]

## Aproximace Taylorovým polynomem

Taylorův polynom stupně $n$ v bodě $x_0$ je
$$
T_n(x)=\sum_{k=0}^{n}\frac{f^{(k)}(x_0)}{k!}(x-x_0)^k.
$$
První dva stupně jsou
$$
T_1(x)=f(x_0)+f'(x_0)(x-x_0),
$$
$$
T_2(x)=f(x_0)+f'(x_0)(x-x_0)+\frac{f''(x_0)}{2}(x-x_0)^2.
$$
Používá se k aproximaci funkce v okolí bodu $x_0$. Pro státnice stačí umět vysvětlit, že čím vyšší derivace v bodě použijeme, tím více se polynom v okolí bodu shoduje s lokálním chováním funkce.

Zdroj: [[hex_compost.pdf#page=22|hex_compost, MA1A - 1, str. 6]]

## Minimum ke zkoušce

Je potřeba bezpečně odlišit limitu, spojitost a derivaci. Limita popisuje okolní chování, spojitost přidává rovnost s hodnotou v bodě a derivace měří lokální změnu funkce. Pro průběh funkce jsou hlavní nástroje znaménka $f'$ a $f''$, lokální extrémy, inflexe a asymptoty.

Zdroj: souhrn podle [[ma1a-23k3.pdf]], [[ma1a-23k4.pdf]], [[ma1a-23k6.pdf]]
