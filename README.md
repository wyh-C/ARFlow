# ARFlow

This page gives the commands for training and evaluating the Support Flow model in the PyTorch implementation.

## Environment

The preprocessed BCV four-organ dataset should be available at:

```text
/data/wyh/bcv15_abdomen_4organs/
```

Create the project environment from the repository root if it has not been installed:

```bash
conda env create -f bin/environment.yml
```

## Datasets

We used the following abdominal datasets:

### Abdominal Datasets

- BCV (CT): [available here](https://www.synapse.org/Synapse:syn3193805/wiki/)
- CHAOS (MR): [available here](https://chaos.grand-challenge.org/)
- AMOS (CT & MR): [available here](https://amos22.grand-challenge.org/)
- TotalSegmentator (MRI): [available here](https://zenodo.org/records/14710732)

## Training

Support Flow is trained in two stages. The first command trains the graph and support-flow branch. It produces a graph checkpoint. Set `EXPERIMENTS_WYH_ROOT` to the directory in which the run should be stored.

```bash
python -u bin/training_inference_torch/train_bcv15_abdomen_4organs_torch.py
```

Use the generated graph checkpoint to initialize the second command. This trains the segmentation network together with the relation-guidance branch and produces `ckpt-50000.pt`.

```bash
python -u bin/training_inference_torch/train_bcv15_abdomen_4organs_torch.py
```

The graph cache path can be changed when a different data root or cache is used. The remaining Support Flow defaults are loaded by the training configuration.

