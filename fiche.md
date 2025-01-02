# CONVERSION D'ENERGIE

## I. Introduction

### Combinaison de sources d'énergie possibles
![alt text](img/image.png)
### Liste des convertisseur non inversible par combinaisons de sources d'énergie
![alt text](img/image-1.png)  
Les "voltage receivers" sont les charge inductives et les "current receivers" sont les charges capacitives.  
On peut former une source de courant en associant une source de tension à une inductance et une source de tension en associant une source de courant à une capacité.
### Rappel sur les composants d'un système de conversion d'énergie
#### Diode parfaite
![alt text](img/image-2.png)
#### Interrupteur commandés
![alt text](img/image-3.png)
#### Interrupter commandé parfait (IGBT)
![alt text](img/image-4.png) ![alt text](img/image-5.png)
#### Rapport cyclique 
$\alpha = \frac{T_{on}}{T}=\frac{\text{temps de conduction}}{\text{periode complete}}$

## II. Convertisseur continu-continu

### 1. Le hacheur série (Buck chopper)
![alt text](img/image-6.png)  
hypothèse : $V_S = constant$
#### 1.1. Principe de fonctionnement
La commande se fait entièrement au niveau du transistor $T_p$
![alt text](img/image-7.png) $T_P$ "fermé" (conduction) ![alt text](img/image-8.png) $T_P$ "ouvert" (non conduction)
#### 1.2. Modes de fonctionnement
Déterminés en fonction des valeurs de $i_L$
- Mode continu : $i_L > 0$
- Mode discontinu : $i_L(t_0) = 0$ avec $t_0 < T$

##### Mode continu
###### Pour $0<t<\alpha T$
D'après l'equation de l'inductance $u_L = L\frac{di_L}{dt}$
D'après la loi des mailles $v = u_L + V_s$ or $v = E$ car la diode est bloquée DONC : $u_l = v-V_s = E-V_s$ 
Finalement : $\frac{di_L}{dt} = \frac{E-V_s}{L}$

Sachant que i_L > 0, on a $E>V_s$ DONC : $\frac{di_L}{dt} > 0$.

$i_L$ est de la forme d'une rampe croissante.

###### Pour $\alpha T<t<T$
$E=0$ car le transistor est bloquant. La relation reste la même que précemment DONC : $\frac{di_L}{dt} = \frac{-V_s}{L}$

Sachant que $V_s > 0$, on a $\frac{di_L}{dt} < 0$.

$i_L$ est de la forme d'une rampe decroissante.

###### Chronogrammes et valeurs à connaitres 

![alt text](img/image-9.png)

- $V_s = \alpha E$
- $\langle v\rangle = \alpha E = V_s$ 
- $\Delta I_{L} = \alpha\cdot(1-\alpha)\cdot\frac{E\cdot T}{L}$ (ondulation de courant)
- Ondulation de courant maximale : $\Delta I_{L_{max}} = \frac{E\cdot T}{4L}$
- ![alt text](img/image-10.png)

###### Principe du filtrage de la sortie

![alt text](img/image-11.png)

D'après l'équation du condensateur, on a $i_C = C_s\frac{dv_s}{dt}$ donc $\frac{i_C}{C_s} = \frac{dv_s}{dt}$

![alt text](img/image-12.png)

$t_1$ et $t_2$ sont les temps auquel le courant $i_c$ est nul, donc à des extremum de $v_s$.

$$\begin{align*}
\begin{cases}
  t_1 = \alpha\frac{T}{2} \\
  t_2 = (1+\alpha)\frac{T}{2}
\end{cases}
\end{align*}$$

Pour obtenir $\Delta V_{s}$, on intègre $\frac{i_C}{C_s}$ entre $t_1$ et $t_2$. On a donc $\Delta V_{s} = \frac{1}{C_s}\int_{t_1}^{t_2}i_Cdt$ puis $\Delta V_{s} = \frac{1}{C_s}\int_{t_1}^{t_2}\frac{\Delta I_L}{2}dt$. On obtient donc que $\Delta V_{s} = \frac{\Delta I_L T}{8C_s}$.

Avec cette formule et en replaçant $\Delta I_L$ par sa formule, on obtient que $C_s=\frac{\alpha(1-\alpha)ET²}{8.L.\Delta V_s}$.

##### Mode limite
$i_L(T)=0$  
![alt text](img/image-13.png)  
Donc $\langle I_L\rangle = \frac{1}{2}(\frac{E-V_s}{L}\alpha T) \Leftrightarrow \langle I_L\rangle = \frac{1}{2} \frac{\alpha(1-\alpha)\cdot E\cdot T}{L}$ OR $V_s = \alpha E$ DONC $\langle I_L\rangle = \frac{T}{2L} \cdot V_s(1-\frac{V_s}{E})$ 

Cette dernière equation est l'equation de la courbe de séparation entre le mode continu et le mode limite ($Vs,Is$)

##### mode discontinue

###### Comportement
![alt text](img/image-15.png)
###### Chronogrammes et valeurs à connaitres
![alt text](img/image-14.png)
![alt text](img/image-16.png)
![alt text](img/image-17.png)
![alt text](img/image-18.png)
![alt text](img/image-19.png)
![alt text](img/image-20.png)

#### Caractéristique de sortie 
![alt text](img/image-21.png)

#### Exemple d'utilisation d'un hacheur série :

Alimentation continue pour un processeur alimenté par une batterie.

### 2. Le hacheur parallèle (Boost chopper)
![alt text](img/image-23.png)
#### 2.1. Principe de fonctionnement
![alt text](img/image-24.png)
#### 2.2. Modes de fonctionnement
- Mode continu : $i_L > 0$
- Mode limite : $i_L(T) = 0$
- Mode discontinue : $i_L(t_0) = 0$ avec $t_0 < T$
##### Mode continu
![alt text](img/image-25.png)
###### Pour $0<t<\alpha T$

D'après l'equation de l'inductance $u_L = L\frac{di_L}{dt}$

D'après la loi des mailles $E= u_L$ car $v=0$ DONC : $\frac{di_L}{dt} = \frac{E}{L}$

Sachant que i_L > 0, on a $\frac{di_L}{dt} > 0$. Donc, $i_L$ est de la forme d'une rampe croissante.

Concernant $v$, on a $v = 0$ car le transistor est passant.

###### Pour $\alpha T<t<T$

D'après la loi des mailles $E = u_L + v$ OR $v= V_S$ car le transistor est bloquant DONC : $u_L = E - V_S$

On a donc $\frac{di_L}{dt} = \frac{E-V_S}{L}$. Donc, $i_L$ est de la forme d'une rampe decroissante.

Dans tous les cas, $E<V_S$. Donc, on a bien boosté la tension.

###### Chronogrammes

![alt text](img/image-27.png)

###### Calcul de V_S

On a $V_S = \frac{E}{1-\alpha}$  
![alt text](img/image-26.png)

###### Calcul de l'ondulation de courant

![alt text](img/image-28.png)  
$\Delta I_L = \alpha\frac{E\cdot T}{L}$ et $\Delta I_{L_{max}} = \frac{E\cdot T}{L}$ ($\alpha = 1$)

###### filtrage de la sortie

![alt text](img/image-29.png) ![alt text](img/image-30.png) ![alt text](img/image-31.png)  
$\Delta V_S = \frac{E T}{R_S C_S}\frac{\alpha}{1-\alpha}$

##### Mode limite
![alt text](img/image-32.png)  
$I_S=\langle i_D\rangle=\frac{1}{2}I_{L_{max}}(1-\alpha)=\frac{ET}{2L}\alpha(1-\alpha)$  
$V_S=\frac{E}{1-\alpha}$  
$I_s = \frac{ET}{2L}\frac{E}{V_s}(1-\frac{E}{V_s})$

##### Mode discontinue
###### Comportement
![alt text](img/image-33.png)  
###### Chronogrammes
![alt text](img/image-34.png) ![alt text](img/image-35.png)

##### Caractéristique de sortie
![alt text](img/image-36.png)

### 3. Hacheurs reversibles

![alt text](img/image-37.png)  
Comportement du hacheur fonction du nombre de quadrant

#### 3.1. Hacheur 2 quadrants reversibles
![alt text](img/image-38.png)  
##### Commande
Comme il ya 2 Interrupteur commandés, il faut 2 rapport cycliques, tel que $\alpha_1+\alpha_2 = 1$  
De plus, quand l'un est passant, l'autre est bloquant. On a donc le Chronogramme suivant :  
![alt text](img/image-39.png)
##### Tension de sortie
![alt text](img/image-40.png)
##### Courant de sortie

###### Seulement le premier quadrant

![alt text](img/image-41.png)

###### Seulement le deuxième quadrant

![alt text](img/image-42.png)

###### Les 2 quadrants : Chronogramme complet

![alt text](img/image-43.png)

##### Caractéristique de sortie

![alt text](img/image-44.png)


#### 3.2. Hacheur 4 quadrants

![alt text](img/image-45.png)

##### Commande complémentaire synchrone

###### Fonctionnement et Chronogrammes
On a 4 interrupteurs commandés, donc 4 rapport cycliques, tels que : 

$$
\begin{cases}
  \alpha_1 = \alpha_4 \\
  \alpha_2 = \alpha_3 \\
  \alpha_1 + \alpha_2 = 1
\end{cases}
$$  

Et les periodes d'ouverture et fermeture dee transistors suivantes :  
![alt text](img/image-46.png)

Ce qui nous donne les Chronogrammes et la circulation de courant suivante : 
![alt text](img/image-47.png) ![alt text](img/image-48.png)

###### Tension de sortie moyenne

$\langle u \rangle = (2\alpha-1)E$ avec $\alpha =\alpha_1$.

Lorsque la frequence de commande est faible, l'ondulation en tension est de $2*E$.

###### Characteristique de sortie

![alt text](img/image-49.png)

###### Controle d'un moteur à courant continu

![alt text](img/image-50.png)

Le convertisseur est bien reversible : dans un sens, la source genere un mouvement du moteur, dans l'autre le moteur agit comme un générateur.

![alt text](img/image-51.png)  
Ici, ses cycles de fonctionnement.  
![alt text](img/image-52.png)  
Et ici les points de fonctionnement.  

##### Commande additionnelle

![alt text](img/image-54.png)  
$U = \plusmn \alpha E$ valeur moyenne durant une periode de commande $T_d$.  
Les ondulations en tensions sont reduites et valent $E$. De plus, ne switchet que sur $T_1$ ou $T_3$ reduit les pertes. Cependant, on constate des instabilités autour de 0 v

##### commande complémentaire décalée

Ici, on a : 
$$
\begin{cases}
  \alpha_1 = \alpha_4 \\
  \alpha_2 = \alpha_3 \\
  \alpha_1 + \alpha_3 = 1 \\
  \alpha_2 + \alpha_4 = 1
\end{cases}
$$

Ainsi, on switch sur $T_1$ et $T_3$ à $t=0$ et  $T_2$ et $T_4$ à $t=T/2$, comme montré ici : 

![alt text](img/image-56.png)

Donc, on a :
$U=(2\alpha-1)E$ et $\Delta U = E$ pour des grande frequence de commande, ce qui nous donne un signal PWM.

##### Moteur pas à pas

POur controler un moteur pas à pas, on utiliser 2 hacheurs 4 quadrants, comme ici : 

![alt text](img/image-61.png)

###### Tour complet
![alt text](img/image-60.png)

###### Demi-tour
![alt text](img/image-59.png)


### 4. Inverseurs

#### 4.1. inverseur 1 phase

![alt text](img/image-62.png)  
Avec un rapport cyclique de  : $\alpha = \frac{1}{2} + \delta_{\alpha}\sin(\omega t)$

![alt text](img/image-63.png)

#### 4.2. inverseur 3 phases

![alt text](img/image-64.png)

permet dalimenter des moteurs continues brushless trisphasés.

![alt text](img/image-65.png)

### 5. Hacheurs à boucle fermée
![alt text](img/image-66.png)

permet de controler la vitesse ou le couple <=> la tension ou le courant.

On rappelle le modèle mathématique/physique du moteur à courant continu :

$$
\begin{cases}
  \text{Equations electrique :}& u= e + r\cdot i + L\frac{di}{dt} \\
  \text{Equations mecanique :}& J \frac{d\Omega}{dt} + f\cdot \Omega = \Gamma_m - \Gamma_r \\
  \text{Equations de couplage :}& \begin{cases}
    \Gamma_m = K_{\phi}\cdot i \\
    e = K_{\phi}\cdot \Omega
  \end{cases}
\end{cases}
$$

On note egalement 2 constantes de temps : 

$$
\begin{cases}
  \text{constante de temps electrique :} & \tau_e = \frac{L}{R} \\
  \text{constante de temps electro-mag :} & \tau_{em} = \frac{JR}{k_{phi}^2 + Rf}
\end{cases}
$$

Le moteur est aproximé electriquement par un circuit RC serie : 
![alt text](img/image-67.png)  
Et se se représente sous la forme d'un schema bloc comme suit :  
![alt text](img/image-68.png)

#### 5.1 Application à un moteur à courant continu

##### Structure réversible

![alt text](img/image-69.png)

##### Modèle du hacheur
![alt text](img/image-70.png)
 
#### 5.2. Controle du courant

![alt text](img/image-71.png) 

##### boucle de courant 

###### Propriétés
Régulation du courant d'armature permet :
- Une regulation du courant
- un controle du couple
- une meilleure reponse transient
- regulation simple (PI)
Mais necessite a capteur de haute performance.

###### Capteur de courant

Resistance de shunt + Capteur à effet Hall

###### Schema bloc et fonction de transfert

![alt text](img/image-72.png) ![alt text](img/image-73.png)

###### Schema 

![alt text](img/image-74.png)

###### Critères de controle

- Accuracy : pas d'erreur statique
- Rapidité : temps de réponse court
- Stabilité non conditionnelle : grande marge

##### Schema bloc et fonction de transfert

![alt text](img/image-76.png)

On choisi un controller PI

![alt text](img/image-77.png)

##### Hacheur de premier ordre 

![alt text](img/image-78.png)

![alt text](img/image-79.png)

#### 5.3. Controle de la vitesse/ fonction de transfert de tension

##### Schema bloc et FT

![alt text](img/image-80.png)

##### Schema synoptique

![alt text](img/image-81.png)

#### 5.4. Combinaison : boucles imbriquées

![alt text](img/image-82.png)


### 6. Hacheurs indirects : hacheurs basé sur le stockage d'energie

#### 6.1. Buck-Boost : hacheur à stockage inductif
![alt text](img/image-83.png)  

##### Schema
![alt text](img/image-84.png)

##### Mode de fonctionnement

- Mode continu : $i_L > 0$
- Mode limite : $i_L(T) = 0$
- Mode discontinue : $i_L(t_0) = 0$ avec $t_0 < T$

###### Mode continu

![alt text](img/image-85.png)
![alt text](img/image-86.png)
![alt text](img/image-87.png)
![alt text](img/image-88.png)
![alt text](img/image-89.png)
![alt text](img/image-90.png)

##### Mode limite

![alt text](img/image-91.png)
![alt text](img/image-92.png)

##### Mode discontinue

![alt text](img/image-93.png)![alt text](img/image-94.png)

![alt text](img/image-95.png)

##### Caractéristique de sortie

![alt text](img/image-96.png)

#### 6.2. Cuk : hacheur à stockage capacitif

![alt text](img/image-97.png)

##### Schema

![alt text](img/image-98.png)

##### Mode de fonctionnement : continue ($U_c > 0$)

![alt text](img/image-99.png)
![alt text](img/image-100.png)

###### Chronogrammes

![alt text](img/image-101.png)

###### Caractéristique de transfert

![alt text](img/image-102.png)


#### 6.3. SEPIC

![alt text](img/image-103.png)

##### Mode continu 

###### Transfert de tension

![alt text](img/image-104.png)

###### Condensateur de couplage

![alt text](img/image-105.png)

