# Le Brief — site avec flux d'éditions synchronisable

Ce projet contient `index.html` (site autonome), `editions.json` (flux public des éditions), `lebrief.config.json` (signature pour retrouver le dépôt). Les 10 éditions initiales restent embarquées dans `index.html`.

## Publication GitHub Pages
1. Connecter GitHub à ChatGPT et autoriser l'accès au dépôt destiné à Le Brief.
2. Créer un dépôt GitHub (par exemple `le-brief`) et y déposer les trois fichiers à la racine. Si vous le souhaitez, garder le dépôt privé selon les possibilités du plan et du produit d'hébergement. GitHub Pages public publie le contenu accessible publiquement.
3. Dans Settings → Pages, choisir « Deploy from a branch », branche `main`, dossier `/ (root)`.
4. Ouvrir l'adresse GitHub Pages. Le site charge automatiquement `editions.json` à chaque ouverture et via l'icône Actualiser.
5. Fournir le propriétaire/dépôt exact et l'adresse GitHub Pages dans la conversation pour finaliser la configuration de publication des deux tâches planifiées.

## Format d'une édition
Chaque édition du flux possède un ID stable et unique (`fintech-YYYY-MM-DD` ou `cyber-YYYY-MM-DD`), `category` (fintech|cyber), `date`, `title`, `summary`, `content` en Markdown, `minutes`, `tag`, `number`, `takeaways` (liste de textes), `sources` (tableaux {title,url}) et `quiz` (liste {question,options,answer,explanation}). Le champ `answer` est l'index 0-based du bon choix. Conserver les autres éditions et les deux catégories lors de tout ajout ; ne pas effacer l'historique. Publier une seule édition par série et par jour.

Exemple de payload :
```json
{
  "format": "lebrief-feed-v1",
  "site": "lebrief",
  "updatedAt": "2026-10-30T08:00:00+01:00",
  "editions": [
    {
      "id": "fintech-2026-10-30",
      "category": "fintech",
      "date": "2026-10-30",
      "number": 6,
      "title": "Exemple : comprendre un paiement",
      "summary": "Exemple fictif, à remplacer par la veille réelle",
      "minutes": 4,
      "tag": "Architecture",
      "content": "## Le sujet du jour\n\nTexte vérifié et sourcé...",
      "takeaways": ["Point 1", "Point 2", "Point 3"],
      "sources": [{"title": "Documentation éditeur", "url": "https://example.org"}],
      "quiz": [{"question": "Quelle est la bonne réponse ?", "options": ["A", "B", "C"], "answer": 0, "explanation": "Explication courte."}]
    }
  ]
}
```

## Contraintes
- Le site ne peut pas écrire dans un dépôt depuis le navigateur : l'écriture doit être effectuée par une tâche disposant d'un outil GitHub autorisé.
- Le fichier local (`file://`) reste lisible, mais la synchronisation du flux se fait depuis la version `https://` publiée.
- Les états « J'ai lu » et les réponses aux quiz sont stockés dans `localStorage` et restent propres au navigateur. Utiliser l'export JSON existant pour sauvegarder ou transférer cette progression.
- Les tâches ChatGPT restent activées du lundi au vendredi aux horaires existants, indépendantes l'une de l'autre. La connexion GitHub, le dépôt exact et l'hébergement doivent être finalisés pour que la publication automatique fonctionne.
