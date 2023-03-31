# **Managing Graph Data**

## **BOZOKI** Raphael & **LUCCHESI** Matthieu
&nbsp;

## Exercice 2.1:
##	*Partie I* 
\
**Q3.**\
On obtient 110 réponses, cela correspond au nombre de triplets.

**Q4.**
```
select (count (*) as ?count) where {?x ?p ?y}
```

##	*Partie II* 

**Q1.**

La requête renvoie les paires [sujet, objet] des triplets ayant comme prédicats rdf:type.
On obtient 37 réponses. 
En effet rdf:type n’était pas le seul prédicat.
John est de type “Person”.

**Q2.**

La requête renvoie les paires [sujet, objet] ayant comme prédicats hasSpouse.
On obtient 6 réponses. La relation est visiblement non symétrique. On a plus de 6 noms.

**Q3.**
```
PREFIX h: <http://www.inria.fr/human#>
select * where {
?x a h:Person;h:shoesize ?y.
}
```

**Q4.**
```turtle
PREFIX h: <http://www.inria.fr/human#>
select * where {
   ?x a h:Person
   optional { ?x h:shoesize ?y. }
}
```
On peut voir 4 personne sans pointures

**Q5.**
```
PREFIX h: <http://www.inria.fr/human#>
SELECT *
WHERE {
?x a h:Person; h:shoesize ?y
FILTER (?y > 8)
}
```

**Q6.**
```
PREFIX h: <http://www.inria.fr/human#>
SELECT ?x
WHERE {
?x a h:Person; h:shoesize ?y; h:trouserssize ?ts
FILTER (?y > 8 || ?ts > 12)
}
```


**Q9.**
```
PREFIX h: <http://www.inria.fr/human#>
SELECT ?x
WHERE {
?x h:hasChild ?c
}
```
5 réponses, dont 2 doublons.

**Q10.**
```
PREFIX h: <http://www.inria.fr/human#>
SELECT DISTINCT ?x
WHERE {
?x h:hasChild ?c
}
```
On a désormais 4 réponses.

**Q11.**
```
PREFIX : <http://example.org/>
CONSTRUCT {?friend :hasFriend ?person}
WHERE {
  ?person :hasFriend ?friend .
}
```

**Q15.**
```
PREFIX h: <http://www.inria.fr/human#>
SELECT ?x (COUNT(?child) as ?nbChildren)
WHERE {
  ?x h:hasChild ?child .
}
GROUP BY ?x
```

**Q16.**
```
PREFIX h: <http://www.inria.fr/human#>
SELECT ?x (COUNT(?child) as ?nbChildren)
WHERE {
  ?x h:hasChild ?child .
}
GROUP BY ?x
HAVING (COUNT(?child) = 1)
```

**Q17.**
```
PREFIX h: <http://www.inria.fr/human#>
SELECT ?x ?child
WHERE {
  ?x h:hasChild ?child .
}
```

**Q18.**

**Q19.**

## Exercice 2.2:

##	*Partie I* 

```
@Prefix xsd: <http://www.w3.org/2001/XMLSchema#>.
@Prefix dc: <http://purl.org/dc/elements/1.1/> .
@Prefix ex:<http://example.org/>.

ex:theThinker a ex:Sculpture ;
    ex:name "The Thinker" ;
    ex:location "Rodin Museum, Paris" ;
    ex:creator "Auguste Rodin" ;
    ex:dateOfCreation "1902"^^xsd:date ;
    ex:description "A bronze sculpture of a seated man deep in thought." .

ex:monaLisa a ex:Artwork ;
    ex:name "Mona Lisa" ;
    ex:location "Louvre Museum, Paris" ;
    ex:creator "Leonardo da Vinci" ;
    ex:dateOfCreation "1503-1519" ;
    ex:description "A portrait of a woman with a mysterious smile." .

ex:notreDame a ex:Structure ;
    ex:name "Notre-Dame Cathedral" ;
    ex:location "Paris, France" ;
    ex:architect "Maurice de Sully" ;
    ex:dateOfConstruction "1163-1345" ;
    ex:description "A Gothic cathedral located on the Île de la Cité in Paris." .

ex:worldWarII a ex:Event ;
    ex:name "World War II" ;
    ex:date "1939-1945" ;
    ex:location "Paris, France" ;
    ex:description "A global war that lasted from 1939 to 1945 and involved many of the world's major countries." .

ex:frenchRevolution a ex:Event ;
    ex:name "The French Revolution" ;
    ex:date "1789-1799" ;
    ex:location "Paris, France" ;
    ex:description "A period of radical social and political upheaval in France that lasted from 1789 until the late 1790s." .

```

##	*Partie II* 

**Q1.**
```
PREFIX ex: <http://example.org/>
SELECT ?x 
WHERE {
  ?x a ex:Sculpture .
}
```

**Q2.**
```
PREFIX ex: <http://example.org/>
SELECT ?x 
WHERE {
  ?x a ex:Artwork .
}
```

**Q3.**
```
PREFIX ex: <http://example.org/>
SELECT ?x 
WHERE {
  ?x a ex:Structure .
}
```

**Q4.**
```
PREFIX ex: <http://example.org/>
SELECT ?x 
WHERE {
  ?x a ex:Museum .
}
```

**Q5.**
```
PREFIX ex: <http://example.org/>
SELECT DISTINCT ?location
WHERE {
  ?x ex:location ?location .
}
```

**Q6.**
```
PREFIX ex: <http://example.org/>
SELECT ?x
WHERE {
  ?x ex:location "Paris, France" .
}
```

**Q7.**
```
PREFIX ex: <http://example.org/>
SELECT ?x
WHERE {
  ?x a ex:Event .
  ?x ex:location "Paris, France" .
}
```

## Exercice 2.3:

**Q1.**
```
PREFIX ex: <http://example.org/movies#>
SELECT ?actor (SAMPLE(?name) as ?actorName)
WHERE {
  ?actor ex:name ?name .
}
GROUP BY ?actor
LIMIT 2
```

**Q2.**
```
PREFIX ex: <http://example.org/movies#>

SELECT (SAMPLE(?movie) as ?randomMovie) (SAMPLE(?movieTitle) as ?title) (SAMPLE(?directorName) as ?director)
WHERE {
  ?movie ex:title ?movieTitle .
  ?movie ex:director ?director .
  ?director ex:name ?directorName .
}
LIMIT 1
```

**Q3.**
```
PREFIX ex: <http://example.org/movies#>
SELECT ?genre (COUNT(?movie) as ?numMovies)
WHERE {
  ?movie ex:genre ?genre .
}
GROUP BY ?genre
```

## Exercice 2.4:

##	*Partie I* 

On remarque que pour les trois requête, les préfixes ne sont pas définis. On rajoutera donc :
```
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX bd: <http://www.bigdata.com/rdf#>
```

**Requête 1**
```
SELECT ?pays ?paysLabel
WHERE {
  ?pays wdt:P31 wd:Q6256 ;
        wdt:P30 wd:Q18 .
  SERVICE wikibase:label {
    bd:serviceParam wikibase:language "fr,en" .
  }
}
```

```
SELECT ?pays ?paysLabel
```
Indique les variables récupérées par la requête select. Ici pays et paysLabel
```
WHERE {
```
Permet de définir le modèle à rechercher dans les données.
```
?pays wdt:P31 wd:Q6256 ;
```
P31 correspond à "instance of" et Q6256 à "country". Les ressources qui ont cette propriété sont bien des pays.
```
wdt:P30 wd:Q18 .
```
P30 correspond à "continent" et Q6256 à "South America". Le pays est sud-américain s'il a cette propriété.
```
  SERVICE wikibase:label {
```
Service qui permet de récupérer des labels pour les éléments.
```
    bd:serviceParam wikibase:language "fr,en" .
```
Défini la langue des labels. On a ici le français en priorité face à l'anglais.

**Requête 2**
```
SELECT ?XLabel, ?YLabel WHERE {
    ?X wdt:P31 wd:Q5;
    wdt:P39 wd:Q11696.
    SERVICE wikibase:label {
        bd:serviceParam wikibase:language "fr,en".
    }
}
```
On remarque la présence d'une virgule dans le SELECT qui ne devrait pas être là.

De plus ?Y n'est pas présent dans la requête donc la colonne ?YLabel sera vide.
```
SELECT ?XLabel WHERE {
```
On sélectionne le label de ?X.
```
?X wdt:P31 wd:Q5;
```
Ressources qui sont une instance de human.
```
wdt:P39 wd:Q11696.
```
Ressources (humains) qui ont été président des États-Unis. P39 = "Property talk", ie sujet qui tient une position publique.
```
SERVICE wikibase:label {
    bd:serviceParam wikibase:language "fr,en".
}
```
Récupère les labels français des éléments. ie les noms complets des humains. 

**Requête 3**
```
SELECT $paysLabel ?capitaleLabel $YLabel WHERE {
    ?pays wdt:P31 wd:Q6256;
    wdt:P17 ?continent;
    wdt:P37 ?langueOfficielle;
    wdt:P36 ?capitale.
    FILTER(?continent = wd:Q15 && ?langueOfficielle = wd:Q150)
    SERVICE wikibase:label {
        bd:serviceParam wikibase:language "fr,en".
    }
}
```
La requête a pour but de récupérer les pays africains et leurs capitales dont la langue officielle est le français.
Le symbole $ est utilisé à la place du ?, ce qui est une erreur.
P17 doit être remplacé par P30 si l'on veut récupérer le continent. En effet P17 = "country".
```
SELECT ?paysLabel ?capitaleLabel WHERE {
```
Sélectionne les noms des pays et des capitales.
```
?pays wdt:P31 wd:Q6256;
```
Ressources qui sont des instances de country.
```
wdt:P30 ?continent;
```
Ressources qui appartiennent à un continent.
```
wdt:P37 ?langueOfficielle;
```
Et qui ont une langue officielle.
```
wdt:P36 ?capitale.
```
Et qui ont une capitale.
```
FILTER(?continent = wd:Q15 && ?langueOfficielle = wd:Q150)
```
Filtre les pays qui sont sur le continent africain et dont la langue officielle est le français.
```
SERVICE wikibase:label {
    bd:serviceParam wikibase:language "fr,en".
}
```
Récupère les noms français.

## Exercice 3.1:

##	*Partie I* 

**Q4.**
```
select ?x where {
  ?x a rdfs:Class
}
```
**Q5.**
```
select ?x where {
  ?x rdfs:subClassOf ?y
}
```
**Q6.**
```
select ?x where {
  ?x ?p ?y .
  FILTER (?p IN (rdfs:domain, rdfs:range) )
}
```

##	*Partie II*

**Q2.**
```
PREFIX h: <http://www.inria.fr/human#>
select (count (*) as ?count) where {
  ?x a h:Person
}
```
Ce sont des personnes.

**Q3.**

La requête retourne 17 resources.

**Q4.**

Dans humanrdfs, des prédicats sont définis, et certains ont comme range ou domain Person. C'est pour cela que l'on a plus de resources retournées.

**Q5.**

On a dans un premier temps une seule ligne comme résultat. Avec la règle d'inférence désactivée, on a aucun résultat.

**Q6.**

Pas de changement observé.

**Q7.**

Dans humanrdfs, hasParent est défini comme une subPropertyOf de hasAncestor. hasParent est bien présent dans human.ttl. Cela explique le résultat.

##	*Partie III* 

**Q1.**

h:hasSpouse a owl:ObjectProperty, rdf:Property, owl:SymmetricProperty ;

**Q2.**

Pas de changements observés avec ou sans OWL RF et RDFS RL. Cependant en désactivant RDFS Subset, la symétrie des relations n'est plus observable.

On en conclu, que ce paramètre permet de définir si les relations sémantiques doivent être prisent en compte.

**Q3.**

h:hasAncestor a rdf:Property, owl:TransitiveProperty ;

**Q4.**
```
h:hasChild a rdf:Property ;
  ...
  owl:inverseOf h:hasParent .
```