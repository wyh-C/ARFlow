# ARFlow

This page gives the commands for training and evaluating the Support Flow model in the PyTorch implementation.

## Environment

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

Run graph Flow pretraining:

```bash
python train_support_flow.py \
  --stage graph \
  --data-root <data-root> \
  --output-root <output-root>
```

Then initialize segmentation training from the generated graph checkpoint:

```bash
python train_support_flow.py \
  --stage segmentation \
  --data-root <data-root> \
  --output-root <output-root> \
  --checkpoint <path-to-ckpt-5000.pt>
```

The graph stage defaults to 5,000 iterations and the segmentation stage to 50,000 iterations. Checkpoints are saved below the specified output root.
```

The graph cache path can be changed when a different data root or cache is used. The remaining Support Flow defaults are loaded by the training configuration.

