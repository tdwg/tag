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

![diagram of a single blank node resource](images/single_bn.png)

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