## Before any data loading ##

Jena assembler config file <**MTW_HOME_DIR**>/instance/conf/mesh.ttl **MUST BE** set up properly ! 

https://github.com/filak/MTW-MeSH/blob/master/flask-app/instance/conf/mesh.ttl

* Adjust the paths in **mesh.ttl** to your <**FUSEKI_DATA_DIR**>

> **Use forward slashes**

        tdb2:location  "c:/<FUSEKI_DATA_DIR>/databases/mesh" ;

        text:directory "c:/<FUSEKI_DATA_DIR>/indexes/mesh" ;

* Validate **mesh.ttl**

> No output = file is OK

      riot --validate mesh.ttl

* Copy the **mesh.ttl** file to:

    <**FUSEKI_DATA_DIR**>/configuration/

## Get the official MeSH RDF dataset ##

Download the official MeSH RDF dataset **mesh.nt.gz** at https://nlmpubs.nlm.nih.gov/projects/mesh/rdf/

> You might use **curl** tool for downloading

    curl https://nlmpubs.nlm.nih.gov/projects/mesh/rdf/mesh.nt.gz --ssl-no-revoke -O
          
## Get the translation RDF dataset ##

> If you have not translated MeSH before - you can proceed to [Import](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets#import-the-rdf-datasets).

### Convert the official UMLS TSV file ###

Use the **trans_only_YYYY_extended.txt** and convert it with the **mesh-trx2nt** tool.

The file MUST have the following columns/items:

    DescriptorUI | ConceptUI | Language | TermType | String | TermUI | ScopeNote | Tree | Created | Relation | ParentCUI	

- the header row is optional
- the TermUI column is always empty
- the Relation and ParentCUI need to be present at rows with *Custom Concepts* (ConceptUI starts with **F...**) and TermType **PEP** only

Display help - open CMD and run:
    
     mesh-trx2nt -h

```
usage: mesh-trx2nt inputFile meshxPrefix [options]

Extracting translation dataset from NLM UMLS text file [trans_only_2023_expanded.txt]

positional arguments:
  inputFile    NLM UMLS text file name (plain or gzipped)
  langcode     Language code
  meshxPrefix  MeSH Translation namespace prefix ie. http://my.mesh.com/id/

options:
  -h, --help   show this help message and exit
  --out OUT    Output file name prefix
```

**IMPORTANT**

The **langcode** parameter **MUST be the same** as the **TARGET_LANG** value in your **mtw.ini config file** ! 

The **meshxPrefix** parameter **MUST be the same** as the **TARGET_NS** value in your **mtw.ini config file** ! 

**Run the conversion** - open CMD and run ie.:
    
     mesh-trx2nt trans_only_2023_extended.txt fr http://id.mesh.fr/ 


### Convert the official MTMS XML file - OBSOLETE ###

Download your ***.xml.gz** translation file at
    
    [ftp://nlmpubs.nlm.nih.gov/online/mesh/MESH_FILES/mtms/](ftp://nlmpubs.nlm.nih.gov/online/mesh/MESH_FILES/mtms/)
    
    or
    
    [ftp://ftp.nlm.nih.gov/online/mesh/MESH_FILES/mtms/](ftp://ftp.nlm.nih.gov/online/mesh/MESH_FILES/mtms/)

Extract translation data from MeSH XML as N-triples dataset using **mesh-xml2trx** tool
  
- Run the extraction script:
    
        mesh-xml2trx *.xml.gz <TARGET_NS>

    **IMPORTANT:  TARGET_NS** - target namespace parameter - the custom URI prefix for you translation - it **MUST be the same** as TARGET_NS used in your **mtw.ini config file** ! 

    https://github.com/filak/MTW-MeSH/blob/master/flask-app/instance/conf/mtw.ini

    ie.
    
        mesh-xml2trx czedesc2018.xml.gz http://mesh.medvik.cz/link/


## Import the RDF datasets ##

0. **ALWAYS validate the input files** - the official annual RDF dataset and your RDF translation dataset

    Run the validation:
        
        riot --validate mesh.nt.gz

        riot --validate mesh-trx_YYYY-MM-DD.nt.gz

    No output = data is OK

1. Move the input files into a versioned <**IMPORT**> directory ie.  .../MeSH-data/2023/import/

2. Load the MeSH datatset(s) into Apache Jena

    **Stop Fuseki server instance (if running)**
    
    Go to your <**IMPORT**> directory
    
    Run the import:
        
        tdb2_tdbloader --loc %FUSEKI_BASE%/databases/mesh mesh.nt.gz mesh-trx_...
    
    or if you do not have a translation then just:
    
        tdb2_tdbloader --loc %FUSEKI_BASE%/databases/mesh mesh.nt.gz

3. Create Fuseki search index
   
    Go to your <**FUSEKI_DATA_DIR**>
   
    Run the indexation:
    
        java -cp %FUSEKI_HOME%/fuseki-server.jar jena.textindexer --desc=configuration/mesh.ttl
    
4. [Start Fuseki server](https://github.com/filak/MTW-MeSH/wiki/Running-Fuseki-server) instance

## Loading data from a backup ##

1. **Stop MTW services**

2. **Stop your Fuseki instance**

3. Go to your <**FUSEKI_DATA_DIR**> 
and make sure the <**mesh**> directories under datatabases and indexes dirs are empty !

    Run the import: 

        tdb2_tdbloader --loc %FUSEKI_BASE%/databases/mesh %FUSEKI_BASE%/backups/mesh_YYYY-MM-DD_....nq.gz

    Create the search index - run:

        java -cp %FUSEKI_HOME%/fuseki-server.jar jena.textindexer --desc=configuration/mesh.ttl

4. Start your Fuseki instance

5. Start MTW services

Continue to [MeSH Annual Updates](https://github.com/filak/MTW-MeSH/wiki/MeSH-Annual-Updates)