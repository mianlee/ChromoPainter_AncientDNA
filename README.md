# ChromoPainter_AncientDNA


In the paper named "[Ancient Rome: A genetic crossroads of Europe andthe Mediterranean](https://science.sciencemag.org/content/366/6466/708)", the authors used the ChromoPainter on ancient individuals to calculate haplotype sharing between ancient Italian individuals and present-day
population, and to reveal fine population genetic structure.

Here, I am trying to repeat their ChromoPainter analysis, and we can use this method to do similar analysis on ancient DNA in the future.

## Download raw data that used in Ancient Rome paper

The author deposited their raw sequencing data at European Nucleotide Archive (ENA) with accession [no.PRJEB32566](https://www.ebi.ac.uk/ena/data/view/PRJEB32566). Samples in this repository include 127 from Rome and Central Italy, as well as 7 from Sardinia (Bronze/Copper Age) that were not reported in the study. They performed whole-genome sequencing to a median depth of 1.05× genome-wide coverage (range 0.4 to 4.0×, [TableS2](data/aay6826_Tables_S1_to_S4.xlsx)).



The indexed bam files (the bam file ```*.bam``` and the index file of the bam ```*.bam.bai```) can be download for each individuals from [PRJEB32566](https://www.ebi.ac.uk/ena/data/view/PRJEB32566) using the following commands in your terminal at designated directory, take downloading sample R7 for example：

```
wget ftp.sra.ebi.ac.uk/vol1/run/ERR355/ERR3559063/R7.bam
```
```
wget ftp.sra.ebi.ac.uk/vol1/run/ERR355/ERR3559063/R7.bam.bai
```

Links for all ```*.bam``` and ```*.bam.bai``` files can be found in [PRJEB32566.txt](data/PRJEB32566.txt). 


## Download the human reference: H.sapiens,UCSC hg19


The [hg19.build.sh](data/hg19.build.sh) script downloads sequences of chromosomes 1-22, X and Y from [UCSC directory](http://hgdownload.cse.ucsc.edu/goldenpath/hg19/chromosomes/) (University of California, Santa Cruz) and combines them in order.

```
#How to run

mkdir ucsc_hg19_fasta  #creat a new directory
cd ucsc_hg19_fasta     #go to the new directory

./hg19.build.sh ucsc.hg19.fasta

or

bash hg19.build.sh ucsc.hg19.fasta
````

Once the final FASTA file is produced, all intermediate files and directory are removed. Because the scripts creates temporary files, please run it in a freshly created directory (or ucsc_hg19_fasta).



**Reference:** [Build ucsc.hg19.fasta](https://github.com/creggian/ucsc-hg19-fasta).



## Genome Analysis Toolkit's (GATK's)


In oder to obtained the genotypes and likelihood scores for SNPs, the authors chose to use GATK ```UnifiedGenotyper```. Here, I quoted "We used ```UnifiedGenotyper``` instead of more recent genotype callers, such as ```HaplotypeCaller```, because it has the option to output genotype likelihood scores."

After I did some researches and found out the ```UnifiedGenotyper```(GATK version 3.XXX, the old version) has been replaced by ```HaplotypeCaller```(GATK version 4.XXXX,) which is a much better tool. And It also took me a while to find the program [**```GenomeAnalysisTK.jar```**](data/GenomeAnalysisTK.jar) since it was being discontinued for two or three years, click the link to download the ```GenomeAnalysisTK.jar```(This is from GATK version 3.8.1).


**Note:**

Some links about this issue: 

1. [Legacy GATK code](https://gatk.broadinstitute.org/hc/en-us/articles/360035889571?id=4022). Also known as "Classic GATK", this covers major versions 1 through 3.

2. [How to donwload GATK version 3.8 forum](https://gatkforums.broadinstitute.org/gatk/discussion/11188/gatk-version-3-8-download).

3. [GATK version 1.0 to 3.8 downloads](https://console.cloud.google.com/storage/browser/gatk-software/package-archive/gatk/), you may need a google account to access google cloud platform.





