# Guide des Techniques NLP : De la Fréquence au Sens

Ce guide définit les quatre piliers fondamentaux du traitement du langage naturel (NLP). Pour chaque concept, nous explorons son rôle, sa justification (**Pourquoi**), son fonctionnement interne (**Comment**) et ses cas d'usage réels (**Où**).

---

## 1. Bag of Words (BoW) - Le Sac de Mots
**"Le Compteur Simple"**

### 🎯 Rôle
C'est la technique la plus ancienne et la plus simple. Elle transforme un texte en un vecteur de nombres en comptant simplement la fréquence d'apparition de chaque mot, sans se soucier de l'ordre ou de la grammaire.

### ❓ Pourquoi l'utiliser ?
* **Simplicité extrême :** Très facile à comprendre et à implémenter.
* **Rapidité :** Nécessite peu de puissance de calcul.
* **Efficacité sur des tâches simples :** Parfait si la présence d'un mot spécifique (ex: "gagnant", "gratuit") suffit à classer le texte.

### ⚙️ Comment ça marche ?
1.  **Vocabulaire :** On liste tous les mots uniques de tout le corpus (ex: 10 000 mots).
2.  **Vectorisation :** Pour chaque phrase, on crée un vecteur de la taille du vocabulaire.
3.  **Comptage :** Si le mot "chat" est le 3ème mot du vocabulaire et apparaît 2 fois dans la phrase, la 3ème position du vecteur prend la valeur `2`. Ailleurs, c'est `0`.

### 📍 Où l'utiliser ?
* **Filtrage de Spam :** Détecter des mots clés suspects.
* **Classification de documents simple :** Classer des articles par thèmes (Sport, Politique) basés sur des mots clés évidents.

---

## 2. TF-IDF (Term Frequency - Inverse Document Frequency)
**"Le Spécialiste"**

### 🎯 Rôle
Une amélioration du BoW. Au lieu de compter bêtement, TF-IDF donne du poids aux mots **importants** et pénalise les mots trop courants (comme "le", "de", "est") qui n'apportent pas d'information.

### ❓ Pourquoi l'utiliser ?
* **Filtrage du bruit :** Dans BoW, le mot "le" apparaît 100 fois et semble important. TF-IDF réduit son score à près de zéro.
* **Mise en valeur de la rareté :** Un mot rare qui apparaît dans un document spécifique devient la "signature" de ce document.

### ⚙️ Comment ça marche ?
C'est une multiplication de deux scores :
1.  **TF (Fréquence du terme) :** Combien de fois le mot apparaît dans *ce* document (comme BoW).
2.  **IDF (Fréquence inverse de document) :** Un calcul logarithmique qui diminue le score si le mot apparaît dans *beaucoup* de documents du corpus.

### 📍 Où l'utiliser ?
* **Moteurs de recherche (classiques) :** Pour trouver le document le plus pertinent pour une requête utilisateur.
* **Extraction de mots-clés :** Résumer automatiquement le sujet d'un texte.
* **Systèmes de recommandation basiques :** "Vous avez aimé cet article sur le 'Jardinage', voici un autre article avec un score TF-IDF élevé sur 'Jardinage'."

---

## 3. Word2Vec (Word Embeddings)
**"Le Sémantique Statique"**

### 🎯 Rôle
Word2Vec abandonne le comptage pour l'apprentissage. Il transforme chaque mot en un **vecteur dense** (une liste de coordonnées, ex: `[0.2, -0.5, 0.9]`) dans un espace géométrique. Les mots ayant un sens proche sont géographiquement proches.

### ❓ Pourquoi l'utiliser ?
* **Capture du sens (Sémantique) :** Contrairement à BoW/TF-IDF, il comprend que "Roi" et "Reine" sont liés.
* **Analogies mathématiques :** On peut faire des calculs sur les mots : `Vecteur(Roi) - Vecteur(Homme) + Vecteur(Femme) ≈ Vecteur(Reine)`.
* **Réduction de dimension :** On passe de vecteurs immenses et vides (taille 100 000 avec plein de zéros) à des vecteurs compacts et pleins (taille 300).

### ⚙️ Comment ça marche ?
Un réseau de neurones est entraîné sur des milliards de phrases pour prédire un mot en fonction de ses voisins (contexte).
* Si "chat" et "chien" apparaissent souvent entourés des mêmes mots ("manger", "dormir", "animal"), le réseau apprend à leur donner des coordonnées similaires.
* **Note :** C'est un embedding *statique*. Le mot "avocat" aura le même vecteur, qu'on parle du fruit ou du métier.

### 📍 Où l'utiliser ?
*