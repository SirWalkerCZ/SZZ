# 12 Aktivní prvky: MOSFET, BJT, zesilovač SE, usměrňovač, optoelektronika

> Hlavní podklad: elp1/elp2.pdf (ek-drive), HEX compost. Znění okruhu: [[SZZ - Odborné okruhy|odborný okruh 12]].
> **Komise se ptá (Voves/Novák):** struktura MOSFETu; BJT zesilovač — nakreslit, vysvětlit, pracovní bod graficky, rozkmit; usměrňovač; fotodioda — fotovoltaický vs. fotovodivostní režim; LED; proč je na PN přechodu ~0,7 V.

## PN přechod prakticky: proč ~0,6–0,7 V

Spojením P a N polovodiče difundují nosiče přes rozhraní a vznikne vyprázdněná oblast s vestavěným (difúzním) napětím — u křemíku ~0,6–0,7 V (dáno šířkou zakázaného pásu a dotacemi). Proud diodou roste exponenciálně podle Shockleyho rovnice

$$
I = I_0\big(e^{U/U_T}-1\big),
\qquad U_T = \frac{kT}{q}\approx 26\ \mathrm{mV},
$$

takže pod ~0,6 V je proud zanedbatelný a nad ním roste velmi strmě — proto se v prvním přiblížení počítá s konstantním úbytkem $U_D \approx 0{,}7$ V (Schottky ~0,3 V).

## Usměrňovač

**Jednocestný:** jedna dioda propustí kladné půlvlny, záporné ořeže. Střední hodnota výstupu nízká, zvlnění na kmitočtu sítě $f$.

**Dvoucestný můstkový (Graetz):** čtyři diody, obě půlvlny se překlopí nahoru — zvlnění na $2f$, lepší využití transformátoru. Proud teče vždy přes dvě diody → úbytek $2U_D \approx 1{,}4$ V.

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=1cm]
    % vstupni sinusovka
    \draw[->] (0,0) -- (3.4,0) node[right] {$t$};
    \draw[->] (0,-1.2) -- (0,1.4) node[above] {$u_1$};
    \draw[blue,thick,domain=0:3.1,samples=80] plot (\x,{sin(2*\x r)});
    % sipka
    \draw[->,very thick] (3.9,0) -- (4.7,0);
    \node[above] at (4.3,0.1) {můstek};
    % vystup dvoucestny
    \draw[->] (5.2,0) -- (8.8,0) node[right] {$t$};
    \draw[->] (5.2,-1.2) -- (5.2,1.4) node[above] {$u_2$};
    \draw[red,thick,domain=5.2:8.5,samples=120] plot (\x,{abs(sin(2*(\x-5.2) r))});
    % vyhlazeny prubeh s kondenzatorem
    \draw[dashed,thick,domain=5.2:8.5,samples=80] plot (\x,{0.78+0.18*cos(4*(\x-5.2) r)});
    \node at (7.4,1.25) {s kondenzátorem};
  \end{tikzpicture}
\end{document}
```

**Filtrační (sběrací) kondenzátor:** nabije se na špičku a mezi špičkami se vybíjí do zátěže — výstup se vyhladí. Zvlnění přibližně

$$
\Delta U \approx \frac{I_z}{f_{zvl}\,C},
$$

kde $f_{zvl}=f$ (jednocestný) nebo $2f$ (dvoucestný). Větší $C$ nebo menší odebíraný proud → menší zvlnění. Diody pak vedou jen v krátkých špičkách (velký opakovaný špičkový proud).

**LED + předřadný rezistor** (oblíbená rychlovka): $R = \dfrac{U_{nap}-U_{LED}}{I_{LED}}$, např. $\frac{5-2}{10\ \mathrm{mA}} = 300\ \Omega$.

## MOSFET — struktura a princip

NMOS: P-substrát, v něm silně dotované oblasti N⁺ Source a Drain, mezi nimi nad substrátem tenký oxid SiO₂ a hradlo (Gate). Gate je **dielektricky izolován** → $I_G \approx 0$, obrovský vstupní odpor.

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=1cm]
    % substrat
    \draw[thick] (0,0) rectangle (8,2.2);
    \node at (4,0.5) {P substrát};
    % n+ oblasti
    \draw[thick] (0.7,1.5) rectangle (2.5,2.2);
    \node at (1.6,1.85) {N$^+$};
    \draw[thick] (5.5,1.5) rectangle (7.3,2.2);
    \node at (6.4,1.85) {N$^+$};
    % oxid
    \fill[gray!30] (2.5,2.2) rectangle (5.5,2.45);
    \draw[thick] (2.5,2.2) rectangle (5.5,2.45);
    \node[right] at (5.6,2.35) {SiO$_2$};
    % gate
    \draw[very thick] (2.5,2.45) rectangle (5.5,2.75);
    \node at (4,2.6) {G};
    % kontakty
    \draw[thick] (1.6,2.2) -- (1.6,3.1) node[above] {S};
    \draw[thick] (6.4,2.2) -- (6.4,3.1) node[above] {D};
    \draw[thick] (4,2.75) -- (4,3.1);
    % kanal
    \draw[dashed,red,very thick] (2.5,1.45) -- (5.5,1.45);
    \node[red,below] at (4,1.4) {indukovaný kanál};
  \end{tikzpicture}
\end{document}
```

Kladné $U_{GS}$ odpudí díry pod hradlem a přitáhne elektrony; nad **prahovým napětím** $U_T$ nastane inverze a vznikne vodivý N-kanál mezi S a D. Výstupní charakteristiky $I_D(U_{DS})$ mají odporovou (lineární) oblast a oblast saturace, kde $I_D \sim (U_{GS}-U_T)^2$.

Proč MOSFET ovládl čipy: izolované hradlo (nulová statická spotřeba, CMOS), vysoká hustota integrace, majoritní nosiče → rychlé spínání. Nevýhoda: citlivost na ESD, vyšší šum 1/f.

## JFET — videa (princip a zaškrcení kanálu)

> 🎥 **What is a JFET and how does it work?** (CircuitBread)

<div style="position:relative;padding-bottom:56.25%;height:0;margin:14px 0;max-width:680px;border-radius:8px;overflow:hidden">
<iframe src="https://www.youtube-nocookie.com/embed/y-ZT7Rd-ATI" title="What is a JFET" loading="lazy" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position:absolute;inset:0;width:100%;height:100%;border:0"></iframe>
</div>

> 🎥 **The VI Characteristics and Operating Regions of a JFET** (CircuitBread)

<div style="position:relative;padding-bottom:56.25%;height:0;margin:14px 0;max-width:680px;border-radius:8px;overflow:hidden">
<iframe src="https://www.youtube-nocookie.com/embed/l_RgDI6Hx-w" title="JFET VI characteristics" loading="lazy" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="position:absolute;inset:0;width:100%;height:100%;border:0"></iframe>
</div>

## BJT — struktura a charakteristiky

NPN: dva PN přechody (B–E, B–C), řízen **proudem báze**. Otevřený tranzistor: přechod B–E propustně (~0,7 V), B–C závěrně. Elektrony injektované z emitoru projdou tenkou slabě dotovanou bází (většina nestihne zrekombinovat) a jsou strženy do kolektoru:

$$
I_C = \beta\, I_B, \qquad \beta \approx 50\text{–}500.
$$

Vstupní charakteristika $I_B(U_{BE})$ = dioda; výstupní $I_C(U_{CE})$ pro různé $I_B$ — aktivní oblast (vodorovné křivky), saturace ($U_{CE} < \approx0{,}2$ V), závěrný stav.

## Zesilovač se společným emitorem — pracovní bod graficky

Schéma, které komise chce vidět na tabuli:

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=1cm]
    % napajeci linie
    \draw[thick] (0.5,4.6) -- (7,4.6) node[right] {$+U_{CC}$};
    % R1
    \draw[thick] (1.5,4.6) -- (1.5,4.1);
    \draw[thick] (1.25,3.1) rectangle (1.75,4.1);
    \node[left] at (1.2,3.6) {$R_1$};
    \draw[thick] (1.5,3.1) -- (1.5,1.9);
    % R2
    \draw[thick] (1.25,0.9) rectangle (1.75,1.9);
    \node[left] at (1.2,1.4) {$R_2$};
    \draw[thick] (1.5,0.9) -- (1.5,0.3);
    % RC
    \draw[thick] (4.5,4.6) -- (4.5,4.1);
    \draw[thick] (4.25,3.1) rectangle (4.75,4.1);
    \node[left] at (4.2,3.6) {$R_C$};
    \draw[thick] (4.5,3.1) -- (4.5,2.9);
    % tranzistor (zjednodusene)
    \draw[very thick] (4.1,2.9) -- (4.1,1.7);
    \draw[thick] (1.5,2.3) -- (4.1,2.3);
    \fill (1.5,2.3) circle (1.5pt);
    \draw[thick] (4.1,2.6) -- (4.5,2.9);
    \draw[->,thick] (4.1,2.0) -- (4.5,1.7);
    \node at (3.7,2.55) {B};
    % RE
    \draw[thick] (4.5,1.7) -- (4.5,1.5);
    \draw[thick] (4.25,0.5) rectangle (4.75,1.5);
    \node[left] at (4.2,1.0) {$R_E$};
    \draw[thick] (4.5,0.5) -- (4.5,0.3);
    % zem
    \draw[thick] (0.5,0.3) -- (7,0.3);
    % vystup
    \fill (4.5,2.95) circle (1.5pt);
    \draw[thick] (4.5,2.95) -- (6,2.95) node[right] {$u_2$ (přes $C_v$)};
    % vstup
    \draw[thick] (0.3,2.3) node[left] {$u_1$} -- (1.5,2.3);
  \end{tikzpicture}
\end{document}
```

- Dělič $R_1, R_2$ nastaví stejnosměrné napětí báze; $R_E$ zavádí zápornou zpětnou vazbu → stabilizace pracovního bodu proti teplotě a rozptylu $\beta$. Vazební kondenzátory oddělují DC.
- SE zapojení **obrací fázi o 180°**, zesílení přibližně $A_u \approx -R_C/R_E$ (s blokovacím kondenzátorem přes $R_E$ větší, $\approx -g_m R_C$).

### Zatěžovací přímka a pracovní bod

Stejnosměrně platí $U_{CC} = R_C I_C + U_{CE}$ (+ $R_E I_E$), tedy v rovině výstupních charakteristik přímka

$$
I_C = \frac{U_{CC} - U_{CE}}{R_C},
$$

s krajními body $(U_{CE}=U_{CC},\ I_C=0)$ a $(U_{CE}=0,\ I_C=U_{CC}/R_C)$. **Pracovní bod Q** = průsečík zatěžovací přímky s charakteristikou pro nastavené $I_B$.

```tikz
\begin{document}
  \begin{tikzpicture}[x=1cm,y=1cm]
    \draw[->] (0,0) -- (7,0) node[right] {$U_{CE}$};
    \draw[->] (0,0) -- (0,4) node[above] {$I_C$};
    % vystupni charakteristiky
    \foreach \y/\l in {0.8/1,1.6/2,2.4/3,3.2/4}
      \draw[blue,thick] (0,0) .. controls (0.3,\y) and (0.5,\y) .. (0.7,\y) -- (6.3,\y+0.12) node[right,font=\small] {$I_{B\l}$};
    % zatezovaci primka
    \draw[red,very thick] (6,0) node[below] {$U_{CC}$} -- (0,3.6) node[left] {$\frac{U_{CC}}{R_C}$};
    % pracovni bod
    \fill (2.95,1.83) circle (2.5pt);
    \node[above right] at (2.95,1.85) {Q};
    \draw[dashed] (2.95,1.83) -- (2.95,0) node[below] {$U_{CEP}$};
    \draw[dashed] (2.95,1.83) -- (0,1.83) node[left] {$I_{CP}$};
    % rozkmit
    \draw[<->,thick] (0.45,-0.65) -- (5.95,-0.65);
    \node[below] at (3.2,-0.7) {využitelný rozkmit $u_{CE}$};
    \draw[dashed] (0.45,0) -- (0.45,-0.7);
    \node[below,font=\small] at (0.55,0) {$U_{CEsat}$};
  \end{tikzpicture}
\end{document}
```

**Rozkmit při daném $U_{CC}$:** výstup se může hýbat jen mezi saturací ($U_{CEsat}\approx0{,}2$ V) a zavřeným tranzistorem ($U_{CE}=U_{CC}$). Maximální nezkreslený rozkmit vyjde při $U_{CEP} \approx U_{CC}/2$; špička-špička pak $\approx U_{CC} - U_{CEsat}$. Při přebuzení se signál **ořízne**: zdola saturací (tranzistor plně otevřen), shora $U_{CC}$ (tranzistor zavřen) → harmonické zkreslení.

Grafický postup u tabule: (1) nakreslit charakteristiky, (2) zatěžovací přímku ze dvou krajních bodů, (3) zvolit/odečíst Q uprostřed, (4) ukázat sinusovku kolem Q a její limity.

## Optoelektronické prvky

**Fotodioda:** foton s $h\nu > E_g$ generuje v oblasti přechodu pár elektron–díra, vestavěné pole je separuje → fotoproud úměrný osvětlení. VA charakteristika se osvětlením posouvá dolů (do 3. a 4. kvadrantu).

- **Fotovoltaický režim** (4. kvadrant, bez vnějšího napětí): dioda sama generuje napětí/proud. Minimální temný proud a šum, ale velká kapacita přechodu → **pomalá**. Použití: solární články, expozimetry.
- **Fotovodivostní režim** (3. kvadrant, závěrné napětí): široká vyprázdněná oblast → malá kapacita, **rychlá odezva (ns)** a výborná linearita fotoproudu; teče malý temný proud. Použití: optické komunikace, snímače, pixely CMOS.

Další detektory: fotorezistor (pomalý, levný), fototranzistor (zisk $\beta$, pomalejší), CCD/CMOS snímače.

**LED:** PN přechod v propustném směru, zářivá rekombinace, $\lambda = hc/E_g$. Vyžaduje **přímý polovodič** (GaAs, GaN…); křemík je nepřímý — rekombinace přes fonony, světlo prakticky nevzniká.

**Laserová dioda (princip laseru):** tři interakce světla s hmotou — absorpce, spontánní emise (LED), **stimulovaná emise** (dopadající foton vyvolá emisi druhého, identického fotonu — koherence). Podmínky laserování: **inverze populace** (čerpáním) a **optický rezonátor** (Fabry–Perot, zrcadla) pro zpětnou vazbu a lavinové zesílení.

## Co umět u zkoušky

- Vysvětlit, proč dioda "otvírá" kolem 0,7 V (Shockley, difúzní napětí).
- Nakreslit jednocestný i můstkový usměrňovač s průběhy, vliv filtračního kondenzátoru, odhad zvlnění.
- Spočítat předřadný rezistor LED.
- Nakreslit řez NMOS, vysvětlit inverzi kanálu a prahové napětí; proč MOSFET na čipech.
- BJT: princip ($I_C=\beta I_B$), vstupní/výstupní charakteristiky.
- **Nakreslit zesilovač SE, sestrojit zatěžovací přímku, graficky určit pracovní bod a ukázat rozkmit/oříznutí při daném $U_{CC}$.**
- Fotodioda: oba režimy s kvadranty VA charakteristiky, rychlost vs. šum; LED a podmínky laserování.
