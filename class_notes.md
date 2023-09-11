# CS 402 Class Notes

most supervised learning when ppl talk about

## ethics

- Mill's utilitarianism:
    maximize benefit for everyone, mostly equally

    bane:
    - conflict of interest
    - personal benefit
- Kant's formalism/ duty ethics:
    unconditional command for every individual

    bane: universal principle may harm specific people
- Locke's Right Ethics:
    individual has right simply by existence

    bane: what to do when two people's rights conflict
- Aristotle's virtue ethics:
    objective goodness from human qualities

    bane: how to find the "golden mean"

the golden rule (all above agrees with)

> Do unto others as you would have others do unto you

### codes of ethics

statements of general principles, followed by instructions for specific conduct

defiens duties the professional owes to
society/employers/clients/colleagues/subordinates/profession/self

### engineering design process

1. recognize problem/need, gather information
1. define problem/goal
1. generate/propose solution/method
1. evaluate benefit&cost of alternatives

### handling ethical issues

1. correct the problem
1. whistle blowing
1. resign in protest

## definition of artificial intelligence

- humanly → acting
- ration → math/theory

### Turing test

- NLP
- knowledge representation
- automated reasoning
- ML

#### total Turing test

perceptional abilities

- computer vision
- robotics

### thinking humanly

- get inside the working of human mind
- general problem solver
- cognitive science

### thinking rationally

- correctness
- logic
- fact-check

### knowledge-based system

- general-purpose search
- domain-specific knowledge
- knowledge bottleneck

## intelligent agent

### rational agent

1. prior knowledge of environment
1. performable action
1. performance measurement
1. perception

### task environment

PEAS: performance measurement, environment, actuators, sensors

properties

1. fully/partially observable
1. single/multiple agent
1. deterministic/stochastic
1. episodic/sequential
1. static/dynamic
1. known/unknown

### agent structure

- function: perception → action
- architecture: sensory → actuator

#### table-driven structure

$$
n_{entry}=\sum_{t=1}^T|P|^T
$$

- simplest
- e.g. industrial robot
- #cases explode

#### simple reflex agent

match input against rule, return action

- model-based: only work for fully observable
- goal-based
- utility-based: maximize gain expectation

## search

- breadth/depth first

## example application

### collaborative perception

- share raw data → huge overhead
- extract feature
- share object position

### anomaly detection

- bidirectional optimization

### uninformed search

- backtracking search

#### breadth-first search

- complete: will find shallowest goal if graph has finite depth
- optimal if path cost $g(n)$ is non-decreasing of depth $d$
- $O(b^d)$ where $b$ is branching factor

#### uniform-cost search

expand node with least path cost $g(n)$

- optimal
- $O(b^{1+\lfloor C^*/\epsilon\rfloor})$ where every action cost $≥\epsilon$

#### informed search (heuristic search)

#### A\* search (A-star search)

- cost $f(n)=g(n)+h(n)$
    - cost to reach node $g(n)$
    - estimated cost to goal, heuristic, $h(n)$
- optimal if $h(n)$ is admissible in tree search
    - admissibility: never overestimate
- optimal if $h(n)$ is consistent in graph search
    - consistency: triangle inequality $h(n)≤c(n,a,n')+h(n')$
- optimally efficient if $h(n)$ is consistent:
    expand fewest node among optimal algorithm

## reinforcement learning

- control system

### dynamic programming

- key: sub-problem

example

- Dijkstra's algorithm: per node
- Bellman-Ford algorithm: per hop

### Markov decision process (MDP)

finite tuple $\{S,A,\{P_{sa}\},\gamma,R\}$

- space $S$
- action $A$
- state transition probabilities $P_{sa}$
- discount factor $\gamma\in[0,1)$
- reward function $R$: evaluation metric
- total payoff. maximize this

    $$
    \sum_i \gamma^iR(S_i)
    $$

- policy $\pi:s\mapsto a$. find this

#### find optimal policy

optimal policy $\pi^*$

$$
\pi^*=\argmax_a \sum_{s'}P_{sa}(s')V^*(s')
$$

- mapping state to expected total payoff $V^\pi:s\mapsto\R$

    $$
    V^\pi(s)=\mathbb E\left[
        \sum_i\gamma^iR(S_i)\Bigr|s_0=s
    \right]=
    \mathbb E\left[
        [R(s)]+\gamma V^\pi(s')
    \right]\\[12pt] ⇒
    V^\pi(s)=R(s)+\gamma\sum_{s'}P_{s\pi(s)}(s')V^\pi(s')
    $$

    Bellman equation

##### value iteration

1. $V(s):=0$
1. Bellman update: $∀\ s,$

    $$
    V(s):=R(s)+\max_a\gamma\sum_{s'}P_{sa}(s')V(s')
    $$

- linear system
- Bellman back operator $V':=B(V)$
- sync/async update
- $\gamma$ force $V$ to converge $V^*$ exponentially

##### policy iteration

1. random $\pi$
1. repeat:

    $$
    V:=V^\pi\qquad\text{by Bellman equation}\\
    \pi(s):=\argmax_a\sum_{s'}P_{sa}(s')V(s')
    $$

- when converge, guarantee optimal policy
- high complexity: linear system very step

##### exploration and exploitation

- $\varepsilon$-greedy

    $$
    a=\begin{cases}
        \argmax V&probability\ 1-\varepsilon\\
        random a\in A&probability\ \varepsilon
    \end{cases}
    $$

    - $\varepsilon$ is small and decrease
- softmax
