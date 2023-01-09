# Boolean Controlled Vocabulary

**Title:** TDWG Boolean Controlled Vocabulary

**Namespace URI:** http://rs.tdwg.org/boolean/values/

**Preferred namespace abbreviation:** boolean:

**Date version issued:** put publication date here

**Date created:** put publication date here

**Part of TDWG Standard:** Not part of any standard

**This version:** http://rs.tdwg.org/dwc/doc/boolean/iso-date-here

**Latest version:** http://rs.tdwg.org/dwc/doc/boolean/

**Abstract:** This vocabulary is intended to be used TDWG-wide in cases where properties specify boolean values. 

**Contributors:** Ben Norton, Steven J. Baskauf

**Creator:** TDWG Technical Architecture Group

**Bibliographic citation:** Technical Architecture Group. 2023. Boolean Controlled Vocabulary. Biodiversity Information Standards (TDWG). <http://rs.tdwg.org/dwc/doc/boolean/>


## 1 Introduction

Write something for this.

### 1.1 Status of the content of this document

In Section 4, the values of the `Term IRI`, `Definition`, and `Controlled value` are normative. The value of `Usage` (if it exists for a given term) is normative.  The values of `Term Name` are non-normative, although one can expect that the namespace abbreviation prefix is one commonly used for the term namespace.  `Label` and the values of all other properties (such as `Notes`) are non-normative.

### 1.2 RFC 2119 key words
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

## 2 Use of Terms

The terms terms of this vocabulary SHOULD be used in any situation where a positive or negative binary response is warranted. 

This includes not only situations where "true" or "false" are appropriate, but also responses such as "yes" or "no", "present" or "absent", 1 or 0, etc. Careful consideration of term local names can make it clearer to a user that the values recommended here are appropriate by chosing a lowerCamelCase phrase that makes sense with a boolean response. 

### 2.1 Examples

Instead of creating the term `ex:required` with recommended values "yes" and "no", create the term `ex:isRequired` with recommended values from this vocabulary. Instead of creating the term `ex:presence` with recommended values "present" and "absent", create the term `ex:isPresent` with recommended values from this vocabulary. 

## 3 Term index
