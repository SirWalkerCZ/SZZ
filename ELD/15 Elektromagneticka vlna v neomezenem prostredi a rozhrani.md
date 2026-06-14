# 15 Elektromagnetická vlna v neomezeném prostředí a na rozhraní

> Hlavní podklad: [[Elektromagnetická vlna_13_5_2021.pdf]]. Znění okruhu: [[SZZ - Odborné okruhy|odborný okruh 15]].

## Elektromagnetická vlna v neomezeném prostředí

Elektromagnetická vlna je časově proměnné elektrické a magnetické pole, které se šíří prostorem. V neomezeném homogenním prostředí nejsou přítomna rozhraní ani vodivé stěny, takže tvar vlny určuje hlavně zdroj a parametry prostředí $\varepsilon$, $\mu$, $\sigma$.

V harmonickém popisu se časová závislost převádí do fázorů a šíření se vyjadřuje komplexním vlnovým číslem

$$
\hat k=\beta-j\alpha,
$$

kde $\beta$ je fázová konstanta a $\alpha$ měrný útlum. V bezeztrátovém prostředí je $\alpha=0$; v dobře vodivém prostředí amplituda rychle klesá a zavádí se hloubka vniku

$$
\delta=\frac{1}{\alpha}.
$$

Přenášený výkon popisuje Poyntingův vektor

$$
\mathbf S=\mathbf E\times\mathbf H,
\qquad
\mathbf S_\mathrm{stř}
=\frac12\operatorname{Re}(\hat{\mathbf E}\times\hat{\mathbf H}^{*}).
$$

**Zdroj:** [[Elektromagnetická vlna_13_5_2021.pdf#page=9|ELD s. 9]], [[Elektromagnetická vlna_13_5_2021.pdf#page=16|ELD s. 16]], [[Elektromagnetická vlna_13_5_2021.pdf#page=19|ELD s. 19]], [[Elektromagnetická vlna_13_5_2021.pdf#page=25|ELD s. 25]].

## Maxwellovy rovnice

Nestacionární elektrické a magnetické pole nelze oddělit: časová změna jedné složky budí druhou. ELD začíná rotačními Maxwellovými rovnicemi

$$
\operatorname{rot}\mathbf H
=\mathbf J+\frac{\partial\mathbf D}{\partial t},
$$

$$
\operatorname{rot}\mathbf E
=-\frac{\partial\mathbf B}{\partial t}.
$$

V lineárním izotropním prostředí platí

$$
\mathbf D=\varepsilon\mathbf E,\qquad
\mathbf B=\mu\mathbf H,\qquad
\mathbf J=\sigma\mathbf E.
$$

Po dosazení materiálových vztahů a vyloučení jedné složky pole vznikne vlnová rovnice. Pro elektrickou intenzitu mimo zdroje má tvar

$$
\nabla^2\mathbf E
-\mu\sigma\frac{\partial\mathbf E}{\partial t}
-\mu\varepsilon\frac{\partial^2\mathbf E}{\partial t^2}=0.
$$

Pro harmonické průběhy přechází na Helmholtzovu rovnici.

**Zdroj:** [[Elektromagnetická vlna_13_5_2021.pdf#page=5|ELD s. 5]], [[Elektromagnetická vlna_13_5_2021.pdf#page=6|ELD s. 6]], [[Elektromagnetická vlna_13_5_2021.pdf#page=7|ELD s. 7]].

## Vlna rovinná, kulová a válcová

Rovinná vlna má rovinné vlnoplochy. Pole závisí jen na souřadnici ve směru šíření; pro šíření ve směru $+z$ lze psát

$$
\hat E_x(z)=\hat E_0e^{-j\hat k z},
$$

$$
E_x(z,t)=E_m e^{-\alpha z}\sin(\omega t-\beta z+\varphi_0).
$$

V rovinné vlně jsou $\mathbf E$, $\mathbf H$ a směr šíření navzájem kolmé. Vlnová impedance je

$$
\hat Z=\frac{\hat E_x}{\hat H_y}.
$$

Vlnová délka a fázová rychlost jsou

$$
\lambda=\frac{2\pi}{\beta},
\qquad
v_f=\frac{\omega}{\beta}.
$$

Kulová vlna má vlnoplochy ve tvaru koulí. Vzniká typicky od bodového zdroje; ve velké vzdálenosti se malý výřez kulové vlnoplochy dá aproximovat rovinnou vlnou. Amplituda ideální kulové vlny klesá přibližně jako $1/r$.

Válcová vlna má vlnoplochy ve tvaru válců, například u dlouhého čárového zdroje. Ve vzdáleném poli ideální válcové vlny klesá amplituda přibližně jako $1/\sqrt{\rho}$.

**Zdroj:** [[Elektromagnetická vlna_13_5_2021.pdf#page=2|ELD s. 2]], [[Elektromagnetická vlna_13_5_2021.pdf#page=3|ELD s. 3]], [[Elektromagnetická vlna_13_5_2021.pdf#page=9|ELD s. 9]], [[Elektromagnetická vlna_13_5_2021.pdf#page=14|ELD s. 14]], doplněk k zadání podle [[hex_compost.pdf#page=157|HEX s. 157]].

## Gaussův svazek

Gaussův svazek je směrový svazek s přibližně Gaussovým příčným rozložením amplitudy nebo intenzity. Používá se jako aproximace laserového svazku. Má osu šíření, nejužší místo svazku o poloměru $w_0$ a Rayleighovu vzdálenost

$$
z_R=\frac{\pi w_0^2}{\lambda}.
$$

Blízko pasu svazku se chová podobně jako rovinná vlna, s rostoucí vzdáleností se začne rozbíhat a jeho vlnoplochy se více podobají kulovým. Rozbíhavost pro velké vzdálenosti souvisí s poměrem $\lambda/w_0$: čím menší je pas svazku, tím větší je difrakční rozbíhavost.

**Zdroj:** doplněk k zadání podle [[hex_compost.pdf#page=158|HEX s. 158]], [[hex_compost.pdf#page=159|HEX s. 159]]. V dodaném ELD PDF není Gaussův svazek samostatně vyložen.

## Vlna na rozhraní dvou prostředí

Při dopadu rovinné vlny na rozhraní dvou prostředí vzniká dopadající, odražená a prostupující vlna. Rovina dopadu obsahuje vlnové vektory dopadající a odražené vlny a normálu k rozhraní.

Na rozhraní musí být splněna spojitost tečných složek polí

$$
\hat E_{1t}=\hat E_{2t},
\qquad
\hat H_{1t}=\hat H_{2t}.
$$

Z okrajových podmínek plyne zákon odrazu a Snellův zákon. Při kolmém dopadu je činitel odrazu

$$
\hat R=\frac{\hat Z_2-\hat Z_1}{\hat Z_2+\hat Z_1},
$$

a činitel prostupu

$$
\hat T=\frac{2\hat Z_2}{\hat Z_2+\hat Z_1}.
$$

Při šikmém dopadu záleží na polarizaci vůči rovině dopadu. Rozlišuje se kolmá polarizace, kde $\mathbf E$ je kolmá na rovinu dopadu, a rovnoběžná polarizace, kde $\mathbf E$ leží v rovině dopadu.

**Zdroj:** [[Elektromagnetická vlna_13_5_2021.pdf#page=37|ELD s. 37]], [[Elektromagnetická vlna_13_5_2021.pdf#page=38|ELD s. 38]], [[Elektromagnetická vlna_13_5_2021.pdf#page=45|ELD s. 45]], [[Elektromagnetická vlna_13_5_2021.pdf#page=46|ELD s. 46]].

## Totální odraz

Totální odraz nastává při přechodu z opticky hustšího prostředí do řidšího, pokud je úhel dopadu větší než kritický. Pro nemagnetická dielektrika ELD uvádí

$$
\vartheta_{i,\mathrm{kr}}
=\arcsin\sqrt{\frac{\varepsilon_{r2}}{\varepsilon_{r1}}},
\qquad
\varepsilon_{r2}<\varepsilon_{r1}.
$$

Pro větší úhly je velikost činitele odrazu rovna jedné:

$$
|\hat R_\parallel|=|\hat R_\perp|=1.
$$

To neznamená, že v druhém prostředí není žádné pole; vniká do něj evanescentní pole, které nepřenáší výkon kolmo hluboko do prostředí.

**Zdroj:** [[Elektromagnetická vlna_13_5_2021.pdf#page=63|ELD s. 63]], [[Elektromagnetická vlna_13_5_2021.pdf#page=64|ELD s. 64]], [[Elektromagnetická vlna_13_5_2021.pdf#page=65|ELD s. 65]].

## Evanescentní vlna

> 🔬 **Interaktivní simulace:** pole evanescentní vlny při totálním odrazu — `sim/eld_evanescent.html` (sekce *Simulace → ELD* ve wiki). Ukazuje interferenci dopadající a odražené vlny nad rozhraním a exponenciálně tlumené pole postupující podél rozhraní pod ním.

Evanescentní vlna se šíří podél rozhraní, ale kolmo od rozhraní exponenciálně zaniká. U totálního odrazu má prostupující pole tvar

$$
\hat E_t(x,y,z)
=\hat E_{t0}e^{-jk_2px}e^{-k_2qz}.
$$

Člen $e^{-jk_2px}$ popisuje postup podél rozhraní, člen $e^{-k_2qz}$ útlum ve směru kolmo od rozhraní. Evanescentní vlna je důležitá právě proto, že i při totálním odrazu musí pole splnit okrajové podmínky na rozhraní.

**Zdroj:** [[Elektromagnetická vlna_13_5_2021.pdf#page=66|ELD s. 66]], [[Elektromagnetická vlna_13_5_2021.pdf#page=67|ELD s. 67]].

## Polarizace vlny odrazem

Polarizace popisuje směr kmitání elektrické intenzity. Obecnou vlnu lze rozložit na dvě složky vůči rovině dopadu: kolmou a rovnoběžnou.

Polarizace odrazem nastane, když se jedna polarizační složka odráží jinak než druhá. U rozhraní dvou dielektrik může pro rovnoběžnou polarizaci existovat Brewsterův úhel, při kterém se rovnoběžná složka neodrazí. ELD pro nemagnetická dielektrika uvádí

$$
\vartheta_{i,\mathrm{BR}}
=\arcsin
\frac{1}{\sqrt{1+\frac{\varepsilon_{r1}}{\varepsilon_{r2}}}}.
$$

Pokud na rozhraní dopadá nepolarizovaná nebo obecně polarizovaná vlna, odražená vlna je při Brewsterově úhlu polarizovaná převážně kolmo k rovině dopadu.

**Zdroj:** [[Elektromagnetická vlna_13_5_2021.pdf#page=26|ELD s. 26]], [[Elektromagnetická vlna_13_5_2021.pdf#page=38|ELD s. 38]], [[Elektromagnetická vlna_13_5_2021.pdf#page=76|ELD s. 76]], [[Elektromagnetická vlna_13_5_2021.pdf#page=77|ELD s. 77]].

## Co umět u zkoušky

- Zapsat rotační Maxwellovy rovnice a materiálové vztahy.
- Vysvětlit rovinnou vlnu, $\alpha$, $\beta$, $\lambda$, $v_f$, vlnovou impedanci a Poyntingův vektor.
- Rozlišit rovinnou, kulovou a válcovou vlnu.
- Stručně popsat Gaussův svazek jako model laserového svazku.
- Popsat dopad na rozhraní, okrajové podmínky, odraz a prostup.
- Vysvětlit kritický úhel, totální odraz, evanescentní vlnu a polarizaci odrazem.
