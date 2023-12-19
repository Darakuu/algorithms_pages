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

# Teorema: Altezza B-Tree

>[!def] L'Altezza h di un B-Tree $T$ di grado minimo $t$ contenente $n$ chiavi, con $n \geq 1$, soddisfa:
>$$ h \leq \log_{t} \dfrac{n+1}{2} $$

$\Large n_{h}\leq n\leq N_{h}$

| livello | \#nodi   | \#chiavi                               |
|:-------:|:--------:|:--------------------------------------:|
|       0 |        1 |                                      1 |
|       1 |        2 | $2(t-1)$                               |
|       2 | $2t$     | $2t(t-1)$                              |
|       3 | $2t^2$   | $2t^2(t-1)$                            |
| ...     | ...      | ...                                    |
| i       | 2t^{i-1} | $2t^{i-1}(t-1)$                        |
| ...     | ...      | ...                                    |
| h       | 2t^{h-1} | $\underbrace{ 2t^{h-1}(t-1) }_{n_{h}}$ |  


![[Pasted image 20231219004511.png|768]]


## Dimostrazione


$$

\begin{align}
n_{h} & = 1+2(t-1)\displaystyle\sum^h_{i=1}t^{i-1} \\
& = 1+2(t-1)\sum^{h-1}_{j=0}t^j \\
& =1+2(\cancel{ t-1 })\cdot \dfrac{t^{h-1}}{\cancel{ t-1 }} \\
& = 1+2t^h-2
\end{align}

$$

Risolviamo per h:

$$
\begin{align}
& n_{h}\leq n \\
& 2t^h-1\leq n \\
& t^h \leq \dfrac{n+1}{2} \\
& \boxed{\textcolor{red}{h \leq\log_{t}\dfrac{n+1}{2}}}
\end{align}
$$
>[!warning] Questa dimostrazione risponde alla domanda:
>"Si fornisca (con dimostrazione) un limite superiore per l’altezza di un B-tree di grado minimo t con n chiavi."


## Con nodi pieni:

![[Pasted image 20231219005231.png|768]]

| livello | \#nodi   | \#chiavi                               |
|:-------:|:--------:|:--------------------------------------:|
|       0 |        1 |                                      2t-1 |
|       1 |        2t | $2t(2t-1)$                               |
|       2 | $(2t^2)$     | $2t^2(2t-1)$                              |
|       3 | $(2t^3)$   | $2t^3(2t-1)$                            |
| ...     | ...      | ...                                    |
| h       | (2t)^{h} | $\underbrace{ 2t^{h}(2t-1) }_{N_{h}}$ |  


Si procede come prima. 


$$
\begin{align}
N_{h} & = (2t-1)\displaystyle\sum^h_{i=0}(2t)^i \\
& =(2t-1) \cdot \dfrac{(2t)^{h+1}-1}{2t-1} \\
& =(2t)^{h+1}-1
\end{align}
$$

Risolviamo nuovamente per h: 


$$
\Large
\begin{align} 
 n & \leq N_{h} \\
 n & \leq 2t(h+1)-1 \\
 n+1 & \leq(2t)^{h+1} \\
 h+1 & \geq lg_{2t}(n+1) \\
 h & \geq \log_{2t}(n+1)-1 \\
 h & \geq \log_{2t}\dfrac{n+1}{2t}
\end{align}
$$

Il -1 entra nel logaritmo dividendo per 2t. 


Perciò, infine, otteniamo: 


$\Large\log_{2t}\dfrac{n+1}{2t}\leq h\leq lg_{t}\dfrac{n+1}{2}$ 

$\Large h=\Theta(\log n)$

# Operazioni di Base sui B-Tree

## Search

x punta alla radice, k è la chiave cercata. 


## Create

...

## Inserimento Key

Procedura naturale: Due possibili passate. 

- Si effettua la ricerca per trovare la foglia in cui inserire k;
- Se tale foglia non è piena, si inserisce k nel posto opportuno.
- Altrimenti, si spezza la foglia piena:

![[Pasted image 20231219012754.png|512]]

Si spezzano i nodi durante la discesa. 


>[!example]- Esempio
>BTree di grado minimo: t = 3, max: 2t-1 = 5 
>![[Pasted image 20231219012848.png|512]]
>![[Pasted image 20231219013020.png|512]]
>![[Pasted image 20231219013222.png|512]]

## Cancellazione Key

Procedura naturale: due possibili passate sempre. 


- Si effettua la ricerca per trovare il nodo che contiene la chiave k;
- Se tale nodo è una foglia con almeno t chiavi (cioè non è magro), si cancella direttamente.
- Se invece la foglia è magra, si farà cedere una chiave da una foglia sorella (se possibile).
	- Se non è possibile, dal nodo padre, contestualmente unendosi a una foglia sorella.
	- Tale processo potrebbe propagarsi fino alla radice.
- Se il nodo che contiene k è invece un nodo interno, si sostituisce k con la chiave immediatamente più piccola (o più grande) di k, e si cancella il predecessore (o il successore) di k, che risiederà sicuramente su una foglia.
- Per evitare la possibile risalita si farà in modo che i nodi sul cammino dalla radice al nodo contenente k NON siano magri (eccezion fatta per la radice);
- Pertanto, supponiamo che il nodo x in esame non sia magro.
- Inoltre, supponiamo anche che se la radice rimane senza alcune chiave, viene deallocata.

Schematizziamo la procedura:

>[!application]
>1. Se $k$ è nel nodo $x$ ed $x$ è una foglia, si cancelli $k$ da $x$.  
>2. Se $k$ è nel nodo $x$ ed $x$ è un nodo interno:
>	1. Se il figlio $y$ di $x$ che precede $k$ ha almeno $t$ chiavi, si determini il predecessore $k'$ di $k$ nel sottoalbero radicato in y.
>	   Si cancelli ricorsivamente $k'$ e si sostituisca $k$ con $k'$
>	2. Situazione simmetrica di 2.1, per il figlio $z$ di $x$ che segue $k$
>	3. Altrimenti, se sia $y$ che $z$ hanno $t-1$ (magri), si uniscono $k$ e il nodo $z$ a $y$, si cancella $k$ da $x$, si dealloca $z$ e si cancella ricorsivamente $k$ da $y$
> 3. Se k non è presente nel nodo interno $x$, si determina la radice $c_{i}[x]$ del sottoalbero di $x$ che contiene $k$:
> 	- Se $c_{i}[x]$ è magro, si esegue il passo 3.1 o 3.2 e quindi ricorsivamente si rimuove la chiave k dal sottoalbero che la contiene
> 	1. Se $c_{i}[x]$ ha un fratello immediato non magro:
> 	   ![[Pasted image 20231219014350.png|512]]
> 	2. Se entrambi i fratelli immediati di $c_{i}[x]$ sono magri
> 	   ![[Pasted image 20231219014429.png|512]]
> 	- Altrimenti, se $c_{i}[x]$ non è magro, si proceda ricorsivamente a cancellare la chiave k a partire dal nodo $c_{i}[x]$ 

>[!example]- Esempio Cancellazione
>- Delete(F) Caso 1
>![[Pasted image 20231219014705.png|512]]
>- Delete(M) Caso 2.1
>![[Pasted image 20231219014920.png|512]]
>- Delete(G) Caso 2.3
>![[Pasted image 20231219015008.png|512]]
>- Delete(D) Caso 3.2
>![[Pasted image 20231219020105.png|512]]
>- Delete(B) Caso 3.1
>![[Pasted image 20231219020138.png|512]]