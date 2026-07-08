---
layout: workshop
title: "How to clean an alignment before making a gene tree"
author: Andrew Wheeler
date:    2026-06-07
docid: 100
---

# Introduction

This recipe explains how to filter out errors from a single gene multiple sequence alignment, prior to gene tree inference, using the "CLOAK" function in Muscle5. 

# What you need

Muscle5: https://www.drive5.com/muscle/

IQ-TREE: http://www.iqtree.org/

# Example Usage

The first step is to generate an ensemble of alignments using the "stratified" option in Muscle5. This creates a set of 16 variant alignments, all output in a single ensemble fasta file, instead of a single alignment.

```
muscle -align sequences.fasta -stratified -output ensemble.efa
```

CLOAK can then generate a single filtered alignment, based on consensus among the ensemble, using the following command:

```
muscle -cloak input_ensemble_file -mincol <integer> -output <output_file_name>
```

Arguments:
- -input_ensemble_file : Path to the input alingment ensemble (EFA) file
- -mincol <integer>   : Minimum number of non-gap characters required per column
                        for that column to be retained in the output.
                        Default value of 2 if not specified
- -output <filename>  : Name of the file where the filtered MSA will be written. By default this will be {input_file_name}.cloak.fa
