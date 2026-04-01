# FDC Food Vocabulary

## Introduction

Welcome to the USDA [Food DataCentral (FDC)](https://fdc.nal.usda.gov/) Food Vocabulary github repository. 

## Accessing the FDC Food Vocabulary

The **FDC Food Vocabulary** is available in `OWL`, `JSON`, and `CSV` formats. See vocabulary files [in the release directory here:](release/)

## Development

### Preamble

This section is for developers of the **FDC Food Vocabulary**. This vocabulary is built using the [ROBOT](https://robot.obolibrary.org/) command-line tool. To modify the vocabulary it is necessary to setup a the necessary compute requirements for ROBOT by following the instructions from the [ROBOT getting started](https://robot.obolibrary.org/) page. 

The FDC Food Vocabulary is implement in the Web Ontology Language (OWL). It makes use of the Simple Knowledge Organization System (SKOS), as well as the Resource Description Framework (RDF). 

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

