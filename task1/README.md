## Task 1

Read in a FASTQ file (``reads.fastq.gz``), align to germline sequences of Variable (V) and Joining (J) segments (``segments.txt``) and report V-J pair counts.

### Summary

* Each read should be aligned to all possible Variable and Joining segments.
* A single best-matching V and J segment should be selected for each read based on alignment score. If the number of bases aligned aligned to a segment is less than 15 the read should be discarded.
* A summary table holding Variable and Joining segment name and corresponding pair count should be provided as output.

### Classes and snippets

The task is performed using few basic classes from MiLib.

```java
import com.milaboratory.milib.*;

// FASTQ file reading
new SingleFastqReader();
SingleRead read;
for ((read = take()) != null) {
	...
}

// Handling reference sequences
new AminoAcidSequence();

// Alignment
Aligner.alignLocalAffine(); // performs local alignment
alignment.getScore(); // get the alignment score
alignment.getSequence2Range(); // aligned range in query, if it was supplied after reference sequence to alignLocalAffine();
```