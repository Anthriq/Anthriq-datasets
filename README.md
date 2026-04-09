# Multimodal Dataset

This dataset contains EEG and EMG recordings organized according to the [Brain Imaging Data Structure (BIDS)](https://bids.neuroimaging.io/) specification for EEG data.

## Experiment Overview

This dataset includes three experimental conditions:

- **Eye Closure** — Resting state with eyes closed
- **SSVEP** — Steady-State Visual Evoked Potentials
- **EMG Gestures** — Electromyography during gesture tasks

## Dataset Structure

```text
dataset/
│
├── dataset_description.json
├── participants.tsv
├── participants.json
│
├── sub-001/
│   └── eeg/
│       ├── sub-001_task-eyesclosure_eeg.edf
│       ├── sub-001_task-eyesclosure_eeg.json
│       ├── sub-001_task-eyesclosure_channels.tsv
│       ├── sub-001_task-eyesclosure_events.tsv
│       ├── sub-001_task-ssvep_eeg.edf
│       ├── sub-001_task-ssvep_eeg.json
│       ├── sub-001_task-ssvep_channels.tsv
│       ├── sub-001_task-ssvep_events.tsv
│       ├── sub-001_task-emggestures_eeg.edf
│       ├── sub-001_task-emggestures_eeg.json
│       ├── sub-001_task-emggestures_channels.tsv
│       └── sub-001_task-emggestures_events.tsv
│
├── sub-002/
│   └── eeg/
│       └── ...
│
└── derivatives/
    └── preprocessed/
        ├── dataset_description.json
        └── sub-001/
            └── eeg/
                ├── sub-001_task-ssvep_desc-preproc_eeg.csv
                └── sub-001_task-ssvep_desc-preproc_eeg.json
```

## File Descriptions

### Root Level

| File | Description |
|------|-------------|
| `dataset_description.json` | Dataset name, authors, license, and references |
| `participants.tsv` | Subject demographics (age, gender, medical conditions) |
| `participants.json` | Description of columns in participants.tsv |

### Subject Level (`sub-XXX/eeg/`)

| File | Description |
|------|-------------|
| `*_eeg.edf` | Raw EEG data in European Data Format |
| `*_eeg.json` | Recording metadata (sampling frequency, electrode type, channel count) |
| `*_channels.tsv` | Channel names, types, and units |
| `*_events.tsv` | Event markers with onset times and descriptions |

### Derivatives (`derivatives/preprocessed/`)

Contains preprocessed data with accompanying JSON files documenting:

- Filters applied (type, cutoff frequencies)
- Artifact rejection methods
- Epoching parameters
- Reference scheme

## Equipment

| Parameter | Value |
|-----------|-------|
| Electrode Type | [Dry / Wet] |
| Number of Channels | [N] |
| Sampling Frequency | [X] Hz |
| Reference | [Reference scheme] |

## Participants

| Participant | Age | Gender | Notes |
|-------------|-----|--------|-------|
| sub-001 | -- | -- | -- |
| sub-002 | -- | -- | -- |

See `participants.tsv` for complete demographics.

## Preprocessing Pipeline

The preprocessed data in `derivatives/` was generated using the following steps:

1. **Filtering** — [e.g., Bandpass 0.5–45 Hz, Notch 50 Hz]
2. **Artifact Rejection** — [e.g., ICA for eye blinks, threshold-based rejection]
3. **Re-referencing** — [e.g., Common average reference]
4. **Epoching** — [e.g., -200 ms to 800 ms relative to stimulus onset]

## How to Use

### Loading with MNE-Python

```python
import mne_bids

bids_path = mne_bids.BIDSPath(
    subject='001',
    task='ssvep',
    datatype='eeg',
    root='path/to/dataset'
)

raw = mne_bids.read_raw_bids(bids_path)
```

### Loading with EEGLAB

```matlab
% Requires EEGLAB with bids-matlab-tools plugin
[STUDY, ALLEEG] = pop_importbids('path/to/dataset');
```

## Citation

If you use this dataset, please cite:

> Anthriq datasets (2026). https://github.com/Anthriq/Anthriq-datasets

## License

CC BY 4.0 (Creative Commons Attribution 4.0 International)


## Contact

For questions about this dataset, please contact:

- collaboration@anthriq.com

## References

- [BIDS-EEG Specification](https://bids-specification.readthedocs.io/en/stable/04-modality-specific-files/03-electroencephalography.html)
- [MNE-BIDS Documentation](https://mne.tools/mne-bids/)
