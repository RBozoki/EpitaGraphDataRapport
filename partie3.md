
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
À partir du résultat de cette requête, on peut déduire la hiérarchie suivante pour ces sous-classes :

|Aimal|||||||
| - |-|-|-|-|-|-|
|Person|Female|Male|
|Woman \| Lecturer\| Man \| Researcher |Woman|Man|

 
**Q6.**
```
PREFIX h: <http://www.inria.fr/human#>
select ?x where {{
  ?x a rdf:Property ;
  rdfs:range h:Person .
}
union {
  ?x a rdf:Property ;
  rdf:domain h:Person .
}}
```
Le résultat est hasFriend et hasSpouse.

##	*Partie II*

**Q2.**
```
PREFIX h: <http://www.inria.fr/human#>
select (count (*) as ?count) where {
  ?x a h:Person
}
```
Il y a 9 entités. Ce sont des personnes. On remarque que les entités déclarées comme homme ou femme ne sont pas considérées comme des personnes.

**Q3.**

La requête retourne 17 resources.

**Q4.**

Dans humanrdfs, Man et Woman sont défini comme des sous-classes de Person. La reqête selectionne désormais aussi les entités Man et Woman.

**Q5.**
```
PREFIX h: <http://www.inria.fr/human#>
select ?x ?y where {
  ?x a h:Male ;
  h:hasSpouse ?y .
}
```
On a dans un premier temps une seule ligne comme résultat. Avec la règle d'inférence désactivée, on a aucun résultat.
La différence est expliqué par le fait que cette relation est inférée.

**Q6.**

Une deuxième resource apparait. Cela s'explique car Karl avait une épouse mais étais défini comme une Personne et non male. Le rajout de cette information en tant que "hasfather" infère qu'il est un Male. En effet Male est le co-domaine de hasfather.

**Q7.**

Dans humanrdfs, hasParent est défini comme une subPropertyOf de hasAncestor. Comme hasParent est bien présent dans human.ttl, par inférence on obtient des réultats.


##	*Partie III* 

**Q1.**
```
h:hasSpouse a owl:ObjectProperty, rdf:Property, owl:SymmetricProperty ;
```
```
h:hasFriend a owl:ObjectProperty, rdf:Property, owl:SymmetricProperty ;
```
**Q2.**

La requête renvoie dans un premier temps 12 ressources dont les symétriques. En désactivant l'inférence (RDFS Subset), les symétriques ne sont plus renvoyés, ie plus que 6.
Pas de changements observés avec ou sans OWL RF et RDFS RL. 

On en conclu, que ce paramètre permet de définir si les relations sémantiques doivent être prisent en compte.

**Q3.**
```
h:hasAncestor a rdf:Property, owl:TransitiveProperty ;
```
On vérifie la transitivité en comparant le nombre de résultats avant et après cet ajout. Les résultats passent de 5 à 10.


**Q4.**
```
h:hasChild a rdf:Property ;
  ...
  owl:inverseOf h:hasParent .
```
On a autant de relations ?x hasChild ?y que de relations ?x hasParent ?y.

**Q5.**
```
h:Professor a owl:Class ;
  rdfs:label "professor"@en ;
  rdfs:label "professeur"@fr ;
  owl:intersectionOf (                          
    [ a owl:Class ; owl:intersectionOf (h:Researcher h:Lecturer) ]                                                                     
  ) .
```
La requête a Professor renvoie bien le même réultat que la requête ne gardant que les Person qui sont à la fois des Researcher et des Lecturer.

```
h:Academic a owl:Class ;
  rdfs:label "academic"@en ;
  rdfs:label "universitaire"@fr ;
  owl:unionOf (                          
    [ a owl:Class ; owl:unionOf (h:Researcher h:Lecturer) ]                                                                     
  ) .
```
Une personne est Professor, et trois sont Academic. On obtient les mêmes résultats en effectuant l'union et l'intersection à la main.

**Q6.**
```
h:Man a rdfs:Class, owl:Class ;
  ...
  rdfs:subClassOf [
    a owl:Restriction ;
    owl:onProperty h:hasSpouse ;
    owl:allValuesFrom h:Woman
  ] .

h:Woman a rdfs:Class, owl:Class ;
  ...
  rdfs:subClassOf [
    a owl:Restriction ;
    owl:onProperty h:hasSpouse ;
    owl:allValuesFrom h:Man
  ] .
```
Nous avons testé cet ajout en ayant exécuté la requête après avoir mis un couple de deux individus du même sexe. Ce résultat n'apparaît pas dans les instances. Donc le allValuesFrom fonctionne.

## Exercice 3.2:

##	*Partie I* 

**Q1.**
```
select (count(distinct(?p)) as ?count) where { 
	?s ?p ?o .
}


select (count(*) as ?count)
where {
  select distinct ?s ?p ?o
  where {
    ?s ?p ?o .
  }
}
```
On a 272 triplets distincts dans le graphe initial.

**Q2.**
En désactivant les inférences on obtient 140 triplets distinct. Il y a donc eu 132 relations disctinctes inférées dans le graphe initial.

**Q3.**


**Q4.**
