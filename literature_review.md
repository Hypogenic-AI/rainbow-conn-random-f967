# Literature Review: Tight Bounds on the Rainbow Connection Number of Random Regular Graphs

## Research Area Overview

The **rainbow connection number** rc(G) of a connected graph G is the minimum number of colors needed for an edge-coloring under which every pair of vertices is joined by a rainbow path (a path with no repeated edge color). Introduced by Chartrand, Johns, McKeon and Zhang (2008), it has attracted substantial interest both theoretically and for networking applications.

The central open question for this research is: for a random d-regular graph G = G(n,d) with d >= 3 fixed and n -> infinity, what is the precise value of rc(G) with high probability (whp)?

**Note on research hypothesis**: The specification states rc(G) = ceil(n/d) + O(1). Based on the established literature, this formula appears to contain a transcription error. The diameter of G(n,d) is whp asymptotic to log_{d-1}(n), not n/d. The natural tight conjecture consistent with known results is rc(G(n,d)) = diam(G(n,d)) + O(1), which would mean the additive gap between rc and diameter is O(1). The "O(log n / d) gap" mentioned in the specification refers to the gap (in the current best bounds) of order log(n)/log(d). A correct restatement: the conjecture is that for d >= 5, rc(G(n,d)) = ceil(log_{d-1}(n)) + O(1) whp.

---

## Key Definitions

**Definition (Rainbow path)**: A path P in an edge-colored graph is rainbow if no two edges of P receive the same color.

**Definition (Rainbow connection number)**: For a connected graph G, rc(G) is the minimum number of colors in an edge-coloring under which every pair of vertices is joined by a rainbow path.

**Definition (Strong rainbow connection number)**: src(G) is the minimum number of colors needed so that every pair of vertices is joined by a rainbow geodesic (shortest path that is rainbow). We always have diam(G) <= rc(G) <= src(G).

**Definition (Random r-regular graph G(n,r))**: A graph drawn uniformly at random from all r-regular graphs on n labeled vertices (well-defined when nr is even).

**Definition (w.h.p.)**: An event holds with high probability if its probability tends to 1 as n -> infinity.

**Definition (Diameter diam(G))**: The maximum distance between any two vertices.

**Definition (Radius rad(G))**: The minimum eccentricity over all vertices.

**Definition (Configuration model)**: A pairing model for constructing random regular graphs (Bollobas 1980) in which each vertex i has r "half-edges" (points), and edges are formed by a uniform random perfect matching on the rn points. Any event holding w.h.p. in this model also holds w.h.p. in G(n,r) for constant r.

**Definition (Edge-splitting)**: A decomposition of a graph G into edge-disjoint spanning subgraphs G1 and G2.

**Definition (Tree-like vertex)**: A vertex x in G(n,r) is tree-like if the ball of radius k_r around x (with k_r = log_{r-1}(K1 log n)) is a tree.

---

## Key Papers

### Paper 1: Rainbow Connection of Random Regular Graphs
- **Authors**: Andrzej Dudek, Alan Frieze, Charalampos E. Tsourakakis
- **Year**: 2013 (arXiv: 1311.2299)
- **Main Result**: **Theorem 1**: For r >= 4 constant, w.h.p. rc(G(n,r)) = O(log n). The case r = 3 was left open.
- **Lower Bound**: diam(G(n,r)) = (1+o(1)) * log_{r-1}(n) w.h.p. (Bollobas-Fernandez de la Vega 1982), so rc >= (1+o(1))*log_{r-1}(n), meaning the O(log n) bound is tight up to a hidden constant.
- **Proof Technique**: Random greedy coloring using q = ceil(K1^2 * r * log n) colors. The key steps are:
  1. Define k_r = log_{r-1}(K1 log n); the ball of radius k_r around most vertices is a tree.
  2. Assign colors greedily to edges, choosing uniformly from colors not used by edges within distance k_r. This ensures each root-to-leaf path in T_x is rainbow.
  3. Use **Lemma 2** (rainbow matching in d-ary trees): For d >= 3, any two vertex-disjoint rainbow complete d-ary trees T1, T2 with ell levels satisfy m(T1,T2) >= d^{2ell}/4, where m counts leaf-pairs whose combined root-to-leaf paths are rainbow.
  4. Grow trees from x and y to size n^{1/20}, then use a path-finding argument with BFS trees of size n^{3/5} to connect them.
  5. Probability that none of n^{1/21} disjoint candidate paths is rainbow is o(n^{-3}).
- **Key Lemmas**:
  - **Lemma 2**: For two vertex-disjoint rainbow d-ary trees T1, T2 with ell levels (d >= 3): kappa_{ell,d} = min m(T1,T2) >= d^{2ell}/4.
  - **Lemma 3**: Stronger version allowing partial repetitions within distance floor(L/2); gives kappa_{L,d} >= (1 - L^2/d^{floor(L/2)} - sum_{i=1}^{floor(L/2)} i/d^i) d^{2L}.
  - **Corollary 4**: For d >= 3 and L large enough, there exist S_i ⊆ L_i and a bijection f: S1 -> S2 with |S_i| >= d^{L/10} such that the concatenated path P_{x,T1} ∪ P_{f(x),T2} is rainbow for all x in S1.
  - **Lemma 5**: W.h.p., (a) no set of s <= t0 = (1/10)*log_{r-1}(n) vertices has more than s edges; (b) at most log^{O(1)}(n) vertices lie within distance k_r of a cycle of length <= k_r.
- **Obstacle for r=3**: Lemma 2 fails for d=2 (binary trees). The example in Figure 1 shows kappa_{ell,2} <= 2^ell, not Omega(2^{2ell}) as needed. An argument of Alon gives |S_i| = Omega(2^ell) pairs, yielding O((log n / log log n)^2) colors.
- **Relevance**: This is the foundational paper for the random regular graph setting with d >= 4.

### Paper 2: Some Remarks on Rainbow Connectivity
- **Authors**: Nina Kamcev, Michael Krivelevich, Benny Sudakov
- **Year**: 2015 (arXiv: 1501.00821)
- **Main Results**:
  - **Theorem 1.1**: For connected n-vertex G with min degree delta >= 4: rc(G) <= 16n/delta.
  - **Theorem 1.2** (Key result): For r >= 5, there is an absolute constant c such that rc(G_{n,r}) <= c*log(n)/log(r) w.h.p. This bound is **asymptotically tight** since diam(G_{n,r}) ~ log(n)/log(r-1) ~ log(n)/log(r).
  - **Theorem 1.3**: For r-regular G with edge expansion >= epsilon*r and r >= max{64*epsilon^{-1}*log(64*epsilon^{-1}), 324}: rc(G) = O(epsilon^{-1} * log n).
  - **Theorem 1.4**: whp rvc(G_{n,r}) <= c*log(n)/log(r) for r >= 28.
- **Key Proof Technique**: The **Edge-Splitting Lemma** (Lemma 2.1):
  - *Lemma 2.1*: If G has two connected spanning subgraphs G1, G2 with |E1 ∩ E2| <= c, then rc(G) <= diam(G1) + diam(G2) + c.
  - *Proof idea*: Color intersection edges distinctly; color remaining edges by BFS-distance level in G1 (colors a_j) and G2 (colors b_j). Any two vertices x1, x2 share rainbow BFS paths to the root; if edge-disjoint they concatenate; otherwise a detour through shared (intersection) edge suffices.
  - For Theorem 1.2 (r >= 6): Use contiguity G_{n,r} ≈ G_{n,r1} ⊕ G_{n,r2} (Janson; Robinson-Wormald). Split into two independent r_i-regular random graphs G1, G2. Each has diameter ~ (1+o(1))*log(n)/log(r_i-1) <= c*log(n)/(2*log r). Splitting lemma gives rc <= c*log(n)/log(r).
  - For r=5: Use G_{n,5} ≈ G_{n,1} ⊕ H_n ⊕ H_n and show each half has O(log n) diameter via Proposition 2.4 (Bollobas-Chung: Hamiltonian cycle + random perfect matching has diameter (1+o(1))*log_2(n) w.h.p.).
- **Significance**: This paper gives the asymptotically tight constant (up to a multiplicative constant), reducing the gap from O(log n) to O(log n / log r). The current gap to the exact diameter is a multiplicative constant c.

### Paper 3: Rainbow Connectivity of Sparse Random Graphs
- **Authors**: Alan Frieze, Charalampos E. Tsourakakis
- **Year**: 2012 (arXiv: 1201.4603)
- **Main Results**:
  - For G(n,p) at connectivity threshold: rc(G) ~ max{Z_1, log n / log log n} whp (where Z_1 = number of degree-1 vertices).
  - For G(n,r) (r >= 4): rc(G) = O(log^{2*theta_r}(n)) where theta_r = log(r-1)/log(r-2).
  - For r=3: rc(G(n,3)) = O(log^4(n)) whp.
- **Key Technique**: The general proof strategy (sketch): grow trees T_x, T_y from each vertex to depth k (well-chosen); find leaf-correspondence f; grow further to depth ~half-diameter; find edge connecting a leaf of BFS-tree from u (leaf of T_x) to a leaf of BFS-tree from f(u) (leaf of T_y); at least one of these paths is rainbow.
- **Note**: This was the first paper on rainbow connectivity of random regular graphs; the exponent was later improved significantly.

### Paper 4: A Note on the Rainbow Connection of Random Regular Graphs
- **Authors**: Michael Molloy
- **Year**: 2017
- **Main Result**: rc(G(n,3)) = O(log n) whp. This completes the case r=3 left open by Dudek-Frieze-Tsourakakis.
- **Significance**: Uses Alon's argument for binary trees (which yields S_i of size Omega(2^ell) instead of Omega(4^ell)) with a more careful analysis. The result shows the same O(log n) bound holds for all r >= 3.

### Paper 5: On the threshold for rainbow connection number r in random graphs
- **Authors**: Annika Heckel, Oliver Riordan
- **Year**: 2013 (arXiv: 1307.7747)
- **Main Results**: For G = G(n,p) and r >= 3:
  - **Conjecture 1**: p*(n) = (C*log n)^{1/r} / n^{1-1/r} with C = r^{r-2}/(r-2)! is the sharp threshold for rc(G) <= r.
  - **Theorem 2**: For r >= 3, p = (C(1+eps)*log n)^{1/r} / n^{1-1/r} implies rc(G(n,p)) = r whp.
  - Lower bound: (2*log n)^{1/r} / n^{1-1/r} is a lower bound for the sharp threshold of {rc(G) <= r}.
- **Relevance**: Studies the regime where rc is a small constant (relevant to non-fixed-d case); different model but related techniques.

### Paper 6: Rainbow Connections of Graphs – A Survey
- **Authors**: Xueliang Li, Yuefang Sun
- **Year**: 2011 (arXiv: 1101.5747)
- **Main Content**: Comprehensive survey covering:
  - Basic results: rc(C_n) = src(C_n) = ceil(n/2); rc(G) = 1 iff G is complete; rc(G) = |E(G)| iff G is a tree.
  - Bounds: diam(G) <= rc(G) <= src(G) <= |E(G)|.
  - Chandran-Das-Rajendraprasad-Varma (2012): rc(G) <= 3n/(delta+1) + 3 for min-degree delta >= 1 (essentially tight).
  - Krivelevich-Yuster (2010): rc(G) <= 20n/delta.
  - Basavaraju-Chandran-Rajendraprasad-Ramaswamy: rc(G) <= rho*(rho+2) where rho is the radius of G (bridgeless G).
- **Relevance**: Foundation survey; gives all known exact values and bounds.

---

## Known Results (Prerequisite Theorems)

### Diameter of Random Regular Graphs

**Theorem (Bollobas, Fernandez de la Vega 1982)**: For fixed r >= 3, the diameter of G(n,r) satisfies diam(G(n,r)) = (1+o(1)) * log_{r-1}(n) whp.

More precisely, by work cited in Kamcev et al. (Theorem 1.2 proof):
diam(G_{n,r}) ~ log(n) / log(r-1) whp for r >= 3.

This is the fundamental lower bound for rc(G(n,r)).

### Upper Bounds for rc in Terms of Degree

**Theorem (Chandran-Das-Rajendraprasad-Varma, J. Graph Theory 2012)**: For connected G with min-degree delta >= 1: rc(G) <= 3n/(delta+1) + 3. This is essentially tight.

**Theorem (Krivelevich-Yuster, J. Graph Theory 2010)**: rc(G) <= 20n/delta for connected G.

**Theorem (Basavaraju-Chandran-Rajendraprasad-Ramaswamy, Graphs Combin. 2014)**: For bridgeless G: rc(G) <= rho*(rho+2) where rho = rad(G). Since rad(G(n,r)) = O(log n), this gives rc = O(log^2 n) for random regular graphs.

### Bounds for rc of Random Regular Graphs (chronological)

| Year | Authors | Result | Range |
|------|---------|--------|-------|
| 2012 | Frieze-Tsourakakis | rc(G(n,r)) = O(log^{2*theta_r} n), theta_r = log(r-1)/log(r-2) | r >= 3 |
| 2013 | Dudek-Frieze-Tsourakakis | rc(G(n,r)) = O(log n) | r >= 4 |
| 2015 | Kamcev-Krivelevich-Sudakov | rc(G(n,r)) <= c*log(n)/log(r) (tight up to const) | r >= 5 |
| 2017 | Molloy | rc(G(n,3)) = O(log n) | r = 3 |

**Lower bound (all r >= 3)**: rc(G(n,r)) >= diam(G(n,r)) = (1+o(1))*log_{r-1}(n) = (1+o(1))*log(n)/log(r-1).

**Current gap**: The multiplicative constant between upper bound c/log(r) and lower bound 1/log(r-1) is exactly c * log(r-1)/log(r) = c * (1 + log(1-1/r)/log r) = c + O(1/r) for large r. For fixed r, the ratio is a constant C(r) > 1. Determining C(r) for each r, and in particular whether it can be taken as 1 (i.e., rc(G) = diam(G) + O(1)), is the central open problem.

### Configuration Model Properties

**Theorem (Bollobas 1980)**: For constant r, if an event holds w.h.p. in the random pairing model, it holds w.h.p. in G(n,r).

**Lemma (Density of small sets in G(n,r))**: Dudek-Frieze-Tsourakakis Lemma 5: w.h.p.
- No set of s <= t0 = (1/10)*log_{r-1}(n) vertices contains more than s edges.
- At most log^{O(1)}(n) vertices lie within distance k_r of a short cycle.

### Contiguity Results for Random Regular Graphs

**Theorem (Janson 1995; Robinson-Wormald 1994)**: G_{n,r+r'} is contiguous with G_{n,r} ⊕ G_{n,r'} (edge-disjoint union). Also G_{n,r+2} is contiguous with G_{n,r} ⊕ H_n (H_n = random Hamiltonian cycle).

**Proposition (Bollobas-Chung 1988)**: The union of an n-cycle and a random perfect matching on [n] has diameter whp (1+o(1)) * log_2(n).

### Chernoff Bounds

Standard tail bounds used throughout: for X ~ Bin(n,p):
- Pr(X <= alpha*np) <= exp(-(1-alpha)^2 * np/2) for 0 <= alpha <= 1.
- Pr(X >= alpha*np) <= (e/alpha)^{alpha*np} for alpha >= 1.

---

## Proof Techniques in the Literature

### 1. Random Greedy Coloring (Dudek-Frieze-Tsourakakis 2013)
Assign edge colors online via a greedy random procedure. Order edges e_1, ..., e_m. Color e_i uniformly at random from colors not appearing on edges within distance k_r in the line graph. This uses O(K1^2 * r * log n) colors but ensures rainbow root-to-leaf paths in all local BFS trees.

**Applicability**: Works for r >= 4 where local trees are binary (branching factor >= 3). Fails for r=3 because binary trees (branching factor 2 in leaves) do not support the leaf-matching construction.

### 2. Edge-Splitting + Contiguity (Kamcev-Krivelevich-Sudakov 2015)
Decompose G into two edge-disjoint spanning subgraphs G1, G2 each with small diameter. Apply Lemma 2.1 to get rc(G) <= diam(G1) + diam(G2). For G(n,r), use contiguity to decompose into two r/2-regular graphs, each with diameter ~ log(n)/log(r/2-1) ~ 2*log(n)/log(r).

**Applicability**: Gives asymptotically tight result with correct log(r) dependence. Requires r >= 5 for the contiguity argument to work directly. This approach is simpler and yields a better constant.

### 3. Path-Growing + Edge Probability (Frieze-Tsourakakis 2012)
Grow trees T_x, T_y of depth ~ log(diam)/2 from each vertex, then grow n^{3/5}-leaf BFS subtrees from the leaves. Use edge probability to show connected leaf-to-leaf edge exists, then argue that one of n^{1/21} candidate paths is rainbow.

### 4. Random Coloring + Recoloring (Heckel-Riordan 2013)
For G(n,p): randomly color all edges; identify "dangerous pairs" (not joined by enough rainbow paths); recolor carefully to fix dangerous pairs without disturbing others.

**Key Lemma**: The dangerous pairs can be fixed greedily because they form a sparse structure that allows conflict-free recoloring.

### 5. Expansion-Based Approach (Kamcev et al. Theorem 1.3)
Decompose an expander G into two subgraphs via the Frieze-Molloy random splitting theorem (using Lovász Local Lemma). Each subgraph is also an expander, hence has logarithmic diameter. Apply edge-splitting lemma.

**Applicability**: Works for any r-regular graph with good expansion; in particular G(n,r) for r >= 5. Potentially applicable to quasi-random graphs more generally.

---

## Related Open Problems

1. **Exact constant for r >= 5**: Is rc(G(n,r)) = (1+o(1)) * log_{r-1}(n) for all r >= 5? I.e., does rc(G) = diam(G) + O(1)?

2. **Case r = 3 tightened**: Molloy (2017) gives O(log n) for r=3, but the constant is unclear. Can the sharp constant be identified?

3. **Case r = 4**: Neither Dudek et al.'s r=3 issue nor Kamcev et al.'s r=5 lower bound apply cleanly. The best known upper bound for r=4 is O(log n) by Dudek et al.

4. **Threshold for rc(G) = d in G(n,p)**: Heckel-Riordan Conjecture 1 proposes the sharp threshold; the upper bound direction is proven; the lower bound remains conjectural.

5. **Strong rainbow connection src(G(n,r))**: Is it also Theta(log n / log r)?

6. **Growing r**: The case r = r(n) -> infinity with n is only partially addressed. Kim-Vu sandwiching can handle some of this range.

---

## Gaps and Opportunities

### Gap 1: Additive constant from diameter
The biggest gap is the multiplicative constant between rc(G(n,r)) and diam(G(n,r)). Both are Theta(log n / log r) but the ratio c = lim sup rc / diam is unknown. The conjecture is c = 1 (rc = diam + O(1)).

**Why it's hard**: The edge-splitting approach gives 2 * diam(G_{r/2}) ≈ 2 * diam(G_r) * log(r-1)/log(r/2-1) which approaches 2 for large r, not 1. To get the right constant 1, a fundamentally different approach is needed.

### Gap 2: Lower bound for r >= 4
Currently only the diameter lower bound is known. The research hypothesis asks whether one can prove rc(G) >= diam(G) (which is trivial) AND that the upper bound matches it. The challenge is proving the upper bound is at most diam(G) + O(1).

### Gap 3: Exact formula for finite r
For specific values r in {3, 4, 5}, the exact leading coefficient of log(n)/log(r-1) in rc(G(n,r)) is unknown.

---

## Recommendations for Proof Strategy

### Most Promising Approach: Tight Edge-Splitting with Diameter Matching

The Kamcev-Krivelevich-Sudakov edge-splitting approach (Lemma 2.1) gives rc(G) <= diam(G1) + diam(G2). To achieve rc(G) = diam(G) + O(1), one needs:

**Goal**: Find spanning subgraphs G1, G2 with very small |E1 ∩ E2| such that diam(G1) + diam(G2) is at most diam(G) + O(1).

This seems impossible naively since diam(G1) >= diam(G) typically. A modification: use a spanning TREE T of G as G1, and a few edges as G2. A spanning tree of G(n,r) has diameter O(log n) but the exact constant matters.

**Alternative**: Use a BFS tree T rooted at any vertex; T has depth exactly diam(G) and diameter at most 2*diam(G). Use the remaining edges as G2. The edge-splitting lemma gives rc(G) <= diam(T) + diam(G') + 0 = O(log n) but possibly not tight.

### Alternative: Direct Probabilistic Argument on Paths

For each pair of vertices x,y, the number of paths of length diam(G)+k (for small constant k) in G(n,r) grows like (r-1)^{diam+k}. If a random coloring uses q = diam(G) + O(1) colors and each path has probability ~1/q! of being rainbow, the expected number of rainbow paths is roughly (r-1)^{diam+k} / q!. For this to be polynomial in n (allowing union bound), we need:

(r-1)^{diam(G)+k} / (diam(G)+O(1))! >= n^2.

Since (r-1)^{diam(G)} ~ n and diam(G)! ~ (diam(G)/e)^{diam(G)}, this requires careful analysis.

### Key Prerequisites to Establish
1. The exact diameter distribution of G(n,r) (not just asymptotics, but concentration).
2. The number of paths of given length in G(n,r) (expansion / eigenvalue bounds from Alon).
3. New rainbow matching argument for trees that improves Corollary 4 to give |S_i| = d^{L/10} for L = diam(G) instead of L = k_r = Theta(log n).

### Computational Tools
- NetworkX (Python) for small-scale experiments on random regular graphs.
- SageMath for algebraic computations.

---

## Summary of Current State

| Quantity | Value (w.h.p.) | Source |
|----------|---------------|--------|
| diam(G(n,r)) | (1+o(1)) * log_{r-1}(n) | Bollobas-Fernandez de la Vega 1982 |
| rc(G(n,r)) lower bound | (1+o(1)) * log_{r-1}(n) | trivial from diameter |
| rc(G(n,r)) upper bound (r>=5) | c * log(n)/log(r) for some c | Kamcev et al. 2015 |
| rc(G(n,r)) upper bound (r=4) | O(log n) | Dudek-Frieze-Tsourakakis 2013 |
| rc(G(n,3)) upper bound | O(log n) | Molloy 2017 |
| Multiplicative gap (r>=5) | c * log(r-1)/log(r) | between bounds |
| Additive gap (r>=5) | Unknown; conjectured O(1) | open |
