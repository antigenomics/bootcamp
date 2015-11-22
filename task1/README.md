## Task 1: Counting V-J junctions

Read in a FASTQ file (``sample.fastq.gz``), align to germline sequences of Variable (V) and Joining (J) segments (``segments.txt``) and report V-J pair counts.

### Summary

Using raw human TCR beta sequencing data:

* Align each sequencing read to all possible V and J segments using a batch aligner
* Generate a summary table with pairs of V and J segment names and corresponding count.
* *(Optional)* Visualize in R with [RCircos](https://cran.r-project.org/web/packages/RCircos/index.html).

### Classes and snippets

The task is performed using some basic classes and ``KAligner`` from MiLib:

```java
import com.milaboratory.milib.*;

// FASTQ file reading
SingleFastqReader reader = new SingleFastqReader();
SingleRead read;
for ((read = reader.take()) != null) {
	...
}

// Creating KAligner, wrapping reference sequences and adding them to the aligner
// (!) separate aligners should be created for V and J references
KAligner aligner = new KAligner(KAlignerParameters.getByName("default"));
aligner.addReference(new NucleotideSequence((String)referenceSequence, (String)referenceName));


// Alignment
KAlignmentResult result = KAligner.align(read.getData().getSequence());
String foundReferenceName = result.getBestHit().getRecordPayload(); // gets the name of the reference found
```