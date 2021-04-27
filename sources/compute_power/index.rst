IT infrastructure
=======================

Private Cluster
------------------

The NBD Linux Cluster consists of 6 computing nodes with 2 GPUS NVIDIA GeForceTM GTX 1080 and 1
xeon Gold Processors, for a total of 156 cores (312 HT threads). Includes 2 GPUs for offloading calculations.


Folders:
    - /shared/scratch: To compute
    - /shared/work: Large storage
    - /shared/home-nbdcalc01/: What used to be the office machine (28 cpus)
    - /shared/data-nbdcalc01/: Libraries of compounds (ZINC, fragments...)
    - /shared/data-ndbdata01/users/user/: Individual storage
    - /shared/data-nbddata01/common/: Shared storaged & Project management

**To connect**: ``ssh -X username@10.10.0.6``


Queue system
++++++++++++++

The cluster uses Slurm workload manager to schedule jobs and allocate resources. It is fairly simple to use, you only have to learn a handful of commands:

.. code-block:: bash

    sbatch run.sl # to submit a file to the queue
    squeue # to see all jobs on the queue
    scancel job_id # to cancel a job with specific ID, e.g. scancel 10240

If you want to dive in deeper, check out the `official Slurm documentation <https://slurm.schedmd.com/quickstart.html>`_.

You can also run programs in interactive mode, e.g.

.. code-block:: bash

    interactive -n 20 # launch interactive with 20 CPUs available
    module load module_name # to load a specific module, e.g. module load Python/3.7.0-foss-2018a


RES
---------
The RES grant allows us to use MN4 to run our in house ModTox project. (MD&PELE for academic purposes/publications)

`ModTox project <https://nostrumbiodiscovery.github.io/modtox/>`_


**To connect**: You need to ask for an account. Please, contact with it@nostrumbiodiscovery.com

Backup
-------------

- A daily backup is done from /shared/home-nbdcalc01/ and /shared/data-nbdcalc01/ to NAS Synology.
- A daily backup is done /shared/data-nbddata01/ to NAS Synology
- The backup is automatically done at 00:00 sending a daily report to support

The backup keeps:

    - A daily backup for the last 14 days
    - A weekly backup for the last 8 weeks
    - A monthly backup for the last 12 months
    - A yearly backup for all years

This means that we have daily granularity up to 2 weeks, weekly granulatiry up to 2 month, month granularity up to 1 year and year granularuty for past years.

**In order to get backed up files contact with HPCNow support**
