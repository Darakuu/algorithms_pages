---
tags:
  - Algoritmi/StruttureDati
  - Algoritmi/PrimaProva
---
# B-Tree

I B-Tree sono alberi bilanciati di ricerca adatti per essere usati su memoria secondaria. Hanno un **fattore di ramificazione** molto alto. 

Ciò consente ai B-Tree di avere un'altezza più bassa rispetto ad altri tipi di alberi bilanciati, a parità di numero di record. 
 

>[!example]- Esempio B-Tree
>![[BTreeEsempio.excalidraw.svg]]

>[!def] Definizione di B-Tree
>Un B-Tree T è un albero con radice root\[T] che gode delle seguenti <ins>proprietà</ins>:
>1. Ciascun Nodo x ha i seguenti campi:
>	- $n[x]$, numero delle chiavi in $x$
>	- Le $n[x]$ chiavi in ordine non decrescente: $key_{1}[x]\leq\dots \leq key_{n[x]}[x]$
>	- $leaf[x]$, campo booleano tale che:
>		- $leaf[x]=\mathtt{TRUE} \longrightarrow x \text{ è una foglia }$
>		- $leaf[x]=\mathtt{FALSE} \longrightarrow x \text{ è un nodo interno}$
>2. Ciascun Nodo interno $x$ contiene $n[x]+1$ puntatori ai figli $c_{1}[x],\dots,c_{n[x]+1}[x]$
>3. Se $k_i$ denota una chiave del sottoalbero di radice $c_{i}[x]$, per $i=1,2,\dots,n[x]+1$, vale:
>	- $k_{1}\leq key_{1}[x]\leq k_{2}\leq key_{2}[x]\leq\dots \leq key_{n[x]}[x]\leq k_{n[x]+1}$
>	- Da cui segue che il B-Tree è un albero di ricerca.
>4. Tutte le foglie hanno la stessa profondità (uguale quindi all'altezza $h$ dell'albero)
>5. Il B-Tree è caratterizzato da una quantità $\textcolor{red}{t\geq 2}$, detta $\mathtt{\textcolor{red}{Grado\ Minimo}}$, tale che:
>	- tutti i nodi, eccezion fatta per la radice, devono contenere **ALMENO** $\textcolor{red}{t-1}$ chiavi.
>	- tutti i nodi devono contenere al più $\textcolor{red}{2t-1}$ chiavi.
>	- Un nodo che contiene $2t-1$ chiavi si dice **PIENO**
>	- Cioè deve valere: $t-1\leq n[x]\leq 2t-1$








