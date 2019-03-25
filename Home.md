# Welcome #

***Medical Subject Headings*** (MeSH) is a biomedical vocabulary (thesaurus) produced by the *National Library of Medicine* ([NLM](https://www.nlm.nih.gov/mesh/), Bethesda, USA)   

MTW stands for **Medical Subject Headings Translation Workflow** project.

## Rationale behind MTW

NLM has abandoned its *MeSH Translation Maintenance System* (MTMS) by the end of 2018 leaving the translating organizations around the globe virtually empty-handed. Fortunately NLM provides a [linked data](https://id.nlm.nih.gov/mesh/) representation of the MeSH vocabulary. Thus I have decided, having years of experience with MeSH data processing, to develop an open source system for handling the translation workflow on behalf of the ***National Medical Library*** (**[NML](https://nlk.cz)**, Prague, Czech Republic). The MTW system has been used in production at NML since January 2019.

## Advantages of using RDF data

* RDF can contain complex structures without tables/schemas
* ability to [extend](https://github.com/filak/MTW-MeSH/wiki/RDF-MTW-Data-model) MeSH RDF data model
and to use custom namespaces for the translations 
* efficient handling of MeSH data updates

## Design goals

* web application
* no proprietary software/components
* no heavy hardware (it runs even on a PC)
* cross-platform portability (though I develop on Windows)
* easy datasets loading and updates
* light but scalable workflow
* clean and intuitive interface - see some [screenshots](https://github.com/filak/MTW-MeSH/wiki/ScreenShots)

## MTW features

* MeSH tree browsing & filtering
* full text searching with *, ? and phrase "" support
* statistics & todo lists, clipboard
* compare & diff descriptors versions
* custom concepts support
* complete audit & changes approval
* reporting & user management
* user roles: viewer, contributor, editor, manager
* duplicate terms check
* exports to UMLS TSV, JSON, XML, MARC21

## MTW Stack

Development of MTW has been possible thanks to many other open source projects, notably:

* Apache Jena & Apache Jena Fuseki
* Flask & Jinja2
* Bootstrap & Bootswatch
* SQLite

# Getting started

* Apache Jena/Fuseki requires Java 8 JRE

1. Follow [Installation on Windows](https://github.com/filak/MTW-MeSH/wiki/Installation-on-Windows) (\#TBD: Linux) 

2. [Load MeSH datasets](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets) into Apache Jena

3. [Run Fuseki server](https://github.com/filak/MTW-MeSH/wiki/Running-Fuseki-server)

4. Enjoy MTW http://localhost:55930/mtw

# Production

* MTW manual \#TBD... 
* [Annual MeSH updates](https://github.com/filak/MTW-MeSH/wiki/MeSH-Annual-Updates)
* Backups \#TBD...

# Deployment

* ALWAYS run the web-app behind a reverse proxy - see [web server config examples](https://github.com/filak/MTW-MeSH/wiki/Web-server-config)
* ALWAYS use HTTPS
* Do not forget to backup regularly
* The Compare/Diff feature requires server-side connection to http://id.nlm.nih.gov/mesh/sparql

# Support

Please use the [Issues](https://github.com/filak/MTW-MeSH/issues).
