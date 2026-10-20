# Differential expression with DESeq2 (Salmon input)

One R notebook, `DESeq2_analysis.ipynb`: Salmon `quant.sf` files → gene-level counts (tximport) →
DESeq2 → PCA, results table with gene symbols, volcano plots. It is a generic version of two
near-identical per-dataset notebooks; all dataset-specific values are set in one **Parameters** cell.

## Requirements
- R 4.3 with Bioconductor packages: DESeq2, tximport, ensembldb, AnnotationHub, org.Hs.eg.db,
  EnhancedVolcano, plus ggplot2 and IRkernel to run it in Jupyter.
- `conda env create -f environment.yml`, or install the packages with BiocManager (commented cell in the notebook).
- Internet access on first run (AnnotationHub downloads the EnsDb; it is cached afterwards).
- Human (Ensembl) annotation. For another species, change `ensdb_species` and the `org.*.eg.db` package.

## Inputs
1. Salmon output: `<quants_dir>/<sample>/quant.sf` for every sample.
2. A sample sheet CSV with columns `sample` (folder name) and `condition` (see `sample_sheet.example.csv`).
3. The Ensembl release (`ensdb_version`) should match the annotation your Salmon index was built from.

## Steps
1. Edit the Parameters cell (paths, `ref_level`, `test_level`, Ensembl version, volcano cutoffs).
2. Run all cells.

## Outputs (prefix set by `out_prefix`)
- `<prefix>_gene_counts.txt`: tximport gene-level counts.
- `<prefix>_results_nofilter.csv`: DESeq2 results for every gene with a non-NA result, with `symbol`.
  Fold change is `test_level / ref_level`.
- PCA and volcano plots
