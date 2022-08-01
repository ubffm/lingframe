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
differences is required.

## 2. Basic structure & principles

Of the three main levels of description offered by BIBFRAME – `bf:Work`, `bf:Instance` and
`bf:Item` – the data model currently mostly uses `bf:Work` and `bf:Instance` while `bf:Item`
is only employed to host `bf:ElectronicLocator`.

If an element is not mentioned in Section3 "Included Elements", it is not a part of this
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
### 3.1 Classes
* [AbbreviatedTitle](https://id.loc.gov/ontologies/bibframe/AbbreviatedTitle)
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
* [Instance](https://id.loc.gov/ontologies/bibframe/Instance)
* [Isbn](https://id.loc.gov/ontologies/bibframe/Isbn)
* [Issn](https://id.loc.gov/ontologies/bibframe/Issn)
* [Item](https://id.loc.gov/ontologies/bibframe/Item)
* [Lccn](https://id.loc.gov/ontologies/bibframe/Lccn)
* [Local](https://id.loc.gov/ontologies/bibframe/Local)
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
* [dissertation](https://id.loc.gov/ontologies/bibframe/dissertation)
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
* [supplementaryContent](https://id.loc.gov/ontologies/bibframe/supplementaryContent)
* [title](https://id.loc.gov/ontologies/bibframe/title)

## BLL subject terms

In order to use [BLL subject terms](https://data.linguistik.de/bll/bll-ontology),
the following approach is used. A subclass `bfle:ClassificationBll` of `bf:Classification` is definied to
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
_:bll-Ainu a bllt:bll-133092208, bfbe:ClassificationBll .
```

Assignment to a bibliographic record:
```turtle
<http://data.linguistik.de/records/33298298X#Work> a                 bf:Work,
                                                                     bf:Text;
                                                   bf:classification _:bll-Ainu .
```
