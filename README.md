# ⭐ Analyse d'avis d'assurance : NLP & Deep Learning

**Écrivez un avis, l'IA devine la note, comprend de quoi vous parlez… et répond à vos questions.**

Un projet à la croisée du **Traitement du Langage Naturel (NLP)** et du **Deep Learning** : un réseau de neurones entraîné from scratch, associé à des modèles de langage pré-entraînés, transforme des avis clients d'assurance, en **français comme en anglais**, en informations exploitables, le tout dans une application web interactive. 💬

---

## ✨ Ce que fait l'application

Vous choisissez un assureur, un produit, vous écrivez votre avis, et l'application vous donne :

- ⭐ **La note prédite** (de 1 à 5 étoiles) par un réseau de neurones **LSTM**
- 🏷️ **La catégorie principale** de l'avis : prix, couverture, service client, réclamations, annulation…
- 📝 **Une explication** de la note générée par IA
- 🔎 **Des avis similaires** retrouvés dans la base de données
- 💡 **Un espace questions-réponses** pour interroger l'avis directement
- 🌍 **Une détection automatique de la langue** (FR/EN)

## 🧪 Comment ça marche

Le projet se déroule en trois étapes :

1. **Explorer** : nettoyage des textes, analyse des mots et expressions les plus fréquents par note, notes moyennes par assureur et par produit, et visualisation des mots proches avec Word2Vec (t-SNE et TensorBoard).
2. **Prédire** : un modèle de **Deep Learning** (LSTM multi-entrées) qui combine le texte de l'avis, l'assureur, le produit et la langue pour prédire la note.
3. **Déployer** : une application **Streamlit** qui rassemble plusieurs modèles de langage pré-entraînés.

| Fonction | Modèle utilisé |
|---|---|
| Prédiction de la note | LSTM (Keras / TensorFlow) |
| Classification de la catégorie | `facebook/bart-large-mnli` |
| Explication de la note | `facebook/bart-large-cnn` |
| Avis similaires | `all-MiniLM-L6-v2` (Sentence-Transformers) |
| Questions-réponses | `google/flan-t5-large` |

## 🧠 Le cœur Deep Learning : un LSTM multi-entrées

Le modèle de prédiction n'est pas un simple classifieur de texte : c'est un **réseau de neurones à quatre branches**, conçu et entraîné pour ce projet.

```
Texte de l'avis ─► Embedding ─► LSTM ─► LSTM ──┐
Assureur ────────► Embedding ──────────────────┤
Produit ─────────► Embedding ──────────────────┼─► Concaténation ─► Dense ─► Dense ─► Note
Langue ──────────► Dense ──────────────────────┘
```

- 🔤 **Deux couches LSTM empilées** pour capter le sens et l'ordre des mots dans l'avis
- 🧩 **Embeddings appris** pour le texte, mais aussi pour l'assureur et le produit
- 🔀 **Fusion multimodale** : texte et variables catégorielles sont combinés avant la décision finale
- 🎯 **Régression** : le réseau prédit directement la note plutôt qu'une simple classe
- 🛡️ **Lutte contre le surapprentissage** : Dropout, régularisation L2 et arrêt anticipé (*early stopping*)

Et dans l'application, d'autres réseaux profonds prennent le relais : des **Transformers pré-entraînés** (BART, MiniLM, Flan-T5) pour classer, expliquer, retrouver et répondre.

## 🚀 Lancer le projet

1. Placez dans le dossier du notebook les fichiers de données (si le notebook est ouvert en dehors de cet espace) : `df_train.xlsx`, `modalites_assureurs.xlsx` et `modalites_produits.xlsx`
2. Exécutez les cellules de `NLP_AppliFinal.ipynb` dans l'ordre : le notebook entraîne le modèle, génère `app.py` et lance l'application
3. Ouvrez le lien public affiché à la fin 🎉

> 💡 Le partage de l'application passe par [ngrok](https://ngrok.com/) : il vous faudra un compte gratuit et votre propre jeton d'authentification.

## 📊 Résultats

Les performances du modèle et l'analyse détaillée sont disponibles dans le **PDF de présentation du projet**.

## 🛠️ Technologies

- Python 3, Jupyter Notebook
- Pandas, NumPy, scikit-learn
- TensorFlow / Keras (LSTM, embeddings), Hugging Face Transformers
- NLTK, Gensim (Word2Vec), langdetect
- Streamlit, ngrok
- Matplotlib, Seaborn, TensorBoard

---

Bonne exploration ! 🔍
