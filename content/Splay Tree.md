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
>#todo

 
Sia $T_{0}$ un albero vuoto #todo

### Lemma

### Dim

>[!def] Teorema
>Il costo ammortizzato dell'operazione Splay(x,T) è al più #todo 
><ins>Dimostrazione</ins>
>Calcoliamo

Casi...