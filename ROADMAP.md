# Feuille de route — Carnet de progression Échecs

> Liste des évolutions souhaitées, à implémenter **uniquement sur demande explicite**.
> Rien dans cette liste ne doit être réalisé sans un ordre du propriétaire du carnet.

## À faire

- [ ] **1. Écran d'accueil = ajout d'un PGN** — faire de l'ajout d'une partie (coller un PGN) l'écran d'accueil / la vue par défaut du carnet.
- [ ] **2. Analyse automatique à l'ajout** — dès qu'un PGN est ajouté, afficher l'analyse du coach et ses recommandations pour progresser.
- [ ] **3. Flashcards générées depuis la partie** — créer automatiquement de nouvelles flashcards à partir des erreurs / thèmes de la partie ajoutée.
- [ ] **4. Redirection vers les nouvelles flashcards** — après l'ajout et la génération, rediriger vers les flashcards nouvellement créées.

## Fait

- [x] **5. Vérification automatique de l'Elo** — synchro depuis Chess.com (`fi0riture`) : live dans le navigateur au chargement et à chaque partie ajoutée (API publique), plus un GitHub Action quotidien (`.github/workflows/sync-elo.yml`) qui met `assets/elo.json` à jour côté serveur — garantit la mise à jour au moins une fois par jour même page fermée. _(Fait le 31/07/2026.)_

---
_Tenu à jour par le coach. Aucune des features restantes n'est développée tant que le propriétaire ne l'a pas explicitement demandé._
