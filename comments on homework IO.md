**IO.I-1**

The point of this exercise was two-fold. One was that you would see that log*B* *n* is very small, even for very large values of n. The other was that you should think about what realistic values of B are, so you should explicitly say something about that. Note that a OS blocksize of 4KB would actually mean that B=512, assuming elements are 8 bytes.

**IO.I-2**

Most of you got this right—the answer was (II)—but did not give a completely correct explanation. In particular, it is important to note that even when the search range is smaller than B it could still lie inside two blocks (instead of one). So to get Θ(logB n) I/Os, instead of Θ (log2 n), the internal memory must be able to hold two blocks (which is obviously true in practice).

**IO.1-3**

Many people tried to prove this by showing that MIN performs Ω(n) I/Os. This is fine if you do it correctly, but often it was stated that MIN would always keep blocks from the top M/B rows in memory (so that an I/O would always be needed for the bottom part). But this is not correct: the rows from which MIN keeps blocks in memory will shift in this algorithm.

**IO.I-4**

Many of you answered this question (mostly) correct, which was good to see because it is an important question. (By the way: the number is I/O’s in part (i) was NOT Θ(n2/B2).) Many people were sloppy in the notation for the “tiles” in part (ii). I usually did not subtract anything for this, but next time you should be more careful. 

**IO.II-1**

This was a relatively easy exercise, which most of you solved correctly, although some made the computations longer than necessary.

**IO.II-2**

This was another easy question: just refer to the permutation lower bound.

**IO.II-3**

To analyze the running time of EM-MergeSort you should write a recurrence (and explain the terms in the recurrence) and then solve it. Some people said that the result was O(n log n), because k is a constant. However, the point was to analyze the dependency on k and so you should *not* say that k is a constant. Indeed, the algorithm sets (roughly) k=M/B and in the analysis we always take M and B into account.  To improve the running time to O(n log n) you should do the merge step in a more efficient way (so it no longer needs O(nk) but something else) and then show that the new recurrence solves to O(n log n).

**IO.II-4**

What many showed correctly was that in the modified algorithm, which simulates an algorithm that uses external memory outside A, some write operations may need 5 I/Os to simulate. However, the global proof structure was often not described well. (Note:  to get to the bound of 3 times as many I/Os for the simulation, it suffices to observe that reads do not need extra I/Os, and that the number of reads is equal to the number of writes. Hence, the total number of I/Os does not increase by more than a factor 3.)   

**IO.III-1**

Most people answered part (i) correctly, although often the description of the blocking strategy was too vague. For part (ii), the proofs were sometimes also a bit vague. A good way to prove would be to argue explicitly that any subtree of size B has a root-to-leaf path of length at most log2 B, otherwise the total number of nodes would be more than 2^{ log2 B}=B. Hence, when you walk down the tree, you can escape any block after at most log2 B steps, meaning you visit at least log2 n / log2 B = logB n blocks. (Question: Can you also prove the result when we do not assume that blocks are connected  subtrees?)

**IO.III-2**

Almost everyone answered this correctly.

**IO.III-3**

The idea here was, of course, to apply Theorem 7.2 from the Course Notes. If you do so, you *do not need to write down the algorithm.* You only need

- to explain how you get a DAG in topological order (if the input is not already a DAG), namely by imagining that each edge (vi,vj) with i<j is directed from vi to vj
- to define a suitable function *f*, and prove that by computing *f* you solve the problem (here: that the *f*-values give a valid coloring)
- to explain that *f* is local (namely: *f*(vi) only depends on the in-neighbors of vi) and *to explain how*  *f*(vi) *can be computed in* O(SORT(1+|Nin(vi)|) I/Os (or O(SCAN(1+|Nin(vi)|) I/Os if this is possible)
- And then explicitly say that by Theorem 7.2 you can compute all f-values in O(SORT(|V|+|E|) I/Os.

Almost everyone just stated without explanation that the f-values in this exercise could be computed from the in-neighbors in O(SORT(1+|Nin(vi)|)  I/Os, and several even said it can be computed using O(SCAN(1+|Nin(vi)|)  I/Os. However, the latter is not true: since dmax could be very large, you cannot maintain a Boolean array of size dmax in internal memory. Hence, you must explicitly explain how you can compute *f*(vi) in O(SORT(1+|Nin(vi)|)  I/Os from the f-values of vi’s in-neighbors.

Another mistake that some people made was that they let the ordering of the nodes depend on their degrees, which is not correct. (You keep the vertices in the order in which they are already given in the adjacency list representation.)