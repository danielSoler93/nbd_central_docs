==================================
Launching Templates
==================================

.. toctree::
   :maxdepth: 2


PelePlatform (cluster)
-------------------------

**Last Update:** 14-02-2021

**PelePlatform - v1.6.3, latest release**

.. code-block:: bash
   
   #!/bin/bash
   #SBATCH -J peleplat_tests
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=2
   #SBATCH --mem-per-cpu=1000

   module purge

   module load intel
   module load intel-oneapi
   module load imkl

   export SCHRODINGER="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/"
   export SCHRODINGER_PYTHONPATH="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/internal/lib/python2.7/site-packages"
   export PELE="/shared/work/NBD_Utilities/PELE/PELE_Softwares/bin/PELE1.7.1/"

   export LC_ALL=C; unset LANGUAGE
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/shared/work/NBD_Utilities/PELE/PELE_Softwares/local_deps/pele_deps/boost_1_52/lib:$LD_LIBRARY_PATH
   export SRUN=1  # this is to avoid having to set usesrun: true in input.yaml
   
   source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh
   conda activate /shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/envs/peleplatform-1.6.3

   python -c "import pele_platform; print('Using PELEPlatform, version', pele_platform.__version__)"
   python -m pele_platform.main input_fast.yaml
   
   
**PelePlatform - v1.6.2

.. code-block:: bash
   
   #!/bin/bash
   #SBATCH -J peleplat_tests
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=2
   #SBATCH --mem-per-cpu=1000

   module purge

   module load intel
   module load intel-oneapi
   module load imkl

   export SCHRODINGER="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/"
   export SCHRODINGER_PYTHONPATH="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/internal/lib/python2.7/site-packages"
   export PELE="/shared/work/NBD_Utilities/PELE/PELE_Softwares/bin/PELE1.7.1/"

   export LC_ALL=C; unset LANGUAGE
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/shared/work/NBD_Utilities/PELE/PELE_Softwares/local_deps/pele_deps/boost_1_52/lib:$LD_LIBRARY_PATH
   export SRUN=1  # this is to avoid having to set usesrun: true in input.yaml
   
   source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh
   conda activate /shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/envs/peleplatform-1.6.2

   python -c "import pele_platform; print('Using PELEPlatform, version', pele_platform.__version__)"
   python -m pele_platform.main input_fast.yaml
   
   
**PelePlatform - v1.6.1**

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J peleplat_tests
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=2
   #SBATCH --mem-per-cpu=1000

   module purge

   module load intel
   module load intel-oneapi
   module load imkl

   export SCHRODINGER="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/"
   export SCHRODINGER_PYTHONPATH="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/internal/lib/python2.7/site-packages"
   export PELE="/shared/work/NBD_Utilities/PELE/PELE_Softwares/bin/PELE1.7.1/"

   export LC_ALL=C; unset LANGUAGE
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/shared/work/NBD_Utilities/PELE/PELE_Softwares/local_deps/pele_deps/boost_1_52/lib:$LD_LIBRARY_PATH
   export SRUN=1  # this is to avoid having to set usesrun: true in input.yaml

   source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh
   conda activate /shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/envs/peleplatform-1.6.1
   
   python -c "import pele_platform; print('Using PELEPlatform, version', pele_platform.__version__)"
   python -m pele_platform.main input_fast.yaml


**PelePlatform - v1.6**

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J peleplat_tests
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=5
   #SBATCH --mem-per-cpu=1000

   module purge
   module load intel-oneapi
   module load imkl

   source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh
   conda activate /shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/envs/peleplatform-1.6.0

   export SCHRODINGER="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/"
   export SCHRODINGER_PYTHONPATH="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/internal/lib/python2.7/site-packages"
   export PELE="/shared/work/NBD_Utilities/PELE/PELE_Softwares/bin/PELE1.7.1/"

   export LC_ALL=C; unset LANGUAGE
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/shared/work/NBD_Utilities/PELE/PELE_dependencies/boost-1.66.0/lib:$LD_LIBRARY_PATH
   export SRUN=1  # this is to avoid having to set usesrun: true in input.yaml

   python -m pele_platform.main input.yaml


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


PelePlatform + singularity (cluster)
------------------------------------

**Last Update:** 21-12-2021

**PelePlatform - v1.6.1 + PELE ++ Singularity v1.7.1**

.. code-block:: bash
   
   #!/bin/bash
   #SBATCH -J peleplat
   #SBATCH --output=peleplat_%j.out
   #SBATCH --error=peleplat_%j.err
   #SBATCH --ntasks=5
   #SBATCH --mem-per-cpu=1000
   
   ##################################################################
   module purge
   module load OpenMPI/3.1.4-GCC-8.3.0
   
   export PELE="/opt/PELE"
   export SCHRODINGER="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4"
   export SCHRODINGER_PYTHONPATH="/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/internal/lib/python2.7/site-packages"
   export PELE_LICENSE="/shared/work/NBD_Utilities/PELE/PELE_Softwares/bin/PELE1.7.1/licenses"
   export SINGULARITY_BIND="$PELE_LICENSE"
   export PELE_MPI_PARAMS="--verbose"
   export SINGULARITY_EXEC="/shared/work/NBD_Utilities/PELE/PELE_Softwares/containers/pele1.7.1_release.sif"
   export LC_ALL=C; unset LANGUAGE
   
   source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh
   conda activate /shared/work/NBD_Utilities/PELE/PELE_Softwares/PelePlatform/envs/peleplatform-1.6.1
   ##################################################################
   
   
   python -m pele_platform.main input.yaml



PelePlatform (tirant)
-------------------------

**Last Update:** 17-12-2021

**PelePlatform - v1.6.2, latest release**

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J peleplat_test
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=5
   #SBATCH --mem-per-cpu=1000

   module purge
   module load impi mkl
   module load miniconda

   source activate /storage/projects/cns14/Utilities/platform/envs/peleplatform-1.6.2

   export SCHRODINGER="/storage/projects/cns14/Utilities/schrodinger2021-4/"
   export SCHRODINGER_PYTHONPATH="/storage/projects/cns14/Utilities/schrodinger2021-4/internal/lib/python3.8/site-packages"
   export PELE="/storage/projects/cns14/Utilities/PELE/PELE1.7.1/"

   export LC_ALL=C; unset LANGUAGE
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/storage/projects/cns14/Utilities/PELE/dependencies/boost-1.66.0/lib:$LD_LIBRARY_PATH
   export SRUN=1  # this is to avoid having to set usesrun: true in input.yaml

   python -m pele_platform.main input.yaml
   
   
**PelePlatform - v1.6.1

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J peleplat_test
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=5
   #SBATCH --mem-per-cpu=1000

   module purge
   module load impi mkl
   module load miniconda

   source activate /storage/projects/cns14/Utilities/platform/envs/peleplatform-1.6.1

   export SCHRODINGER="/storage/projects/cns14/Utilities/schrodinger2021-4/"
   export SCHRODINGER_PYTHONPATH="/storage/projects/cns14/Utilities/schrodinger2021-4/internal/lib/python3.8/site-packages"
   export PELE="/storage/projects/cns14/Utilities/PELE/PELE1.7.1/"

   export LC_ALL=C; unset LANGUAGE
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/storage/projects/cns14/Utilities/PELE/dependencies/boost-1.66.0/lib:$LD_LIBRARY_PATH
   export SRUN=1  # this is to avoid having to set usesrun: true in input.yaml

   python -m pele_platform.main input.yaml


**PelePlatform - v1.6.0

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J peleplat_test
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=5
   #SBATCH --mem-per-cpu=1000

   module purge
   module load impi mkl
   module load miniconda

   source activate /storage/projects/cns14/Utilities/platform/envs/peleplatform-1.6.0

   export SCHRODINGER="/storage/projects/cns14/Utilities/schrodinger2021-4/"
   export SCHRODINGER_PYTHONPATH="/storage/projects/cns14/Utilities/schrodinger2021-4/internal/lib/python3.8/site-packages"
   export PELE="/storage/projects/cns14/Utilities/PELE/PELE1.7.1/"

   export LC_ALL=C; unset LANGUAGE
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/storage/projects/cns14/Utilities/PELE/dependencies/boost-1.66.0/lib:$LD_LIBRARY_PATH
   export SRUN=1  # this is to avoid having to set usesrun: true in input.yaml

   python -m pele_platform.main input.yaml
   

PeleSimulationAnalysis (cluster)
------------------------------------

**Last Update:** 05-07-2021

This script allows the user to create a dispersion plot of any two metrics from a PELE simulation. A third metric can be represented with a colorbar.

.. code-block:: bash

   # Generate plot with interactive
   interactive -n 1 -X

   # Import modules
   module purge
   module load intel-oneapi
   module load imkl

   # Set up conda
   source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh

   # Activate conda environment
   conda activate /shared/work/NBD_Utilities/PELE/PELE_Softwares/conda_envs/pele_analysis

   # Run PELEPlot.py
   python -m PELEPlot.run -i output/0/report_* -X 7 -Y 5

   # Or call its helper
   python -m PELEPlot.run --help


.. code-block:: none

   #Generate plot with interactive
   interactive -n 1 -X

   export PYTHONPATH=/work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2015_GNU/AdaptivePELE_1.5.1

   module load Python/2.7.10-foss-2015a

   python /work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2015_GNU/AdaptivePELE_1.5.1/AdaptivePELE/analysis/interactivePlot.py  5 6 8 --top topology.pdb --cpus 15 --min_clustsize 5

   (5 6) columns in run_report that will be plotted, starting by 1
   (8) number of adaptive steps
   (--top topology.pdb) if working with .xtc format instead of .pdb


   #Clustering of all the trajectories and selection of centroid representative

   module load Python/2.7.10-foss-2015a

   export PYTHONPATH=/work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2015_GNU/AdaptivePELE_1.5.1/

   #If using xtc
   python -m AdaptivePELE.analysis.clusterAdaptiveRun 200 5 6 STR --traj trajectory_ --report report_ --top topology.pdb --CA --cpus 50

   #If using pdb
   python -m AdaptivePELE.analysis.clusterAdaptiveRun 200 5 6 STR --traj trajectory_ --report report_ --CA --cpus 50


   (200) number of clusters - decide based on plot
   Output: ClusterMap.pdf
   --use_pdb (only in case of having pdb files with .xtc extension)


   #Generate movie of a selected trajectory:

   interactive -n 1 -X

   module load Python/2.7.14-intel-2018a

   export PYTHONPATH=/work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2_intel/AdaptivePELE_1.5.1/

   python /work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2015_GNU/AdaptivePELE_1.5.1/AdaptivePELE/analysis/backtrackAdaptiveTrajectory.py  5 123 1

   (5) epoch
   (123) trajectory number
   (2) snapshot

   #Genenerate n bestStructures from a metric

   interactive -n 1 -X

   module load Python/2.7.14-intel-2018a

   export PYTHONPATH=/work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2_intel/AdaptivePELE_1.5.1/

   python /work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2015_GNU/AdaptivePELE_1.5.1/AdaptivePELE/analysis/backtrackAdaptiveTrajectory.py  COM Distance -n 50


   #Plot with Gnuplot

   export PYTHONPATH=/work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2_intel/AdaptivePELE_1.5.1/

   module load Python/2.7.14-intel-2018a

   python /work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2_intel/AdaptivePELE_1.5.1/AdaptivePELE/analysis/plotAdaptive.py 8 5 6 run_report_ -points -zcol 4 | gnuplot -p
   python /work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2_intel/AdaptivePELE_1.5.1/AdaptivePELE/analysis/plotAdaptive.py 8 5 6 run_report_ -points -traj_col | gnuplot -p

   # Normal PELE

   export PYTHONPATH=/work/NBD_Utilities/PELE/PELE_Softwares/adaptive_types/adaptive_python_2_intel/AdaptivePELE_1.5.1/

   gnuplot

   plot for [i=1:X] 'run_report_'.i.'' using 5:6 title ''.i.''

   (X=number of processors in PELE)
                                 
.. code-block:: bash

   $ #Path: 
   $ /shared/work/NBD_Utilities/PELE/PELE_Templates/analisis.sl


Launch with: Copy and paste the analysis part you want to run to commandline


Pele++ (cluster)
------------------------------------

**Last Update:** 09-06-2021

**PELE-1.7.1**

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J PELE_MPI
   #SBATCH --output=mpi_%j.out
   #SBATCH --error=mpi_%j.err
   #SBATCH --ntasks=5        # Change this value to match CPUs in mpi run --ntasks=XXX 
   #SBATCH --mem-per-cpu=1000

   ##################################################################
   module purge
   export LC_ALL=C; unset LANGUAGE
   module load intel-oneapi
   module load imkl
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/shared/work/NBD_Utilities/PELE/PELE_dependencies/boost-1.66.0/lib:$LD_LIBRARY_PATH
   export PATH=/shared/work/NBD_Utilities/PELE/PELE_Softwares/bin/PELE1.7.1/bin:$PATH
   module list
   ##################################################################

   #CHOOSE NUMBER OF PROCESSORS TO USE i.e. XXX = 5 
   #srun -n XXX Pele_mpi pele.conf
   srun -n 5 Pele_mpi pele.conf


.. code-block:: bash

   $ # Path:
   $ /shared/work/NBD_Utilities/PELE/PELE_Templates/PELE_mpi/run_pele-1.7.1_nbd.sl

Launch with: `sbatch run_pele-1.7.1_nbd.sl`

**PELE-1.6**

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J PELE_MPI
   #SBATCH --output=mpi_%j.out
   #SBATCH --error=mpi_%j.err
   #SBATCH --ntasks=5        # Change this value to match CPUs in mpi run --ntasks=XXX
   #SBATCH --mem-per-cpu=1000

   ##################################################################
   module purge
   export LC_ALL=C; unset LANGUAGE
   module load impi/2018.1.163-iccifort-2018.1.163-GCC-6.4.0-2.28 wjelement/1.3-intel-2018a
   module load Crypto++/6.1.0-intel-2018a OpenBLAS/0.2.20-GCC-6.4.0-2.28
   export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so
   export LD_LIBRARY_PATH=/shared/work/NBD_Utilities/PELE/PELE_Softwares/local_deps/pele_deps/boost_1_52/lib:$LD_LIBRARY_PATH
   export PATH=/shared/work/NBD_Utilities/PELE/PELE_Softwares/bin/PELE1.6/bin:$PATH
   module list
   ##################################################################

   #CHOOSE NUMBER OF PROCESSORS TO USE i.e. XXX = 5
   #srun -n XXX Pele_mpi pele.conf
   srun -n 5 Pele_mpi pele.conf


.. code-block:: bash

   $ # Path:
   $ /shared/work/NBD_Utilities/PELE/PELE_Templates/PELE_mpi/run_pele-1.6_nbd.sl


Launch with: `sbatch run_pele-1.6_nbd.sl`


AI Environment (cluster)
-------------------------

**Last Update:** 02-03-2022

.. code-block:: bash
   
   #!/bin/bash
   #SBATCH -J ai_env
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=2
   #SBATCH --mem-per-cpu=1000

   module purge
   source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh
   conda activate /shared/work/NBD_Utilities/conda_envs/aienv
   
   python ai_script.py
   
   
AnalogsSearch (Office)
---------------------------

**Last Update:** 19-03-2020

.. code-block:: bash

   #Read the docs for more info in the possible searches and commands:
   # https://danielsoler93.github.io/analogs_finder/

   export PYTHONPATH=/data/software/python_scripts/analogs_finder/v1.1/
   python -m analogs_finder.main database.sd query.sdf --combi_subsearch


.. code-block:: bash

   $ # Path:
   $ /shared/data-nbdcalc01/software/python_scripts/analogs_finder/analogs.shi

Launch with: `bash analogs.sh`

MDPocket (Office)
--------------------

**Last Update:** 02-01-2020

.. code-block:: none

   README MDpocket
   SUWIPA April 4, 2019.


  1. Cpptraj to extract snapshots from the autoimage & stripwater trajectory
      #####
      parm ../run1_stripwatmembrane.top

      trajin ../run1_trajautoimage_md14-md19_pro450ns_stripwater.x 1 45000 10

      reference ../initial_stripwatmembrane.crd

      rms reference :1-296@CA,C,N,O
      trajout snapshots/snap.pdb pdb multi
      go
      #####
      Noted !! use multi command to save pdb into seperate files.


   2. To convert snap.pdb.#  to snap_#.pdb

      under directory snapshots run command:
      ls | cut -f3 -d"." | awk '{print "mv snap.pdb."$0" snap_"$0".pdb"}' | sh


   3. use python script to create mdpocket input file (containing all snap_#.pdb files)

      python createMDPocketInputFile.py /home/ssaenoon/Alm_Par/MD_PAR2/AMBERMD/cutNter/run1/Analysis/MDpocket/snapshots mdpocket_input.txt

   4. Run MDpocket using fpoket V2:
      /dist/fpocket/fpocket2/bin/mdpocket -L mdpocket_input.txt

   5. Visulize the density grid (output "mdpout_dens_grid.dx" in VMD) - adjusting the isovalue for your selected pocket to be separated.

   6. Use this python script to extract the selected_mdpoket_iso#.pdb

       usage: python extractISOPdb.py path/my_dx_file.dx outputname.pdb isovalue

       example: python extractISOPdb.py  mdpout_dens_grid.dx mdpout_dens_iso3.pdb 3

   7. In PYMOL: open file "mdpout_dens_iso3.pdb"
       in mode - selecting "molecule"  --> select your selected pocket  then save
       > Export Molecule
       > Swlwct "sele"
       > save file.pdb   eg. mdpocket_selected_pocket_iso3.pdb

   8. Then run /dist/fpocket/fpocket2/bin/mdpocket -L mdpocket_input.txt -f  mdpocket_selected_pocket_iso3.pdb -v 10000

   9. In the output file "mdpout_descriptors.txt" containing many columns, use:

      > awk '{print $1}' mdpout_descriptors.txt > snapshot.txt
      > awk '{print $2}' mdpout_descriptors.txt > volume.txt
      ...
      paste snapshot.txt volume.txt > snapshot_volume.txt



.. code-block:: bash

   $ # Path:
   $ /shared/data-nbdcalc01/software/MDpocket/mdpocket_readme_suwipa/README_MDpocket


Launch with: Follow instructions and copy paste to command line


CAVIAR (cluster)
----------------

**Last Update:** 08-07-2021

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J caviar
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=1
   #SBATCH --mem-per-cpu=1000
   
   module purge
   module load intel-oneapi
   module load imkl
   
   source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh
   conda activate /shared/work/NBD_Utilities/miniconda3/envs/caviar
   
   caviar -code 1dwc


PSI4 (cluster)
--------------

**Last Update:** 15-11-2021

.. code-block:: bash

   #!/bin/bash
   #SBATCH -J PSI4
   #SBATCH --output=report_%j.out
   #SBATCH --error=report_%j.err
   #SBATCH --ntasks=16
   #SBATCH --time=1:00:00
   
   module purge
   source /shared/work/NBD_Utilities/PSI4/psi4conda/etc/profile.d/conda.sh
   conda activate

   psi4 -i input.in -o output.dat -n $SLURM_NPROCS 
