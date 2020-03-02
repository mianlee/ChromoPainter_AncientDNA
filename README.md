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

./hg19.build.sh hg19.fasta

or

bash hg19.build.sh hg19.fasta
````

Once the final FASTA file is produced, all intermediate files and directory are removed. Because the scripts creates temporary files, please run it in a freshly created directory (or ucsc_hg19_fasta).



**Reference:** [Build hg19.fasta](https://github.com/creggian/ucsc-hg19-fasta).


## Prepare the FASTA file to use as reference (hg19)


**Why these steps are necessary**

The GATK uses two files to access and safety check access to the reference files: a ```.dict``` dictionary of the contig names and sizes and a ```.fai``` fasta index file to allow efficient random access to the reference bases. You have to generate these files in order to be able to use a Fasta file as reference.


[How can I prepare a FASTA file to use as reference?](https://gatkforums.broadinstitute.org/gatk/discussion/1601/how-can-i-prepare-a-fasta-file-to-use-as-reference)



**Indexing ```hg19.fasta```  using samtools:**

```
samtools faidx hg19.fasta
```

You will get ```hg19.fasta.fai``` file.


**Creating the fasta sequence dictionary file for your reference**

Using ```CreateSequenceDictionary``` tool from ```Picard``` to create a ```.dict``` file for the ```hg19.fasta``` file.

```
java -jar picard.jar CreateSequenceDictionary R=hg19.fasta O=hg19.dict 
```
You will get ```hg19.dict``` file.

**Note:**

On our server, we have ```samtools``` installed, and you just need to download ```picart``` and you are good to go. Just in case if you want to run it on your local computer, see belows:


1. How to download and install [Samtools](http://www.htslib.org/).
2. Download and install Picart

You can download [Picart](https://broadinstitute.github.io/picard/). Note that it is not possible to add jar files to your path to make the tools available on the command line; you have to specify the full path to the jar file in your java command, which would look like this:

```java -jar ~/my_tools/jars/picard.jar <Toolname> [options]```

However, you can set up a shortcut called an "environment variable" in your shell profile configuration to make this easier. The idea is that you create a variable that tells your system where to find a given jar, like this:

```
export picard=/home/mianlee/Desktop/Software/gatk-4.1.2.0/picard.jar

#Ubuntu 16.04

```
So then when you want to run a Picard tool, you just need to call the jar by its shortcut, like this:

```
java -jar $picard <Toolname> [options]
```





## Genome Analysis Toolkit's (GATK's)


In oder to obtained the genotypes and likelihood scores for SNPs, the authors chose to use GATK ```UnifiedGenotyper```. Here, I quoted "We used ```UnifiedGenotyper``` instead of more recent genotype callers, such as ```HaplotypeCaller```, because it has the option to output genotype likelihood scores."

After I did some researches and found out the ```UnifiedGenotyper``` (GATK version 3.XXX, the old version) has been replaced by ```HaplotypeCaller``` (GATK version 4.XXX), which is a much better tool. And It also took me a while to find the program [**```GenomeAnalysisTK.jar```**](data/GenomeAnalysisTK.jar) (This is from GATK version 3.8.1) since it was being discontinued for two or three years, click the link to download.


**Note:**

Some links about this issue: 

1. [Legacy GATK code](https://gatk.broadinstitute.org/hc/en-us/articles/360035889571?id=4022). Also known as "Classic GATK", this covers major versions 1 through 3.

2. [How to donwload GATK version 3.8 forum](https://gatkforums.broadinstitute.org/gatk/discussion/11188/gatk-version-3-8-download).

3. [GATK version 1.0 to 3.8 downloads](https://console.cloud.google.com/storage/browser/gatk-software/package-archive/gatk/), you may need a google account to access google cloud platform.





