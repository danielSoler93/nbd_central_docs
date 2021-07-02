=======
GROMACS
=======

GROMACS is a versatile package to perform molecular dynamics.


2021.2
------

`Documentation for this version <https://manual.gromacs.org/documentation/2021-current/index.html>`_

Installation path (NBD cluster)::
	
	/shared/work/NBD_Utilities/GROMACS/gromacs-2021.2

Dependencies::

	module load intel-oneapi/2021.1.0 intel imkl
	export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so


2019.6 (patched with plumed 2.7.1)
---------------------------------

`Documentation for this version <https://manual.gromacs.org/documentation/2019-current/index.html>`_

Installation path (NBD cluster)::
	
	/shared/work/NBD_Utilities/GROMACS/gromacs-2019.6

Dependencies::

	module load intel-oneapi
	export LD_LIBRARY_PATH=/shared/work/NBD_Utilities/PLUMED/plumed-2.7.1_impi/lib:$LD_LIBRARY_PATH
	export I_MPI_PMI_LIBRARY=/usr/lib64/libpmi.so


