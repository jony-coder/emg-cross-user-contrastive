# Related work

Short reading list for this project. Each entry: what the paper does, and how it relates to this notebook.

## 1. Do sEMG Foundation Models Improve Cross-Subject Generalisation? (read first)
**W. Raftery, D. Farina** (Imperial College London), arXiv 2611.08199, Nov 2026. https://arxiv.org/abs/2611.08199

Evaluates three pretrained sEMG foundation models (TinyMyo, PhysioWave, NeuroRVQ) on NinaPro DB5, EPN-612 and **UCI EMG Gestures** (the dataset used here), under intra-session and inter-subject splits, comparing full fine-tuning, training from scratch and linear probing. Pretraining helps within a session, but on inter-subject splits the benefit largely disappears: on UCI-EMG, Random Forest and SVM on classical Hudgins features reach about 89%, versus about 84% for the best foundation model with full fine-tuning. They recommend always reporting inter-subject results and a from-scratch baseline.

**Relation to this project:** same dataset and same question. My quick run also found that pretraining did not automatically help on unseen users. Their result suggests adding a classical feature baseline (RF/SVM on Hudgins features) as a next step.

## 2. EMG-UP: Unsupervised Personalization in Cross-User EMG Gesture Recognition
**N. Wang, G. Li, Z. Fan, S. Wang**, arXiv 2509.21589, 2025. https://arxiv.org/abs/2509.21589

Adapts a pretrained model to each new user using only that user's **unlabeled** data, in two stages: (1) contrastive learning between each EMG sequence and its time-reversed view, (2) fine-tuning on high-confidence pseudo-labels from a teacher model. Evaluated on emg2pose (193 users) and a private dataset; reports gains of about 2–3% over strong domain-adaptation baselines.

**Relation:** the closest published version of my `contrastive+target` setting (using unlabeled data from new users). EMG-UP adds pseudo-labelling, which I did not try.

## 3. CPEP: Contrastive Pose-EMG Pre-training Enhances Gesture Generalization on EMG Signals
**W. Cui, C. Sandino, H. Pouransar** (Apple / USC), arXiv 2509.04699, 2025 (workshop: Foundation Models for the Brain and Body). https://arxiv.org/abs/2509.04699

Pretrains an EMG encoder with self-supervised learning and aligns it contrastively with hand-pose representations. Reports that purely supervised EMG-to-pose models generalize poorly to unseen gestures or users.

**Relation:** shows that a second modality (pose / vision) can guide EMG representations, which is the direction of combining EMG with egocentric vision.

## 4. Tackling Electrode Shift in Gesture Recognition with HD-EMG Electrode Subsets
**J. Pereira, D. Chalatsis, B. Hodossy, D. Farina** (Imperial College London), IEEE, 2024; arXiv 2401.02773. https://arxiv.org/abs/2401.02773

Treats electrode shift as an input transformation and trains on subsets of high-density EMG channels to learn shift-invariant mappings, improving inter-session performance across subjects and classifiers.

**Relation:** the published basis for my "armband rotation" augmentation, done more carefully on high-density electrode grids.

## 5. Conservative Subject Invariant EMG-based Gesture Recognition (CSIN)
arXiv 2607.03783, 2026. https://arxiv.org/abs/2607.03783

Combines gesture classification, adversarial subject confusion and triplet metric learning on a shared encoder. Argues cross-subject generalisation is hard because the signals that identify a person and those that identify a gesture are not cleanly separable, and leaves open whether this entanglement is fundamental.

**Relation:** a different strategy (explicitly removing subject identity) for the same gap; its open question is a possible PhD-level direction.

## 6. Classic: transfer learning for EMG with CNNs
**U. Côté-Allard et al.**, "Deep Learning for Electromyographic Hand Gesture Signal Classification Using Transfer Learning", IEEE TNSRE, 2019.

Early, widely cited work showing that knowledge learned from many users helps a CNN adapt to a new user with little data.

**Relation:** background for the whole cross-user problem; useful to cite as the starting point.
