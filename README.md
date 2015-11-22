## Getting familiar with immune repertoire sequencing data analysis

Solutions for tasks listed in this repository are to be implemented in [Java](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) or [Groovy](http://www.groovy-lang.org/), using Java 1.8 and [Apache Maven](https://maven.apache.org/) for dependency management is recommended.

It is strongly recommended to map some of the sequencing reads using [IgBlast](http://www.ncbi.nlm.nih.gov/igblast/igblast.cgi) and [BLAT](http://genome.ucsc.edu/cgi-bin/hgBlat, and browse clonotype tables using [VDJviz](http://vdjviz.milaboratory.com) to better understand the data structure.

### Libraries

To facilitate analysis and get familiar with our coding practices the following two libraries should be used when solving tasks provided here:

* [MiLIB](https://github.com/milaboratory/milib) is a core library for working with sequencing data, nucleotide and amino acid sequences, sequence alignment and pattern matching. The library is avalable in Maven central repository.

* [VDJtools](https://github.com/mikessh/vdjtools) contains useful routines for handling immune repertoire data: parsing and handling clonotype sets. The library can be compiled from source and linked using Maven.

### Tasks

Currently 

* [Task#1](https://github.com/antigenomics/bootcamp/tree/master/task1) Reading FASTQ pairs and counting V-J junctions.

* [Task#2](https://github.com/antigenomics/bootcamp/tree/master/task2) Reading a sample and building CDR3 sequence similarity graph.

* [Task#3](https://github.com/antigenomics/bootcamp/tree/master/task3) 
