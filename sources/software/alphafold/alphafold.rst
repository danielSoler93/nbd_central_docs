==========================
Alpha Fold
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
	* **obsolete_pdbs_path:** Path to a file mapping obsolete PDB IDs to their replacements.
	* **max_template_date:** Maximum template release date to consider (ISO-8601 format - i.e. YYYY-MM-DD). Important if folding historical test sets. Default is None.
	* **output_dir:** Path to a directory that will store the results.
	* **model_names:** Names of models to use.
	* **preset:** ['reduced_dbs', 'full_dbs', 'casp14']. Choose preset model configuration - no ensembling and smaller genetic database config (reduced_dbs), no ensembling and full genetic database config (full_dbs) or full genetic database config and 8 model ensemblings (casp14). Default is full_dbs.
	* **benchmark:** [True, False]. Run multiple JAX model evaluations to obtain a timing that excludes the compilation time, which should be more indicative of the time required for inferencing many proteins. Default is False. 

The reference databases and models were downloaded in the directory ``/shared/work/NBD_Utilities/Alphafold/databases`` 

To run Alpha Fold, please change in the following template:
	* output_dir
	* fasta_paths

.. warning::
    The memory needed for a job depends on the length of the input FASTA sequence. Consider increasing the memory if you are working with a large sequence.

**Alpha Fold - v2.0 - Template to run**

.. code-block:: bash 
    
    #!/bin/bash
    #SBATCH --job-name alphafold-run
    #SBATCH --time=08:00:00
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
     --pwd  /shared/work/NBD_Utilities/AlphaFold/test_container/alphafold /shared/work/NBD_Utilities/AlphaFold/test_container/alphafold/alphafold.sif \
     --fasta_paths=/shared/work/NBD_Utilities/AlphaFold/test_container/input.fasta  \
     --uniref90_database_path=/data/uniref90/uniref90.fasta  \
     --data_dir=/data \
     --mgnify_database_path=/data/mgnify/mgy_clusters.fa   \
     --bfd_database_path=/data/bfd/bfd_metaclust_clu_complete_id30_c90_final_seq.sorted_opt \
     --uniclust30_database_path=/data/uniclust30/uniclust30_2018_08/uniclust30_2018_08 \
     --pdb70_database_path=/data/pdb70/pdb70  \
     --template_mmcif_dir=/data/pdb_mmcif/mmcif_files  \
     --obsolete_pdbs_path=/data/pdb_mmcif/obsolete.dat \
     --max_template_date=2020-05-14   \
     --output_dir=/shared/work/NBD_Utilities/AlphaFold/test_container/alphafold_output  \
     --model_names='model_1','model_2','model_3','model_4','model_5' 

====================
AlphaFold output
====================

The outputs will be in a subfolder of `output_dir`. They
include the computed MSAs, unrelaxed structures, relaxed structures, ranked
structures, raw model outputs, prediction metadata, and section timings. The
`output_dir` directory will have the following structure:

::

    <target_name>/
        |-input/
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

