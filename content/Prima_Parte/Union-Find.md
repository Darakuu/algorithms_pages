---
tags:
  - Algoritmi
  - Algoritmi/PrimaProva
  - Algoritmi/StruttureDati
draft: false
---
# Strutture dati per insiemi disgiunti

- è spesso utile rappresentare in maniera efficiente famiglie dinamiche di insiemi disgiunti soggette alle seguenti operazioni:
	- Make_Set(x): Introduzione del singoletto $\{x\}$
	- Union(x,y): Unioni degli insiemi disgiunti che contengono rispettivamente x e y
	- Find_Set(x): Ricerca dell'insieme che contiene x
- Tali operazioni consentono la gestione di relazioni di equivalenza dinamiche monotone non-decrescenti.
- Analizzeremo seguenze di $m$ operazioni Make_Set, Union e Find_Set comprendenti n operazioni Make_Set, a partire da una configurazione vuota.
- Ovviamente:
	- $n \leq m$
	- $\# Union \leq n-1$
 
Esempio di una semplice applicazione: Mantenimento delle componenti connesse in un grafo non orientato crescente.

## Implementazione di insiemi disgiunti

Una possibile implementazione è con Liste Concatenate. 


Serve un puntatore da ciascun elemento al primo elemento della lista. 

è utile mantenere un puntatore all'ultimo elemento di ciascuna lista (tail), e conviene concatenare la seconda lista alla prima, durante l'esecuzione di una Union. 

Per eliminare il campo tail: la ricerca della coda della seconda lista si può fare mentre si aggiornano i campi $\mathtt{repr}$ della seconda lista.

Nell'eseguire l'operazione di Union, si appena la lista più corta a quella più lunga. (Unione per Ranghi) 

## Complessità

- Data una sequenza $S$ di operazioni Make_Set, Union, e Find_Set, poniamo:
	- $n= \#\text{Make\_Set}$
	- $m = \#\text{Make\_Set}+\#\text{Union} + \#\text{Find\_Set}$
	- $k = \#\text{Aggiornamenti ai campi Repr}$
- La complessità della sequenza $S$ è chiaramente: $\Theta(m+k)$

I costi ammortizzati delle operazioni sono:

- Find_Set(x) = Union(x,y) = $O(1)$
- Make_Set(x) = $O(\log n)$

### Calcoliamo $k$ in funzione di $n$

- Quante volte può cambiare il valore $repr[x]$ in un nodo $x$?
- Per l'euristica dell'Unione per Ranghi, ogni qualvolta il valore $repr[x]$ è aggiornato, la lunghezza della lista che contiene $x$ aumenta almeno $2$ volte.
- Quindi, il campo $repr[x]$ può cambiare al più $\left\lfloor {\log n} \right\rfloor$ volte.
- Di conseguenza, il numero totale di aggiornamenti al campo $repr$ di tutti i nodi è $O(n\log n)$
- **Pertanto** la complessità della sequenza $S$ è $\textcolor{red}{O(m+n\log n)}$

## Rappresentazione di insiemi disgiunti con alberi disgiunti

![[Pasted image 20231219185900.png|512]]

# Euristiche:

>[!warning] Efficienza
>L'implementazione con alberi disgiunti non è più efficiente di quella con liste concatenate, a meno che non si utilizzino le euristiche. 

>[!tip] Per quanto concerne l'esame, ci interessano principalmente le due euristiche fondamentali di implementazione, ossia:
> - Unione per Ranghi
> - Compressione dei Cammini

## Unione per Ranghi

- Si definisce opportunamente la nozione di Rango di un albero (legata in qualche modo all'altezza).
- Quindi si sceglie di innestare l'albero di <ins>rango più piccolo</ins> nella radice dell'albero di <ins>rango più alto</ins>.
- Nel caso di alberi aventi lo stesso rango, gli alberi si innestano in maniera arbitraria e il rango dell'albero risultante sarà incrementato di un'unità.

## Compressione dei Cammini
- Tutti i nodi incontrati nell'esecuzione di una $\mathtt{FIND\_SET}$ vengono innestati nella radice.
![[Pasted image 20231219191808.png|512]]

## Effetto delle Euristiche sulla complessità

- La sola Unione per ranghi (senza compressione cammini) dà luogo a complessità $O(m\ \log n)$.
- La sola Compressione dei Cammini (senza unione ranghi) dà luogo a complessità $\Theta(n+f\cdot(1+\log_{2+f/n}n)),$ dove f=$\#\mathtt{FIND\_SET}$.
- Utilizzando entrambe le euristiche, si ottiene una complessità $O(m\ \alpha\ (n)),$ dove $\alpha(n)$ è la [[Funzione di Ackermann]].
	- In pratica, $\alpha(n)\leq 4,$ sebbene $\alpha(n)\to +\infty$

## Pseudo-Codice delle operazioni:

```c
Make_Set(x):
p[x] = x
rank[x] = 0
```
 

```c
Find_Set(x):
if (x != p[x])
	p[x] = FIND_SET(p[x])
return p[x]
```
 

```c
Link(x,y):
if (rank[x]>rank[y])
	p[y] = x
else
	p[x] = y
		if (rank[x] == rank[y])
			rank[y]++
```
 

```c
Union(x,y):
Link(FIND_SET(x),FIND_SET(y))
```