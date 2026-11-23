# VoiceGuard: Detecting Cloned Voices in Phone Calls

GenAI course project · Eyal Raveh

**Status:** project proposal stage.

## The problem

Voice cloning lets a scammer sound like someone you trust. A small-business owner can get a call in a known supplier's voice asking to send a payment to a new bank account. Banks use voice biometrics, and those have already been bypassed with AI clones. Small businesses usually rely on recognising the voice by ear.

## The project

VoiceGuard is a research prototype that analyses recorded calls to a small business and decides whether the caller is who they claim to be. It combines:

1. **Synthetic-speech detection:** is the voice real or generated?
2. **Speaker verification:** does the voice match the enrolled person?
3. **Knowledge questions** from the business's own records

The scores are fused into a calibrated risk score and an action: allow, verify or hold.

The focus is evaluation under phone conditions (8 kHz, codecs, noise) and in a low-resource language, Hebrew, alongside English and Spanish.

## Planned methods

| Component | Model |
| --- | --- |
| Detection baseline | CNN on log-mel spectrograms |
| Deepfake detector | XLS-R + classification head; AASIST zero-shot for comparison |
| Speaker verification | ECAPA-TDNN (pretrained) |
| Fusion | Average (baseline), then logistic regression |
| Content check (stretch goal) | Whisper + LLM |

## Evaluation

- Real vs. synthetic: EER, minDCF, ROC-AUC, PR-AUC
- Call type (genuine, clone, impostor, replay): macro-F1, MCC, confusion matrix
- System: FAR / FRR, recall at FAR ≤ 1%, calibration
- Speaker-disjoint splits, one held-out generator, Hebrew as an unseen language

## Repository structure

| Folder | Contents |
| --- | --- |
| `Slides/` | Presentations in PPT and PDF format |
| `Code/` | Python files and notebooks |
| `Data/` | Audio/text samples, JSON and CSV metadata |
| `Results/` | CSV/JSON results of experiments |
| `Visuals/` | Result figures and visual abstract |

## Timeline

| Weeks | Phase |
| --- | --- |
| 1–2 | Feasibility: data, licences, pretrained models |
| 3–4 | Data generation and quality control |
| 5–6 | Deepfake detection |
| 7 | Speaker verification and fusion |
| 8 | Evaluation |
| 9 | Stretch goals |
| 10 | Report and final presentation |
