---
title: "Building blocks"
date: 2021-03-26T14:36:57+13:00
draft: false
weight: 5
---

Most bioinformatic methods can be organised into a few basic concepts. I have organised these in terms of how the method influences the sequence files and how it modifies or what information is gathered from them. I use the term 'sequence file' very broadly; it can encompass anything from raw reads to assembled contigs to scaffolds to whole organelle or chromosome assemblies. I have furthur divided these into two main classes: lower-level processes and higher-level processes. These are explained in detail below.

## Lower-level building blocks

I identify three major types of lower-level processes:

1. <span style="color:red">**Pattern searching**</span> -- finding patterns within a sequence
2. <span style="color:blue">**Mapping**</span> -- pairwise alignment of a sequence against a database
3. <span style="color:green">**Clustering**</span> -- group together a collection of sequences based on identity

Each of these process types can encompass or be a part of many programs, and be applied to multiple sequence types--as outlined above. <span style="color:red">**Pattern searching**</span> is typical of early steps in most processing of raw reads, and includes adapter and primer removal, as well as quality filtering. However, it also is involved in many downstream processing steps, including searching for coding regions or CG islands on assembled contigs, or repeats across whole genome assemblies. Note that often these searches are looking for patterns based on existing references, such as adapter sequence files or repeat databases, but they can also involve looking for patterns not neccesarily dependent on any external reference, such as start and stop codons along a contig. 

For <span style="color:blue">**Mapping**</span> processes, these involve searching whole sequences against some kind of reference database. As with Pattern searching, these can involve a BLAST search of short reads or assembled contigs or aligning RNA reads to a transcriptome. Kraken, HMM

These first two processes may seem like the same thing, and indeed they are more or less two sides of the same coin. But because they are usually very separate in pipelines I am keeping them distinct. I distinguish them by what is the subject and what is the object of the search: generally Pattern searching is looking for elements of a database somewhere along a sequence (database is subject, sequence is object), wherease Mapping is searching in a database for whole sequence reads (sequence is subject, database is object). Though for many searches, especially local alignments, matches to only part of the sequence may be found, it is usually the whole sequence that is the search query. Because of the nature of both of these (especially where pattern searching is looking for shorter and often, fragmentary patterns), generally the algorithms used for both are different. 

The third type, <span style="color:green">**Clustering**</span>, 