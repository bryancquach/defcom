# Detecting Footprints Containing Motifs (DeFCoM)

This respository includes the source code for the DeFCoM supervised ML genomic footprint classification framework described in [this publication](https://doi.org/10.1093/bioinformatics/btw740). If you use this tool in your research, please include the following citation:

> Quach, B., & Furey, T. S. (2017). DeFCoM: analysis and modeling of transcription factor binding sites using a motif-centric genomic footprinter. Bioinformatics, 33(7), 956-963.

_Note:_ This framework has not been maintained since 2017 and was written in Python 2.7. Please reach out if you are interested in collaborations to refactor the codebase. The `manuscript` branch includes source files that correspond to the [manuscript version](https://doi.org/10.1093/bioinformatics/btw740) of the tool.

## Documentation

For a general overview of genomic footprinting see this review by [Sung _et al._(2016)](https://doi.org/10.1038/nmeth.3766). DeFCoM was designed to learn patterns for chromatin accessibility signals at transcription factor binding sites across the genome from DNaseI-seq or ATAC-seq data. These learned transcription factor binding patterns can then be used to predict binding sites in new DNaseI-seq or ATAC-seq samples. The following image provides an overview of the DeFCoM framework:

![image](https://github.com/user-attachments/assets/76ac9d9d-b475-4947-affd-550b916fee5a)

For detailed documentation see the [Read the Docs page](https://defcom.readthedocs.io/en/latest/).

## Developer notes

Code structure (arrows represent dependencies based on import statements):

```mermaid
graph TD
    subgraph "defcom"
        defcom_main["__main__.py"]
        defcom_cli["cli.py"]
        defcom_defcom["defcom.py"]
        defcom_gene_sets["gene_sets.py"]
        defcom_ica["ica.py"]
        defcom_misc["misc.py"]
        defcom_nn["nn.py"]
    end

    subgraph "experiments"
        experiments_canned["canned.py"]
        experiments_dataset["dataset.py"]
        experiments_grid_search["grid_search.py"]
        experiments_learning_rate["learning_rate.py"]
        experiments_utils["utils.py"]
    end

    subgraph "tests"
        tests_context["context.py"]
        tests_test_defcom["test_defcom.py"]
        tests_test_gene_sets["test_gene_sets.py"]
        tests_test_ica["test_ica.py"]
        tests_test_misc["test_misc.py"]
    end

    setup["setup.py"]

    defcom_main --> defcom_cli
    defcom_cli --> defcom_defcom
    defcom_defcom --> defcom_gene_sets
    defcom_defcom --> defcom_ica
    defcom_defcom --> defcom_misc
    defcom_defcom --> defcom_nn

    experiments_canned --> defcom_defcom
    experiments_canned --> experiments_dataset
    experiments_canned --> experiments_utils
    experiments_grid_search --> defcom_defcom
    experiments_grid_search --> experiments_dataset
    experiments_learning_rate --> defcom_defcom
    experiments_learning_rate --> experiments_dataset

    tests_test_defcom --> defcom_defcom
    tests_test_gene_sets --> defcom_gene_sets
    tests_test_ica --> defcom_ica
    tests_test_misc --> defcom_misc

```
