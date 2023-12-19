---
tags:
  - Algoritmi
  - Algoritmi/PrimaProva
  - Algoritmi/StruttureDati
draft: false
---
# Strutture dati per insiemi disgiunti

#todo

#todo rimuovi:

>[!quote]
>Si descriva la struttura dati union-find nella sua versione più efficiente, presentando le due euristiche su cui si basa e
illustrando mediante pseudo-codice le operazioni supportate.
Qual e la complessità di una sequenza di m operazioni di cui n sono Make Set?

# Euristiche:

>[!tip] Per quanto concerne l'esame, ci interessano principalmente le due euristiche fondamentali di implementazione, ossia:
> - Unione per Ranghi
> - Compressione dei Cammini

## Unione per Ranghi

- Si definisce opportunamente la nozione di Rango di un albero (legata in qualche modo all'altezza).
- Quindi si sceglie di innestare l'albero di <ins>rango più piccolo</ins> nella radice dell'albero di <ins>rango più alto</ins>.
- Nel caso di alberi aventi lo stesso rango, gli alberi si innestano in maniera arbitraria e il rango dell'albero risultante sarà incrementato di un'unità.


## Compressione die Cammini
- Tutti i nodi incontrati nell'esecuzione di una $\mathtt{FIND\_SET}$ vengono innestati nella radice.

## Effetto delle Euristiche sulla complessità

- La sola Unione per ranghi (senza compressione cammini) dà luogo a complessità $O(m\ \log n)$.
- La sola Compressione dei Cammini (senza unione ranghi) dà luogo a complessità $\Theta(n+f\cdot(1+\log_{2+f/n}n)),$ dove f=$\#\mathtt{FIND\_SET}$.
- Utilizzando entrambe le euristiche, si ottiene una complessità $O(m\ \alpha\ (n)),$ dove $\alpha(n)$ è la [[Funzione di Ackermann]].
	- In pratica, $\alpha(n)\leq 4,$ sebbene $\alpha(n)\to +\infty$

 
