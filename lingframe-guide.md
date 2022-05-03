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
* AbbreviatedTitle
* AdminMetadata
* Agent
* Audio
* Classification
* CollectiveTitle
* Contribution
* Dataset
* Dissertation
* Doi
* Electronic
* Extent
* GenerationProcess
* GenreForm
* Instance
* Isbn
* Issn
* Item
* Lccn
* Local
* MixedMaterial
* Multimedia
* Nbn
* Note
* Organization
* ParallelTitle
* Person
* Place
* Print
* ProvisionActivity
* Publication
* Role
* Source
* SupplementaryContent
* Text
* Title
* Topic
* Urn
* VariantTitle
* Work

### 3.2. Properties
* adminMetadata
* agent
* assigner
* classification
* contribution
* count
* creationDate
* date
* degree
* dissertation
* electronicLocator
* extent
* generationProcess
* genreForm
* grantingInstitution
* hasInstance
* hasItem
* hasSeries
* heldBy
* identifiedBy
* instanceOf
* issuance
* itemOf
* mainTitle
* note
* noteType
* part
* partName
* partNumber
* partOf
* place
* provisionActivity
* qualifier
* references
* responsibilityStatement
* role
* seriesEnumeration
* seriesStatement
* source
* subject
* subtitle
* supplementaryContent
* title

## BLL subject terms

In order to use [BLL subject terms](https://data.linguistik.de/bll/bll-ontology/),
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
