## Task 2: Building CDR3 sequence similarity graph.

Read in clonotype table (``sample.txt.gz``) and build a graph connecting similar CDR3 sequences.

### Summary

Using human Immunoglobulin Heavy Chain data sample:

* Read in clonotype table and index clonotype CDR3 sequences using sequence tree map.
* Find all clonotype pairs that have no more than 2 mismatches, 1 insertion, 1 deletion and no more than 2 mutations total difference between CDR3 sequences.
* Report all edges connecting such clonotype pairs. Simplify the graph: remove duplicate edges, for ``a -> b, b -> c, a -> c`` cases ``a -> c`` edges should also be removed.
* *(Optional)* Visualize in R with [igraph](https://cran.r-project.org/web/packages/igraph/index.html).

### Classes and snippets

Loading and iterating through sample using VDJtools:

```java
import com.antigenomics.vdjtools.*;

// Load sample
Sample sample = SampleFileConnection.load("sample.txt");

// Iterate over sample
for (Clonotype clonotype : Sample sample) {
	...
}

// Getting clonotype CDR3 sequence
if (clonotype.isCoding()) { // ensure CDR3 sequence can be translated (!)
	clonotype.getCdr3aaBinary();
} 
```

Indexing and fuzzy search using MiLib:

```java
import com.milaboratory.milib.*;

// Create index
SequenceTreeMap<AminoAcidSequence, Clonotype> stm = new SequenceTreeMap(AminoAcidSequence.ALPHABET);

// Update index
stm.put(clonotype.getCdr3aaBinary(), clonotype);

// Query index
TreeSearchParameters treeSearchParameters = new TreeSearchParameters(...) // set the number of matches, etc for fuzzy search
NeighborhoodIterator ni = stm.getNeighborhoodIterator(clonotype.getCdr3aaBinary(), treeSearchParameters);
while (true) { // iterate over matches
    Clonotype clonotype = ni.next();
}
```