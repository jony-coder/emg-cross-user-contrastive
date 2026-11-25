# Cross-user sEMG gesture recognition with contrastive pretraining

Short self-directed study: how much does gesture-recognition accuracy drop on **unseen users**, and does EMG-specific contrastive pretraining (electrode gain, armband rotation, channel dropout, noise, time shift) close the gap? Includes Integrated Gradients attributions with completeness and deletion-test faithfulness checks.

**Data:** UCI *EMG Data for Gestures* (Myo armband, 8 channels, 36 subjects). Downloaded automatically by the notebook.

## Results
_To be filled in after the full run._

## Run it
```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```
Then open `notebooks/emg_cross_user_study.ipynb` in VS Code, pick the `.venv` kernel, and Run All.
Set `QUICK=True` in section 1 for a fast smoke test.

## Author
Jahid Hasan Jony · MSc Communications Engineering and Data Science (Erasmus Mundus CODAS)
