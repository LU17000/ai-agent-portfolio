# Étude de cas — Conception d'un workflow de développement logiciel multi-agents contrôlé

*Projet personnel de R&D · Prototype expérimental · Présentation anonymisée*

## Vision

L'objectif à long terme est de transformer une idée de logiciel exprimée en langage naturel en une application fonctionnelle, testée et livrable, avec un minimum d'interventions humaines.

Il s'agit de **l'objectif visé**, et non d'une affirmation selon laquelle une automatisation complète, de l'idée au produit final, aurait déjà été atteinte. Le projet actuel explore les étapes plus ciblées et vérifiables nécessaires pour y parvenir.

## Problème à résoudre

Les agents IA de développement peuvent générer et modifier du code, mais les coordonner au sein d'un processus fiable introduit plusieurs risques : un modèle peut déclarer avoir réussi sans preuve suffisante, valider une révision dépassée, répéter une action distante après une interruption ou franchir une limite d'autorisation.

Le défi consistait à transformer des interactions entre agents en un workflow contrôlé, avec des vérifications indépendantes, une progression récupérable et une supervision humaine.

## Approche

Le prototype distingue les tâches réalisées par les modèles IA du contrôle déterministe du workflow :

1. Confier des tâches de développement délimitées à des agents, notamment Claude Code et Codex.
2. Exécuter des contrôles définis et demander une revue indépendante.
3. Renvoyer les problèmes identifiés dans un cycle de correction encadré.
4. Vérifier à nouveau les changements et les preuves associées à la bonne révision.
5. Exiger des autorisations explicites pour les opérations sensibles et conserver suffisamment d'état pour reprendre après une interruption.

Les outils tiers de coordination et les modèles intégrés ne sont pas présentés comme des inventions personnelles.

## Mécanismes implémentés

Le prototype examiné contient du code et des tests ciblés pour :

- **Orchestration et corrections limitées :** implémentation, revue, correction et nouvelle validation, avec des limites explicites.
- **Évaluation indépendante :** séparation entre les participants à l'implémentation et une étape distincte de revue finale.
- **Vérification CI associée au commit :** contrôle du dépôt, de la révision, du workflow, de la tentative d'exécution et des tâches attendues, plutôt que de se fier à une déclaration de réussite d'un agent.
- **Reprise après interruption :** conservation de l'état des missions et traitement des opérations interrompues ou incertaines.
- **Autorisation humaine :** contrôles liés à des actions précises et à leurs conditions.
- **Encadrement de l'exécution :** isolation par conteneur et vérifications des conditions d'exécution des agents.
- **Livraison contrôlée :** étapes d'intégration au dépôt et de revue, sans prétendre à un déploiement d'application en production.

## Validation et résultats observés

Des tests automatisés avec des acteurs contrôlés couvrent notamment le rejet d'une implémentation par un agent réviseur, suivi d'une correction et de nouveaux contrôles. Ils couvrent également des scénarios de reprise, d'autorisation et de preuves de validation périmées.

La documentation du projet rapporte des essais réels limités avec des agents de développement sur des dépôts temporaires. Certaines exécutions ont atteint un état prêt pour revue ou des étapes de livraison contrôlée, mais ont aussi nécessité des investigations et des corrections. Elles ne démontrent pas un fonctionnement autonome prolongé sans intervention.

Certains contrôles GitHub CI ont réussi pour des révisions précises ; cela ne certifie ni les modifications locales ultérieures ni le système dans son ensemble.

Le principe essentiel démontré est que **la déclaration de réussite d'un agent ne suffit pas : l'achèvement doit reposer sur des preuves vérifiées indépendamment**.

## Mon rôle et attribution des outils

J'ai défini l'objectif du projet et piloté la conception du système, ses règles de fonctionnement, ses critères d'acceptation et les priorités de revue. J'ai supervisé l'implémentation et la validation assistées par IA, auxquelles Claude Code, Codex et d'autres outils intégrés ont participé.

Cette description correspond à un rôle de porteur de projet et de concepteur de systèmes IA ; elle **ne signifie pas** que j'ai écrit manuellement l'intégralité du code.

## Limites actuelles

- Prototype expérimental, non prêt pour la production.
- L'automatisation complète, de l'idée au logiciel terminé, reste un objectif et non une capacité validée.
- Les tests automatisés déterministes couvrent davantage de cas que les essais répétés avec de vrais modèles.
- L'isolation et les contrôles d'autorisation réduisent certains risques, sans constituer une certification de sécurité.
- Aucun gain de productivité, aucune économie et aucun taux de fiabilité global chiffrés ne sont revendiqués sans preuve.
- Aucune reproduction publique complète n'est fournie ; les sources et l'infrastructure privées restent confidentielles.

## Compétences illustrées

Conception de systèmes IA ; orchestration multi-agents ; workflows de développement assisté par IA ; revue indépendante ; validation des preuves CI ; reprise après défaillance ; autorisation humaine ; automatisation encadrée ; tests d'intégration ; documentation technique.

---

**Note sur les preuves :** cette étude de cas est une synthèse anonymisée fondée sur l'examen d'un projet privé expérimental et de ses tests. Elle ne publie aucun code privé, chemin interne, secret ni architecture propriétaire. Les preuves techniques originales détaillées ne sont pas publiées ici.
