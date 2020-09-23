IT infrastructure
=======================

Private Cluster
------------------

The NBD Linux Cluster consists of 6 computing nodes with 2 GPUS NVIDIA GeForceTM GTX 1080 and 1
xeon Gold Processors, for a total of 156 cores (312 HT threads). Includes 2 GPUs for offloading calculations.


Folders:
    - Scratch: To compute
    - Work: Large storage
    - Home: Transient Files

**To connect**: ``ssh -p 22022 -X username@94.24.113.46``


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


Private OfficeGPU AK40
--------------------------

The NBD OfficeGPU consists of 28 nodes for schrodinger calculations as well as general analysis tools.

Folders:
    - Scratch: Long calculation
    - Home: Transient files or fast calculations
    - Data: Chemolibraries

**To connect**: 

1) ``ssh -X ùsername@10.8.0.1``
2) ``ssh -X username@nbdcalc01``

Storage Server
---------------

The NBD Server contains 7T of personal storage
and 7 more for daily back ups of all other machines

Folders:
    - /data/users/user/: Individual storage
    - /data/common/: Shared storaged & Project management

**To connect**: ``ssh -X username@10.8.0.1``


RES
---------
The RES grant allows us to use MN4 to run our in house ModTox project. (MD&PELE for academic purposes/publications)

`ModTox project <https://nostrumbiodiscovery.github.io/modtox/>`_


**To connect**: You need to ask for an account. Please, talk with daniel.soler@nostrumbiodiscovery.com

Backup
-------------

- A daily backup is done from NBDCALC01 to NAS Synology in /home and /data.
- A daily backup is done from NBDDATA01 to NAS Synology in /data
- The backup is automatically done at 00:00 sending a daily report to support

The backup keeps:

    - A daily backup for the last 14 days
    - A weekly backup for the last 8 weeks
    - A monthly backup for the last 12 months
    - A yearly backup for all years

This means that we have daily granularity up to 2 weeks, weekly granulatiry up to 2 month, month granularity up to 1 year and year granularuty for past years.

**In order to get backed up files contact with HPCNow support**
