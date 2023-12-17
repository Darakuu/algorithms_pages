---
tags:
  - Algoritmi/StruttureDati
  - Algoritmi/PrimaProva
draft: false
---
# Splay Tree

Struttura dati di tipo Self-Adjusting.
- Gli Splay Tree implementano $M$ operazioni consecutive di ricerca, inserimento, cancellazione in tempo $O(M\log N)$, dove $N$ è il numero di inserimenti in un albero inizialmente vuoto.
- Cioè ciascuna delle $M$ operazioni è eseguita in un tempo [[Analisi Ammortizzata|ammortizzato]] $O(\log N)$.

>[!tip] Idea:
>Per quanto possibile, avvicinare alla radice i nodi che si incontrano durante un accesso.

Una procedura che funziona è di risalire due passi per volta quando possibile.

>[!application] Splay($x$,$T$)
>- Si cerca $x$ su $T$ con una ricerca binaria.
>- A partire dal nodo dove la ricerca si è fermata, e procedendo verso la radice, si applicano le operazioni di tip Zig, Zig-Zag o Zig-Zig necessarie

>[!Application] Insert($x,T$)
>- Si esegue Splay($x,T$)
>- Si inserisce il nuovo nodo $x$
>- Si esegue nuovamente Splay$(x,T)$

Siano i nodi:
- $g$, nonno;
- $p$, padre o parent;
- $x$, nodo su cui stiamo effettuando l'operazione.
 

Stiamo effettuando l'operazione Splay su $x$ in tutti i seguenti esempi:
## Zig-Zag

>[!example]- Esempio di Zig-Zag
>![[ZigZag.excalidraw.svg]]

Ogni nodo si sposta una posizione a destra seguita da una posizione a sinistra dalla posizione corrente.
In super short:  $\text{Zig-Zag:}\ \boxed{x}\to,\leftarrow$
## Zig-Zig

>[!example]- Esempio di Zig-Zig
>![[ZigZig.excalidraw.svg]]


Altro non è che una doppia operazione zig, definita sotto. Ogni nodo si muove due posizioni a destra dalla sua posizione attuale.

In super short: $\text{Zig-Zig:}\ \boxed{x}\to,\to$
## Zig
Nello Zig il nodo $x$ è sprovvisto di nonno. 
Ogni nodo si muove una posizione a destra dalla sua attuale posizione.

>[!example]- Esempio di Zig
>![[Zig.excalidraw.svg]]

 
In super short: $\text{Zig:}\ \boxed{x}\to$
## Insert(x,T)

Per inserire il nuovo nodo, prima effettuo una ricerca. 

Ovviamente, non trovando il nodo, effettuo l'inserimento nel punto dove la ricerca è fallita. 

In questo modo, manteniamo la proprietà di ricerca binaria: Difatti, se $x> root$, saremo sicuri che $x$ si trova nel sottoalbero destro rispetto a $root$. Viceversa, se $x\leq root$, $x$ si troverà nel sottoalbero sinistro.

Dopo l'inserimento, eseguiamo una ulteriore Splay per ribilanciare l'albero.

>[!example]- Esempio di Insert(x,T)
>![[SplayInsert.excalidraw.svg]]
## Delete(x,T)

- Si esegue una Splay(x,T) iniziale, portando x alla radice dell'albero.
- Si cancella il nodo x, ottenendo così due alberi $T_{1},T_{2}$.
- Si esegue una Splay(x,$\textcolor{red}{T_{1}}$), con $r$ nuova radice.
- Si pone la radice di $T_{2}$ come figlio destro di $r$.

Siamo sicuri che $r>\text{Tutti i nodi di }T_{1}$.

>[!example]- Esempio di Delete(x,T)
>![[SplayDelete.excalidraw.svg]]

# Analisi Ammortizzata Splay Tree

Costi delle operazioni elementari:
- Zig: 1 rotazione
- Zig-Zag: 2 rotazioni
- Zig-Zig: 2 rotazioni

Poniamo:
- $S(\nu)=_{def}\#\text{Nodi del sottoalbero con radice } \nu$
- $R(\nu)=_{def}\log(S(\nu))$, rango di $\nu$
- $\Phi(T)=_{def}\displaystyle\sum_{\nu \in T}R(\nu)$
>[!example]- Esempio di Calcolo $\phi(T)$
>![[SplayCalcoloPhi.excalidraw.svg|512]]
>
>$\phi(T)=5+\log3+\log 5+\log 10 = 5+\log 150$

 
Sia $T_{0}$ un albero vuoto, si ha:

$\phi(T_{0})=\displaystyle\sum_{\nu \in T_{0}} R(\nu)=0$ 

Sia $T$ un qualsiasi albero:
$\phi(T)=\displaystyle\sum_{\nu \in T} R(\nu)=\sum_{v \in T}\log S(\nu)\geq 0 = \Phi(T_{0})$

Pertanto, possiamo utlizzare il potenziale $\Phi(T)$ per calcolare un upper bound al costo reale di $M$ operazioni (cioè $Splay$,$Insert$,$Delete$) di cui $N$ sono $Insert$, a partire da uno splay tree vuoto. 


>[!def] Lemma
>
>Siano $a,b \in \mathbb{N^+}$, e sia $c \geq a+b$ 
>
>Allora: $\log a+\log b \leq 2\log c -2$
>
><ins>Dimostrazione</ins>
>Si osservi:
>$$\begin{align}
>(a+b)^2&=a^2+2ab+b^2 \\
> & = a^2-2ab+b^2+4ab \\
> & = (a-b)^2+4ab \\
> & \geq 4ab \\
>a+b & \geq 2\sqrt{ ab }
>\end{align} $$
>Considerando $c$
>$c\geq a+b\geq 2\sqrt{ ab }$
>Prendendo i logaritmi di ambo i membri:
>$\log c \geq 1+\dfrac{1}{2}(\log a+\log b)$
>$2\log c-2\geq \log a+\log b$

 


>[!def] Teorema
>Il costo ammortizzato dell'operazione Splay(x,T) è al più $3(R(root(T))-R(x))+1$ 

>[!def] Dimostrazione (Per casi!)
>Calcoliamo per iniziare il costo ammortizzato di una operazione di tipo Zig, Zig-Zag, Zig-Zig

### Notazione e Abbreviazioni

Indiamo con $S_{i}(x) \text{ e } S_{f}x$ il numero di nodi nel sottoalbero di radice x prima e dopo l'operazione in esame, analogamente per il Rango. 

Inoltre:
- $R_{i}(x,p) = R_{i}(x)+R_{i}(p)$
- $R_{f}(x,p,g)=R_{f}(x)+R_{f}(p)+R_{f}(g)$
etc... 

## Caso Zig-Zig

Costo Reale=2 


$\Delta \phi=R_{f}(x,p,g)-R_{i}(x,p,g)$ 

Si osservi che: $S_{f}(x) = S_{i}(g) \to R_{f}(x) =R_{i}(g)$, e quindi $\to \Delta \phi \leq R_{f}(x,g)-R_{i}(x,p)$ 

$S_{i}(x)+S_{f}(g)\leq S_{f}(x) \overset{ lemma }{ \longrightarrow }R_{i}(x)+R_{f}(g)\leq 2R_{f}(x)-2$
$$
\begin{align}
\longrightarrow\Delta \Phi & \leq R_{f}(x,g)-R_{i}(x,p)+R_{i}(x)-R_{i}(x) \\
& = R_{f}(x) \textcolor{lightgreen}{+R_{f}(g)} \textcolor{lightblue}{-R_{i}(x)}-R_{i}(p)\textcolor{lightgreen}{+R_{i}(x)} \textcolor{lightblue}{-R_{i}(x)} \\
& \leq R_{f}(x) +{\underset{ \text{somma maggiorata} }{\textcolor{lightgreen} {2R_{f}(x)-2} }}\textcolor{lightblue}{-2R_{i}(x)}-R_{i}(p) \\
& = 3R_{f}(x)-2-2R_{i}(x)-R_{i}(p) \\
& \leq 3R_{f}(x) -2 -\underbrace{ 2R_{i}(x)-R_{i}(x) }_{  } \\
& \leq 3R_{f}(x) - 2 -3R_{i}(x)  \\
& = 3(R_{f}(x)-R_{i}(x))-2 \\
\text{Da cui segue} \\
& -R_{i}(p) \leq -R_{i}(x) \\
\text{Cons. i nodi:} \\
S_{i}(x)\leq S_{i}(p) & \to R_{i}(x)\leq R_{i}(p) \\ \\

\Delta \Phi & \leq 3(R_{f}(x)- R_{i}(x)) -2 \\
 \\
 \\
&\Large\boxed{\hat{c}_{\text{zig-zig}}=2+\Delta \Phi \leq 3(R_{f}(x)-R_{i}(x))}
\end{align}
$$
 
>[!example] Grafico
>

## Caso Zig-Zag
$$
todo
$$
>[!example] Grafico
>
## Caso Zig

$$
todo
$$
>[!example] Grafico
>