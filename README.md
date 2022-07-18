# S2I PyTorch Notebook

Custom Notebook built with Thoth s2i-minimal-notebook.

This custom notebook contains [PyTorch](https://pytorch.org/) related packages install with minimal notebook for Data Science usage. This image can be directly used if user needed these package while using the minimal jupyter notebook.

We have configured this repository to used pipenv and micropipenv python dependency managers.

# List of packages in pytorch-notebook

```
- bokeh
- cython
- dask
- dill
- distributed
- h5py
- ipywidgets
- matplotlib
- pandas
- plotly
- pyarrow
- s3fs
- scikit-image
- scikit-learn
- scipy
- seaborn
- sqlalchemy
- statsmodels
- torch
- torchvision
```

# List of extensions

```
- jupyter-bokeh
- jupyter-tensorboard
- jupyterlab-git
- jupyterlab-s3-browser
- elyra-python-editor-extension
```

## Importing the PyTorch Notebook

A pre-built version of the pytorch notebook based on [Thoth s2i-minimal-notebook](https://github.com/thoth-station/s2i-minimal-notebook), can be found at quay.io:

[![Docker Repository on Quay](https://quay.io/repository/thoth-station/s2i-pytorch-notebook/status "Docker Repository on Quay")](https://quay.io/repository/thoth-station/s2i-pytorch-notebook)

- <https://quay.io/repository/thoth-station/s2i-pytorch-notebook>

This image could be imported into an OpenShift cluster using OpenShift ImageStream:

```yaml
apiVersion: image.openshift.io/v1
kind: ImageStream
metadata:
  # (Below label is needed for Opendatahub.io/JupyterHub)
  # labels:
  #   opendatahub.io/notebook-image: "true"
  name: s2i-pytorch-notebook
spec:
  lookupPolicy:
    local: true
  tags:
  - name: latest
    from:
      kind: DockerImage
      name: quay.io/thoth-station/s2i-pytorch-notebook:latest
```

## Building the PyTorch Minimal Notebook

Instead of using the pre-built version of the minimal notebook, you can build the minimal notebook from source code.

With [Thoth](https://thoth-station.ninja/) advise

```bash
s2i build . quay.io/thoth-station/s2i-minimal-py38-notebook:latest \
--env ENABLE_PIPENV=1 \
--env THOTH_ADVISE=1 \
--env THOTH_DRY_RUN=0 \
--env THOTH_PROVENANCE_CHECK=1 \
s2i-pytorch-notebook
```

Without [Thoth](https://thoth-station.ninja/) advise

```bash
s2i build . quay.io/thoth-station/s2i-minimal-py38-notebook:latest \
--env ENABLE_PIPENV=1 \
--env THOTH_ADVISE=0 \
--env THOTH_ERROR_FALLBACK=1 \
--env THOTH_DRY_RUN=1 \
--env THOTH_PROVENANCE_CHECK=0 \
s2i-pytorch-notebook
```
