# Utiliser des graphiques RDF dans Graph Studio

## Présentation

Graph Studio dans Oracle Autonomous Database permet aux utilisateurs de modéliser, de créer, d'interroger et d'analyser des données de graphique. Il comprend des blocs-notes, des API de développeur pour l'exécution de requêtes de graphique à l'aide de PGQL, plus de 60 algorithmes de graphique intégrés, et offre des dizaines de visualisations, y compris la visualisation de graphique native. En plus du graphique de propriétés, Graph Studio étend désormais la prise en charge des technologies sémantiques, y compris les capacités de stockage, d'inférence et de requête pour les données et les ontologies basées sur Resource Description Framework (RDF) et Web Ontology Language (OWL). Vous pouvez désormais utiliser Graph Studio pour les fonctions RDF prises en charge suivantes :

*   Créer un graphe RDF
*   Exécuter des requêtes SPARQL sur le graphique RDF dans un paragraphe de bloc-notes
*   Analyser et visualiser les graphiques RDF

RDF est un modèle de données standard W3C pour la représentation des données liées. RDF utilise les URI (Uniform Resource Identifiers) comme identificateurs uniques globaux pour les ressources et les URI afin de nommer la relation entre deux ressources. En plus des URI, RDF utilise des littéraux pour représenter des valeurs scalaires telles que des nombres, des chaînes et des horodatages. RDF modélise les données liées sous la forme d'un graphique orienté et étiqueté, où chaque arête est généralement appelée triple. Le sommet source du bord est appelé le sujet du triple. L'étiquette ou le nom de l'arête est appelé le prédicat du triple, et le sommet de destination de l'arête est appelé l'objet du triple. Les graphes RDF sont particulièrement adaptés aux graphes de connaissances et aux applications d'intégration de données, car les URI fournissent des identificateurs uniques au niveau global et la structure triple simple et sans schéma permet de combiner très facilement des données de plusieurs graphes RDF différents en un seul graphe. En outre, RDFS et OWL fournissent des moyens standard de définir des lexiques réutilisables (ensembles d'étiquettes d'arêtes sémantiquement significatives et de types de ressources) pour des données graphiques plus interopérables et traitées par machine. Pour plus d'informations sur les normes W3C RDF 1.1, cliquez [ici](https://www.w3.org/TR/rdf11-primer/).

SPARQL Protocol and RDF Query Language (SPARQL) est l'une des technologies standardisées par W3C pour l'interrogation des données RDF (Resource Description Framework). Vous trouverez plus d'informations sur la norme W3C SPARQL 1.1 [ici](https://www.w3.org/TR/sparql11-overview/).

SPARQL utilise une structure **SELECT some elements WHERE some conditions** pour spécifier une requête. Les conditions de la clause WHERE d'une requête SPARQL sont créées à l'aide de trois modèles, qui sont essentiellement un triple RDF où les éléments du triple peuvent être remplacés par des variables de requête (indiquées par un préfixe ?). Une variable de requête selon un modèle triple agit comme un caractère générique. Considérez le modèle triple **?movie ms:genre ms:genre\_Comedy**. Lorsque ce modèle triple est évalué par rapport à un graphique RDF, il renvoie tous les **sujets** de triples avec le prédicat **ms:genre** et **object ms:genre\_Comedy**. La clause SPARQL SELECT indique la liste des variables de requête à projeter à partir de la requête. Dans la syntaxe SPARQL, les URI sont placés entre chevrons et les littéraux entre guillemets (par exemple, "Kevin Bacon"). Les littéraux peuvent être suivis de ^^ et d'un URI de type de données (par exemple,"100"^^[http://www.w3.org/2001/XMLSchema#integer](http://www.w3.org/2001/XMLSchema#integer)) ou suivis de @ et d'une balise de langue (par exemple,"Jalapeño"@es). La plupart des types de données de schéma XML sont pris en charge dans SPARQL, et les littéraux simples sans URI de type de données sont considérés comme ayant le type de données [http://www.w3.org/2001/XMLSchema#string](http://www.w3.org/2001/XMLSchema#string).

Cette vidéo présentée ci-dessous est un exemple de démonstration utilisant un ensemble de données similaire qui sera utilisé dans cet atelier. Cette vidéo met l'accent sur la structure de l'ontologie de la structure du film en utilisant RDF. La démonstration présente RDF Graph à l'aide d'une table intermédiaire en combinaison avec SQL Developer, qui est nettement différent de cette version d'Autonomous Database de l'atelier. Cependant, le langage SPARQL utilisé pour interroger et visualiser les données est très similaire pour le contexte.

[](youtube:e_EQjInas50)

Dans ce laboratoire, un graphique sémantique sera construit à l'aide de SPARQL, une méthodologie standardisée pour l'intégration de différentes sources de données. Cette procédure vous apprendra à analyser les données à l'aide de requêtes et de visualisations basées sur des graphiques.

Temps estimé : 35 minutes

### Objectifs

*   Préparation de l'environnement
*   Introduction aux graphiques RDF
*   Créer et valider un utilisateur de graphique RDF dans Graph Studio
*   Interroger et visualiser le graphique RDF

### Prérequis

Cet exercice suppose que vous disposez des éléments suivants :

*   Compte Oracle Cloud - Consultez la page de destination LiveLabs de cet atelier pour connaître les environnements pris en charge

*   Téléchargez le fichier MOVIESTREAM (moviestream\_rdf.nt) à l'aide de ce [lien](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)

Ceci conclut ce laboratoire. Vous pouvez maintenant _passer à l'exercice suivant_.

## Accusés de réception

*   **Auteur** - Nicholas Cusato, Ethan Shmargad, Matthew McDaniel Ingénieurs solutions, Ramu Murakami Gutierrez Chef de produit
*   **Contributeur technique** - Melliyal Annamalai Chef de produit distingué, Joao Paiva Consulting Membre du personnel technique, Lavanya Jayapalan Développeur principal d'assistance utilisateur
*   **Dernière mise à jour par/date** - Chef de produit Ramu Murakami Gutierrez, juin 2023