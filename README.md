# Scop3D v3

 * [Project Description](#project-description)
 * [Usage](#usage)
 * [System requirements](#system-requirements)
 * [Previous version](#previous-version)
 * [Project Support](#project-support)

----

## Project Description

Scop3D (Sequence Conservation On Protein 3D structure) allows the visualization of sequence variation of a protein on its structure.

Scop3D is composed of two parts. The first part focuses on the analysis of sequence conservation or SNP variants, while the second part involves structural annotation. There is also an intermediate blast step available.

**New in version 3:** 
* added analysis of sequence SNP variants
* refreshed command line interface

### Sequence analysis

The starting point for the sequence conservation analysis is a FASTA-file which contains all sequence variants of interest. It is also possible to download sequence variants using UniprotID - the sequence will be blasted and cutoff value applied. These variants are aligned with MUSCLE. From the resulting multiple sequence alignment, the consensus sequence is constructed by retaining the most frequently found residue across all variant sequences for each position. This residue should be found more than the conservation threshold which is set be the user. Two matrices are created. The first matrix annotates the consensus sequence with the absolute abundance of each amino acid per position. In the second matrix, these numbers are converted into relative abundances in percent. Finally, a sequence logo is created with WebLogo.

The SNP variants analysis is based on Ensembl and Uniprot data, and therefore UniprotID is needed. The varians data is downloaded from the Uniprot database as well as Ensembl database. Using this info a matrix is created, annotating the protein sequence with the frequency, variants and type. Based on that the sequence is coloured accordingly.

### Structure annotation

In this part, a PDB-file is needed. This file can be obtained from the PDB or an own PDB-file can be used. If no protein structure is at hand, scop3D provides the option to retrieve a homologous structure by performing a BLAST search of the consensus sequence against the PDB. The outcome of the structure annotation is two PDB-files with altered B-values and a set of figures. The output depends wheater the sequence conservation or SNP variants analysis was performed as the first step.

For conservation analysis in the first PDB-file, the B-values are replaced by the percent variation (defined as one hundred minus the percentage conservation) at that position. In the second PDB-file, the B-values are replaced by the entropy factor.

For SNP variants analysis in the first PDB-file, the B-values are replaced by the SNP frequency at that position. In the second PDB-file, the B-values are replaced by the SNP type.

### Citation
 * [Vermeire and Vermaere et al.: Proteomics. 2015 Apr;15(8):1448-52.](http://www.ncbi.nlm.nih.gov/pubmed/25641949)
 * If you use scop3D as part of a paper, please include the reference above.

----

## Usage

Couple of typical flows are shown below:

### Sequence conservation analysis

```
# ./scop3d sequence -ent -w ~/outputdir -f sequences.fasta
# ./scop3d blast ~/outputdir/consensus.fasta
# ./scop3d structure -ent -w ~/outputdir -i 4F15
```

```
# ./scop3d sequence -ent -w ~/outputdir -u A8K2U0 -t 50
# ./scop3d structure -ent -w ~/outputdir -f 4F15.pdb -c A,C
```

### Sequence conservation analysis

```
# ./scop3d sequence -var -w ~/outputdir -u P06858
# ./scop3d blast ~/outputdir/uniprot.fasta
# ./scop3d structure -var -w ~/outputdir -i 4ACQ
```

```
# ./scop3d sequence -var -w ~/outputdir -u A8K2U0
# ./scop3d structure -var -w ~/outputdir -f 4F15.pdb
```

### Remarks

Please use -w to bundle all output/input files in one directory. The subsequent runs will search for input files in this directory.

----

## System requirements

* Python >= 2.7
* Perl >= 5
* Biopython
* Bioperl
* Ensembl Perl API
* Weblogo
* Muscle
* Emboss

----

## Previous version

The documentation for previous version of the tool (including binaries for windows, linux, mac) can be found under [https://github.com/compomics/scop3d](https://github.com/compomics/scop3d)

----

## Project Support

The scop3D project is grateful for the support by:

* [VIB Bioinformatics Core](http://www.bits.vib.be)
* [Compomics](http://www.compomics.com)
* [VIB](http://www.vib.be)
* [Ghent University](http://www.ugent.be)

[Go to top of page](#scop3d-v3)
