---
title: Home
layout: home
---
# Optimització

## Taller Nous Usos de la Informàtica

<h1><img width="150"  src="https://i.imgur.com/vvZMy0I.png"></h1>

---

## Que és l'optimització?

En matemàtiques, estadística, ciències de la computació o economia, el concepte d'**optimització** correspon al procés de selecció del **millor element** (o conjunt d'elements), respecte d'un **criteri** determinat (amb o sense restriccions), entre un conjunt d'elements disponibles.

Moltes vegades, els problemes d'optimització es redueixen a la cerca del màxim (o el mínim) d'una funció que representa el criteri.
<center><img width="350"  src="https://i.imgur.com/LFrS302.png"></center>

---

### Mètodes clàssics

+ Per funcions unimodals contínues amb un únic punt extrem, podem usar mètodes basats en la derivada (o el gradient). En aquest cas tenim certes garanties sobre la solució trobada.
+ Per funcions multimodals contínues podem usar mètodes estocàstics basats en les derivades, però les garanties sobre la solució trobada es relaxen. 
+ Per funcions discretes o amb valors enters, hi ha mètodes específics.
+ També hi ha mètodes estocàstics que poden servir per qualsevol tipus de funció. Per exemple, algorismes genètics. 


---

### Les dades

Durant tot aquest curs representarem els **conjunts de dades** de $m$ elements en forma matricial, amb valors definits sobre $n$ **característiques**:

<center><img width="450"  src="https://i.imgur.com/jQvsA9K.png"></center>



Suposem de moment que totes les característiques de les dades són numèriques (hi ha mètodes per transformar-les a numèriques quan no ho són).

---

### Quina és la relació entre optimització i dades?

L'objectiu de molts mètodes d'anàlisi de dades és convertir aquesta matriu de dades en un **model**.

Un **model** és una expressió matemàtica $f_w$ que depen d'uns quants paràmetres $w$ i que representa fidelment i de forma compacte algun aspecte de la matriu de dades.

---

### Exemple

Suposem que les nostres dades representen els pisos de Barcelona amb dues característiques, els metres quadrats ($X$) i el preu de venda d'aquests pisos ($Y$).

<center><img width="450"  src="https://i.imgur.com/AV8Qv6U.png"></center>



---

### Exemple

Enlloc de tenir una gran taula $D$ amb moltes files, podriem buscar una funció linial , $y=ax+b$, que només depen de 2 paràmetres $a$ i $b$, que representi el preu en funcio dels metres quadrats.

Aquest model pot ser útil per moltes coses perquè pot **predir** el preu d'un pis qualsevol. 

Evidentment, a la realitat, per trobar un bon model, cal que $X$ representi tots els aspectes relacionats amb el preu d'un pis: barri, alçada, carrer, habitacions, etc, i per tant el model ha de tenir més paràmetres.

Els mètodes d'optimització serveixen per buscar els valors dels paràmetres que minimitzen els errors de representació del model!

---

### Quina és la relació entre optimització i dades?

Per fer-ho seguirem aquest mètode:
+ Definirem una familia de funcions, el **model**,  que pugui representar el conjunt de dades. En el nostre exemple triem una funció linial $f(x)$ d'una característica $y = ax+b$. 
+ Llavors definirem una funció que **mesuri l'error** que cometem al representar cada fila de la matriu de dades amb aquest model, $(a x_i + b - y_i)^2$, on $x_i, y_i$ són dades de la fila $i$ que representen els $m^2$ i el *preu* del pis $i$. 
+ Sumarem tots els termes per obtenir un valor $L(f)$ que representa la "qualitat" del model $f$:

$$
L(f) = \sum_{i \in D} (a x_i + b - y_i)^2
$$

---

### Quina és la relació entre optimització i dades?

<center><img width="450"  src="https://i.imgur.com/mFQYqSz.png"></center>


---


### Quina és la relació entre optimització i dades?

+ Finalment, usarem un algorisme d'optimització per trobar els paràmetres $a$ i $b$ òptims, és a dir, els que fan que $L$ sigui el més petit possible:

$$
\arg_{min}^{(a,b)} \sum_{i \in D} (a x_i + b - y_i)^2
$$

---

### Quina és la relació entre optimització i dades?



Aquest **model** representa el conjunt de dades des del punt de vista que si sabem els metres quadrats, podem obtenir el preu (aproximat) aplicant una fòrmula, sense necessitat de tenir la taula.


:::info
:bulb: També podriem fer un model per predir els $m^2$ a partir del preu, o directament modelar $f(x,y)$. 
:::

---

### Optimització i aprenentatge de dades


:::info
:bulb: **Compte!** Aplicar un algorisme d'optimització directament pot ser perillós: podem trobar un model que aproximi molt bé les dades i que predigui el preu d'un pis que no està al conjunt de dades molt malament. 
:::

<center><img width="450"  src="https://i.imgur.com/mgCmcoW.png"></center>

Aquest fenòmen es diu sobre-estimació (*overfitting*). Si l'objectiu del nostre model no és simplement **representar** el conjunt de dades sinó que volem **generalitzar** (predir el valor de dades $x$ que no estan al conjunt d'aprenentatge), ho hem de controlar!

---

### Optimització i aprenentatge de dades

En general **aprendre de les dades** vol dir **inferir** (construir de baix cap a dalt, de les dades cap el model) un model que ens permet representar-les de forma **compacte** i/o ens permet **generalitzar** el seu comportament (extrapolar).


+ En el primer cas, donat un conjunt de dades $\{\mathbf x_i\}_{i=1,\dots,n}$, volem construir un funció $f$ tal que $\mathbf y_i = f(\mathbf x_i)$ és una representació *compacta* (més simple, de menys dimensions, etc.) de $\mathbf x_i$. 
    + Exemple: $\mathbf x_i$ són les estadístiques de les paraules que apareixen en un llibre (moltes dimensions!) i $f(\mathbf x_i)$ és un model lineal que produeix un vector de dimensió 200 que representa adequadament el llibre des del punt de vista de les seves "propietats". 

---


### Optimització i aprenentatge de dades

+ En el segon cas, donat un conjunt de dades etiquetades $\{\mathbf x_i,y_i\}_{i=1,\dots,n}$, volem construir un funció $f$ tal que quan rebem una nova dada $\mathbf x_j$, no vista anteriorment, el càlcul de $\mathbf y_j = f(\mathbf x_j)$ és **probablement correcte**. 
    + Exemple: $\mathbf x_j$ és un nou llibre que acaba de sortir i volem determinar el seu gènere. 

---


### Optimització i aprenentatge de dades

La solució del problema de la sobre-estimació és usar una metodologia d'aprenentatge adequada durant l'optimització: la validació encreuada (*cross-validation*).

Aquest consisteix a dividir en dos subconjunts complementaris el conjunt de dades $D$, avaluant el model sobre un subconjunt (anomenat dades d'entrenament o *training set*), i validant-lo en l'altre subconjunt (anomenat dades de prova o *test set*).

El model només s'ajusta amb el conjunt de dades d'entrenament i a partir d'aquí calcula els valors de sortida per al conjunt de dades de prova (valors que no ha analitzat abans). Si el resultat sobre les dades de prova no és prou bó, hem de canviar la familia del model!


---

### Optimització i aprenentatge de dades

Una gran part dels algorismes que "aprenen" de les dades estan basats en la resolució (iterativa) d'un problema matemàtic que construeix un model $f$ a partir de les dades seguint els passos que hem vist abans i per tant minimitzant:

$$
\arg_{min}^{w} \sum_{i \in D} (f_w(x_i) - y_i)^2
$$

on $w$ són els paràmetres del model $f$.

Si existís una solució directa (no iterativa) que derivés la fòrmula de la solució, adopatariem aquesta estratègia, però no és el cas...

La metodologia més emprada per resoldre aquest problema és el **descens del gradient** sobre la funció $\sum_{i \in D} (f_w(x_i) - y_i)^2$.

---
