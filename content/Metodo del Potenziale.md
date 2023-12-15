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
> - Il costo ammortizzato $\hat{c}^i$ della i-esima operazione rispetto alla funzione potenziale $\phi$ è:
> 	- $\hat{c}^i=c_{i}+\phi(D_{i})-\phi(D_{i-1})$

to be continued
