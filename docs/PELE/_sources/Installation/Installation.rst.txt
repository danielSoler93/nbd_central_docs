############################
Installation
############################

In this section we will install the next software:

    1) PELE++ (The main C++ source code)

    2) PELE Platform (Python features on top of the C++)


PELE++
+++++++++++++++++++++++++

Send an e-mail to daniel.soler@nostrumbiodiscovery.com if you are interested on receiving the commercial software. 
After revision of your application, we will send you a form to fill in with your machine specifications.
Then, you will recieve the PELE (pele.zip) binary containing the licenses to run and a test case to check the installation.

Test PELE installation
``````````````````````````````
.. code-block:: bash

    unzip PELE-1.6.zip 
    tar -xvf PELE-1.6.tgz
    cd PELE-1.6/samples/aspirin
    chmod -R u+wrx .
    mpirun -np 3 ../../bin/Pele_mpi control_file --license-directory ../../licenses

(You may have to set some environment variables by exporting LD_LIBRARY_PATH)



PelePlatform
++++++++++++++

0) ExternalRequirements:

  - Academic Schrodinger

  - PyMol Python API (For Global exploration)
    
    .. code-block:: bash

        yum install gcc gcc-c++ kernel-devel python-devel tkinter python-pmw glew-devel
        freeglut-devel libpng-devel freetype-devel libxml2-devel glm-devel
        
        git clone https://github.com/schrodinger/pymol-open-source.git
        
        cd pymol-open-source
        
        python setup.py install (with same python you will use later)


1) Installation:
   
   - From Pypi: ``pip install pele_platform`` (with the right python as it will compile cython extensions) --> numpy and cython need to be installed.

   - From Conda: ``conda install -c NostrumBioDiscovery -c conda-forge pele_platform``

   - From Source code: 
     
        ``git clone https://github.com/NostrumBioDiscovery/pele_platform.git``

        ``cd pele_platform``

        ``python setup.py install``

2) go to ``lib/pythonX/site-packages/pele_platform/constants/constants.py`` and manually change this paragraph inside the  constants.py file

    .. code-block:: bash
    
      else:
          SCHRODINGER = "/sNow/easybuild/centos/7.4.1708/Skylake/software/schrodinger2017-4/"
          PELE = "/sNow/easybuild/centos/7.4.1708/Skylake/software/PELE/1.5.0.2524/"
          PELE_BIN = "/sNow/easybuild/centos/7.4.1708/Skylake/software/PELE/1.5.0.2524-intel-2018a/bin/Pele_mpi"
          MPIRUN = "/sNow/easybuild/centos/7.4.1708/Skylake/software/OpenMPI/2.1.2-GCC-6.4.0-2.28/bin/"
          LICENSE = "/sNow/easybuild/centos/7.4.1708/Skylake/software/PELE/licenses/"


Test PelePlatform installation
`````````````````````````````````
.. code-block:: bash

  git clone https://github.com/NostrumBioDiscovery/pele_platform.git
  cd pele_platform/test
  pytest 



