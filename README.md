# Evolution d'un modèle CNN sur CIFAR-10 : Apprentissage et Optimisation

## 📌 À propos de ce projet
Ce dépôt regroupe les différentes étapes de création et d'optimisation d'un réseau de neurones convolutif (CNN) pour la classification d'images (Dataset CIFAR-10).

> **Avertissement important** : Le code contenu dans ce projet n'a pas pour objectif d'être une solution "clés en main" ou parfaitement optimisée pour la production. Ce travail a été réalisé dans un but **purement pédagogique**. L'objectif était d'apprendre à identifier les limites d'un modèle simple et d'implémenter itérativement des techniques d'optimisation pour comprendre leur impact réel.

## Le Parcours d'Optimisation
Plutôt que de viser 95% de précision immédiatement, j'ai choisi de partir d'une architecture basique pour explorer les concepts suivants :

1. **Modèle de base** : Compréhension des couches de convolution et de pooling.
2. **Architecture Profonde** : Ajout de filtres (32, 64) et gestion de la perte d'information avec le `padding`.
3. **Data Augmentation** : Lutte contre l'overfitting en "torturant" les données (rotations, flips, variations de lumière).
4. **Stabilité avec la Batch Normalization** : Accélération de la convergence et stabilisation des gradients.
5. **Régularisation avec le Dropout** : Amélioration de la capacité de généralisation du modèle.

## Résultats obtenus
Le passage d'un modèle simple à un modèle stabilisé par **Batch Normalization** a permis de passer d'environ **55%** à plus de **76%** de précision moyenne sur le set de test, avec des percées significatives sur des classes complexes comme le "Chat" ou l'"Oiseau".

## Technologies utilisées
* Python
* PyTorch / Torchvision
* Matplotlib / Seaborn (Visualisation des pertes et matrices de confusion)
