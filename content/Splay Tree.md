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

![[ZigZag.excalidraw.svg]]



Ogni nodo si sposta una posizione a destra seguita da una posizione a sinistra dalla posizione corrente.
## Zig-Zig

![[ZigZig.excalidraw.svg]]


Altro non è che una doppia operazione zig, definita sotto. Ogni nodo si muove due posizioni a destra dalla sua posizione attuale.
## Zig
Nello Zig il nodo $x$ è sprovvisto di nonno. 
Ogni nodo si muove una posizione a destra dalla sua attuale posizione.

![[Zig.excalidraw.svg]]