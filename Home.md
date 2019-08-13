# Welcome #

***Medical Subject Headings*** (MeSH) is a controlled vocabulary (thesaurus) for biomedical fields produced by the *National Library of Medicine* ([NLM](https://www.nlm.nih.gov/mesh/), Bethesda, USA). 

MTW stands for **Medical Subject Headings Translation Workflow** project.

## Rationale behind MTW

NLM has abandoned its *MeSH Translation Maintenance System* (MTMS) by the end of 2018 leaving the translating organizations around the world virtually empty-handed. Fortunately NLM provides a [linked data](https://id.nlm.nih.gov/mesh/) representation of the MeSH vocabulary. Thus I have decided, having some experience with MeSH data processing, to develop an open source system for handling the translation workflow on behalf of the ***National Medical Library*** (**[NML](https://nlk.cz)**, Prague, Czech Republic). The MTW system was developed in the second half of 2018 and it has been used **in production at NML since January 2019**.

## Advantages of using RDF data for MeSH translation

* can contain complex structures & relations without tables/schemas
* SPARQL endpoint for data access 
* ability to extend the official data model
([custom namespaces for the translations](https://github.com/filak/MTW-MeSH/wiki/RDF-MTW-Data-model)) 
* efficient handling of data updates
* possibility to publish the translation as linked data #TBD


## Design goals

* web application
* no proprietary software/components
* no special hardware (running even on a PC/laptop)
* cross-platform portability (though I develop on Windows)
* easy datasets loading and updates
* light but scalable workflow
* clean and intuitive interface - see some [screenshots](https://github.com/filak/MTW-MeSH/wiki/ScreenShots)

## MTW features

* MeSH tree browsing & filtering
* full text searching with *, ? and phrase "" and boolean support
* statistics & todo lists, clipboard
* compare & diff descriptor versions
* custom concepts support
* complete audit & changes approval
* reporting & user management
* user roles based workflow: viewer, contributor, editor, manager
* duplicate terms check
* exports to UMLS TSV, JSON, XML, MARC21

## MTW Stack

Development of MTW has been possible thanks to many other open source projects, notably:

* Apache Jena & Fuseki
* Flask & Jinja2
* Bootstrap & Bootswatch
* SQLite

# Getting started

* Apache Jena/Fuseki requires Java 8 JRE & at least 2-4GB of RAM

1. Follow [Installation on Windows](https://github.com/filak/MTW-MeSH/wiki/Installation-on-Windows) (\#TBD: Linux - want to help ?) 

2. [Load MeSH datasets](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets) into Apache Jena

3. [Run Fuseki server](https://github.com/filak/MTW-MeSH/wiki/Running-Fuseki-server)

4. Enjoy MTW http://localhost:55930/mtw

# Deployment

* ALWAYS run the web-app behind a reverse proxy - see [web server config examples](https://github.com/filak/MTW-MeSH/wiki/Web-server-config)
* ALWAYS use HTTPS
* The Compare/Diff feature requires server-side connection to http://id.nlm.nih.gov/mesh/sparql

# Production

* [Annual MeSH updates](https://github.com/filak/MTW-MeSH/wiki/MeSH-Annual-Updates)
* Backups
    - for Jena data use Fuseki GUI or [command](https://jena.apache.org/documentation/fuseki2/fuseki-server-protocol.html)
    - for SQLite db use [mtw_backup-vacuum.bat](https://github.com/filak/MTW-MeSH/blob/master/flask-app/instance/db/mtw_backup-vacuum.bat)
    - backup <MTW_HOME_DIR> directory as zip or tar file
    - **store the backup files safely** 
* Upgrades
    - download the newest [release](https://github.com/filak/MTW-MeSH/releases) MTW-vX.Y.Z
    - check the release notes on breaking changes (if any)
    - stop the MTW services 
    - **backup <MTW_HOME_DIR> directory** 
    - rewrite binaries and static, templates, tools dirs in <MTW_HOME_DIR> 
    - start the services 
* Manual/FAQ \#TBD... 

# Support

Please use the [Issues](https://github.com/filak/MTW-MeSH/issues).

# License

[MIT](https://github.com/filak/MTW-MeSH/blob/master/LICENSE) 
