---
title: Conseguenze semantiche
header-includes:
  - \usepackage{mathtools}
  - \usepackage{stmaryrd}
  - \usepackage{cancel}
---

\newcommand{\limplies}{\rightarrow}
\newcommand{\liff}{\longleftrightarrow}
\newcommand{\val}[1]{\llbracket\,#1\,\rrbracket}
\newcommand{\rep}[1]{[\,#1\,]}
\newcommand{\taut}{\vDash}

- [Ragionamento ipotetico deduttivo](#ragionamento-ipotetico-deduttivo)
  - [Conseguenze semantiche](#conseguenze-semantiche)
          - [Notazione](#notazione)
      - [Esempio](#esempio)
      - [Esercizio](#esercizio)
    - [Tautologie notevoli](#tautologie-notevoli)
  - [Stringhe ed occorrenze](#stringhe-ed-occorrenze)
  - [Sostituzione](#sostituzione)
    - [Definizione iterativa](#definizione-iterativa)
      - [Esempio](#esempio-1)
    - [Definizione ricorsiva](#definizione-ricorsiva)
    - [Teorema](#teorema)
  - [Relazioni di equivalenza](#relazioni-di-equivalenza)
          - [Nota bene](#nota-bene)
  - [Teorema](#teorema-1)

# Ragionamento ipotetico deduttivo

Il ragionamento tipico della matematica è il ragionamento ipotetico-deduttivo, rappresentato in logica dalle conseguenze semantiche.

## Conseguenze semantiche

###### Notazione

- $\Gamma,\Sigma,\Delta$ rappresentano insiemi arbitrari di proposizioni
- $\alpha,\beta,\phi,\psi$ rappresentano generiche proposizioni

Quindi per indicare che da un'ipotesi segue una proposizione si adotta la scrittura $\Gamma\taut{\psi}$, che si legge come "Da $\Gamma$ segue $\psi$".

Possiamo affermare che la valutazione di un'insieme di proposizioni è uguale ad uno se e solamente se la valutazione di tutti i suoi elementi è tale, infatti, dato un insieme $\Gamma$ ed una valutazione $v$:

$$
\val{\Gamma}_v=1\iff\forall{\phi}\in{\Gamma},\;\val{\phi}_v=1
$$

L'espressione $\Gamma\taut{\psi}$ si dice conseguenza semantica se e solamente se $\psi$ è verificata da ogni valutazione $v$ che verificha anche $\Gamma$, per cui scriviamo:

$$
\forall{v}\val{\Gamma}_v=1\implies\val{\psi}_v=1
$$

#### Esempio

Vogliamo provare che se $\alpha$ ed $\alpha\limplies\beta$ sono vere, allora lo è anche $\beta$, cioè che $\alpha\limplies\beta,\alpha\taut{\beta}$.

Svolgimento:

$$
\begin{aligned}
  \val{\alpha\limplies\beta,\alpha}_v=1
  &\iff\val{\alpha\limplies\beta}_v=1\text{ and }\val{\alpha}_v=1\\
  &\iff(\cancel{\val{\alpha}_v=0}\text{ or }\val{\beta}_v=1)\text{ and }\val{\alpha}_v=1\\
  &\implies\val{\beta}_v=1\text{ and }\val{\alpha}_v=1\\
  &\implies\val{\beta}_v=1
  &\square
\end{aligned}
$$

#### Esercizio

Vogliamo dimostrare che $(\Gamma,\alpha\taut{\beta})\implies\Gamma\taut{\alpha\limplies\beta}$.

Svolgimento:

$$
\begin{aligned}
    \forall{v}\val{\Gamma,\alpha}_v=1\implies\val{\beta}_v=1
    &\iff(\val{\Gamma}_v=1\text{ and }\val{\alpha}_v=1)\implies\val{\beta}_v=1\\
    &\iff(\val{\Gamma}_v\ne{1}\text{ or }\underline{\val{\alpha}_v=0})\text{ or }\underline{\val{\beta}_v=1}\\
    &\iff\val{\Gamma}_v\ne{1}\text{ or }\val{\alpha\limplies\beta}_v=1\\
    &\implies\Gamma\taut{\alpha\limplies\beta}
    &\square
\end{aligned}
$$

### Tautologie notevoli

A livello teorico esistono infinite tautologie, ma tra le più importanti citiamo:

- Leggi di De Morgan

$$
\begin{aligned}
    \neg(\phi\land\psi)&\liff(\neg\phi\lor\neg\psi)\\
    \neg(\phi\lor\psi)&\liff(\neg\phi\land\neg\psi)\\
\end{aligned}
$$

- Involutività della negazione

$$
\neg(\neg\alpha)\liff\alpha
$$

- Commutatività

$$
\begin{aligned}
    (\phi\land\psi)&\liff(\psi\land\phi)\\
    (\phi\lor\psi)&\liff(\psi\lor\phi)\\
\end{aligned}
$$

- Distributività

$$
\begin{aligned}
    \phi\land(\psi\lor\sigma)&\liff(\phi\land\psi)\lor(\phi\land\sigma)\\
    \phi\lor(\psi\land\sigma)&\liff(\phi\lor\psi)\land(\phi\lor\sigma)\\
\end{aligned}
$$

- Associatività

$$
\begin{aligned}
    \phi\land(\psi\land\sigma)&\liff(\phi\land\psi)\land\sigma\\
    \phi\lor(\psi\lor\sigma)&\liff(\phi\lor\psi)\lor\sigma
\end{aligned}
$$

## Stringhe ed occorrenze

Dato un insieme di simboli generici $\Omega$, una stringa su questo insieme è una sequenza di finita lunghezza $n$, della forma:

$$
s=c_1\;c_2\;\dots\;c_n\\
$$

dove per ogni indice $i$ appartenente all'intervallo $(1,n)$ il simbolo $c_i$, si trova in $\Omega$. 

Di conseguenza, dato un simbolo $a\in\Omega$ si dice occorrenza della stringa $s$, ogni coppia $(a,i)$ tale per cui il simbolo di partenza $a=c_i$.

## Sostituzione

Siano quindi $\phi,\psi\in{PROP}$ e $p\in\phi$, si scrive $\phi\rep{\psi/p}$ per indicare che il simbolo $p$ viene rimpiazzato dalla proposizione $\psi$.

### Definizione iterativa

Per applicare la sostituzione in modo iterativo, si scorre una proposizione per individuare tutte le occorrenze e si rimpiazza il valore.

#### Esempio

Data $\phi=((p_1\limplies(p_5\lor{p_1}))\land{p_3})$, vogliamo sostituire $p_1$ con $\phi$.

Svolgimento:

> Le occorrenze di $p_1$ sono $(p_1,3),(p_1,8)$, sostituendo $p_1$ con $\psi$ otteniamo: $((\psi\limplies(p_5\lor{\psi}))\land{p_3})$.

### Definizione ricorsiva

Sia $*$ un connettivo tra $\{\land,\lor,\limplies\}$, allora:

1. $\phi\,\rep{\psi/p}\;=\begin{dcases}\bot\text{ iff }&\phi=\bot\\\phi\text{ iff }&\phi\in{AT},\,\phi\ne{p}\\\psi\text{ iff }&\phi\in{AT},\,\phi=p\end{dcases}$

2. $(\neg\phi)\rep{\psi/p}\;=\neg(\;\phi\rep{\psi/p}\;)$

3. $(\phi_1*\phi_2)\rep{\psi/p} = (\;\phi_1\rep{\psi/p}*\phi_2\rep{\psi*p}\;)$

### Teorema

Sia $\psi_1\liff\psi_2=(\psi_1\limplies\psi_2)\land(\psi_2\limplies\psi_1)$, allora dato $\taut{\psi_1\liff\psi_2}$, vale:

$$
\taut{\phi\rep{\psi_1/p}\liff\phi\rep{\psi_2/p}}
$$

## Relazioni di equivalenza

Sia $A$ un insieme e sia $R\subseteq{A\times{A}}$, quest'ultima viene chiamata relazione di equivalenza se e solamente:

- È riflessiva: $\forall{a}\in{A},aRa$
- È transitiva: $\forall{a,b,c}\in{a},(aRb,bRc)\implies{aRc}$
- E simmetrica: $\forall{a,b}\in{A},(aRb,bRa)$

###### Nota bene

> Un esempio di relazione di equivalenza è la similitudine tra triangoli.

## Teorema

Si dice che $\phi$ è equivalente a $\psi$ se e solamente se $\phi\liff\psi$ è una tautologia, infatti scriviamo che:

$$
\phi\approx\psi\iff\taut{\phi\liff\psi}
$$

Con $\approx\;\subseteq{PROP\times{PROP}}$.