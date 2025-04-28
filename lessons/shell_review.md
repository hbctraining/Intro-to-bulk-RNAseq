---
title: "The Shell"
author: "Mary Piper, Radhika Khetani, Meeta Mistry, Jihe Liu"
date: "October 26, 2020"
---

## Learning Objectives
- Review shell commands and concepts


## Setting up

This workshop assumes that you have either a) taken our [Introduction to command-line interface workshop](https://hbctraining.github.io/Shell-for-bioinformatics/schedule/) or b) been working on the command-line and are already fluent with shell/bash. **We ask that you complete the exercises below**, to refresh some basic commands that you will be using over the course of the workshop. For each section we have relevant materials linked as a helpful reference. 

### Opening up a terminal window

> *NOTE: This mandatory pre-work does not require you to login to the O2 cluster.*

On your local laptop, you will need to open up your terminal window. This will be different depending on what kind of operating system (OS) you are working on.

**With Mac OS**

Macs have a utility application called "**Terminal**" for performing tasks on the command line (shell), both locally and on remote machines. 

Please find and open the Terminal utility on your computers using the *Spotlight Search* at the top right hand corner of your screen.

**With Windows OS**

By default, there is no built-in Terminal that uses the bash shell on the Windows OS. So, we will be using a downloaded program called "**Git BASH**" which is part of the [Git for Windows](https://git-for-windows.github.io/) tool set. **Git BASH is a shell/bash emulator.** What this means is that it shows you a very similar interface to, and provides you the functionality of, the Terminal utility found on the Mac and Linux Operating systems.

Please find and open Git BASH.

> **Tip** - Windows users can use another program called [Putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) instead of a *bash emulator* to log in to remote machines, but it is a little more involved and has different capabilities. We encourage you to take a look at it, but we will not be covering it in this workshop.

### Downloading the example data folder

We will be exploring the capabilities of the shell by working with some RNA-Seq data. We need to **download the data to our current folder** using the link below. To do so, follow the step-by-step instructions below.

**1. Find out what folder we are currently inside**. To do this, we can use the 'print working directory' command:

```bash
$ pwd
```

> On a **Mac** your current folder should be something starting with `/Users/`, like `/Users/marypiper/`.
> 
> On a **Windows** machine your current folder should be something starting with `/c/Users/marypiper`. To find this in your File explorer try clicking on PC and navigating to that path.

_Once you have identified which folder you are in, this is where we will be downloading your data._

**2. Click on the link below then go to file > download to download the data"**. This will automatically download the folder to your downloads folder. If you downloaded the data previously as a part of the Basic Shell workshop, you do not need to download it again unless you have deleted it.

* Download data by [clicking here](https://www.dropbox.com/s/x66jksdd4jklpdw/unix_lesson.zip?dl=0).

**3.** Once you have downloaded the file to the correct location, go back to your **terminal window and type the 'list' command**:

```bash
$ ls
```

> `ls` stands for 'list' and it lists the contents of a directory.

_You should see `unix_lesson.zip` as part of the output to the screen._

**4.** Finally, to **decompress the folder**:

* Double click on unix_lesson.zip on a mac. This will automatically inflate the folder.
* If you are on windows, press and hold (or right-click) the folder, select Extract All..., and then follow the instructions.


**5.** Now when you **run the `ls` command** again you should see a folder called `unix_lesson`, which means you are all set with the data download!

```bash
$ ls
```

**6.** Go into the folder for the lesson

on mac type: 
```bash
$ cd unix_lesson
```

on windows type:

```bash
$ cd unix_lesson/unix_lesson
```

***


## Reviewing shell commands

### Shell basics
We are going to start this review with some basic commands pertaining to navigating around the filesystem. Helpful reference materials are listed below:

* [Introduction to Shell](https://hbctraining.github.io/Shell-for-bioinformatics//lessons/01_the_filesystem.html)
* [Wildcards and shortcuts in Shell](https://hbctraining.github.io/Shell-for-bioinformatics/lessons/02_wildcards_shortcuts.html)
* [Examining and creating files](https://hbctraining.github.io/Shell-for-bioinformatics/lessons/03_working_with_files.html)

1. Change directory into the `unix_lesson/` directory.
2. Take a quick look at the `Mov10_oe_1.subset.fq` file (located in `raw_fastq` directory) using `less` from `unix_lesson/`, without changing directories.
3. Use a shortcut to move out of the directory to the parent of `unix_lesson/`.
4. Change directories into the `raw_fastq/` folder with a single command.
5. What does the `~` in the command prompt mean?
6. What is the full path to the `unix_lesson` directory?
8. List all the files in the `raw_fastq` directory.
8. Modify the above command using the `*` wildcard to only list those files that have "oe" in their names.
10. How many and which commands have you run so far?

### Searching and redirection
Next, we will search our files for specific patterns and redirect the results to file. Helpful reference materials are listed below:

* [Searching and redirection](https://hbctraining.github.io/Shell-for-bioinformatics/lessons/04_searching_files.html)

12. Create a new directory called `shell_review/` within the `unix_lesson/` directory.
13. Search the file `unix_lesson/reference_data/chr1-hg19_genes.gtf` for lines containing the string "MOV10". Save the output in the `shell_review/` directory with a new name - "Mov10_hg19.gtf".
14. Use `vim` to open the newly created file `unix_lesson/shell_review/Mov10_hg19.gtf` and add a comment at the top specifying how this file was created and the source of the content. Save the modified file and quit `vim`.
15. In the new file "Mov10_hg19.gtf", how many lines contain the word "exon"?

### Loops and shell scripts

* [Shell scripts and variables in Shell](https://hbctraining.github.io/Shell-for-bioinformatics/lessons/05_shell-scripts_variable.html)
* [Loops and automation](https://hbctraining.github.io/Shell-for-bioinformatics/lessons/06_loops_and_automation.html)

16. Use the `for` loop to iterate over each FASTQ file in `raw_fastq` and do the following:
      * Print the name of the current file
      * Generate a prefix to use for naming our output files, and store it inside a variable called `sample`.
      * Dump out the first 40 lines into a new file that will be saved in `shell_review`
17. Place the above `for` loop into a shell script using `vim` and run it.

### Permissions

* [Interpreting the permissions string](https://hbctraining.github.io/Shell-for-bioinformatics/lessons/07_permissions_and_environment_variables.html#permissions)

There is a folder in the HBC training shared space on the O2 cluster called `intro_rnaseq_hpc`. Below we have displayed a long listing of its contents. 

``` bash
total 714
drwxrwsr-x  3 mm573 hbctraining 1111 Aug 22  2017 bam_STAR
drwxrwsr-x  8 mp298 hbctraining 1914 May 21  2018 bam_STAR38
drwxrwsr-x  2 mm573 hbctraining  522 Oct  6  2015 bam_tophat
drwxrwsr-x  2 mm573 hbctraining  240 Oct 19  2015 counts
drwxrwsr-x  2 mm573 hbctraining  260 Oct 19  2015 counts_STAR
-rw-rw-r--  1 mm573 hbctraining 2416 Aug 22  2017 DE_script.R
-rw-rw-r--  1 mm573 hbctraining 2064 Mar 28  2018 DESeq2_script.R
drwxrwsr-x  2 mm573 hbctraining  705 Oct  6  2015 fastqc
drwxrwsr-x  2 mm573 hbctraining  272 Jan 31  2018 full_dataset
-rw-rw-r--  1 mm573 hbctraining  216 Nov 10  2015 install_libraries.R
-rw-rw-r--  1 mm573 hbctraining  117 Oct 19  2015 install_libraries.sh
drwxrwsr-x 78 mm573 hbctraining 1969 Aug 22  2017 R-3.3.1
drwxrwsr-x  3 mp298 hbctraining  234 Feb 27  2019 reference_data_ensembl38
drwxrwsr-x  2 mm573 hbctraining  555 Oct  5  2015 reference_STAR
drwxrwsr-x  2 rsk27 hbctraining  260 Aug 22  2017 salmon.ensembl37.idx
drwxrwsr-x  2 mm573 hbctraining  306 Oct  6  2015 trimmed_fastq

```

18. How many owners have files in this folder?
19. How many groups?
20. Are there any executable *files* in this folder?
21. What kind of access does the user `mm573` have to the `full_dataset/` directory?
22. You are considered as "other" or everyone else on this system (i.e you are not part of the group `hbctraining`. What command would allow the user `mm573` do to take away your ability to look inside the `full_dataset/` directory?


### Environment variables

* [Understanding environment variables](https://hbctraining.github.io/Shell-for-bioinformatics/lessons/07_permissions_and_environment_variables.html#environment-variables)

23. Display the contents of the `$HOME` variable on your computer.
24. Use the `which` command to check where the executable file for the `pwd` command lives in the directory structure.
25. How does shell know where to find the executable file for the `pwd` command?
26. Display the contents of the variable that stores the various paths to folders containing executable command files.



### Review your answers
* [Answer key](shell_review_answer_key.md)

****

*This lesson has been developed by members of the teaching team at the [Harvard Chan Bioinformatics Core (HBC)](http://bioinformatics.sph.harvard.edu/). These are open access materials distributed under the terms of the [Creative Commons Attribution license](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0), which permits unrestricted use, distribution, and reproduction in any medium, provided the original author and source are credited.*
