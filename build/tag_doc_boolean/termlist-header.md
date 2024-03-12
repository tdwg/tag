# {document_title}

Title
: {document_title}

Namespace IRI
: {namespace_uri}

Preferred namespace abbreviation
: {pref_namespace_prefix}:

Date version issued
: {ratification_date}

Date created
: {created_date}

Part of TDWG Standard
: Not part of any standard

This version
: <{current_iri}{ratification_date}>

Latest version
: <{current_iri}>

{previous_version_slot}

Abstract
: {abstract}

Contributors
: {contributors}

Creator
: {creator}

Bibliographic citation
: {creator}. {year}. {document_title}. {publisher}. <{current_iri}{ratification_date}>

## 1 Introduction

This vocabulary is a technical recommendation of the TDWG Technical Architecture Group, approved at their [2023-03-13 meeting](https://github.com/tdwg/tag/blob/master/meetings/2023-03-13-tag-meeting-notes.pdf). As such, it is RECOMMENDED that it will be used across TDWG vocabluaries as values for property terms that require booleans. 

### 1.1 Status of the content of this document

All parts of Sections 1 and 2 are normative, except for examples listed as non-normative.

Section 3 is not normative.

In Section 4, the values of the `Term IRI`, `Definition`, and `Controlled value` are normative. The value of `Usage` (if it exists for a given term) is normative.  The values of `Term Name` are non-normative, although one can expect that the namespace abbreviation prefix is one commonly used for the term namespace.  `Label` and the values of all other properties (such as `Notes`) are non-normative.

### 1.2 RFC 2119 key words
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [BCP 14](https://www.rfc-editor.org/info/bcp14) [\[RFC 2119\]](https://datatracker.ietf.org/doc/html/rfc2119) and [\[RFC 8174\]](https://datatracker.ietf.org/doc/html/rfc8174) when, and only when, they appear in all capitals, as shown here.

## 2 Use of Terms

The terms terms of this vocabulary SHOULD be used in any situation where a positive or negative binary response is warranted. 

This includes not only situations where "true" or "false" are appropriate, but also responses such as "yes" or "no", "present" or "absent", 1 or 0, etc. Careful consideration of term local names can make it clearer to a user that the values recommended here are appropriate by chosing a lowerCamelCase phrase that makes sense with a boolean response. 

In Linked Data contexts (i.e. RDF), native boolean values SHOULD be used rather than the term IRIs, which are minted primarily to allow unambiguous reference to term metadata.

### 2.1 Examples (non-normative)

Instead of creating the term `ex:required` with recommended values "yes" and "no", create the term `ex:isRequired` with recommended values from this vocabulary. Instead of creating the term `ex:presence` with recommended values "present" and "absent", create the term `ex:isPresent` with recommended values from this vocabulary. 

