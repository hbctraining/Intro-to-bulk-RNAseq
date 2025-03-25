# Introduction to bulk RNA-seq: From reads to count matrix

> **Pre-requisite for this workshop:** The *Basic Data Skills* [Shell for Bioinformatics](https://hbctraining.github.io/Shell-for-bioinformatics/) workshop or a working knowledge of the command line and cluster computing.

## Pre-reading

* [Shell basics review](../lessons/shell_review.md)
* [Best Practices in Research Data Management (RDM)](../lessons/04a_data_organization.md)
* [Introduction to RNA-seq](../lessons/01_intro-to-RNAseq.md)

## Day 1

| Time |  Topic  | Instructor |
|:-----------:|:----------:|:--------:|
| 09:30 - 09:45 | [Workshop Introduction](../lectures/workshop_intro_slides.pdf) | Will |
| 09:45 - 10:25 | [Working in an HPC environment - Review](../lessons/03_working_on_HPC.md) | Upen |
| 10:25 - 11:05 | [Project Organization (using Data Management best practices)](../lessons/04b_data_organization.md) | Will |
| 11:05 - 11:45 | [Quality Control of Sequence Data: Running FASTQC](../lessons/05_qc_running_fastqc_interactively.md) | Upen |
| 11:45 - 12:00 | Overview of self-learning materials and homework submission | Will |

### Before the next class:

1. Please **study the contents** and **work through all the code** within the following lessons:

 * [Experimental design considerations](../lessons/02_experimental_planning_considerations.md)
 * [Quality Control of Sequence Data: Running FASTQC on multiple samples](../lessons/06_qc_running_fastqc_sbatch.md)
 * [Quality Control of Sequence Data: Evaluating FASTQC reports](../lessons/07_qc_fastqc_assessment.md)

    > **NOTE:** To run through the code above, you will need to be **logged into O2** and **working on a compute node** (i.e. your command prompt should have the word `compute` in it).
    > 1. Log in using `ssh rc_trainingXX@o2.hms.harvard.edu` and enter your password (replace the "XX" in the username with the number you were [assigned in class](https://docs.google.com/spreadsheets/d/1kBlYowhjjHJC9ZovmbBULmbqozKpprM17vZ2wPlhNg0/edit#gid=0)). 
    > 2. Once you are on the login node, use `srun --pty -p interactive -t 0-2:30 --mem 1G /bin/bash` to get on a compute node or as specified in the lesson.
    > 3. Proceed only once your command prompt has the word `compute` in it.
    > 4. If you log out between lessons (using the `exit` command twice), please follow points 1. and 2. above to log back in and get on a compute node when you restart with the self learning.

2. **Complete the exercises**:
   * Each lesson above contain exercises; please go through each of them.
   * Add your answers to the questions to [Google forms](https://docs.google.com/forms/d/e/1FAIpQLSdxdSM4528uYTWT7k5c8gYAuCUaTqRkUSI88eUmKg7qyQZZAQ/viewform?usp=sf_link) the **day before the next class**.
   
### Questions?
* ***If you get stuck due to an error*** while runnning code in the lesson, [email us](mailto:hbctraining@hsph.harvard.edu) 

***

## Day 2

| Time |  Topic  | Instructor |
|:-----------:|:----------:|:--------:|
| 09:30 - 10:30 | Self-learning lessons review | All |
| 10:30 - 11:10 | [Expression quantification: Theory and Tools](../lectures/expression_quantification.pdf) | Will |
| 11:10 - 11:50 | [Quantifying expression using alignment-free methods (Salmon)](../lessons/08_quasi_alignment_salmon.md) | Upen |
| 11:50 - 12:00 | [Review of workflow](../lectures/workflow_overview.pdf) | Upen |

### Before the next class:

1. Please **study the contents** and **work through all the code** within the following lessons:

 * [Quantifying expression using alignment-free methods (Salmon on multiple samples)](../lessons/09_quasi_alignment_salmon_sbatch.md)
      <details>
       <summary><i>Click here for a preview of this lesson</i></summary>
         <br>Now that we know how to run the quantification of one sample with Salmon, this lesson will guide you to run multiple samples by creating a job submission script<br><br>
       </details>
 * [QC with Alignment Data](../lessons/10_QC_Qualimap.md)
      <details>
       <summary><i>Click here for a preview of this lesson</i></summary>
         <br>Besides transcript-level quantification, we also want to understand the quality of the mapping, which is not provided in Salmon output. <br><br>This lesson will cover:<br>
             - Aligning the reads with an aligner, STAR<br>
             - Assessing QC metrics among samples<br><br>
       </details>
 * [Documenting Steps in the Workflow with MultiQC](../lessons/11_multiQC.md)
      <details>
       <summary><i>Click here for a preview of this lesson</i></summary>
         <br>It would be great to have a summary document of all QC results from the previous analysis. <br><br>This lesson will cover:<br>
             - Generating such a summary report with multiQC<br>
             - Generating alignment metric with Qualimap<br><br>
       </details>

     > **NOTE:** To run through the code above, you will need to be **logged into O2** and **working on a compute node** (i.e. your command prompt should have the word `compute` in it).
     > 1. Log in using `ssh rc_trainingXX@o2.hms.harvard.edu` and enter your password (replace the "XX" in the username with the number you were assigned in class). 
     > 2. Once you are on the login node, use `srun --pty -p interactive -t 0-2:30 --mem 8G /bin/bash` to get on a compute node or as specified in the lesson.
     > 3. Proceed only once your command prompt has the word `compute` in it.
     > 4. If you log out between lessons (using the `exit` command twice), please follow points 1. and 2. above to log back in and get on a compute node when you restart with the self learning.

2. **Complete the exercises**:
   * Each lesson above contain exercises; please go through each of them.
   * Add your answers to the questions to [Google forms](https://docs.google.com/forms/d/e/1FAIpQLScxaj3IIO4Bx7FCRw87cCeuTPQyhD_7WR2QU638y8IZDv5r1A/viewform?usp=sf_link) the **day before the next class**.
   
### Questions?
* ***If you get stuck due to an error*** while runnning code in the lesson, [email us](mailto:hbctraining@hsph.harvard.edu) 

***

## Day 3

| Time |  Topic  | Instructor |
|:-----------:|:----------:|:--------:|
| 09:30 - 10:10 | Self-learning lessons review | All |
| 10:10 - 11:10 | [Automating the RNA-seq workflow](../lessons/12_automating_workflow.md) | Will |
| 11:10 - 11:45 | [Troubleshooting RNA-seq Data Analysis](../lectures/RNA-seq_troubleshooting.pdf)| Upen |
| 11:45 - 12:00 | [Wrap up](../lectures/workshop_wrapup_slides.pdf) | Will |

***

* Downloadable Answer Keys (Day 2 exercises): 
  * [Experimental design (one possible solution)](https://www.dropbox.com/scl/fi/vk6g9qvvosgmjjonoqint/exp_design_table.xlsx?rlkey=rbxkeln9mm0lxf4kdjbrqsidt&st=6sf562u3&dl=0)
  * [sbatch script](https://www.dropbox.com/scl/fi/3y7oa5i1eub7dzajfpko7/mov10_fastqc.run?rlkey=4eii6tc6nrludbjagcdgs1qxi&st=ipmbrx9y&dl=0)
  * [.out file](https://www.dropbox.com/scl/fi/m0f1ux4522sw2flt73aje/22914006.out?rlkey=sizy0vkm0r5fz14uyswrtdeew&st=sk7gh4i5&dl=0)
  * [.err file](https://www.dropbox.com/scl/fi/iye10ysh780danfo6r6v6/22914006.err?rlkey=maeny1p52dmio5ovli8c5ipss&st=lu0iuvcw&dl=0)

* Downloadable Answer Keys (Day 3 exercises): 
  * [sbatch script to run salmon for all samples](../answer_key/salmon_all_samples.sbatch)

* [Automation Script](../scripts/rnaseq_analysis_on_input_file.sh)

***

## Resources
* [Getting an O2 account](https://harvardmed.atlassian.net/wiki/spaces/O2/pages/1918304257/How+to+request+an+O2+account)
* [Video about statistics behind salmon quantification](https://www.youtube.com/watch?v=TMLIxwDP7sk)
* Advanced bash for working on O2:
  * [Creating shortcuts or aliases](https://hbctraining.github.io/In-depth-NGS-Data-Analysis-Course/sessionVI/lessons/more_bash.html#alias)
  * [Copying files from other remote locations to O2](https://hbctraining.github.io/In-depth-NGS-Data-Analysis-Course/sessionVI/lessons/more_bash.html#rsync)
  * [Creating symbolic links](https://hbctraining.github.io/In-depth-NGS-Data-Analysis-Course/sessionVI/lessons/more_bash.html#symlink)
* [Obtaining reference genomes or transcriptomes](https://hbctraining.github.io/Accessing_public_genomic_data/lessons/accessing_genome_reference_data.html)
* Youtube videos
    * [Hash tables - Paul Programming](https://www.youtube.com/watch?v=MfhjkfocRR0&ab_channel=PaulProgramming)
    * [Suffix arrays - William Fiset](https://www.youtube.com/watch?v=zqKlL3ZpTqs)
***

## Building on this workshop
* [Introduction to R workshop materials](https://hbctraining.github.io/Intro-to-R-flipped/#lessons)
* [Introduction to Differential Gene Expression analysis workshop materials](https://hbctraining.github.io/Intro-to-DGE/#lessons)

***
*These materials have been developed by members of the teaching team at the [Harvard Chan Bioinformatics Core (HBC)](http://bioinformatics.sph.harvard.edu/). These are open access materials distributed under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.*
