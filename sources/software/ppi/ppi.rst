========================
Protein-protein docking
========================

Here you will find how to use various protein-protein docking programs installed on the NBD cluster.

LightDock 0.9.0
----------------

`Official webpage <https://lightdock.org>`_

`External tutorial for this version <https://www.bonvinlab.org/education/HADDOCK24/LightDock-membrane-proteins/#lightdock-general-concepts>`_

Installation path (NBD cluster)::
	
	/shared/work/NBD_Utilities/LightDock

Load environment::

	source /shared/work/NBD_Utilities/miniconda3/etc/profile.d/conda.sh
	conda activate /shared/work/NBD_Utilities/LightDock/envs/lightdock/


Voronota(VoroMQA) 1.22 
-----------------------

`Documentation <https://bioinformatics.lt/wtsam/voromqa/help/standalone>`_

Installation path (NBD cluster)::
	
	/shared/work/NBD_Utilities/Voronota

Load environment::

	source /shared/work/NBD_Utilities/Voronota/etc/configure.sh


LZerD 
------

`Documentation <https://kiharalab.org/proteindocking/lzerd.php>`_

Installation path (NBD cluster)::
	
	/shared/work/NBD_Utilities/LZerD

Load environment and copy required files to current directory::

	source /shared/work/NBD_Utilities/LZerD/etc/configure.sh

Launch LZerD::

	runlzerd.sh receptor.pdb ligand.pdb     
