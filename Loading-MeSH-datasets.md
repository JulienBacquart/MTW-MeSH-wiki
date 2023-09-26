## Before any data loading ##

Jena assembler config file <**MTW_HOME_DIR**>\instance\conf\mesh.ttl **MUST BE** set up properly ! 

https://github.com/filak/MTW-MeSH/blob/master/flask-app/instance/conf/mesh.ttl

* Adjust paths "c:/Data/mesh-mtw/apache-jena-data" in mesh.ttl to your <**FUSEKI_DATA_DIR**>

        tdb2:location  "c:/Data/mesh-mtw/apache-jena-data/databases/mesh" ;

        text:directory "c:/Data/mesh-mtw/apache-jena-data/indexes/mesh" ;

* Copy mesh.ttl file to:

    <**FUSEKI_DATA_DIR**>\configuration\

## Get the official MeSH RDF dataset ##

Download the official MeSH RDF dataset **mesh.nt.gz** at https://nlmpubs.nlm.nih.gov/projects/mesh/rdf/

> You might use curl for downloading

    curl https://nlmpubs.nlm.nih.gov/projects/mesh/rdf/mesh.nt.gz --ssl-no-revoke -O
          
## Get the translation RDF dataset ##

> If you have not translated MeSH before - you can proceed to [Import](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets#import-the-rdf-datasets).

### Convert the official MTMS XML file - OBSOLETE ###

1. Download your ***.xml.gz** translation file at
    
    [ftp://nlmpubs.nlm.nih.gov/online/mesh/MESH_FILES/mtms/](ftp://nlmpubs.nlm.nih.gov/online/mesh/MESH_FILES/mtms/)
    
    or
    
    [ftp://ftp.nlm.nih.gov/online/mesh/MESH_FILES/mtms/](ftp://ftp.nlm.nih.gov/online/mesh/MESH_FILES/mtms/)

2. Extract translation data from MeSH XML as N-triples dataset using **mesh-xml2trx** tool
  
    Run the extraction script:
    
        mesh-xml2trx *.xml.gz <TARGET_NS>

    **IMPORTANT:  TARGET_NS** - target namespace param - the custom URI prefix for you translation - **MUST be the same** as TARGET_NS used in your **mtw.ini config file** ! 

    https://github.com/filak/MTW-MeSH/blob/master/flask-app/instance/conf/mtw.ini

    ie.
    
        mesh-xml2trx czedesc2018.xml.gz http://mesh.medvik.cz/link/

### Convert the official UMLS TSV file ###

**trans_only_YYYY.txt**

> #TBD


## Import the RDF datasets ##

0. **ALWAYS validate the input files**

    Run the validation:
        
        riot --validate mesh.nt.gz

        riot --validate mesh-trx_YYYY-MM-DD.nt.gz

    No output = data is OK

1. Move the input files into a versioned <**IMPORT**> directory ie.  ...\MeSH-data\2019-1\import\

2. Load the MeSH datatset(s) into Apache Jena

    **Stop Fuseki server instance (if running)**
    
    Go to your <**IMPORT**> directory
    
    Run the import:
        
        tdb2_tdbloader --loc %FUSEKI_BASE%\databases\mesh mesh.nt.gz mesh-trx_YYYY-MM-DD.nt.gz ...
    
    ie:
    
        tdb2_tdbloader --loc %FUSEKI_BASE%\databases\mesh mesh.nt.gz mesh-trx_2018-12-19.nt.gz
    
    or if you do not have a translation then just:
    
        tdb2_tdbloader --loc %FUSEKI_BASE%\databases\mesh mesh.nt.gz

3. Create Fuseki search index
   
    Go to your <**FUSEKI_DATA_DIR**>
   
    Run the indexation:
    
        java -cp %FUSEKI_HOME%\fuseki-server.jar jena.textindexer --desc=configuration/mesh.ttl
    
4. [Start Fuseki server](https://github.com/filak/MTW-MeSH/wiki/Running-Fuseki-server) instance

## Loading data from a backup ##

1. **Stop MTW services**

2. **Stop your Fuseki instance**

3. Go to your <**FUSEKI_DATA_DIR**> 
and make sure the <**mesh**> directories under datatabases and indexes dirs are empty !

    Run the import: 

        tdb2_tdbloader --loc %FUSEKI_BASE%\databases\mesh %FUSEKI_BASE%\backups\mesh_YYYY-MM-DD_....nq.gz

    Create the search index - run:

        java -cp %FUSEKI_HOME%\fuseki-server.jar jena.textindexer --desc=configuration/mesh.ttl

4. Start your Fuseki instance

5. Start MTW services

Continue to [MeSH Annual Updates](https://github.com/filak/MTW-MeSH/wiki/MeSH-Annual-Updates)