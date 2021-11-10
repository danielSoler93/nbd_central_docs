==========================
AlphaFold
==========================
This documentation provides the information and templates to run `Alpha Fold <https://github.com/deepmind/alphafold>`_.

The parameters needed to run Alpha Fold are:

	* **ALPHAFOLD_DATA_PATH:** Absolute path to folder with databases.
	* **ALPHAFOLD_MODELS:** Absolute path to folder with models.
	* **pwd:** Path to Singularity Image File (SIF) file.
	* **fasta_paths:** Path to the input sequence in fasta format.
	* **uniref90_database_path:** Path to Uniref90 database for use by JackHMMER.
	* **mgnify_database_path:** Path to the MGnify database for use by JackHMMER.
	* **bfd_database_path:** Path to the BFD database for use by HHblits.
	* **uniclust30_database_path:** Path to Uniclust30 database for use by HHblits.
	* **pdb70_database_path:** Path to PDB70 database for use by HHsearch.
	* **template_mmcif_dir_** Path to a directory with template mmCIF structures, each named <pdb_id>.cif.
        * **uniprot_database_path** Path to the UniProt database for AlphaFold Multimer.
	* **obsolete_pdbs_path:** Path to a file mapping obsolete PDB IDs to their replacements.
	* **max_template_date:** Maximum template release date to consider (ISO-8601 format - i.e. YYYY-MM-DD). Important if folding historical test sets. Default is None.
	* **output_dir:** Path to a directory that will store the results.
	* **model_preset:** ['monomer','monomer_casp14','monomer_ptm','multimer']. Control which AlphaFold model use, choosing between the original model used at CASP14 with no ensembling (monomer). the original model used at CASP14 with num_ensemble=8, matching our CASP14 configuration. This is largely provided for reproducibility as it is 8x more computationally expensive for limited accuracy gain (+0.1 average GDT gain on CASP14 domains) (monomer_casp14). the original CASP14 model fine tuned with the pTM head, providing a pairwise confidence measure. It is slightly less accurate than the normal monomer model ('monomer_ptm'). The AlphaFold-Multimer model, to use this model, provide a multi-sequence FASTA file. In addition, the UniProt database should have been downloaded ('multimer').
	* **db_preset:** ['reduced_dbs', 'full_dbs', 'casp14']. Choose preset model configuration - no ensembling and smaller genetic database config (reduced_dbs), no ensembling and full genetic database config (full_dbs) or full genetic database config and 8 model ensemblings (casp14). Default is full_dbs.
	* **benchmark:** [True, False]. Run multiple JAX model evaluations to obtain a timing that excludes the compilation time, which should be more indicative of the time required for inferencing many proteins. Default is False. 


:Important: The reference databases and models were downloaded in the directory **/shared/work/NBD_Utilities/AlphaFold/databases** and the singularity image file (alphafold_2.1.0.sif) of AlphaFold is available at **/shared/work/NBD_Utilities/AlphaFold**

:Important: The max_template_date flag is mandatory when running AlphaFold. If you are predicting the structure of a protein that is already in PDB and you wish to avoid using it as a template, then max_template_date must be set to be before the release date of the structure. If you do not need to specify a date, by default we set today's date. For example, if we are running the simulation on August 7th 2021, we set -- max_template_date = 2021-08-07.

=======================================
Running AlphaFold within Singularity
=======================================

Here is an example on how to run AlphaFold.
First, we need a protein sequence in FASTA format.

::

    >5ZE6_1
    MNLEKINELTAQDMAGVNAAILEQLNSDVQLINQLGYYIVSGGGKRIRPMIAVLAARAVGYEGNAHVTIAALIEFIHTATLLHDDVVDESDMRRGKATANAA
    FGNAASVLVGDFIYTRAFQMMTSLGSLKVLEVMSEAVNVIAEGEVLQLMNVNDPDITEENYMRVIYSKTARLFEAAAQCSGILAGCTPEEEKGLQDYGRYLG
    TAFQLIDDLLDYNADGEQLGKNVGDDLNEGKPTLPLLHAMHHGTPEQAQMIRTAIEQGNGRHLLEPVLEAMNACGSLEWTRQRAEEEADKAIAALQVLPDTP
    WREALIGLAHIAVQRDR

If we want to run AlphaFold in, for example, the directory ``AlphaFold/test``

::

    user@login01:~$  cd AlphaFold/test
    user@login01:AlphaFold/test$  mkdir alphafold_output # Create the directory for AlphaFold output
    user@login01:AlphaFold/test$  ls # The directory should contain the singularity image file (.sif) and the input FASTA sequence
    alphafold_output alphafold_2.1.0.sif input.fasta 
    

To run Alpha Fold, please change in the following template:
	* output_dir
	* fasta_paths

**Alpha Fold - v2.0 - Template to run**

::

    The memory needed for a job depends on the length of the input FASTA sequence and the number of models used. 
    Consider increasing the memory if you are working with a large sequence or with all the models.
    

.. code-block:: bash 
    
    #!/bin/bash
    #SBATCH --job-name alphafold-run
    #SBATCH --gres=gpu:1
    #SBATCH --cpus-per-task=8
    #SBATCH --mem=40G
    
    #set the environment PATH
    export PYTHONNOUSERSITE=True
    ALPHAFOLD_DATA_PATH=/shared/work/NBD_Utilities/AlphaFold/databases
    ALPHAFOLD_MODELS=/shared/work/NBD_Utilities/AlphaFold/databases/params

    module load CUDA/9.2.88-iccifort-2018.1.163-GCC-6.4.0-2.28
    module load cuDNN
    export CUDA_VISIBLE_DEVICES=-1

    #Run the command
    singularity run --nv \
     -B $ALPHAFOLD_DATA_PATH:/data \
     -B $ALPHAFOLD_MODELS \
     -B .:/etc \
     --pwd  /app/alphafold alphafold_2.1.0.sif \
     --fasta_paths=/path/to/input/sequence/input.fasta  \
     --uniref90_database_path=/data/uniref90/uniref90.fasta  \
     --data_dir=/data \
     --mgnify_database_path=/data/mgnify/mgy_clusters.fa   \
     --bfd_database_path=/data/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt \
     --uniclust30_database_path=/data/uniclust30/uniclust30_2018_08/uniclust30_2018_08 \
     --pdb70_database_path=/data/pdb70/pdb70  \
     --template_mmcif_dir=/data/pdb_mmcif/mmcif_files  \
     --obsolete_pdbs_path=/data/pdb_mmcif/obsolete.dat \
     --max_template_date= YYYY-MM-DD \
     --output_dir=/path/to/output/directory  \
     --model_preset='monomer' 

====================
AlphaFold output
====================

The outputs will be in a subfolder of `output_dir`. They
include the computed MSAs, unrelaxed structures, relaxed structures, ranked
structures, raw model outputs, prediction metadata, and section timings. The
`output_dir` directory will have the following structure:

::

    <target_name>/
        |- input/
	   |- features.pkl
	   |- ranked_{0,1,2,3,4}.pdb
	   |- ranking_debug.json
	   |- relaxed_model_{1,2,3,4,5}.pdb
	   |- result_model_{1,2,3,4,5}.pkl
	   |- timings.json
	   |- unrelaxed_model_{1,2,3,4,5}.pdb
	   |- msas/
	      |- bfd_uniclust_hits.a3m
	      |- mgnify_hits.sto
	      |- uniref90_hits.sto

The contents of each output file are as follows:

*   **features.pkl:** A pickle file containing the input feature NumPy arrays
    used by the models to produce the structures.
*   **unrelaxed_model_x.pdb:** A PDB format text file containing the predicted
    structure, exactly as outputted by the model.
*   **relaxed_model_x.pdb:** A PDB format text file containing the predicted
    structure, after performing an Amber relaxation procedure on the unrelaxed
    structure prediction (see Jumper et al. 2021, Suppl. Methods 1.8.6 for
    details).
*   **ranked_x.pdb:** A PDB format text file containing the relaxed predicted
    structures, after reordering by model confidence. Here `ranked_0.pdb` should
    contain the prediction with the highest confidence, and `ranked_4.pdb` the
    prediction with the lowest confidence. To rank model confidence, we use
    predicted LDDT (pLDDT) scores (see Jumper et al. 2021, Suppl. Methods 1.9.6
    for details).
*   **ranking_debug.json:** A JSON format text file containing the pLDDT values
    used to perform the model ranking, and a mapping back to the original model
    names.
*   **timings.json:** A JSON format text file containing the times taken to run
    each section of the AlphaFold pipeline.
*   **msas/:** - A directory containing the files describing the various genetic
    tool hits that were used to construct the input MSA.
*   **result_model_x.pkl:** A `pickle` file containing a nested dictionary of the
    various NumPy arrays directly produced by the model. In addition to the
    output of the structure module, this includes auxiliary outputs such as:

    *   Distograms (**distogram/logits** contains a NumPy array of shape [N_res,
        N_res, N_bins] and **distogram/bin_edges** contains the definition of the
        bins).
    *   Per-residue pLDDT scores (**plddt** contains a NumPy array of shape
        [N_res] with the range of possible values from 0 to 100, where 100
        means most confident). This can serve to identify sequence regions
        predicted with high confidence or as an overall per-target confidence
        score when averaged across residues.
    *   Present only if using pTM models: predicted TM-score (**ptm** field
        contains a scalar). As a predictor of a global superposition metric,
        this score is designed to also assess whether the model is confident in
        the overall domain packing.
    *   Present only if using pTM models: predicted pairwise aligned errors
        (**predicted_aligned_error** contains a NumPy array of shape [N_res,
        N_res] with the range of possible values from 0 to
        **max_predicted_aligned_error**, where 0 means most confident). This can
        serve for a visualisation of domain packing confidence within the
        structure.

================================
Running AlphaFold Multimer 
================================

The steps are the same as when folding a monomer, but it is needed to provide:

1. An input `fasta file with multiple sequences.

2. Set the **--model-preset** flag to 'multimer'.

3. Optionally set the **--is_prokaryote_list** flag with booleans that determine whether all input sequences in the given `fasta` file are prokaryotic. If that is not the case or the origin is unknown, set to `false` for that `fasta`.

Example
#########

In this tutorial we will fold a multimer using AlphaFold. We will be using a Human GITR-GITRL complex (PDB ID: 7KHD).

1. Sequence file preparation:
The multimer sequence can be download from the PDB databse. 

::

    >7KHD_1|Chains A, B|Tumor necrosis factor ligand superfamily member 18|Homo sapiens (9606)
    QLETAKEPCMAKFGPLPSKWQMASSEPPCVNKVSDWKLEILQNGLYLIYGQVAPNANYNDVAPFEVRLYKNKDMIQTLTNKSKIQNVGGTYELHVGDTIDLIFNSEHQVLKNNTYWGIILLANPQFIS
    >7KHD_2|Chains C, D|Tumor necrosis factor receptor superfamily member 18|Homo sapiens (9606)
    QRPTGGPGCGPGRLLLGTGTDARCCRVHTTRCCRDYPGEECCSEWDCMCVQPEFHCGDPCCTTCRHHPCPPGQGVQSQGKFSFGFQCIDCASGTFSGGHEGHCKPWTDCTQFGFLTVFPGNKTHNAVCVPGSPPAEP

If the multimer has repeated chains,the input fasta should be

::

    >7KHD_1|Chain A
    QLETAKEPCMAKFGPLPSKWQMASSEPPCVNKVSDWKLEILQNGLYLIYGQVAPNANYNDVAPFEVRLYKNKDMIQTLTNKSKIQNVGGTYELHVGDTIDLIFNSEHQVLKNNTYWGIILLANPQFIS
    >7KHD_2|Chain B
    QLETAKEPCMAKFGPLPSKWQMASSEPPCVNKVSDWKLEILQNGLYLIYGQVAPNANYNDVAPFEVRLYKNKDMIQTLTNKSKIQNVGGTYELHVGDTIDLIFNSEHQVLKNNTYWGIILLANPQFIS
    >7KHD_3|Chain C
    QRPTGGPGCGPGRLLLGTGTDARCCRVHTTRCCRDYPGEECCSEWDCMCVQPEFHCGDPCCTTCRHHPCPPGQGVQSQGKFSFGFQCIDCASGTFSGGHEGHCKPWTDCTQFGFLTVFPGNKTHNAVCVPGSPPAEP
    >7KHD_4|Chain D
    QRPTGGPGCGPGRLLLGTGTDARCCRVHTTRCCRDYPGEECCSEWDCMCVQPEFHCGDPCCTTCRHHPCPPGQGVQSQGKFSFGFQCIDCASGTFSGGHEGHCKPWTDCTQFGFLTVFPGNKTHNAVCVPGSPPAEP

In our multimer, chains A-B and chains C-D are repeated.

Then, submit the following sh file:

::

  When running AlphaFold Multimer, it is needed to define UniProt's database file.

.. code-block:: bash

  #!/bin/bash
  #SBATCH --job-name af_multimer
  #SBATCH --cpus-per-task=8
  #SBATCH --mem=20G

  #set the environment PATH
  export PYTHONNOUSERSITE=True
  ALPHAFOLD_DATA_PATH=/shared/work/NBD_Utilities/AlphaFold/databases
  ALPHAFOLD_MODELS=/shared/work/NBD_Utilities/AlphaFold/databases/params

  module purge
  module load CUDA/9.2.88-iccifort-2018.1.163-GCC-6.4.0-2.28
  module load cuDNN
  export CUDA_VISIBLE_DEVICES=-1

  #Run the command
  singularity run --nv \
   -B $ALPHAFOLD_DATA_PATH:/data \
   -B $ALPHAFOLD_MODELS \
   -B .:/etc \
   --pwd  /app/alphafold  alphafold_2.1.0.sif \
   --data_dir=/data \
   --fasta_paths=/shared/work/NBD_Utilities/AlphaFold/test_container/af_multimer/sep_chains/7khd.fasta \
   --uniref90_database_path=/data/uniref90/uniref90.fasta  \
   --data_dir=/data \
   --mgnify_database_path=/data/mgnify/mgy_clusters.fa   \
   --bfd_database_path=/data/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt \
   --uniclust30_database_path=/data/uniclust30/uniclust30_2018_08/uniclust30_2018_08 \
   --pdb_seqres_database_path=/data/pdb_seqres/pdb_seqres.txt \
   --uniprot_database_path=/data/uniprot/uniprot.fasta \
   --template_mmcif_dir=/data/pdb_mmcif/mmcif_files  \
   --obsolete_pdbs_path=/data/pdb_mmcif/obsolete.dat \
   --max_template_date=2021-03-03 \
   --model_preset='multimer' \
   --output_dir=/shared/work/NBD_Utilities/AlphaFold/test_container/af_multimer/sep_chains/7khd
