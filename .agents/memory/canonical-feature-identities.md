---
name: Identifiants canoniques des fonctionnalités
description: Règle de conversion des libellés, slugs et identifiants historiques avant l’affichage des modules.
---

Les sélections de fonctionnalités doivent être converties par les options canoniques du module avant d’alimenter les permissions, le menu latéral ou les onglets internes. Les identifiants de navigation restent distincts des slugs de permission.

**Why:** La réorganisation de l’administration MAXIMUS a pu laisser des valeurs persistées sous forme de libellés ou d’anciens alias. Les filtrer directement contre des identifiants modernes faisait disparaître des entrées ou désynchronisait le menu et la page.

**How to apply:** Faire passer toute sélection par la normalisation de `module-features`, conserver un libellé canonique pour le rendu, puis convertir séparément vers l’identifiant d’onglet dans chaque routeur.

Pour Immobilier, la liste canonique doit rester synchronisée à quatre endroits : catalogue des fonctionnalités, liens du menu, paramètre `feature` de la route et vue rendue. Une entrée visible dans le menu ne doit jamais retomber sur une vue par défaut d’une autre entrée.

**Why:** Une correction limitée à deux liens peut laisser les autres fonctionnalités Immobilier afficher le même écran, ce qui rend le routage nominal mais le parcours métier incohérent.

**How to apply:** Ajouter toute nouvelle fonctionnalité dans `getModuleFeatureOptions`, le test de routes Immobilier et la table de vues du module avant de la publier dans un pack.

Dans le menu des comptes employés et managers, la sélection de fonctionnalités d’une unité ne peut qu’affiner le menu : elle doit être recoupée avec le droit `voir` du rôle. Une sélection d’unité plus large ne doit pas exposer les entrées non accordées.

**Why:** Les sélections explicites d’unité peuvent être plus larges que les droits d’un employé; les utiliser seules rend le menu incohérent avec l’autorisation effective.

**How to apply:** Calculer les fonctionnalités visibles comme l’intersection de la sélection de l’unité et des permissions de lecture du rôle, en gardant les contrôles API comme autorité.