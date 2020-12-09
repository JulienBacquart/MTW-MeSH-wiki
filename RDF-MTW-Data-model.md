## MTW Namespaces

PREFIX **text:** \<http\://jena.apache.org/text#>
- required by [Jena Full Text search](https://jena.apache.org/documentation/query/text-query.html)

PREFIX **meshx:** \<configurable for each target language>
- used for Terms & custom Concepts URIs
- value is uuid.uuid4()

PREFIX **mesht:** \<http\://www.medvik.cz/schema/mesh/vocab/#>

## mesht: Predicates

Language tag is used for non-english literal values ie. @cs

> \* denotes custom predicates - otherwise a property has the same definition and usage as the [official meshv:predicates](https://hhs.github.io/meshrdf/predicates)

**mesht:active** - Custom Concept/Terms property 
- present only when Concept/Term is deleted - always: false

**mesht:annotation** - Descriptor property

**mesht:concept** - Descriptor property

**mesht:considerAlso** - Descriptor property

**mesht:dateCreated** - Term property

**mesht:dateUpdated** - Term property

**mesht:historyNote** - Descriptor property

**mesht:identifier** - Term property
- only retained from XML
- not used with newly translated terms as this identifier is optional in UMLS TSV spec
- might be generated in future if required - #TBD

**mesht:lexicalTag** - Term property

*_mesht:lockedBy_ - Descriptor property 
- if exists/true indicates a MTW user is working on the descriptor

**mesht:narrowerConcept** - Concept property

*_mesht:notTranslatable_ - Concept property 
- if exists/true a MTW user stated the concept is not translatable

**mesht:prefLabel** - Term property

**mesht:preferredTerm** - Concept property

**mesht:relatedConcept** - Concept property

**mesht:scopeNote** - Concept property

**mesht:term** - Concept property

*_mesht:translatorsNote_ - Concept/Descriptor property 
- custom translators non-public/internal note

## Examples [simplified]

### Translated preferrered term extracted from czedesc2019.xml
```
mesh:M0025841 
    mesht:preferredTerm   meshx:cze0019091

meshx:cze0019091
    mesht:prefLabel   "rotátorová manžeta"@cs

meshx:cze0019091 
    mesht:dateCreated   "2006-03-22"^^<http://www.w3.org/2001/XMLSchema#date>

meshx:cze0019091
    mesht:identifier   "cze0019091"
```

### Terms newly translated in MTW
```
### preferred term
mesh:M000611436 
    mesht:preferredTerm   meshx:3e0d87cf-fe1f-4909-ad4d-905eeaa1c3ae

meshx:3e0d87cf-fe1f-4909-ad4d-905eeaa1c3ae 
    mesht:prefLabel   "musculus teres minor"@cs 

meshx:3e0d87cf-fe1f-4909-ad4d-905eeaa1c3ae 
    mesht:dateCreated   "2019-01-16"...

mesh:M000611436 
    mesht:scopeNote   "Pouzdro tvořené šlachami ... okolo podélné osy."@cs 

### non-pref term
mesh:M000611436 
    mesht:term   meshx: 4eb3597d-dc66-498e-924f-77c822ff0c28

meshx:4eb3597d-dc66-498e-924f-77c822ff0c28 
    mesht:prefLabel   "malý sval oblý"@cs 

meshx:4eb3597d-dc66-498e-924f-77c822ff0c28 
    mesht:dateCreated   "2019-01-16"...
```

### Custom concept
```
mesh:D018806 
    mesht:concept   meshx:98ac2cab-5ca2-454d-b304-cfd8c4eefe48 

mesh:M0028159 
    mesht:narrowerConcept   meshx:98ac2cab-5ca2-454d-b304-cfd8c4eefe48 

meshx:98ac2cab-5ca2-454d-b304-cfd8c4eefe48 
    mesht:preferredTerm   meshx:b93f1c08-c65a-4a7f-9f02-732518225548 

meshx:98ac2cab-5ca2-454d-b304-cfd8c4eefe48 
    mesht:translatorsNote   "term is used, see e.g. https://www.ncbi.nlm.nih.gov/pubmed/16540951"@en 

meshx:98ac2cab-5ca2-454d-b304-cfd8c4eefe48 
    mesht:preferredTerm   meshx:b93f1c08-c65a-4a7f-9f02-732518225548 

meshx:b93f1c08-c65a-4a7f-9f02-732518225548 
    mesht:prefLabel   "APACHE IV"@cs 

meshx:b93f1c08-c65a-4a7f-9f02-732518225548 
    mesht:dateCreated "2019-01-11"^^http://www.w3.org/2001/XMLSchema#date 
```

