# TDWG Boolean Controlled Vocabulary List of Terms

Title
: TDWG Boolean Controlled Vocabulary List of Terms

Namespace IRI
: http://rs.tdwg.org/boolean/values/

Preferred namespace abbreviation
: boolean:

Date version issued
: 2023-03-13

Date created
: 2023-03-13

Part of TDWG Standard
: Not part of any standard

This version
: <http://rs.tdwg.org/tag/doc/boolean/2023-03-13>

Latest version
: <http://rs.tdwg.org/tag/doc/boolean/>

Abstract
: This vocabulary is intended to be used TDWG-wide in cases where properties specify boolean values.

Contributors
: [Steven J. Baskauf](https://orcid.org/0000-0003-4365-3135) ([Vanderbilt University Libraries](http://www.wikidata.org/entity/Q16849893)), [Ben Norton](https://orcid.org/0000-0002-5819-9134) 

Creator
: TDWG Technical Architecture Group

Bibliographic citation
: TDWG Technical Architecture Group. 2023. TDWG Boolean Controlled Vocabulary List of Terms. Biodiversity Information Standards (TDWG). <http://rs.tdwg.org/tag/doc/boolean/2023-03-13>

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

## 3 Term Index 

[boolean values concept scheme](#boolean_b) |
[false](#boolean_b0) |
[true](#boolean_b1) 

## 4 Vocabulary
<table>
	<thead>
		<tr>
			<th colspan="2"><a id="boolean_b"></a>Term Name  boolean:b</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Term IRI</td>
			<td><a href="http://rs.tdwg.org/boolean/values/b">http://rs.tdwg.org/boolean/values/b</a></td>
		</tr>
		<tr>
			<td>Modified</td>
			<td>2023-03-13</td>
		</tr>
		<tr>
			<td>Term version IRI</td>
			<td><a href="http://rs.tdwg.org/boolean/values/version/b-2023-03-13">http://rs.tdwg.org/boolean/values/version/b-2023-03-13</a></td>
		</tr>
		<tr>
			<td>Label</td>
			<td>boolean values concept scheme</td>
		</tr>
		<tr>
			<td>Definition</td>
			<td>A SKOS Concept Scheme for boolean values</td>
		</tr>
		<tr>
			<td>Type</td>
			<td>http://www.w3.org/2004/02/skos/core#ConceptScheme</td>
		</tr>
	</tbody>
</table>

<table>
	<thead>
		<tr>
			<th colspan="2"><a id="boolean_b0"></a>Term Name  boolean:b0</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Term IRI</td>
			<td><a href="http://rs.tdwg.org/boolean/values/b0">http://rs.tdwg.org/boolean/values/b0</a></td>
		</tr>
		<tr>
			<td>Modified</td>
			<td>2023-03-13</td>
		</tr>
		<tr>
			<td>Term version IRI</td>
			<td><a href="http://rs.tdwg.org/boolean/values/version/b0-2023-03-13">http://rs.tdwg.org/boolean/values/version/b0-2023-03-13</a></td>
		</tr>
		<tr>
			<td>Label</td>
			<td>false</td>
		</tr>
		<tr>
			<td>Definition</td>
			<td>Concept representing a boolean false value</td>
		</tr>
		<tr>
			<td>Usage</td>
			<td>In systems where datatyping is possible, this value SHOULD be serialized using the datatyped value appropriate for false values in that system.</td>
		</tr>
		<tr>
			<td>Controlled value</td>
			<td>false</td>
		</tr>
		<tr>
			<td>Type</td>
			<td>Concept</td>
		</tr>
	</tbody>
</table>

<table>
	<thead>
		<tr>
			<th colspan="2"><a id="boolean_b1"></a>Term Name  boolean:b1</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Term IRI</td>
			<td><a href="http://rs.tdwg.org/boolean/values/b1">http://rs.tdwg.org/boolean/values/b1</a></td>
		</tr>
		<tr>
			<td>Modified</td>
			<td>2023-03-13</td>
		</tr>
		<tr>
			<td>Term version IRI</td>
			<td><a href="http://rs.tdwg.org/boolean/values/version/b1-2023-03-13">http://rs.tdwg.org/boolean/values/version/b1-2023-03-13</a></td>
		</tr>
		<tr>
			<td>Label</td>
			<td>true</td>
		</tr>
		<tr>
			<td>Definition</td>
			<td>Concept representing a boolean true value</td>
		</tr>
		<tr>
			<td>Usage</td>
			<td>In systems where datatyping is possible, this value SHOULD be serialized using the datatyped value appropriate for true values in that system.</td>
		</tr>
		<tr>
			<td>Controlled value</td>
			<td>true</td>
		</tr>
		<tr>
			<td>Type</td>
			<td>Concept</td>
		</tr>
	</tbody>
</table>


