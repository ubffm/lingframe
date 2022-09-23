# Guide to the Lingframe BIBFRAME Application Profile for FID Linguistik

This document describes how the [BIBFRAME 2.0](https://www.loc.gov/bibframe/) data model is
adapted and used by the [Lin|gu|is|tik](https://linguistik.de) portal, for both internal
purposes as well as data dumps and exports. For convenience, we refer to
this application profile as "Lingframe". This guides lists the elements
of BIBFRAME used, outlines the specific conventions pertaining to their
use, as well as which elements are not part of the application profile (AP).

This document is to be considered as a "living documentation" and will
therefore be adapted or modified to reflect changes made to the data model
which become necessary during its continuous development.

Furthermore, as a general rule, this document is intended to complement
the official BIBFRAME documentation. In terms of elements allowed or
not in this application profile, the documentation at hand
takes precedence. In terms of definitions of the allowed elements, the
official definitions stated in the BIBFRAME documentation hold unless
differing definitions are given here. If a different definition is given,
this is done to state combinatoric restrictions with other BIBFRAME elements
or restrict the values of literals.


## 1. Introduction

As a bibliographic resource for a specific academic discipline rather than
a fully-fledged library system, the Lin|gu|is|tik portal requires only a
subset of what BIBFRAME has to offer. Certain areas of BIBFRAME
such as elements to describe e.g. notated music are not required by the
Lin|gu|is|tik portal and are thus not part of this application profile.
At the same time, some requirements are not directly addressed by BIBFRAME
such as a straightforward way of describing research papers. However, research papers
constitute the majority of the resources indexed into the Linguistik Portal.
Other features, such as the linking of bibliographic resources to research data,
are non-standard requirements and call for custom solutions altogether.
Therefore, the definition of an application profile which captures these
differences is required. Both the [Marc2Bibframe2 converter](https://github.com/lcnetdev/marc2bibframe2)
by the Library of Congress as well as the data model used by [Swepub](https://www.kb.se/samverkan-och-utveckling/swepub.html)
served as examples and reference points in the development of this 
application profile.


## 2. Basic structure & principles

Of the three main levels of description offered by BIBFRAME – `bf:Work`, `bf:Instance` and
`bf:Item` – the data model currently mostly uses `bf:Work` and `bf:Instance` while `bf:Item`
is only employed to host `bf:ElectronicLocator` and `bf:heldBy`.

If an element is not mentioned in Section 3 "Included Elements", it is not a part of this
application profile.  If an element is not mentioned in Section 4 "Diverging Definitions", its
original definition holds.

### 2.1. Basic structure

The following example outlines the basic structure a record generated with our reference implementation,
i.e. the Hebis-Pica To BIBFRAME converter. The `rdfs:label` can vary accordingly.

```turtle
<https://data.linguistik.de/records/<recordid>#Work>
    a bf:Work ;
    bf:hasInstance <https://data.linguistik.de/records/<record_id>#Instance> ;
    bf: adminMetadata [
        a bf:AdminMetadata ;
        bf:generationProcess [
            a bf:GenerationProcess ;
            rdfs:label "Linguistik-Portal Pica2BIBFRAME"
        ] ;
       bf:identifiedBy [
           a bf:Local ;
           rdf:value "<record_id>"
       ]  ;
    ] .
 
<https://data.linguistik.de/records/<record_id>#Instance>
    a bf:Instance ;
    bf:instanceOf <https://data.linguistik.de/records/<record_id>#Work> .
```

### 2.2. On blank nodes

The current version of the application profile makes extensive use of blank nodes.
This may change in the future.

### 2.3. On language tags and datatype for literals

Language tags are at the moment only used with `rdfs:label` for `bf:Topic` and `bf:GenreForm`.
In these cases, they are uniformly set to `de`.

Datatypes for literals are currently only used with literals that are objects of `bf:creationDate`.
In these cases, they are unisormly set do `xsd:date`.


## 3. Included Elements
### 3.1. Classes
* [AbbreviatedTitle](https://id.loc.gov/ontologies/bibframe/AbbreviatedTitle)
* [AccessPolicy](https://id.loc.gov/ontologies/bibframe/AccessPolicy)
* [AdminMetadata](https://id.loc.gov/ontologies/bibframe/AdminMetadata)
* [Agent](https://id.loc.gov/ontologies/bibframe/Agent)
* [Audio](https://id.loc.gov/ontologies/bibframe/Audio)
* [Classification](https://id.loc.gov/ontologies/bibframe/Classification)
* [CollectiveTitle](https://id.loc.gov/ontologies/bibframe/CollectiveTitle)
* [Contribution](https://id.loc.gov/ontologies/bibframe/Contribution)
* [Dataset](https://id.loc.gov/ontologies/bibframe/Dataset)
* [Dissertation](https://id.loc.gov/ontologies/bibframe/Dissertation)
* [Doi](https://id.loc.gov/ontologies/bibframe/Doi)
* [Electronic](https://id.loc.gov/ontologies/bibframe/Electronic)
* [Extent](https://id.loc.gov/ontologies/bibframe/Extent)
* [GenerationProcess](https://id.loc.gov/ontologies/bibframe/GenerationProcess)
* [GenreForm](https://id.loc.gov/ontologies/bibframe/GenreForm)
* [_Hdl_](https://id.loc.gov/ontologies/bibframe/Hdl)
* [Instance](https://id.loc.gov/ontologies/bibframe/Instance)
* [Isbn](https://id.loc.gov/ontologies/bibframe/Isbn)
* [Issn](https://id.loc.gov/ontologies/bibframe/Issn)
* [Item](https://id.loc.gov/ontologies/bibframe/Item)
* [Lccn](https://id.loc.gov/ontologies/bibframe/Lccn)
* [Local](https://id.loc.gov/ontologies/bibframe/Local)
* [_Manuscript_](https://id.loc.gov/ontologies/bibframe/Manuscript)
* [MixedMaterial](https://id.loc.gov/ontologies/bibframe/MixedMaterial)
* [Multimedia](https://id.loc.gov/ontologies/bibframe/Multimedia)
* [Nbn](https://id.loc.gov/ontologies/bibframe/Nbn)
* [Note](https://id.loc.gov/ontologies/bibframe/Note)
* [Organization](https://id.loc.gov/ontologies/bibframe/Organization)
* [ParallelTitle](https://id.loc.gov/ontologies/bibframe/ParallelTitle)
* [Person](https://id.loc.gov/ontologies/bibframe/Person)
* [Place](https://id.loc.gov/ontologies/bibframe/Place)
* [Print](https://id.loc.gov/ontologies/bibframe/Print)
* [ProvisionActivity](https://id.loc.gov/ontologies/bibframe/ProvisionActivity)
* [Publication](https://id.loc.gov/ontologies/bibframe/Publication)
* [Role](https://id.loc.gov/ontologies/bibframe/Role)
* [Source](https://id.loc.gov/ontologies/bibframe/Source)
* [Summary](https://id.loc.gov/ontologies/bibframe/Summary)
* [SupplementaryContent](https://id.loc.gov/ontologies/bibframe/SupplementaryContent)
* [Text](https://id.loc.gov/ontologies/bibframe/Text)
* [Title](https://id.loc.gov/ontologies/bibframe/Title)
* [Topic](https://id.loc.gov/ontologies/bibframe/Topic)
* [Urn](https://id.loc.gov/ontologies/bibframe/Urn)
* [VariantTitle](https://id.loc.gov/ontologies/bibframe/VariantTitle)
* [Work](https://id.loc.gov/ontologies/bibframe/Work)

### 3.2. Properties

* [adminMetadata](https://id.loc.gov/ontologies/bibframe/adminMetadata)
* [agent](https://id.loc.gov/ontologies/bibframe/agent)
* [assigner](https://id.loc.gov/ontologies/bibframe/assigner)
* [classification](https://id.loc.gov/ontologies/bibframe/classification)
* [contribution](https://id.loc.gov/ontologies/bibframe/contribution)
* [count](https://id.loc.gov/ontologies/bibframe/count)
* [creationDate](https://id.loc.gov/ontologies/bibframe/creationDate)
* [date](https://id.loc.gov/ontologies/bibframe/date)
* [degree](https://id.loc.gov/ontologies/bibframe/degree)
* [descriptionLanguage](https://id.loc.gov/ontologies/bibframe/descriptionLanguage)
* [dissertation](https://id.loc.gov/ontologies/bibframe/dissertation)
* [editionStatement](https://id.loc.gov/ontologies/bibframe/editionStatement)
* [electronicLocator](https://id.loc.gov/ontologies/bibframe/electronicLocator)
* [extent](https://id.loc.gov/ontologies/bibframe/extent)
* [generationProcess](https://id.loc.gov/ontologies/bibframe/generationProcess)
* [genreForm](https://id.loc.gov/ontologies/bibframe/genreForm)
* [grantingInstitution](https://id.loc.gov/ontologies/bibframe/grantingInstitution)
* [hasInstance](https://id.loc.gov/ontologies/bibframe/hasInstance)
* [hasItem](https://id.loc.gov/ontologies/bibframe/hasItem)
* [hasSeries](https://id.loc.gov/ontologies/bibframe/hasSeries)
* [heldBy](https://id.loc.gov/ontologies/bibframe/heldBy)
* [identifiedBy](https://id.loc.gov/ontologies/bibframe/identifiedBy)
* [instanceOf](https://id.loc.gov/ontologies/bibframe/instanceOf)
* [issuance](https://id.loc.gov/ontologies/bibframe/issuance)
* [itemOf](https://id.loc.gov/ontologies/bibframe/itemOf)
* [mainTitle](https://id.loc.gov/ontologies/bibframe/mainTitle)
* [note](https://id.loc.gov/ontologies/bibframe/note)
* [noteType](https://id.loc.gov/ontologies/bibframe/noteType)
* [part](https://id.loc.gov/ontologies/bibframe/part)
* [partName](https://id.loc.gov/ontologies/bibframe/partName)
* [partNumber](https://id.loc.gov/ontologies/bibframe/partNumber)
* [partOf](https://id.loc.gov/ontologies/bibframe/partOf)
* [place](https://id.loc.gov/ontologies/bibframe/place)
* [provisionActivity](https://id.loc.gov/ontologies/bibframe/provisionActivity)
* [qualifier](https://id.loc.gov/ontologies/bibframe/qualifier)
* [references](https://id.loc.gov/ontologies/bibframe/references)
* [responsibilityStatement](https://id.loc.gov/ontologies/bibframe/responsibilityStatement)
* [role](https://id.loc.gov/ontologies/bibframe/role)
* [seriesEnumeration](https://id.loc.gov/ontologies/bibframe/seriesEnumeration)
* [seriesStatement](https://id.loc.gov/ontologies/bibframe/seriesStatement)
* [source](https://id.loc.gov/ontologies/bibframe/source)
* [subject](https://id.loc.gov/ontologies/bibframe/subject)
* [subtitle](https://id.loc.gov/ontologies/bibframe/subtitle)
* [summary](https://id.loc.gov/ontologies/bibframe/summary)
* [supplementaryContent](https://id.loc.gov/ontologies/bibframe/supplementaryContent)
* [title](https://id.loc.gov/ontologies/bibframe/title)
* [usageAndAccessPolicy](https://id.loc.gov/ontologies/bibframe/usageAndAccessPolicy)

Items that are printed in _italics_ are included provisionally,
as they are likely to occur in the source data at some point,
but do not yet.

## 4. Special cases
### 4.1. BLL subject terms

In order to use [BLL subject terms](https://data.linguistik.de/bll/bll-ontology),
the following approach is taken. A subclass `bfle:ClassificationBll` of `bf:Classification` is definied to
easily allow using BLL terms with BIBFRAME.

```turtle
@prefix bf: <http://id.loc.gov/ontologies/bibframe/> .
@prefix bfbe: <http://data.linguistik.de/bibframe-bll-extensions> .
@prefix bllo: <https://data.linguistik.de/bll/bll-ontology#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix bllt: <https://data.linguistik.de/bll/bll-thesaurus#> .
 
bfbe:ClassificationBll a               owl:Class;
                       rdfs:subClassOf bf:Classification;
                       skos:definition "BLL Classification for use with BIBFRAME";
                       rdfs:label      "BLL Classification" .
 
bllt:BLLConcept        rdfs:subClassOf bfbe:ClassificationBll .
 
bllo:BLLConcept        rdfs:subClassOf bfbe:ClassificationBll .
```

Individuals:
```
_:bll-Ainu a bllt:bll-133092208, bfbe:ClassificationBll, bf:Language .
```

Assignment to a bibliographic record:
```turtle
<http://data.linguistik.de/records/33298298X#Work> a                 bf:Work,
                                                                     bf:Text;
                                                   bf:classification _:bll-Ainu .
```

In addition to the aforemetioned classes, BLL terms that represent languages are also
instances of `bf:Language`. This way, it is possible to use BLL language terms as
objects of `bf:language` and `bf:descriptionLanguage`.

### 4.2. Article level description

For the most part, articles are modelled in Lingframe like every other bibliographic record.
`bf:genreForm <http://data.linguistik.de/lingframe-genreterms#article>` is used to explicitly
mark articles as such on `bf:Work` level.

Articles are linked to their host by using the following approach (inspired by [Swepub](https://www.kb.se/samverkan-och-utveckling/swepub/datamodell/swepub-bibframe.html)):

```turtle
bf:partOf [ a bf:Instance ;
        bf:extent [ a bf:Extent ;
                rdfs:label "283-311" ] ;
        bf:instanceOf <http://data.linguistik.de/records/1935> ;
        bf:part "34 2006 4 283-311" ;
        bf:provisionActivity [ a bf:Publication ;
                bf:date "2006" ] ;
        bf:title [ a bf:Title ;
                rdfs:label "Journal of English linguistics. - Thousand Oaks, Calif. {[u.a.] : Sage" ;
                sdo:issueNumber "4" ;
                sdo:volumeNumber "34" ] ] ;
```

### 4.3. Description of text corpora

Text corpora are treated as `bf:Dataset`. For a detailed example, please see the examples folder.


### 4.4 References to research data

References to corpora are modelled on `bf:Instance` level like
this:

```turtle
bf:references [ a bf:Instance ;
            bf:instanceOf bllt:bll-44698227X ] ;
```

If a research paper references a specific version of a text corpus, this can be be stated via `bf:qualifier`
inside the blank node.
