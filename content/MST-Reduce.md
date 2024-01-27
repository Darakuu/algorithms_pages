---
tags:
  - Algoritmi
  - Algoritmi/MST
  - Algoritmi/SecondaProva
---
# MST in Grafi Sparsi

## Contrazione


> [!def] Definizione
> Una contrazione id un grafo non orientato $G=(V,E)$ è un grafo $G'=(V,E)$ tale che:
> - $V'=\{ V_{1},V_{2},\dots,V_{k} \}$ è una partizione di $V$;
> - Ciascuno dei sottografi di G indotti dagli insiemi di vertici $V_{1},V_{2},\dots,V_{k}$ è **connesso**,
> - Per ogni coppia $V_{i},V_{j} \in V'$ con $i\neq j$ si ha:
> 	- $(V_{i},V_{j})\in E' \iff (\exists\ v_{i} \in V_{i}, v_{j} \in V_{j}):(v_{i},v_{j}) \in E$

![[MST-Reduce-20240127042634398.png]]

## MST-Reduce

Dato un grafo non orientato e connesso $G=(V,E)$ con funzione peso $w:E\to \mathbb{R}$, descriveremo la procedura **MST-Reduce**, che costruisce:
- Un **Grafo Contratto** $G'=(V',E')$ con funzione peso $w'$, con $V'$ partizione di V tale che $|V'|\leq\dfrac{|V|}{2}$
- Una funzione $\textbf{orig'}:E'\to E$ tale che:
	- $((u',v')\in E\ \&\ orig'(u',v')=(u,v))\to(u \in u'\ \&\ v \in v'\ \&\ w'(u',v')=w(u,v))$
- Un insieme di archi $T\subseteq E$ tale che:
	- $(\forall\ (u_{1},u_{2})\in T) (\exists\ V_{i} \in V'),\quad u_{1},u_{2} \in V$

Tali che: 

Per ogni MST $\mathcal{A}$ di $(G',w')\implies T \cup orig'[\mathcal{A}]$ è un MST di $(G,w)$.

Cioè, per ciascun $V_i \in V'$, il sottografo di $(V,T)$ indotto da $V_{i}$ è un MST.
## MST-Reduce: Implementazione

$\text{MST-Reduce(G,orig,w,T):}$ 


```cs
foreach (v in V[G]) do:
	mark[v] = FALSE;
	MAKE-SET(v);
foreach (u in V[G]) do:
	if (mark[u] == FALSE) then:
		 scegli v in Adj[u] tale che w[u,v] è minimizzato
		 UNION(u,v);
		T = T Unito-a {orig[u,v]};
		mark[u] = mark[v] = TRUE;
V[G'] = {FIND-SET(v): v in V[G]};
E[G'] = EMPTY_SET;
foreach (x,y) in E[G] do:
	u = FIND_SET(x);
	v = FIND_SET(y);  
	if (u != v) then:
		if ((u,v) !in E[G']) then: 
			E[G'] = E[G'] Unito-a {(u,v)};
			orig'[u,v] = orig[x,y];
			w'[u,v] = w[x,y];
		else if (w[x,y]<w'[u,v]) then:
			orig'[u,v] = orig[x,y];
			w'[u,v] = w[x,y];
construct lista adiacenza Adj per G' 
return (G', orig', w', T)
```

## Complessità


wip