# Notebooks

## Apptainer image

A pre-built Docker image is available that includes all required packages (Scanpy, scVI-tools, Harmony, CuPy for GPU, etc.):

```
ericsalomaki/scanpy_rapids_gpu_v3:notebooks26.02-cuda13-py3.13-traj
```

**For this workshop, this image is the recommended way to run the notebook.** All packages are pre-installed, so no extra setup is required — just pull the image and launch via OpenOnDemand (see below).

If you need to run outside the container, set up a virtual environment by following the [Oscar Python virtual environment guide](https://docs.ccv.brown.edu/oscar/software/python-installs), then install the packages from `requirements.txt`. See the [full venv setup instructions in the main README](../README.md#prerequisites) for the exact commands.

Pull it to Oscar with Apptainer (run this on an Oscar login or compute node):

```bash
apptainer pull scanpy_rapids_gpu_v3.sif docker://ericsalomaki/scanpy_rapids_gpu_v3:notebooks26.02-cuda13-py3.13-traj
```

Note the full path where you save the `.sif` file — you will need it when launching the session.

## Running the notebook on Oscar via OpenOnDemand

See the [main README](../README.md) for step-by-step instructions on launching the notebook through the Oscar OpenOnDemand portal using the **Jupyter Notebook for Apptainer Images** app.

> **Note on GPU-accelerated tools:** The notebooks are written to run on CPU by default (standard Scanpy calls). When run inside the container on a GPU node, `cuml` / `cudf` / `rapids` are available and can be used to accelerate PCA, UMAP, and kNN construction significantly for large datasets.

---

## Path portability

All notebooks use [**pyhere**](https://pypi.org/project/pyhere/) to resolve file paths relative to the project root.
`here()` walks up from the current working directory until it finds `.here`, `.git`, `setup.py`, or similar root markers.
This means notebooks run correctly regardless of where the repository is cloned, and without any manual path configuration.

Key directories scaffolded at the repo root:

| Directory | Purpose |
|-----------|---------|
| `data/` | Downloaded datasets and output `.h5ad` files (`sc.settings.datasetdir`) |
| `figures/` | Saved plots (`sc.settings.figdir`) |

A `.here` file is placed at the repository root as an explicit anchor for `pyhere`.

**Required package:**
```bash
pip install pyhere
```

---

* `scRNAseq_in_Python.ipynb`: Workshop notebook for single-cell RNA-seq analysis using Scanpy and the PBMC3k dataset. Covers the full workflow from raw data loading through pathway enrichment. Key sections include:
  - AnnData data structure introduction
  - Raw data exploration (`sc.pl.highest_expr_genes`)
  - QC metrics, filtering, and doublet detection (Scrublet)
  - Normalization, highly variable gene selection, and scaling
  - Cell cycle scoring (Tirosh et al. 2016 gene lists)
  - PCA, UMAP, t-SNE, and Leiden clustering
  - Complete visualization gallery (violin, dotplot, heatmap, matrixplot, stacked violin, tracksplot)
  - Marker gene detection and cell type annotation
  - Data integration using `sc.tl.ingest` (PBMC3k reference → PBMC68k query)
  - **Integration comparison: Harmony vs scVI** with batch mixing UMAPs (§15)
  - **Clustering resolution optimization** — resolution sweep, UMAP grid, clustree hierarchy diagram (§16)
  - **Pathway enrichment: ORA & GSEA** via `gseapy` with MSigDB Hallmarks, GO, and KEGG gene sets (§17)
  - Workshop exercises at beginner / intermediate / advanced levels

  References: [clustering-2017](https://scanpy.readthedocs.io/en/1.10.x/tutorials/basics/clustering-2017.html), [clustering](https://scanpy.readthedocs.io/en/1.10.x/tutorials/basics/clustering.html), [integrating-data-using-ingest](https://scanpy.readthedocs.io/en/1.10.x/tutorials/basics/integrating-data-using-ingest.html), [plotting/core](https://scanpy.readthedocs.io/en/1.10.x/tutorials/plotting/core.html), [plotting/advanced](https://scanpy.readthedocs.io/en/1.10.x/tutorials/plotting/advanced.html)
