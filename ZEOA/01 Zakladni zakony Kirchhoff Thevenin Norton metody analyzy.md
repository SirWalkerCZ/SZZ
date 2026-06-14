# 01 Základní zákony, Kirchhoffovy zákony, Thévenin, Norton, metody analýzy

> Hlavní podklad: SZZ___ZEOA.pdf (ek-drive). Znění okruhu: [[SZZ - Odborné okruhy|odborný okruh 1]].
> **Komise se ptá:** vyřešit jednoduchý obvod (zdroj napětí, zdroj proudu, dva rezistory) vybranou metodou — Pokorný i Pollák. Thévenin/Norton, MUN, MSP — Pollák.

## Kirchhoffovy zákony

**1. Kirchhoffův zákon (proudový, KZ1):** součet proudů vtékajících do uzlu se rovná součtu proudů vytékajících. Plyne ze zákona zachování náboje:

$$
\sum_k i_k = 0 \quad \text{(v uzlu)}.
$$

**2. Kirchhoffův zákon (napěťový, KZ2):** součet napětí podél uzavřené smyčky je nulový. Plyne ze zákona zachování energie:

$$
\sum_k u_k = 0 \quad \text{(ve smyčce)}.
$$

Pro obvod s $n$ uzly a $v$ větvemi lze napsat $n-1$ nezávislých proudových rovnic a $v-(n-1)$ nezávislých napěťových rovnic.

## Elementární metody

- **Zjednodušování obvodu** — postupné slučování sériových ($R = R_1 + R_2$) a paralelních ($R = \frac{R_1 R_2}{R_1+R_2}$) rezistorů, přepočet děličů.
- **Dělič napětí:** $U_2 = U \dfrac{R_2}{R_1+R_2}$ (nezatížený!). **Dělič proudu:** $I_1 = I \dfrac{R_2}{R_1+R_2}$ (proud teče víc menším odporem).
- **Metoda úměrných veličin** — u žebříkového obvodu zvolím výstupní veličinu rovnou 1, dopočítám zpět vstup a výsledek přeškáluji.
- **Princip superpozice** — v lineárním obvodu je odezva na více zdrojů součtem odezev na jednotlivé zdroje působící samostatně. Při vyřazení zdroje: **zdroj napětí → zkrat, zdroj proudu → rozpojení.**
- **Transfigurace** hvězda–trojúhelník, pokud nelze slučovat sériově/paralelně.

## Théveninův a Nortonův teorém

Libovolný lineární dvojpól lze vůči svorkám nahradit:

- **Thévenin:** zdroj napětí $U_i$ v sérii s odporem $R_i$,
- **Norton:** zdroj proudu $I_i$ paralelně s odporem $R_i$.

Postup:

1. $U_i$ = napětí **naprázdno** na svorkách (odpojená zátěž),
2. $I_i$ = proud **nakrátko** (zkratované svorky),
3. $R_i$ = odpor ze svorek při **vyřazených zdrojích** (U-zdroje zkrat, I-zdroje rozpojení).

Vzájemný převod:

$$
U_i = R_i I_i,
\qquad
R_i = \frac{U_i}{I_i}.
$$

## Metoda uzlových napětí (MUN)

Nejpoužívanější obecná metoda. Neznámé jsou napětí uzlů proti zvolenému referenčnímu uzlu (zem). Pro každý uzel kromě reference se píše KZ1, proudy větvemi se vyjádří pomocí uzlových napětí a vodivostí:

$$
\sum_k G_k (U_\text{uzel} - U_\text{soused,k}) = \sum I_\text{zdrojové do uzlu}.
$$

Počet rovnic: $n-1$. Ideální zdroj napětí mezi uzly se řeší tzv. supernodem nebo přepočtem na Nortonův ekvivalent.

## Metoda smyčkových proudů (MSP)

Duální k MUN. Neznámé jsou fiktivní smyčkové proudy v nezávislých smyčkách, pro každou smyčku se píše KZ2:

$$
\sum_k R_k (I_\text{smyčka} - I_\text{sousední smyčka,k}) = \sum U_\text{zdrojové ve smyčce}.
$$

Počet rovnic: $v-(n-1)$. Ideální zdroj proudu ve větvi rovnou určuje smyčkový proud (nebo se použije supersmyčka).

**Volba metody:** méně uzlů → MUN, méně smyček → MSP. U obvodu se zdrojem proudu je MUN obvykle přímočařejší (zdrojový proud jde rovnou do pravé strany).

## Řešený příklad: U-zdroj, I-zdroj, dva rezistory

Zadání: $U = 10\ \mathrm V$, $I = 1\ \mathrm A$, $R_1 = 2\ \Omega$, $R_2 = 3\ \Omega$. Určete napětí $U_A$ na $R_2$ a proudy rezistory.

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=1cm]
    % zem
    \draw[thick] (0,0) -- (8,0);
    \foreach \x in {0.6,4,7.4} \draw (\x-0.25,-0.08) -- (\x+0.25,-0.08);
    % zdroj napeti U
    \draw[thick] (0.6,0) -- (0.6,1) ;
    \draw[thick] (0.6,1) circle (0.45);
    \node at (0.6,1) {$U$};
    \draw[thick] (0.6,1.45) -- (0.6,2.5) -- (2,2.5);
    % R1
    \draw[thick] (2,2.2) rectangle (3.4,2.8);
    \node at (2.7,2.5) {$R_1$};
    \draw[thick] (3.4,2.5) -- (5.6,2.5);
    % uzel A
    \fill (4,2.5) circle (2pt);
    \node[above] at (4,2.65) {A};
    % R2
    \draw[thick] (4,2.5) -- (4,1.9);
    \draw[thick] (3.7,0.7) rectangle (4.3,1.9);
    \node at (4,1.3) {$R_2$};
    \draw[thick] (4,0.7) -- (4,0);
    % zdroj proudu I
    \draw[thick] (5.6,2.5) -- (7.4,2.5) -- (7.4,1.45);
    \draw[thick] (7.4,1) circle (0.45);
    \draw[->,thick] (7.4,0.75) -- (7.4,1.25);
    \node[right] at (7.9,1) {$I$};
    \draw[thick] (7.4,0.55) -- (7.4,0);
  \end{tikzpicture}
\end{document}
```

### a) MUN (jediný uzel A)

$$
\frac{U_A - U}{R_1} + \frac{U_A}{R_2} - I = 0
\;\Rightarrow\;
U_A = \frac{\dfrac{U}{R_1} + I}{\dfrac{1}{R_1}+\dfrac{1}{R_2}}
= \frac{U R_2 + I R_1 R_2}{R_1 + R_2}
= \frac{10\cdot 3 + 1\cdot 6}{5} = 7{,}2\ \mathrm V.
$$

### b) Superpozice

Jen $U$ ($I$ rozpojen — dělič): $U_A' = U\frac{R_2}{R_1+R_2} = 6\ \mathrm V$.
Jen $I$ ($U$ zkrat — proud do $R_1 \parallel R_2$): $U_A'' = I\frac{R_1R_2}{R_1+R_2} = 1{,}2\ \mathrm V$.
Součet: $U_A = 6 + 1{,}2 = 7{,}2\ \mathrm V$. ✓

### c) Thévenin vůči svorkám $R_2$

Naprázdno ($R_2$ odpojen, $I$ teče přes $R_1$ proti zdroji): $U_i = U + I R_1 = 12\ \mathrm V$.
Vyřazené zdroje: $R_i = R_1 = 2\ \Omega$.
Se zátěží: $U_A = U_i\frac{R_2}{R_i + R_2} = 12\cdot\frac{3}{5} = 7{,}2\ \mathrm V.$ ✓ (Norton: $I_i = U_i/R_i = 6\ \mathrm A$.)

### Kontrola proudů (KZ1 v uzlu A)

$$
I_{R_1} = \frac{U - U_A}{R_1} = 1{,}4\ \mathrm A,
\qquad
I_{R_2} = \frac{U_A}{R_2} = 2{,}4\ \mathrm A,
\qquad
1{,}4 + 1 = 2{,}4. ✓
$$

## Co umět u zkoušky

- Vyslovit oba Kirchhoffovy zákony a říct, z čeho plynou.
- Vyřešit obvod se dvěma zdroji a dvěma rezistory **třemi způsoby** (MUN, superpozice, Thévenin) a zkontrolovat KZ1.
- Postup určení $U_i$, $I_i$, $R_i$ (naprázdno / nakrátko / vyřazené zdroje) a převod Thévenin ↔ Norton.
- Jak se vyřazují zdroje (U → zkrat, I → rozpojení) a kdy zvolit MUN vs. MSP.
- Pozor na nezatížený vs. zatížený dělič napětí.
