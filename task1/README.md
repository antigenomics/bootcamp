### Task 1

Read in a FASTQ file (``reads.fastq.gz``), align them to germline sequences of Variable and Joining segments (``segments.txt``) and report summary of V-J pair count.

Each read should be aligned to all possible Variable and Joining segments. A single best-matching V and J segment should be selected for each read based on alignment score. If the number of bases aligned aligned to a segment is less than 15 the read should be discarded. A summary table holding Variable and Joining segment name and corresponding pair count should be provided as output.

```java
// FASTQ file reading
new SingleFastqReader()

// Handling reference sequences
new AminoAcidSequence()

// Alignment
Aligner.alignLocalAffine() // performs local alignment
alignment.getScore() // get the alignment score
alignment.getSequence2Range() // aligned range in query, if it was supplied after reference sequence to alignLocalAffine()
```