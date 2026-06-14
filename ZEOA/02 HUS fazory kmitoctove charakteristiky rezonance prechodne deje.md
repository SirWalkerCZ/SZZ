# 02 Harmonický ustálený stav, fázory, kmitočtové charakteristiky, rezonance, přechodné děje

> Hlavní podklad: SZZ___ZEOA.pdf (ek-drive). Znění okruhu: [[SZZ - Odborné okruhy|odborný okruh 2]].
> **Komise se ptá:** kmitočtové charakteristiky — význam, jak se počítají, kraje přenosové funkce limitami (Pokorný/Pollák); přechodové děje 1. řádu; přenos dvojbranu (Pollák).

## Harmonický ustálený stav a fázory

V harmonickém ustáleném stavu (HUS) mají všechna napětí a proudy stejný kmitočet, liší se jen amplitudou a fází. Harmonický průběh $u(t)=U_m\cos(\omega t+\varphi)$ se reprezentuje **fázorem** — komplexním číslem

$$
\hat U = U_m e^{j\varphi}
$$

(případně v efektivní hodnotě $U_m/\sqrt2$). Derivace v čase přejde na násobení $j\omega$, takže diferenciální rovnice obvodu přecházejí na algebraické rovnice s komplexními čísly.

Impedance prvků:

$$
Z_R = R,
\qquad
Z_L = j\omega L,
\qquad
Z_C = \frac{1}{j\omega C}.
$$

Cívka: napětí předbíhá proud o 90°. Kondenzátor: proud předbíhá napětí o 90°.

## Přenosová funkce a kmitočtové charakteristiky

Přenos napětí je poměr fázorů výstupu a vstupu:

$$
\hat K(j\omega) = \frac{\hat U_2}{\hat U_1}
= |\hat K(\omega)|\,e^{j\varphi(\omega)}.
$$

- **Modulová (amplitudová) charakteristika** $|\hat K(\omega)|$ — kolikrát se signál zesílí/zeslabí; obvykle v dB: $K_{dB}=20\log|\hat K|$.
- **Fázová charakteristika** $\varphi(\omega)$ — o kolik se posune fáze.

### Kraje přenosové funkce limitními hodnotami

Klíčový trik, na který se komise ptá: chování na krajích pásma se určí **bez počítání**, náhradou reaktančních prvků v limitě:

| Prvek | $\omega \to 0$ | $\omega \to \infty$ |
|---|---|---|
| kondenzátor $C$ | rozpojení | zkrat |
| cívka $L$ | zkrat | rozpojení |

Z překresleného obvodu se kraje přenosu rovnou vidí (0, 1, nebo dělič odporů).

### Příklad: RC dolní propust

Sériový $R$, výstup na $C$:

$$
\hat K(j\omega) = \frac{\frac{1}{j\omega C}}{R+\frac{1}{j\omega C}}
= \frac{1}{1+j\omega RC}.
$$

- $\omega\to0$: $C$ rozpojen → $\hat K \to 1$ (0 dB), fáze 0°.
- $\omega\to\infty$: $C$ zkrat → $\hat K \to 0$, pokles −20 dB/dekádu, fáze → −90°.
- **Zlomový kmitočet** $\omega_0 = 1/RC$: $|\hat K| = 1/\sqrt2$ (−3 dB), fáze −45°.

Bodeho aproximace: do $\omega_0$ vodorovná asymptota 0 dB, od $\omega_0$ přímka −20 dB/dek.

```tikz
\begin{document}
  \begin{tikzpicture}[x=1.1cm,y=0.9cm]
    \draw[->] (0,0) -- (6.2,0) node[right] {$\log\omega$};
    \draw[->] (0,-2.6) -- (0,1) node[above] {$K$ [dB]};
    \draw[thick,blue] (0,0) -- (3,0) -- (5.6,-2.4);
    \draw[dashed] (3,0.6) -- (3,-2.4);
    \node[below] at (3,-2.4) {$\omega_0=\frac{1}{RC}$};
    \fill[red] (3,-0.3) circle (1.6pt);
    \node[red,right] at (3.1,-0.45) {$-3$ dB};
    \node[blue] at (4.9,-1.2) {$-20$ dB/dek};
  \end{tikzpicture}
\end{document}
```

CR horní propust ($\hat K = \frac{j\omega RC}{1+j\omega RC}$) zrcadlově: na nule 0, na nekonečnu 1, fáze od +90° k 0°.

## Rezonance

Sériový RLC: impedance $Z = R + j(\omega L - \frac{1}{\omega C})$ je čistě reálná (minimální) při **rezonančním kmitočtu**

$$
\omega_0 = \frac{1}{\sqrt{LC}}.
$$

Proud je v rezonanci maximální. Činitel jakosti a šířka pásma:

$$
Q = \frac{\omega_0 L}{R} = \frac{1}{R}\sqrt{\frac{L}{C}},
\qquad
B = \frac{\omega_0}{Q}.
$$

Na $L$ a $C$ může být v rezonanci napětí $Q$-krát větší než na zdroji. Paralelní RLC duálně: impedance maximální, proud ze zdroje minimální.

## Přechodné děje 1. řádu

Po přepnutí spínače přechází obvod s jedním akumulačním prvkem do nového ustáleného stavu exponenciálně:

$$
x(t) = x(\infty) + \big(x(0^+) - x(\infty)\big)\,e^{-t/\tau},
\qquad
\tau_{RC} = RC,\quad \tau_{RL} = \frac{L}{R}.
$$

Postup (stačí tři čísla):

1. $x(0^+)$ — **napětí na kondenzátoru a proud cívkou se nemění skokem**: $u_C(0^+)=u_C(0^-)$, $i_L(0^+)=i_L(0^-)$.
2. $x(\infty)$ — nový stejnosměrný ustálený stav: kondenzátor = rozpojení, cívka = zkrat.
3. $\tau$ — odpor počítaný ze svorek akumulačního prvku při vyřazených zdrojích (Théveninův odpor).

Příklad — nabíjení $C$ přes $R$ ze zdroje $U$: $u_C(0^+)=0$, $u_C(\infty)=U$, $\tau=RC$:

$$
u_C(t) = U\big(1-e^{-t/\tau}\big),
\qquad
i(t) = \frac{U}{R}e^{-t/\tau}.
$$

Za $t=\tau$ je dosaženo ~63 %, za $5\tau$ prakticky ustáleno.

```tikz
\begin{document}
  \begin{tikzpicture}[x=1.1cm,y=1.4cm]
    \draw[->] (0,0) -- (5.6,0) node[right] {$t$};
    \draw[->] (0,0) -- (0,1.45) node[above] {$u_C$};
    \draw[dashed] (0,1) -- (5.2,1) node[right] {$U$};
    \draw[thick,blue,domain=0:5.2,samples=80] plot (\x,{1-exp(-\x)});
    \draw[dashed] (1,0) node[below] {$\tau$} -- (1,0.632);
    \draw[dashed] (0,0.632) node[left] {$0{,}63U$} -- (1,0.632);
  \end{tikzpicture}
\end{document}
```

## Dvojbrany a přenos

Dvojbran = obvod se vstupní a výstupní bránou. V HUS jej popisují čtyři veličiny $\hat U_1, \hat I_1, \hat U_2, \hat I_2$ a dvojice rovnic, např.:

- **Impedanční parametry:** $\hat U_1 = Z_{11}\hat I_1 + Z_{12}\hat I_2$, $\hat U_2 = Z_{21}\hat I_1 + Z_{22}\hat I_2$.
- **Admitanční** ($Y$), **kaskádní** ($A$) — volí se podle způsobu spojování dvojbranů (kaskáda → násobení matic $A$).

Parametry se měří stavem naprázdno/nakrátko na druhé bráně (např. $Z_{11} = \hat U_1/\hat I_1$ při $\hat I_2=0$). **Přenos napětí naprázdno** $\hat K_u = \hat U_2/\hat U_1\big|_{I_2=0}$; u zatíženého dvojbranu závisí na zátěži. Vstupní impedance $\hat Z_{vst} = \hat U_1/\hat I_1$ se zátěží na výstupu.

## Periodický neharmonický ustálený stav

Periodický signál se rozloží Fourierovou řadou na stejnosměrnou složku a harmonické. Lineární obvod se řeší **superpozicí po harmonických**: každá složka projde přenosem $\hat K(jk\omega_1)$ a výsledky se sečtou. Efektivní hodnota: $U^2 = U_0^2 + \sum_k U_k^2$.

## Co umět u zkoušky

- Zavést fázor, napsat impedance $R$, $L$, $C$ a fázové vztahy.
- Odvodit přenos RC článku, nakreslit modulovou i fázovou charakteristiku, vyznačit $\omega_0$ a −3 dB.
- **Kraje přenosové funkce určit limitami** ($C$/L → zkrat/rozpojení) bez počítání.
- Sériová rezonance: $\omega_0$, $Q$, šířka pásma, co se děje s proudem a napětími.
- Přechodný děj 1. řádu třemi čísly $x(0^+)$, $x(\infty)$, $\tau$ + spojitost $u_C$, $i_L$.
- Dvojbran: co jsou Z/Y/A parametry, jak se měří, co je přenos naprázdno.
