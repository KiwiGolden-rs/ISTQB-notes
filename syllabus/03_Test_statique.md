# Chapitre 3 - Test statique

## 3.1 Bases du test statique

**Définition** : Le test statique est une activité de test qui **n'implique pas l'éxecution du code** ou du système. Il consiste à **examiner les produits d'activité** conçus tout au long du SDLC, afin d'identifier les anomalies, ambiguïtés, incohérences ou omissions avant l'exécution des tests dynamiques.
Les tests statiques comprennent deux grandes familles :
1. Les revues (*reviews*) : Activité humaines d'examen (informelles à très formelles).
2. L'analyse statique : Permet d'identifier les problèmes avant le test dynamique. Elle est souvent incorporée dans des frameworks d'intégration continue (CI).

**Objectifs du test statique** :
- **Détecter les défauts tôt** dans le SDLC (avant même la phase d'éxecution).
- **Améliorer la qualité** des livrables : lisibilité, complétude, justesse, testabilité et cohérence.
- **Réduire le coût des corrections** en corrigeant les anomalies avant l'implémentation.
- **Favoriser la communication** entre les parties prenantes.
- **Assurer la conformité** aux normes, aux exigences et aux critères qualité définis.

**Produits d'activités examinables par le test statique** : Le test statique peut s'appliquer à l'enssemble, ou presque, des produits d'activités et pas seulement au code. Ci-dessous, quelques exemples :
- **Documents de planification** : Plans de projet, plan de test, stratégie de test.
- **Exigences / spécifications** : *User stories* , cas d'utilisation, critères d'acceptation.
- **Modèles** : Architectures, workflows.
- **Code source** : Modules, script, fonctions.
- ***Testwares*** : Cas de test, jeux de donnée, script d'automatisation.
- **Documents de support** : Guides utilisateur, documentation technique.

**Valeur du test statique** :
Les tests statiques offrent les possibilités de :
- **Détection précoce des défauts**
  - Les erreurs détectées tôt coûtent moins cher à corriger qu'en phase de test ou après déploiement (i.e., corriger une exigence mal comprise avant le développement évite de recoder et retester).
- **Amélioration de la qualité globale**
  - Les revues permettent de vérifier la **complétude**, la **cohérence** et la **testabilité** des documents.
  - Les outils d'analyse statique identifient les **problèmes structurels** du code (complexité, dépendances, vulnérabilité).
- **Renforcement de la communication**
  - Améliore la compréhension commune du produit et des attentes.
- **Complémentarité avec le test dynamique**
  - Les tests statiques **ne remplacent pas** les tests dynamiques.
  - Les testent statiques les **préparent** en assurant la qualité des *testwares* utilisés (plans, cas de test, code).
  - Les anomalies détectées statiquement réduisent le nombre de défauts avant les tests dynamiques.

**Différence entre le test statique et le test dynamique** : Les pratiques de test statique et dynamique **se complètent**. Elles ont des objectifs similaires, tels que la détection des défauts dans les produits d'activités, mais il existe également des différences, comme :
- Certains types de défauts ne peuvent être trouvés que par le test statique ou le test dynamique.
- Le test **statique** constate directement les **défauts**, tandis que le test **dynamique** provoque des **défaillances** à partir desquelles les défauts associés sont déterminés par une analyse ultérieure.
- Le test statique permet de détecter plus facilement les défauts qui se trouvent sur des **chemins du code rarement exécutés ou difficile à atteindre** par le test dynamique.
- Le test **statique** peut être appliqué à des produits d'activités **non exécutables**, alors que le test **dynamique** ne peut être appliqué qu'à des produits d'activités **exécutables**.
- Le test statique peut être utilisé pour mesurer les caractéristiques qualité (e.g., la maintenabilité) qui ne dépendent pas de l'exécution du code, tandis que le test dynamique peut être utilisé pour mesurer les caractéristiques qualité (e.g., l'efficacité de la plateforme) qui dépendent de l'exécution du code.

Les défauts typiques qu'il est **plus facile et/ou moins coûteux** de trouver par le biais du test statique :
- Défauts dans les exigences (e.g., incohérences, ambiguïtés, contradictions, omissions, inexactitudes, duplications).
- Défauts de conception (e.g., structures de base de données inefficaces, modularité insuffisante).
- Certains types de défauts de codage (e.g., variables avec des valeurs non définies, variables non déclarées, code inaccessible ou dupliqué, complexité excessive du code).
- Des écarts par rapport aux standards (e.g., le non-respect des conventions de nommage dans les standards de codage).
- Des spécifications d'interface incorrectes (e.g., nombre, type ou ordre des paramètres non concordants).
- Des types spécifiques de vulnérabilités en matière de sécurité (e.g., *buffer overflows*).
- Des lacunes ou des imprécisions dans la couverture de la base de test (e.g., tests manquants pour un critère d'acceptation).

## 3.2 Processus de feedback et de revue

**Bénéfices d'un feedback précoce et fréquent des parties prenantes** : Le feedback (retour d'information) est une composantes essentielle des tests statiques. En effet, le feedback précoce et fréquent permet :
- **Amélioration de la compréhension commune**
  - Les parties prenantes comprennent mieux les exigences et contraintes.
  - Réduit les **malentendus** et les **redondances** entre équipe.
  - Améliore la compréhension de l'équipe de développement de ce qu'elle est en train de construire.
- **Meilleure qualité et productivité**
  - Les produits d'activités sont revus en continu ce qui amène à moins d'erreurs cumulées.
  - Optimisation du processus de développement ce qui apporte en qualité et en productivité.

**Activités du processus de revue** : Le **standard ISO/IEC 20246** définit un processus de revue générique qui fournit un cadre structuré mais flexible à partir duquel un processus de revue spécifique peut être adapté à une situation particulière.
Les activités du processus de revue sont les suivantes :
- **Planification** : Au cours de la phase de planification, le périmètre de la revue, qui comprend l'objectif, le produit d'activités à éxaminer, les caractéristiques-quelité à évaluer, les domaines à privilégier, les critères de sortie, les informations complémentaire (telles que les standards), l'effort et les délais de la revue ; doit être défini.
- **Lancement de la revue** : Lors du lancement de la revue, l'objectif est de s'assurer que toutes les personnes impliquées sont prêtes à commencer la revue. Il s'agit notamment de s'assurer que chaque participant a accès au produitd'activités examiné, qu'il comprend son rôle et ses responsabilitéset qu'il reçoit tout ce qui est nécessaire à l'exécution de la revue.
- **Revue individuelle** : Chaque révisuer effectue une revue individuelle afin d'évaluer la qualité du produit d'activités en cours de revue et d'identifier les anomalies, les recommandations et des questions en appliquant une ou plusieurs techniques de revue (e.g., checklists, scénarios). Les réviseurs enregistrent toutes les anomalies, recommandations et questions qu'ils ont identifiées.
- **Communication et analyse** : Les participants se réunissent pour discuter des défauts identifiés, afin de confirmer, clarifier et classer les anomalies.
- **Correction et rapport** : Pour chaque défauts, un rapport de défaut doit être créé afin que les actions correctives puissent faire l'objet d'un suivi. Lorsque les critères de sortie sont atteints, le produit d'activités peut être accepté. Les résultats de la revue font l'objet d'un rapport.

**Rôles et responsabilités dans les revues** :
Une revue réussi repose sur une répartition claire des rôles :
- **Manager** : Décide de ce qui doit être revu et fournit les ressources, telles que le personnel et le temps nécessaires à la réalisation de la revue.
- **Auteur** : Crée et corrige le produit d'activités en cours de revue.
- **Modérateur (facilitateur)** : Planifie et pilote la revue, veille au respect du processus et anime les discussions.
- **Scribe (rapporteur)** : Rassemble les anomalies provenant des réviseurs et enregistre les informations relatives à la revue, telles que les décisions et les nouvelles anomalies trouvées au cours de la réunion de revue.
- **Réviseur** : Effectue les revues. Il peut être une personne travaillant sur le projet, un expert en la matière ou toute autre partie prenante.
- **Responsable de la revue** : assume la responsabilité générale de la revue, notamment en décidant qui sera impliqué et en organisant le lieu et la date de la revue.

**Types de revues** : Les revues peuvent varier du plus informel au plus formel.
Le choix du bon type de revue est essentiel pour atteindre les objectifs de revue requis. La selection ne se fait pas uniquement via les objectifs, mais aussi par des facteurs tels que les besoins du projet, les disponibilités, le type de produit d'activité et les risques, le domaine d'activité et la culture de l'entreprise.
Exemples de revues couramment utilisés :
- **Revue informelle** : Les revues informelles ne suivent pas un processus défini et n'éxigent pas de résultat formel documenté. L'objectif principal est de détecter des anomalies.
- **Relecture technique** : Une relecture technique, menée par l'auteur, peut répondre à de nombreux objectifs, tels que l'évaluation de la qualité et le renforcement de la confiance dans le produit d'activités, la formation des réviseurs, l'obtention d'un consensus, la génération de nouvelles idées, la motivation et la capacité des auteurs à s'améliorer et la détection d'anomalies. Les réviseurs peuvent effectuer une revue individuelle avant la relecture technique, mais ce n'est pas obligatoire.
- **Revue technique** : Se fait par des réviseurs techniquement qualifiés et dirigée par un modérateur. Les objectifs sont de parvenir à un consensus et de prendre des décision concernant un problème technique, mais aussi de détecter des anomalies, d'évaluer la qualité et de construire la confiance dans le produit d'activités, de générer de nouvelles idées, de motiver les auteurs et de leur permettre de s'améliorer.
- **L'inspection** : Il s'agit du type de revue le plus formel, elle suit le processus générique complet. L'objectif principal est de trouver le maximum d'anomalies. Elle a aussi comme objectif d'évaluer la qualité, de construire la confiance dans le produit d'activités, de motiver les auteurs et de leur permettre de s'améliorer. Des métriques sont collectées et utilisées pour améliorer le SDLC, y compris le processus d'inpection. Lors des inspections, l'auteur ne peut pas jouer le rôle de réviseur ou de scribe.

**Facteurs de réussite des revues** :
Certaines conditions favorisent le succès d'une revue :
- Définir des **objectifs clairs** et des **critères de sortie mesurables**. L'évaluation des participants ne doit jamais être un objectif.
- Choisir le **type de revue approprié** pour atteindre les objectifs fixés et s'adapter au **type de produit d'activités**, aux **participants** à la revue, aux **besoins** du projet et au **contexte**.
- Réaliser des revues en **petits groupes**, pour que les réviseurs ne se déconcentrent pas au cours d'une revue individuelle et/ou de la réunion de revue.
- Fournir un **feedback** des revues **aux parties prenantes et aux auteurs** pour qu'ils puissent améliorer le produit et leurs activités.
- Accorder aux participants **suffisamment de temps** pour se préparer à la revue.
- Bénéficier d'un **soutient**, de la part du management, au processus de revue.
- Intégrer les revues dans la **culture de l'organisation**, afin de promouvoir l'apprentissage et l'amélioration des processus.
- Fournir une **formation adéquate** à tous les participants afin qu'ils sachent comment remplir leur rôle.
- Faciliter les réunions.

## :white_check_mark: Synthèse
- Le test statique est une approche efficace pour détecter des **défauts sans éxecuter le logiciel** : Il s'applique à de nombreux livrables, pas uniquement au code.
- Il offre un retour **précoce et fréquent**, réduisant les coûts de correction et améliorant la qualité du produit.
- Le test statique ne remplace pas le test dynamique : Les deux sont complémentaires. La compréhension de leurs différences est essentielle.
- Dans un contexte moderne (e.g., agile/DevOps), le test statique joue un rôle important dans la montée en qualité et le *shift left*.
- Le processus de revue est structuré : grâce à des rôles, des activités planifiées, des types de revue adaptés et des conditions de succès identifiées.