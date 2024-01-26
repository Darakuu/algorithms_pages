---
tags:
  - Algoritmi
  - Algoritmi/MST
  - Algoritmi/SecondaProva
---
# Distanza tra due Spanning Tree


> [!def] Distanza
> Siano $\mathcal{T_{1}}=(V,T_{1})$ e $\mathcal{T_{2}}=(V,T_{2})$ spanning tree di un medesimo grafo connesso $G=(V,E)$. 
>
> Definiamo la distanza tra $\mathcal{T_{1}}$ e $\mathcal{T_{2}}$ ponendo:
> $d(\mathcal{T_{1}},\mathcal{T_{2}}):=d(T_{1},T_{2}):=\dfrac{|T_{1}\Delta T_{2}|}{2}$ 

# Segnatura Grafo Pesato

Sia $G=(V,E)$ un grafo non orientato con un funzione peso $w:E\to \mathbb{R}$.


> [!def] Segnatura
> La Segnatura $\displaystyle\sum_{w}(G)$ è la sequenza dei pesi degli archi di $G$ in ordine non decrescente.


## Unicità della Segnatura


> [!tldr] Teorema
> Due qualunque MST di uno stesso grafo pesato non orientato e connesso hanno la medesima segnatura.

<ins>Dimostrazione</ins>

- Procediamo per assurdo:
- Sia $(G,w)$ un grafo non orientato connesso e pesato, con $G=(V,E)$ e $w:E\to \mathbb{R}$, contenente degli MST con segnature distinte
- In particolare, siano $\mathcal{T_{1}}=(V,T_{1})$ e $\mathcal{T_{2}}=(V,T_{2})$ due MST di $G$ con segnature distinte, e tali che la loro distanza $d(\mathcal{T_{1}},\mathcal{T_{2}})$ sia minima.
- Sia $e=(u,v)$ un arco di peso minimo in $T_{1}\Delta T_{2}$ senza perdita di generalità, possiamo supporre che $e$ appartenga a $T_{1}$, e non a $T_{2}$.
- Sia $(V_{1},V_{2})$ il taglio di $G$ indotto cancellando l'arco $e$ dall'MST $\mathcal{T_{1}}$
- Sia $\pi$ un cammino in $\mathcal{T_{2}}$ da $u$ a $v$, e sia $e'$ un arco in $\pi$ che attraversa il taglio $(V_{1},V_{2})\implies e' \in T_{2}\backslash T_{1}$
- Per la minimalità di $w(e)$ in $T_{1}\Delta T_{2}$, si ha $w(e)\leq w(e')$
- Pertanto, posto $T_{2}'=(T_{2}\backslash \{e'\}) \bigcup \{ e \},$ si ha che:
	- $\mathcal{T_{2}'}=(V,T_{2}')$ è uno spanning tree di $G$,
	- e
	- $w(T_{2})\leq w(T_{2}')=w(T_{2})-w(e')+w(e)\leq w(T_{2}),$
	- da cui $w(T_{2}')=w(T_{2})$ e quindi $w(e)=w(e'),$ e $w(\mathcal{T_{2}'})$ è un MST di G
- Si noti inoltre che:
	- $\displaystyle\sum_{W}(\mathcal{T_{2}'})=\sum_{W}(\mathcal{T_{2}})\impliedby w(e)=w(e')$
	- Questo perché $T_{1}\Delta T_{2}'=(T_{1}\Delta D_{2}\backslash \{ e,e' \})$
	- e quindi:
	- $d(T_{1},T_{2}')=\dfrac{|T_{1}\Delta T_{2}'|}{2}=\dfrac{|T_{1}\Delta T_{2}|}{2}-1<d(T_{1},T_{2}),$ contraddicendo la minimalità di $d(T_{1},T_{2})$
- Questa contraddizione deriva dall'aver supposto che possano esistere grafi pesati non orientati e connessi dotati di MST con segnature distinte. Pertanto il teorema risulta **dimostrato** $\qquad \blacksquare$

- Cammino $\Large\textcolor{green}{\pi}:$
- ![[MST-Segnatura-20240126211752420.png|384]]

- Visualizzazione distanze con $e'$ rimosso:
- ![[MST-Segnatura-20240126211902664.png|384]]




> [!tldr] Corollario
> Un grafo non orientato e connesso con funzione peso iniettiva ha **unico** MST

<ins>Dimostrazione</ins>

Sia  $\sigma$ la segnatura degli MST di un grafo con funzione peso iniettiva. 

Dall'iniettività di $w$ segue immediatamente che G ha un unico MST, cioè quello di segnatura $\sigma \qquad \blacksquare$

facile eh?

## Minimalità della Segnatura

