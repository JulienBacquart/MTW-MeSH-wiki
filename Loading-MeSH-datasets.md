## Loading data from a backup ##

    tdb2_tdbloader --loc %FUSEKI_BASE%\databases\mesh %FUSEKI_BASE%\backups\mesh_YYYY-MM-DD_....nq.gz

## Initial data loading ##

Set up a Jena assembler config file

Copy file:

<**MTW_HOME_DIR**>\instance\conf\mesh.ttl

to:

<**FUSEKI_DATA_DIR**>\configuration\

> If you have not translated MeSH before - you can proceed to step 4.


1. Download your *.xml.gz translation file at
    
    [ftp://nlmpubs.nlm.nih.gov/online/mesh/MESH_FILES/mtms/](ftp://nlmpubs.nlm.nih.gov/online/mesh/MESH_FILES/mtms/)
    
    or
    
    [ftp://ftp.nlm.nih.gov/online/mesh/MESH_FILES/mtms/](ftp://ftp.nlm.nih.gov/online/mesh/MESH_FILES/mtms/)

2. Extract translation data from MeSH XML as N-triples dataset using **mesh-xml2trx** tool
  
    Run:
    
        mesh-xml2trx *.xml.gz <TARGET_NS>
   
    ie.
    
        mesh-xml2trx czedesc2018.xml.gz http://mesh.medvik.cz/link/

3. **ALWAYS validate the output file**
    
    Run:
        
        riot --validate mesh-trx_YYYY-MM-DD.nt.gz

4. Download the official MeSH RDF dataset mesh.nt.gz at [ftp://ftp.nlm.nih.gov/online/mesh/rdf/](ftp://ftp.nlm.nih.gov/online/mesh/rdf/)
   and validate the file - run:
    
        riot --validate mesh.nt.gz

5. Move the file(s) into a versioned <**IMPORT**> directory ie.  ...\MeSH-data\2019-1\import\

6. Load the MeSH datatset(s) into Apache Jena

    **Stop Fuseki server instance (if running)**
    
    Go to your <**IMPORT**> directory
    
    Run:
        
        tdb2_tdbloader --loc %FUSEKI_BASE%\databases\mesh mesh.nt.gz mesh-trx_YYYY-MM-DD.nt.gz ...
    
    ie:
    
        tdb2_tdbloader --loc %FUSEKI_BASE%\databases\mesh mesh.nt.gz mesh-trx_2018-12-19.nt.gz
    
    or if you do not have a translation then just:
    
        tdb2_tdbloader --loc %FUSEKI_BASE%\databases\mesh mesh.nt.gz

7. Create Fuseki search index
   
    Go to:  <**FUSEKI_DATA_DIR**>
   
    Run:
    
        java -cp %FUSEKI_HOME%\fuseki-server.jar jena.textindexer --desc=configuration/mesh.ttl
    
8. [Start Fuseki server](https://github.com/filak/MTW-MeSH/wiki/Running-Fuseki-server) instance