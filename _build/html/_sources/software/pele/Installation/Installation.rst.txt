############################
Installation
############################

In this section we will install the next software:

    1) PELE++ (The main C++ source code)

    2) PELE Platform (Python features on top of the C++)

Option 1 - Singularity - (Recommended)
==========================================

.. code-block:: bash

    git clone https://github.com/NostrumBioDiscovery/pele_platform.git
    
    cd pele_platform/singularity/
    
    bash create_pele_image.sh (You will need acces to PELE dockerhub)
    
    cd test/
    
    #Change the licenses and folders inside singularity.sl (IT section)
    
    bash singularity.sl  #If not queue system
    
    sbatch singularity.sl  #If slurm queue system


Option 2 - Manual
=====================

PELE++
+++++++++++++++++++++++++

External Requirements: OpenMPI

Send an e-mail to daniel.soler@nostrumbiodiscovery.com if you are interested on receiving the commercial software. 
After revision of your application, we will send you a form to fill in with your machine specifications.
Then, you will recieve the PELE (pele.zip) binary containing the licenses to run and a test case to check the installation.

Test PELE installation
``````````````````````````````

.. code-block:: bash

    unzip PELE-1.6.zip 
    tar -xvf PELE-1.6.tgz
    mv /path/to/pele_licenses PELE-1.6/licenses/
    cd PELE-1.6/samples/aspirin
    chmod -R u+wrx .
    #mpirun must be in PATH
    mpirun -np 3 ../../bin/Pele_mpi control_file --license-directory ../../licenses

(You may have to set some environment variables by exporting LD_LIBRARY_PATH)

**If the error** ``what():  locale::facet::_S_create_c_locale name not valid`` arises please run the command below
and execute again

.. code-block:: bash

   export LC_ALL=C; unset LANGUAGE



PelePlatform
++++++++++++++

ExternalRequirements:

  - Academic Schrodinger
    

Installation:
   
  https://nostrumbiodiscovery.github.io/pele_platform/installation/index.html

Test PelePlatform installation
`````````````````````````````````

  https://nostrumbiodiscovery.github.io/pele_platform/installation/index.html#test-it-works


