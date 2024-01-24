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


> [!example]- Esempio Colorazione (hi-DPI, espandi)
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
	- Sia $e'=(u_{1},v_{1})$ un arco su tale cammino che attraversa il taglio $(V_{1},V_{2})$. Esso è **non colorato**.
- Si consideri ora $T'$ tale che:
	- $\mathcal{E}[T']=(\mathcal{E}[T]\backslash\{(u_{1},v_{1})\})\cup\{(u,v)\}$
- Poichè $w(u,v)\leq w(u_{1},v_{1})$ si ha $w(T')\leq w(T)\leq w(T') \implies \textbf{w(T')\ =\ w(T)}$
 

Cioè $T'$ è un MST contenente **tutti** gli archi blu al passo $k+1$. 

In altre parole: 

L'arco $e$, appena colorato di blu al passo $k+1$, nasce da un taglio. Supponiamo di essere nel caso in cui $e$ non appartiene all'MST $T$. 

Considerando un arco $e'=(u_{1},v_{1})$ sul cammino in $T$ da $u$ a $v$. Questo arco:
- Attraversa il taglio;
- Non può essere rosso perché non avevamo archi rossi al passo precedente;
- Non può essere blu perché abbiamo appena colorato di blu l'arco $e$.
Quindi è non colorato. 


A questo punto vale la relazione $w(e)\leq w(e')$ perché T è un MST. 

Ma dato che T è un MST,vllora vale anche $w(T') \leq w(T)$. 

Questo ci fa concludere che $T$ e $T'$ sono uguali, quindi anche $T'$ è un MST.

Due domande che potremmo porci a questo punto sono: 
- "ma $T'$ è ancora un albero?" $\implies$ Sì, perché la cardinalità degli archi è uguale
- "Ma dopo che esce $e'$ l'albero è ancora connesso?" $\implies$ Sì, perché un albero è un grafo connesso minimale.


> [!example]- Visualizzazione dimostrazione
> ![[Minimum Spanning Tree-20240123124251171.png]]


<ins>Passo k+1</ins> $\textcolor{red}{rosso}$ 

Caso: il passo k+1 colora di $\textcolor{red}{rosso}$ l'arco $e=(u_{1},u_{2})$ relativo al ciclo semplice $(u_{1},u_{2},\dots,u_{r},u_{r+1}=u_{1})$ 

- Se $e \notin T$ non c'è niente da dimostrare. 
- Supponiamo allora che $e \in T$, perché potrebbe non mantenere l'invariante.
- $T\backslash\{e\}$ ha due componenti connesse che determinano una partizione $(V_{1},V_{2})$ di $V$.
- Sia $f$ un arco sul cammino $(u_{2},\dots,u_{r},u_{1})$ che attraversa il taglio $(V_{1},V_{2})$.
	- Si noti che $f$ non può essere blu perché $f \notin T$.
	- Inoltre $f$ non può essere rosso perché il ciclo semplice scelto per effettuare il $(r+1)\text{-esimo}$ passo non contiene archi rossi
	- Pertanto $f$ non è colorato.
- $w(e)\geq w(f)$

Sia $T''$ tale che $\mathcal{E}[T'']=(\mathcal{E}[T]\backslash\{e\})\cup\{f\}$. $T''$ è uno **spanning tree**. 

$w(T)\leq w(T'')\leq w(T) \implies w(T'')=w(T)$ 

Quindi $T''$ è un MST che verifica l'invariante del colore. 

L'albero è ancora connesso? $\implies$ sì, le 2 componenti connesse da $e$ sono ora connesse da $f$


> [!example]- Visualizzazione dimostrazione
> 
> ![[Minimum Spanning Tree-20240123132912280.png]]


> [!def] Lemma
> Al termine dell'esecuzione della colorazione, **tutti** gli archi sono stati colorati.


<ins>Dimostrazione</ins> 

- Sia $e=(u,v)$ un arco non ancora colorato,
- Sia $T$ un MST che verifica l'invariante del colore,
- Se $e \in T$, cancellando $e$ da $T$ si ottengono due componenti connesse che determinano un taglio $V_{1},V_{2}$
- $(V_{1},V_{2})$ non è attraversato da alcun arco $\textcolor{royalblue}{blu}$ ed è attraversato da archi non colorati $\implies$ è possibile applicare un passo $\textcolor{royalblue}{blu}$
- Se $e \notin T$, sia $\pi_{u,v}$ il cammino da $u$ a $v$ in $T$, e si consideri il ciclo semplice $(\pi_{u,v};e)$
- Tale ciclo non contiene archi $\textcolor{red}{rossi}$ ed inoltre contiene archi non colorati $\implies$ è possibile applicare un passo $\textcolor{red}{rosso}$ a tale ciclo.



> [!example]- Visualizzazione Lemma, caso Blu
> 
> ![[Minimum Spanning Tree-20240123134545911.png|512]]

> [!example]- Visualizzazione Lemma, caso Rosso
> ![[Minimum Spanning Tree-20240123134545691.png|512]]

## Unicità MST


> [!def] Proprietà
> Sia $G=(V,E)$ un grafo non orientato e connesso con funzione peso $w:E\to \mathbb{R}$ **iniettiva** $\implies$ $G$ ha un **unico** MST.

**Reminder**: $\Delta=\text{Differenza Simmetrica tra due insiemi} = (B-A) \cup (A-B)$

<ins>Dimostrazione</ins>

Siano $T_{1}\neq T_{2}$ due MST di $G$. 

Sia $e=(u,v) \in \mathcal{E}[T_{1}]\ \Delta\  \mathcal{E}[T_{2}]$ di peso minimo. 

Supponiamo che $e \in \mathcal{E}[T_{1}]\backslash\mathcal{E}[T_{2}]$, sia $\pi$ un cammino da $u$ a $v$ in $T_{2}$, ovviamente $\pi \cancel{ \subseteq }T_{1}$ 

Sia $e'=(u',v') \in (\mathcal{E}[T_{2}]\backslash\mathcal{E}[T_{1}])\cap \pi \subseteq \mathcal{E}[T_{1}]\ \Delta\  \mathcal{E}[T_{2}]$. 

Pertanto $w(e')>w(e)$. 

Sia ora $T_{2}'=T_{2}\ \backslash\ {e'}\cup e$, si ha che $T_{2}'$ è un albero. 

Inoltre $w(T_{2}')=w(T_{2})-w(e')+w(e)<w(T_{2})$, cioè che $T_{2}'$ è un altro MST con peso minore a $T_{2}$, che è **assurdo**. $\quad \blacksquare$

### Spiegazione più grafica e discorsiva di questa cosa apparentemente brutta brutta:


> [!warning] È un .svg, apri in un altra scheda

![[MST-UnicitaMST.svg]]
