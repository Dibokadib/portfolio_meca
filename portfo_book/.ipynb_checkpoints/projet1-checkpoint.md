---
title: Projet 2
publishDate: 2020-03-04 00:00:00
img: /assets/stock-2.jpg
img_alt: Pearls of silky soft white cotton, bubble up under vibrant lighting
description: |
  Réponse d'une barre à une explosion.
tags:
  - Design
  - Dev
  - Branding
---

<script>
MathJax = {
  	tex: {
    	inlineMath: [['$', '$'], ['\\(', '\\)']]
  	},
  	svg: {
    fontCache: 'global'
  	}
};
</script>

### I. Introduction

<p style="text-align: justify;">
Cette deuxième étude de dynamique de structures porte sur l'équilibre d'un bâtiment à trois étages soumis à un séisme. Nous observerons, dans un premier temps, les modes de vibration en régime libre, puis soumis à un chargement, une excitation extérieure dans la direction parallèle au sol puis dans une direction oblique.
</p>
<p style="text-align: justify;">
Le but sera alors de résoudre le problème aux valeurs propres à l'aide de `POSTVIBR` afin de comparer ces modes propres à la réponse au séisme.
</p>

<p style="text-align: justify;">
La méthode d'intégration utilisée sera implicite car le phénomène étudié est de nature lente contrairement au premier travail pratique où la structure était soumise à une explosion.
</p>

### II. Description du problème

<p style="text-align: justify;">
On considère un bâtiment représenté en Figure 1., dont on souhaite étudier la réponse à un séisme. La modélisation de ce bâtiment a déjà été réalisé dans **Cast3M**.
</p>

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f1.png" alt="Figure 1 : Modélisation du bâtiment" width="300"/>
    <figcaption>Figure 1 : Modélisation du bâtiment</figcaption>
  </figure>
</div>

<p style="text-align: justify;">
À l'aide du jeu de données, trois modèles élémentaires y sont créés :  
— **modpoto** (Figure 2.) : modélise les poteaux avec des poutres de section définie par le modèle mods1.
</p>

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f2.png" alt="Figure 2 : Poteaux" width="300"/>
    <figcaption>Figure 2 : Poteaux</figcaption>
  </figure>
</div>

<p style="text-align: justify;">
— **modpout** (Figure 3.) : modélise les poutres porteuses avec des poutres de section définie par le modèle mods2.
</p>

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f3.png" alt="Figure 3 : Poutres porteuses" width="300"/>
    <figcaption>Figure 3 : Poutres porteuses</figcaption>
  </figure>
</div>

<p style="text-align: justify;">
— **moddiap** (Figure 4.) : modélise les dalles (planchers) avec des coques.
</div> 

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f4.png" alt="Figure 4 : Dalles" width="300"/>
    <figcaption>Figure 4 : Dalles</figcaption>
  </figure>
</div>

<p style="text-align: justify;">
On assemble les différentes parties afin d'obtenir la structure du bâtiment (Figure 5.) pour l'analyse sismique.
</div> 

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f5.png" alt="Figure 6 : Modélisation du bâtiment" width="300"/>
    <figcaption>Figure 5 : Modélisation du bâtiment</figcaption>
  </figure>
</div>

### III. Prise en main du modèle

1. Déterminons dans un premier temps le choix des poutres.

    a. Section des poteaux :  

    De longueur et de largeur respectivement égales à:
    
    <p style="text-align: justify;">
    $$
    \left\{
        \begin{array}{ll}
            a = 0.25 \;m\\
            b = 0.4 \;m
        \end{array}
    \right.
    $$
    </p>

    soit une section 

    <p style="text-align: justify;">
    $$
    S=a\cdot b = 0.1 \, m^2
    $$
    </p>

    b. Section des poutres porteuses :  
    De longueur et de largeur respectivement égales à:
    
    <p style="text-align: justify;">
    $$
    \left\{
        \begin{array}{ll}
            a = 0.50 \;m\\
            b = 0.50 \;m
        \end{array}
    \right.
    $$
    </p>

    soit une section 

    <p style="text-align: justify;">
    $$
    S=a\cdot b = 0.25 \; m^2
    $$
    </p>


2. Montrons dès à présent que les poutres sont bien orientées.

<p style="text-align: justify;">
Le repère lié aux éléments poutres de TIMOshenko est défini en prenant $x_{timo}$ l'axe de la poutre et $y_{timo}$ défini par la composante 'VECT' du matériau. Nous avons pris pour les poutres `VECT = ((-1.)*vz)`, soit $y_{timo}$ dirigé dans le repère global par la direction (0. 0. -1.). D'autre part $x_{section}$ correspond à la longueur b (la plus grande).
</p>


<p style="text-align: justify;">
Le repère du modèle section qui sert à définir la géométrie de la section de la poutre dit repère local est défini par les axes $y_{timo}$ et $z_{timo}$. Or, la section est décrite dans le plan xOy, et d'après l'énoncé nous avons l'axe Ox du repère de description de la section étant identifié à l'axe local Oy de l'élément TIMO, soit $x_{section} = y_{timo}$.
</p>

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f6.png" alt="Figure 6 : Repère local" width="300"/>
    <figcaption>Figure 6 : Repère local</figcaption>
  </figure>
</div>

<p style="text-align: justify;">
Ainsi les poutres seront plutôt orientées comme la poutre de type 1 de la figure
</p>

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f7.png" alt="igure 7 : Poutre de type 1" width="300"/>
    <figcaption>Figure 7 : Poutre de type 1</figcaption>
  </figure>
</div>

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f8.png" alt="Figure 8 : Poutre de type 2" width="300"/>
    <figcaption>Figure 8 : Poutre de type 2</figcaption>
  </figure>
</div>

<p style="text-align: justify;">
En effet l'orientation de la poutre type 1 correspond bien pour soutenir les dalles du bâtiment car dans ce sens la rigidité en flexion D est plus grande.
</p>

<p style="text-align: justify;">
$$D=EI_{z_{timo}}=\frac{ba^3}{12} \qquad \text{avec} a>b$$ 
</p>

### IV. Analyse modale

3. Conditions aux limites

    Les neufs poteaux sont encastrés au sol à leurs extrémités droites.

    ```gibiane
    *  MAILLAGE du 1er etage  
    meshp0 = pj01 et pj02 et pj03
    et pj11 et pj12 et pj13
    et pj21 et pj22 et pj23;
    * CONDITIONS AUX LIMITES 
    cl = BLOQ DEPL ROTA meshp0 ;
    ```

4. Calculons les matrices nécessaires pour cette étude.

    ```gibiane
    * MATRICES NECESSAIRES : RAIDEUR et MASSE
      K = RIGI modtot mattot;
      M = MASS modtot mattot;
    * ASSEMBLAGE
      Ktot = K et cl ;
    ```

5. Calculons les modes propres (via VIBR ’IRAM’) et post-traitons les (via EXPLORER ou POSTVIBR).

    ```gibiane
    * ANALYSE MODALE
    * Nmode = 100;
      Nmode =  40;
      Tmode = VIBR 'IRAM' 1. Nmode Ktot M 'TBAS';
      POSTVIBR Tmode;
    ```

<p style="text-align: justify;">
`Tmode` nous permet ici de calculer une collection de phases et de pulsations ($\Phi$,$w$) qui, par la suite, permettra de calculer les modes propre de la structure via la résolution:
</p>

$$ (K - w^2M)\Phi = 0 $$
  
<p style="text-align: justify;">
avec $K$ et $M$ respectivement les matrices de rigidité et de masse et calculées à la question ultérieure (4.).
</p>

<p style="text-align: justify;">
 $\underline{Remarque}$ : La procédure `POSTVIBR` a été rajoutée au code permettant de dépouiller graphiquement les résultats d'une table `BASE MODALE`.
</p>

<p style="text-align: justify;">
6. Combien en avons-nous calculer ? Pouvez-nous le justifier dès à présent ?  
Nous avons calculé les cent premiers modes puis les 40 premiers modes, mais sans raison valable. En effet, à ce stade il n'est pas encore possible de déterminer quels seront les modes intéressants pour le calcul de l'équilibre de la structure du séisme, puisque ces modes dépendent directement de la force d'excitation de l'onde sismique.
</p>

### V. Réponse au séisme

<p style="text-align: justify;">
Nous allons étudier la réponse du bâtiment au séisme. Un séisme est un mouvement du sol que l'on notera $u_{sol}(t)$ souvent donné en terme d’accélération $\ddot{u}_{sol}(t)$. Les études de séisme considèrent le mouvement relatif du bâtiment noté $u(t) = u_{tot}(t) - u_{sol}(t)$.
</p>

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f9.png" alt="Modélisation de la réponse au séisme" width="300"/>
    <figcaption>Figure 9 : Modélisation de la réponse au séisme</figcaption>
  </figure>
</div>

<p style="text-align: justify;">
7. En se rappelant que le principe fondamental de la dynamique s’applique sur le mouvement absolu :  
$u_{tot} = u_{sol} + u$, écrivons l’équation d’équilibre.
</p>

<p style="text-align: justify;">
$$  M\ddot{u}_{tot} + C\dot{u}_{tot} + Ku_{tot} = 0 $$
</p>

avec, $u_{tot} = u_{sol} + u$, on obtient :

<p style="text-align: justify;">
\begin{equation} 
    M(\ddot{u}_{sol} + \ddot{u}) + C(\dot{u}_{sol} + \dot{u}) + K(u_{sol} + u) = 0
\end{equation}
</p>

<p style="text-align: justify;">
Soit l’équation différentielle de la réponse du bâtiment au séisme :
</p>

<p style="text-align: justify;">
\begin{equation}
M\ddot{u} + C\dot{u} + Ku = -M\ddot{u}_{sol} - C\dot{u}_{sol} - Ku_{sol}
\end{equation}
</p>

<p style="text-align: justify;">
On passe ensuite les terme inconnus à gauche et les termes connus à droite de l'expression, ce qui donne :
</p>

<p style="text-align: justify;">
\begin{equation} 
\underbrace{M\ddot{u} + C\dot{u} + Ku}_{\text{solide déformable}} = \underbrace{\overbrace{-M\ddot{u}_{sol}}^{F} - \cancel{C\dot{u}_{sol}} - \cancel{Ku_{sol}}}_{\text{sol rigide}}
\end{equation}
</p>
L'équation du séisme s'écrit alors:
<p style="text-align: justify;">
\begin{equation}
\textcolor{red}{\fbox{$
\textcolor{white}{M\ddot{u} + C\dot{u} + Ku = -M\ddot{u}_{sol}}
$}}
\end{equation}
</p>

<li> Traçons le signal de l’accélération en fonction du temps récupéré via $\texttt{ACQU}$.

```gibiane
* RECUPERATION DU SIGNAL
  nligne = 1189;
  OPTI 'ACQU' 'Melendy.t';
  ACQUE lt*'LISTREEL' nligne;
  OPTI 'ACQU' 'Melendy.acc';
  ACQUE la*'LISTREEL' nligne;
  acc_mel  = EVOL 'ORAN' 'MANU'  'LEGE' 'Melendy' 
            't (s)' lt '\g (m/s^{2})' la;
  DESS acc_mel;
```

<p style="text-align: justify;">
Ainsi \texttt{lt} représente une liste de 1189 points espacés d'une valeur $2.10^{-2}$ (pas de temps) permettant de créer l'abscisse en temps de la durée du phénomène, avec un temps maximum donné par \texttt{MAXI lt} = 23,76 s.
</p>
\begin{equation}
dt = \frac{\text{temps total}}{\text{nombre de lignes}} = \frac{23.76}{1189} = 2.10^{-2} s 
\label{dt}
\end{equation}

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f10.png" alt="Signal de l'accélération en fonction du temps" width="500"/>
    <figcaption>Figure 10 : Signal de l'accélération en fonction du temps</figcaption>
  </figure>
</div>

<p style="text-align: justify;">
9. Calculons la transformée de Fourier de ce signal pour la plage de fréquences $[0-40] Hz$ (via $\texttt{TFR ’MOPH’}$).
La commande $\texttt{TFR}$ demande un nombre entier de points égale à $2^p$.
</div>
<p style="text-align: justify;">
Puisque pour $p = 10$ on tronque 165 points (pertes d'informations), on préfère prendre $p = 11$, quitte à compléter avec des zéros le surplus. Autre chose, le calcul de la $\texttt{TFR}$ nous donne deux évolutions en fonction de la fréquence, la phase et l'amplitude, on choisit ici de tracer l'amplitude à l'aide de $\texttt{EXTR}$ et $\texttt{MODULE}$.
</div>

```gibiane
* TRANSFORMEE DE FOURIER 
  p = (log nligne )/(log 2.);
  MESS p;
  p = ENTI 'SUPERIEUR' p;
  Tacc = TFR acc_mel p 'MOPH' 'FMIN' 0. 'FMAX' 40.;
  Tmodu = EXTR Tacc 'COUR' 'MODULE';
  DESS Tmodu;
```

<p style="text-align: justify;">
D'aprés [\ref{dt}] on a $df = \frac{1}{dt} = 50 Hz$. Or d'après le théorème de $\textit{Shanon}$ on a
</div>
\begin{equation}
f_{max} \leq \frac{df}{2} = 25 Hz  
\end{equation}
<p style="text-align: justify;">
La plage de fréquences ne peut pas aller au-delà de $25 Hz$ (\texttt{FMAX} $= 40 Hz$), ce qui justifie la figure suivante lorsque l'on a à calculer la TFR.
</div>
<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f11.png" alt="Transformée de Fourrier du signal d'accélération}" width="500"/>
    <figcaption>Figure 11 :Transformée de Fourrier du signal d'accélération}
  </figure>
</div>

<p style="text-align: justify;">
10. En comparant aux fréquences propres, on observe que la structure soumise au séisme ne fait pas participer la totalité des modes dans la plage de fréquences étudié. 0n constate un décalage fréquentiel entre l'excitation et les modes propres. De plus, le module du signal d'accélération est maximal aux alentours de $5 Hz$ et est nul au-delà de $20 Hz$ (voir figure c si-dessus [\ref{TFRcourbe}]). Ainsi le chargement sollicite davantage le mode propre correspondant au mode de torsion (figure ci dessous).
</div>


<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f12.png" alt="Mode 3 : f= 4.27 Hz}" width="500"/>
    <figcaption>Figure 12 : Mode 3 : f= 4.27 Hz}
  </figure>
</div>

<p style="text-align: justify;">
$\texttt{Conclusion}$ : Pour ce chargement le mode de torsion est le plus critique pour l'équilibre de la structure. Il suffit, d'après cette analyse, de prendre au minima les quatre premiers modes.  Cependant, il est nécessaire, pour l'analyse complète de l'équilibre du bâtiment, de prendre en compte les modes allant jusqu'à une fréquence de 20 Hz après laquelle l'amplitude est nulle. Dans le cas le plus général d'une étude complète, on prendra jusqu'à douze modes, au delà les modes n'affectent pas l'équilibre de la structure.
</div>

<p style="text-align: justify;">
11. Le paramètre $\beta$ fourni dans le jeu de données correspond à l'angle de chargement, angle pris entre la direction parallèle au sol et la direction de la force d'excitation du séisme dans le sens trigonométrique. Pour $\beta = 0$, la force est donc uniquement selon $u_x$.
</div>

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f13.png" alt="Coin du bâtiment}" width="200"/>
    <figcaption>Figure 13 : Coin du bâtiment}
  </figure>
</div>


<p style="text-align: justify;">
On peut alors définir le chargement en créant un vecteur unitaire de type champ par point paramétré avec la valeur de $\beta$, qui dans le cas $\beta = 0$ donne UX = 1 et UY = 0 en tout point de la structure :
</div>

```gibiane
un_x  = MANU 'CHPO' meshtot 2 
          'UX' (cos beta) 'UY' (sin beta) 'NATURE' 'DIFFUS';
* force (2nd membre) = ...
acc_x = -1.*M *un_x;
```
<p style="text-align: justify;">
Nous pouvons alors former le chargement qui sera dirigé, proportionnel à la masse et en relation avec l’équation de la dynamique préalablement établie,
</div>

```gibiane
 * objet chargement :  
 CHA1 = CHAR 'MECA' acc_x acc_mel;
```

<p style="text-align: justify;">
12. Réalisons l’intégration temporelle avec le schéma de l’accélération moyenne (via DYNAMIC) sur base physique.
</div>

<p style="text-align: justify;">
Remarque : puisque l'équation différentielle est d'ordre 2, nous avons besoin de deux conditions initiales:
</div>

```gibiane
* CONDITIONS INITIALES
  U0 = MANU CHPO meshtot 2 'UX' 0. 'UY' 0. 'NATURE' 'DIFFUS';
  V0 = U0;
```

<p style="text-align: justify;">
Après avoir créé la table TAB1, on effectue un premier appel de $\texttt{DYNAMIC}$
</div>

```gibiane
* INTEGRATION TEMPORELLE 
  TAB1 = DYNAMIC TAB2 ;
```
 qui permet de traiter les modes avec la formule [\ref{mode}],
 
 \begin{equation}
    (K - w^2M)\Phi = 0
    \label{mode}
 \end{equation}

<p style="text-align: justify;">
Justifions dès à présent le choix du pas de temps ainsi que la durée du calcul.
</div>

```gibiane
* DISCRETISATION TEMPORELLE
  tfin  = 23.70;
  dt    = 2E-2;
  tprog = prog 0. PAS dt tfin;
  nt    = DIME tprog;
```

<p style="text-align: justify;"> 
13. On lance ensuite le calcul, et on remarque que les oscillations en fin de calcul perdurent, cela n'est pas réaliste. En effet un élément de modélisation a été négligé, responsable de ce phénomène, qui n'est autre que l'amortissement dénommé C.
</div>

<p style="text-align: justify;"> 
On intègre maintenant le paramètre d'amortissement et on relance le calcul. On constate alors que le calcul se termine plus rapidement.
</div>

<p style="text-align: justify;"> 
$\texttt{Conclusion}$ : Le paramètre d'amortissement est essentiel au calcul d'analyse de structures puisqu'il s'oppose naturellement au mouvement de la structure soumise au séisme. Il représente une stabilisation intrinsèque de la structure en régime permanent.
</div>

### VI. Effet de la projection sur base modale

<p style="text-align: justify;">   
14. On passe maintenant de la base physique vers la base modale en faisant la projection sur base à l'aide de la commande $\texttt{PROJBA}$
</div>

```gibiane
* PROJECTION DES MATRICES ET CHPOINTS
  M_P    = PJBA M    Tmode;
  K_P    = PJBA K    Tmode;
  CHA1_P = PJBA CHA1 Tmode; 
```
  
Cela revient à faire les opérations suivantes de projections :
<p style="text-align: justify;">
\begin{align*}
&\Phi^T M\Phi = M_p\\
&\Phi^T K\Phi = K_p\\
&\Phi^T F = F_p \qquad (\text{CHA1} = F)\\
\end{align*}
</div>
On obtient ainsi la nouvelle équation d'équilibre projetée sur la base modale :
<p style="text-align: justify;">
\begin{equation}
\textcolor{red}{\fbox{$
\textcolor{white}{M_p\ddot{u} + K_pu = -M_p\ddot{u}_{sol}}
$}}
\end{equation}
</div>
que l'on intègre une seconde fois via $\texttt{DYNAMIC}$

```gibiane
* INTEGRATION TEMPORELLE 
  TAB1_P = DYNAMIC TAB2_P ;
```  

ce qui revient aux calculs du système, 

  \begin{equation}
      (K_p - w^2M_p)\Phi_p = 0
  \end{equation}

<p style="text-align: justify;"> 
Les résultats sont identiques, il n'y a donc pas de pertes de précisions de calcul lors de la projection sur base modale.
</div>
<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f14.png" alt="Déplacement $u_y$ de la structure}" width="500"/>
    <figcaption>Figure 14 : Déplacement $u_y$ de la structure}
  </figure>
</div>

<p style="text-align: justify;"> 
On constate aussi que la vitesse d’exécution du programme est à peu près quatre fois plus rapide sur base modale.
</div>
<p style="text-align: justify;"> 
15. Le calcul est ensuite réalisé avec seulement deux modes. On constate que les résultats sont identiques. On en conclut qu'il suffit de prendre deux modes pour l'analyse sur base modale de la structure.
</div>

### VII. Pour aller plus loin

<p style="text-align: justify;"> 
16. Si nous fixons le paramètre $\beta$ à $15^{o}$, nous constatons que la solution en $x$ reste la même, mais selon $y$, le déplacement a augmenté de deux ordres de grandeur de plus par rapport à la configuration où la direction du séisme était uniquement selon $x$.
</div>

<div style="text-align: center;">
  <figure style="display: inline-block;">
    <img src="/assets/projet2/p2f15.png" alt="Déplacement $u_y$ de la structure}" width="500"/>
    <figcaption>Figure 15 : Déplacement $u_y$ de la structure}
  </figure>
</div>


Pour réaliser le calcul de :

<li> <p style="text-align: justify;"> 
Pour un séisme sur un bâtiment au comportement élasto-plastique endommageable, nous avons un phénomène à temps long mais sur structure au comportement non-linéaire, il faudrait plutôt utiliser la procédure PASAPAS permettant de traiter la non-linéarité de comportement.
</div>

<li>  <p style="text-align: justify;"> 
Pour un séisme sur 2 bâtiments s’entrechoquant, il faudrait combiner les deux schémas d'intégration vus dans les deux travaux pratiques, c.à.d une intégration temporelle pour traiter le phénomène rapide qui est le choc de type explicite et un deuxième schéma d'intégration pour le phénomène à temps long de type implicite.
</div>

<li> <p style="text-align: justify;"> 
Pour l'explosion sur un bâtiment endommageable, le phénomène est court mis il faudrait plutôt utiliser la procédure PASAPAS permettant de traiter la non-linéarité de comportement.
</div>

