# Mini Tweeter (Vite + React)

Tutoriel simple pour recréer la même app pas à pas.

## Objectif

Créer une mini application type Twitter/X avec ces fonctionnalités :

- Poster un tweet
- Afficher la liste des tweets
- Aimer un tweet
- Supprimer un tweet
- Limiter le message à 280 caractères

## Prérequis

- Node.js et npm installé (nodejs.org)

## 1) Créer le projet Vite React

```bash
npm create vite@latest mini-tweeter-vite -- --template react
cd mini-tweeter-vite
npm install
```

## 2) Ajouter Tailwind via CDN

Dans `index.html`, ajoute le script dans `<head>` :

```html
<script src="https://cdn.tailwindcss.com"></script>
```

But: utiliser les classes utilitaires Tailwind sans config complexe.

## 3) Simplifier le CSS global

Dans `src/index.css`, garde un style minimal (reset léger) :

- `box-sizing: border-box`
- `body { margin: 0; font-family: Arial, Helvetica, sans-serif; }`
- `#root { min-height: 100vh; }`

But: laisser Tailwind gérer la majorité du design.

## 4) Créer la structure des fichiers

Crée ces dossiers/fichiers :

```txt
src/
	components/
		FormulaireTweet.jsx
		Tweet.jsx
	services/
		serviceTweet.js
	App.jsx
```


## 6) Créer le service local (fausse API)

Dans `src/services/serviceTweet.js` :

- `stockageTweets` : tableau local en mémoire
- `attendre(ms)` : petite latence simulée
- `obtenirTweets()` : retourne tous les tweets
- `creerTweet(message)` : crée un tweet et l’ajoute en tête
- `basculerAimeTweet(idTweet)` : inverse l’état `aime`
- `supprimerTweet(idTweet)` : retire le tweet ciblé

But: séparer la logique de données de l’interface, comme avec une vraie API.

## 7) Créer le composant formulaire

Dans `src/components/FormulaireTweet.jsx` :

- État local du message (`useState`)
- État de publication (`enCoursPublication`)
- Compteur de caractères (`caracteresRestants`)
- Soumission du formulaire (`onCreer`) fournie par le parent

But: isoler la création de tweet dans un composant réutilisable.

## 8) Créer le composant tweet

Dans `src/components/Tweet.jsx` :

- Affiche un tweet
- Bouton « Aimer » (`onAimer`)
- Bouton « Supprimer » (`onSupprimer`)

But: encapsuler l’affichage d’un tweet et ses actions.

## 9) Assembler tout dans App.jsx

Dans `src/App.jsx` :

- `listeTweets` dans un `useState`
- Chargement initial via `obtenirTweets()` (`useEffect`)
- `gererCreationTweet` → appelle `creerTweet`
- `gererAimeTweet` → appelle `basculerAimeTweet`
- `gererSuppressionTweet` → appelle `supprimerTweet`
- Rendu conditionnel : message vide si aucun tweet, sinon liste

But: `App` orchestre les composants + le service.

## 10) Lancer et vérifier

```bash
npm run dev
```

Puis pour vérifier la qualité :

```bash
npm run lint
npm run build
```

## À quoi sert chaque élément ?

- `index.html` : point d’entrée HTML + CDN Tailwind
- `src/main.jsx` : monte React dans `#root`
- `src/App.jsx` : écran principal et logique d’orchestration
- `src/components/FormulaireTweet.jsx` : création d’un tweet
- `src/components/Tweet.jsx` : affichage d’un tweet + actions
- `src/services/serviceTweet.js` : couche « données » locale simulant une API
- `src/index.css` : styles globaux minimaux

---

Tu peux maintenant reproduire le projet de zéro, étape par étape, sans complexité inutile.
