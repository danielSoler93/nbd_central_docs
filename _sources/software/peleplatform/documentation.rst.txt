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

**PelePlatform - v1.6.1, latest release**

.. code-block:: bash

   #SBATCH -J peleplat_tests
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=2
   #SBATCH --mem-per-cpu=1000

   module purge
   source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh
   conda activate /shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/envs/peleplatform-1.6.1

   module load intel

   export SCHRODINGER="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/"
   export SCHRODINGER_PYTHONPATH="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/internal/lib/python2.7/site-packages"
   export PELE="/shared/work/NBD_Utilities/PELE/PELE_Softwares/bin/PELE1.6/"

   export LC_ALL=C; unset LANGUAGE
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/shared/work/NBD_Utilities/PELE/PELE_Softwares/local_deps/pele_deps/boost_1_52/lib:$LD_LIBRARY_PATH
   export SRUN=1  # this is to avoid having to set usesrun: true in input.yaml

   python -c "import pele_platform; print('Using PELEPlatform, version', pele_platform.__version__)"
   python -m pele_platform.main input_fast.yaml


**PelePlatform - v1.6**

.. code-block:: bash

   #SBATCH -J peleplat_tests
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=2
   #SBATCH --mem-per-cpu=1000

   module purge
   source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh
   conda activate /shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/envs/peleplatform-1.6.0

   module load intel

   export SCHRODINGER="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/"
   export SCHRODINGER_PYTHONPATH="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/internal/lib/python2.7/site-packages"
   export PELE="/shared/work/NBD_Utilities/PELE/PELE_Softwares/bin/PELE1.6/"

   export LC_ALL=C; unset LANGUAGE
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/shared/work/NBD_Utilities/PELE/PELE_Softwares/local_deps/pele_deps/boost_1_52/lib:$LD_LIBRARY_PATH
   export SRUN=1  # this is to avoid having to set usesrun: true in input.yaml

   python -c "import pele_platform; print('Using PELEPlatform, version', pele_platform.__version__)"
   python -m pele_platform.main input_fast.yaml


**PelePlatform - v1.5.1**

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J PELE_MPI_test
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=5
   #SBATCH --mem-per-cpu=1000

   # DO NOT CHANGE ###########################

   module purge

   export SCHRODINGER="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/"
   export SCHRODINGER_PYTHONPATH="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/internal/lib/python2.7/site-packages"
   export PELE="/shared/work/NBD_Utilities/PELE/PELE_Softwares/bin/PELE1.6/"
   export LC_ALL=C; unset LANGUAGE

   unset PYTHONPATH

   module load impi/2018.1.163-iccifort-2018.1.163-GCC-6.4.0-2.28 wjelement/1.3-intel-2018a
   module load Crypto++/6.1.0-intel-2018a OpenBLAS/0.2.20-GCC-6.4.0-2.28

   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/shared/work/NBD_Utilities/PELE/PELE_Softwares/local_deps/pele_deps/boost_1_52/lib:$LD_LIBRARY_PATH
   export PYTHONPATH="/shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/depend:$PYTHONPATH"
   export SRUN=1  # this is to avoid having to set usesrun: true in input.yaml

   ###################################################################

   /shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/depend/bin/python -m pele_platform.main input.yaml

