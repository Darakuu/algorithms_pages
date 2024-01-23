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
> Ad ogni passo della procedura di colorazione esiste un MST contenente **tutti** gli archi $\textcolor{royalblue}{blu}$ e **nessun** arco $\textcolor{red}{rosso}$.


> [!tldr] Teorema
> Ogni esecuzione del processo di colorazione colora **tutti** gli archi mantenendo l'invariante del colore.


> [!tldr] Corollario con DIM
> Alla fine della procedura di colorazione, l'insieme degli archi $\textcolor{royalblue}{blu}$ forma un MST 
>
> <ins>Dimostrazione</ins>
>  - Sia $E'$ l'insieme degli archi blu alla fine del processo,
>  - Sia $T=(V,E'')$ un MST tale che $E'\subseteq E''$ (che esiste grazie all'invariante del colore),
>  - Poiché $E''$ non contiene alcun arco rosso, si ha anche il viceversa, cioè $E''\subseteq E' \implies E'=E''$
>  - Quindi $(V,E')$ è un MST $\blacksquare$

Verifichiamo che l'invariante d el colore è mantenuto dopo ogni passo di colorazione, per induzione. 

- Inizialmente l'invariante del colore è banalmente verificato, in quanto non ci sono nè archi blu, nè archi rossi.
- **Ipotesi Induttiva:** Sia $T=(V,E')$ un MST che contiene **tutti** gli archi blu al passo $k$, e nessun arco rosso
 

<ins>Passo k+1</ins> $\textcolor{royalblue}{blu}$  

Caso: il passo $k+1$ colora di $\textcolor{royalblue}{blu}$ l'arco $e=(u,v)$ che attraversa il taglio $(V_{1},V_{2})$ privo di archi blu. 

- Se $e \in T, T$ verifica l'invariante del colore anche al passo $k+1$.
- Se $e \notin T$, si consideri il cammino in $T$ da $u$ a $v$.
	- Sia $(u,v_{1})$ un arco su tale cammino che attraversa il taglio $(V_{1},V_{2})$. Esso è **non colorato**.
- Si consideri ora $T'$ tale che:
	- $\mathcal{E}[T']=(\mathcal{E}[T]\backslash\{(u_{1},v_{1})\})\cup\{(u,v)\}$
- Poichè $w(u,v)\leq w(u_{1},v_{1})$ si ha $w(T')\leq w(T)\leq w \implies \textbf{w(T')\ =\ w(T)}$
 

Cioè $T'$ è un MST contenente **tutti** gli archi blu al passo $k+1$. 

<ins>Passo k+1</ins> $\textcolor{red}{rosso}$ 

Caso: il passo k+1 colora di $\textcolor{red}{rosso}$ l'arco $e=(u_{1},u_{2})$ relativo al ciclo semplice $(u_{1},u_{2},\dots,u_{r},u_{r+1}=u_{1})$ 

- Se WORKINPROGRESS