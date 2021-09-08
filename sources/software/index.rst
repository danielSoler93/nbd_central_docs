.. NBD documentation master file, created by
   sphinx-quickstart on Mon Dec  4 11:58:09 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Software
=========

Summary
----------

The NBD's main technologies are:

- PELE++ (`PELE docs <https://nostrumbiodiscovery.github.io/pele_docs/>`_)

- PELE Platform (`PELE Platform <https://nostrumbiodiscovery.github.io/pele_platform/>`_)

- Adaptive PELE Simulation (`Adaptive PELE docs <https://adaptivepele.github.io/AdaptivePELE/>`_)

- Frag PELE Simulation (`FrAG PELE docs <https://carlesperez94.github.io/frag_pele/>`_)

- MSM PELE Simulation (`MSM PELE docs <https://nostrumbiodiscovery.github.io/msm_pele/>`_)

- NAMD Molecular Dynamics (`NAMD docs <http://www.ks.uiuc.edu/Research/namd/>`_)

- analogs finder  (`analogs finder docs <https://nostrumbiodiscovery.github.io/analogs_finder/>`_)

- modtox AI (`modtox AI docs  <https://nostrumbiodiscovery.github.io/modtox/>`_)

- schrodinger platform (`schrodinger docs  <https://www.schrodinger.com/>`_)

- GROMACS (`GROMACS docs <https://manual.gromacs.org/documentation/>`_)

- PLUMED (`PLUMED docs <https://www.plumed.org/doc>`_)


Job launching Templates
-------------------------

.. toctree::
   templates/documentation

PELE
---------

Pele is our in-house comercial software that we sell and use for speeding up DD projects

.. toctree::
   pele/documentation

.. toctree::
   peleplatform/documentation

.. toctree::
   adaptive/documentation

NAMD
----------

NAMD is used to perform molecular dynamics over several system to study its dynamics along time

.. toctree::
   MD/documentation

Schrodinger
------------------

Schrodinger is used for virtual screening purposes and system preparation. 

.. toctree::
   Schrodinger/documentation

Python packages
---------------------

A micelaneous of several Python Packages built along the years

.. toctree::
   python/packages

GROMACS
------------------
GROMACS is a versatile package to perform molecular dynamics.

.. toctree::
   GROMACS/documentation

PLUMED
------------------
PLUMED is a plugin that works with a large number of molecular dynamics codes. PLUMED can also work as a Command Line Tool to perform analysis on trajectories saved in most of the existing formats.

.. toctree::
   PLUMED/documentation


Nice DCV
------------

NICE DCV is the remote 3D visualization technology that enables Technical Computing users to connect to OpenGL applications running in a data center. (https://aws.amazon.com/es/hpc/dcv/)

.. toctree::
   Nice/nice

Tests
----------

Here you will find information of the automatic tests
run on nbdcalc01 computer


.. toctree::
   tests/index

NewComers
-------------

Here you will find how to set up your laptop to access NBD facilities

.. toctree::
   new_comers/index

AlphaFold
------------
Here you will find how to run AlphaFold

.. toctree::
   alphafold/alphafold

Protein-protein docking
-----------------------
Here you will find information about several PPI software installed in our cluster

.. toctree::
   ppi/ppi
