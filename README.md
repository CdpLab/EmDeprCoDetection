#  <p align="center">Multimodal Emotion and Depression Co-detection Method Based on Source-Free Domain Adaptation and Task Specialization</p>

 <p align="center">Jia Liu, Yiyang Wang, Tianshuo Fu, Yangrui Zhang, and Dapeng Chen*</p>
  <p align="center">Nanjing University of Information Science & Technology</p>

---
## <p align="center">ABSTRACT</p>
Recognizing emotional states and detecting depression play a critical role in psychiatric healthcare. However, current methodologies are frequently hindered by limited data availability, high inter-subject variance, and inadequate integration of diverse modalities. Furthermore, prior research lacks a cohesive architecture capable of seamlessly linking these dual objectives. To overcome these limitations, this study introduces a novel cooperative detection network for multimodal emotion and depression, driven by task specialization and Source-Free Domain Adaptation (SFDA). A key advantage of this architecture is its capacity to conduct concurrent modeling and cross-individual generalization for both tasks, entirely independent of source domain datasets.Methodologically, our approach relies on acoustic features and electroencephalogram (EEG) signals as the core inputs, supplemented by textual data integration. By applying a Contrastive EEG-Audio-Text Learning (CEAT) mechanism, the heterogeneous data streams are projected into a common feature dimension, thereby facilitating semantic alignment across modalities. Moreover, we incorporate a tailored SFDA protocol. Utilizing a blend of a freeze-thaw mechanism, knowledge distillation, and most-likely category encouragement, this approach significantly minimizes inter-subject distribution variations within unannotated target domains while boosting the synergistic optimization potential between the two tasks.Performance evaluations reveal that our model attains a 93.17% precision rate on the MODMA benchmark for depression screening. For cross-subject emotion classification, it registers accuracies of 87.79% and 62.11% on the SEED and SEED-IV databases, respectively. These empirical findings robustly substantiate the efficacy of the presented framework in jointly handling multimodal affective and depressive analysis.

## <p align="center">Method Overview</p>
![Architecture](assets/图1.jpg)

Feature Extractors
![Architecture](assets/图2.jpg)

Task-specific SFDA
![Architecture](assets/图3.jpg)



# CEAT + SFDA  Skeleton

This repo provides a runnable skeleton for:
- Multimodal encoders (EEG/Audio/Text)
- CEAT-style contrastive alignment (E-A, E-T, A-T)
- Source training (supervised)
- Target SFDA adaptation 
- Evaluation

## Quick start
```bash
pip install -r requirements.txt


python scripts/_debug_data.py

python scripts/_debug_model.py

python scripts/train_source.py --data_cfg configs/seed.yaml --model_cfg configs/model.yaml

python scripts/adapt_target_sfda.py --data_cfg configs/seed.yaml --model_cfg configs/model.yaml --sfda_cfg configs/sfda.yaml \
  --source_ckpt runs/seed_emotion/source_best.pt

python scripts/evaluate.py --data_cfg configs/seed.yaml --model_cfg configs/model.yaml --ckpt runs/seed_emotion/source_best.pt
