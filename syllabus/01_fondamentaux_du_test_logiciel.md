# Chapitre 1 - Fondamentaux du test logiciel

## Objectifs d'apprentissage
Comprendre pourquoi le test logiciel existe, ses objectifs, ses principes, son processus et les compétences essentielles attachées à cette pratique.

## 1.1 Qu'est-ce que le Test ?

**Définition** : Le test est un ensemble d'activités visant à **découvrir des défauts** et à **évaluer la qualité** des produits de travail logiciel. On appel **objets de test** (*test objects*) ces derniers lorsqu'ils sont soumis au test.

**Vérification & Validation** : Le test comprend la **vérification** (vérifier que le produit satisfait aux exigences spécifiées) et la **validation** (vérifier que le produit répond aux besoin réels des utilisateurs et des parties prenantes).

**Types de test** : Le test peut être **statique** (n'implique pas l'éxécution de l'objet de test, implique les revues et l'analyse du code par exemple) ou **dynamique** (implique l'éxécution de l'objet de test).

**Objectifs type du test** : L'**évaluation** des objets de test (e.g. : code, exigences) ; **provoquer des défaillances** pour trouver des défauts ; assurer la bonne **couverture** requise pour l'objet de test ; **réduire le risque** d'une qualité insuffisante ; vérifier la **conformité** aux éxigences contractuelles et/ou réglementaire ; **valider** les attentes des parties prenantes ; **fournir des informations** aux partie prenantes pour la prise de décisio éclairée.

**Test vs. Débogage** : Il s'agit bien de deux activités distinctes, mais complémentaires. Le **test** est là pour **chercher et trouver** des défauts pouvant amener à des défaillances du logiciel. Le **débogage** est le processus d'**analyse et d'élimination** du défaut (correction du défaut). Après correction, un **test de confirmation** vérifie la résolution du problème, et un **test de régression** vérifie l'absence de nouveaux défauts introduits ailleurs.

## 1.2 Pourquoi le test est nécessaire ?

**Nécessité** : Le test est nécessaire comme forme de **contrôle qualité** pour aider à atteindre les objectifs définis et constitue un moyen **rentable** de détecter les défauts. Il peut aussi être requis pour la conformité légale ou contactuelles.

**Test et Assurance Qualité (AQ)** : Le **test** est une approche **corrective, orientée produit** (contôle qualité). L'**AQ** est une approche **préventive, orientée processus**. Les résultats des test sont utilisés par l'AQ pour évaluer la performance des processus de développement et de test.

**Erreurs, défauts, défaillances et causes racine** : Une **erreur** (*error*) humaine engendre un **défaut** (*defect* ou *bug*). L'execution du défaut peut entraîner une **défaillance** (*failure*) du système. La **cause racine** est la raison principale d'un problème, et son analyse vise à prévenir de futurs problèmes similaires.

## 1.3 Principe du test

Les sept grands principes du test :
1. **Le test montre la présence, pas l'absence de défauts** : Le test peut prouver la présence de défauts, mais jamais leur absence.
2. **Le test exhaustif est impossible** : Tout tester n'et pas réalisable, sauf cas triviaux. Les efforts de test doivent être concentrés à l'aide de techniques de test et de priorisation basée sur les risques.
3. **Le test précoce (*shift-left*) économise du temps et de l'argent** : Les défauts éliminés tôt ne causeront pas de défauts subséquents. Les tests statiques et dynaiques devraient commencer le plus tôt possible.
4. **Les défauts se regroupent** : L'effort de test devrait être fixé proportionnelement à la densité des défauts prévus et constatés dans différents modules. La plupart des défauts découverts (ou des défaillances opérationnelles) se trouvent généralement dans un petit nombre de composants du système (principe de Pareto).
5. **Les tests s'usent (Paradoxe du pesticide)** : Répéter les même tests plusieurs fois devient inefficace pour détecter de nouveaux défauts. Les tests et les données de test doivent être revus et révisés, sauf dans le cas de test de régression automatisé.
6. **Le test dépend du contexte** : Il n'existe pas d'approche de test unique universellement applicable. Le test est effectué différement dans des contextes différents.
7. **Le sophisme de l'absence de défauts (*Absence-of-defects fallacy*)** : Tester minutieusement toutes les exigences et corriger tous les défauts ne garantit pas le succès du prodramme s'il ne répond pas aux besoins réels des utilisateurs (d'où l'importance de la validation en plus de la vérification).

## 1.4 Activités de test, outils de test (*testware*) et rôles de test

Activités majeures du **processus de test** : 
- **Planification du test** : Définition des objectifs et sélection de l'approche qui permet de réaliser ces objectifs.
- **Surveillance et contrôle du test** : Vérification continue des activités par rapport au plan et prise d'actions nécessaires pour atteindre les objectifs.
- **Analyse du test** : Analyser la base du test (*test basis*) pour identifier les fonctionnalités testables, les conditions de test, et évaluer la testabilité de l'objet de test. Cette phase répond à la question "quoi tester ?".
- **Conception du test** : Elaborer les conditions de test en cas de test (*test cases*). Identifier les exigences de données et l'environnement de test. Cette phase répond à la question "comment tester ?".
- **Implémentation du test** : Créer les outils de test (*testware*), organiser les cas de test en procédures de test et suite de test. Les procédures de test sont classées par ordre de priorité et organisées dans un calendrier d'execution des test. L'environnement de test est mis en place et vérifié afin d'assurer qu'il est correctement configuré.
- **Execution du test** : Exécuter les tests manuellement ou automatiquement, comparer les résultats, enregistrer les résultats et analyser les anomalies observées.
- **Achèvement du test** : Se produit aux étapes importantes du projet (e.g., livraison, fin d'itération, niveau de test achevé). La phase d'achèvement comprend la gestion des défauts non résolus, l'archivage des outils de test utile pour le futur, l'analyse des leçons apprises ainsi que la communication d'un rapport de fin de test aux parties prenantes.
  
**Contexte** : Le processus de test doit être adapté au contexte, influencé par des facteurs tels que : les parties prenantes ; les membres de l'équipe (compétences, etc.) ; le domaine d'activité (criticité, risques, besoin du marcher, etc.) ; les facteurs techniques (architecture, technologie utilisée, type de logiciel, etc.) ; les contraintes du projet (temps, budget, etc.) ; les facteurs organisationnels (politiques existantes, pratiques utilisées, etc.) ; le cycle de vie du développement logiciel (*Software development lifecycle* - SDLC) ; les outils (disponibilité, utilisable, conformité, etc.).
Ces facteurs ont un impact sur la stratégie de test, les techniques, l'automatisation et le niveau de détail des outils de test.

**Outils de test (*testware*)** : Produits de travail générés par les activités de test. Ils doivent être soumis à une gestion de configuration appropriée pour assurer la cohérence et l'intégrité des produits de travail. Des exemples de produits de travail :
- **Plannification** : Plan de test, registre de risques, critères d'entrée et de sortie.
- **Surveillance et contrôle** : Rapports d'avancement des tests, documentation des directives de contrôle et information sur les risques.
- **Analyse** : Conditions de test et rapports de défauts sur la base des défauts de la base de test.
- **Conception** : Cas de test, chartes de test, exigences en données de test et en environnement de test.
- **Implémentation** : Procédures de test, scripts manuels et automatisés, suites de test, données de test, calendrier d'exécution de test et éléments d'environnement de test (bout de code, pilotes, simulateurs et virtualisation des services).
- **Exécution** : Journaux de test (*test logs*) et rapports de défauts.
- **Produit finaux** : Rapport de fin de test et évaluer les leçons apprises et demandes de changement.

Ces activités peuvent se chevaucher ou être réalisées en parallèle dans certaines méthodologies.

**Traçabilité** : L'établissement et le maintien de la tracabilité entre les éléments de la **base de test** (e.g., exigences) et les **outils de test** (e.g., cas de test, résultats, risques) sont essentiels pour la surveillance et le contrôle des tests. Une bonne tracabilité permet d'évaluer la couverture du test, de déterminer l'impact des modifications, de faciliter les audits et de communiquer l'état des éléments de la base de test aux parties prenantes.

**Rôles** :
- **Rôle de gestion du test (*test management role*)** : Responsabilité globale du processus de test, de l'équipe et du leadership. Se concentre sur la planification, la surveillance, le contr^le et l'achèvement.
- **Rôle de testeur (*testing role*)** : Responsabilité technique (*engineering*) du test. Se concentre sur l'analyse, la conception, l'implémentation et l'exécution.

Selon le contexte, ces rôles peuvent être assumés par différentes personnes ou par une seule personne à la fois.

## 1.5 Compétences essentielles et bonne pratiques de test.

**Compétences génériques** :
- Connaissances des tests.
- Rigueur, curiosité, attention protée aux détails.
- Bonnes compétences en communication, écoute active, esprit d'équipe.
- Pensée analytique, pensée critique, créativité.
- Connaissances technique et connaissance du domaine.

**Approche d'équipe globale** : Cette approche, issue de l'*extreme programming*, implique que tout membre de l'équipe ayant des compétences nécssaires peut effetuer n'importe quelle tâche, et que chacun est responsable de la qualité. Elle favorise la communication, la collaboration et permet aux testeurs de transférer leurs connaissances aux autres membres.

**Indépendance des tests** : Un certain degré d'indépendance augmente l'éfficacité pour trouver des défauts en raison de biais cognitifs différents de ceux de l'auteur du code. L'indépendance peut varier du test effectué par l'auteur lui-même, au test par des entités externes à l'organisation. Les **avantages** incluent une meilleure reconnaissance des défaillances et la remise en question des hypothèses. Les **inconvénients** potentiels sont le risque d'isolement des testeurs, les problèmes de communication et la perte du sentiment de responsabilité de qualité chez les développeurs.

:white_check_mark:**Synthèse**
- Tester = *Exposer des défauts**. Ce n'est pas démontrer qu'il n'y en a pas.
- Le test est **nécessaire** pour réduire les risques, garantir la qualité du produit final et fournir de l'information pertinentes aux partie prenantes.
- Les **7 principes** de test fixent le cadre de réflexion autour du test logiciel.
- Le processus de test comporte 5 grandes activités (planifier, analyser/concevoir, implémenter/exécuter, évaluer/rapporter et clôturer).
- *Testware* (outils de test) = tout ce qui est produit par et pour le test.
- Le testeur doit avoir des compétences techniques, analytiques, collaboratives et de communication.