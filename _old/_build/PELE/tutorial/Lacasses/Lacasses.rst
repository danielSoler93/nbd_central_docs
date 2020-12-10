##############################################
Lacasses: Mutant design for ligand fitting
##############################################

**Aniline polymerization with laccases**: Laccases are multicopper oxidases capable of oxidizing a wide range of aromatic and phenolic compounds. The reaction occurs in a copper, and the electron moves to the trinuclear copper cluster, where it will be accepted by molecular oxygen releasing water as the final by-product.
The reaction in a copper molecule (T1) and the electron move to the trinuclear copper cluster where will be accepted by molecular oxygen releasing water as the final by-product.

Aniline is an arylamine (highly toxic in the monomeric form) with many applications when polymerized at low pH. The protonation state of the monomer is translated into a conductive polymer with several industrial applications (Figure 10). The idea is to replace toxic chemical oxidants with a green biocatalyst like a laccase. 

.. figure:: system.png
    :align: center

    Conductive polyaniline (PANI) production

The tutorial is focused on the limiting step of PANI production, the aniline monomers oxidation by laccase and an enhanced variant. Before starting the simulations several points have to be mentioned.

- There are several histidines and a cysteine coordinating the copper molecules. Therefore, it is very important to check the protonation state of all these residues before starting any simulation.

- At the working pH of the system (pH=3), the aniline monomer has the amine group protonated.

- Theoretically, the coppers have a +2 charge, but in nature, the charge is distributed onto the coordinating residues, so a +1 charge is more realistic. 


***********
Objective
***********

- Study aniline interaction with 7D5
- Observe the effect of two mutations towards enzyme-ligand interaction

**************
Preparation
**************

To start the simulation, we need the complex, the ligand, the ligand parameters, and the input control file.

Receptor
==========

**PDB - 7D5** crystal processed with Protein Preparation Wizard at pH 3 (Schrodinger). For this system is very important to manually check the histidine protonation states to coordinate with the four different coppers of the laccase.  

Generate 5JD3 mutant variant PDB using the mutating option of Maestro (Schrodinger) and introduce the mutations N207S and N263D

Ligand
=========

**Aniline**: Processed with LigPrep. Calculate protonation state at pH 3±0,5 + ESP charges obtained with Jaguar single-point (DFT/M06) calculation. Of note, the C-ring predicted to be neutral. 


Template of ligand
=====================

Output a mae file that contains the ligand only, then run that one through PlopRotTemp.py as explain `here <../../intro/SystemPreparation/SystemPreparation.html#ligand-preparation>`__ to obtain the parameters and rotamers of the ligand and place them in the DataLocal Folder as specified `here <../../molecularParameters.html#adding-the-generated-template-and-rotamer-library-files-to-pele>`_.


********************************************
Procedure: PELE Global Exploration
********************************************

Main characteristics of the simulation
========================================

- Starting poses for PELE Global Exploration: 10 initial poses at random positions around the whole protein were generated.
- Processors: 48
- Compute time: 12-15h


Control File specifics
==========================

Special required parameters for this simulation are:

Constraining Cu coordination distances
+++++++++++++++++++++++++++++++++++++++++

In other to fix a coordinated metal position, it is the addition of distant constraints to retain the molecule in a certain position.

.. code-block:: json

    { "type": "constrainAtomsDistance", "springConstant": 200, "equilibriumDistance": 2.39, "constrainThisAtom": "A:394:_ND1", "toThisOtherAtom": "A:604:_CU_" }

.. code-block:: json

    { "type": "constrainAtomsDistance", "springConstant": 200, "equilibriumDistance": 2.09, "constrainThisAtom": "A:455:_ND1", "toThisOtherAtom": "A:604:_CU_" }

.. code-block:: json

    { "type": "constrainAtomsDistance", "springConstant": 200, "equilibriumDistance": 2.01, "constrainThisAtom": "A:450:_SG_", "toThisOtherAtom": "A:604:_CU_" }


Distances to monitor
+++++++++++++++++++++++

In this example, we control the catalytic distance of the limiting step of the reaction.

.. code-block:: json
  
  {
  "metrics": [{
      "type": "com_distance",
      "selection_group_1": {
              "atoms": {
                      "ids": ["A:455:_NE2"]
              }
      },
      "selection_group_2": {
              "atoms": {
                      "ids": ["L:1:_N2_"]}
        }
    },]}



Results
==============

The ligand exploration of the aniline with the wild-type and the mutant will look like: 



The figure is generated with Gnuplot as explained `here <../../intro/GeneralAnalysis/GeneralAnalysis.html#plot-metrics>`__.

.. figure:: result_lacasses.png
   :align: center

   Binding energy versus H455-ANL distance (wild-type in red and mutant in blue).



One can see from the Figure how the ligand gets closer to the catalytic residue in the mutant than in the wild-type.



