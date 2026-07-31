# Feuille de route — Carnet de progression Échecs

> Liste des évolutions souhaitées, à implémenter **uniquement sur demande explicite**.
> Rien dans cette liste ne doit être réalisé sans un ordre du propriétaire du carnet.

## À faire

- [ ] **1. Écran d'accueil = ajout d'un PGN** — faire de l'ajout d'une partie (coller un PGN) l'écran d'accueil / la vue par défaut du carnet.
- [ ] **4. Redirection vers les nouvelles flashcards** — après l'ajout et la génération, rediriger automatiquement vers les flashcards nouvellement créées. _(Pour l'instant : bouton manuel « Voir les flashcards ».)_

## Fait

- [x] **2. Analyse automatique à l'ajout** — carte « Analyse du coach » affichée à l'ajout d'un PGN (et dans la visionneuse) : bilan factuel calculé côté navigateur avec chess.js (issue/mat, roque, plus gros recul matériel net, pression de la dame sur le roi, échecs subis). _(Fait le 31/07/2026.)_
- [x] **3. Flashcards générées depuis la partie** — flashcards ancrées sur la partie, dédoublonnées et persistées (localStorage), ajoutées au paquet. _(Fait le 31/07/2026. À basculer un jour vers Supabase pour la synchro multi-appareils — nécessite une table.)_
- [x] **5. Vérification automatique de l'Elo** — synchro depuis Chess.com (`fi0riture`) : live dans le navigateur au chargement et à chaque partie ajoutée (API publique), plus un GitHub Action quotidien (`.github/workflows/sync-elo.yml`) qui met `assets/elo.json` à jour côté serveur — garantit la mise à jour au moins une fois par jour même page fermée. _(Fait le 31/07/2026.)_

---
_Tenu à jour par le coach. Aucune des features restantes n'est développée tant que le propriétaire ne l'a pas explicitement demandé._
