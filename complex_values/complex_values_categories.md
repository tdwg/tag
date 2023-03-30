# Complex values categories

## Multiple literal values

![multiple literal value diagram](images/multiple_literals.png)

**Current tabular data serialization**

```
"skin | skull | skeleton"
```

**RDF Turtle**

```
@prefix dwc: <http://rs.tdwg.org/dwc/terms/> .
[] dwc:preparations "skin",
                    "skull",
                    "skeleton".
```

**JSON-LD with CURIES**

```
{
  "@context": {
    "dwc": "http://rs.tdwg.org/dwc/terms/"
  },
  "dwc:preparations": [
    "skin",
    "skull",
    "skeleton"
  ]
}
```

**Simplified JSON**

```
{
  "preparations": [
    "skin",
    "skull",
    "skeleton"
  ]
}
```

**JSON-LD without CURIES**

```
{
  "@context": {
    "preparations": "http://rs.tdwg.org/dwc/terms/preparations"
  },
  "preparations": [
    "skin",
    "skull",
    "skeleton"
  ]
}
```

## Multiple IRI-denoted values

![multiple IRI value diagram](images/multiple_iri.png)

**RDF Turtle**

```
@prefix dwciri: <http://rs.tdwg.org/dwc/iri/> .
[] dwciri:recordedBy <https://orcid.org/0000-0002-1772-1045>,
                  <https://orcid.org/0000-0003-1715-4850>,
                  <https://orcid.org/0000-0003-4365-3135>.
```

**JSON-LD with CURIES**

```
{
  "@context": {
    "dwciri": "http://rs.tdwg.org/dwc/iri/"
  },
  "dwcdwciri:recordedBy": [
    {"@id": "https://orcid.org/0000-0002-1772-1045"},
    {"@id": "https://orcid.org/0000-0003-1715-4850"},
    {"@id": "https://orcid.org/0000-0003-4365-3135"}
  ]
}
```

**Simplified JSON**

```
{
  "recordedBy": [
    "https://orcid.org/0000-0002-1772-1045",
    "https://orcid.org/0000-0003-1715-4850",
    "https://orcid.org/0000-0003-4365-3135"
  ]
}
```

**JSON-LD without CURIES**

```
{
  "@context": {
    "recordedBy": {
        "@id": "http://rs.tdwg.org/dwc/iri/recordedBy",
        "@type": "@id"
    }
  },
  "recordedBy": [
    "https://orcid.org/0000-0002-1772-1045",
    "https://orcid.org/0000-0003-1715-4850",
    "https://orcid.org/0000-0003-4365-3135"
  ]
}
```

## Single blank node value

![diagram of a single blank node resource value](images/single_bn.png)

**RDF Turtle**

```
@prefix dwciri: <http://rs.tdwg.org/dwc/iri/> .
@prefix dwc: <http://rs.tdwg.org/dwc/terms/> .
[] dwciri:eventDuration [
    dwc:measurementValue 12;
    dwc:measurementUnit "h"
    ].
```

**JSON-LD with CURIES**

```
{
  "@context": {
    "dwciri": "http://rs.tdwg.org/dwc/iri/",
    "dwc": "http://rs.tdwg.org/dwc/terms/"
  },
  "dwciri:eventDuration": {
    "dwc:measurementValue": 12,
    "dwc:measurementUnit": "h"
  }
}
```

**Simplified JSON**

```
{
  "eventDuration": {
    "measurementValue": 12,
    "measurementUnit": "h"
  }
}
```

**JSON-LD without CURIES**

```
{
  "@context": {
    "eventDuration": {
        "@id": "http://rs.tdwg.org/dwc/iri/eventDuration"
    },
    "measurementValue": {
        "@id": "http://rs.tdwg.org/dwc/terms/measurementValue"
    },
    "measurementUnit": {
        "@id": "http://rs.tdwg.org/dwc/terms/measurementUnit"
    }
  },
  "eventDuration": {
    "measurementValue": 12,
    "measurementUnit": "h"
  }
}
```

## Multiple blank node values

![diagram of a multiple blank node resource values](images/multiple_bn.png)

**RDF Turtle**

```
@prefix dwciri: <http://rs.tdwg.org/dwc/iri/> .
@prefix dc: <http://purl.org/dc/elements/1.1/> .
@prefix skosxl: <http://www.w3.org/2008/05/skos-xl#> .
@prefix ex: <http://example.org/> .
[] dwciri:vernacularName [
    skosxl:literalForm "Mountain Lion";
    dc:language "en";
    ex:isPrimary true
    ],
    [
    skosxl:literalForm "Cougar";
    dc:language "en";
    ex:isPrimary false
    ].
```

**JSON-LD with CURIES**

```
{
  "@context": {
    "dwciri": "http://rs.tdwg.org/dwc/iri/",
    "dc": "http://purl.org/dc/elements/1.1/",
    "skosxl": "http://www.w3.org/2008/05/skos-xl#",
    "ex": "http://example.org/"
  },
  "dwciri:vernacularName": [
    {
    "skosxl:literalForm": "Mountain Lion",
    "dc:language": "en",
    "ex:isPrimary": true
    },
    {
    "skosxl:literalForm": "Cougar",
    "dc:language": "en",
    "ex:isPrimary": false
    }
  ]
}
```

**Simplified JSON**

```
{
  "vernacularName": [
    {
    "literalForm": "Mountain Lion",
    "language": "en",
    "isPrimary": true
    },
    {
    "literalForm": "Cougar",
    "language": "en",
    "isPrimary": false
    }
  ]
}
```

**JSON-LD without CURIES**

```
{
  "@context": {
    "vernacularName": {
        "@id": "http://rs.tdwg.org/dwc/iri/vernacularName"
    },
    "literalForm": {
        "@id": "http://www.w3.org/2008/05/skos-xl#literalForm"
    },
    "language": {
        "@id": "http://purl.org/dc/elements/1.1/language"
    },
    "isPrimary": {
        "@id": "http://example.org/isPrimary"
    }
  },
  "vernacularName": [
    {
    "literalForm": "Mountain Lion",
    "language": "en",
    "isPrimary": true
    },
    {
    "literalForm": "Cougar",
    "language": "en",
    "isPrimary": false
    }
  ]
}
```
