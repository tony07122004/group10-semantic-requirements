# SHACL validation - Tony Awards

## Improved conceptual model

The original conceptual model was improved by introducing the class `myOnt:AwardWinning`.

This class represents each concrete award-winning record in the dataset. Each record links:

- the winning person,
- the awarded work,
- the award category,
- the award year,
- and the gender category.

This model is more accurate because the dataset rows represent award-winning record, not only persons or works.

![Improved conceptual model](diagrama_corregido.png)

## Implemented SHACL shapes and restrictions

The SHACL file contains several shapes checking different kinds of constraints: cardinality, datatype, class, pattern, value range and controlled values.

1. Every `foaf:Person` must have exactly one non-empty `foaf:name`.
2. Every `schema:CreativeWork` must have exactly one non-empty `myOnt:workTitle`.
3. Every `myOnt:AwardCategory` must have one category label.
4. Every `myOnt:AwardCategory` must have one category type, either `Play` or `Musical`.
5. Every `myOnt:AwardCategory` must be linked to `myOnt:TonyAward` through `myOnt:belongsToAward`.
6. Every `myOnt:AwardWinning` must have one record identifier.
7. Every `myOnt:AwardWinning` must have exactly one winner.
8. Every `myOnt:AwardWinning` must be linked to exactly one work.
9. Every `myOnt:AwardWinning` must have exactly one award category.
10. Every `myOnt:AwardWinning` must have exactly one gender category.
11. Every `myOnt:AwardWinning` must have exactly one award year.
12. The award year must be an integer between 1982 and 2015.
13. The gender category literal must be either `masculina` or `femenina`.

## Validation result

The final SHACL validation conforms.

The final result was:

```text
Validation Report
Conforms: True
```

The generated validation report is stored in:

```text
shacl/report.ttl
```

The report contains:

```turtle
[] a sh:ValidationReport ;
    sh:conforms true .
```

## Corrections applied

The data was corrected to obtain a conformant validation result.

The final data file:

- removes intentionally incorrect `Bad_` examples,
- includes valid names for persons,
- includes valid work titles,
- includes valid award categories,
- links each award-winning record to exactly one winner,
- links each award-winning record to exactly one work,
- uses valid years between 1982 and 2015,
- uses only the accepted gender category literals: `masculina` and `femenina`.

## OOPS! ontology evaluation

The ontology was evaluated using OOPS! before and after applying corrections.

Initial OOPS! results detected several pitfalls:

- P04: Creating unconnected ontology elements.
- P10: Missing disjointness.
- P12: Equivalent properties not explicitly declared.
- P13: Inverse relationships not explicitly declared.

The ontology was improved by:

- Adding disjointness axioms.
- Adding inverse object properties.
- Removing disconnected ontology elements.
- Replacing duplicated name usage for creative works with `myOnt:workTitle`.
- Keeping `myOnt:AwardWinning` as the central n-ary class that connects winners, works, award categories, years and gender categories.

Final OOPS! result reports:

```text
No pitfalls detected
```

### OOPS! evaluation screenshots

- Initial evaluation: `oops_evaluation_before.png`
- Intermediate evaluation: `oops_evaluation_after.png`
- Final evaluation: `oops_evaluation_final_no_pitfalls.png`

## FOOPS! evaluation

The ontology was also evaluated using FOOPS! to assess its FAIRness.

The final FOOPS! score was:

```text
97%
```

### FOOPS! evaluation screenshot

- Final FOOPS! evaluation: `foops_evaluation_final_97.png`

## Final validation summary

Final project results:

- SHACL validation: `Conforms: True`
- OOPS! evaluation: `No pitfalls detected`
- FOOPS! evaluation: `97%`
