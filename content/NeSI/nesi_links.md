+++
title = "NeSI Links"
date = 2021-03-24T12:58:37+13:00
draft = false
weight = 5
+++

The NeSI support page has good documentation for help in getting started and running many tools. This page has some of the most important links. The main page is here:

[**NeSI support home page**](https://support.nesi.org.nz/hc/en-gb)

## Initial set up

This page provides guidelines for setting up your computer to access NeSI:

[**Standard Terminal Setup**](https://support.nesi.org.nz/hc/en-gb/articles/360000625535-Standard-Terminal-Setup)



## Job scripts

The biggest difference for doing analyses on NeSI versus your own computer is that you need to submit your analysis to a queue, so that the server can handle the demand. The queueing system that NeSI uses is the [**Slurm system**](https://en.wikipedia.org/wiki/Slurm_Workload_Manager). This entails writing a *job script* that details the resources you need for each analysis. 

Here is a guide to the basics:

[**Job basics**](https://support.nesi.org.nz/hc/en-gb/articles/360000684396-Submitting-your-first-job)

[**SLURM Best Practice**](https://support.nesi.org.nz/hc/en-gb/articles/360000705196)

Here is more documentation on the SLURM website:

[**Slurm workload manager**](https://slurm.schedmd.com/squeue.html)

One of the most important factors to getting your analyses run is to ask for the right resources (i.e. CPUs and RAM). This requires a balance: if you don't ask for enough memory, for example, the job will die; if you ask for too much, the job will sit on the queue for a long time. Here is a guide to finding the right balance:

[**Finding job efficiency**](https://support.nesi.org.nz/hc/en-gb/articles/360000903776)

There are several partitions on NeSI for running analyses. Some are designed for very large jobs. Normally, the queueing system will pick the partition based on the resources you demand, but you can specify a partition. Here is a guide to the Mahuika partitions:

[**Mahuika Slurm Partitions**](https://support.nesi.org.nz/hc/en-gb/articles/360000204076)

## Tools on NeSI

The [**job basics**](https://support.nesi.org.nz/hc/en-gb/articles/360000684396-Submitting-your-first-job) link has a guide to using the `module` command to find the program you need. Here is a list of all currently installed applications:

[**Supported applications**](https://support.nesi.org.nz/hc/en-gb/sections/360000040076)

If you use R for a lot of your data analysis, you probably use RStudio on your own computer. For running R on NeSI, you will have to make some changes. Here is a good article to help that adjustment:

[**R on NeSI**](https://support.nesi.org.nz/hc/en-gb/articles/209338087-R)

Another way to run R on NeSI is through the JupyterHub. This is a great way to run Python, R, or other languages on NeSI, and is a good way to start using the server if you are not used to it. Here is a good guide:

[**Jupyter on NeSI**](https://support.nesi.org.nz/hc/en-gb/articles/360001555615)

And here is a direct link to the Hub:

[**JupyterHub**](https://jupyter.nesi.org.nz/)

In the future, RStudio server may be available on NeSI so that you can run large R jobs through NeSI with a familiar interface. Currently there is an experimental version of this, however, it is not in alpha mode and not recommended for beginners. You can [**read about it here**](https://support.nesi.org.nz/hc/en-gb/articles/360001555615#rstudio_via_jupyter).









