---
tags:
  - Algoritmi/AnalisiAmmortizzata
todo:
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

Poniamo $\phi(S)=_{def}\mid S\mid$, con $S_{0}$ lo Stack vuoto.

to be continued
