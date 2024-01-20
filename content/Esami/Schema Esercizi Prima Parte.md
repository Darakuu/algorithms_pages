---
tags:
  - Algoritmi/PrimaProva
---
# Analisi Ammortizzata

sempre quello mbare

# Splay Tree

- Descrivere le operazioni bottom-up, e top-down
- Fai operazioni

# B-Tree

- Si definisca la struttura dati BTree
- (Completo) Si definisca in maniera precisa la struttura dati B-tree e se ne illustri sinteticamente un’applicazione.
- Si determini il numero massimo e minimo di nodi che può essere contenuto in un B-Tree di altezza h e grado minimo $t=2$
	- $\log_{2t}\dfrac{n+1}{2t}\leq h\leq \log_{t}\dfrac{n+1}{2}$
	- numero minimo nodi: $\#NodiMin=1+2\displaystyle\sum^{h-1}_{i=0}t^i$
	- numero Massimo nodi: $\#NodiMax=\displaystyle\sum^h_{i=0}(2t)^i$
	  
	- numero minimo chiavi con grado minimo t: $n_{t,h}=2t^h-1$
	- numero Massimo chiavi con grado minimo: $N_{h} = (2t)^{h+1}-1$
- Fornire CON DIMOSTRAZIONE il limite superiore per l'altezza $h$ di un B-Tree di grado minimo $t$ con $n$ chiavi
- Sia $T'$ un B-tree con $6000$ chiavi, il cui grado minimo è il medesimo di quello in figura. Qual è la massima altezza possibile per $T'$?
- Si determinino una minorazione e una maggiorazione del numero di nodi a profondità $i=0,1,\dots,h$ in un B-Tree di grado minimo $t$ e altezza $h$ (fai tabella)
- Si effettui l’inserimento delle chiavi $D, G, R, F, M, H, P, Q, I, L, A, B, C$ (nell’ordine dato) in un B-tree di grado minimo 2, inizialmente vuoto, e quindi si cancellino le chiavi $F, L, D$.



# Alberi Binomiali

- Definire, enunciare e dimostrare proprietà [[Alberi Binomiali]]
- Definire, enunciare e dimostrare proprietà [[Alberi Binomiali Non Ordinati]]

# Heap Binomiali

- Definire e fornire una maggiorazione al grado massimo di un nodo in uno heap binomiale contenente $n$ nodi [[Heap Binomiali]]
- Fornire un esempio di Heap Binomiale che contiene 8 chiavi e effettuare l'operazione di Extract-Min
- e descrivi DecreaseKey, ExtractMin, Delete, e Insert (Ed esegui esercizio)
- Determinare un limite superiore e un limite inferiore per il numero di alberi binomiali in un heap binomiale con $n$ chiavi.
- Nel caso degli heap binomiali, è richiesto che gli alberi binomiali nella lista delle radici siano ordinati per grado. Perché?

# Heap di Fibonacci

- Indicare operazioni supportate, e la loro complessità.
- Sia $x$ un nodo di grado $k$ in un heap di Fibonacci e siano $y_{1},\dots,y_{k}$ i figli di $x$ nell'ordine in cui sono stati innestati in $x$. Quale limitazione inferiore è possibile dare per il grado degree$(y_{i})$. Perché? [[Heap di Fibonacci#Lemma 3|Lemma 3]]
- Fornire (e dimostrare) una minorazione dei gradi dei figli di ciascun nodo (**LEMMA**)
- Stabilire se esistono heap di Fibonacci dati nel compito


## Esercizio 4 (super schematizzabile):
- Si definiscano gli alberi binomiali e si enuncino le loro principali proprietà, dimostrandole;
- Si definiscano gli heap binomiale e si fornisca una maggiorazione al grado max di un nodo in un heap binomiale contenente n nodi

# Union-Find

- Si descriva la struttura dati union-find nella sua versione più efficiente, presentando le due euristiche su cui si basa e illustrando mediante pseudo-codice le operazioni supportate.  

- Qual è la complessità di una sequenza di $m$ operazioni di cui $n$ sono Make Set?

