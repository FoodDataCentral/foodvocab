# FDC Food Vocabulary

## Introduction

Welcome to the USDA [Food DataCentral (FDC)](https://fdc.nal.usda.gov/) Food Vocabulary github repository. The **FDC Food Vocabulary** is a hierarchically-structured a web vocabulary describing the foods and food-products analyzed for components of nutritional interest in FDC. The **FDC Food Vocabulary** extends the **Nutrient Data Bank (NDB)** numbering system used in the [Nutrient
Database of Standard Reference (SR-Legacy)](https://www.ars.usda.gov/ARSUserFiles/80400525/Data/SR-Legacy/SR-Legacy_Doc.pdf), as well as the [Foundation Foods](https://fdc.nal.usda.gov/Foundation_Foods_Documentation) datasets. Existing NDB numbers have been used to create web-identifiers for terminology in the FDC Food Vocabulary. In addition, the vocabulary includes a hierarchical structure of existing, as well as new terms created to facilitate search and discovery of FDC data.  

## Accessing the FDC Food Vocabulary

The **FDC Food Vocabulary** is available in `OWL`, `JSON`, and `CSV` formats hosted [in the release directory](release/). Quick links to the files are as follows:

* [fdc-foodvocab.owl](release/fdc-foodvocab.owl)
* [fdc-foodvocab.json](release/fdc-foodvocab.json)
* [fdc-foodvocab.csv](release/fdc-foodvocab.csv)

## Development

### Preamble

This section is for developers of the **FDC Food Vocabulary**. This vocabulary is built using the [ROBOT](https://robot.obolibrary.org/) command-line tool. To modify the vocabulary it is necessary to setup a the necessary compute requirements for ROBOT by following the instructions from the [ROBOT getting started](https://robot.obolibrary.org/) page. 

The FDC Food Vocabulary is implement in the [Web Ontology Language (OWL)](http://www.w3.org/2002/07/owl#). It makes use of the [Simple Knowledge Organization System (SKOS)](http://www.w3.org/TR/skos-reference/skos.rdf), as well as the [Resource Description Framework (RDF)](http://www.w3.org/1999/02/22-rdf-syntax-ns#) and the [RDF Schema vocabulary (RDFS)](https://www.w3.org/2000/01/rdf-schema#). 

**Dependencies**

[ROBOT](https://robot.obolibrary.org/)

[Java 11 (or later)](https://www.oracle.com/java/technologies/javase/jdk11-archive-downloads.html)

### Working with the **FDC Food Vocabulary**

**Making Modifications**

It is only necessary to work with the [fdc-foodvocab-edit.csv](src/fdc-foodvocab-edit.csv). The `CSV` file is a [ROBOT Template](https://robot.obolibrary.org/template), which is first complied into  `OWL` format and in subsequently into `JSON`, and `CSV`. 


#### Compiling the FDC Food Vocabulary

After making modifications to the [fdc-foodvocab-edit.csv](src/fdc-foodvocab-edit.csv), run the following commands From the top level directory:

**Compile `foodvocab-edit` ROBOT Template to create OWL file**

```
robot template --template src/fdc-foodvocab-edit.csv -i src/skos.rdf --prefix "FDCFOOD:https://fdc.nal.usda.gov/vocab/FDCFOOD_" --ontology-iri "https://fdc.nal.usda.gov/vocab/fdc-foodvocab.owl" -o release/fdc-foodvocab.owl
```

**Update the `JSON` file**
```
robot convert --input release/fdc-foodvocab.owl --prefix "FDCFOOD:https://fdc.nal.usda.gov/vocab/FDCFOOD_" --output release/fdc-foodvocab.json
```

**Update the `CSV` file**
```
robot export --input release/fdc-foodvocab.owl --prefix "FDCFOOD:https://fdc.nal.usda.gov/vocab/FDCFOOD_" --header "ID|LABEL|SubClass Of|source|hasTopConcept|altLabel|IRI|seeAlso|comment|definition|isDefinedBy|historyNote|" --sort "SubClass Of" --strict --export release/fdc-foodvocab.csv
```

