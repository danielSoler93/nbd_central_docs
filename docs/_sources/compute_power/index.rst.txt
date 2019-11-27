NBD's insfrastructure
=======================

Private Cluster
------------------

The NBD Linux Cluster consists of 6 computing nodes with 2 GPUS NVIDIA GeForceTM GTX 1080 and 1
xeon Gold Processors, for a total of 156 cores (312 HT threads). Includes 2 GPUs for offloading calculations.


Folders:
    - Scratch: To compute
    - Work: Large storage
    - Home: Transient Files


Private OfficeGPU AK40
--------------------------

The NBD OfficeGPU consists of 28 nodes for schrodinger calculations as well as general analysis tools.

Folders:
    - Scratch: Long calculation
    - Home: Transient files or fast calculations
    - Data: Chemolibraries

Storage Server
---------------

The NBD Server contains 7T of personal storage
and 7 more for daily back ups of all other machines

Folders:
    - /data/users/user/: Individual storage
    - /data/common/: Shared storaged & Project management

RES
---------
The RES grant allows us to use MN4 to run our in house ModTox project. (MD&PELE for academic purposes/publications)

`ModTox project <https://nostrumbiodiscovery.github.io/modtox/>`_

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
