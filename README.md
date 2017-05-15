# DSW-NHC

The DSW-NHC (Darwin Core Semantic Web for Natural History Collections) is an extension of the Darwin-SW ontology used to semantically describe present-day biodiversity data. The DSW-NHC is an application ontology that extends the Darwin-SW and serves to structure the entities in natural history collections through semantic annotation. It connects to digitized manuscript scans with the Web Annotation Data Model<sup>1</sup>.

<sup>1</sup>The Web Annotation Model [Link](https://www.w3.org/TR/annotation-model/).

Figure 1: Example occurrence record annotated with the DSW-NHC. 
![alt text](https://github.com/lisestork/DSW-NHC/blob/master/example_occurrence3.png)

Figure 1 shows one fully linked observation record that was produced in compliance with all three researchers. Orange nodes indicate IRIs and thus instances of classes from the ontology. Purple nodes also indicate IRIs but from different data providers. The IRI viaf:45106482 for instance refers to "Heinrich Kuhl", a german naturalist and zoologist and the writer of this field book. The IRI is an instance of the foaf:Person class. Further, purple nodes connect to the Uberon Ontology and the NCI Thesaurus and finally, green nodes indicate labels connected to the IRIs with the rdfs:label property. 

Figure 2: Example of an annotation that connects to the DSW-NHC. 
![alt text](https://github.com/lisestork/DSW-NHC/blob/master/AnnotationExample.png)









