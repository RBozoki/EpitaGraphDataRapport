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

##	*Partie II* 