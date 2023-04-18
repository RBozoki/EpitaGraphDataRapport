
##	*Partie III* 


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
select ?x ?y where {
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


**Q1.**
```
h:hasSpouse a owl:ObjectProperty, rdf:Property, owl:SymmetricProperty ;
```
**Q2.**

Pas de changements observés avec ou sans OWL RF et RDFS RL. Cependant en désactivant RDFS Subset, la symétrie des relations n'est plus observable.

On en conclu, que ce paramètre permet de définir si les relations sémantiques doivent être prisent en compte.

**Q3.**
```
h:hasAncestor a rdf:Property, owl:TransitiveProperty ;
```
**Q4.**
```
h:hasChild a rdf:Property ;
  ...
  owl:inverseOf h:hasParent .
```
**Q5.**
```
h:Professor a rdfs:Class ;
  rdfs:label "professor"@en ;
  rdfs:label "professeur"@fr ;
  owl:intersectionOf (h:Researcher h:Lecturer) .
```

```
h:Academic a rdfs:Class ;
  rdfs:label "academic"@en ;
  rdfs:label "universitaire"@fr ;
  owl:unionOf (h:Researcher h:Lecturer) .
```

**Q6.**

## Exercice 3.2:

##	*Partie I* 

**Q1.**

**Q2.**

**Q3.**

**Q4.**
