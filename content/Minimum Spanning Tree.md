---
tags:
  - Algoritmi
  - Algoritmi/SecondaProva
  - Algoritmi/MST
  - Algoritmi/StruttureDati
---
# Alberi Ricoprenti Minimi

Input: 
- Grafo non Orientato ==Connesso==: $G=(V,E)$
- Una funzione ==peso== $w:E\to \mathbb{R}$
Output:
- Albero $T=(V,E')$ con $E' \subseteq E$, tale che per ogni altro albero $T_{1}=(V,E_{1}')$, con $E'\subseteq E$ si abbia:
	- $w(T)=\displaystyle\sum_{e \in E'}w(e)\leq \displaystyle\sum_{e \in E_{1}'}w(e)=w(T_{1})$
	- Cioè un albero la cui somma di tutti i pesi dei suoi archi è minore o uguale a quella di ogni altro albero possibile.
 


Algoritmo semplice: ricerca esaustiva di un MST. 

Problema: la ricerca esaustiva è però **esponenziale**, infatti il numero di alberi ricoprenti in un grafo completo su $n$ vertici è $n^{n-2}$. 


Discutiamo tre algoritmi Greedy:
- [[Algoritmo di Boruska]]
- [[Algoritmo di Kruskal]]
- [[Algoritmo di Prim]]

Sono tutti basati su un processo, **non deterministico**, di colorazione che mantiene un opportuno invariante (==invariante del colore==). 

A seconda dell'euristica utilizzata nel processo di colorazione si otterranno i tre algoritmi sopra. 

In generale, si scelgono gli archi $\textcolor{royalblue}{blu}$, e si eliminano gli archi $\textcolor{red}{rossi}$.

## Taglio


> [!def] Definizione
> Un **Taglio** di $G$ è una partizione $(V_{1},V_{2})$ di $V$ non banale (cioè tale che $V_{1,2}\neq \emptyset$). 
> 
> Un arco $(u,v)$ tale che $u \in V_{1}$ e $v \in V_{2}$ si dice che **attraversa** il taglio $(V_{1},V_{2})$.


![[Minimum Spanning Tree-20240123005940441.png|384]]

## Processo di Colorazione


> [!NOTE] Inizialmente nessun arco è colorato.

Finchè è possibile, si applichi uno dei due passi: 


- $\text{Passo }\textcolor{royalblue}{Blu}$
	- Si seleziona un taglio **non attraversato** da alcun arco blu;
	- Tra gli archi non colorati che attraversano il taglio se ne selezioni uno di peso <ins>minimo</ins> e lo si colori di $\textcolor{royalblue}{blu}$.
- $\text{Passo }\textcolor{red}{Rosso}$
	- Si seleziona un ciclo **semplice** privo di archi rossi;
	- Tra gli archi non colorati del ciclo se ne selezioni uno di peso <ins>massimo</ins> e lo si colori di $\textcolor{red}{rosso}$.
 


In un ciclo semplice: 

![[Minimum Spanning Tree-20240123010850884.png|384]]

I tre algoritmi sono tutti istante di questo processo di colorazione. Dimostrando che la colorazione è corretta, tutte le sue istanze, di conseguenza, lo saranno.


> [!example]- Esempio Colorazione
> ![[Minimum Spanning Tree-20240123013937896.png]]

Durante l'esecuzione del processo di colorazione vale la:

## Invariante del Colore


> [!def] Definizione
> Ad ogni passo della procedura di colorazione esiste un MST contente **tutti** gli archi $\textcolor{royalblue}{blu}$ e **nessun** arco $\textcolor{red}{rosso}$
