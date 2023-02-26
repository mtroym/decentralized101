# Chapter Zero: Step into BlockChain

## Merkle Tree.
1. Collision-resistant Function(CRF) 
   -  A function 
     $$H: \mathrm{M} \rightarrow \mathrm{T}, \mathrm{s.t.}  \forall x,y \in \mathrm{M}, x \neq y, H(x) \neq H(y)$$
   -  Hash fuction, eg. SHA256
   -  If Bob has $m^\prime \Rightarrow h=H(m^\prime)$, and Alice gives $h=H(m)$, then Bob can conclude that $m=m^\prime$
2. Merkle Tree Proof(Merkle 1989)
   - We denote **Merkle Hash Tree** as $\mathrm{MHT}$, A extend of CRF, but takes a sequence $S =(x_1, x_2, \cdots, x_n)$ as input. 
   - Alice posts $\mathrm{MHT}(S) = h$. If Bob has an input $x_i$ and a proof denoted as $\mathbb{\pi_i}$, which can verify that $x_i$ is $i$th input of $S$.
   - Merkle Tree Structure:
     - Is a Bi-Tree of leaves count $n$, height $\log_2n$, each node has an output of CRF Hash function $H$. For example, a node $y_k = H(m_i, m_j)$
     - A very simple graph example:
       - `m_i` denote hash of some data `x_i`, which is `m_i = H(x_i)`.
       - `h_1 = H(m_1, m_2), h_2 = H(m_3, m_4)` and `root = h = H(h_1, h_2)`;
       - Given proof `p_2 = proof(x_2) = (m_1, h_2)`, We can get:
       - to verify if `root == H(H(m_1, H(x_2)), h_2)`
   - Verify Function can be denoted as $\mathrm{verify}(h, i, x_i, \pi_i) \rightarrow \{0, 1\}$
   - Application: Proof of Work as in Bitcoin
     - Define $D$ as difficulty, find $x \in X, st. H(x, y) < \frac{2^n}{D}$ where $y$ is the last block hash.
     - In Bitcoin, `H(x, y)=SHA256(SHA256(x.y))`
   - > **Theorem A (Merkle trees are collision-resistant)**: It is unfeasible to find two sets of leaves $S =(x_1,x_2,\cdots,x_n)$ and $S^\prime =(x^{\prime}_1,x^{\prime}_2,\cdots,x^{\prime}_n)$ such that $S\neq S^\prime$ but $\mathrm{MHT}(S)=\mathrm{MHT}(S^\prime)$
   
   - To prove above theorem, we can prove even stronger one below. A proof can be [checked here](https://decentralizedthoughts.github.io/2020-12-22-what-is-a-merkle-tree/)

   - > **Theorem B (Merkle proof consistency)**: It is unfeasible to output a Merkle root $h$ and two "inconsistent" proofs $\pi_i$ and $\pi_i^{\prime}$ for two different inputs $x_i$ and $x_i^\prime$ at the $i$th leaf in the tree of size $n$.

## Digital Signitures.
1. Use a secret key to sign a file, and use paired public key to verify accept or reject.
    - Triple of algorithm
      - `pk, sk = Gen()`
      - `sign = Sign(sk, msg)`
      - `is_accept = Verify(pk, msg, sign)` 
    - Signature Schemes: 
      - RSA signatures, 
      - Discrete-log signatures(Schnorr, ECDSA), 
      - BLS signature, 
      - Post-quantum signature.


## Simple Consensus.
1. Byzantine Generals Problem.(Lamport etal. 1982)
   - Problem Statement: 
     - There are $n$ generals, one of which is *commander*. Some of which are *loyal*, while some of which are *traitors* (including the commander)
     - To model this problem. 
        1. Generals: Nodes, 
        2. Commander: Leader 
        3. Loyal: Honest, Traitor: **Adversary**.
     - The **Adversary Nodes** can have 
        1. Crash faults(close node), 
        2. Omission faults(select which to send/receive), 
        3. Byzantine faults.(deviate)


### reference
1. [What is a Merkle Tree?, Alin Tomescu, 20221222](https://decentralizedthoughts.github.io/2020-12-22-what-is-a-merkle-tree/)
2. [Lecture 1 of CS251 Fall 2022](https://cs251.stanford.edu/lectures/lecture1.pdf)
3. [Lecture 4 of CS251 Fall 2022](https://cs251.stanford.edu/lectures/lecture1.pdf)