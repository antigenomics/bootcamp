## Demonstrating the ability to solve basic computational tasks arising in immune repertoire sequencing data analysis

This repository contains several tasks that are used to demonstrate the ability to understand and use basic functionality of our immune repertoire sequencing data analysis API, as well as decent coding skills. Each task folder contains all required data files in plain-text, [FASTQ](https://en.wikipedia.org/wiki/FASTQ_format) and [VDJtools clone set](http://vdjtools-doc.readthedocs.org/en/latest/input.html#vdjtools-format) formats.

Solutions for tasks listed in this repository are to be implemented in [Java](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) or [Groovy](http://www.groovy-lang.org/), using Java 1.8 and [Apache Maven](https://maven.apache.org/) for dependency management is recommended.

> Note:

> -- It is recommended to map some of the sequencing reads using [IgBlast](http://www.ncbi.nlm.nih.gov/igblast/igblast.cgi) and [BLAT](http://genome.ucsc.edu/cgi-bin/hgBlat), and browse clonotype tables using [VDJviz](http://vdjviz.milaboratory.com) to better understand the data structure.

> -- It is also highly recommended to fork this repository and submit solutions as **pull requests**. In such case, provide some minimal unit test coverage for your source code and set up [Travis](https://travis-ci.org/) continuous integration system to automatically generate pull request build status.

### Libraries

To facilitate implementation and get familiar with our coding practices the following two libraries should be used when solving tasks provided here:

* [MiLIB](https://github.com/milaboratory/milib) is a core library for working with sequencing data, nucleotide and amino acid sequences, sequence alignment and pattern matching. The library is avalable in Maven central repository.

* [VDJtools](https://github.com/mikessh/vdjtools) contains useful routines for handling immune repertoire data: parsing and handling clonotype sets. The library can be compiled from source and linked using Maven.

### Tasks

Currently available tasks:

* [Task#1](https://github.com/antigenomics/bootcamp/tree/master/task1) Counting V-J junctions.

* [Task#2](https://github.com/antigenomics/bootcamp/tree/master/task2) Building CDR3 sequence similarity graph.

* [Task#3](https://github.com/antigenomics/bootcamp/tree/master/task3) Constructing immunoglobulin tree.

---

...

![FMJ](https://i.ytimg.com/vi/GTQAXX08A-s/maxresdefault.jpg)