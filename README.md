# PCB Defect Detection — YOLOv8

Détection automatique de défauts sur cartes de circuits imprimés (PCB) par deep learning,
réalisé dans le cadre du cours **Deep Learning for Computer Vision 2025/2026**.

**Auteurs :** Riad SAHRANE · Abdourahmane TIMERA

---

## Résultats

| Métrique | Valeur |
|---|---|
| Precision | **0.971** |
| Recall | **0.954** |
| mAP@0.5 | **0.985** |
| mAP@0.5:0.95 | **0.777** |

---

## Classes détectées

| ID | Classe | Description |
|---|---|---|
| 0 | `open` | Connexion interrompue |
| 1 | `short` | Court-circuit |
| 2 | `mousebite` | Entaille en demi-lune |
| 3 | `spur` | Excroissance de cuivre |
| 4 | `copper` | Résidu de cuivre |
| 5 | `pine_hole` | Trou de perçage anormal |

---

## Structure du dépôt
```
PCB-Defect-Detection-YOLOv8/
├── notebooks/
│   ├── 01_training_yolov8_pcb.ipynb       # Préparation + entraînement
│   └── 02_evaluation_yolov8_pcb.ipynb     # Évaluation + analyse des erreurs
├── report/
│   ├── rapport_pcb.pdf                    # Rapport final
│   └── rapport_pcb.tex                    # Source LaTeX
├── images/                                # Figures générées
│   ├── training_curves.png
│   ├── results_par_classe.png
│   ├── confusion_matrix_test.png
│   ├── courbes_performance.png
│   ├── gt_vs_pred.png
│   ├── error_analysis.png
│   └── confidence_threshold.png
└── README.md
```

---

## Structure du dataset (Google Drive)

Le dataset est stocké sur Google Drive (non inclus dans ce dépôt — taille > 500 Mo).
```
MyDrive/COMPUTER VISION/dataset/
├── img/                          # 1 500 images brutes (640×640, .jpg)
├── annotation/                   # Annotations originales format xyxycls
├── labels_yolo/                  # Labels convertis format YOLO normalisé
├── pcb.yaml                      # Fichier de configuration YOLOv8
├── yolo_dataset/
│   ├── images/
│   │   ├── train/                # 1 050 images (70%)
│   │   ├── val/                  # 225 images (15%)
│   │   └── test/                 # 225 images (15%)
│   └── labels/
│       ├── train/
│       ├── val/
│       └── test/
├── training_outputs_run1/        # Résultats entraînement principal
│   ├── weights/
│   │   ├── best.pt               # Meilleur modèle
│   │   └── last.pt
│   ├── results.csv
│   ├── BoxPR_curve.png
│   ├── BoxF1_curve.png
│   ├── confusion_matrix.png
│   └── confusion_matrix_normalized.png
└── evaluation_outputs_test/      # Figures générées par le notebook 2
    ├── gt_vs_pred.png
    ├── error_analysis.png
    └── confidence_threshold.png
```

---

## Reproduire les expériences

### Prérequis
```bash
pip install ultralytics opencv-python matplotlib pandas
```

### 1. Monter le Drive et configurer les chemins
```python
BASE = Path("/content/drive/MyDrive/COMPUTER VISION/dataset")
BEST_MODEL = BASE / "training_outputs_run1/weights/best.pt"
YAML_PATH  = BASE / "pcb.yaml"
```

### 2. Lancer les notebooks dans l'ordre

1. `01_training_yolov8_pcb.ipynb` — préparation du dataset + entraînement (GPU recommandé)
2. `02_evaluation_yolov8_pcb.ipynb` — évaluation complète sur le jeu de test

> Les notebooks sont conçus pour Google Colab avec GPU Tesla T4.
> Sur CPU uniquement, l'entraînement n'est pas recommandé mais l'évaluation fonctionne.

---

## Environnement

- Python 3.12
- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics) 8.4.19
- PyTorch 2.10.0
- Google Colab (GPU Tesla T4 pour l'entraînement)

---

## Références

- Jocher, G. et al. (2023). *Ultralytics YOLOv8*. https://github.com/ultralytics/ultralytics
- Ding, R. et al. (2019). *TDD-Net: A Tiny Defect Detection Network for PCB*. IEEE Access.
- Redmon, J. & Farhadi, A. (2018). *YOLOv3: An Incremental Improvement*. arXiv:1804.02767.
