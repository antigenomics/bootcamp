## Task 1

Read in a FASTQ file (``reads.fastq.gz``), align to germline sequences of Variable (V) and Joining (J) segments (``segments.txt``) and report V-J pair counts.

### Summary

Using raw human TCR beta sequencing data:

* Align each sequencing read to all possible V and J segments, 
* Select top V and J matches using alignment score, discard sequencing reads in case the number of aligned bases for V or J.
* Generate a summary table with pairs of V and J segment names and corresponding count.

### Classes and snippets

The task is performed using few basic classes from MiLib:

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