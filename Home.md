# Welcome #

***Medical Subject Headings*** (MeSH) is a controlled vocabulary (thesaurus) for biomedical fields produced by the *National Library of Medicine* ([NLM](https://www.nlm.nih.gov/mesh/), Bethesda, USA). 

MTW stands for **Medical Subject Headings Translation Workflow**

## Why the MTW application ?

NLM has deprecated its legacy *MeSH Translation Maintenance System* (MTMS) by the end of 2018 leaving the translating organizations virtually empty-handed. Fortunately NLM provides a [linked data](https://id.nlm.nih.gov/mesh/) representation of the MeSH vocabulary - so a open source application for supporting the MeSH translation has been developed for the ***National Medical Library*** (**[NML](https://nlk.cz)**, Prague, Czech Republic). The MTW app has been used **in production in NML since January 2019**.

## Advantages of using RDF

* implementation of MeSH complex structures & relations without tables/schemas mapping
* SPARQL endpoints for data access
* ability to extend the official data model
([custom namespaces for the translations](https://github.com/filak/MTW-MeSH/wiki/RDF-MTW-Data-model)) 
* efficient handling of the annual data updates
* possibility to publish the translation as linked data

## Design goals

* web application with no proprietary software or components - open source stack
* no special hardware - app running even on a PC/laptop
* cross-platform (though developed on Windows)
* easy datasets management - updates, backups, migrations
* basic approval process/workflow
* clean and intuitive interface - see some [screenshots](https://github.com/filak/MTW-MeSH/wiki/ScreenShots)

## Features

* MeSH tree browsing & filtering
* fulltext searching with *, ? and phrase "" and boolean support
* statistics & todo lists, clipboard
* compare & diff descriptor versions
* custom concepts support
* complete audit & changes approval
* reporting & user management
* user roles based workflow: viewer, contributor, editor, manager
* duplicate terms checking & other data consistency checks
* exports to UMLS TSV, JSON, XML, MARC21 etc.

## Stack

Development of MTW has been possible thanks to many open source projects, notably:

* SPARQL server: Apache Jena Fuseki
* Web framework - Python: Flask & Jinja2 templates
* WSGI server - Python:   Waitress
* Frontend: Bootstrap & Bootswatch
* Database: SQLite

# Getting started

1. Install Java, Apache Jena&Fuseki, Sqlite3 - follow [Installation on Windows](https://github.com/filak/MTW-MeSH/wiki/Installation-on-Windows) (On Linux - follow [README](https://github.com/filak/MTW-MeSH/blob/master/flask-app/README.md)) 

2. [Load MeSH datasets](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets) into Apache Jena

3. [Run Fuseki server](https://github.com/filak/MTW-MeSH/wiki/Running-Fuseki-server)

4. Setup a web server with a reverse proxy - see [web server config examples](https://github.com/filak/MTW-MeSH/wiki/Web-server-config)

5. Start MTW services & Enjoy MTW at https://<HOST_LINK>/mtw

# Deployment & Production

* The MTW Compare/Diff feature requires server-side connection to https://id.nlm.nih.gov/mesh/sparql
* [Annual MeSH updates](https://github.com/filak/MTW-MeSH/wiki/MeSH-Annual-Updates)
* Backups
    - for Jena data use Fuseki GUI or [command](https://jena.apache.org/documentation/fuseki2/fuseki-server-protocol.html)
    - for SQLite db use [mtw_backup-vacuum.bat](https://github.com/filak/MTW-MeSH/blob/master/flask-app/instance/db/mtw_backup-vacuum.bat)
    - backup <MTW_HOME_DIR> directory as zip or tar file
    - **backup regularly and store the backup files safely**
    - [loading dataset from backup](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets#loading-data-from-a-backup) 
* MTW Upgrades
    - download the newest [release](https://github.com/filak/MTW-MeSH/releases/latest) MTW-X.Y.Z
    - check the release notes on breaking changes (if any)
    - stop the MTW services 
    - **backup <MTW_HOME_DIR> directory** 
    - rewrite binaries and static, templates, tools dirs in <MTW_HOME_DIR> 
    - start the MTW services
* Apache Jena/Fuseki upgrades
    - do not reuse old data - always use the last backup to [restore](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets#loading-data-from-a-backup) in the new Jena version instance 

# Support

Please use the [Issues](https://github.com/filak/MTW-MeSH/issues).

* Manual/FAQ \#TBD... 

# License

[MIT](https://github.com/filak/MTW-MeSH/blob/master/LICENSE) 
