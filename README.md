# ChromoPainter_AncientDNA


In the paper named "[Ancient Rome: A genetic crossroads of Europe andthe Mediterranean](https://science.sciencemag.org/content/366/6466/708)", the authors used the ChromoPainter on ancient individuals to calculate haplotype sharing between ancient Italian individuals and present-day
population, and to reveal fine population genetic structure.

Here, I am trying to repeat their ChromoPainter analysis, and we can use this method to do similar analysis on ancient DNA in the future.


The author deposited their raw sequencing data at European Nucleotide Archive (ENA) with accession [no.PRJEB32566](https://www.ebi.ac.uk/ena/data/view/PRJEB32566). Samples in this repository include 127 from Rome and Central Italy, as well as 7 from Sardinia (Bronze/Copper Age) that were not reported in the study. They performed whole-genome sequencing to a median depth of 1.05× genome-wide coverage (range 0.4 to 4.0×, [TableS2](data/aay6826_Tables_S1_to_S4.xlsx)).



The indexed bam files (the bam file ```*.bam``` and the index file of the bam ```*.bam.bai```) can be download for each individuals from [PRJEB32566](https://www.ebi.ac.uk/ena/data/view/PRJEB32566) using the following commands in your terminal at designated directory, take downloading sample R7 for example：

```
wget ftp.sra.ebi.ac.uk/vol1/run/ERR355/ERR3559063/R7.bam
```
```
wget ftp.sra.ebi.ac.uk/vol1/run/ERR355/ERR3559063/R7.bam.bai
```
All links for ```.bam``` and ```.bam.bai``` can be found in [PRJEB32566.txt](data/PRJEB32566.txt).

