################################################################
RoRγ: Dissociation Pathway to guide unbiased binding simulation
################################################################

The Retinoic-acid related-orphan-receptor-C (RORC or RORγ) belongs to the nuclear hormone receptor (NHR) superfamily. It plays a fundamental role in the maturation of IL-17 producing Th17 cells is thus an attractive target for a variety of autoimmune diseases such as psoriasis and rheumatoid arthritis. RORγ features a multidomain structure characterized by an N-terminal DNA binding domain (DBD) and a C-terminal ligand-binding domain (LBD) capable of binding ligands and recruiting co-activator or co-repressor proteins. The LBD is a compact globular structure rich in α-helices. Its ligand-binding site is located deeply at the core of the domain. Inspection of all co-crystal structures does not reveal an obvious entry path into this deep buried site. An interesting and unresolved question remains related to how compounds active on RORγ-LBD
 diffuse in and out of the binding site, which is at the core of the LBD.


.. figure:: system.png
   :align: center 

   RoRγ system

***********
Objective
***********

To explore the exit pathway of ligand from the protein-ligand bound complex.

**************
Preparation
**************

To start the simulation, we need the complex, the ligand, the ligand parameters, and the input control file.

Receptor
==========

Process the protein complex (PDB id: 5VB7) with Protein Preparation Wizard (Schrodinger Program Suite) at pH 7.4 ± 0.5 to assign the protonation state to all ionizable residue as well as optimize the H-bond network.


Ligand
=========

Process with LigPrep module in Schrodinger Program Suite to assign protonation state at pH 7.4 ± 0.5 and tautomerization of the molecule. ESP charges is obtained from single-point calculation at MO6/6-31G** level of theory calculation within Jaguar software.

Template of ligand
=====================

Output a mae file that cointains the ligand only, then run that one through PlopRotTemp.py as explain `here <../../intro/SystemPreparation/SystemPreparation.html#ligand-preparation>`__ to obtain the parameters and rotamers of the ligand and place them in the DataLocal Folder as specified `here <../../molecularParameters.html#adding-the-generated-template-and-rotamer-library-files-to-pele>`_.


********************************************
Procedure-Part 1: PELE Exit Path
********************************************

Main characteristics of the simulation
========================================

- Using the starting structure from protein-ligand crystal complex.     
- AdaptivePELE mode: "Unbinding". This will move the ligand towards the bulk little by little.
- Processors: 20 processors
- Compute time: 1-2 hours

ControlFile specifics
==========================

Special required parameters for exit simulation are:

Unbinding Mode and Exit Condition
+++++++++++++++++++++++++++++++++++++++

.. code-block:: json


    {
    "simulation": {
        "type" : "pele",
        "params" : {
            "iterations" : 25,
            "processors" : 20,
            "peleSteps" : 5,
            "seed": 67890,
            "controlFile" : "pele.conf",
            "runEquilibration": true,
            "modeMovingBox" : "unbinding",
            "exitCondition" : {
                "type" : "metricMultipleTrajectories",
                "params" : {
                    "metricCol" : 4,
                    "exitValue" : 0.9,
                    "condition" : ">",
                    "numberTrajectories" : 5
    }}}},
    }

Where:

“runEquilibration": true is a keyword to run equilibration before  starting the exit simulation by means of a short minimization involving all the residues and sidechain within 4 Å from the ligand.

"modeMovingBox" : "unbinding" is a keyword to define a type of “box” as unbinding type. This “box” is defined to limit ligand perturbation within 7 Å from the center-of-mass of the ligand and is dynamically moved along the ligand path during exit simulation.


.. code-block:: json

    {
     "exitCondition" : {
          "type" : "metricMultipleTrajectories",
          "params" : {
          "metricCol" : 6,
          "exitValue" : 0.9,
          "condition" : ">",
          "numberTrajectories" : 5}
          },
    }

These parameters define the exit condition: where to stop the simulation if at least 5 trajectories ("numberTrajectories": 5) have the SASA value of ligand more than 0.9 (metricCol" : 6 defined as the matrix column number 6 in the “pele.cof”, "conditiodn" : ">", "exitValue" : 0.9).

Clutering
+++++++++++

We set the parameter "alternativeStructure" to true to start from
multiple different conformations of the same cluster and not only the
representative one.

.. code-block:: json

 {"params" : {
            "alternativeStructure": true,
            "ligandResname" : "AGO",
            "contactThresholdDistance" : 8
        },}

Metrics
+++++++++++

Distance between the atoms of the important residue HID479:NE2 and the ligand O2 is tracked.

.. code-block:: json
   
    {
    "metrics" : [
    { "type": "com_distance",
    "selection_group_1": { "atoms": { "ids": ["A:479:_NE2"] } },
    "selection_group_2": { "atoms": { "ids": ["L:602:_O2_"] } },
    "tag": "distance"
    },
    ]
    }


Results
==============

Exit Plot 
+++++++++++

To monitor the exit path we plot the SASA vs the number of steps

.. figure:: exit_plot.png
   :align: center

   Plot of Pele steps (X-axis) SASA (Y-axis) and Binding Energy (Z-axis).

Important residues in exit path
++++++++++++++++++++++++++++++++

To map the residues movement along the ligand exit pathway from the trajectory
make the movie as described `here <../../intro/AdaptiveMethodology/GeneralAnalysis/GeneralAnalysis.html#extract-the-movie-of-your-best-snapshot>`__ and plot all the residues close to the ligand of all snapshots together to see their fluctuation as seen in the Figure below.

To map the movement of residues along the ligand exit pathway, make a movie as described `here <../../intro/AdaptiveMethodology/GeneralAnalysis/GeneralAnalysis.html#extract-the-movie-of-your-best-snapshot>`__ and display all the residues close to the ligand in one Figure to see their fluctuations (see below).


.. figure:: exit_path.png
   :align: center

   The important residues along the dissociation pathway.



********************************************
Procedure-Part 2: PELE Entrance Path
********************************************

Main characteristics of the simulation
========================================

- Manually placed the ligand near the exit path
- Medium box containing the entry of the pocket and binding site
- Processors: 250 processors
- Compute time: 15 hours

ControlFile specifics
==========================

Special required parameters for exit simulation are:

Box definition
+++++++++++++++++++++++++++++++++++++++

We will set a small box containing entrance path and binding site

.. code-block:: json

    {
    "Perturbation": {
               "Box" : {
                         "radius" : 14,
                          "fixedCenter": [ -1.709, 22.433, 10.093],
           "type" : "sphericalBox"
        },
    }

Clustering well set
++++++++++++++++++++++++++

We must adjust the clustering accordingly to our system looking at the epoch/clustering(summary_clustering.txt) file.

.. code-block:: json 

          {"params" : {

              "values" : [2, 3, 5, 7],

              "conditions": [1.0, 0.75, 0.5]

            },}



Metrics
+++++++++++

RMSD to the native pose

.. code-block:: json
   
          {
             "type": "rmsd",
             "Native": { "path": "/gpfs/scratch/bsc72/bsc72156/NDB/ROR/PELE/apo/ago/5vb7_prw_processed.pdb" },
             "selection": { "chains": { "names": [ "L" ] } },
             "includeHydrogens": false,
             "doSuperposition": false,
             "tag" : "rmsd_lig"
          }


Results
==============

Entrance Plot
++++++++++++++++

To monitor the ligand entrance progress from its binding site we measure the distance between HID479:NE2 and ligand O2 atoms, as defined in the "com_distance" as "tag": "distance" (column number 7 in run_report file)


Entrance Path
++++++++++++++++++++++++++++++++

To map the movement of residues along the ligand exit pathway, make a movie as described `here <../../intro/AdaptiveMethodology/GeneralAnalysis/GeneralAnalysis.html#extract-the-movie-of-your-best-snapshot>`__ and display all the residues close to the ligand in one Figure to see their fluctuations (see below).


.. figure:: entrance_path.png
   :align: center

   The important residues along the entrance pathway.
