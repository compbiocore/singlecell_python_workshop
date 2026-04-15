# Single-Cell RNA-seq Analysis in Python Workshop

This workshop introduces single-cell RNA-seq (scRNA-seq) analysis in Python using [Scanpy](https://scanpy.readthedocs.io/) and the classic PBMC 3k dataset. The workshop is delivered as a Jupyter notebook and is designed to be run on [Oscar](https://docs.ccv.brown.edu/oscar/) at Brown University via the OpenOnDemand portal.

## Notebook

* `notebooks/scRNAseq_in_Python.ipynb` — Main workshop notebook covering quality control, normalization, dimensionality reduction, clustering, and visualization of scRNA-seq data.

## Running the notebook on Oscar via OpenOnDemand

### Prerequisites

1. **Clone this repository** to your Oscar home or data directory:
   ```bash
   git clone https://github.com/compbiocore/singlecell_python_workshop.git
   ```
2. **Obtain the Apptainer image** (`.sif` file) that contains all required Python packages. Save it to a location on Oscar (e.g. your home or `/oscar/data/` directory). Note the full path — you will need it in the steps below.

### Launching Jupyter via OpenOnDemand

1. Navigate to the Oscar OpenOnDemand portal:
   [https://ood.ccv.brown.edu/pun/sys/dashboard/batch_connect/sys/bc_ccv_jupyter_singularity/session_contexts/new](https://ood.ccv.brown.edu/pun/sys/dashboard/batch_connect/sys/bc_ccv_jupyter_singularity/session_contexts/new)

2. Under **Interactive Apps → Expert GUIs**, select **Jupyter Notebook for Apptainer Images**.

3. Fill in the form fields as follows:

   | Field | Value |
   |---|---|
   | **Path to apptainer image** | Full path to your `.sif` file, e.g. `/oscar/home/<username>/images/scanpy.sif` |
   | **Extra Jupyter Args** | `--notebook-dir=<path/to/cloned/repo>`, e.g. `--notebook-dir=/oscar/home/<username>/singlecell_python_workshop` |
   | **Partition** | Leave blank to use the default partition |
   | **Number of cores** | `1` |
   | **Memory per job** | `50G` |
   | **Number of GPUs** | `0` (no GPU needed for this workshop) |
   | **Condo account** | Leave blank unless you are using a condo |
   | **Number of hours** | `2` (increase if you need more time) |
   | **Additional Data Path** | Path to any extra data on Oscar you need accessible inside the container, e.g. `/oscar/data/<your-data-dir>` |

4. Click **Launch**.

5. Once the session starts (you will see it appear under **My Interactive Sessions**), click **Connect to Jupyter**.

6. In the Jupyter file browser, open `notebooks/scRNAseq_in_Python.ipynb` and run the cells.
