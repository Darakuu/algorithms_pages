---
tags:
  - Algoritmi
  - Algoritmi/MST
  - Algoritmi/SecondaProva
---
Supponiamo che gli archi siano ordinati totalmente da un ordinamento che è in accordo con quello sui pesi, cioè: 

$w(e)\lt w(e') \implies e<e'$ 

Si applica il seguente passo finché possibile:


> [!NOTE] Passo Boruska
> Per ciascun albero blu, si selezioni l'arco incidente "minimo" non ancora colorato.
> 
> Si colorino di blu gli archi selezionati.
> (e di rosso gli archi non ancora colorati.)
