.. NBD documentation master file, created by
   sphinx-quickstart on Mon Dec  4 11:58:09 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Main Cluster
===========================================

The NBD Linux Cluster consists of 5 computing nodes  with 2 GPUS NVIDIA GeForceTM GTX 1080 and 1 xeon Gold Processors, for a total of 306 cores (384 HT threads).  It is configured with 576 Gb of total memory and 6 TB of NFS disk space, although more storage can be transparently added. The cluster has a theoretical peak performance of 12.6TFlops and 57.5 TFlops including the GPUs.  All NBD nodes run Linux Centos 7.4 and support queue system through slurm workload manager. User data space is supported by 2xHD 1TB, 6 Gb/s 7.200 r.p.m 3,5 64MB Nearline Enterprise Storage controlled over a login node at 10GbE.


.. toctree::
   software/software


.. toctree::
   storage/storage
