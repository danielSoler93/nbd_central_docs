==========================
Alpha Fold
==========================
This documentation provides the infromation and templates to run Alpha Fold.

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

