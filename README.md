# NHC-Ontology

The NHC-Ontology (Natural History Collections Ontology) is an application ontology that extends the Darwin-SW, an ontology to describe present-day biodiversity information, and serves to structure the entities in the content of natural history collections through semantic annotation. It connects to digitized manuscript scans with the Web Annotation Data Model<sup>1</sup>.

On a collection and item level, we use the following standards to describe natural history collections: Natural Collection Description (NCD) from TDWG for describing collections and the Dublin Core for items. For the content, we integrate the Darwin Core and Darwin-SW for describing Biodiversity, and some classes taken from NCIT, Uberon and Geonames. See figure 1 for a graphical representation of the model. 

In this repository you can find the application ontology. The code of the Semantic Field Book Annotator for crowd-sourcing semantic annotations from Field Books using this ontology can be found in the following GIT Repository: https://github.com/lisestork/SFB-Annotator. A README file is in progress. 

<sup>1</sup>The Web Annotation Model [Link](https://www.w3.org/TR/annotation-model/).

Figure 1: The NHC-Ontology
![alt text](https://github.com/lisestork/NHC-Ontology/blob/master/Images/OccurrenceModel.png)

Figure 2: Example queries (tested) to be used to query the SPARQL endpoint (http://localhost:8080/rdf4j-server/repositories/NC through the Virtuoso SPARQL query editor: https://dbpedia.org/sparql.
![alt text](https://github.com/lisestork/NHC-Ontology/blob/master/Images/Example_Queries_SPARQLEndpoint.png)

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dwciri: <http://rs.tdwg.org/dwc/iri/>
PREFIX dsw: <http://purl.org/dsw/>
PREFIX oa: <http://www.w3.org/ns/oa#>
SELECT ?label ?page WHERE { 
       ?identification dwciri:toTaxon ?taxon .
       ?taxon rdfs:label ?label .
       ?organism dsw:hasIdentification ?identification .
       ?organism dsw:hasOccurrence ?occurrence .
       ?occurrence dwciri:recordedBy 
                   <http://viaf.org/viaf/45106482> .
       ?occurrence dsw:hasEvidence ?observationRecord . 
       ?anno oa:hasBody ?observationRecord . 
       ?anno oa:hasTarget ?page
       }
       
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX nhc: <http://example.org/nhc/>
PREFIX nc: <http://testingsense.liacs.nl/rdf/nc#>
PREFIX dwc: <http://rs.tdwg.org/dwc/>
PREFIX dwciri: <http://rs.tdwg.org/dwc/iri/>
PREFIX dsw: <http://purl.org/dsw/>
PREFIX viaf: <http://viaf.org/viaf/>
SELECT ?label WHERE {
       ?taxon rdfs:label ?label .
       ?taxon nhc:taxonRank nc:species .
       ?taxon nhc:belongsToTaxon ?taxon2 .
  	   ?taxon2 rdfs:label ?chiroptera
       FILTER regex(?chiroptera, "Chiropterae") .
       ?identification dwciri:toTaxon ?taxon .
       ?organism dsw:hasIdentification 
                                    ?identification . 
       ?occurrence dsw:occurrenceOf ?organism . 
       ?occurrence dwciri:recordedBy 
                                    viaf:45106482 }

PREFIX nhc: <http://example.org/nhc/>
PREFIX dwc: <http://rs.tdwg.org/dwc/terms/>
PREFIX dsw: <http://purl.org/dsw/>
PREFIX oa: <http://www.w3.org/ns/oa#>
SELECT ?page WHERE {  
       ?event nhc:verbatimEventDate ?date .
       ?date dwc:year ?year .
       FILTER (?year >= 1820). 
       FILTER (?year <= 1821) .
       ?event dsw:eventOf ?occurrence .
       ?occurrence dsw:hasEvidence ?observationRecord . 
       ?anno oa:hasBody ?observationRecord . 
       ?anno oa:hasTarget ?page 
       }
       
PREFIX dwciri: <http://rs.tdwg.org/dwc/iri/>
PREFIX dsw: <http://purl.org/dsw/>
PREFIX uberon: <http://purl.obolibrary.org/obo/>
PREFIX ncit: <http://identifiers.org/ncit/>
PREFIX nhc: <http://example.org/nhc/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
SELECT DISTINCT ?label2 
WHERE { ?identification dwciri:toTaxon ?taxon .
  		?taxon rdfs:label ?label 
        FILTER regex(?label, "Pteropus") 
        ?identification dsw:isBasedOn ?token . 
        ?token dsw:hasDerivative ?measurement . 
	    ?measurement nhc:measuresOrDescribes 
	                        ?propertyorattribute .
  		?propertyorattribute rdfs:label ?label2 .
  		?propertyorattribute rdf:type ?ncitClass .
		?ncitClass rdfs:subClassOf ncit:C20189 
	}

Figure 3: Example occurrence record annotated with the NHC-Ontology. 
![alt text](https://github.com/lisestork/NHC-Ontology/blob/master/Images/example_occurrence.png)

Figure 3 shows one fully linked observation record that was produced in compliance with three biology and history of science researchers. Orange nodes indicate IRIs and thus instances of classes from the ontology. Purple nodes also indicate IRIs but from different data providers. The IRI viaf:45106482 for instance refers to "Heinrich Kuhl", a german naturalist and zoologist and the writer of this field book. The IRI is an instance of the foaf:Person class. Further, purple nodes connect to the Uberon Ontology and the NCI Thesaurus and finally, green nodes indicate labels connected to the IRIs with the rdfs:label property. 

Figure 4: Example of an annotation that connects to the NHC-Ontology. 
![alt text](https://github.com/lisestork/NHC-Ontology/blob/master/Images/AnnotationExample.png)

