---
tags:
  - Algoritmi/PrimaProva
  - Algoritmi/AnalisiAmmortizzata
---
Anziché rappresentare il lavoro prepagato come credito memorizzato su specifici oggetti nella struttura dati, il metodo del potenziale rappresenta il lavoro prepagato come una sorta di "_energia potenziale_" che può essere liberata per pagare operazioni future. 


Il potenziale è associato alla struttura dati nella sua interezza, anzichè a specifici oggetti. 


>[!def] Definiamo: 
> - $D_{0}$ una generica struttura dati iniziali, su cui vengono eseguite $n$ operazioni;
> - $\phi$ la **Funzione Potenziale**, che associa ciascuna struttura dati $D_{i}$ a un numero reale $\Phi(D_{i})$, che è il potenziale della struttura dati $D_{i}$;
> - Il costo ammortizzato $\hat{c}_{i}$ della i-esima operazione rispetto alla funzione potenziale $\phi$ è:
> 	- $\hat{c}_{i}=c_{i}+\underbrace{ \phi(D_{i})-\phi(D_{i-1}) }_{ \Large\Delta \phi }$
> 	- In altre parole, il suo costo effettivo più la variazione di potenziale scaturita dall'operazione.
> - Il costo ammortizzato totale è dato da una serie telescopica:
> 	- $\displaystyle\sum^n_{i=1}\hat{c}_{i}=\displaystyle\sum^n_{i=1}c_{i}+\phi(D_{n})-\phi(D_{0})$

La scelta della funzione potenziale sta a noi, è di fatto arbitraria, a una condizione: la somma dei costi ammortizzati deve sempre essere maggiore della somma dei costi reali. 

Difatti, se definiamo una funzione potenziale tale che $\phi(D_{n})\geq \phi(D_{0})$ il costo ammortizzato totale è un upper bound per il costo effettivo totale. 

Nella pratica, non sappiamo quante operazioni potrebbero essere eseguite, quindi questo upper bound è necessario per avere la garanzia che paghiamo in anticipo. 

Se imponiamo che $\phi(D_{i})\geq \phi(D_{0})\ \forall\  i$, ciò è garantito.  
 

Intuitivamente, se $\Delta \phi>0$, allora il costo ammortizzato rappresenta un valore sovrastimato per per la i-esima operazione, e il potenziale della struttura aumenta. 
Altrimenti, accade il viceversa. 


>[!tip] Negli esercizi, risulta utile porre $\phi(D_{0})=0$, e poi dimostrare che $\phi(D_{i})\geq 0$

>[!info]
>Funzioni potenziali diverse possono produrre costi ammortizzati diversi, che sono comunque limiti superiori per i costi effettivi.
>Spesso la funzione potenziale scelta è il risultato di qualche compromesso.

>[!note] Lemma:
>$\displaystyle\sum^n_{i=1}\hat{c}_{i}\geq \sum^n_{i=1}c \iff \phi(D_{n})\geq \phi(D_{0})$ 
>
>**Nota Bene:** anche se vale questo lemma, non ci è garantito un buon tempo di esecuzione.

>[!example] Esempi:
>- [[Stack Multipop#Multipop con Metodo del Potenziale Potenziale|Stack Multipop]]
>- [[Contatore binario]]