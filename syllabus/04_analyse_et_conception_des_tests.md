# Chapitre 4 - Analyse et conception des tests

## 4.1 Aperçu des techniques de test

Les techniques de tests sont des outils qui assistent le testeur à la fois dans **l'analyse de test** (ce qu'il faut tester) et la **conception des tests** (comment tester). Elles permettent de développer de manière systématique un ensemble de cas de tests qui est à la fois **restreint** et **suffisant**. Elles aident également à définir les conditions de test, les éléments de couverture et les données de test nécessaires.

Les techniques de test sont classées en trois catégories principales :
- **Techniques de test boîte noire** (ou technique basées sur les spécifications) :
  - Elles sont fondées sur l'analyse du **comportement spécifié** de l'objet de test.
  - Elles sont utilisées **sans référence à la structure interne** de l'objet de test.
  - Les cas de test qui en découlent sont **indépendants de l'implémentation** du logiciel. Si l'implémentation change, mais que le comportement requis demeurs identique, les cas de test restent pertinents.
- **Techniques de test boîte blanche** (ou technique basée sur la structure) :
  - Elles reposent sur l'analyse de la **structure interne** et du traitement de l'objet de test.
  - Les cas de test **dépendent de la conception logiciel** et ne peuvent donc être créés qu'après que l'objet de test ait été conçu ou implémenté.
- **Techniques de test basées sur l'expérience** :
  - Elles exploitent efficacement les **connaissances et l'expérience des testeurs** pour la conception et l'implémentation des cas de test.
  - Leur efficacité est liée aux **compétences** du testeur.
  - Elles sont considérées comme complémentaires des techniques boîte noire et boîte blanche, car elles peuvent identifier des défauts que ces dernières techniques pourraient manquer.

## 4.2 Techniques de test boîte noire

Les techniques de test boîte noire couramment utilisées et présentées dans les sections suivantes sont :
- **Partitions d'équivalence**.
- **Analyse des valeurs limites**.
- **Test par tables de décisions**.
- **Test de transition d'état**.

**Partitions d'équivalence** :
- **Concept** : La technique des partitions d'équivalence divise les données en ensembles appelés **partitions d'équivalence**. Elle repose sur la théorie que si un cas de test utilisant une valeur d'une partition détecte un défaut, tout autre cas de test utilisant une valeur de cette même partition devrait détecter le même défaut. Par conséquent, un seul test pour chaque partition est suffisant.
- **Caractéristiques et type de partitions** : Les partitions d'équivalence peuvent être identifiées pour n'importe quel élément de données lié à l'objet de test, comme les entrées, les sorties, les éléments de configuration, les valeurs internes, les valeurs liées au temps et les paramètres d'interface. Ces partitions sont classées comme :
  - **Partition valide** : Contient des valeurs valides.
  - **Partition invalide** : Contient des valeurs invalides.
- **Couverture** : Les **partitions d'équivalence** sont considérées comme les **éléments de couverture**. Pour atteindre une **couverture de 100%**, il faut que les cas de test exercent toutes les partitions identifiées, y compris les partitions invalides, au moins une fois.
$$Couverture(\%) = (Partitions\ exercées\ /\ Total\ partitions\ identifiées)\ *\ 100$$
- **Cas complexes** : Dans les cas où l'objet de test comprend plusieurs ensembles de partitions (e.g., plusieurs paramètres d'entrée), le critère de couverture le plus simple est la **couverture *Each Choice***. Cette approche exige que les cas de test exercent chaque partition de chaque enssemble au moins une fois, mais elle **ne prend pas en compte les combinaisons** de partitions.

Deux exemples, un "simple" et un "complexe" :
- Champ "âge" dans un formulaire qui n'accepte qu'un âge compris entre 18 et 65 ans inclus.

| Partition | Description | Type |
|:----------|:-----------:|:-----|
| P1 | Âge < 18 | Invalide |
| P2 | 18 ≤ Âge ≤ 65 | Valide |
| P3 | Âge ≥ 65 | Invalide |

| Partition | Valeur testée | Résultat attendu |
|:----------|:-----------:|:-----|
| P1 | 13 | Rejeté |
| P2 | 40 | Accepté |
| P3 | 80 | Rejeté |

- Formulaire de connexion avec :
  - Champ 1 : Nom d'utilisateur (doit exister dans la base de donnée).
  - Champ 2 : Mot de passe (doit être correct).

| Partition | Valeur testée | Résultat attendu |
|:----------|:-----------|:-----|
| P1 | Chp 1 existe & Chp 2 correct | Accepté |
| P2 | Chp 1 existe & Chp 2 incorrect | Rejeté |
| P3 | Chp 1 n'existe pas & Chp 2 correct | Rejeté |
| P4 | Chp 1 n'existe pas & Chp 2 incorrect | Rejeté |

**Analyse des valeurs limites** :
- **Concept** : L'analyse des valeurs limites est basées sur l'exercice des **limites des partitions d'équivalence**. Elle n'est applicable qu'aux **partitions ordonnées**. Pour que cette technique s'applique, si deux éléments font partie d'une même partition, tous les éléments situés entre eux doivent également appartenir à cette partition.<br/>Cette technique est jugée efficace car les **développeurs sont plus suceptible de commettre des erreurs** lors de l'implémentation du logiciel au niveau des limites de partitions. Les défauts typiques découverts par cette analyse sont liés à des limites implémentées qui sont incorrectement décalées (supérieures ou inférieures à celle prévues) ou complètement omises.
- **Deux versions de la technique** :
  - **Technique à 2 valeurs** :
    - Pour chaque valeur limite, on identifie **deux éléments de couverture**.
    - Ces éléments sont la **valeur limite en question** et sa **voisine la plus proche** appartenant à la partition adjacente.
    - Pour atteindre une couverture de **100%**, les cas de test doivent exercer toutes les valeurs limites identifiées.
  - **Technique à 3 valeurs** :
    - Pour chaque valeur limite, on identifie **trois éléments de couverture**.
    - Ces éléments sont **la veleur limite en question** et ses **deux voisines**.
    - Certains de ces éléments de couverture peuvent donc ne pas être des valeurs limites elles-mêmes.
    - La technique à 3 valeurs est considérée comme **plus rigoureuse** que celle à 2 valeurs. Par exemple, elle peut détecter un défaut d'implémentation (comme une condition "si(x ≤ 10)..." incorrectement codée en "si (x=10)...") en utilisant la voisine interne (x=9), ce que la technique à 2 valeurs pourrait manquer.
    - Pour atteindre une couverture de **100%**, les cas de test doivent exercer toutes les valeurs limites identifiées ainsi que leurs voisines.

```math
Couverture(\%) = (Valeurs\ limites\ exercées\ /\ Total\ valeurs \ limites \ identifiées)\ *\ 100
```

**Test par tables de décisions** :
- **Concept** : Les tables de décision sont utilisées pour tester l'implémentation des éxigences du système qui spécifient la manière dont différentes **combinaisons de condition** aboutissent à des résultats variés. Elles constituent un moyen efficace d'enregistrer une logique complexe, en particulier les **règles de gestion** (ou règle métier).
- **Structure et création des tables** : Lors de la construction d'une table de décision, les **conditions** et les **actions** résultantes du système sont définies et forment les lignes de la table. Chaque **colonne** correspond à une **règle de décision**, définissant une combinaison unique de conditions et les actions associées.<br/>Il existe deux types de tables de décision :
  - **Tables à entrée limitée** : Où les valeurs des conditions et des actions sont présentées sous forme de valeurs booléennes (vrai ou faux).
  - **Tables à entrée étendue** : Où tout ou partie des conditions et des actions peuvent prendre des valeurs multiples (comme des plages de nombres, des partitions d'équivalence ou des valeurs discrètes).
- La notation utilisée pour les conditions est "V" (vrai) ou "F" (faux). Le symbole "-" indique que la valeur de la condition n'est **pas pertinentes** pour le résultat, et "N/A" indique que la condition est **irréalisable** pour une règle donnée. Pour les actions, "X" signifie que l'action doit avoir lieu, et un blanc signifie qu'elle ne doit pas se produire.
- Une table de décision complète couvre toutes les combinaisons de conditions, mais elle peut être simplifiée en retirant les colonnes correspondant à des combinaisons irréalisable. Elle peut aussi être minimisé en fusionnant les colonnes où certaines conditions n'affectent pas le résultat.
- **Couverture** : Les **éléments de couverture** sont les **colonnes contenant les combinaisons de conditions réalisables**. Pour atteindre **100%**, les cas de test doivent exercer toutes ces colonnes réalisable.<br/>
  ```math
  Couverture(\%) = (Colonnes\ exercées\ /\ Total\ colonnes\ réalisables)\ *\ 100
  ```
- **Avantages et limites** : La force du test par tables de décisions est qu'il frounit une approche systématique pour identifier toutes les combinaisons de conditions, permettant de trouver des lacunes ou des contradictions dans les exigences qui pourraient être négligées autrement. Cependant, si les conditions sont nombreuses, le nombre de règles croît de manière exponentielle, ce qui peut rendre l'exercice de toute les règles très long. Dans de tels cas, l'utilisation d'une table de décision réduite ou d'une approche basée sur les risques est recommandées.
- Exemple avec le formulaire de connexion :

| Condition/Action | Règle 1 | Règle 2 | Règle 3 | Règle 4 |
|:-----------------|:-------:|:-------:|:-------:|:-------:|
| Utilisateur enregistré | V | V | F | F |
| Mot de passe correcte | V | F | V | F |
| Autoriser l'accès | X |  |  |  |

**Test de transition d'état** :
- **Concept** : Cette technique utilise un **diagramme de transition d'états** pour modéliser le comportement d'un système en affichant ses **étapes possibles** et ses **transitions d'états valides**.
  - Transition : Une transition est initiée par un **évènement**, lequel peut être précisé par une **condition de garde**. Les transitions sont supposées être instantanées et peuvent générer une **action du logiciel**. La syntaxe courante est : "évènement [condition de garde] / action".
  - **Table d'états** : C'est un modèle équivalent au diagramme de transition d'états. Ses lignes représentent les **états** et ses colonnes représentent les **évènements** (et les conditions de garde si elles existent). Les cellules de la table représentent les transitions et contiennent l'état cible ainsi que les conditions de garde et les actions, le cas échéant. Les **transitions non valide** sont montrées explicitement par des cellules vides.
  - **Cas de test** : Un cas de test est généralement une **séquence d'évènements** qui produit une séquence de changement d'état (et d'action). Un cas de test peut, et ces souvent le cas, couvrir plusieurs transitions d'états.
- **Couverture** : Trois exemples de critères de couverture :
  - **Couverture de tous les états** :
    - Les **états** sont les éléments de couverture.
    - L'objectif de 100% de couverture est atteint lorsque les cas de test garantissent que **tous les états sont visités**.
    - C'est la couverture **la plus faible**, car elle peut être obtenue sans exercer toutes les transitions.
  - **Couverture des transitions valides** (ou couverture *0-switch*) :
    - Les **transitions valides uniques** sont les éléments de couverture.
    - L'objectif de 100% de couverture est atteint lorsque les cas de test **exercent toutes les transitions valides**.
    - Ce critère est le **plus largement utilisé** et son obtention garantit une couverture complète de tous les états.
  - **Couverture de toutes les transitions** :
    - Les éléments de couverture sont **toutes les transitions** figurant dans la table d'état.
    - L'objectif de 100% de couverture est atteint lorsque les cas de test exercent **toutes les transitions valides** et **tentent d'exécuter des transitions non valides**.
    - Pour éviter le **masquage des défauts** (un défaut empêchant la détection d'un autre), il faut tester qu'une seul transition non valide dans un seul cas de test.
    - Cette couverture garantit la couverture de tous les états et des transitions valides. Elle est considérée comme une **exigence minimal** pour les logiciels critiques en termes de mission et de sécurité.
    - Quel que soit le critère, la couverture se calcul :
    ```math
    Couverture(\%) = (Elements\ de\ couverture\ exercées\ /\ Total\ éléments\ de\ couverture)\ *\ 100
    ```

## 4.3 Techniques de test boîte blanche

Cette section se concentre sur deux techniques de teste boîte blanche liées au code :
- **Le test des instructions**.
- **Le test des branches**.

**Test des instructions et couverture des instructions** : 
- **Concept** : Dans le cadre du test des instructions, les éléments de couverture sont définis comme les **instructions exécutables** du code. L'objectif de cette technique est de concevoir des cas de test qui exercent ces instructions jusqu'à ce qu'un niveau de couverture acceptable soit atteint.
- **Couverture** : Lorsqu'une **couverture des instructions de 100%** est atteinte, cela signifie que toutes les instructions exécutables du code ont été testées au moins une fois. Théoriquement, l'exécution d'une instruction contenant un défaut peut provoquer une défaillance, ce qui démontre la présence du défaut.<br/> 
  ```math
  Couverture(\%) = (Instructions\ exercées\ /\ Total\ instructions\ exécutables)\ *\ 100
  ```
  - **Limites de la couverture de instructions** : Cependant, l'exécution d'une instruction ne permet pas de détecter les défauts dans tous les cas.
    - Elle peut ne pas détecter les défauts qui dépendent des **données** (e.g., une division par zéro qui ne se produit que lorsque le dénominateur est égal à zéro).
    - Une couverture des instruction à 100% **ne garantit pas que toutes la logique de décision a été testée**, car toutes les branches du code n'auront pas nécessairement été exercées.

**Test des branches et couverture des branche** :
- **Concept** :
  - Une **branche** est définie comme un transfert de contrôle qui se produit entre deux noeuds dans le graphe de flux de contrôle. Ce transfert peut être inconditionnel (code en ligne droite) ou conditionnel (résultat de décision).
  - Dans le test des branches, les **branches** sont les **éléments de couverture**. L'objectif est de concevoir des tests qui exercent ces branches jusqu'à ce qu'un niveau de couverture acceptable soit atteint.
- **Couverture** :
  - Atteindre une **couverture des branches de 100%** assure que toutes les branches du code sont exercées, qu'elles soient conditionnelles (e.g., résultat vrai ou faux d'une décision "if...then" ; résultat d'une instruction "switch/case" ; une décision de boucle) ou inconditionnelles.
  - La **couverture des branches englobe la couverture des instructions**. Cela signifie que si un ensemble de cas de test atteint 100% de couverture des branches, il atteint également 100% de couverture des instructions (mais l'inverse n'est pas vrai). Cependant, même à 100% cette technique peut ne pas détecter les défauts nécessitant l'exécution d'un chemin spécifique dans le code.
```math
Couverture(\%) = (Branches\ exercées\ /\ Total\ branches)\ *\ 100
```

**La veleur des test boîte blanche** :
- **Force fondamentale** : Une force fondamentale partagée par toutes les techniques de test boîte blanche est qu'elles prennent en compte l'**implémentation entière du logiciel** pendant le test. Cela permet de faciliter la détection des défauts, même lorsque la spécification du logiciel est **vague, obsolète ou incomplète**.
- **Faiblaisses** : Cependant, les tests boîte blanche présentent une faibless : si le logiciel n'implémente pas une ou plusieurs exigences (c'est à dire s'il y a des omissions), les tests boîte blanche pourraient ne pas détecter les défauts résultant de ces omissions.
- **Application et couverture** :
  - Les techniques boîte blanche peuvent être utilisées dans le cadre des **tests statiques** (e.g., lors d'une exécution à blanc du code).
  - Elles sont bien adaptées pour la revue de code qui n'est pas encore prêt à être exécuté.
  - Elles peuvent également être appliquées au pseudocode et aux logiques de haut niveau modélisées à l'aide d'un graphe de flux de contrôle.
  - Se consacrer uniquement aux tests boîte noire ne permet pas de mesurer la couverture réelle du code. Les mesures de couverture boîte blanche fournissent une **mesure objective de la couverture** et donnent les informations nécessaires pour générer des tests supplémentaires afin d'augmenter cette couverture. En augmentant la couverture, on accroît la confiance dans le code.

## 4.4 Techniques de test basées sur l'expérience

Les techniques basées sur l'expérience, couramment utilisées et abordées dans les sections suivantes, sont :
- **Estimation d'erreurs**.
- **Test exploratoire**.
- **Test basé sur des checklists**.

**Estimation d'erreurs** :
- **Concept** : L'estimation d'erreurs est une technique utilisée pour **anticiper** l'apparition d'erreurs, de défauts et de défaillances. Cette anticipation est basée sur les connaissances et l'expérience du testeur. Ces connaissances incluent :
  - La manière dont l'application s'est comportée par le passé.
  - Les types d'erreurs que les développeurs ont tendance à commettre et les défauts qui en résultent.
  - Les types de défaillances qui se sont produites dans d'autres applications similaires.
- **Types de problèmes anticipés** : Les erreurs, défauts et défaillances anticipés peuvent être liés à :
  - L'**entrée** (e.g., entrée correcte non acceptée, paramètres erronés ou manquants).
  - La **sortie**(e.g., format incorect, résultat erroné).
  - La **logique** (e.g., cas manquants, opérateur incorrect).
  - Le **calcul** (e.g., opérande incorrect, calcule erroné).
  - Les **interfaces** (e.g., non-concordance des paramètres, types incompatible).
  - Les **données** (e.g., initialisation incorrecte, type incorrect).
- **Les attaques de fautes** : Une approche méthodique pour mettre en oeuvre l'estimation d'erreurs est l'utilisation des **attaques de fautes** (*fault attacks*). Cette technique exige que le testeur :
  - Crée ou acquière une liste d'erreurs, de défauts et de défaillances possibles.
  - Conçoive des tests qui identifieront les défauts associés aux erreurs, exposeront les défauts ou provoqieront les défaillances.
  - Ces listes peuvent être établies sur la base de l'expérience, des données relatives aux défauts et aux défaillances, ou des connaissances communes sur les raisons des défaillances, ou des connaissances communes sur les raisons des défaillances des logiciels.

**Test exploratoire** :
- **Concept** : Dans le test exploratoire, la conception, l'exécution et l'évaluation des tests se font **simultanément** pendant que le testeur découvre l'objet de test. L'objectif est d'en apprendre davantage sur cet objet, de l'explorer plus en profondeur avec des tests ciblés et de créer des tests pour les domaines qui n'ont pas encore été testés.
- **Structure par sessions** : Le test exploratoire est parfois structuré au moyen de l'approche du **test basé sur des sessions**. Dans cette approche :
  - Les tests exploratoires sont menés dans un **laps de temps défini**.
  - Le testeur utilise une **charte de test** contenant des objectifs pour guider l'activité.
  - Les objectifs de test peuvent être traités comme des **conditions de test de haut niveau**.
  - Les **éléments de couverture** sont identifiés et exercés pendant la session de test.
  - La session est généralement suivie d'un **débriefing**, impliquant une discussion entre le testeur et les parties prenantes intéressées par les résultats.
  - Le testeur peut utiliser des **formulaires de session de test** pour documenter les étapes et les découvertes.
- **Application et efficacité** : Le test exploratoire est particulièrement utile dans les scénarios où les **spécifications sont peu nombreuses ou inadéquates**, ou lorsque l'équipe est soumise à une **forte pression de temps**. Il sert également à **compléter d'autres techniques de test plus formelles**. Pour être efficace, le test exploratoire exige que le testeur soit **expérimenté** et possède des **connaissances essentielles**, comme l'esprit d'analyse, la curiosité et la créativité. Cette technique peut intégrer l'utilisation d'autres techniques de test, telles que les partitions d'équivalence.

**Test basé sur des checklists** :
- **Concept** : Dans le test basé sur des checklists, le testeur conçoit, implémente et exécute des tests dont le but est de couvrir les **conditions de test répertoriées dans une checklist**. Les checklists peuvent être élaborées à partir de diverses sources, notamment :
  - L'**expérience** du testeur.
  - La connaissance de ce qui est important pour l'**utilisateur**.
  - La compréhension des raisons et des mécanismes des **échecs logiciels**.
  - Des **heuristiques** connues, comme les 10 heuristiques pour les tests d'utilisabilité (Nielsen 1994), qui soutiennent différents types de tests, y compris fonctionnels et non fonctionnels.
- **Structure et contenu** : Les éléments d'une checklist sont souvent formulés sous forme de **questions**. Chaque élément de la checklist doit pouvoir être vérifié **séparément et directement**. Ces éléments peuvent faire référence à des exigences, à des propriétés d'interface graphique, à des caractéristiques-qualité ou à d'autres formes de conditions de test.
- **Lignes directrices et maintenance** : Les checklists ne doivent **pas contenir** :
  - Des éléments qui peuvent être vérifiés automatiquement.
  - Des éléments qui correspondent davantage à des critères d'entrée ou de sortie.
  - Des éléments trop généraux.

  Les développeurs apprennent à éviter de commetre les mêmes erreurs, certaines entrées de la checklist peuvent progressivement devenir **moins efficaces** au fil du temps. Il peut donc être nécessaire d'ajouter de nouvelles entrées pour tenir compte des défauts de sévérité élevée récemment trouvés. Par conséquent, les checklists doivent être **régulièrement mises à jour** sur la base de l'analyse des défauts. Il est important de veiller à ce que la checklist ne devienne pas exessivement longue.
- **Cohérence et répétabilité** : Lorsque des cas de test détaillés sont absents, le test basé sur des checklists fournit des **lignes directrices** et assure un certain degré de **cohérence** pour les tests. Toutefois, si les checklists sont de haut niveau, il est probable qu'il y ait une certaine variation dans les tests effectivement menés, ce qui peut se traduire par une **couverture potentiellement plus grande** mais une **répétabilité moindre**.

## 4.5 Approches de test basées sur la collaboration

Chacune des techniques susmentionnées a un objectif particulier en ce qui concerne la détection des défauts. Les approches basées sur la collaboration, en revanche, se concentrent également sur l'évitement des défauts par la collaboration et la communication.

**Rédaction collaborative de *User Stories*** : Une ***User Story*** (scénario utilisateur) représente une caractéristique qui sera utile à l'utilisateur ou à l'acheteur d'un système ou d'un logiciel.
Les *User Stories* possèdent trois aspects fondamentaux, appelés ensemble les "**3 C**" :
- **Carte** : Le support physique ou électronique décrivant la *User Story* (e.g., carte d'index, une entrée dans un tableau électronique).
- **Conversation** : Elle explique comment le logiciel sera utilisé (peut être documentée ou verbale).
- **Confirmation** : Elle correspond aux critères d'acceptation.

Le format le plus courant pour rédiger une *User Story* est : "En tant que **[rôle]**, je veux que **[objectif à atteindre]**, afin de pouvoir **[valeur métier résultante pour le rôle]**", ce qui est ensuite suivi des critères d'acceptation.

La rédaction collaborative peut faire appel à des techniques comme le **brainstorming** et la **cartographie mentale**. L'intérêt majeur de cette collaboration est qu'elle permet à l'équipe d'obtenir une **vision commune** de ce qui devrait être livré en intégrant les trois perspectives clés : celle du **métier**, celle du **développement** et celle du test.

Pour garantir leur qualité, les bonnes *User Stories* doivent respecter le critère **INVEST** (Indépendantes, Négociables, apportant de la Valeur, Estimables, Petites et Testables). Si une partie prenante éprouve des difficulté à définir la manière de tester une *User Story*, cela peut indiquer qu'elle n'est pas assez claire, qu'elle ne reflète pas une valeur valable, ou que la partie prenante a besoin d'aide pour le test.

**Critères d'acceptation** :
- **Définition et rôle** : Les critères d'acceptation d'une *User Story* représentent les **conditions** que l'implémentation de cette *User Story* doit remplir pour être acceptée. Ils découlent généralement de la phase de **conversation** (l'un des "3 C" des *User Story*). D'un point de vue pratique, ces critères sont considérés comme les **conditions de test** qui doivent être vérifiées par les tests.
- **Utilisation des critères d'acceptation** : Ces critères sont essentiels pour plusieurs activités du projet :
  - Définir clairement le **périmètre** de la *User Story*.
  - Obtenir un **concensus** entre toutes les parties prenantes.
  - Décrire les scénarios attendus, qu'ils soient **positifs ou négatifs**.
  - Servir de base aux **tests d'acceptation des utilisateurs**.
  - Permettre une **planification et une estimation précises** du travail nécessaire.

  Il existe plusieurs façons de documenter ces critères. Les deux formats les plus courants :
  - **Orienté-scénario** : Ce format utilise souvent la structure ***Given/When/Then*** (Etant donné/Lorsque/Alors), couramment employée par le développement piloté par le comportement (BDD).
  - **Orienté vers les règles** : Ce format peut être présenté sous forme de **liste de vérification à puce** ou de **tableau de correspondance entrée-sortie**.

  L'équipe a également la possibilité d'utiliser un format **personnalisé**, à condition que les critères d'acceptation restent **bien définis et sans ambiguîté**.

**Développement piloté par les tests d'acceptation (ATDD)** :
- **Principes** : L'ATDD est une approche pilotée par les tests. Les cas de test sont **créés avant d'implémenter la *User Story***. Ces cas de test sont élaborés par des membres de l'équipe ayant des perspectives variées, notamment les **clients**, les **développeurs** et les **testeurs**. Ils peuvent être exécutés manuellement ou de manière automatisée.
- **Processus de mise en oeuvre** :
  - **Atelier de spécification (Première étape)** : Cette étape cruciale implique les membres de l'équipe qui analysent, discutent et rédigent la *User Story* ainsi que ses critères d'acceptation (s'ils ne sont pas encore définis). L'atelier vise à **résoudre les lacunes, les ambiguïtés ou les défauts** de la *User Story*.
  - **Création des cas de test (Seconde étape** : Les cas de test sont ensuite créés par l'équipe ou individuellement par le testeur. Ces cas sont **basés sur les critères d'acceptation** et son considérés comme des exemples du fonctionnement du logiciel. En général, les termes "exemples" et "tests" sont utilisés de manière interchangeable dans ce contexte. Ces tests aident l'équipe à implémenter correctement la *User Story*.
  - **Application des techniques de test** : Lors de la conception des tests, les autres techniques de test (boîte noire, boîte blanche, basées sur l'expérience) peuvent être appliquées.
  - **Développement des cas de test** :
    - **Tests positifs et négatifs** : Les premiers cas de test sont généralement **positifs**, confirmant le comportement correct sans conditions d'erreur ou exception, et couvrent la séquence d'activités exécutées si tout se passe comme prévu. Une fois ces cas réalisés, l'équipe doit effectuer des **tests négatifs**.
    - **Caractéristiques non fonctionnelles** : L'équipe doit également couvrir les **caractéristiques non fonctionnelles** (e.g., l'efficacité de la performance et l'utilisabilité).
    - **Format et contenu** : Les cas de test doivent couvrir toutes les caractéristiques de la *User Story* sans la dépasser, ni décrire les mêmes caractéristiques (uniques et non redondantes).
    - **Automatisation** : Lorsque les cas de test sont définis dans un format pris en charge par un *framework* d'automatisation des tests, les développeurs peuvent automatiser ces cas en écrivant le code correspondant au fur et à mesure de l'implémentation de la caractéristique. Dans ce cas, les tests d'acceptation deviennent des **exigences exécutables**.

## :white_check_mark: Synthèse

Ce chapitre présente les **techniques de conceptions de tests**, utilisées pour transformer la base de test (exigence, spécifications, code, etc.) en **conditions**, **cas** et **procédures de test**.
Il distingue trois catégories principales:
- Les **techniques boîte noire**, fondées sur le comportement attendu du système (e.g., partitions d'équivalence, valeurs limites, tables de décision, transitions d'état).
- Les **techniques boîte blanche**, basées sur la structure interne du code (e.g., couverture des instructions, des branches, des conditions).
- Les **techniques fondées sur l'expériences**, reposant sur l'intuition, l'historique des défauts ou l'expertise du testeur.

Le chapitre explique comment ces techniques permettent d'assurer une **couverture optimale** du système testé, d'**améliorer la qualité** et de **prioriser les efforts de test**.
Il met également l'accent sur les **aproches de test collaboratives**, où testeurs, développeurs et parties prenantes conçoivent ensemble les test afin de partager la compréhension du système, réduire les anbiguïtés et renforcer la détection précoce des défaut.