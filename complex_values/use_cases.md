# Complex values use cases

## Humboldt Extension (draft addition to Darwin Core)

Submitted by Wesley Hochachka, eBird, 2022-11-02

Observations of organisms are essentially always imperfect in the sense that not all individuals that are present within the surveyed region are detected during an observation/collection process.  One of the major components of analyses of biodiversity-observation data is to account for this imperfect detection.  Variation in the probability of detection can be thought of as being a function of observation/collection "effort", with greater effort leading to a greater proportion of individual organisms actually being detected (i.e. increased detection rate).  Different observation/collection processes will have different measures of effort, and often multiple and independent measures of effort will exist.  An example of this is with data collected by the citizen science project eBird (https://ebird.org/home), for which experience has led us to identify 4 separate facets to observation effort that are important for describing variation in detection rate: duration of observation periods, distance travelled during the observation period, area searched within the observation period, and the number of observers within the group that was making observations.  Only one of these 4 facets of effort is described within by Darwin Core by dedicated terms: duration of the observation is covered by the two Darwin Core terms eventDuration and eventDurationUnits.  The other three do not have dedicated fields that describe variation in these aspects of effort (although kludges could be used to force this information into various fields in the existing Darwin Core and the current proposal for the Humboldt Extension to Darwin Core).  While eBird has these four facets of effort, other forms of data collection will have different measures of effort that also will not have dedicated terms.  Rather than trying to create terms for all possible measures of effort, I suspect that the more logical and generalizable way of incorporating information on these three aspects of effort will be to fit them into the pair of terms within the Humboldt Extension: samplingEffortValue and samplingEffortUnit.  Effectively, allowing placement of multiple types of effort information within these two Humbolt Extension terms is the equivalent of creating a sub-table within a database that is dedicated to store the information on observation/collection effort.  I believe that it makes sense to store all potential information about effort as a unit because these effort data all would need to be accessed and used in the same way by anyone fitting models to the data.  To my mind, the major question remaining is whether there is a standardized form in which we can suggest that these multiple data types should be stored as a unit within a single term/database field?

It's not so much that there's an absolute need to have the effort information grouped together, but more that it would make the end-user experience less painful if all facets of observation/collection effort are grouped in one location.  Below is a description of the specific case for eBird:

The publicly distributed data from eBird come have been collected using multiple "protocols" that each have different types of effort information associated with them:
- "traveling count": one or more observers moving over the course of an observation period (3 components to effort: duration of observation period, distance travelled, number of observers)
- "stationary count": one or more observers remaining stationary throughout an observation period (2 components of effort: duration of observation period, number of observers)
- "area search": one or more observers systematically making observations within a contiguous area (3 components of effort: duration of observation period, area in which observations were made, number of observers)
- "incidental": one or more species reported potentially as an instantaneous observation; this is the equivalent of a presence-only observation in other citizen science projects such as iNaturalist (i.e. no effort information recorded)

In order to facilitate end users' recognition of the existence of these multiple protocol types within this single publicly distributed data product, and that the types of effort information vary in both type and quantity, I think that it would be useful to have all of the effort information placed in very close proximity within a downloaded set of data.  Duration of observation period already has specific fields within Darwin Core (eventDuration and eventDurationUnits), so the question is how to package the other effort information: distance travelled, area searched, number of observers).  For the purpose of illustration, a JSON object could contain records such as these:

```
      {"effort": {"distance": 1.2, "area": null, "nObservers": 2}}     for a travelling count
      {"effort": {"distance": null, "area": null, "nObservers": 1}}     for a stationary count
      {"effort": {"distance": null, "area": null, "nObservers": null}}  for an incidental count
```
   
The key point that I want to communicate is the variation in both quantities and types of effort existing within the same collection of data.  Grouping together as much of the effort information as possible would make the data more self-documenting, because users have a bad habit of not reading documentation in my experience.

## Agent information

Submitted by Steve Baskauf, TDWG TAG, 2022-11-03

When human-readable information is provided about authors of publications, recorders of occurrences, determiners of taxa, etc. we can provide important information by indicating the role played by each person and their affiliation. The order in which the people are listed may also be important. Thinking more broadly, we should probably consider these to be agents rather than people, since occurrences may be recorded by machines and determiners may be software agents. So there may also be a need to identify the type of agent (human, software, camera, etc.).

For example, the prior TDWG standard "Floristic Regions of the World" (<http://www.tdwg.org/standards/104>) has an author, a translator, and an editor. That information is captured in tabular form several places ([here](https://github.com/tdwg/rs.tdwg.org/blob/master/docs/docs-authors.csv) and [here](https://github.com/tdwg/rs.tdwg.org/blob/master/docs-roles/docs-roles.csv)) and can be obtained as RDF [here](http://rs.tdwg.org/frw/doc/book.ttl) and [here](rs.tdwg.org/dump/docs-roles.ttl), but none of these forms are simply expressed or serialized in an easily consumable form. 

Example data:

```
[
    {
        "@id": "http://viaf.org/viaf/19771885", 
        "foaf:name": "Armen Leonovich Takhtajan", 
        "role": "http://www.wikidata.org/entity/Q482980"
    },
    {
        "@id": "http://viaf.org/viaf/91310738", 
        "foaf:name": "Theodore J. Crovello", 
        "role": "http://www.wikidata.org/entity/Q333634"
    },
    {
        "@id": "http://viaf.org/viaf/61620062"", 
        "foaf:name": "Arthur Cronquist", 
        "role": "http://www.wikidata.org/entity/Q1607826"
    }
]
```

In another example, an organism may be identified by a machine-learning algorithm (e.g. image recognition in iNaturalist or bird song recognition in Merlin), with that identification verified at a later date by a human expert. How can the agent identity and type be grouped while also providing the ability to specify multiple values?

Example data for <https://macaulaylibrary.org/asset/451198811> (sound recording docummenting an occurrence of Worm-eating Warbler)

```
[
    {
        "agent_name": "Merlin",
        "agent_type": "software"
        "dwc:scientificName": "Helmitheros vermivorum",
        "dwc:dateIdentified": "2022-05-20"
    },
    {
        "agent_name": "Steven J. Baskauf",
        "agent_type": "person"
        "dwc:scientificName": "Helmitheros vermivorum",
        "dwc:dateIdentified": "2022-05-21"
    }
]
```

## Multiple life stages/sexes in museum sample

Use case inspired by https://github.com/tdwg/dwc-qa/issues/192, 2022-10-28

A museum stores multiple individuals with several life stages and sexes retrieved from a single material sample, with a single catalog number. How can this information be recorded under a single record?

Example data:

```
[
    {
        "dwc:individualCount": 5,
        "dwc:sex": "male",
        "dwc:lifeStage": "nymph"
    },
    {
        "dwc:individualCount": 3,
        "dwc:sex": "female",
        "dwc:lifeStage": "nymph"
    },
    {
        "dwc:individualCount": 1,
        "dwc:sex": "male",
        "dwc:lifeStage": "adult"
    },
    {
        "dwc:individualCount": 4,
        "dwc:sex": "female",
        "dwc:lifeStage": "adult"
    }
]
```

## Vernacular names

Submitted by Ben Norton, TDWG TAG, at the 2022-11-07 working session

Vernacular name record records include not only the name string itself, but also the language and if it's the primary one. When there is more than one vernacular name per species, how does one maintain the connection between the metadata statements about a particular vernacular name?

Example data:

```
[
    {
        "dwc:vernacularName": "cougar",
        "dc:language": "en",
        "isPreferred": true
    },
    {
        "dwc:vernacularName": "panther",
        "dc:language": "en",
        "isPreferred": false
    },
    {
        "dwc:vernacularName": "puma",
        "dc:language": "es",
        "isPreferred": true
    }
]
```

## Latimer Core

Ben Norton

## Humboldt Core (ID vs. IRI terms)

From 2023-01-18 task group meeting

Values for the terms `dwc:samplingPerformedBy` and `dwc:identifiedBy` may be people who also have ORCIDs. If there were a single value, then the IRI analogs (`dwciri:samplingPerformedBy` and `dwciri:identifiedBy`) could be used. However, multiple IRI values cannot be providided for the IRI analogs. Thus the "ID" terms might be used instead (`dwc:samplingPerformedByID` and `dwciri:identifiedByID`) since it is permissible to provide multiple values separated by a vertical bar. It would be preferable to use the IRI terms, but currently there is not a way to express multiple values outside of RDF (i.e. in a table).

# JSON-LD

Here's what [unordered multiple values look like in JSON-LD](https://www.w3.org/TR/json-ld11/#sets-and-lists):

```
{
  "@context": {
    "dwciri": "http://rs.tdwg.org/dwc/iri/"
  },
  "@id": "http://arctos.database.museum/guid/MSB:Mamm:233627",
  "dwciri:identifiedBy": [
    "https://orcid.org/0000-0003-4365-3135",
    "https://orcid.org/0000-0003-1144-0290",
    "https://orcid.org/0000-0003-1617-5895"
  ]
}
```

It serializes to RDF N-Quads as:

```
<http://arctos.database.museum/guid/MSB:Mamm:233627> <http://rs.tdwg.org/dwc/iri/identifiedBy> "https://orcid.org/0000-0003-1144-0290" .
<http://arctos.database.museum/guid/MSB:Mamm:233627> <http://rs.tdwg.org/dwc/iri/identifiedBy> "https://orcid.org/0000-0003-1617-5895" .
<http://arctos.database.museum/guid/MSB:Mamm:233627> <http://rs.tdwg.org/dwc/iri/identifiedBy> "https://orcid.org/0000-0003-4365-3135" .
```

Here's what an [ordered list looks like in JSON-LD](https://www.w3.org/TR/json-ld11/#lists):

```
{
  "@context": {
    "dwciri": "http://rs.tdwg.org/dwc/iri/"
  },
  "@id": "http://arctos.database.museum/guid/MSB:Mamm:233627",
  "dwciri:identifiedBy": {
    "@list": [
      "https://orcid.org/0000-0003-4365-3135",
      "https://orcid.org/0000-0003-1144-0290",
      "https://orcid.org/0000-0003-1617-5895"
    ]
  }
}
```

It serializes to RDF N-Quads as:

```
<http://arctos.database.museum/guid/MSB:Mamm:233627> <http://rs.tdwg.org/dwc/iri/identifiedBy> _:b0 .
_:b0 <http://www.w3.org/1999/02/22-rdf-syntax-ns#first> "https://orcid.org/0000-0003-4365-3135" .
_:b0 <http://www.w3.org/1999/02/22-rdf-syntax-ns#rest> _:b1 .
_:b1 <http://www.w3.org/1999/02/22-rdf-syntax-ns#first> "https://orcid.org/0000-0003-1144-0290" .
_:b1 <http://www.w3.org/1999/02/22-rdf-syntax-ns#rest> _:b2 .
_:b2 <http://www.w3.org/1999/02/22-rdf-syntax-ns#first> "https://orcid.org/0000-0003-1617-5895" .
_:b2 <http://www.w3.org/1999/02/22-rdf-syntax-ns#rest> <http://www.w3.org/1999/02/22-rdf-syntax-ns#nil> .
```

# See also

[Examples of list values used for multiple Regions of Interest and Service Access Points](https://github.com/tdwg/ac/blob/master/roi-recipes.md) (discussed on the [existing precedents page](https://github.com/tdwg/tag/blob/master/complex_values/existing_precedents.md)).

----
Revised 2023-01-18
