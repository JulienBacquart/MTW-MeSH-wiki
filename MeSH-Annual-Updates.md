Check MeSH RDF release notes: https://hhs.github.io/meshrdf/release-notes

> You can update more often than annually if required - just repeat the steps.

Download: https://nlmpubs.nlm.nih.gov/projects/mesh/rdf/

Use curl if browser fails:

     curl https://nlmpubs.nlm.nih.gov/projects/mesh/rdf/mesh.nt.gz.sha1 -O 
     curl https://nlmpubs.nlm.nih.gov/projects/mesh/rdf/mesh.nt.gz -O

1. ALWAYS perform the checks and resolve any issues - ie. duplicates, locks, pending changes etc.

2. Export required datasets from MTW - ie. UMLS TSV, MARC etc.

3. **BACKUP** your <**mesh**> dataset using Fuseki interface

4. ALWAYS validate the backup - run:
    
        riot --validate mesh_YYYY-MM-DD_....nt.gz

   No output = data is OK

5. Extract the translation from the backup using **mesh-nt2trx** tool - run:
    
        mesh-nt2trx %FUSEKI_BASE%\backups\mesh_YYYY-MM-DD_....nq.gz

6. **Stop MTW Server and MTW Worker services**

7. **Stop Fuseki server instance (if running)**

8. Go to your <**FUSEKI_DATA_DIR**> and DELETE the <**mesh**> directories under datatabases and indexes dirs

9. **Update MTW config file**  for new target year/period

    <MTW_HOME_DIR>\instance\conf\mtw.ini 

10. **Perform steps 4 to 8** in [Loading MeSH datasets](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets#initial-data-loading)

11. Clear the MTW cache - delete all files in *instance/cache*

12. Start MTW Server and MTW Worker services

13. **Reset the Initial stats in Manage dashboard**