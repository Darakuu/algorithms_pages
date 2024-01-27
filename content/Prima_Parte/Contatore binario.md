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

>[!warning] Il contatore è inizialmente nullo a meno che non venga specificato altrimenti

## Contatore Binario con [[Metodo dell'Aggregazione|Aggregazione]]

Supponiamo che esistano due operazioni:

$Set \quad 0 \longrightarrow 1$ </br>
$Reset \quad 1 \longrightarrow 0$ </br>

E che il contatore sia inizialmente nullo.

Notiamo che su $n$ operazioni di tipo $\text{Increment}$:
- $A[0]$ cambia $n$ volte, indica il bit del pari/dispari.
- $A[1]$ cambia $\left\lfloor {\dfrac{n}{2}} \right\rfloor$ volte, cioè una volta sì e una no.
- $A[2]$ cambia $\left\lfloor {\dfrac{n}{2^2}} \right\rfloor$ volte, ogni 4 volte.
- $A[3]$ cambia $\left\lfloor {\dfrac{n}{2^3}} \right\rfloor$ volte.
- ...
- $A[i]$ cambia $\left\lfloor {\dfrac{n}{2^i}} \right\rfloor$ volte.
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

Otteniamo:
$T(n)=n+\left\lfloor {\dfrac{n}{2}} \right\rfloor+\dots+\left\lfloor {\dfrac{n}{2^{k-1}}} \right\rfloor=$  
Otteniamo una serie geometrica di ragione $\dfrac{1}{2}$  
$= \displaystyle\sum^{k-1}_{i=0}\left\lfloor {\dfrac{n}{2^i}} \right\rfloor\leq \sum^{k-1}_{i=0}{\dfrac{n}{2^i}}<\sum^{\infty}_{i=0}\dfrac{n}{2^i}=2n$

Abbiamo tolto il floor ponendo la serie senza floor maggiore o uguale a quella con il floor, e sostituito k-1 con $\infty$ per maggiorare.  
Otteniamo $T(n)<2n \implies \dfrac{T(n)}{n}<\dfrac{2\cancel{ n }}{\cancel{ n }}=2$ 
<br>

## Contatore Binario con [[Metodo degli Accantonamenti|Accantonamenti]]

Poniamo:

$\hat{c}_{\text{set}}=2$  

$\hat{c}_{\text{Reset}}=0$  


Un'operazione di $\text{Increment}$ altro non è che $\text{Set}+\text{Reset}$, per cui: 

$\hat{c}_{\text{increment}}\leq 2$  


$\displaystyle\sum^n_{i=i}\hat{c}_{i}-\sum^n_{i=1}c_{i}=\text{\#bit sul contatore uguali ad } 1 \geq 0$ , La differenza è non negativa per ogni istante di esecuzione. 

Per cui vale: $\displaystyle\sum^n_{i=i}\hat{c}_{i}\geq\sum^n_{i=1}c_{i}$ , e riotteniamo lo stesso risultato del metodo dell'aggregazione: $2n\geq\displaystyle\sum^n_{i=i}\hat{c}_{i}\geq\sum^n_{i=1}c_{i}$ 


Ossia $n$ incrementi in tempo $2n$, indipendentemente da $k$  (il numero di bit) 


## Contatore Binario con [[Metodo del Potenziale|Potenziale]]

Sia $\Phi(D_{i})=\text{\#Bit Uguali ad }1$, e $\phi(D_{0})=0$.  

Stiamo rispettando la disuguaglianza $\phi (D_{i})\geq\phi(D_{o})$. 

Di nuovo, il costo ammortizzato è:

$\hat{c}_{i}=c_{i}+\underbrace{ \phi(D_{i})-\phi(D_{i-1}) }_{ \Large\Delta \phi_{i} }$ 

Si ha perciò: 

$c_{i}=\color{cyan}\text{\#Set}_{i}+\text{\#Reset}_{i}$ 

$\Delta \phi_{i}=\color{orange}\text{\#Set}_{i}-\text{\#Reset}_{i}$

>[!note] Nota Bene: $0\leq \text{\#Set}_{i}\leq 1$ 

Pertanto: 
$\hat{c}_{i}=\color{cyan}c_{i}\color{white}+\color{orange}\Delta \phi_{i}\color{white}=(\color{cyan}\text{\#Set}_{i}+\cancel{ \text{\#Reset}_{i} }\color{white})+(\color{orange}\text{\#Set}_{i}-\cancel{ \text{\#Reset}_{i} }\color{white})=2\times \text{\#Set}_{i}\leq 2$

Da cui: 

$\displaystyle\sum^n_{i=1}c_{i}\leq \sum^n_{i=1}\hat{c}_{i}=2\times \sum^n_{i=1}\text{\#Set}_{i}<2n$ 


### Contatore binario con incremento inizialmente <ins>non nullo</ins>

Poniamo come prima $\Phi(D_{i})=\text{\#Bit Uguali ad }1$, ma stavolta $\phi(D_{0})\neq0$. 

Otteniamo il valore del costo reale: 


$\displaystyle\sum^n_{i=1}{c}_{i}=\displaystyle\sum^n_{i=1}\hat{c}_{i}-\phi(D_{n})+\phi(D_{0}) \leq 2n+\phi(D_{0})\leq 2n+k$ 

Dove k è il numero di bit nel contatore. 

Se $k=O(n)$, allora $2n+k=O(n)$ e quindi $\displaystyle\sum^n_{i=1}c_{i}=O(n)$. 


Troveremo che il numero di bit k si palesa anche utilizzando negli altri metodi, nel caso di contatore non nullo.