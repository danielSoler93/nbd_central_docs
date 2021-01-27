=======
PELE++
=======

Full documentation
------------------------

`Pele++ docs <https://nostrumbiodiscovery.github.io/pele_docs/>`_


Tutorial
---------

The steps for launch a simulation are:

* Prepare the complex
* Prepare the input file (.conf)
* Run command

You can find sample data to launch aspirin example in the NBD cluster. The steps to run the simulation are:

Change to a personal folder, for example (<USERNAME> refers to your system user):

.. code-block:: bash

   $ cd /shared/scratch/jobs/<USERNAME>

Copy sample data (includes the complex and the input file):

.. code-block:: bash

   $ cp -r /shared/work/NBD_Utilities/PELE/PELE_TestData/aspirin .

Copy the launching file:

.. code-block:: bash

   $ cp /shared/work/NBD_Utilities/PELE/PELE_Templates/PELE_mpi/run_pele_nbd.sl aspirin/

Launch the simulation:

.. code-block:: bash

	$ cd aspirin
	$ sbatch run_pele_nbd.sl

Check the simulation state (more info in `queue-system <../../compute_power/index.html#queue-system>`_):

.. code-block:: bash

	$ squeue


When the job is done, the outputs will be available in the folder **results**.



Generate your own pele control file
-----------------------------------

More information about the syntax of control file is available in `Pele++ reference manual <https://nostrumbiodiscovery.github.io/pele_docs/GeneralStructure/GeneralStructure.html>`_


Templates for launching
-----------------------

You can find a launching file (.sl) for the NBD cluster under:

-  **/shared/work/NBD_Utilities/PELE/PELE_Templates/PELE_mpi/**


