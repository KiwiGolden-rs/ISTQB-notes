# Chapitre 2 - Le test tout au long du cycle de vie du développement logiciel (*SDLC*)

## Objectifs d'apprentissage
Comprendre la manière dont le test est intégré dans les différentes approches de développement, les concepts des approches *test-first* (tester en premier), le contexte DevOps, les différents niveaux de test, les types de test et le test de maintenance.

## 2.1 Le test dans le contexte d'un cycle de vie de développement logiciel (SDLC)

**Impact du SDLC sur les tests** :
- Modèle de **cycle de vie de développement logiciel** = Représentation abstraite des phases de développement et de relation logique et chronologique entre ces phases.
  - Exemples de modèles : Séquentiels (e.g., cascade, V) ; itératifs (e.g., spiral, prototypage), incrémentaux (e.g., Unified Process)
- Le Choix du SDLC a plusieurs **impactes** :
  - La portée et le moment des activités de test.
  - Le niveau de détail de la documentation de test
  - Le choix des techniques de test et de l'approche de test.
  - L'étendue de l'automatisation des test.
  - Le rôle et les responsabilités d'un testeur.
  - Exemple : Dans un modèle **séquentiel**, les testeurs sont souvent impliqués dans les **revues des exigences**, l'**analyse** et la **conception** des test dès les **premières phases**. L'éxecution dynamique des tests ne peut typiquement pas débuter trop tôt car le code exécutable arrive tard.

**SDLC et bonnes pratiques de test** :
Quel que soit le modèle :
- Chaque activité de développement doit avoir une activité de test correspondante.
- Les différents niveaux de test doivent avoir des objectifs spécifiques pour assurer une couverture adaptée tout en évitant les redondances.
- L'analyse et la conception des test doivent commencer dès la phase de développement correspondante (principe du **test précoce**).
- Les testeurs doivent être impliqués dans la **revue des produits de travail** dès qu'ils sont disponibles (même sous forme de brouillon) pour soutenir l'approche *shift left*.

**Le test comme moteur du développement logiciel** :
- Les approches de développement *test-first* :
  - **Test-Driven Development (TDD)** : Dirige le codage par des cas de test écrits avant le code.
  - **Acceptance Test-Driven Development (ATDD)** : Dérive les tests à partir des critère d'acceptation dans le cadre de la conception du système.
  - **Behavior-Driven Development (BDD)** : Exprime le comportement souhaité avec des cas de test rédigés dans un langage naturel simple (format *Given/When/Then*).
- Ces approches placent les tests **au coeur du développement logiciel** et changent le rôle du testeur et la planification des activité de test.

**DevOps et test** : DevOps est une approche organisationnelle qui vise la synergie entre le développement (dont le test) et les opérations.
- Le test doit s'adapter en termes de **rythme**, d'**automatisation** et de **retour rapide**.
- Les tests doivent être **intégrés à la chaîne CI/CD** (Intégration Continue / Déploiment Continue), avec un fort accent sur l'**automatisation**, le **retour rapide** et l'**amélioration continue**.
- Le rôle du testeur devient plus **collaboratif**, aligné avec les développeurs et les opérations (rôles moins séparés).
- **Bénéfices** : Retour rapide sur la qualité du code, promotion du *shift left*, facilitation d'environnements de test stables (via CI/CD), augmentation de la visibilité sur les caractéristiques non fonctionnelles (e.g., performance, fiabilité) et minimisation du risque de regréssion par l'automatisation.
- **Risques/Défis** : La définition et l'établissement du pipeline de livraison DevOps, l'introduction et la maintenance des outils CI/CD et la nécéssité de tests manuels malgré l'automatisation élevée.

**Shift Left** : Le *shift left* est l'application du principe de **test précoce**. Il s'agit d'effectuer les test plus tôt dans le SDLC, sans négliger les test ultérieurs.
- L'approche *shift left* signifie déplacer les activités de test plus tôt dans le SDLC (phases de conception ou de développement).
- Permet de détecter des défauts plus tôt et de réduire les coûts de correction, d'améliorer la qualité globale.
- Pour mettre en oeuvre le *shift left* : impliquer les testeurs dès les phases d'exigences/conception, automatiser les tests, déclencher des révisions et tests très tôt.
- Revue des spécifications par les testeurs, écriture des cas de test avant le codage, utilisation de la CI/CD, analyse statique du code source avant les tests dynamiques et démarer les tests non fonctionnels au niveau du test composant.

**Rétrospectives et amélioration des processus** : Les rétrospectives sont des réunions où les participants discutent de ce qui a réussi et de ce qui pourrait être amélioré, afin d'incorporer ces leçons dans le futur.
- Les rétrospectives sont utilisées comme **mécanisme d'amélioration continue du processus de test**.
- Elles permettent de revoir ce qui a bien/mal fonctionné, d'identifier des **opportunités d'amélioration** et d'ajuster les activités de test dans les itérations ou version suivantes.

## 2.2 Niveaux de test et types de test

**Niveaux de test (*test levels*)** : Les niveaux de test sont des groupes d'activités de test liées à une phase donnée du développement.
- Les niveaux typiques :
  - **Test de composant (*Unit testing*)** : Vise les composants isolément, souvent effectué par les développeurs.
  - **Test d'intégration de composants** : Vise les interfaces et intéractions entre composants.
  - **Test système** : Vise le comportement global et les capacités d'un système complet, incluant les tests fonctionnels de bout en bout et les tests non fonctionnels.
  - **Test d'intégration système** : Vise les interfaces du système testé avec d'autres systèmes et services externes, nécessitant des environnements de test représentatifs.
  - **Test d'acceptation** : Vise la validation et la démonstration de la préparation au déploiement (le système répond aux besoins de l'utilisateur).
- Chaque niveau se focalise sur une petite partie différente du logiciel ou de son intégration, et doit être planifié et exécuté avec des objectifs adaptés.

**Types de test (*test type*)** : Les types de test sont liés à des caractéristiques de qualité spécifiques et peuvent être appliqués à tous les niveaux.
- **Test fonctionnel** : Evalue ce que le système doit faire. Il vérifie que le logiciel fait ce qu'il doit faire (complétude, exactitude, adéquation).
- **Test non-fonctionnel** : Evalue comment le logiciel se comporte, en se concentrant sur des attributs tels que l'efficacité des performances, la compatibilité, l'utilisabilité, fiabilité, la sécurité, la maintenabilité, la portabilité et la sûreté (*ISO/IEC 25010 standard*).
- **Test boîte noire (*Black-box testing*)** : Dérive les tests à partir de la spécification, sans regarder la structure interne.
- **Test boîte blanche (*White-box testing*)** : Dérive les tests à partir de la structure interne ou de l'implémentation (e.g., code, architecture, flux de travail et flux de données).

**Test de confirmation et test de régression** :
- **Test de confirmation** : Exécution de test, précédement échoués, après correction pour **confirmer que le défaut est supprimé**.
- **Test de régression** : Confirme qu'un changement (e.g., un correctif) **n'a causé aucune conséquence indésirable sur les parties inchangées ou d'autres composants**. C'est un exéllent candidat pour l'**automatisation**.

## 2.3 Test de maintenance

Le test de maintenance intervient **après déploiement** du logiciel, lorsque celui-ci est en service et subit des modifications (correctives, adaptatives, amélioratives), des migrations ou le retrait du logiciel. Il évalue le succès du changement et vérifie les régréssions. La **portée du test** de maintenance dépend du **degré de risque** du changement, de la **taille du système existant** et de la **taille des changements**.

**Déclencheurs (*triggers*) du test de maintenance** :
- **Modifications** : Amélioration planifiées, modifications correctives ou correctifs urgents.
- **Mises à niveau ou Migrations** : Changements d'environnement opérationnel (e.g., plateforme), nécessitant des tests spécifiques au nouvel environnement ou des tests de conversion de données.
- **Retrait** : Nécessite des tests d'archivage et des procédures de restauration des données.

## :white_check_mark: Synthèse
- Le test est **intégré à tout le cycle de vie du développement logiciel (SDLC)** : pas uniquement après le développement du code.
- Le modèle de SDLC influence directement comment et quand les tests sont faits (temporalité, documentation, techniques, responsabilités).
- Que ce soit un modèle de développement séquentiel ou DevOps, il existe des **bonnes pratiques communes** (impliquer tôt les testeurs, correspondance développement-test, niveau de test bien définis).
- Les approches modernes (*test-first, shift left, DevOps*) permettent de tester plus tôt, renforcent l'automatisation, l'intégration continue et l'amélioration permanente.
- Il existe **plusieurs niveaux de test** (composant, intégration, système, acceptation) et **types de test** (fonctionnel, non-fonctionnel, boîte noire, boîte blanche) à maîtriser et distinguer.
- Le test de **maintenance** est une partie importante du SDLC : une fois le système en production, les activités de test continuent pour les changements, migrations et retrait.