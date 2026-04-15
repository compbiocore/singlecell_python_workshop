# Files

Files for your notebooks (Rmd, Quarto, Jupyter, etc) should go here. Make sure to describe your files in the README here or in the main one.

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

* `01_scanpy_pbmc_workshop.ipynb`: Initial starter workshop notebook for single-cell analysis in Scanpy using the PBMC3k tutorial dataset. Includes an outline plus runnable preprocessing, clustering, and marker-gene analysis steps. Paths managed via `pyhere`.

* `02_scanpy_pbmc_basics_visualization.ipynb`: Comprehensive beginner workshop notebook for single-cell RNA-seq analysis using Scanpy and the PBMC3k dataset. Covers the full workflow from raw data loading through cell type annotation and data integration. Key sections include:
  - AnnData data structure introduction
  - Raw data exploration (`sc.pl.highest_expr_genes`)
  - QC metrics, filtering, and doublet detection (Scrublet)
  - Normalization, highly variable gene selection, and scaling
  - Cell cycle scoring (Tirosh et al. 2016 gene lists)
  - PCA, UMAP, t-SNE, and Leiden clustering
  - Complete visualization gallery (violin, dotplot, heatmap, matrixplot, stacked violin, tracksplot)
  - Marker gene detection and cell type annotation
  - Data integration using `sc.tl.ingest` (PBMC3k reference → PBMC68k query)
  - Workshop exercises at beginner / intermediate / advanced levels

  References: [clustering-2017](https://scanpy.readthedocs.io/en/1.10.x/tutorials/basics/clustering-2017.html), [clustering](https://scanpy.readthedocs.io/en/1.10.x/tutorials/basics/clustering.html), [integrating-data-using-ingest](https://scanpy.readthedocs.io/en/1.10.x/tutorials/basics/integrating-data-using-ingest.html), [plotting/core](https://scanpy.readthedocs.io/en/1.10.x/tutorials/plotting/core.html), [plotting/advanced](https://scanpy.readthedocs.io/en/1.10.x/tutorials/plotting/advanced.html)
