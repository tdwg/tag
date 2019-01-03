# SKOS-XL as a general model for labels within TDWG standards

Steve Baskauf  2019-01-02

Note: The term IRI (Internationalized Resource Identifier) can be considered to be synonymous with URI (Uniform Resource Identifier) throughout this document.

## Background

Within several existing TDWG vocabularies and vocabularies under development, there is a need for a system to document multiple labels for entities of interest.  This includes tracking the provenance of those labels, and asserting relationships between the labels and the entities they identify.  

In current TDWG standards, there are several features designed to facilitate the use of what are effectively labels and may be variously known as "names", "literals", "string values", and "verbatim values".

Within Darwin Core, the [dwciri: namespace](https://dwc.tdwg.org/rdf/#25-terms-in-the-dwciri-namespace-normative) (`http://rs.tdwg.org/dwc/iri/`) was created to differentiate between terms whose values were IRI identifiers for entities and terms whose values were string labels (literals) for entities.  Similarly, within Audubon Core, there exist pairs of analogous terms where one term is expected to have a IRI identifier as a value and the other is expected to have a string label (literal) as a value (for example, [ac:reviewer for IRI values and ac:reviewerLiteral for literal values](http://tdwg.github.io/ac/termlist/#ac_reviewer)).  

Darwin Core also contains sets of analogous terms where the value of one term is expected to contain an unprocessed string documenting the original verbatim value for the property (e.g. dwc:verbatimLatitude) and another term is expected to contain a standardized value for the property (e.g. dwc:decimalLatitude).

In controlled vocabularies (currently under development, but none yet having reached the status of standard), a value that is an abstract concept may have preferred labels in different languages, alternative (but non-preferred labels) in different langauges, and possibly many known erroneous labels for that concept. The [TDWG Standards Documentation Specification](https://github.com/tdwg/vocab/blob/master/sds/documentation-specification.md) suggests in [Section 4.5.2](https://github.com/tdwg/vocab/blob/master/sds/documentation-specification.md#45-metadata-properties-for-describing-vocabulary-terms) that the SKOS terms skos:prefLabel and skos:altLabel be used to indicate preferred and alternate labels in various languages, but does not suggest any way to track the provenance of those labels.

What each of these situations has in common is that they provide a partial solution to the problem of tracking what are in essence labels for abstract entities.  Although they provide a way to link to associated labels, they do not provide a mechanism for describing metadata about those labels or indicating their origin.

## SKOS-XL

The [Simple Knowledge Organization System (SKOS)](https://www.w3.org/TR/skos-primer/) is a ratified W3C standard for developing concept schemes and is based on [ISO Standards 25964-1 and -2 for development of thesauri](https://www.niso.org/schemas/iso25964).  The [SKOS eXtension for Labels (SKOS-XL)](https://www.w3.org/TR/skos-reference/#xl) defines an optional extension to the SKOS that supports identifying, describing, and linking labels.  Although designed to enhance the description of labels for SKOS concepts that are part of thesauri, the [SKOS labeling properties are not constrained to be used exclusively with SKOS concepts](https://www.w3.org/TR/skos-reference/#L1541).  SKOS-XL terms can be used to describe labels associated with any kind of resource.  

Although SKOS-XL terms can be used with labels associated with any kind of thing, there are certain restrictions and entailments associated with SKOS-XL terms (see the [SKOS-XL Namespace Document](https://www.w3.org/TR/skos-reference/skos-xl.html) for detailed definitions).  Additionally, there are certain restrictions in the use of SKOS-XL terms that are not included in the term definitions, but that are required for consistency with the SKOS model (in particular, [the requirement that there be no more than one preferred label for a resource in each language](https://www.w3.org/TR/skos-reference/#L1567)).  Nevertheless, it appears that the SKOS-XL extension is flexible enough to be used in most of the situations where TDWG has an interest in documenting names, verbatim values, and other sorts of labels.

## Getty Thesaurus example

A good model for using SKOS-XL to manage label information is the Getty Thesauri.  For example, see the machine-readable metadata for the [Getty Thesaurus of Geographic Names entry for China](http://vocab.getty.edu/page/tgn/1000111) in [RDF/Turtle](http://vocab.getty.edu/tgn/1000111.ttl) or [JSON-LD](http://vocab.getty.edu/tgn/1000111.jsonld).  See the Appendix for an abbreviation of this example in Turtle.

## Conventional databases vs. Linked Data

SKOS-XL is an abstract model that describes how things are related to labels that denote them.  Thus, it is possible to create a conventional database based on this model.  However, SKOS-XL is also designted to enable data to be expressed as a Linked Data graph.  Thus modeling label data on SKOS-XL has the advantage of enabling, but not requiring the data to be expressed as Linked Data.

In the following examples, the data will first be expressed in conventional tables, then serialized as machine-readable Linked Data.

# Nomenclatural examples

The following examples are related to JSON examples discussed in [Issue #24](https://github.com/tdwg/tnc/issues/24#issuecomment-445436128) of the [Taxon Names and Concepts Interest Group](https://github.com/tdwg/tnc).  The example involves names having a history something like this (please pardon any misunderstanding  on my part of the technical details of the botanical Code): 

Carl Müller published the name *Dicranum braunii* for a moss, indicated by:

`Dicranum braunii Müll. Hal.`

but the publication was invalid. Roelof Benjamin van den Bosch and Cornelius Marinus van der Sande Lacoste published the same name in a valid publication:

`Dicranum braunii Müll. Hal. ex Bosch & Sande Lac.`

Jean Édouard Gabriel Narcisse Paris moved the species to a new genus, *Dicranoloma*:

`Dicranoloma braunii (Bosch & Sande Lac.) Paris`

These examples are intended to show how SKOS-XL could work in several TDWG contexts.  They don't constitute a proposal for term names.

## People tables

The example includes four people.  For convenience, I used the [Tropicos IRI](http://www.tropicos.org/PersonSearch.aspx) as a unique identifier to serve as the primary key for each person.  Data about the four people are in the table [person.csv](person.csv).  Each row in that table represents a curated record for that person, and includes information about that person that is NOT label (names, abbreviations, etc.) information.  Since the focus of this example is description and provenance of labels, I haven't made any attempt to show how the provenance of this other information might be documented. 

Each row in the table [personLabels.csv](personLabels.csv) represents an instance of a skosxl:Label.  Each label has been assigned a unique UUID identifier to distinguish it from other labels.  The literal value of the label is designated by the property skosxl:literalForm, and the foreign key linking the label to the person it denotes is in the labelOf column.  In this example, the only other column in this table is the type column, which indicates whether a particular label is consiedered the one preferred label for that person, or one of several alternate labels for that person.  However, there could be many additional columns in this table to indicate additional metadata about the label, such as its source, the date it was added to the database, etc.  See the Appendix for examples of additional properties.

## Machine-readable metadata about people

The information in these two tables has been turned into RDF/Turtle in the file [skosxl-person.ttl](skosxl-person.ttl).  RDF/Turtle is used to make the example more readable, but it would be trivial to serialize the data in another machine-readable format such as JSON-LD.  Here is a snippet from that file:

```turtle
@prefix tnc: <http://rs.tdwg.org/tnc/> .
@prefix tex: <http://rs.tdwg.org/tnc/example/> .

<http://www.tropicos.org/Person/10766> a foaf:Person;
	skosxl:prefLabel tex:62eb5840-c7fd-4965-b080-b69aa57f71ae;
	skosxl:altLabel tex:1be0ca20-0e29-412a-9092-e41b1a40b272;
	foaf:familyName "van der Sande Lacoste";
	foaf:givenName "Cornelius Marinus";
	tnc:ipniId "8882-1";
	tnc:country "Netherlands";
	tnc:dateRange "1815-1887".

tex:62eb5840-c7fd-4965-b080-b69aa57f71ae a skosxl:Label;
	skosxl:literalForm "Cornelius Marinus van der Sande Lacoste";
	dcterms:identifier "62eb5840-c7fd-4965-b080-b69aa57f71ae".

tex:1be0ca20-0e29-412a-9092-e41b1a40b272 a skosxl:Label;
	skosxl:literalForm "C.M. van der Sande Lacoste";
	dcterms:identifier "1be0ca20-0e29-412a-9092-e41b1a40b272".
```

The namespace `tnc:` is a fake namespace that represents possible future terms created as part of the efforts of the Taxonomic Names and Concepts Interest Group.  The fake tnc: terms could be replaced by terms from some other well-known vocabulary.  

The UUIDs that identify the skosxl:label instances have been turned into IRIs by appending them to another fake namespace `tex:`, which could represent any domain name used to resolve the IRI.  In the description of the skosxl:Label instances, the term dcterms:identifier is used to indicate that the raw UUID is the identifier for the label.

The links between the person and the labels were made using the skosxl:prefLabel and skosxl:altLabel according to the values given in the type column of the [personLabel.csv table](https://github.com/tdwg/tag/blob/master/skos-xl/personLabels.csv).  

An important feature of SKOS-XL is that vanilla SKOS labels (skos:prefLabel, skos:altLabel, and skos:hiddenLabel) can be inferred by a ["dumb-down" process based on sub-property chain axioms](https://www.w3.org/TR/skos-reference/#L780).  Thus, the RDF shown in the example entails the following:

```
<http://www.tropicos.org/Person/10766> a foaf:Person;
	skos:prefLabel "Cornelius Marinus van der Sande Lacoste";
	skos:altLabel "C.M. van der Sande Lacoste".
```

If machine-readable data were made available, for ease of use it would be desirable to include these entailed SKOS label relationships.  However, it would not be necessary to store the relationship in the raw data since it can be inferred from the SKOS-XL metadata.  

The skosxl:literalForm string values do not include language tags, since names don't necessarily correspond to particular languages.  However, if desired, the SKOS-XL label table could include additional prefLabel instances in languages using other character sets such as "ru" for Cyrillic or "hans" for simplified Chinese characters.

## Organism names tables

The nomenclatural example includes three "name things".  I am purposefully avoiding using a more specific term to indicate what they are.  Rather, I'll describe what a "name thing" is based on its properties and let the reader apply his or her own termanology. But to be clear, a "name thing" is not a string - it's an abstract thing that has a label that is a string.

A name thing can have one "correct" (i.e. preferred) label.  In the first instance, the correct label (skosxl:prefLabel literal form) is "Dicranum braunii Müll. Hal.".  

A name thing can also have zero to many incorrect labels.  In the first instance, the label "Dicranum braunii Mull. Hal." is incorrect because the umlaut is missing from the "u" in "Müll.", either because of human entry error or because of problems cause by bad character set conversion. In the third instance,  the incorrect label "Dicranum braunii Müll.Hal. ex Bosch & Sande Lac." differs from the correct label "Dicranum braunii Müll. Hal. ex Bosch & Sande Lac." by a missing space after the first period.  In every case, the incorrect label is caused by some sort of typographical error or inconsistent application of formatting rules, not because the creator of the label intended for it to be different.

Whether the incorrect label is identified as an [altLabel or hiddenLabel](https://www.w3.org/TR/skos-reference/#L2007) is somewhat arbitrary depending on whether we consider that the incorrect label should really not be seen by users, or should be displayed as a possible alternative.  In any case, the prefLabel should be substituded for the incorrect label when displaying the label to users as they view information about the name thing.

The [nameThing.csv](nameThing.csv) table includes very little information about the nameThing (only the code that governs it).  In contrast, the [nameLabels.csv](nameLabels.csv) table of skosxl:label instances has a number of fields where components of the label are the parsed out.  The decision to place a field in the skosxl:label table rather than in the nameThing table depends primarily on whether we believe that field can have only a single value per nameThing, or many values.  For example, if our concept of what a nameThing is dictates that a single name thing can only ever have one genus string and one specific epithet string (i.e. we believe that orthographic variants represent different name things), then the tnc_genus and tnc_specificEpithet columns should be moved to the nameThing table.  The decision of how to place these fields should be based on the practicalities of how data are expected to be received, processed, stored, and exposed, rather than on philosophical beliefs about what a "name thing" is.  

For readability, I used values like "thing1" as the primary key in the [nameThing.csv](nameThing.csv) table.  In reality, one would generate UUIDs or use some systematic method for assigning unique identifiers to the name things.  

In the [nameLabels.csv](nameLabels.csv) table, the labelOf column is the foreign key that relates the skosxl:label instance to the nameThing that it denotes.

The [nameLabels.csv](nameLabels.csv) table also includes some columns that indicate how skosxl:label instances are related to other skosxl:label instances.  Because there is only a single prefLabel for each nameThing, every altLabel should be able to be linked to its corresponding prefLabel by a property that indicates how they are related.  The columns tnc_orthErrorCorrection and tnc_normalizedTo indicate the relationship is due to spelling and formatting errors respectively.

## Join tables

There are two join tables that indicate how nameThings are related to people and other name things ([thing-author-relationships.csv](thing-author-relationships.csv) and [nameThingRelationships.csv](nameThingRelationships.csv) respectively).  The nameThing/author relationships include: author, originalAuthor, and exAuthor.  The nameThing/nameThing relationships include hasBasionym and has Designation (not sure whether these are actually correct terms, but hopefully they illustrate the idea that name entities can be related to each other).

## Machine-readable metadata about organism names

The data in the nameThing.csv, nameLabels.csv, thing-author-relationships.csv, and nameThingRelationships.csv tables have been combined in machine-readable form in the file [skosxl-name.ttl](skosxl-name.ttl).  Here is a snippet of RDF/Turtle from that file:

```turtle
tnc:normalizedTo rdfs:subPropertyOf skosxl:labelRelation.
tnc:orthErrorCorrection rdfs:subPropertyOf skosxl:labelRelation.

tex:thing1 a tnc:NameThing;
	skosxl:prefLabel tex:f92c1382-408b-5790-abc3-f158178be286;
	skosxl:altLabel tex:bf6d8361-1cb7-580a-bd3f-dc8bea94b893;
	tnc:author <http://www.tropicos.org/Person/2>;
	tnc:code "botanical".

tex:f92c1382-408b-5790-abc3-f158178be286 a skosxl:Label;
	skosxl:literalForm "Dicranum braunii Müll. Hal.";
	tnc:authorship "Müll. Hal.";
	tnc:canonicalName "Dicranum braunii";
	dcterms:identifier "f92c1382-408b-5790-abc3-f158178be286";
	tnc:genus "Dicranum";
	tnc:specificEpithet "braunii".

tex:bf6d8361-1cb7-580a-bd3f-dc8bea94b893 a skosxl:Label;
	skosxl:literalForm "Dicranum braunii Mull. Hal.";
	tnc:authorship "Mull. Hal.";
	tnc:canonicalName "Dicranum braunii";
	dcterms:identifier "bf6d8361-1cb7-580a-bd3f-dc8bea94b893";
	tnc:genus "Dicranum";
	tnc:specificEpithet "braunii";
	tnc:orthErrorCorrection tex:f92c1382-408b-5790-abc3-f158178be286.
```
In this example, the UUIDs for the strings were generated using the [Global Names Parser](http://parser.globalnames.org/).  The generation process is determinstic, so any particular string of characters will always generate the same UUID.  As before, the UUIDs have been turned into IRIs by appending them to the fake namespace `tex:`. 

As in the earlier RDF/Turtle file, skosxl:prefLabel and skosxl:altLabel are used to link the nameThings to instances of their labels.  In addition, the made-up term tnc:author links the nameThing to its author and the made-up term tnc:orthErrorCorrection links the mispelled label to the correct one. The SKOS-XL specification [defines the property skosxl:labelRelation specifically to serve as a superproperty for more specific subproperties](https://www.w3.org/TR/skos-reference/#L1193) that refine the relationship between labels.  Such refinement was accomplished by the definitions:

```
tnc:normalizedTo rdfs:subPropertyOf skosxl:labelRelation.
tnc:orthErrorCorrection rdfs:subPropertyOf skosxl:labelRelation.
```

at the beginning of the document.  


# Appendix - XKOS-XL used in the Getty Thesaurus of Geographic Names entry for China

The full dataset can be downloade from <http://vocab.getty.edu/tgn/1000111.ttl>

```turtle
@prefix aat: <http://vocab.getty.edu/aat/> .
@prefix dc: <http://purl.org/dc/elements/1.1/> .
@prefix dct: <http://purl.org/dc/terms/> .
@prefix gvp: <http://vocab.getty.edu/ontology#> .
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
@prefix skosxl: <http://www.w3.org/2008/05/skos-xl#> .
@prefix tgn: <http://vocab.getty.edu/tgn/> .
@prefix tgn_contrib: <http://vocab.getty.edu/tgn/contrib/> .
@prefix tgn_source: <http://vocab.getty.edu/tgn/source/> .
@prefix tgn_term: <http://vocab.getty.edu/tgn/term/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

tgn:1000111 a gvp:Subject , skos:Concept , gvp:AdminPlaceConcept ;
	skosxl:prefLabel tgn_term:158-en , tgn_term:1002193462-zh ;
	skosxl:altLabel tgn_term:143323-en .
tgn_term:158-en a skosxl:Label ;
	gvp:term "China"@en ;
	gvp:displayOrder "4"^^xsd:positiveInteger ;
	skosxl:literalForm "China"@en ;
	gvp:termPOS <http://vocab.getty.edu/term/POS/Noun> ;
	dct:contributor tgn_contrib:10000000 , tgn_contrib:10000002 , tgn_contrib:10000001 , tgn_contrib:10000003 ;
	gvp:contributorNonPreferred tgn_contrib:10000000 , tgn_contrib:10000002 , tgn_contrib:10000001 , tgn_contrib:10000003 ;
	dct:source tgn_source:9006303 , tgn_source:9006449 , tgn_source:2009007144 , tgn_source:2009007639 , tgn_source:9004779-term-158 , tgn_source:9004802-term-158 , tgn_source:9004966-term-158 ;
	gvp:sourceNonPreferred tgn_source:2009007144 , tgn_source:2009007639 ;
	dc:identifier "158" ;
	dct:language aat:300388277 .
tgn_term:1002193462-zh a skosxl:Label ;
	gvp:term "中国"@zh ;
	gvp:displayOrder "16"^^xsd:positiveInteger ;
	skosxl:literalForm "中国"@zh ;
	gvp:termFlag <http://vocab.getty.edu/term/flag/Vernacular> ;
	dct:contributor tgn_contrib:10000000 ;
	gvp:contributorNonPreferred tgn_contrib:10000000 ;
	dct:source tgn_source:2009007144 , tgn_source:2009008247-term-1002193462 ;
	gvp:sourceNonPreferred tgn_source:2009007144 , tgn_source:2009008247-term-1002193462 ;
	dc:identifier "1002193462" ;
	dct:language aat:300388113 .
tgn_term:143323-en a skosxl:Label ;
	gvp:term "People's Republic of China"@en ;
	gvp:displayOrder "6"^^xsd:positiveInteger ;
	skosxl:literalForm "People's Republic of China"@en ;
	gvp:termPOS <http://vocab.getty.edu/term/POS/Noun> ;
	dct:contributor tgn_contrib:10000000 ;
	gvp:contributorNonPreferred tgn_contrib:10000000 ;
	dct:source tgn_source:2009007144 , tgn_source:9004954-term-143323 , tgn_source:9006781-term-143323 ;
	gvp:sourceNonPreferred tgn_source:2009007144 ;
	dc:identifier "143323" ;
	dct:language aat:300388277 .
```
