# CONVENTIONS.md — kern-wiki

Autorité locale pour ce repo, comme annoncé par le [CONTRIBUTING.md](https://github.com/kern-ia/.github/blob/main/CONTRIBUTING.md)
de l'organisation. Les règles communes à tous les repos `kern-ia` sont reprises ci-dessous ;
la section « Spécificités » couvre ce qui n'appartient qu'à `kern-wiki`.

`kern-wiki` héberge la documentation de conception et de package de l'org (visée annoncée par
`CONTRIBUTING.md` : « Design notes and package documentation live in the wiki »). D'après les
commits en cours (Epics 1 à 5), le repo est en train de devenir un site Hugo statique avec sa
propre suite de checks CI — ce document décrit la cible, pas encore un état stabilisé.

## Branches

- `main` : branche stable, publiée. Protégée — aucun push direct.
- Branches de travail : `feature/<slug>`, `docs/<slug>`, ou des branches nommées par epic
  (pattern déjà observé : `epic-2-github-surface-resolved`) tant que le repo est en
  construction — à faire converger vers `feature/epic-N-<slug>` une fois la structure stable.
- Toute modification de `main` passe par une Pull Request — déjà respecté (PR #60 en cours).

## Commits

Conventional Commits : `docs:` domine naturellement ici (contenu = documentation), `feat:`/
`chore:` pour l'outillage du site (build Hugo, CI). Aucune signature d'outil (trailer
`Co-Authored-By`, `Claude-Session` ou équivalent) dans les messages de commit.

## Pull Requests

- Un seul sujet par PR, liée à l'issue/epic qu'elle résout.
- Template PR hérité de `kern-ia/.github`.
- Pas de notion de semver applicable à ce repo (pas un package) — la case correspondante du
  template PR peut être marquée `none`.

## Contenu

- Une page = un sujet, liée à l'epic ou l'issue qui l'a produite.
- Les décisions de conception publiées ici doivent renvoyer vers la RFC ou l'issue d'origine
  plutôt que dupliquer son contenu.
- Aucune donnée personnelle réelle dans les captures, exemples ou schémas.

## CI

> **Écart actuel** : aucun workflow GitHub Actions n'existe encore sur ce repo, alors que les
> commits en cours (« the CI check suite that makes criterion 1 a lint rule ») annoncent son
> arrivée comme partie de l'Epic 1. À ajouter avant que le volume de pages ne rende la dérive
> difficile à rattraper.

## Documentation du repo lui-même

- `README.md` à ajouter s'il n'existe pas encore à la racine, décrivant comment builder et
  servir le site Hugo en local.
- Pas de `CLAUDE.md` aujourd'hui — à créer si des sessions Claude Code interviennent
  régulièrement ici (déjà le cas d'après l'historique de commits).

## Sécurité / confidentialité

Voir `SECURITY.md` hérité de l'org. Rien de spécifique en plus : ce repo ne contient pas de
code exécuté en production.
