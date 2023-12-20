---
title: "Option Pricer"
date: 2023-12-20
draft: false
showTableOfContents: true
showReadingTime: false
---

You may find this project
[here](https://github.com/Marcgil1/option-pricer).

# Introduction

This project implements pricing algorithms for European and American options,
both based on a Monte Carlo approach. The project is tailored to be used in the
HPC facilities of the University of Luxembourg (supercomputers nicknamed Iris
and Aion). However, simple modifications of scripts within the mk folder should
make it possible to build and execute this code in other computing clusters or
even on a PC provided with OMP and MPI installations.

# How to execute the code

Supposing a standard computing cluster architecture in which jobs are submitted
via Slurm from a common entry point to execution nodes, running `mk/submit` should
submit a job for building and executing the program. Please be sure to tweak
mk/batch-job to match the specific requirements of your computing cluster.
Particularly, you should modify the module load commands to match those
available in your cluster. These just load a gcc compiler toolchain, OMP, MPI,
and Laplack.

For executing this project on a PC, please make sure that the aforementioned
libraries are installed, then just remove the module-loading operations from
`mk/batch-job` and execute this script. Set `OMP_NUM_THREADS=1` and substitute
`$SLURM_NTASKS` for the number of cores you want to allocate for this job.
