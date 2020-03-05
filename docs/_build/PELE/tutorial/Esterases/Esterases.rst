#############################################
Esterase: Mutant design for cavity creation
#############################################

Cavity creation to increase substrate promiscuity: Esterases are hydrolytic enzymes with a huge variety of industrial applications. These enzymes work with the catalytic triad system, where three residues (Ser/His/Asp) and water can break the ester bond, releasing the corresponding acid and alcohol (Figure 1). 


.. figure:: system.png
   :align: center 

   
   Catalytic triad mechanism

***********
Objective
***********

The aim of this project is to increase the substrate promiscuity of a certain esterase (PDB code: 5JD3). To achieve this goal several mutations will be proposed to create a cavity in the enzyme to fit several ligands. 

**************
Preparation
**************

To start the simulation we need complex, ligand, ligand parameters and the input controlfile.

Receptor
==========

PDB: 5JD3 crystal processed with Protein Preparation Wizard at pH 8 (Schrodinger).For this system is very important to manually check the catalytic triad histidine protonation.  

Generate 5JD3 mutant variant PDB using the mutating option of Maestro (Schrodinger) and introduce the mutations I92A, W96G, I16G.


Ligand
=========

Calculate protonation state at pH 8±0,5 + ESP charges obtained with Jaguar single-point (DFT/M06) calculation. Of note, the C-ring predicted to be neutral. 

Template of ligand
=====================

Output a mae file only cointaining the ligand, then run that one through PlopRotTemp.py as explain `here <../../intro/SystemPreparation/SystemPreparation.html#ligand-preparation>`__ to obtain the parameters and rotamers of the ligand and place them on the DataLocal Folder as specified `here <../../molecularParameters.html#adding-the-generated-template-and-rotamer-library-files-to-pele>`_.


********************************************
Procedure: PELE Local Exploration
********************************************

Main Charachteristic of the simulation
========================================

- Starting pose for PELE Local Exploration (check box definition)
- Processors: 48
- Compute time: 12-15h

ControlFile specifics
==========================

Special required parameters for this simulation are:

Box definition
+++++++++++++++++++++++++++++++++++++++

Since we know where the binding site is, a box is defined to reduce the exploration space and make the simulation easier. The ligand’s center of mass must be placed inside the box.

.. code-block:: json

  {"Box": {
    "type": "sphericalBox",
    "radius": 15,
     "fixedCenter": [-24.84, 6.36, 39.73]
      }
  }


Distances to monitor
++++++++++++++++++++++

We monitor the catalytic distance of the limiting step of the reaction and the distances between the residues of the catalytic triad.


.. code-block:: json
   
     {
     "metrics": [
            { "type": "com_distance",
              "selection_group_1": { "atoms": { "ids": ["A:15:_OG_"] } },
              "selection_group_2": { "atoms": { "ids": ["L:900:_C4_"] } },
              "tag": "S161-lig"
           },


           {
           "type": "com_distance",
            "selection_group_1": { "atoms": { "ids": ["A:195:_NE2"] } },
            "selection_group_2": { "atoms": { "ids": ["A:15:_HG_"] } },
             "tag": "S161-H286"
           },
           {
           "type": "com_distance",
            "selection_group_1": { "atoms": { "ids": ["A:192:_OD2"] } },
            "selection_group_2": { "atoms": { "ids": ["A:195:_HD1"] } },
            "tag": "asp-his"
           },]}
 

Results
==============

The resulting output of the simulations will be very different for both variants. In the wild type the ligand will be stick in the enzyme surface. The binding energies will be bad and the SASA high due to the exposition of the ligand.

In the other hand the mutant variant has a medium-size open cavity due to the mutations included to the protein. The binding energies are significantly better and the SASA extremely low due to the new cavity. 

.. figure:: result_esterases.png
   :align: center

   Binding Energy and SASA against the catalytic distance for the wild-type and the mutant variant.

Here we depict the produced cavity:

.. figure:: cavity_esterases.png
   :align: center

   Representation of the enzyme-ligand interaction

