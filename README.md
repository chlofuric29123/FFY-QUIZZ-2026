# Questionnaire « Qui est le plus ? »

Le dossier contient :
- `index.html` : questionnaire à envoyer aux participants.
- `results.html` : page organisateur avec résultats, pourcentages et classement.
- `data.js` : participants + 43 questions.
- `style.css` : design.
- `firebase-config.js` : configuration Firebase à renseigner pour que les votes de tous les téléphones se regroupent.

## Mise en ligne sur GitHub Pages
1. Crée un nouveau dépôt GitHub (par ex. `weekend-questionnaire-2026`).
2. Ajoute les 5 fichiers du dossier.
3. Dans GitHub : Settings → Pages → Deploy from a branch → `main` / `(root)` → Save.
4. Le questionnaire sera à `https://TON-PSEUDO.github.io/weekend-questionnaire-2026/`
5. Les résultats seront à `https://TON-PSEUDO.github.io/weekend-questionnaire-2026/results.html`

## Pour centraliser les votes de tous les téléphones
GitHub Pages ne stocke pas les réponses. Il faut activer Firebase Realtime Database :

1. Va sur Firebase Console et crée un projet.
2. Ajoute une application Web.
3. Active **Realtime Database**.
4. Copie la configuration Firebase dans `firebase-config.js`.
5. Dans les règles Realtime Database, utilise pendant le week-end :

```json
{
  "rules": {
    "submissions": {
      ".read": true,
      "$voter": {
        ".write": true
      }
    }
  }
}
```

Après le week-end, désactive les écritures ou supprime la base.

## Détails
- Chaque participant choisit son prénom au début.
- Un même prénom renvoie/écrase son vote précédent : pratique pour corriger.
- Une réponse est obligatoire par question.
- Pour « Qui a la plus grosse bite ? », **Julien est la seule réponse proposée**.
- La page résultats est protégée côté interface par le code `weekend2026`.
  Pour le modifier, change `const ADMIN_CODE="weekend2026";` dans `results.html`.

⚠️ La protection par code est surtout pour éviter que les invités ouvrent les résultats par accident ; ce n’est pas une sécurité forte puisque le site est statique.
