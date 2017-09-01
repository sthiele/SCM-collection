---
header-includes:
  - \usepackage{cleveref}
  
  - \newcommand\BS[1]{\text{\fontshape{n}\fontseries{bx}\selectfont#1}}
  - \newcommand\plus{\BS{+}}
  - \newcommand\minus{\BS{--}}

  - \newcommand\uncertainincrease{\vartriangle}
  - \newcommand\uncertaindecrease{\triangledown}

  - \newcommand\weakplus{\boldsymbol{\oplus}}
  - \newcommand\weakminus{\boldsymbol{\ominus}}
---
# Predicting system responses to perturbations

In Part 1 of this series we learned how to use interaction graphs and sign consistency methods
 to reason about steady states in closed systems.
In this part we add external influences to our model and answer the question
 of how a biological system responds to external influences.

## Inputs and perturbations

Most systems interact in some ways with a surrounding context i.e. their environment.
The interface to the environment is provided by variables which are not controlled by the modeled system itself but externally.
We call variables in our system which are controlled externally \emph{inputs},
and we denote the set of nodes that represent input variables with $I \subseteq V$.
Because input nodes are controlled externally, they are excluded from the sign consistency rules.

For the closed system shown in Figure \ref{fig:ig},
 there exists no single labeling $\mu: V \rightarrow \{\plus, \minus, 0\}$,
 with $\mu(a)=\plus$ and $\mu(b)=\minus$ that satisfies Rule~\ref{rule_bw} for all $v \in V$.
In other words, there exists no transition between steady states where $a$ increases and $b$ decreases.
Because $a$ is the only predecessor of $b$, between all steady states changes in $a$ and $b$ must have the same sign.

![Example of an interaction graph. Green arrows indicate positive ($\plus$) influence, red edges negative ($\minus$) influence. \label{fig:ig}](figures/paper-figure0.png )

We can interpret our model as an open system,
 were the value of $b$ is determined by the environment by declaring $b$ as an input variable.
With perturbations, we can now take control over the input variables and find out how the system behaves under different environmental conditions.
For example, we can now find out how our system reacts to a decrease in $b$.
Figure~\ref{fig:ig_labeled2} shows all labelings $\mu_i$ that satisfy Rule~\ref{rule_bw} for all $v\in V \setminus I$ with 
$I=\{b\}$ and $\mu_i(a)=\plus$ and $\mu_i(b)=\minus$. 
Input nodes are denoted with a black incoming arrow.

![A Markdown logo](figures/paper-figure9.png)
  ![A Markdown logo\label{fig:ig2}](figures/paper-figure10.png)
  ![A Markdown logo\label{fig:ig3}](figures/paper-figure11.png)
  ![A Markdown logo\label{fig:ig4}](figures/paper-figure12.png)
  ![A Markdown logo\label{fig:ig5}](figures/paper-figure13.png)

Labeled interaction graph


We see that using a perfect perturbation, a sustained decrease of $b$,
 the system can reach a quasi steady state where both $a$ and $d$ are increased.
This is a state which could not be reached in the closed system without perturbation.
While this is already an interesting reasoning mode,
 it is even more interesting to flip the question around and use this approach to do some treatment planning.
Let's see, what are the minimal perturbations that would allow the system to transition 
 into a state where $a$ and $d$ are increased?
Figure~\ref{fig:ig_labeled3} shows the potential perturbations (along with partial labelings) that allow for such a state-transition.
We can see that we have two more alternatives to reach our goal, either a direct increase in $d$ or a decrease in $c$.
 
![A Markdown logo](figures/paper-figure14.png)
![A Markdown logo\label{fig:ig5}](figures/paper-figure15.png)
![A Markdown logo\label{fig:ig5}](figures/paper-figure16.png)
Minimal perturbations of the system that can results in an increase of $a$ and $d$ (along with partial labeling)

## Perturbations and model topology

Perturbations play a major role in the analysis of biological models.
A complementary view point on perturbations is that they allow us to alter the model structure.
In particular, all incoming edges of an input node can be ignored because the node is no longer constrained by the system but by us.
A special-role play so called 0-perturbations, 
 these are perturbations were the value of a variable is kept constant over the state transition.
For those nodes the only possible label is 0,
and we can ignore their outgoing edges because they can't be responsible for any downstream changes.
It's easy to see that for complex models with many cyclic interactions such perturbations are very useful
 to investigate the influence of single components while excluding the influence of others.
In a later part, we will see how perturbations are used to design experiments that allow discriminating among alternative model topologies.

## Conclusion

In this part I introduced inputs,
and we have seen how one can model perturbations of a system.
We have seen how we can reason over possible perturbations of a system, and how to use this for treatment planning.
In the next part I will introduce a new consistency rule that allows us to handle constraints that are posed by minima or maxima of system variables.
