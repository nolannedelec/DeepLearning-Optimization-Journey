# CIFAR-10 CNN : Parcours d'Optimisation et Apprentissage

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-ee4c2c.svg)](https://pytorch.org/)

## 📌 Présentation du Projet
Ce dépôt documente l'évolution d'un modèle de classification d'images (Dataset CIFAR-10) développé avec **PyTorch**. 

> [!IMPORTANT]
> Ce projet est une **démarche pédagogique**. L'objectif n'était pas d'atteindre un score de pointe par simple copie de modèles existants, mais de comprendre l'impact réel de chaque brique technologique (Batch Normalization, Data Augmentation, Dropout) en les implémentant de manière itérative.

## Étapes de l'Optimisation

Le modèle a évolué d'une architecture basique vers une version optimisée incluant :

1. **Architecture CNN Profonde** : Passage à un système de 4 blocs convolutifs (32 et 64 filtres) pour extraire des caractéristiques complexes.
2. **Batch Normalization (BN)** : L'ajout de couches `BatchNorm2d` après chaque convolution a été le point de bascule du projet, stabilisant massivement l'apprentissage.
3. **Optimisation de la Décision (Bottleneck)** : Ajout d'une troisième couche linéaire (passage de 512 à 64 neurones) pour forcer le modèle à synthétiser ses connaissances.
4. **Data Augmentation** : Test de transformations (flips, rotations, jitter) pour améliorer la robustesse globale.
5. **Régularisation (Dropout)** : Implémentation de Dropout (0.3) pour prévenir l'overfitting.

## Analyses et Enseignements Clés

### 1. La Batch Normalization : Le "Game Changer"
C'est l'optimisation la plus marquante. Avant la BN, la convergence était lente et instable. 
- **Impact** : La précision est passée d'environ 55% à **plus de 76%** en seulement 10 époques.
- **Démarrage rapide** : Grâce à la BN, la perte (Loss) démarre beaucoup plus bas (environ 1.6 au lieu du 2.3 théorique du hasard), car le modèle se stabilise et apprend dès les premières itérations de l'époque 0.

### 2. Le dilemme de la couche 64 (512 → 64 → 10)
L'ajout d'une couche de réflexion supplémentaire a montré un transfert de performance intéressant :
- **Succès** : La détection des **Chiens** a bondi (atteignant ~75.8%).
- **Échec** : La détection des **Chats** s'est dégradée (tombant sous les 50%).
- **Analyse** : La réduction à 64 neurones a créé un goulot d'étranglement informatif. Le modèle a privilégié des caractéristiques fortes pour certaines classes au détriment des détails plus subtils nécessaires à la distinction des chats.

### 3. Analyse Critique de la Data Augmentation
Mes tests ont révélé que sur CIFAR-10 (images de $32 \times 32$ pixels) :
- La Data Augmentation **ralentit considérablement** le temps de calcul.
- À cette résolution, les déformations peuvent être "destructrices" et n'apportent pas toujours de gain de précision pure face à un modèle "propre" stabilisé par BN.
- Elle reste cependant indispensable pour la **robustesse** face à des images qui ne seraient pas parfaitement cadrées.

## Résultats Modèle Stabilisé avec BN en 30 époques sans Data Augmentation.
- **Précision moyenne** : ~82.99 %
- **Performances par classe (Exemples)** :
    - 🚢 **Bateau** : 91.4 %
    - 🚛 **Camion** : 85.4 %
    - 🐎 **Cheval** : 88.0 %
    - 🐱 **Chat** : 63.0 % (Meilleur score atteint sans le bottleneck trop étroit)


Le projet est contenu dans le notebook `cifar10.ipynb`. Il inclut un système de **Checkpointing** qui sauvegarde le meilleur modèle rencontré :
---
*Projet réalisé dans le cadre d'une exploration personnelle du traitement d'image classique.*
