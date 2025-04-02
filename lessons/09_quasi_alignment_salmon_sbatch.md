---
title: "Quantification of transcript abundance using Salmon"
author: "Mary Piper, Meeta Mistry, Radhika Khetani, Jihe Liu"
date: "November 16, 2020"
---

Approximate time: 30 minutes

## Learning Objectives

* Create a job submission script to run Salmon on all samples in the dataset

 
## Running Salmon on multiple samples 

In class we talked in depth about how the Salmon algorithm works, and provided the command required to run Salmon on a single sample. In this lesson we walk through the steps required to **efficiently run Salmon on all samples** in the dataset. Unlike our experience with FastQC, where we could use one command and simply provide all files with the use of a wildcard (`*`), Salmon is only able to take a single file as input.

Rather than typing out the Salmon command six times, we will use **a for loop to iterate over all FASTQ files in our dataset** (inside the `raw_fastq` directory). Furthermore, rather than running this `for` loop interactively, we will put it inside a text file and create a **job submission script**.

### Create a job submission script to run Salmon in serial

Let's start by opening up a text file in `vim`:

```
$ vim salmon_all_samples.sbatch
```

Begin the script starting with the **shebang line**. 

```bash
#!/bin/bash

```
***

**Exercise 1**

1. Add the Slurm directives ( i.e `#SBATCH`) to request specific resources for our job. The resources we need are listed below. 

> **NOTE:** Helpful resources include:
> * This [linked lesson](03_working_on_HPC.md#requesting-resources-from-slurm) 
> * [HMS-RC's O2 Wiki](https://wiki.rc.hms.harvard.edu/display/O2/Using+Slurm+Basic) 

* Your job will use the `short` partition
* Request 6 cores to take advantage of Salmon's multi-threading capabilities
* Request 12 hours of runtime
* Request 8G of memory 
* Give your job the name `salmon_in_serial`
* Add an email and request to be notified when the job is complete

***

Now that we have the resources requested, we can begin to **add the commands into our shell script**. 


***

**Exercise 2**

1. Add a line of code required to load the Salmon module
2. Add a line of code to change directories to where the Salmon results will be output (be sure to use a full path here).

> *Add comments to your script liberally, wherever you feel it's needed.*

***

The last piece of the shell script is the **for loop** code provided below. **Copy and paste this into your script**.

```bash
for fq in ~/rnaseq/raw_data/*.fq

do

# create a prefix for the output file
samplename=`basename $fq .fq`

# run salmon
salmon quant -i /n/groups/hbctraining/RNA_seq_part_1/reference_data/salmon/ref-transcripts \
 -l A \
 -r $fq \
 -o ${samplename}_salmon \
 --seqBias \
 --useVBOpt \
 --validateMappings

done
```

Note, that our for loop is iterating over all FASTQ files in the `raw_fastq` directory. For each file, a prefix is generated to name the output file and then the Salmon command is run with the same parameters as used in the single sample run.

***

**Exercise 3**

1. Add two additional parameters (as described below) to the current Salmon command (*remember to use "`\`" if dissecting one command in multiple lines*): 

	1.  `-p`: specifies the number of processors or cores we would like to use for **multi-threading**. What value will you provide here, knowing what we asked for in our Slurm directives?
	1. `--numBootstraps`: specifies computation of bootstrapped abundance estimates. **Bootstraps are required for isoform level differential expression analysis for estimation of technical variance**. Here, you can set the value to 30.
	
> _**NOTE:** `--numBootstraps` is necessary if performing **isoform-level differential expression analysis** with Sleuth, but not for gene-level differential expression analysis. Due to the statistical procedure required to assign reads to gene isoforms, in addition to the random processes underlying RNA-Seq, there will be **technical variability in the abundance estimates** output from the pseudo-alignment tool [[2](https://rawgit.com/pachterlab/sleuth/master/inst/doc/intro.html), [3](https://www.nature.com/articles/nmeth.4324)] for the isoform level abundance estimates (not necessary for gene-level estimates). Therefore, **we would need technical replicates to distinguish technical variability from the biological variability** for gene isoforms._
>
> _The bootstraps estimate technical variation per gene by calculating the abundance estimates for all genes using a different sub-sample of reads during each round of bootstrapping. The variation in the abundance estimates output from each round of bootstrapping is used for the estimation of the technical variance for each gene._

2. Save and close the script. This script is now ready to run.

```
$ sbatch salmon_all_samples.sbatch
```

3. **After you confirmed that the script runs as expected, copy and paste your final script to [Google forms](https://docs.google.com/forms/d/e/1FAIpQLScxaj3IIO4Bx7FCRw87cCeuTPQyhD_7WR2QU638y8IZDv5r1A/viewform?usp=sf_link).** 

---

*This lesson has been developed by members of the teaching team at the [Harvard Chan Bioinformatics Core (HBC)](http://bioinformatics.sph.harvard.edu/). These are open access materials distributed under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.*
