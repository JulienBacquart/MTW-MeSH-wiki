## MTW namespaces

PREFIX text: \<http\://jena.apache.org/text#>

PREFIX meshx: \<target language custom value#>
- used for Terms & custom Concepts URIs
- value is uuid.uuid4()

PREFIX mesht: \<http\://www.medvik.cz/schema/mesh/vocab/#>

## mesht: predicates

Language tag is used for non-english values ie. @cs

> \* denotes custom predicates - otherwise a property has the same definition and usage as the [official meshv:predicates](https://hhs.github.io/meshrdf/predicates)

**mesht:annotation** - Descriptor property

**mesht:concept** - Descriptor property

**mesht:considerAlso** - Descriptor property

**mesht:dateCreated** - Term property

**mesht:dateUpdated** - Term property

**mesht:historyNote** - Descriptor property

**mesht:identifier** - Term property

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

