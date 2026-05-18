# group10-semantic-requirements
Group 10 project: requirements + use cases + discarded fields + datasets (Tony Awards).
# Tony Awards Semantic Resource

This repository contains the semantic resource developed by Group 10 for the Open Interoperable Semantic Resources final project.

The project represents information about Tony Award winners between 1982 and 2015, including winners, awarded works, award categories, award years and gender categories.

## Main files

- `ontology/Ontology.ttl`: OWL ontology in Turtle.
- `ontology/Ontology.owl`: OWL ontology in RDF/XML.
- `data/tony_awards_data.ttl`: Knowledge Graph data.
- `shacl/shapes.ttl`: SHACL shapes.
- `shacl/report.ttl`: SHACL validation report.
- `shacl/README_SHACL.md`: SHACL and evaluation explanation.
- `chowlk/diagrama_corregido.png`: conceptual model diagram.
- `evaluation/oops/`: OOPS! evaluation screenshots.
- `evaluation/foops_evaluation_final_97.png`: FOOPS! evaluation screenshot.

## Ontology namespace

`https://w3id.org/tony-awards/ontology#`

## Main modelling decision

The central class is `myOnt:AwardWinning`, which represents each concrete award-winning record. It connects the winner, the awarded work, the award category, the year and the gender category.

## Validation and evaluation

The repository includes:
- SHACL validation with pySHACL.
- OOPS! ontology evaluation.
- FOOPS! FAIRness evaluation.
