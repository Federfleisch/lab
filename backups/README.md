# Backups

`latest.json` est un instantané des tables Supabase (`games` et
`flashcard_status`), régénéré chaque jour par le workflow
`.github/workflows/backup.yml`.

## Historique / restauration

Chaque backup est un commit : l'**historique Git de ce fichier** contient
donc toutes les versions quotidiennes.

- Voir les versions : `git log --oneline -- backups/latest.json`
- Récupérer une version d'une date : `git show <commit>:backups/latest.json > restore.json`

Le fichier contient `games` et `flashcard_status` sous forme de tableaux
JSON, réinjectables dans Supabase (import CSV/JSON ou `insert` via l'API).
