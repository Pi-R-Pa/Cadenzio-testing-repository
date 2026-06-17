# Cadenzio — Testing Repository

Ce repository est un **dépôt de test dédié à l'application [Cadenzio](https://github.com/Pi-R-Pa/dora-metric-kpi-accelerate)**. Il n'héberge aucun code applicatif et ne doit pas être utilisé à d'autres fins.

---

## Objectif

Ce dépôt sert à valider le bon fonctionnement de deux fonctionnalités critiques de Cadenzio :

### 1. Clone de repository

Cadenzio clone les repositories Git enregistrés afin d'accéder à leur historique (tags, commits, dates, auteurs, annotations). Ce dépôt est utilisé pour vérifier que le mécanisme de clonage fonctionne correctement — authentification, accès réseau, écriture sur disque, mise à jour ultérieure via `fetch`.

> Cadenzio lit **uniquement les métadonnées Git**. Aucune analyse sémantique du contenu du code n'est effectuée.

### 2. Calcul des métriques DORA

Une fois cloné, ce dépôt sert de données d'entrée pour valider le moteur de calcul des quatre métriques DORA :

| Métrique | Description |
|---|---|
| **Deployment Frequency** | Nombre de déploiements en production sur une période (les hotfixes ne sont pas comptabilisés). |
| **Lead Time for Change** | Temps entre le premier commit d'une release et son déploiement en production. |
| **Change Failure Rate** | Ratio hotfixes / total déploiements (releases + hotfixes). |
| **Mean Time to Restore (MTTR)** | Temps entre le déploiement d'une release incidente et le hotfix qui la corrige. |

Les calculs s'appuient sur les **tags Git annotés** de ce dépôt, qui suivent les conventions de tagging de Cadenzio (semver + suffixe `-hotfix` + annotation `Team XXX`).

## Lien avec Cadenzio

| Cadenzio | Ce dépôt |
|---|---|
| Clonage & synchronisation des repos | Cible de test du clone |
| Cron de calcul DORA (00h10 quotidien) | Source de tags pour le calcul |
| Aperçu des regexps (backoffice) | Alimente la table `raw_tags` |
| Benchmarks Elite / High / Medium / Low | Résultats attendus documentés dans les scénarios de test |

---

## ⚠ Avertissement

Ce dépôt est **en lecture seule du point de vue de Cadenzio** : l'application n'y écrit jamais. Toute modification de l'historique Git (rebase, suppression de tags) peut invalider les scénarios de test existants.
