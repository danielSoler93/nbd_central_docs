=============
PELE Platfom
=============

Full documentation
------------------------

`Pele Platform  docs <https://nostrumbiodiscovery.github.io/pele_platform/>`_


Tutorial
--------

`Pele Platform tutorial <https://nostrumbiodiscovery.github.io/pele_platform/tutorials/index.html>`_


Templates for launching
-----------------------

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J peleplat_tests
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=5
   #SBATCH --mem-per-cpu=1000
   # export when running tests from nbdcalc01 (it cannot see cluster files)
   export LC_ALL=C; unset LANGUAGE
   export PELE=/scratch/PELE-repo/
   export PATH="/usr/lib64/openmpi/bin/":$PATH
   export SCHRODINGER=/opt/schrodinger2020-1/
   export LD_LIBRARY_PATH=/scratch/PELE-compilation/PELE-dependencies/boost-1.52.0/lib/
   eval "$(conda shell.bash hook)"
   conda activate /shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/envs/peleplatform-1.6.0
   /shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/envs/peleplatform-1.6.0/bin/python  -m pele_platform.main -h

