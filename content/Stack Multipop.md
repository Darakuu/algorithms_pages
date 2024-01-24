---
tags:
  - Algoritmi/AnalisiAmmortizzata
todo: false
---
# Stack con Multipop

Abbiamo tre operazioni:
- $\text{Pop}(S) \qquad\qquad\qquad \to \mathbf{O}(1)$
- $\text{Push}(S,x) \qquad\qquad\ \ \to \mathbf{O}(1)$
- $\text{STACK\_EMPTY}(S) \to \mathbf{O}(1)$

Definiamo la procedura di $\text{Multipop}$:

```c
Multipop(S,k)
while not STACK_EMPTY(s) and k>0 do:
	POP(s)
	k--
```

$\text{Multipop}(S) \to O(min(|S|,k))$

Analisi di una sequenza di $n$ operazioni su uno stack <ins>inizialmente vuoto</ins>.
- $|S| = \mathbf{O}(n)$
- Costo di una singola operazione $= \mathbf{O}(n)$
- Costo di $n$ operazioni $=n \mathbf{O}(n) = \mathbf{O}(\color{red}{n^{2}}\color{white})$
Questa è una sovrastimazione del costo effettivo che potremmo ottenere.

>[!warning] Lo Stack è inizialmente vuoto a meno che non venga specificato altrimenti

## Multipop con [[Metodo dell'Aggregazione|Aggregazione]]

Le operazioni di Pop e Push sono elementari, mentre MultiPop(S,k) è un'operazione composta (da più pop).
Sia $op_{i}$ una qualsiasi operazione (pop, push, multipop):

$\underbrace{ op_{1},op_{2},op_{3},\dots,op_{n-1},op_{n} }_{ \downarrow }$ $\quad \longleftarrow \quad${Pop, Push, Multipop}
$op'_{1},op'_{2},op'_{3},\dots,op'_{m-1},op'_{m}$ $\quad \longleftarrow \quad${Pop, Push}

Ossia abbiamo ora $m$ operazioni elementari. Ogni multipop è stata scomposta in una sequenza di pop semplici.

Costo $\mid<op_{1},\dots,op_{n}>\mid$ = costo $\mid<op_{1},\dots,op_{m}>\mid$ = $\large m$

Cioè abbiamo fatto:

$\large\text{Multipop}(S,k) \quad \longrightarrow \quad \underbrace{ \text{Pop}(S),\dots,\text{Pop}(S) }_{ min(\mid S\mid,k) }$

Per questo cambia l'indice da n ad m.
$min(\mid S\mid,k)$ significa che multipop esegue per $k$ volte, oppure fino a svuotamento totale dello stack.


> [!example] Multipop $\to$ Sequenza di Pop
> $\quad\qquad\Large\text{Multipop}(4)$
> $\overbrace{ \large\overset{op'4}{\text{Pop}(S)},\Large\overset{op'4}{\text{Pop}(S)},\Large\overset{op'4}{\text{Pop}(S)} }^{\color{red}\downarrow}$

### Upper Bound numero Pop

Il numero delle pop può al più essere il numero delle push effettuate nello stack.

$\#\text{Pop}(op'_{1},\dots,op'_{m}) \leq \#Push(op'_{1},\dots,op'_{m}) = \#Push(op_{1},\dots,op_{n}) \leq n$

Cioè il numero di push non varia nella semplificazione di multipop in sequenze di pop.

Pertanto

$\#Pop(\dots) \leq n$

Da cui troviamo il costo $T(n)$:
$$\large
\begin{align}
 T(n)& =  \text{costo}(\langle op_{1},\dots,op_{n}\rangle) = \text{costo}(\langle op'_{1},\dots,op'_{m}\rangle) \\
& = \#\text{pop}(\langle op'_{1},\dots,op'_{m}\rangle) +\#\text{push}(\langle op'_{1},\dots,op'_{m}\rangle) \\
& \leq n+m \\ & \\
& \text{Costo Ammortizzato per Operazione: } \dfrac{T(n)}{n} \leq \dfrac{2\cancel{ n }}{\cancel{ n }}=2
\end{align}
$$

>[!example]- Esempio di sequenza peggiore
>$(n-1)Push + (n-1)MultiPop$

## Multipop con [[Metodo degli Accantonamenti|Accantonamenti]]

Assegneremo un costo più alto all'operazione di $\text{Push}$. 

Poniamo: 

$\hat{c}_{\text{push}}=2$ (1 unità per il costo reale, + 1 unità per il costo ammortizzato da noi assegnato);  

$\hat{c}_{\text{pop}}=\hat{c}_{\text{multipop}}=0$ 

In ogni istante avremo: $\displaystyle\sum^n_{i=1}\hat{c}_{i}-\displaystyle\sum^n_{i=1}c_{i}=|S|\geq 0$ dove |S| è il numero di elementi nello stack. 

e quindi: $\displaystyle\sum^n_{i=1}\hat{c}_{i}\geq \sum^n_{i=1}c_{i}$ 

Avendo assegnato 2 al costo ammortizzato dell'operazione $\text{Push}$, avremo: 

$\displaystyle\sum^n_{i=1}\hat{c}_{i}\geq \sum^n_{i=1}c_{i} = 2\times \text{\#Push}\leq 2n$

>[!example]- Controesempio:
>Se avessimo assegnato costi ammortizzati inversi, una sequenza di sole push senza mai eseguire pop avrebbe generato credito negativo.

## Multipop con [[Metodo del Potenziale|Potenziale]]

Poniamo $\phi(S)=_{def}\mid S\mid$, con $S_{0}$ lo Stack vuoto. Poniamo, come da teoria, $\phi(S_{o}=0)$, quindi siamo sicuri che $\phi(S)\geq \phi(S_{0})$. 


>[!tip] Vogliamo trovare valori costanti nei costi ammortizzati.
 

- $\hat{c}_{pop}=c_{pop}+\phi(S_{i})-\phi(S_{i-1})=1+\mid S_{i}\mid-\mid S_{i-1}\mid\ = \ \boxed{\color{lightgreen}0}$ 
	- in quanto: $|S_{i}|=|S_{i-1}|-1$
- $\hat{c}_{\text{multipop}}=c_{\text{multipop}}+\phi(|S_{i}|)-\phi(|S_{i-1}|) = k + |S_{i}|-|S_{i-1}| = \boxed{\color{lightgreen}0}$
	- in quanto $|S_{i}|=|S_{i-1}|-k$
- $\hat{c}_{\text{push} }=c_{\text{push}}+|S_{i}|-|S_{i-1}|=1+1=\boxed{\color{lightgreen}2}$
	- in quanto: $|S_{i}|=|S_{i-1}|+1$
 
Abbiamo trovato gli stessi valori degli altri metodi: $2\times\#\text{push} = 2n$. 

Questa è una manifestazione della Proprietà di Confluenza: i crediti non dipendono dalla sequenza, ma dalla struttura dati.

### Stack inizialmente non vuoto

Se lo stack non è vuoto, purché non sia enorme, le sue operazioni rimangono lineari.

$$\begin{align}
\displaystyle\sum^n_{i=1}c_{i} &= \sum^n_{i=1}-\phi(D_{n})+\phi(D_{o}) \\
& \leq 2\times\#\text{Push} - |S_{n}|+|S_{0}| \\
& \leq 2\times n\qquad\ \ -|S_{n}|+|S_{0}| \\
& \leq 2 \times n \qquad\qquad\quad\ \ +|S_{0}| \\ 
\end{align}$$

Se $|S_{0}|=O(n) \implies \displaystyle\sum^n_{i=1}c_{i}=O(n)$

