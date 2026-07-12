# MNE: N170 EEG Analysis

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![MNE-Python](https://img.shields.io/badge/MNE--Python-EEG%20Analysis-purple)

A Jupyter Notebook project for preprocessing and analyzing electroencephalography (EEG) data with [MNE-Python](https://mne.tools/stable/) and [HU Neuro Pipeline](https://hu-neuro-pipeline.readthedocs.io/).

This project applies an EEG-processing workflow to the **N170 experiment from the ERP CORE dataset**. It compares neural responses to face and car stimuli and extracts the N170 event-related potential around the PO8 electrode.

## Project Overview

The notebook demonstrates an end-to-end EEG analysis workflow, including:

- Loading EEGLAB `.set` EEG recordings
- Loading event information from `.tsv` files
- Applying a BioSemi 64-channel montage
- Re-referencing EEG channels to the average reference
- Filtering the signal between 0.1 and 40 Hz
- Detecting and removing artifacts with ICA
- Creating stimulus-locked epochs
- Applying baseline correction
- Rejecting high-amplitude epochs
- Calculating face and car condition averages
- Extracting the N170 component
- Exporting trial-level and averaged results

## Analysis Configuration

The included example analysis uses the following settings:

| Parameter | Value |
|---|---|
| Dataset | ERP CORE N170 |
| Example participant | `sub-004` |
| EEG montage | BioSemi 64 |
| Reference | Average reference |
| High-pass filter | 0.1 Hz |
| Low-pass filter | 40 Hz |
| ICA method | FastICA |
| ICA components | 15 |
| Epoch start | −0.5 seconds |
| Epoch end | 1.5 seconds |
| Baseline | −0.2 to 0 seconds |
| Rejection threshold | 200 µV |
| N170 time window | 110–150 ms |
| N170 electrode | PO8 |
| Conditions | Face and car |

The condition definitions used by the example configuration are:

- **Face:** event values from 1 to 40
- **Car:** event values from 41 to 80

## Repository Structure

```text
MNE/
├── main.ipynb
├── requirements.txt
├── README.md
└── output/
    ├── ave.csv
    ├── channel_locations.csv
    ├── config.json
    ├── grand_ave.csv
    └── trials.csv
```

### Main files

- `main.ipynb` — Main EEG preprocessing and analysis notebook.
- `requirements.txt` — Python packages required to run the notebook.
- `output/config.json` — Analysis parameters, package versions, rejected epochs, and rejected ICA components.
- `output/trials.csv` — Trial-level EEG measurements and metadata.
- `output/ave.csv` — Participant-level condition averages.
- `output/grand_ave.csv` — Grand-average results.
- `output/channel_locations.csv` — EEG channel coordinates.

## Installation

Clone the repository:

```bash
git clone https://github.com/arq7arq/MNE.git
cd MNE
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Linux or macOS:

```bash
source .venv/bin/activate
```

Activate it on Windows:

```powershell
.venv\Scripts\activate
```

Install the dependencies:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## Dependencies

The project uses the following main packages:

- NumPy
- pandas
- MNE-Python
- Matplotlib
- Seaborn
- Jupyter Notebook
- IPython kernel
- HU Neuro Pipeline

The exact dependency list is available in `requirements.txt`.

## Dataset

This project uses data from the [ERP CORE](https://erpinfo.org/erp-core) project, an open resource containing EEG data and analysis materials for several commonly studied event-related potential components.

The dataset itself is **not included** in this repository.

Download the N170 data and place it in a local data directory. The notebook expects:

- An EEGLAB EEG recording in `.set` format
- A corresponding events file in `.tsv` format

Example:

```text
data/
└── erpcore/
    └── N170/
        └── sub-004/
            └── eeg/
                ├── sub-004_task-N170_eeg.set
                └── sub-004_task-N170_events.tsv
```

## Running the Analysis

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open `main.ipynb` and complete the following steps:

1. Update the EEG and event file paths to match their locations on your computer.
2. Review the preprocessing and epoching parameters.
3. Select or create an output directory.
4. Run the notebook cells from top to bottom.
5. Inspect the generated visualizations and exported files.

> [!IMPORTANT]
> The example configuration contains absolute paths from the original development environment. Replace these paths with valid paths on your own computer before running the notebook.

## Output

After a successful run, the analysis exports several files to the `output` directory.

### `trials.csv`

Contains trial-level data, experimental conditions, and extracted EEG measurements.

### `ave.csv`

Contains participant-level averaged ERP results for the face and car conditions.

### `grand_ave.csv`

Contains grand-average ERP results that can be used when analyzing multiple participants.

### `channel_locations.csv`

Contains channel names and electrode-position information.

### `config.json`

Records the analysis configuration, software versions, automatically rejected epochs, and ICA components marked for removal. This file helps document and reproduce the preprocessing workflow.

## Notes

- The committed outputs are example results and may change when the analysis is run with another participant or configuration.
- EEG preprocessing choices should be reviewed for the requirements of each experiment.
- This repository is intended for education, experimentation, and reproducible EEG-analysis practice.
- The project is not intended for clinical diagnosis or medical decision-making.

## Attribution

This project was developed using the following repository as a learning resource and foundation:

**Introduction to EEG Analysis** by Alex Enge  
https://github.com/alexenge/intro-to-eeg

The original project provides introductory EEG-analysis course material using Python and MNE-Python.

This repository is an independent adaptation. Changes include project-specific notebook organization, configuration for ERP CORE N170 data, local data handling, and generated CSV and JSON outputs.




## Acknowledgements

- [Alex Enge](https://github.com/alexenge) for the original Introduction to EEG Analysis course
- The [MNE-Python](https://mne.tools/stable/) contributors
- The [HU Neuro Pipeline](https://hu-neuro-pipeline.readthedocs.io/) contributors
- The researchers and contributors behind the [ERP CORE](https://erpinfo.org/erp-core) dataset