---
tags:
  - Algoritmi
  - Algoritmi/SecondaProva
  - Algoritmi/ShortestPath
---
# Cammini Minimi in un Grafo

- Si tratta di uno dei problemi di ottimizzazione su grafi più importante e più studiato.

## Richiami di Definizioni

- $V:$ insieme finito di nodi;
- $E:\subseteq V\times V$ tale che $(v,v)\not\in E$ per ogni $v \in V$;
- La coppia $G=(V,E)$ è un grafo orientato:
	- $V$ è l'insieme dei nodi di G,
	- $E$ è l'insieme degli archi di G.
- Sia $w:E\to \mathbb{R}$ una funzione peso o costo $\implies (G,w)$ si dice grafo pesato. 

### Matrice di Adiacenza

- Dato $G=(V,E)$ con $V=\{ 1,2,\dots,n \}$ la matrice di adiacenza associata a G è la matrice A di dimensioni $n\times n$ tale che:

$$
\begin{equation}
A_{ij}=
\begin{cases}
 1 \quad se\ (i,j)\in E\\
\qquad\qquad \qquad\qquad\quad O(V^2) \\
0\quad altrimenti
\end{cases}
\end{equation}
$$

### Liste di Adiacenza

- Dato $G=(V,E)$ le liste di adiacenza associate a G sono gli insiemi $Adj_{G}(u)=\{ v \in V : (u,v) \in E \}$.

### Cammini

- Sia $G=(V,E)$ un grafo con funzione peso $w: E\to \mathbb{R}$
- Siano $u,v \in E$. un **Cammino** da $u$ a $v$ è una sequenza $\pi=(v_{0},v_{1},\dots ,v_{k})$ di nodi contigui di G, cioè tale che:
	- $v_{0}=u,v_{k}=v$
	- $(v_{i-1},v_{i})\in E,\quad \text{per}\ i=1,2,\dots,k$
- Si usa anche la notazione $v_{0}\to v_{1} \to\dots\to v_{k}$

Poniamo:
- $w(\pi)=\displaystyle\sum^k_{i=1}w(v_{i-1},v_{i})$ Peso del cammimo $\pi$;
- $length(\pi)=k$
- $head(\pi)=v_{0}$
- $tail(\pi)=v_{k}$

Poniamo inoltre:
- PATHS(G) = Insieme di tutti i cammini in G;
- PATHS(G; u) = insieme di tutti i cammini in G che iniziano da u;
- PATHS(G; u, v) = insieme di tutti i cammini in G che iniziano da u e terminano in v;

### Concatenazione di Cammini

- Siano $\pi_1=(v_{0},v_{1},\dots,v_{k})$ e $\pi_2=(v_{k},v_{k+1},\dots,v_{\mathcal{l}})$ due cammini tali che $head(\pi_{2})=tail(\pi_{1})$.
- Scriviamo $\pi_{1};\pi_{2}$ per indicare la concatenazione tra i due cammini.
- Ovviamente il peso del cammino concatenato è la somma dei pesi dei due cammini.

### Distanza

- Poniamo $\delta(u,v)=inf\  \{ w(\pi):\pi \in PATHS(G;u,v) \}$
	- con $inf\ \emptyset=+\infty$


# Cammini Minimi

- Un cammino è minimo se $w(\pi)=\delta(u,v)$


> [!def] Un Grafo ammette cammini minimi se:
> $\delta(u,v)\neq-\infty,\ \forall\ u,v \in V$


> [!tldr] Lemma
> Un grafo ammette cammini minimi se e solo se ammette cammini minimi da ciascuno dei suoi nodi



> [!tldr] Lemma: Condizione necessaria e sufficiente per cammini minimi
> Non vi deve essere alcun ciclo di peso negativo raggiungibile da una sorgente s

<ins>Dimostrazione: Necessità</ins>

Se da s è possibile raggiungere un ciclo $\gamma$ di peso negativo da $v \text{ a } v$, allora:

- $PATHS(G;s,v) \supseteq \{ \pi;(\gamma)^k : k\geq0 \}$

Ma: 
- $inf(w(PATHS(G;s,v)))\leq inf(w(\{ w;(\gamma)^k :\mathbf{k}\geq 0\})) =-\infty$

Quindi G non ammette cammini minimi da s.

<ins>Dimostrazione: Sufficienza</ins>

Supponiamo che da s non sia raggiungibile alcun ciclo di peso negativo. 

Per ogni $v$ poniamo:

$\text{SIMPLE\_PATHS}(G;s,v)=\{ \pi \in PATHS(G;s,v) : \pi \text{ SEMPLICE} \}$ 


è facile verificare che: 

$(\forall\ \pi \in PATHS(G;s,v))(\exists\ \pi' \in SIMPLE\_PATHS(G;s,v)), w(\pi')\leq w(\pi)$

E quindi l'estremo inferiore del peso tra SIMPLE_PATHS e PATHS è uguale. Poiché SIMPLE_PATHS è finito, siamo sicuri che non sarà mai uguale a $-\infty$, da cui:

$\delta_{G_{s}}(v)\neq-\infty$

Data l'arbitrarietà di $v$, concludiamo che G ammette cammini minimi da s.

- Corollario 1

Condizione necessaria e sufficiente perché un grafo pesato (G,w) ammetta cammini minimi è che non contenga alcun ciclo di peso negativo.

- Corollario 2

Ogni grafo con funzione peso non negativa ammette sempre cammini minimi.

- Corollario 3

Ogni grafo aciclico ammette sempre cammini minimi

## Sottostruttura Ottima

Sia $(\pi=v_{0},v_{1},\dots v_{k})$ un cammino minimo in (G,w). 

Allora il sottocammino $\pi_{ij}=(v_{i},v_{i+1},\dots,v_{j})$ per ogni $0\leq i\leq j\leq k$ è minimo.

# Cammini minimi da una singola sorgente

- Sia (G,w) un grafo pesato, con $s \in V$ sorgente assegnata, e supponiamo che (G,w) ammetta cammini minimi da $s$.
- Vogliamo memorizzare in maniera spazialmente efficiente un cammino minimo da s. 
	- La soluzione ingenua consiste nel memorizzare O(n) liste di lunghezza O(n) ciascuna $\implies O(n^2)$

## Grafo dei Cammini Minimi

- Sia MIN_PATHS(G;s) l'insieme di tutti i cammini minimi da s in G;
- Sia $E'_{s}$ l'insieme di tutti gli archi contenuti in qualche cammino minimo da s
- Chiamiamo il grafo $G'_{s}=(V,E_{s}')$ grafo dei cammini minimi da s in G


> [!success] Esempio

![[Cammini Minimi-20240127201648540.png]]

### Proprietà: 

MIN_PATHS(G;s) $\neq \emptyset \implies$ PATHS($G'_{s};s$) = MIN_PATHS(G;s)

<ins>Dimostrazione</ins>

wip

## Albero di Cammini Minimi

 - Sia (G,w) un grafo pesato, con $s \in V$ sorgente assegnata, e supponiamo che (G,w) ammetta cammini minimi da $s$.

Allora esiste un albero $G''_{s}=(V'',E_{s}'')$, con $V''\subseteq V$ e $E_{s}''\subseteq E$ radicato in s e contenente **esattamente** un cammino minimo in G da s per ciascun nodo $v \in V$ raggiungibile da s in G.

<ins>Dimostrazione</ins>

Basta effettura una visita, DFS o BFS, da $s$ nel grafo dei cammini minimi $G_{s}'=(V,E_{s}')$.

Complessità Spaziale: $O(n)$

> [!success] Esempio

![[Cammini Minimi-20240128005324454.png]]

## Alberi di Cammini Minimi in Grafi non orientati e MST

Dato un grafo non orientato $G=(V,E)$ con funzione peso $w: E\to \mathbb{R}$ e sorgente $s \in V$, non è necessariamente vero che tra i suoi alberi di cammini minimi da s ci debba essere un MST di (G,w).

(wip)

# Further reading

- [[Algoritmi per calcolo distanza e dei cammini minimi da una data sorgente]]
- [[Cammini minimi tra tutte le coppie di nodi]]
- [[Superare la complexity barrier]]