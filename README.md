# Tony Awards Semantic Resource

This repository contains the semantic resource developed by Group 10 for the Open Interoperable Semantic Resources final project.

The project represents information about Tony Award winners between 1982 and 2015. The represented data includes winners, awarded works, award categories, award years and gender categories.

## Group members

| Name | Student ID |
|---|---|
| Tonybingfeng Lin | 230025 |
| Huangkai Chen | 220238 |
| Diego Armenteros Riaza | c200264 |
| Víctor Taboada | 220084 |
## Repository

Project repository:

https://github.com/tony07122004/group10-semantic-requirements

## Repository structure

```text
group10-semantic-requirements/
├── ontology/
│   ├── Ontology.ttl
│   └── Ontology.owl
├── data/
│   └── tony_awards_data.ttl
├── shacl/
│   ├── shapes.ttl
│   ├── report.ttl
│   ├── README_SHACL.md
│   └── evaluation/
│       ├── oops/
│       │   ├── oops_evaluation_before.png
│       │   ├── oops_evaluation_after.png
│       │   └── oops_evaluation_final_no_pitfalls.png
│       └── foops/
│           └── foops_evaluation_final_97.png
├── chowlk/
│   └── diagrama_corregido.png
├── requirements/
│   └── Requirement.csv
├── casos_de_uso.pdf
└── README.md
```

## Ontology

The ontology is available in two serializations:

- `ontology/Ontology.ttl`: OWL ontology in Turtle.
- `ontology/Ontology.owl`: OWL ontology in RDF/XML.

The intended ontology URI is:

```text
https://w3id.org/tony-awards/ontology
```

The intended ontology namespace is:

```text
https://w3id.org/tony-awards/ontology#
```

The intended resource namespace is:

```text
https://w3id.org/tony-awards/resource#
```

These W3ID persistent identifiers have been requested through a pull request to the official W3ID repository:

```text
https://github.com/perma-id/w3id.org/pull/6089
```

Until the W3ID pull request is accepted, the ontology files are available directly in this GitHub repository.

## Main modelling decision

The central modelling decision was to introduce the class:

```text
myOnt:AwardWinning
```

This class represents each concrete award-winning record in the dataset.

Each `myOnt:AwardWinning` record connects:

- the winning person;
- the awarded creative work;
- the award category;
- the award year;
- the gender category.

This avoids modelling the award as a simple binary relation and makes explicit who received the award, for which work, in which category and in which year.

## Main ontology elements

The ontology includes reused classes and custom classes.

### Reused classes

- `foaf:Person`
- `schema:CreativeWork`

### Custom classes

- `myOnt:TonyAward`
- `myOnt:AwardWinning`
- `myOnt:AwardCategory`
- `myOnt:PerformanceAward`
- `myOnt:ActingAward`
- `myOnt:PlayAward`
- `myOnt:MusicalAward`
- `myOnt:BestActorAward`
- `myOnt:BestActressAward`
- `myOnt:GenderCategory`
- `myOnt:MasculineCategory`
- `myOnt:FeminineCategory`

## Object properties

The main object properties are:

- `myOnt:winner`
- `myOnt:awardedForWork`
- `myOnt:hasAwardCategory`
- `myOnt:hasGenderCategory`
- `myOnt:belongsToAward`
- `myOnt:isWinnerOf`
- `myOnt:isWorkAwardedIn`
- `myOnt:isAwardCategoryOf`
- `myOnt:isGenderCategoryOf`
- `myOnt:hasCategory`

## Datatype properties

The main datatype properties are:

- `myOnt:awardYear`
- `myOnt:genderCategory`
- `myOnt:recordIdentifier`
- `myOnt:categoryType`
- `myOnt:categoryLabel`
- `myOnt:workTitle`
- `foaf:name`

## Reused ontological resources

The ontology reuses terms from existing vocabularies:

- FOAF: used to represent people with `foaf:Person` and `foaf:name`.
- Schema.org: used to represent awarded works with `schema:CreativeWork`.
- SKOS: used for preferred labels with `skos:prefLabel`.
- Dublin Core Terms: used for ontology metadata such as title, creator, description, source and license.
- VANN: used to declare the preferred namespace prefix and namespace URI.

## Knowledge Graph

The Knowledge Graph data is available in:

```text
data/tony_awards_data.ttl
```

The data file contains valid examples of Tony Award winning records according to the ontology and the SHACL shapes.

Each award-winning record includes:

- one winner;
- one awarded creative work;
- one award category;
- one gender category;
- one award year;
- one record identifier.

## SHACL validation

The SHACL shapes are available in:

```text
shacl/shapes.ttl
```

The validation report is available in:

```text
shacl/report.ttl
```

The SHACL validation checks different types of constraints:

- cardinality constraints;
- datatype constraints;
- class constraints;
- value range constraints;
- controlled value constraints;
- string pattern constraints;
- closed shape constraints.

The final validation report conforms:

```text
Conforms: True
```

## How to run the SHACL validation

Install pySHACL:

```bash
pip install pyshacl
```

Run the validation:

```bash
python -m pyshacl -s shacl/shapes.ttl -f turtle -o shacl/report.ttl data/tony_awards_data.ttl
```

The output file will be generated at:

```text
shacl/report.ttl
```

## OOPS! ontology evaluation

The ontology was evaluated with OOPS! before and after applying corrections.

Initial OOPS! results detected several pitfalls:

- P04: Creating unconnected ontology elements.
- P10: Missing disjointness.
- P12: Equivalent properties not explicitly declared.
- P13: Inverse relationships not explicitly declared.

The ontology was improved by:

- adding disjointness axioms;
- adding inverse object properties;
- removing disconnected ontology elements;
- replacing duplicated name usage for creative works with `myOnt:workTitle`;
- keeping `myOnt:AwardWinning` as the central n-ary class.

The final OOPS! evaluation reports no pitfalls.

OOPS! screenshots are available in:

```text
shacl/evaluation/oops/
```

Main OOPS! files:

- `shacl/evaluation/oops/oops_evaluation_before.png`
- `shacl/evaluation/oops/oops_evaluation_after.png`
- `shacl/evaluation/oops/oops_evaluation_final_no_pitfalls.png`

## FOOPS! evaluation

The ontology was also evaluated with FOOPS! to assess its FAIRness.

The final FOOPS! score was:

```text
97%
```

FOOPS! screenshot:

```text
shacl/evaluation/foops/foops_evaluation_final_97.png
```

## Conceptual model

The corrected conceptual model diagram is available in:

```text
chowlk/diagrama_corregido.png
```

The diagram shows the main classes and relationships used in the ontology, especially the central `myOnt:AwardWinning` class and its links to persons, creative works, award categories, years and gender categories.

## License

The ontology declares the following license:

```text
https://creativecommons.org/licenses/by/4.0/
```

## Tools used

The following tools were used during the development of the project:

- GitHub for repository management.
- diagrams.net / draw.io for the conceptual model diagram.
- RDF/Turtle for ontology and Knowledge Graph representation.
- OWL for ontology implementation.
- pySHACL for SHACL validation.
- OOPS! for ontology evaluation.
- FOOPS! for FAIRness evaluation.
- RDFLib for converting Turtle to RDF/XML.

## Main project results

- Ontology: `ontology/Ontology.ttl`
- Ontology RDF/XML serialization: `ontology/Ontology.owl`
- Knowledge Graph: `data/tony_awards_data.ttl`
- SHACL shapes: `shacl/shapes.ttl`
- SHACL validation report: `shacl/report.ttl`
- SHACL validation result: `Conforms: True`
- OOPS! final result: no pitfalls detected
- FOOPS! final score: 97%
- W3ID pull request: `https://github.com/perma-id/w3id.org/pull/6089`
