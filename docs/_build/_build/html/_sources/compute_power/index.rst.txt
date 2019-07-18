NBD's insfrastructure
=======================

Private Cluster
------------------

The NBD Linux Cluster consists of 6 computing nodes with 4 GPUS NVIDIA GeForceTM GTX 1080 and 1
xeon Gold Processors, for a total of 192 cores (384 HT threads). Includes 4 GPUs for offloading calculations.


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
The RES grant allows us to use MN4 to run our in house ModTox project

`ModTox project <https://nostrumbiodiscovery.github.io/modtox/>`_
