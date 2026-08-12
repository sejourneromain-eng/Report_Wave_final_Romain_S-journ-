# Report Wave Final - Romain S. Journé

Projet de détection et d’analyse de vagues à partir de vidéos, avec utilisation de YOLOv8 pour l’identification d’objets dans les images et le calcul d’un risque lié à la dynamique des vagues.

## Objectif

Ce dépôt contient des scripts pour :

- télécharger une vidéo YouTube,
- extraire des images clés (frames) depuis une vidéo,
- préparer un dataset sur Google Drive,
- entraîner un modèle YOLOv8,
- visualiser et analyser les résultats de détection.

Le projet est orienté vers une application de surveillance de vagues et d’évaluation de risque sur des séquences vidéo.

---

## Structure du dépôt

- [Code to create frame of a video youtube.md](Code%20to%20create%20frame%20of%20a%20video%20youtube.md) : script pour télécharger une vidéo YouTube et extraire des images.
- [code to create frame of a video in a drive](code%20to%20create%20frame%20of%20a%20video%20in%20a%20drive) : script pour découper une vidéo déjà présente sur Google Drive et sauvegarder les frames.
- [Code to see the training](Code%20to%20see%20the%20training) : script pour visualiser et inspecter le training / les résultats du modèle.
- [Code to train the YOLOv8 AI](Code%20to%20train%20the%20YOLOv8%20AI) : script principal pour l’entraînement YOLOv8.
- [take data on Copernicus](take%20data%20on%20Copernicus) : fichier de collecte ou de préparation de données environnementales.

---

## Pipeline général

1. Récupérer des vidéos depuis YouTube ou depuis Google Drive.
2. Extraire des frames à intervalle régulier.
3. Préparer le dataset pour l’entraînement.
4. Entraîner un modèle YOLOv8.
5. Réaliser la détection des vagues sur de nouvelles vidéos.
6. Calculer une estimation de risque ou de danger selon les paramètres de détection.

---

## Script 1 : création de frames depuis YouTube

Le script dans [Code to create frame of a video youtube.md](Code%20to%20create%20frame%20of%20a%20video%20youtube.md) permet :

- de télécharger une vidéo YouTube via `yt-dlp`,
- de l’enregistrer dans Google Drive,
- de découper la vidéo en images à intervalle défini,
- de sauvegarder les images dans un dossier dataset dédié.

### Variables principales

- `URL_YOUTUBE` : URL de la vidéo
- `DRIVE_PROJECT_FOLDER` : dossier Google Drive du projet
- `DESTINATION_IMAGES_FOLDER` : dossier où seront enregistrées les images
- `FRAME_INTERVAL` : nombre de frames entre deux extractions

---

## Script 2 : extraction depuis un fichier Google Drive

Le script [code to create frame of a video in a drive](code%20to%20create%20frame%20of%20a%20video%20in%20a%20drive) permet de :

- connecter Google Drive,
- lire une vidéo stockée dans Drive,
- sauvegarder des images selon un intervalle fixe,
- créer automatiquement les dossiers manquants.

---

## Script 3 : entraînement YOLOv8

Le script [Code to train the YOLOv8 AI](Code%20to%20train%20the%20YOLOv8%20AI) montre l’approche pour :

- installer Ultralytics,
- monter Google Drive,
- charger un modèle pré-entraîné `yolov8c.pt`,
- lancer l’entraînement sur un dataset YAML spécifique,
- sauvegarder les résultats et poids du modèle dans Drive.

Exemple de commande utilisée :

```bash
!yolo train \
  model=yolov8c.pt \
  data=/content/drive/MyDrive/Project_Yolo_v9/Waveproject.yaml \
  project=/content/drive/MyDrive/Wave/Project \
  name=train \
  epochs=75 \
  batch=10 \
  imgsz=640 \
  save=True
```

---

## Script 4 : visualisation du training

Le fichier [Code to see the training](Code%20to%20see%20the%20training) montre les étapes liées à :

- montage du Drive,
- chargement du modèle,
- détection sur des vidéos,
- ajout de boîtes autour des objets détectés,
- affichage d’un statut global de risque.

Il combine l’utilisation de OpenCV et de YOLO pour obtenir une sortie annotée de vidéos.

---

## Dépendances recommandées

- Python 3.9+
- OpenCV (`cv2`)
- `yt-dlp`
- `ultralytics`
- Google Colab (si utilisé tel quel)
- Google Drive pour le stockage des données

Installation rapide :

```bash
pip install yt-dlp
pip install ultralytics
pip install opencv-python
```

---

## Exemple d’utilisation

1. Ouvrir un notebook Google Colab.
2. Monter Google Drive.
3. Télécharger ou préparer les frames.
4. Ajouter le dataset dans le bon dossier.
5. Lancer le script d’entraînement YOLOv8.
6. Utiliser le modèle sur une vidéo pour détecter les vagues.
7. Vérifier les résultats annotés et le statut de risque.

---

## Remarques

- Ce projet est encore en développement et reste fortement orienté vers le prototypage.
- Les chemins d’accès Google Drive doivent être adaptés selon l’arborescence réelle de votre compte.
- Les paramètres d’entraînement, de calibration et de risque sont à ajuster selon les données réelles.

---

## Auteur

Romain S. Journé

## Licence

Ce repository est partagé à des fins de projet et de démonstration. Si vous souhaitez l’utiliser ou le modifier, merci de citer la source originale.
