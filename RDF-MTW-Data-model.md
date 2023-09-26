## MTW Namespaces

PREFIX **text:** \<http\://jena.apache.org/text#>
- required by [Jena Full Text search](https://jena.apache.org/documentation/query/text-query.html)

PREFIX **meshx:** \<configurable for each target language>
- identifiers used for Terms & custom Concepts URIs
- values can be either MESH DUI/CUI/TermID or UUID v4 (random)

PREFIX **mesht:** \<http\://www.medvik.cz/schema/mesh/vocab/#>

See [mesh.ttl](https://github.com/filak/MTW-MeSH/blob/master/flask-app/instance/conf/mesh.ttl)

## Predicates

Language tag is used for non-english literal values ie. @cs

> \* denotes custom predicates - otherwise a property has the same definition and usage as the [official meshv:predicates](https://hhs.github.io/meshrdf/predicates)

**mesht:active** - Custom Concept/Terms property 
- present only when Concept/Term has been deleted - always: false

**mesht:annotation** - Descriptor property

**mesht:concept** - Descriptor property

**mesht:considerAlso** - Descriptor property

**mesht:dateCreated** - Term property

**mesht:dateUpdated** - Term property

**mesht:dateDeleted** - Custom Concept property when deleted

**mesht:historyNote** - Descriptor property

**mesht:identifier** - Term property
- kept for the archiving purpose (retained from the original MESH XML dataset) 
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

### Translated preferrered term 

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

### Custom concept for D018153 "Czech Republic" 
```
mesh:D018153
    mesht:concept   meshx:4ffb2f83-16fe-4e6e-88d1-58aaa32306fd 

mesh:M0027363
    mesht:narrowerConcept   meshx:4ffb2f83-16fe-4e6e-88d1-58aaa32306fd

# concept props
meshx:4ffb2f83-16fe-4e6e-88d1-58aaa32306fd
    mesht:identifier   "F20210002"

meshx:4ffb2f83-16fe-4e6e-88d1-58aaa32306fd
    mesht:scopeNote   "Krátká forma (úřední) názvu České republiky."@cs
 
meshx:4ffb2f83-16fe-4e6e-88d1-58aaa32306fd	
    mesht:scopeNote   "Short form name (official) of the Czech Republic."@en 

meshx:4ffb2f83-16fe-4e6e-88d1-58aaa32306fd
    mesht:translatorsNote   "[justification for the Custom concept] Short form name (official) of the Czech Republic."@en

meshx:4ffb2f83-16fe-4e6e-88d1-58aaa32306fd
    mesht:preferredTerm   meshx:5e1bb9ea-68ca-4848-b1af-bd5d4ca3eabf

meshx:4ffb2f83-16fe-4e6e-88d1-58aaa32306fd
    mesht:term   meshx:55792212-383e-47da-b0dd-5655543ae476

# preferred term props
meshx:5e1bb9ea-68ca-4848-b1af-bd5d4ca3eabf
    mesht:prefLabel   "Česko"@cs 

meshx:5e1bb9ea-68ca-4848-b1af-bd5d4ca3eabf
    mesht:dateCreated "2019-11-22"^^http://www.w3.org/2001/XMLSchema#date 

# term props
meshx:55792212-383e-47da-b0dd-5655543ae476
    mesht:prefLabel   "Czechia"@cs 

meshx:55792212-383e-47da-b0dd-5655543ae476
    mesht:dateCreated "2019-11-22"^^http://www.w3.org/2001/XMLSchema#date 

```

