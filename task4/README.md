## Task 4: Finding enriched TCR motifs.

The problem covered by the task can be formulated as follows:

> Given a pair of samples with amino acid sequences: a sample of interest and a control with random sequences, find a group of homologous amino acid sequences in the sample of interest that has more members than expected by chance.

The solution to be implemented is based on a) building a graph of sequences, with edges connecting sequences that differ by a single mismatch, and b) counting the number of adjacent nodes for each node of a graph and looking for nodes with unexpectedly high number of neighbors.

### Plan / Subtasks

1. Compute [degrees](https://en.wikipedia.org/wiki/Degree_distribution) (number of neighbors) ``d1`` and ``d2`` for each [CDR3](https://en.wikipedia.org/wiki/Complementarity-determining_region) amino acid (CDR3aa) sequence in the ``sample.txt`` file (``cdr3aa`` column) as follows:

  * ``d1`` is the number of CDR3aa sequences from the ``sample.txt`` file that differ from a given sequence by no more than ``1`` AA substitution (i.e. Hamming distance of ``1``)
  * ``d2`` is computed the same way, but we count the number of neighbor sequences in ``control.txt`` instead; i.e. count the degree assuming that a CDR3aa from ``sample.txt`` is placed into ``control.txt``

2. Assign a ``P-value`` to the degree ``d1`` of each CDR3aa in ``sample.txt`` using the Poisson distribution with mean ``d2 / N2 * N1`` where ``N1`` and ``N2`` is the total number of sequences in ``sample.txt`` and ``control.txt`` respectively. I.e. we compute ``1 - P(1..(d1-1) | d2 / N2 * N1)``.

3. Select top ``N`` (say ``N=10``) CDR3aa sequences with the best P-value. Build a graph that includes these CDR3aa, their first neighbors in ``sample.txt``, and all possible edges with Hamming distance of ``1``. Select the largest connected component of the graph.

4. Check the specificity of the largest connected component using [VDJdb](https://vdjdb.cdr3.net/search) and visualize the position weight matrix using [Weblogo](https://weblogo.berkeley.edu).

### Guidelines

In general, you are encouraged to use existing libraries where possible, there is no need to implement every step on your own (e.g. in Java use com.google.common.graph to find connected component of a graph).

#### Java

The implementation should be written in the form of a Maven project. The actual procedure of applying steps 1. to 3. to the input files ``control.txt`` and ``samples.txt`` should be written within JUnit tests (i.e. no ``main`` method).

Third-party libraries that should be used:

* Use [milib](https://github.com/milaboratory/milib) for finding CDR3aa sequences that differ by no more than ``1`` substitution. Here is an example code snippet:

```java
import com.milaboratory.milib.*;

// Create index
SequenceTreeMap<AminoAcidSequence, Object> stm = new SequenceTreeMap(AminoAcidSequence.ALPHABET);

// Update index
stm.put(new AminoAcidSequence(str), payload);

// Query index
TreeSearchParameters treeSearchParameters = new TreeSearchParameters(...) // set the number of substitutions = 1, insertions/deletions = 0, total = 1
NeighborhoodIterator ni = stm.getNeighborhoodIterator(clonotype.getCdr3aaBinary(), treeSearchParameters);
while (ni.hasNext()) { // iterate over matches
    Object payload = ni.next();
    // rest of the logic ...
}
```

* For computing Poisson distribution P-values use ``PoissonDistribution::cumulativeProbability`` from Apache Commons Math
* For building the graph/finding connected components use the Google Guava library.

#### R/Python

**R**: the implementation should utilize ``tidyverse`` package and rely on corresponding best practices as much as possible. The implementation should be written in R markdown.

**python**: the implementation should use ``pandas``, ``numpy`` and other standard libraries. The implementation should be written in Jupyter notebook.

For graph operations use the ``igraph`` package. It is not necessery to use ``Bio*`` packages for working with sequences, e.g. ``stringdistr`` can be used to compute Hamming distances in R.
