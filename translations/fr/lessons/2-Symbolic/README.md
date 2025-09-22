<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "98c5222ff9556b55223fed2337145e18",
  "translation_date": "2025-08-24T20:58:26+00:00",
  "source_file": "lessons/2-Symbolic/README.md",
  "language_code": "fr"
}
-->
# Représentation des connaissances et systèmes experts

![Résumé du contenu de l'IA symbolique](../../../../translated_images/ai-symbolic.715a30cb610411a6964d2e2f23f24364cb338a07cb4844c1f97084d366e586c3.fr.png)

> Sketchnote par [Tomomi Imura](https://twitter.com/girlie_mac)

La quête de l'intelligence artificielle repose sur une recherche de connaissances, pour comprendre le monde de manière similaire aux humains. Mais comment peut-on s'y prendre pour y parvenir ?

## [Quiz avant le cours](https://ff-quizzes.netlify.app/en/ai/quiz/3)

Aux débuts de l'IA, l'approche descendante pour créer des systèmes intelligents (discutée dans la leçon précédente) était populaire. L'idée était d'extraire les connaissances des humains dans un format lisible par une machine, puis de les utiliser pour résoudre automatiquement des problèmes. Cette approche reposait sur deux grandes idées :

* Représentation des connaissances
* Raisonnement

## Représentation des connaissances

Un des concepts importants de l'IA symbolique est la **connaissance**. Il est essentiel de différencier la connaissance de l'*information* ou des *données*. Par exemple, on peut dire que les livres contiennent des connaissances, car on peut les étudier et devenir expert. Cependant, ce que les livres contiennent est en réalité appelé *données*, et en lisant les livres et en intégrant ces données dans notre modèle du monde, nous transformons ces données en connaissances.

> ✅ **La connaissance** est quelque chose qui se trouve dans notre tête et représente notre compréhension du monde. Elle est obtenue par un processus actif d'**apprentissage**, qui intègre les informations reçues dans notre modèle actif du monde.

Le plus souvent, nous ne définissons pas strictement la connaissance, mais nous l'alignons avec d'autres concepts connexes en utilisant la [pyramide DIKW](https://fr.wikipedia.org/wiki/Pyramide_DIKW). Elle contient les concepts suivants :

* **Données** : quelque chose représenté sur un support physique, comme un texte écrit ou des mots prononcés. Les données existent indépendamment des êtres humains et peuvent être transmises entre eux.
* **Information** : la manière dont nous interprétons les données dans notre esprit. Par exemple, lorsque nous entendons le mot *ordinateur*, nous avons une certaine compréhension de ce que c'est.
* **Connaissance** : l'information intégrée dans notre modèle du monde. Par exemple, une fois que nous apprenons ce qu'est un ordinateur, nous commençons à avoir des idées sur son fonctionnement, son coût et ses usages. Ce réseau de concepts interconnectés forme notre connaissance.
* **Sagesse** : un niveau supplémentaire de compréhension du monde, représentant une *méta-connaissance*, c'est-à-dire une notion sur la manière et le moment d'utiliser les connaissances.

*Image [de Wikipédia](https://commons.wikimedia.org/w/index.php?curid=37705247), par Longlivetheux - Travail personnel, CC BY-SA 4.0*

Ainsi, le problème de la **représentation des connaissances** consiste à trouver un moyen efficace de représenter les connaissances dans un ordinateur sous forme de données, afin de les rendre utilisables automatiquement. Cela peut être vu comme un spectre :

![Spectre de la représentation des connaissances](../../../../translated_images/knowledge-spectrum.b60df631852c0217e941485b79c9eee40ebd574f15f18609cec5758fcb384bf3.fr.png)

> Image par [Dmitry Soshnikov](http://soshnikov.com)

* À gauche, il y a des types très simples de représentations des connaissances qui peuvent être efficacement utilisés par les ordinateurs. Le plus simple est l'algorithmique, où les connaissances sont représentées par un programme informatique. Cependant, ce n'est pas la meilleure façon de représenter les connaissances, car ce n'est pas flexible. Les connaissances dans notre tête sont souvent non algorithmiques.
* À droite, il y a des représentations comme le texte naturel. C'est la plus puissante, mais elle ne peut pas être utilisée pour un raisonnement automatique.

> ✅ Réfléchissez un instant à la manière dont vous représentez les connaissances dans votre tête et les convertissez en notes. Y a-t-il un format particulier qui fonctionne bien pour vous et facilite la rétention ?

## Classification des représentations des connaissances informatiques

Nous pouvons classer les différentes méthodes de représentation des connaissances informatiques dans les catégories suivantes :

* **Représentations en réseau** : elles se basent sur le fait que nous avons un réseau de concepts interconnectés dans notre tête. Nous pouvons essayer de reproduire ces réseaux sous forme de graphe dans un ordinateur - un **réseau sémantique**.

1. **Triplets Objet-Attribut-Valeur** ou **paires attribut-valeur**. Puisqu'un graphe peut être représenté dans un ordinateur comme une liste de nœuds et d'arêtes, nous pouvons représenter un réseau sémantique par une liste de triplets contenant des objets, des attributs et des valeurs. Par exemple, nous construisons les triplets suivants sur les langages de programmation :

Objet | Attribut | Valeur
------|----------|-------
Python | est | Langage-Non-Typé
Python | inventé-par | Guido van Rossum
Python | syntaxe-bloc | indentation
Langage-Non-Typé | n'a pas | définitions de types

> ✅ Réfléchissez à la manière dont les triplets peuvent être utilisés pour représenter d'autres types de connaissances.

2. **Représentations hiérarchiques** : elles mettent en avant le fait que nous créons souvent une hiérarchie d'objets dans notre tête. Par exemple, nous savons qu'un canari est un oiseau, et que tous les oiseaux ont des ailes. Nous avons aussi une idée de la couleur habituelle d'un canari et de sa vitesse de vol.

   - **Représentation par cadre** : elle repose sur la représentation de chaque objet ou classe d'objets sous forme de **cadre** contenant des **slots**. Les slots ont des valeurs par défaut possibles, des restrictions de valeurs ou des procédures stockées qui peuvent être appelées pour obtenir la valeur d'un slot. Tous les cadres forment une hiérarchie similaire à une hiérarchie d'objets dans les langages de programmation orientés objet.
   - **Scénarios** : ce sont des cadres spéciaux qui représentent des situations complexes pouvant se dérouler dans le temps.

**Python**

Slot | Valeur | Valeur par défaut | Intervalle |
-----|--------|-------------------|------------|
Nom | Python | | |
Est-Un | Langage-Non-Typé | | |
Casse des variables | | CamelCase | |
Longueur du programme | | | 5-5000 lignes |
Syntaxe de bloc | Indentation | | |

3. **Représentations procédurales** : elles reposent sur la représentation des connaissances par une liste d'actions pouvant être exécutées lorsqu'une certaine condition se produit.
   - Les règles de production sont des déclarations si-alors qui permettent de tirer des conclusions. Par exemple, un médecin peut avoir une règle disant que **SI** un patient a une forte fièvre **OU** un taux élevé de protéine C-réactive dans une analyse de sang **ALORS** il a une inflammation. Une fois que nous rencontrons une des conditions, nous pouvons conclure à une inflammation, puis l'utiliser dans un raisonnement ultérieur.
   - Les algorithmes peuvent être considérés comme une autre forme de représentation procédurale, bien qu'ils ne soient presque jamais utilisés directement dans les systèmes basés sur les connaissances.

4. **Logique** : initialement proposée par Aristote comme un moyen de représenter les connaissances humaines universelles.
   - La logique des prédicats, en tant que théorie mathématique, est trop riche pour être calculable. Par conséquent, un sous-ensemble est généralement utilisé, comme les clauses de Horn utilisées dans Prolog.
   - La logique descriptive est une famille de systèmes logiques utilisés pour représenter et raisonner sur des hiérarchies d'objets et des représentations de connaissances distribuées comme le *web sémantique*.

## Systèmes experts

Un des premiers succès de l'IA symbolique a été les **systèmes experts** - des systèmes informatiques conçus pour agir comme un expert dans un domaine problématique limité. Ils étaient basés sur une **base de connaissances** extraite d'un ou plusieurs experts humains, et contenaient un **moteur d'inférence** qui effectuait un raisonnement à partir de celle-ci.

![Architecture humaine](../../../../translated_images/arch-human.5d4d35f1bba3ab1cdfda96af2f10b89574eb31e9796d0e3011cd9beda1c35112.fr.png) | ![Système basé sur les connaissances](../../../../translated_images/arch-kbs.3ec5c150b09fa8dadc2beb0931a4983c9e2b03913a89eebcc103b5bb841b0212.fr.png)
---------------------------------------------|------------------------------------------------
Structure simplifiée du système neural humain | Architecture d'un système basé sur les connaissances

Les systèmes experts sont construits comme le système de raisonnement humain, qui contient une **mémoire à court terme** et une **mémoire à long terme**. De même, dans les systèmes basés sur les connaissances, nous distinguons les composants suivants :

* **Mémoire du problème** : contient les connaissances sur le problème en cours de résolution, par exemple la température ou la pression artérielle d'un patient, s'il a une inflammation ou non, etc. Ces connaissances sont également appelées **connaissances statiques**, car elles contiennent un instantané de ce que nous savons actuellement sur le problème - l'état du problème.
* **Base de connaissances** : représente les connaissances à long terme sur un domaine problématique. Elle est extraite manuellement des experts humains et ne change pas d'une consultation à l'autre. Comme elle permet de naviguer d'un état du problème à un autre, elle est également appelée **connaissances dynamiques**.
* **Moteur d'inférence** : orchestre tout le processus de recherche dans l'espace des états du problème, pose des questions à l'utilisateur si nécessaire. Il est également responsable de trouver les bonnes règles à appliquer à chaque état.

À titre d'exemple, considérons le système expert suivant pour déterminer un animal en fonction de ses caractéristiques physiques :

![Arbre AND-OR](../../../../translated_images/AND-OR-Tree.5592d2c70187f283703c8e9c0d69d6a786eb370f4ace67f9a7aae5ada3d260b0.fr.png)

> Image par [Dmitry Soshnikov](http://soshnikov.com)

Ce diagramme est appelé un **arbre AND-OR**, et il s'agit d'une représentation graphique d'un ensemble de règles de production. Dessiner un arbre est utile au début de l'extraction des connaissances de l'expert. Pour représenter les connaissances dans l'ordinateur, il est plus pratique d'utiliser des règles :

```
IF the animal eats meat
OR (animal has sharp teeth
    AND animal has claws
    AND animal has forward-looking eyes
) 
THEN the animal is a carnivore
```

Vous pouvez remarquer que chaque condition sur le côté gauche de la règle et l'action sont essentiellement des triplets objet-attribut-valeur (OAV). La **mémoire de travail** contient l'ensemble des triplets OAV correspondant au problème en cours de résolution. Un **moteur de règles** recherche les règles dont la condition est satisfaite et les applique, ajoutant un autre triplet à la mémoire de travail.

> ✅ Dessinez votre propre arbre AND-OR sur un sujet qui vous intéresse !

### Inférence avant vs. arrière

Le processus décrit ci-dessus est appelé **inférence avant**. Il commence avec des données initiales sur le problème disponibles dans la mémoire de travail, puis exécute la boucle de raisonnement suivante :

1. Si l'attribut cible est présent dans la mémoire de travail - arrêtez et donnez le résultat.
2. Recherchez toutes les règles dont la condition est actuellement satisfaite - obtenez l'**ensemble de conflit** des règles.
3. Effectuez une **résolution de conflit** - sélectionnez une règle qui sera exécutée à cette étape. Il peut y avoir différentes stratégies de résolution de conflit :
   - Sélectionnez la première règle applicable dans la base de connaissances.
   - Sélectionnez une règle au hasard.
   - Sélectionnez une règle *plus spécifique*, c'est-à-dire celle qui satisfait le plus de conditions dans le côté gauche (LHS).
4. Appliquez la règle sélectionnée et insérez une nouvelle connaissance dans l'état du problème.
5. Répétez à partir de l'étape 1.

Cependant, dans certains cas, nous pourrions vouloir commencer avec une connaissance vide du problème et poser des questions qui nous aideront à arriver à une conclusion. Par exemple, lors d'un diagnostic médical, nous ne réalisons généralement pas toutes les analyses médicales à l'avance avant de commencer à diagnostiquer le patient. Nous préférons effectuer des analyses lorsqu'une décision doit être prise.

Ce processus peut être modélisé en utilisant l'**inférence arrière**. Elle est guidée par le **but** - la valeur de l'attribut que nous cherchons à trouver :

1. Sélectionnez toutes les règles qui peuvent nous donner la valeur d'un but (c'est-à-dire avec le but sur le côté droit (RHS)) - un ensemble de conflit.
1. S'il n'y a pas de règles pour cet attribut, ou s'il existe une règle disant que nous devrions demander la valeur à l'utilisateur - demandez-la, sinon :
1. Utilisez une stratégie de résolution de conflit pour sélectionner une règle que nous utiliserons comme *hypothèse* - nous essaierons de la prouver.
1. Répétez de manière récurrente le processus pour tous les attributs dans le LHS de la règle, en essayant de les prouver comme des buts.
1. Si à un moment donné le processus échoue - utilisez une autre règle à l'étape 3.

> ✅ Dans quelles situations l'inférence avant est-elle plus appropriée ? Et l'inférence arrière ?

### Implémentation des systèmes experts

Les systèmes experts peuvent être implémentés en utilisant différents outils :

* Les programmer directement dans un langage de programmation de haut niveau. Ce n'est pas la meilleure idée, car l'avantage principal d'un système basé sur les connaissances est que les connaissances sont séparées de l'inférence, et qu'un expert du domaine problématique devrait potentiellement pouvoir écrire des règles sans comprendre les détails du processus d'inférence.
* Utiliser un **shell de système expert**, c'est-à-dire un système spécifiquement conçu pour être alimenté par des connaissances en utilisant un langage de représentation des connaissances.

## ✍️ Exercice : Inférence animale

Consultez [Animals.ipynb](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/2-Symbolic/Animals.ipynb) pour un exemple d'implémentation d'un système expert avec inférence avant et arrière.
> **Remarque** : Cet exemple est assez simple et donne seulement une idée de l'apparence d'un système expert. Une fois que vous commencez à créer un tel système, vous ne remarquerez un comportement *intelligent* qu'après avoir atteint un certain nombre de règles, environ 200 ou plus. À un moment donné, les règles deviennent trop complexes pour toutes les garder en tête, et c'est à ce moment-là que vous pourriez commencer à vous demander pourquoi le système prend certaines décisions. Cependant, une caractéristique importante des systèmes basés sur la connaissance est que vous pouvez toujours *expliquer* exactement comment chacune des décisions a été prise.
## Ontologies et le Web sémantique

À la fin du 20ᵉ siècle, une initiative a vu le jour pour utiliser la représentation des connaissances afin d'annoter les ressources Internet, permettant ainsi de trouver des ressources correspondant à des requêtes très spécifiques. Ce mouvement a été appelé **Web sémantique**, et il repose sur plusieurs concepts :

- Une représentation des connaissances particulière basée sur les **[logiques de description](https://en.wikipedia.org/wiki/Description_logic)** (DL). Elle est similaire à la représentation des connaissances par cadres, car elle construit une hiérarchie d'objets avec des propriétés, mais elle possède une sémantique logique formelle et des capacités d'inférence. Il existe toute une famille de DLs qui équilibrent expressivité et complexité algorithmique de l'inférence.
- Une représentation des connaissances distribuée, où tous les concepts sont représentés par un identifiant URI global, rendant possible la création de hiérarchies de connaissances couvrant l'ensemble d'Internet.
- Une famille de langages basés sur XML pour la description des connaissances : RDF (Resource Description Framework), RDFS (RDF Schema), OWL (Ontology Web Language).

Un concept central du Web sémantique est celui d'**ontologie**. Cela fait référence à une spécification explicite d'un domaine problématique en utilisant une représentation formelle des connaissances. L'ontologie la plus simple peut être une simple hiérarchie d'objets dans un domaine donné, mais des ontologies plus complexes incluront des règles pouvant être utilisées pour l'inférence.

Dans le Web sémantique, toutes les représentations sont basées sur des triplets. Chaque objet et chaque relation sont identifiés de manière unique par un URI. Par exemple, si nous voulons indiquer que ce programme d'IA a été développé par Dmitry Soshnikov le 1er janvier 2022, voici les triplets que nous pouvons utiliser :

<img src="images/triplet.png" width="30%"/>

```
http://github.com/microsoft/ai-for-beginners http://www.example.com/terms/creation-date “Jan 13, 2007”
http://github.com/microsoft/ai-for-beginners http://purl.org/dc/elements/1.1/creator http://soshnikov.com
```

> ✅ Ici, `http://www.example.com/terms/creation-date` et `http://purl.org/dc/elements/1.1/creator` sont des URIs bien connus et universellement acceptés pour exprimer les concepts de *créateur* et de *date de création*.

Dans un cas plus complexe, si nous voulons définir une liste de créateurs, nous pouvons utiliser certaines structures de données définies dans RDF.

<img src="images/triplet-complex.png" width="40%"/>

> Diagrammes ci-dessus par [Dmitry Soshnikov](http://soshnikov.com)

Le développement du Web sémantique a été quelque peu freiné par le succès des moteurs de recherche et des techniques de traitement du langage naturel, qui permettent d'extraire des données structurées à partir de textes. Cependant, dans certains domaines, des efforts significatifs sont encore déployés pour maintenir des ontologies et des bases de connaissances. Voici quelques projets notables :

* [WikiData](https://wikidata.org/) est une collection de bases de connaissances lisibles par machine associées à Wikipédia. La plupart des données sont extraites des *InfoBoxes* de Wikipédia, des morceaux de contenu structuré présents dans les pages Wikipédia. Vous pouvez [interroger](https://query.wikidata.org/) WikiData en SPARQL, un langage de requête spécifique au Web sémantique. Voici un exemple de requête affichant les couleurs d'yeux les plus populaires chez les humains :

```sparql
#defaultView:BubbleChart
SELECT ?eyeColorLabel (COUNT(?human) AS ?count)
WHERE
{
  ?human wdt:P31 wd:Q5.       # human instance-of homo sapiens
  ?human wdt:P1340 ?eyeColor. # human eye-color ?eyeColor
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
GROUP BY ?eyeColorLabel
```

* [DBpedia](https://www.dbpedia.org/) est un autre projet similaire à WikiData.

> ✅ Si vous souhaitez expérimenter avec la création de vos propres ontologies ou explorer des ontologies existantes, il existe un excellent éditeur visuel d'ontologies appelé [Protégé](https://protege.stanford.edu/). Téléchargez-le ou utilisez-le en ligne.

<img src="images/protege.png" width="70%"/>

*Éditeur Web Protégé ouvert avec l'ontologie de la famille Romanov. Capture d'écran par Dmitry Soshnikov*

## ✍️ Exercice : Une ontologie familiale

Consultez [FamilyOntology.ipynb](https://github.com/Ezana135/AI-For-Beginners/blob/main/lessons/2-Symbolic/FamilyOntology.ipynb) pour un exemple d'utilisation des techniques du Web sémantique afin de raisonner sur les relations familiales. Nous prendrons un arbre généalogique représenté au format GEDCOM courant et une ontologie des relations familiales pour construire un graphe de toutes les relations familiales pour un ensemble donné d'individus.

## Microsoft Concept Graph

Dans la plupart des cas, les ontologies sont soigneusement créées à la main. Cependant, il est également possible de **miner** des ontologies à partir de données non structurées, par exemple à partir de textes en langage naturel.

Une tentative en ce sens a été réalisée par Microsoft Research, et a donné lieu au [Microsoft Concept Graph](https://blogs.microsoft.com/ai/microsoft-researchers-release-graph-that-helps-machines-conceptualize/?WT.mc_id=academic-77998-cacaste).

Il s'agit d'une vaste collection d'entités regroupées à l'aide de la relation d'héritage `is-a`. Cela permet de répondre à des questions comme "Qu'est-ce que Microsoft ?" - la réponse étant quelque chose comme "une entreprise avec une probabilité de 0,87, et une marque avec une probabilité de 0,75".

Le Graph est disponible soit via une API REST, soit sous forme d'un grand fichier texte téléchargeable listant toutes les paires d'entités.

## ✍️ Exercice : Un graphe de concepts

Essayez le notebook [MSConceptGraph.ipynb](https://github.com/microsoft/AI-For-Beginners/blob/main/lessons/2-Symbolic/MSConceptGraph.ipynb) pour voir comment nous pouvons utiliser le Microsoft Concept Graph pour regrouper des articles d'actualité en plusieurs catégories.

## Conclusion

De nos jours, l'IA est souvent considérée comme un synonyme de *Machine Learning* ou de *réseaux neuronaux*. Cependant, un être humain fait également preuve de raisonnement explicite, ce qui est quelque chose que les réseaux neuronaux ne gèrent pas encore. Dans les projets du monde réel, le raisonnement explicite est toujours utilisé pour effectuer des tâches nécessitant des explications ou la capacité de modifier le comportement du système de manière contrôlée.

## 🚀 Défi

Dans le notebook Family Ontology associé à cette leçon, il y a une opportunité d'expérimenter avec d'autres relations familiales. Essayez de découvrir de nouvelles connexions entre les personnes de l'arbre généalogique.

## [Quiz post-cours](https://ff-quizzes.netlify.app/en/ai/quiz/4)

## Révision et auto-apprentissage

Faites des recherches sur Internet pour découvrir des domaines où les humains ont tenté de quantifier et de codifier les connaissances. Jetez un œil à la taxonomie de Bloom, et remontez dans l'histoire pour apprendre comment les humains ont essayé de comprendre leur monde. Explorez le travail de Linné pour créer une taxonomie des organismes, et observez la manière dont Dmitri Mendeleïev a créé un système pour décrire et regrouper les éléments chimiques. Quels autres exemples intéressants pouvez-vous trouver ?

**Devoir** : [Construire une ontologie](assignment.md)

**Avertissement** :  
Ce document a été traduit à l'aide du service de traduction automatique [Co-op Translator](https://github.com/Azure/co-op-translator). Bien que nous nous efforcions d'assurer l'exactitude, veuillez noter que les traductions automatisées peuvent contenir des erreurs ou des inexactitudes. Le document original dans sa langue d'origine doit être considéré comme la source faisant autorité. Pour des informations critiques, il est recommandé de recourir à une traduction professionnelle réalisée par un humain. Nous déclinons toute responsabilité en cas de malentendus ou d'interprétations erronées résultant de l'utilisation de cette traduction.