# CONVERSION D'ENERGIE

## I. Introduction

### Combinaison de sources d'énergie possibles
![alt text](image.png)
### Liste des convertisseur non inversible par combinaisons de sources d'énergie
![alt text](image-1.png)
### Rappel sur les composants d'un système de conversion d'énergie
#### Diode parfaite
![alt text](image-2.png)
#### Interrupteur commandés
![alt text](image-3.png)
#### Interrupter commandé parfait (IGBT)
![alt text](image-4.png) ![alt text](image-5.png)
#### Rapport cyclique 
$\alpha = \frac{T_{on}}{T}=\frac{\text{temps de conduction}}{\text{periode complete}}$

## II. Convertisseur continu-continu
### 1. Le hacheur série (Buck chopper)
![alt text](image-6.png)  
hypothèse : $V_S = constant$
#### 1.1. Principe de fonctionnement
La commande se fait entièrement au niveau du transistor $T_p$
![alt text](image-7.png) $T_P$ "fermé" (conduction) ![alt text](image-8.png) $T_P$ "ouvert" (non conduction)
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

![alt text](image-9.png)

- $V_s = \alpha E$
- $\langle v\rangle = \alpha E = V_s$ 
- $\Delta I_{L} = \alpha\cdot(1-\alpha)\cdot\frac{E\cdot T}{L}$ (ondulation de courant)
- Ondulation de courant maximale : $\Delta I_{L_{max}} = \frac{E\cdot T}{4L}$
- ![alt text](image-10.png)

###### Principe du filtrage de la sortie

![alt text](image-11.png)

D'après l'équation du condensateur, on a $i_C = C_s\frac{dv_s}{dt}$ donc $\frac{i_C}{C_s} = \frac{dv_s}{dt}$

![alt text](image-12.png)

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
![alt text](image-13.png)  
Donc $\langle I_L\rangle = \frac{1}{2}(\frac{E-V_s}{L}\alpha T) \Leftrightarrow \langle I_L\rangle = \frac{1}{2} \frac{\alpha(1-\alpha)\cdot E\cdot T}{L}$ OR $V_s = \alpha E$ DONC $\langle I_L\rangle = \frac{T}{2L} \cdot V_s(1-\frac{V_s}{E})$ 

Cette dernière equation est l'equation de la courbe de séparation entre le mode continu et le mode limite ($Vs,Is$)

##### mode discontinue

###### Comportement
![alt text](image-15.png)
###### Chronogrammes et valeurs à connaitres
![alt text](image-14.png)
![alt text](image-16.png)
![alt text](image-17.png)
![alt text](image-18.png)
![alt text](image-19.png)
![alt text](image-20.png)

#### Caractéristique de sortie 
![alt text](image-21.png)

#### Exemple d'utilisation d'un hacheur série :

Alimentation continue pour un processeur alimenté par une batterie.

### 2. Le hacheur parallèle (Boost chopper)
