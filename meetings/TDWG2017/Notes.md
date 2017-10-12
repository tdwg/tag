# IG02 - Technical Architecture Meeting, TDWG 2017 #

## Organizer: Greg Whitbread (chair), Paul Morris (deputy chair) ##

Attending (Tuesday 2017-Oct-03):  Paul Morris, Dimitris Koureas, Jonathan Rees, Dag Endresen, Joel Sachs, Pier Buttigieg, Jeff Gerbracht, Steve Baskauf (remote) , Stan Blum

Attending (Thursday 2017-Oct-05): Matt Djos, Paul Morris, Dimitris Koureas, Stan Blum, John Wieczorek, Dag Endresen, Chuck Miller, Jonathan Rees, Jeff Gerbracht, William Ulate (remote), Steve Baskauf (remote)

Notes taken collaboratively in sessions into http://bit.ly/TDWG17-IG02

*Tuesday*

## Agenda: ##
### Review Charter ###

Steve: I think having a group that can act as consultants on technical issues is important.  In several of the TGs I’ve worked on, we’ve had technical questions and could only get answers for them if we had the right technical people in the Task Group.  We are likely in the future to have groups developing controlled vocabularies who have little experience with technical issues and will need such help.

Stan: we need better definition of TAG’s scope in the charter, in particular separation between concerns for the Exec and TAG.

Jonathan Rees:  TAG has been primarily responsive (acts in response to request by EC to review charter, proposed standard, etc.
So we need to be careful about the language and whether TAG is supposed to initiate things.  

Steve: The Vocabulary Maintenance Specification (VMS) has specific things to say about the requirements for use case definition and documenting implementation experience.  But requiring that outside of vocabularies was outside of the scope of that specification.  It perhaps should be required beyond vocabularies.

Pier:  can/should assess and provide feedback about “feasibility” and approach.

Stan:  TDWG is now focussing on content standards (vocabularies), so in the TDWG context, the spirit of “2 independent implementations” be represented by two separately managed databases that claim to comply with a vocab spec. Do they combine effectively and without serious problem?

Paul raised the issue (afterwards) that the Data Quality IG is producing specs that will be implemented as operating software (testing content).

Steve: In the VMS, there is no requirement for use case definition and documenting implementation experience to simply define vocabulary terms.  But if the extension of a vocabulary is supposed to “do” something, it’s required to clearly define what the extension is supposed to do (use cases) and show that it actually works (implementation experience).  

Dimitris:  the TAG charter should also call out the responsibility to produce and update a technical / architectural roadmap.

Dimitris: In response to the GUID AS replacement, there is a large initiative towards the ‘Global Digital Object Cloud’ where PID system discussions and standards will be at the core of discussions. TDWG can pick up a relevant task in collaboration with international players.  

### Review work plan ###

UPdate the GUID-AS.   We will need resources and some working meetings to make this happen.  GBIF, NSF, EC could all be interested in supporting this work.

We’ll move a version of this into GitHub; also the PPT

*Thursday*

Please identifiy yourself in association with comments.

### Review work plan ###
#### Review GUID Applicability Statement ####
#### Review TDWG Metamodel ####

Steve Baskauf: Metamodel comment: Please refer to section 4.1 of the Vocabulary Maintenance Specification

https://github.com/tdwg/vocab/blob/master/vms/maintenance-specification.md

There is a process established for development of “vocabulary enhancements” that involves collecting use cases, etc.  I believe that process applies here.  It also includes the requirement for reporting of implementation experience.

Steve Baskauf: Why do we want a metamodel? What is it supposed to do?  Until we answer that question, it’s premature to plan like this.  What are the use cases?  As far as I know, these questions were never asked about the TDWG Ontology and it failed.

Steve Baskauf:  For example, depending on what you want to do, you might develop an ontology, a SKOS concept scheme, or just mint linked data properties.  But you can’t know which direction to go until you know why you are doing it.  Start with collecting the use cases.

Three potential areas of work and entanglement
Adding class structure to DarwinCore 
Integrate across domains, such as biodiversity and geospatial
Within TDWG, how do we guide development of standards and coordinate among groups?

Dimitris: TAG and Process were jointly tasked with creating a landscape document that would help guide TDWG participants and groups.

Fairsharing (http://fairsharing.org) (https://fairsharing.org/collection/TDWGBiodiversity) can help us know who uses what standards

John W.:  a picture of groups and their relationships (interfaces / overlaps) would help a lot

Steve B: Basically you are talking about laying out a graph model.  That can be directly converted into RDF/Linked Data/JSON-LD.  The model needs to be just as complex as is necessary to facilitate the identified use cases and no more.  But until you decide what use cases you want to satisfy, you won’t know how complicated to make it.

Stan: agree with Steve

Paul: a small group should be able to tackle the picture problem

John W.:  if the group starts to argue too much, it would indicate that they’re getting into the weeds (getting in too deep).

Concrete use case: Help TDWG clientele to navigate what vocabularies TDWG has to offer, and how that relates to other domains.


DK:  fairshairing can handle relationships among standards and use of standards by organizations/applications

Steve: The Standards Documentation Specification links all components of all standards regardless of whether they are vocabularies, although vocabularies are included. 

https://raw.githubusercontent.com/tdwg/vocab/master/tdwg-standards-hierarchy-2017-01-23.png

![TDWG Standards Heirarchy](https://raw.githubusercontent.com/tdwg/vocab/master/tdwg-standards-hierarchy-2017-01-23.png)

JW: @Steve Do you mean to say that the information needed to build a graph of standards within TDWG would ultimately be deliverable from standards following the documentation standard?

Steve: It’s already done as a prototype and loaded in the Vanderbilt graph database.  And querieable.  

@Steve Can you make a graphic to include here? 


Just the top levels are relevant outside of vocabularies.  All of the standards would be linked to TDWG at the top by a dcterms:publisher link.  

Here is an example query, runnable at https://sparql.vanderbilt.edu if you paste it into the box:

    PREFIX dcterms: <http://purl.org/dc/terms/>
    SELECT DISTINCT ?standard ?document ?type
    FROM <http://rs.tdwg.org/>
    WHERE {
      ?standard dcterms:publisher <https://www.grid.ac/institutes/grid.480498.9>.
      ?standard a dcterms:Standard.
      ?standard dcterms:hasVersion ?version.
      ?document dcterms:isPartOf ?standard.
      OPTIONAL {
         ?document a ?type.
      }
    }

The query finds standards whose publisher is TDWG (https://www.grid.ac/institutes/grid.480498.9), then asks what the parts of the standards are.  If the type of the part is known, it’s listed. 

The results currently are:

![Query results](https://github.com/tdwg/tag/blob/master/meetings/TDWG2017/VlSneX.png)

Hard to read, but try it yourself and you can make the text bigger.  At the moment, there are a number of things wrong with the results, but that’s only because I haven’t entered a lot of the metadata for all parts of all standards.  There are also some issues with me using particular distributions of the documents rather than abstract identifiers for the documents.  But the point is, we have a model that would allow an application to acquire machine-readable information about all parts of all TDWG Standards. What remains is to pull these data and make them look pretty on a web page.  Ultimately, that will happen when we finish complying with the Standards Documentation spec. I’m intending to keep chipping away at entering the metadata, although there are some unanswered questions about what actually is part of a standard like TAPIR and what is not.  For vocabulary standards, one can explore the pieces on a more detailed level, such as discovering which terms are minted by TDWG and which are borrowed from elsewhere.


## Action Items ##

1. Charter a task group to revise the GUID-AS (etc)  Issue: GH-14
1. TAG and Process should begin with a road-map document (with graphic representations) showing relationships among TDWG IG/TGs as well as a graph depicting the view from each IG/TG.  Each IG/TG should validate/revise the IG/TG centered view of the TDWG landscape.  Issue: GH-16
1. Investigate Zoom, Go-to-Meeting to support monthly conference calls



