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

## Multipop con [[Metodo dell'Aggregazione|Aggregazione]]

Lo stack è inizialmente vuoto. Le operazioni di Pop e Push sono elementari, mentre MultiPop(S,k) è un'operazione composta (da più pop).
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

## Multipop con [[Metodo degli Accantonamenti|Accantonamenti]]

## Multipop con [[Metodo del Potenziale|Potenziale]]