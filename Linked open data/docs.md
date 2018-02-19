# Linked Open Data documentatie
	Linked open data is open data dat gestructureerd is om interlinked te zijn om het zo gemakkelijker te maken om te werken met semantic query

Linked Open Data is conceptueel vrij eenvoudig. Er wordt ervan uit gegaan dat alles in de wereld kan uitgedrukt worden aan de hand van “feiten” en die feiten nemen de vorm aan van drie-delige constructies : “onderwerp - predikaat - voorwerp”. Dit worden  “triples” genoemd.

Alle Linked Open Data van de Stad Gent is bevraagbaar via een [“SPARQL endpoint”](https://stad.gent/sparql).

## SPARQL (Protocol And RDF Query Language)
	SPARQL is een RDF Query Language wat wil zeggen dat het een semantic query language is voor databases dat data kan ophalen in het RDF format. Dit is een standaard volgens RDF Data Access Working Group van de W3C.

**Structuur van een SPARQL query**

- **Prefix declaration**: Wordt gebruikt om een namespace te creëren bij een bepaalde URI zodat je in je query's niet altijd de volle URI moet schrijven.
- **Result clause**: Om te kiezen welke data je moet terugkrijgen van de query.
- **Query pattern**: specificeren waarnaar moet worden gezocht in de onderliggende dataset.
- **Query modifiers**: Om je resultaten die je terugkrijgt van je query te ordenen.

> ? of $ zijn aanduidingen van variabelen

```
# Prefix declaration
PREFIX ex: <http://example.com/exampleOntology#>
# Result clause
SELECT ?capital
       ?country
# Query pattern
WHERE
  {
    ?x  ex:cityname       ?capital   ;
        ex:isCapitalOf    ?y         .
    ?y  ex:countryname    ?country   ;
        ex:isInContinent  ex:Africa  .
  }
# Query modifiers
ORDER BY DESC(?capital)
LIMIT 100
```

## Voorbeeld queries



**Alle diensten/producten van de stad Gent weergeven**

Door SELECT * te gebruiken worden de resultaten weergeggeven van alle variabels in de query.

```
PREFIX schema: <http://schema.org/>
PREFIX dct:<http://purl.org/dc/terms/>
SELECT *
WHERE {
  ?product a <http://purl.org/vocab/cpsv#PublicService>.  
  ?product schema:audience ?audience.
  ?product dct:title ?titel
}
```
[Resultaat van de query](https://stad.gent/sparql?default-graph-uri=&query=PREFIX+schema%3A+<http%3A%2F%2Fschema.org%2F>%0D%0APREFIX+dct%3A<http%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F>%0D%0ASELECT+*%0D%0AWHERE+%7B%0D%0A++%3Fproduct+a+<http%3A%2F%2Fpurl.org%2Fvocab%2Fcpsv%23PublicService>.++%0D%0A++%3Fproduct+schema%3Aaudience+%3Faudience.%0D%0A++%3Fproduct+dct%3Atitle+%3Ftitel%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on)


**Diensten voor ecologische bedrijven**

Via Linked Open Data kan een programma of een app bijvoorbeeld uitzoeken welke stedelijke dienstverlening bestaat voor bedrijven die iets willen doen aan hun ecologische voetafdruk:

```
PREFIX schema: <http://schema.org/>
PREFIX dct:<http://purl.org/dc/terms/>
SELECT ?product ?titel
WHERE {
  ?product a <http://purl.org/vocab/cpsv#PublicService>.
  ?product schema:audience <http://stad.gent/data/ns/gpdc/doelgroepen/onderneming>.
  ?product dct:subject <http://stad.gent/data/ns/themas/natuur-milieu>.
  ?product dct:title ?titel
}
```

[Resultaat van deze query](https://stad.gent/sparql?default-graph-uri=&query=PREFIX+schema%3A+%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+dct%3A%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0ASELECT+%3Fproduct+%3Ftitel%0D%0AWHERE+%7B%0D%0A%3Fproduct+a+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Fcpsv%23PublicService%3E.%0D%0A%3Fproduct+schema%3Aaudience+%3Chttp%3A%2F%2Fstad.gent%2Fdata%2Fns%2Fgpdc%2Fdoelgroepen%2Fonderneming%3E.%0D%0A%3Fproduct+dct%3Asubject+%3Chttp%3A%2F%2Fstad.gent%2Fdata%2Fns%2Fthemas%2Fnatuur-milieu%3E.%0D%0A%3Fproduct+dct%3Atitle+%3Ftitel%0D%0A%7D&format=text%2Fhtml&timeout=0&debug=on)


**Recent museumnieuws**
Een krantenredactie kan zo automatisch de 5 laatste nieuwsberichten van het Huis van Alijn en het SMAK opvragen:


```
PREFIX schema:<http://schema.org/>
SELECT ?article ?titel ?published
WHERE {
  VALUES ?org {
    <https://stad.gent/id/agents/a5294c55-f789-e111-a140-0050569826fc>
    <https://stad.gent/id/agents/96677ab3-f689-e111-a140-0050569826fc>
  }.
  ?article a schema:NewsArticle.
  ?article schema:datePublished ?published.
  ?article <http://schema.org/sourceOrganization> ?org.
  ?article schema:headline ?titel
}
ORDER BY DESC(?published)
LIMIT 5
```

[Resultaat van deze query](https://stad.gent/sparql?default-graph-uri=&query=%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0ASELECT+%3Farticle+%3Ftitel+%3Fpublished%0D%0AWHERE+%7B%0D%0A++VALUES+%3Forg+%7B%0D%0A++++%3Chttps%3A%2F%2Fstad.gent%2Fid%2Fagents%2Fa5294c55-f789-e111-a140-0050569826fc%3E%0D%0A++++%3Chttps%3A%2F%2Fstad.gent%2Fid%2Fagents%2F96677ab3-f689-e111-a140-0050569826fc%3E%0D%0A++%7D.%0D%0A++%3Farticle+a+schema%3ANewsArticle.%0D%0A++%3Farticle+schema%3AdatePublished+%3Fpublished.%0D%0A++%3Farticle+%3Chttp%3A%2F%2Fschema.org%2FsourceOrganization%3E+%3Forg.%0D%0A++%3Farticle+schema%3Aheadline+%3Ftitel%0D%0A%7D+ORDER+BY+DESC%28%3Fpublished%29+LIMIT+5&format=text%2Fhtml&timeout=0&debug=on)


[Extra voorbeelden](https://www.w3.org/2009/Talks/0615-qbe/#q1)
