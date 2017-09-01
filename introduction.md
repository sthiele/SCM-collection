---
header-includes:
  - \usepackage{graphicx}
  - \usepackage{colortbl}
  - \definecolor{dark}{RGB}{115,115,115} 
  
  - \newcommand\BS[1]{\text{\fontshape{n}\fontseries{bx}\selectfont#1}}
  - \newcommand\plus{\BS{+}}
  - \newcommand\minus{\BS{--}}

  - \newcommand\uncertainincrease{\vartriangle}
  - \newcommand\uncertaindecrease{\triangledown}

  - \newcommand\weakplus{\boldsymbol{\oplus}}
  - \newcommand\weakminus{\boldsymbol{\ominus}}
---


# Interaction graphs and signed system changes

In this part I want to give an introduction to interaction graph models and how they are
used by sign consistency methods to model the changes in a dynamic system.

## What are interaction graphs?

Interaction or influence graphs are a widely used representation for complex systems.
Nodes represent the components or players in the system and edges denote how these components interact with each other.
A lot of biological systems have a representation as interaction graph: 
 hunter prey models, gene regulatory networks, signaling networks,  etc. 
Here is a more formal definition.

### Definition
An interaction graph is a signed directed graph $(V, E, \sigma)$,
 where $V$ is a set of nodes, $E$ a set of edges, and $\sigma : E \rightarrow \{ \plus, \minus \}$ a labeling of the edges. 
Every node in $V$ represents a state variable in the modeled system and 
an edge $i \rightarrow j$ means that the change of $i$ in time influences the value of $j$. 
Every edge $i \rightarrow j$ of an interaction graph can be labeled with a sign,
 either $\plus$ or $\minus$, denoted by $\sigma(i, j)$,
 where $\plus$ ($\minus$) indicates that $i$ tends to increase (decrease) $j$.

An example of an interaction graph is given in Figure~\ref{fig:ig}. 
There exist many variants of interaction graphs some have weighted edges and 
some have other kind of edges or different types of nodes. 
But with this definition we will come pretty far.
![Example of an interaction graph. Green arrows indicate positive ($\plus$) influence, red edges negative ($\minus$) influence. \label{fig:ig}](figures/paper-figure0.png )

## What are signed system changes?

Interaction graphs are an abstraction of dynamic
 quantitative systems where a quantitative state of the system is a mapping 
 $S_i : V \rightarrow \mathbb{R}^+$.
Sign consistency methods use signs to denote changes in the variables of the modeled system. 
Examples for such changes could be increased or decreased in metabolite concentrations or expression levels of genes.
The signs $\plus$ and $\minus$ are used to denote increase and decrease and 0 signifies no-change.
Sign consistency methods relate the IG model of the system and the variations in between system states
 by representing the variations as labels on the nodes in the graph. 
For example, the changes between two states of the system 
 can be represented as a sign labeling of the IG. 
Given two system states $S_R$ and $S_O$
 the differences between these states can be represented as the labeling $\mu_{RO} : V \rightarrow \{\plus, \minus, 0\}$ with
$\mu_{RO}(x) = sign(x_{S_O} - x_{S_R})$.
See Figure~\ref{fig:state_change} for an example of two states and the corresponding sign labeling.
We use the colors 
$\blacksquare$,
$\blacksquare$,
$\blacksquare$
 to represent the signs $\plus, \minus, 0$.

![a](figures/paper-figure1.png ) 
![b](figures/paper-figure2.png ) 
![Example of a sign labeling representing the change between two quantitative states. \label{fig:state_change}](figures/paper-figure3.png ) 

Further, sign consistency methods define rules that determine which labelings 
of the graph are considered consistent and which are considered inconsistent.
There exist several consistency rules which are useful to model different 
properties of a biological system. 
For now, we only consider the following.

### backwards propagation
\label{rule_bw}
_Every change in a node must be explained by a change in one of its predecessors._

Let $(V, E, \sigma)$ be an IG.
Then a labeling $\mu : V \rightarrow \{\plus, \minus, 0\}$ satisfies Rule~\ref{rule_bw} for node $i \in V$ iff

- $\mu(i) = 0$, or
- there is some edge $j \rightarrow i$ in $E$ 
       such that $\mu(i)=\mu(j)\sigma(j,i)$.

Rule~\ref{rule_bw} implements backward reasoning.
Given an effect we look backwards to verify its cause.
Labelings that are consistent with this rule represent the differences between steady states.
In a steady state the values of all state variables are balanced. 
Hence, the change in one variable must be sustained by the change in one of its predecessors.
In other words,
 if $S_R$ and $S_O$ are steady states of the system
 then the labeling $\mu_{RO}$ is consistent with Rule~\ref{rule_bw}.
The trivial example is when both states are the same $S_R = S_O$ then nothing changes $\forall x \in V : \mu_{RO}(x) = 0$.

Let's see what else we can do with that. 
Figure~\ref{fig:ig_labeled} shows an interaction graph and all labelings $\mu_i : V \rightarrow \{\plus, \minus, 0\}$ with $\mu_i(a)=\plus$ 
that satisfy Rule~\ref{rule_bw}.

![a](figures/paper-figure4.png )
![b](figures/paper-figure5.png ) 
![c](figures/paper-figure6.png ) 
![Labeled interaction graph \label{fig:ig_labeled}](figures/paper-figure7.png )

Often it is useful to represent the labelings in a table as shown in Table~\ref{tab:labeled}.
As you can see, there exist only four labelings that satisfy these constraints. 
In every of these labeling it holds $\mu_i(e)=\plus$ and $\mu_i(f)=\minus$.
We can use this table to predict the behavior of the system.
We see that in every steady state, with an increase in $a$ we also have an increase in $e$ and a decrease in $f$.
For $b$ and $c$ we can predict that they will not decrease,
 and for $d$ that it will not increase.

|    | $\mu_1$ | $\mu_2$ | $\mu_3$ | $\mu_4$ |
|----|:-------:|:-------:|:-------:|:-------:|
|$a$ | $\plus$ | $\plus$ | $\plus$ | $\plus$ |
|$b$ | $0$     | $\plus$ | $\plus$ | $\plus$ |
|$c$ | $0$     | $0$     | $\plus$ | $\plus$ |
|$d$ | $0$     | $0$     | $0$     | $\minus$|
|$e$ | $\plus$ | $\plus$ | $\plus$ | $\plus$ |
|$f$ | $\minus$| $\minus$| $\minus$| $\minus$|
Table of admissible labelings.
\label{tab:labeled} 


## Conclusion

In this part I introduced interaction graphs and explained how they can be used to model biological systems.
We have seen how sign consistency methods represent variations in the system as sign labelings,
and how sign consistency constraints can be used to derive predictions over the steady states of a system.
So far we have modeled a closed system.
In Part 2 I will introduce external inputs and perturbations.


