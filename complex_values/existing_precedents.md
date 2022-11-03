# Complex values - existing precedents

Steve Baskauf - 2022-11-03

## Darwin Core/Audubon Core literal/IRI valued terms

Both the main Darwin Core and the main Audubon Core vocabularies have a mechanism for distinguishing between terms expected to have literal (string) values and terms expected to have values that represent abstract ("nonliteral") entities. It is generally expected that abstract entities will be denoted by IRIs. However, in serializations that permit anonymous (blank) nodes, it is possible to link to a described entity without specifying an IRI for the entity (see [section 2.4.2.2 of the Darwin Core RDF Guide](http://rs.tdwg.org/dwc/terms/guides/rdf/#2422-objects-which-are-blank-anonymous-nodes-non-normative) for an example).

### Literal valued terms

The strategies used by Darwin Core and Audubon Core are similar. Audubon Core-defined terms do not offer guidance as part of the indivicual term metadata, but rather offers a general suggestion in the normative [section 4 of the Audubon Core Stucture Guide](http://rs.tdwg.org/ac/doc/structure/#4-lists-of-plain-text-values): 

>Some AC terms permit values that are lists to be represented as plain text. The choice of how to separate list items is ultimately left to the implementers of AC. Typical usage is to choose a punctuation mark such as “,”, “;”, or “|”. In these cases a special escape syntax needs to be defined for cases in which the separator is part of the metadata value. Unfortunately, even for standard list formats like CSV, different software packages choose different escape methods, hindering interchange. In the absence of an implementation-specific choice we RECOMMEND to use “|” as separator and “\\|” as an escaped vertical bar.

In Darwin Core, the practice of separating multiple values with vertical bars is recommended systematically within the metadata for individual terms. In the non-normative `Notes` field of the metadata, typical text is:

>Recommended best practice is to separate the values in a list with space vertical bar space ( | ).

with examples shown in the non-normative `Examples` field.

Darwin Core mints an additional category of terms not found in Audubon Core. These are the so-called "ID" terms: term analogs whose local name ends in "ID", with the first part of the local name the same as the non-ID analog. For example, [dwc:recordedByID](http://rs.tdwg.org/dwc/terms/recordedByID) is the "ID" analog of [dwc:recordedBy](http://rs.tdwg.org/dwc/terms/recordedBy). It is expected that the "ID" analogs will have values that are identifiers rather than string names or descriptions. However, there is not necessarily any expectation that the identifiers will be IRIs (although they may be). The guidelines for providing multiple values is generally the same as for the non-ID analogs: separate the multiple values by space vertical bar space. The order that the identifiers is listed does not necessarily have any significance. For example, the Notes field for dwc:recordedBy states:

>...  The order of the identifiers on any list for this term can not be guaranteed to convey any semantics.

Thus although the "ID" terms allow for multiple values, they do not enable designation of order or role of the designated resource.

### Non-literal valued terms

In Darwin Core, term analogs expected to have non-literal (abstract entity) values are separated from the literal valued analogs by placing the non-literal analogs in a separate namespace: `dwciri:` (`http://rs.tdwg.org/dwc/iri/`). For example, [dwc:recordedBy](http://rs.tdwg.org/dwc/terms/recordedBy) is expected to have a literal (string) value and [dwciri:recordedBy](http://rs.tdwg.org/dwc/iri/recordedBy) is expected to have a non-literal (IRI) value.

In Audubon Core, the term analogs are distinguished by a convention for the local name part of the term IRI. Analogs expected to have literal values have a local name ending with "Literal" and those expected to have non-literal values do not. For example, [ac:metadataCreator](http://rs.tdwg.org/ac/terms/metadataCreator) is expected to have a non-literal (IRI) value and [ac:metadataCreatorLiteral](http://rs.tdwg.org/ac/terms/metadataCreatorLiteral) is expected to have a literal (string) value.

In both vocabularies, one could distinguish between terms that are expected to have IRIs that represent values from controlled vocabularies and terms that are expected to have IRIs because the values represent abstract entities that cannot be represented intrinsically by a string. An example in Darwin Core of a term expected to have an IRI value from a controlled vocabulary would be [dwciri:degreeOfEstablishment](http://rs.tdwg.org/dwc/iri/degreeOfEstablishment) and an example from Audubon Core would be [ac:variant]](http://rs.tdwg.org/ac/terms/variant). For Darwin Core, these two categories of terms are distinguished in [table 3.7 of the Darwin Core RDF Guide]](http://rs.tdwg.org/dwc/terms/guides/rdf/#37-dwc-namespace-terms-that-have-analogues-in-the-dwciri-namespace-normative) Although it possible that a user may wish to supply multiple values for IRI valued analogs expected to have a value from a controlled vocabulary, this is less likely than for terms where the value represents a non-literal entity such as a person, publication, protocol, language, organization, etc. 

In Darwin Core, the existing precedent for handling multiple values for IRI terms is laid out for formal RDF serializations in [section 2.5.1 of the RDF Guide](http://rs.tdwg.org/dwc/terms/guides/rdf/#251-definition-of-dwciri-terms-normative). The normative prescription there specifies that values of `dwciri:` predicates SHOULD be a single resource; in cases where there are multiple values, there should be a triple for the IRI denoting each value. However, the single resource MAY be a complex resource that is described by multiple triples; as noted before this resource could be assigned an IRI or could be represented as a blank node. 

Although the IRI-valued analogs were originially designed with the intent of enabling the serialization of Darwin Core metadata as RDF, nothing prevents those terms from being used in other non-RDF serializations, such as CSV tables or vanilla (non-JSON-LD) JSON. However, there is no guidance on how multiple values would be represented in such serializations. 

Originally, Audubon Core did not provide any guidance on how to serialize multiple values for IRI-valued terms, although the term metadata did specify that those terms were "Repeatable" (for example, [ac:reviewer](http://rs.tdwg.org/ac/terms/reviewer)). This implies that in the context of RDF a subject resource could have multiple triples for the same predicate (i.e. property term). [Section 3 of the Audubon Core Structure Guide](http://rs.tdwg.org/ac/doc/structure/#3-multiplicity-and-cardinality) discusses cases where pairs or tuples of properties are repeated (for example a reviewer and the comments made by that reviewer). Some examples of structuring using XML are provided, although these examples dealt exclusively with multiple ServiceAccessPoints (media variant forms). There are also examples provided for tabular representations of multiple ServiceAccessPoints. 

However, when [Regions of Interest (ROIs)](https://ac.tdwg.org/termlist/#711-region-of-interest-vocabulary) were defined as part of Audubon Core, the somewhat kludgy solutions suggested in the Structure guide were not sufficient to handle complex cases where a media item had both multiple ServiceAccessPoints and multiple ROIs. A non-normative "recipes" guide was created to provide examples of how these complex cases of multiple values could be handled via JSON-LD or multiple tables. (No single-table solutions were suggested.) The issues with the deficiencies of the existing structure guide were recognized in [Issue 234](https://github.com/tdwg/ac/issues/234), which is as of now unresolved.

# Specific solutions

Several terms or sets of terms within Darwin Core use mechanisms for describing more complex relationships among multiple resources.

## dwc:dynamicProperties

[dwc:dynamicProperties](http://rs.tdwg.org/dwc/terms/dynamicProperties) suggests using key:value encoding such as JSON as a mechanism for structuring content. The value is "about" the "record", which could be somewhat ambiguous if the record included information about several related resources. Nevertheless, it provides a mechanism for documenting the association between several related assertions. The examples make it clear that the keys do not necessarily correspond to any standardized properties.

## MeasurementOrFact terms

The set of [MeasurementOrFact](https://dwc.tdwg.org/terms/#measurementorfact) terms makes it possible to group related assertions by creating a record whose fields contain the various values necessary to fully describe some factual assertion. For example, an assertion about a measurement would group its value, type, accuracy, and unit by placing them together in a single record. (Not clear to me how the resource that the measurment is "about" is designated.) 

This solution is designed for tabular data, although perhaps it could be implemented in structured serializations. There doesn't seem to be a mechanism within this group of terms for indicating that particular measurements or facts are related to each other. 

## ResourceRelationsip terms

The [ResourceRelationship](https://dwc.tdwg.org/terms/#resourcerelationship) terms provide a table-based mechanism for asserting links between resources. Because each resource and the relationship itself can be associated with identifiers by means of "ID" terms, it would be possible to map the asserted relationships to subject-predicate-object triples. (See https://doi.org/10.3897/biss.5.74266 and https://doi.org/10.6084/m9.figshare.16823473 for more on this.) Thus, one could theoretically use ResourcesRelationship terms to express multiple values for a property by generating ResourceRelationship records with identical `dwc:resourceID` and `dwc:relationshipOrResourceID` values for each assertion. However, there would not seem to be any benefit to this approach over using some serialization that included structuring as part of its design (e.g. XML or JSON).

----
Revised 2022-11-03
