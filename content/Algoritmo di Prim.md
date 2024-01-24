---
tags:
  - Algoritmi
  - Algoritmi/SecondaProva
  - Algoritmi/MST
draft: false
---
# Strategia

- Si seleziona un nodo $s$;
- Si esegue $|V|-1$ volte la seguente operazione:
	- si seleziona l'albero $\textcolor{royalblue}{blu}\ T$ contenente $s$,
	- si seleziona un arco di costo minimo incidente su $T$ e lo si colora di $\textcolor{royalblue}{blu}$.

# Implementazione

$Prim(G,w,s)$
## Inizializzazione


> [!def] Terminologia:
> - $k[v]:$ Campo 'key' del vertice, rappresenta il peso minimo di un arco qualsiasi che collega v a un vertice nell'albero finale MST. Per convenzione, $k[v]=\infty$ se l'arco non esiste.
> - $pred[v]:$ Padre o predecessore del vertice v nell'albero finale
> - $s:$ nodo di inizio, start, o la radice dell'albero MST finale.



```cs title="Prim(G,w,s)_init"
for (u in V[G]):             // per ogni vertice in G
	k[u] = +INFTY;           // poni tutte le 'key' di ogni vertice a infinito, perché inizialmente tutti i nodi attorno alla radice sono 'sconosciuti'
	pred[u] = NIL;           // poni tutti i predecessori di ogni nodo a NIL, perché ancora l'albero finale MST è vuoto
k[s] = 0;                    // poni il campo 'key' della radice a 0. La radice è il primo nodo da visitare
Q = Build-Heap(V[G],k);      // Q è una coda di min-priorità che si svuota man mano che costruiamo l'MST finale.
```


## Costruzione

```cs title="Prim(G,w,s)_build"
while (Q != EMPTY_SET):                         // finchè non svuotiamo la coda di min-priorità Q, l'albero MST finale non è completo 
	u = Extract_Min(Q);                         // trova il prossimo vertice da considerare: quello con valore 'key' minore
	for (v in G.Adj[u]):                        // il vertice da considerare deve essere adiacente a quello appena processato
		if (v in Q) && (w(u,v) < k):            // se v è nella coda Q (cioè ancora sconosciuto) e il peso del suo arco è minore della key...
			Decrease_Key(Q, v, w(u,v) );        // ...aggiorna la coda,
			pred[v] = u;                        // ... e aggiorna il predecessore del vertice v
return { (pred[v],v) : v in V[G] \ {s} }
```

Questo ciclo $while$ mantiene la seguente invariante di ciclo:
- $A=\{\  (\ v,\ pred[v]\  ): v \in V - \{\ r\ \}-Q\ \}$
- I vertici già inseriti nell'MST finale sono quelli che appartengono a $V-Q$.
- Per ogni vertice $v \in Q$, se $pred[v] \neq \text{NIL}$, allora la key del vertice v è minore di infinito ($\text{v.key} < \infty$), ed è il peso di un arco leggero tra: $(v, pred[v])$ che collega $v$ a qualche vertice che si trova già nell'MST


## Esempio Esercizio:

Per eseguire l'esercizio in maniera "formale", cioè seguendo strettamente lo pseudocodice, conviene mantenere una tabella a lato del grafo, del tipo:

| Vertice | Visitato? | Costo | Percorso |
| :--: | :--: | :--: | :--: |
| a | FALSE | $\infty$ | -1 |
| b | FALSE | $\infty$ | -1 |
| c | FALSE | $\infty$ | -1 |
| ... | ... | ... | ... |
Esempio di una tabella di inizio.


> [!warning] Il seguente esercizio è parecchio lungo:

Nota, l'esercizio è leggermente modificato rispetto alla prova d'esame. In particolare, ho cambiato i pesi degli archi $(l,m)$ e $(f,l)$

> [!danger]- Esempio svolgimento esercizio D'ESAME con Prim (svg)
> **Consiglio di aprire in un'altra scheda**
>![[MST-Prim_Esercizio.svg]]


# Complessità

## Confronto tra E logV ed E + V logV