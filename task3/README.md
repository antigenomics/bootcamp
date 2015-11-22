## Task 3: Constructing immunoglobulin tree.

Read in a FASTQ file (``sample.fastq.gz``), align to germline sequence of Variable (V) segment and construct immunoglobulin evolution tree.

### Summary

Using raw human Immunoglobulin Heavy Chain sequencing data calculate somatic hypermutations and construct sequence hierarchy starting from most mutated sequences up to germline sequence:

* Sequencing reads should be aligned to reference using local alignment algorithm, mutations with respect to germline (ℳ) should be collected
* Identical mutation sets should be collapsed and count of each mutation set should be recorded
* The graph should be computed as follows:
  * Connect mutation sets ℳ<sub>1</sub> and ℳ<sub>2</sub> with a directed edge ``1->2`` if ℳ<sub>1</sub> ∈ ℳ<sub>2</sub>
  * Simplify graph by removing ``1->3`` edge for ``1->2,1->3`` subgraphs
  * Choose smallest mutation set 𝓂 for each subgraph
    * For each 𝓂<sub>1</sub> search for 𝓂<sub>2</sub> with highest overlap, create a virtual node with 𝓂<sub>0</sub> := 𝓂<sub>1</sub> ∩ 𝓂<sub>2</sub> and ``0->1,0->2`` edges
    * Collapse virtual nodes, leaving only unique ones
    * Repeat until the mutation set intersection is empty for all virtual node pairs or there is only one top virtual node remaining at current step
    * Assign top-level virtual node(s) to "germline" node with ``0`` mutations
* *(Optional)* Visualize in R with [igraph](https://cran.r-project.org/web/packages/igraph/index.html).

The following Variable segment reference should be used for alignment:

```md
>IGHV4-38-2*01
caggtgcagctgcaggagtcgggcccaggactggtgaagccttcggagaccctgtccctc
acctgcgctgtctctggttactccatcagcagtggttactactggggctggatccggcag
cccccagggaaggggctggagtggattgggagtatctatcatagtgggagcacctactac
aacccgtccctcaagagtcgagtcaccatatcagtagacacgtccaagaaccagttctcc
ctgaagctgagctctgtgaccgccgcagacacggccgtgtattactgtgcgaga
```

### Classes and snippets

The task is performed using some basic classes from MiLib:

```java
import com.milaboratory.milib.*;

// FASTQ file reading
new SingleFastqReader();
SingleRead read;
for ((read = take()) != null) {
	...
}

// Alignment and mutation extraction
Alignment alignment = Aligner.alignLocalAffine(
                      new AffineGapAlignmentScoring(NucleotideSequence.ALPHABET, 1, -3, -6, -1),
                      germlineSequence, readSequence); // performs local alignment
alignment.getAbsoluteMutations(); // gets the mutation set
```