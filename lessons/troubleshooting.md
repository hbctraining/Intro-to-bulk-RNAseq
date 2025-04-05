---
title: RNA-Seq Analysis Troubleshooting
author: Radhika Khetani, Meeta Mistry, Mary Piper, Jihe Liu, Will Gammerdinger
date: November 2021
---

# Learning Objectives
- Interpret figures from FASTQC and Qualimap
- Identify possible errors in sequence data

# Table of Contents
[Raw Data Quality Control using FASTQC](#Raw-Data-Quality-Control-using-FASTQC)
- [Per Base Sequence Quality](#Per-Base-Sequence-Quality)
- [Per Sequence Base Score](#Per-Sequence-Base-Score)
- [Per Base Sequence Content](Per-Base-Sequence-Content)
- [Per Base GC Content](#Per-Base-GC-Content)
- [Overrepresented Sequences](#Overrepresented-Sequences)

[Aligned Data Quality Control using Qualimap](#Aligned-Data-Quality-Control-using-Qualimap)
- [Reads Genomic Origin](#Reads-Genomic-Origin)

# Raw Data Quality Control using FASTQC

Once you recieve your raw data from the sequencing facility, there can be a sense of rushing right into your analyses. However, taking the time to do some basic quality control on your raw data can save you potential headaches down the line. Quality control analyses can:

- Isolate sequencing problems that need to be resolved with the sequencing core
- Identify contaminated samples
- Provide insight into library complexity

**IMPORTANT:** FASTQC will give either a green check, yellow exclamation mark or red X above each plot. These evaluations done my FASTQC should be taken ***VERY*** lightly. Some of these metrics can be very conservative and it can also depend on your dataset. FASTQC is not designed for different dataset types, so a "good" ChIP-seq run could have some elements that would look problematic in a RNA-seq or whole genome sequencing run, or vis-a-versa. As a result, is it best to taken their evaluations lightly and assess the plots yourself with knowledge about your datasets. 


## Per Base Sequence Quality

The first place to start when assessing your raw data is analyzing the qualiy of base calls. In the figure below you will see that the y-axis is the meausre of base call quallity (PHRED score) and the x-axis is the position in the read. It is farily common for these figures to have a bit of an arc to them with base quality deteriotating near the end of the read. Generally, speaking the median (?) represented by the blue line should be relatively smooth and devoid of large substantially drops or spikes. Ideally, the bar plots should mostly stay in the green region, but sometimes they may dip into the yellow region near the end of the read. An example of a "good" result could be seen below:

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/good_quality.png" width="500">
</p>

Now we can compare this to a sequencing runs we would be concerned about. In this example, we can see that very early on, the barplots are dipping into the yellow and even red regions. This is a big warning sign for low quality data.


Another signal that something went wrong in your sequencing can be seen below. The sudden drop in base quality around cycle 26 should be cause for alarm.

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/qc_manifold_burst.png" width="500">
</p>

The very eradict and jumping nature of the reads quality scores in the below figure would also very likely be problematic.

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/qc_cycles_lost.png" width="500">
</p>

These are a few examples of error profiles to look out for when analyzing your data. These types of problems are not common and are usually sequencer problems. If you run into issues like this, it is best to reach out to your sequencing center.

---

## Per Sequence Base Score

In addition to checking base scores across the read, we will likely also want to visualize the distribution of base scores. In this next plkot we have the PHRED scores on the x-axis and the counts on the y-axis. Ideally, we should see a low density of base scores until it increases sharply near the right side.

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/Per_sequence_quality_scores_good.png" width="500">
</p>

This indicates that the bulk of our distribution is near the the upper end of the PHRED score range and thus is high-quality data.

In the two images below, we see bumps at PHRED scores of 12 and 20, respectively. The size of the bumps and where in the PHRED range they fall will factor how seriously you should be concerned. In general, any bumps below 30 within this plot should be a warning sign to pause and consider the quality of this data. 

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/fastqc_per_sequence_quality_scores.png" width="500">
</p>

> NOTE: In the above plot we can see that a good proportion of the data is centered around a PHRED score of 36 and very little of it actually reached a PHRED score of 40 as in the plot before the above plot. There's not much read to into these differences at the top end of the distributions besides the first plot is definitly cleaner data.

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/Per_sequence_quality_scores_bad.png" width="500">
</p>

---

## Per Base Sequence Content

Next, we should evaluate the sequence content for your data sets. Here we will be evaluating the levels of the various bases called at each position in the read. It is quite common for the first few bases to be quite "spike-y" due to some adaptor contamination in the sample. Hoever usually by the 10th base or so it should level out and remain relatively constant for the rest of the length of the read. An example of this can be seen below: 

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/fastqc_per_base_sequence_content.png" width="500">
</p>

However, if your data does not remain relatively constant after about the 10th base, you should have some concerns about your data. In the plot below, we can see that the %A steadily rises over the course of the run. This would be problematic behavior that should be addressed with the sequencing facility.

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/Per_base_sequence_content_bad.png" width="500">
</p>

---

## Per Base GC Content

Another metric to assess the GC composition of your data. Hopefully, you know the approximate GC composition of your dataset prior to sequencing or atleast have a rough approximation from a related species. The per base GC content plot should have a distribution centered near that expected GC content. In the figure below is from a whole genome DNA library, the expect GC content of the organism was ~48% and the peak of our distribution mirrored that. 

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/Per_sequence_GC_content_good.png" width="500">
</p>

However, if investigating RNA-seq samples, this plot can be more difficult to interpret as it could show some spikes that result from highly expressed genes like in the figure below.

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/fastqc_GC.png" width="500">
</p>

> NOTE: If you see a very bimodal distribution, it could be an indication of contamination. Sources of contamination could be different species, adapters, vectors and/or mitochonrial/ribosomal RNA. 

> NOTE: If you are carrying out an experiment that non-randomly sequences certain regions of the genome, like a ChIP-seq experiment, there could be some distortions to the figure.

However, in the next figure we can see that that GC content distribution has a small bump around 52%, while the majority of the data is piling up near 100%. The bump around 52% likely represents the data from the organism, but the data near 100% is indicative of a problem with the sequencing and should be a reason to reach out to the sequencing facility.

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/Per_sequence_GC_content_bad.png" width="500">
</p>

---

## Overrepresented Sequences

A final metric to consider in your raw data are the overrepresented sequences. It is not uncommon to find one or two overrepresented sequences that are below 1-2% and are the result of TruSeq adaptors. In the table below you can see that is infact the case. You can see that it has identified the overepresented sequence as a TruSeq adaptor and that it represents only 0.2% of the data set.

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/Overrepresented_sequences_adaptor_only.png" width="500">
</p>

It is also common to find more overrepresented sequences when carrying out RNA-seq experiments. Some of these overrepresented sequences can simply be the result of highly expressed transcripts in your sample like below. It is best practice to do a [BLAST search](https://blast.ncbi.nlm.nih.gov/Blast.cgi) of any overrepresented sequence that doesn't have a known hit in order to make sure it came from your sample of interest and is not the result of contamination.

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main//img/FastQC_contam.png" width="500">
</p>

> NOTE: Once again, if you are sampling the genome non-randomly, like in a ChIP-seq experiment, you may see more overrepresented seqeunces. 

This figure can be problematic if it contains a overrepresented sequences constitutes a high proportion of data (>2%) or if this sequence represents long homopolymers. Both of these are demonstrated below. 

<p align="center">
<img src="https://github.com/hbctraining/Intro-to-rnaseq-hpc-salmon-flipped/blob/main/img/Overrepresented_sequences_homopolymers.png" width="500">
</p>

---

# Aligned Data Quality Control using Qualimap

Analyzing aligned data can also be a criitcally important quality control check for an RNA-seq data set. This type of analysis can tell you things about your data that raw data quality control metrics weren't able to tell you, such as:

- Potential DNA contamination
- 5'-3' biases

## Reads Genomic Origin


