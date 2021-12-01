====
PSI4
====

PSI4 is the latest in the family of the PSI quantum chemistry programs. 
PSI4 is a fully open-source project hosted at: `psicode.org <https://psicode.org/>`_

If you want to check-out input examples you can find a large set of them at: `/shared/work/NBD_Utilities/PSI4/psi4conda/share/psi4/samples`_


1.4.rc2
-------

`Documentation for this version <https://psicode.org/psi4manual/1.4.0/>`_

Installation path (NBD cluster)::
	
	/shared/work/NBD_Utilities/PSI4

Launching::

	source /shared/work/NBD_Utilities/PSI4/psi4conda/etc/profile.d/conda.sh
	conda activate

	psi4 -i /shared/work/NBD_Utilities/PSI4/psi4conda/share/psi4/samples/pubchem1/test.in -o output.dat 

