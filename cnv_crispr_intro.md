# Homework - 'Omics data and CRISPR
## Objectives

Using CRISPR library data supplied and A375 'omics data of your choice, identify relationships between target site status and CRISPR guide activity. This CRISPR library was conducted in the A375 melanoma cell line, so 'omics data should be obtained for this cell line using published literature or cell line databases. Examples of 'omics datasets could be RNA-seq, chromatin accessibility (e.g. MNase-seq, ATAC-seq, DNase-seq, ChIP-seq), copy-number variation, or genotype data. The data source should be justified.

## Rules
This task is un-timed. You may use any programming language, libraries, or frameworks available to you provided they are available to others to reproduce your analysis. You should clearly distinguish your original code from 3rd party code. Clearly demonstrating your process and laying out your “thoughts in code” is more important than runtime performance. We must be able to re-create your analysis. Organisation counts and the ability to layout and document a source repository in a sensible way is part of the assignment. Formal unit testing is not required, but one should provide evidence their analysis was executed as intended and results are not due to errors like improper parameters.

## Instructions
For this repository, write one or more scripts to analyse the included guide_data.tsv file, then make a pull request back with your code and email getin@desktopgenetics.com with the subject “Homework Complete” including a summary of your results. You may also want to generate documents, makefiles, plots, figures, or other pieces of code to support your analysis or allow it to be reproduced by us.

In addition, you should then prepare a 30 minute presentation on your approach and findings for the Desktop Genetics team. 

In your analysis, consider the following topics:

1. Which guide-targeted regions of the A375 genome exhibit the most diverse target site status based on 'omics data?

2. What statistical tests are appropriate to analyse CRISPR guide activity vs target site status?

3. Readability and modularity of your code. We would like to understand how it works and how to re-use it. Useability should be well documented, as well as your thought process for code development and organisation.

4. There isn't necessarily a right or wrong answer to this task. We are more interested in how you tackle this problem, and the thought processes involved.

## A very basic CRISPR introduction
In CRISPR/Cas9 genome editing, a DNA cutting enzyme (nuclease) known as Cas9 is targeted toward a specific part(s) of the genome by encoding instructions in a nucleic acid sequence, known as a guide RNA. The nuclease is thought to search the genome by jumping to a random point and then linearly scanning for the pattern NGG before detaching and repeating the cycle at a new location. If the pattern NGG is found, the nuclease then checks the 20 character programmable pattern right to left. If the match is *sufficiently close*, typically fewer than 4 mismatches, then the nuclease will cut the genome at this location. Otherwise it will detach and try another location.
![CRISPR searches for a 20 character sequence and cuts](images/fgen-crispr-diagram.jpg)
The host cell will then attempt to repair this cut with one of several different repair pathways each with a characteristic, at times imperfect, outcome. For example, if the genome is cut inside of functional region, a gene, this gene may be disabled if the repair is imperfect. If this gene is essential and imperfectly repaired, then the cell can die. By repeating this process in parallel millions of times with different guide sequences, we can use CRISPR to determine the genes a cell needs to survive. These genes are often good drug targets when the cell is a cancer cell.

When there are numerous copies of the target sequence, the nuclease cannot differentiate between which is the right and wrong sequence to cut and therefore causes excess DNA cutting. We call this "off target effects" which means nuclease activity in multiple locations and there is a loss in specificity of the CRISPR cut. By identifying where these problematic regions in the genome exist, we can target around that region and therefore sidestep cutting errors.

## Sample Dataset
We have provided a **Knock-out CRISPR dataset** (`data/crispr_guide_data.tsv`) from [Shalem et al. 2014](http://www.ncbi.nlm.nih.gov/pubmed/24336571). This is a pooled CRISPR library targeting essential genes. CRISPR-Cas9 induced gene disruption will result in cell death/ growth arrest genes essential to cell viability, and this will be reflected by a relative decrease in NGS read count.

The reads have been counted, and normalised, and the data has been processed into .tsv format showing for each guide RNA the 20bp spacer sequence (excluding the PAM sequence), the target gene, and experimental readouts at various timepoints:
 - **plasmid** represents the baseline counts, prior to CRISPR

2 replicates each for post-CRISPR timepoints:
 - **D7** read counts taken 7 days after drug selection for viral integration of CRISPR construct
 - **D14** read counts taken 14 days after drug selection for viral integration of CRISPR construct


Cell-line specific **'omics** data:
    You may use any dataset you deem appropriate to obtain a genome-wide readout specific to A375 cells. You will be expected to justify your choice of data source.

## Prior Art 

To add additional flavour to this task, **CRISPR guides are not all created equal**. Guides have various intrinsic and extrinsic factors that affect their on-target activity at the intended site and specificity (off-target activity). It is an active interest of Desktop Genetics, and the CRISPR community as a whole to understand guide characteristics that allow accurate prediction of activity. Although analyses of these factors is outside the scope of this homework assignment, it is important to bear them in mind.


