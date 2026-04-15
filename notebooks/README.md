# Files

Files for your notebooks (Rmd, Quarto, Jupyter, etc) should go here. Make sure to describe your files in the README here or in the main one.

## Running on a cluster with Apptainer (recommended for GPU acceleration)

A pre-built Docker image is available that includes all required packages (Scanpy, scVI-tools, Harmony, CuPy for GPU, etc.):

```
ericsalomaki/scanpy_rapids_gpu_v3:notebooks26.02-cuda13-py3.13-traj
```

### Pull the image with Apptainer

```bash
# Pull from Docker Hub and convert to a Singularity Image File
apptainer pull scanpy_rapids_gpu_v3.sif docker://ericsalomaki/scanpy_rapids_gpu_v3:notebooks26.02-cuda13-py3.13-traj
```

### Launch Jupyter inside the container

```bash
# Start an interactive session with GPU access (adjust bind path to your data directory)
apptainer exec --nv \
    -B /path/to/your/data:/path/to/your/data \
    scanpy_rapids_gpu_v3.sif \
    jupyter notebook --no-browser --port=8888 --ip=0.0.0.0
```

### Submit via SLURM

```bash
#!/bin/bash
#SBATCH --job-name=sc_workshop
#SBATCH --partition=gpu
#SBATCH --nodes=1
#SBATCH --time=04:00:00
#SBATCH --mem=32G
#SBATCH --gres=gpu:1
#SBATCH --output=sc_workshop_%j.log

IMAGE=/path/to/scanpy_rapids_gpu_v3.sif
BIND=/path/to/your/project:/path/to/your/project

srun apptainer exec --nv -B $BIND $IMAGE \
    jupyter notebook --no-browser --port=8888 --ip=0.0.0.0
```

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

* `01_scanpy_pbmc_workshop.ipynb`: Initial starter workshop notebook for single-cell analysis in Scanpy using the PBMC3k tutorial dataset. Includes an outline plus runnable preprocessing, clustering, and marker gene analysis steps. Paths managed via `pyhere`.

* `02_scanpy_pbmc_basics_visualization.ipynb`: Comprehensive beginner workshop notebook for single-cell RNA-seq analysis using Scanpy and the PBMC3k dataset. Covers the full workflow from raw data loading through pathway enrichment. Key sections include:
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
