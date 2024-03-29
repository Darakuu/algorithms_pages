---
tags:
  - Algoritmi/SecondaProva
  - Algoritmi
  - Algoritmi/MST
draft: false
---
# Strategia

Seguendo un ordine non decrescente per costi, se l'arco corrente $e$ è contenuto in un albero $\textcolor{royalblue}{blu}$ lo si colori di $\textcolor{red}{rosso}$, altrimenti lo si colori di $\textcolor{royalblue}{blu}$.


> [!example]- Esempio
> ![[Algoritmo di Kruskal-20240124015826262.png|512]]
> 
> <ins>Ordinamento</ins>
> 
> $(b,d)<(c,d)<(e,g)<(a,c)<(a,b)<(b,c)<(d,e)<(d,g)<(c,f)<(b,e)<(f,g)<(d,f)$
> 
> <ins>Colorazione</ins>
> 
> $\textcolor{royalblue}{(b,d)}<\textcolor{royalblue}{(c,d)}<\textcolor{royalblue}{(e,g)}<\textcolor{royalblue}{(a,c)}<\textcolor{red}{(a,b)}<\textcolor{red}{(b,c)}<\textcolor{royalblue}{(d,e)}<\textcolor{red}{(d,g)}<\textcolor{royalblue}{(c,f)}<\textcolor{red}{(b,e)}<\textcolor{red}{(f,g)}<\textcolor{red}{(d,f)}$

Oppure, per una strategia senza colori: ordina gli edge in ordine non-decrescente, come da pseudocodice (vedi sotto), crea un set per ogni vertice del grafo, e controlla via via in ordine di peso se due vertici sono nello stesso subset. 

Se sono in subset diversi, aggiungi l'arco nell'MST, e unisci il subset precedentemente disgiunto. 

Seguendo questo ragionamento senza sbagliare, avremo un MST corretto senza cicli.  

La riga 6 dello pseudocodice (l'istruzione *if* ) garantisce che il vertice $u$ e il vertice $v$ sono in subset diversi, garantendo appunto l'assenza di cicli.
# Correttezza

- Sia $\large w(e_{1})\leq w(e_{2})\leq\dots \leq w(e_{|E|})$ l'ordinamento per pesi utilizzato;
- Siano $\large op(e_{1}),op(e_{2}),\dots,op(e_{|E|})$ le operazione di colorazione effettuate dall'algoritmo di Kruskal.
- Procediamo per induzione su $i=1,\dots,|E|$
 

Caso: $op(e_{i})$ colora $e_{i}$ di $\textcolor{royalblue}{BLU}$: 


- Sia $e_{i}=(u_{i},v_{i})$
- Si ha che $u_{i}$ e $v_{i}$ appartengono a **due alberi blu distinti** $S_{i},T_{i}$
- Si consideri il taglio $(v[S_{i}]\ ,\ V\ \backslash \ v[S_{i}])$
- Esso è attraversato dall'arco $e_{i}$
- Si osservi che tutti gli archi $e$ tali che $w(e)<w(e_{i})$ sono già colorati.
- Pertanto $e_{i}$ ha peso minimo tra tutti gli archi non colorati che attraversano il taglio $(v[S_{i}]\ ,\ V\ \backslash \ v[S_{i}])$
- Pertanto $e_{i}$ può essere colorato da un passo $\textcolor{royalblue}{BLU}$

Caso: $op(e_{i})$ colora $e_{i}$ di $\textcolor{red}{ROSSO}$: 


- Sia $e_{i}=(u_{i},v_{i})$
- $u_{i}$ e $v_{i}$ appartengono ad **uno stesso albero blu** $T$
- Sia $\pi$ il cammino da $u_{i}$ a $v_{i}$ in $T$
- Si consideri il ciclo $\pi_{i}e_{i}$
- Tale ciclo non contiene archi rossi ed inoltre $e$ è l'unico arco non colorato
- Pertanto $e$ può essere colorato da un passo $\textcolor{red}{ROSSO}\qquad \blacksquare$


# Implementazione

Pseudocodice:

```cs title="Kruskal(G,w)"
T = EMPTY_SET();                             // T is going to be the MST
foreach (v in V)
	MAKE_SET(v)                              // create a subtree for each vertex
E = sort(E,w);                               // non-decreasing order
foreach ((u,v) in E)                         // in sorted edges...
	if (FIND_SET(u) != FIND_SET(v))          // if u and v are in different subtrees (sets), avoid cycles
		T = T U {(u,v)}                  // insert the edge inside the MST
		UNION(u,v)                       // union between the two different subtrees (sets), we're sure there are no cycles.
return T;                                    // return the MST
```

# Complessità

$\Large O(E\log V)$ 

Infatti si ha:
- $O(E\log V)$: ordinamento degli archi
- Union-Find: 
	- $|V|\quad$        MAKE_SET
	- $2|E|\quad$      FIND_SET
	- $|V|-1\quad$ UNION
	- $\underline{ \_ }_{ }\underline{ \_ }_{ }\underline{ \_ }_{ }\underline{ \_ }_{ }\underline{ \_ }_{ }\underline{ \_ }_{ }\underline{ \_ }_{ }\underline{ \_ }_{ }\underline{ \_ }_{ }\underline{ \_ }_{ }$
	- $2(|V|+|E|)-1=O(E)$ operazioni, di cui $|V|$ MAKE_SET
	- $\implies (2(|V|+|E|)-1)\propto(V)=O(E\log V) = O(E\log V)$

