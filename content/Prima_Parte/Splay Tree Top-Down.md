---
tags:
  - Algoritmi/StruttureDati
  - Algoritmi/PrimaProva
---
# Top Down Splay Tree

Nonostante i bottom-up splay tree siano facili da analizzare da un punto di vista teorico, sono poco efficienti dal punto di vista pratico. 
La variante top down mantiene un costo ammortizzato logaritmico pur non scendendo prima sul fondo dell'albero. 
 
## Idea di base

- Mentre si procede nella ricerca di un dato nodo, si trattano opportunamento i nodi incontrati, nonché i loro sottoalberi.
- Nel corpo dell'operazione di $Splay$, l'albero risulterà spezzato in tre parti:
	- Un albero $L$;
	- Un albero $T'$ di radice un certo nodo $x$;
	- Un albero $R$;
- Tali che $L\leq T'\leq R$. (invariante)
Inizialmente $x$ è la radice dell'albero $T$ originale, e L ed R sono vuoti. 

- Successivamente, scendiamo di due livelli per volta, se possibile, alla ricerca del nostro nodo, ed applichiamo Zig-Zag o Zig-Zig a seconda della situazione.
- Se si scende di un solo livello, si applica Zig ovviamente.
  

- Le tre operazioni hanno l'effetto di aggiornare i tre alberi $L$, $T'$, $R$ mantenendo l'invariante di prima.
- Alla fine, i tre alberi vengono riassemblati in un unico albero. 


## Zig
![[Pasted image 20231218214657.png|768]]
 
L'elemento su cui viene effettuata la Zig finisce in uno dei due alberi vuoti, a seconda se il figlio dell'elemento che subisce l'operazione è destro o sinistro.
- Se il figlio è destro ($x<y$), allora $x$ finisce nell'albero $L$;
- Se il figlio è sinistro ($x>y$), allora $x$ finisce nell'albero $R$;

## Zig-Zig

![[Pasted image 20231218214931.png|768]]

Immaginiamo di vedere, "al contrario:"
- Z: "nonno" (in realtà nipote di X)
- Y: "parent" (in realtà figlio di X)
- X: nodo su cui effetuiamo la splay.
Essenzialmente simile alla zig. Il "nonno" rimane nell'albero originale, il "parent" diventa il figlio di mezzo, mentre invece il nodo $x$ su cui viene effettuata la Zig-Zig diventa il nodo più profondo (con i suoi sottoalberi). 

## Zig-Zag
### Top-Down Destra

![[Pasted image 20231218215119.png|768]]

### Top-Down Sinistra

![[SplayTopDownZigZag_Sinistra.excalidraw.svg|768]]


## Zig-Zag Semplificata

![[Pasted image 20231218221324.png|768]]

Mantieni le relazioni dei figli di X in T', e sposti solo X

## Riassemblaggio finale

![[Pasted image 20231218221636.png|768]]
L'elemento più alto di T (ossia quello su cui abbiamo effettuato lo splay) diventa la nuova radice,  e perde i suoi sottoalberi, che finiscono su L o R a seconda se sottoalberi sinistri o destri. 

Inoltre, il sottoalbero sinistro di X sarà L, mentre il destro sarà R. 

