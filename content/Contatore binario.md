---
tags:
  - Algoritmi/AnalisiAmmortizzata
---
# Contatore Binario con Increment

Sia $A[0,\dots ,k-1]$ un array di k Bit.
$$
\begin{flalign}
& \text{Value}[A] = \displaystyle\sum^{k-1}_{i=0}A[i]\times 2^{i} \\

& \text{Value}[\text{Increment}(A)] = \text{Value}[A]+1 (mod\ 2^{k}) \\
\end{flalign}
$$
1101011 $\to$ 1101100

$\LARGE\overset{7\quad \! \! 6\quad \! \! 5\quad \! \! 4\quad \! \!3 \quad \! \! 2\quad \! \! 1\quad \! \! 0 }{\boxed{0}\boxed{0}\boxed{0}\boxed{1}\boxed{0}\boxed{0}\boxed{0}\boxed{0}}$

```c
Increment(A)
i = 0
while (i<k) && A[i]=1 do:
	A[i] = 0
	i++
if (i<k) then:
	A[i] = 1
```

Costo di un'incremento: $\mathbf{O}(k)$
Costo di $\color{red}n$ incrementi = $\color{red}nO(k) = O(nk)$

Anche in questo caso c'è un'analisi sovrabbondante.

## Contatore Binario con [[Metodo dell'Aggregazione|Aggregazione]]

Supponiamo che esistano due operazioni:

ciaoooo

$Set \quad 0 \longrightarrow 1$
$Reset \quad 1 \longrightarrow 0$

E che il contatore sia inizialmente nullo.

Notiamo che su $n$ operazioni di tipo $\text{Increment}$:
- $A[0]$ cambia $n$ volte
- $A[1]$ cambia $\left\lfloor {\dfrac{n}{2}} \right\rfloor$ volte
- $A[2]$ cambia $\left\lfloor {\dfrac{n}{2^2}} \right\rfloor$ volte
- $A[3]$ cambia $\left\lfloor {\dfrac{n}{2^3}} \right\rfloor$ volte
- ...
- $A[i]$ cambia $\left\lfloor {\dfrac{n}{2^i}} \right\rfloor$ volte

ciao

**Esempio Contatore**
$$ \Large

\begin{flalign*} \\
& \overbrace{0\ 0\ 0\ 0\ 0}^k \ bit &\\
&0\ 0\ 0\ 0\ \color{red}1\ \quad \\
&0\ 0\ 0\ \color{red}1\ 0\ \\
&0\ 0\ 0\ 1\ \color{red}1 \\
&0\ 0\ \color{red} 1\ 0\ 0\ \\
&0\ 0\ 1\ 0\ \color{red}1 \\
&0\ 0\ 0\ \color{red}1\ 0 \\
&0\ 0\ 1\ 1\ \color{red} 1 \\
&0\ 1\ \color{red}0\ 0\ 0\ \\
&0\ 1\ 0\ 0\ \color{red}1 \\
&\underset{_{4}\ \ _{3}\ \ _{2}\ \ _{1}\ \ _{0}}{0\ 1\ 0\ \color{red}1\ 0 }\\

\end{flalign*}

$$


## Contatore Binario con [[Metodo degli Accantonamenti|Accantonamenti]]

## Contatore Binario con [[Metodo del Potenziale|Potenziale]]