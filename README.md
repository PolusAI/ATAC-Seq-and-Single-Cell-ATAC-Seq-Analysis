[comment]: <> (Hi. If you are seeing this message, please open this file with markdown preview or Jupyter Notebook. You can do this by right clicking on the readme file and picking 'open with'.)
![course-card](images/UNMC-course-card-3.png)
Image adapted from https://doi.org/10.1038/s41596-022-00692-9   
   
   
# An open-source interactive pipeline tutorial for differential ATAC-seq footprint analysis


## Overview

Included here are several tutorials in the form of Jupyter Notebooks.

The purpose of these tutorials is to help users familiarize themselves with the analysis steps for processing ATAC-seq data including considerations for single-end, paired-end, or single-cell data. 

![atacseq 60k image](images/60k_bmmc_dsciATAC.png)

These tutorials do this by going step-by-step through specific workflows. These workflows cover the start to finish of basic bioinformatics analysis; starting from downloading raw sequence data, and extending to differential peak identification, genome annotation, and transcription factor footprinting, while producing common plots and visualizations. Submodules 1 through 3 focus on analysis of bulk cellular data while submodule 4 focuses on single cell data. 

For submodule 4, we will use RAPIDS pipeline to demonstrate on how to use analyze single-cell ATAC sequencing data. We demonstrate the use of RAPIDS pipeline to accelerate the analysis of single-cell ATAC-seq data from 60,495 cells.  RAPIDS is a suite of open-source Python libraries that can speed up data science workflows. We start with the peak-cell matrix, then perform peak selection, normalization, dimensionality reduction, clustering, and visualization. We also visualize regulatory activity at marker genes and compute differential peaks.

Dataset sizes for single-cell genomics studies are increasing, presently reaching millions of cells. With RAPIDS pipeline, it becomes easy to analyze large datasets interactively and in real time, enabling faster scientific discoveries.

This module will cost you about $3.80 to run, assuming you tear down all resources upon its completion.

Watch this [Introduction Video](https://youtu.be/w5reYUKnf60) to learn more about the module.  

## Table of Contents

+ [Requirements](#requirements)
+ [Getting Started](#getting-started)
+ [Workflows](#workflows)
+ [Data](#data)
+ [Funding](#funding)


## Requirements

These tutorials were designed to be used on cloud computing platforms, with the aim of requiring nothing but the files within this GitHub repository.

With this in mind, our tutorials use Jupyter Notebook files, which are natively supported in Polus Notebooks Hub. Therefore, the only requirement is to create an appropriate environment module in your instance of Notebooks Hub based on included conda `environment.yaml`.

## Getting Started

This repository contains several notebook files which serve as bioinformatics workflow tutorials.

Begin by first navigating to your instance of Notebooks Hub, i.e. https://hub.scb-ncats.io and logging in with your credentials. Then, create a new JupyterLab server and make sure to select `atacseq-unmc-env` software environment in settings. Tutorials 1-3 only need CPU hardware, but Tutorial 4 calls for GPU option.

### Launching Server

Once a server has been created, click green 'Start' button on a server card. Wait for the button to turn into 'Stop', indicating that the server is running and then click on green 'Launch' button in the bottom of the right sidebard. JupyterLab will open.

### Downloading Tutorial Files

Now that you have created your server, and are in the JupyterLab screen, you can run our tutorial files. But first you will need to download them. 

The easiest way to do this would be to clone the NIGMS repository into your storage. Navigate to `work` folder in Notebooks Hub by double clicking on it (this way the files will stay available between restarts and your different servers). Using the 'Git' menu in JupyterLab, and select the clone option. 

Next you can type in the link of repository: `https://github.com/PolusAI/ATAC-Seq-and-Single-Cell-ATAC-Seq-Analysis` and click 'Clone'. 

This should download our repository, and the tutorial files inside, into a folder called 'atacseqUNMC'. Double-click this folder now. Inside you will find all our tutorial files, which you can double-click and run.

![ATAC-Seq workflow](images/gitclone.png)

### Running Tutorial Files

All our tutorial workflows are in Jupyter Notebook format. To run them you need only to double-click the tutorial file you want.

This will open the Jupyter file in Jupyter Notebook. From here you can run each section, or 'cell', of the code, one by one, by pushing the 'Play' button on the above menu. 

Some 'cells' of code take longer for the computer to process than others. You will know a cell is running when a cell has an asterisk next to it \[\*\]. Wait until the \[\*\] disappears before you run the next code block. When the cell finishes running, that asterisk will be replaced with a number which represents the order that cell was run in.

You can now explore the tutorials by running the code in each, from top to bottom. Look at the 'workflows' section below for a short description of each tutorial.

Jupyter is a powerful tool, with many useful features. For more information on how to use Jupyter, we recommend searching for Jupyter tutorials and literature online.

### Configuration for Submodule 4: Single-Cell Genomics Analysis with RAPIDS

#### RAPIDS

Unified Virtual Memory (UVM) can be used to [oversubscribe](https://developer.nvidia.com/blog/beyond-gpu-memory-limits-unified-memory-pascal/) your GPU memory so that chunks of data will be automatically offloaded to main memory when necessary. This is a great way to explore data without having to worry about out of memory errors, but it does degrade performance in proportion to the amount of oversubscription. UVM is enabled by default in these examples and can be enabled/disabled in any RAPIDS workflow with the following:


```
import cupy as cp
import rmm
rmm.reinitialize(managed_memory=True)
cp.cuda.set_allocator(rmm.rmm_cupy_allocator)
```

### Stopping Your Server

When you are finished running code, you can stop your server to prevent unneeded resource use by returning to Notebooks Hub and pressing the 'Stop' button on the server card.

## Workflows

Our tutorials are broken down into 'workflows'. Each notebook file covers a specific workflow, which contains written and visual commentary, as well as the actual step-by-step code for running that workflow analysis. 

![ATAC-Seq workflow](images/ATACseqWorkflow.png)
**Workflow for ATAC Sequencing (submodules 1 through 3)**


**[Tutorial One](ATACseq_Tutorial1_Preprocessing.ipynb):** This short tutorial demonstrates the initial processing steps for ATAC-seq analysis. In this module we focus on generating quality reports of the fastq files, adapter trimming, mapping, and removal of PCR duplicates.

**[Tutorial Two](ATACseq_Tutorial2_PeakDetection.ipynb):** In this section we will focus on visualization of the signal, create average plots of signal around transcription start sites (TSSs), and identification of peak signal.

**[Tutorial Three](ATACseq_Tutorial3_Downstream.ipynb):** In this section we will focus on differential peak identification, motif footprinting, and annotation of nearby genomic features.

![single cell workflow](images/Tutorial_4.png)
**Workflow for sc-ATAC Sequencing (submodule 4)**. 
  

**[Tutorial Four](scATACseq_Tutorial4.ipynb):** In this section we will demonstrate a single cell ATAC-Seq analysis workflow. 


## Data

In the ATAC Sequencing tutorial(notebooks 1 through 3) we will process a randomly chosen published dataset. This is available from GEO: GSE67382 Bao X, Rubin AJ, Qu K, Zhang J et al. A novel ATAC-seq approach reveals lineage-specific reinforcement of the open chromatin landscape via cooperation between BAF and p63. Genome Biol 2015 Dec 18;16:284. PMID: [26683334](https://pubmed.ncbi.nlm.nih.gov/26683334/)

This dataset is paired-end 50 bp sequencing. We will analyze two samples representing NHEK cells with BAF depletion compared to a control. Note that to allow faster processing we have limited the reads to that of a specific region of chromosome 4.

The 4th notebook focusing on single cell analysis will use data from Lareau et al., Nat Biotech 2019, one of the highest throughput single-cell ATAC-seq experiments to date. In this tutorial we focus on the 60K resting cells from this experiment. PMID: [33637727](https://pubmed.ncbi.nlm.nih.gov/33637727/)

## Funding

Funded by the INBRE Program (NIH/NIGMS P20 GM103427).