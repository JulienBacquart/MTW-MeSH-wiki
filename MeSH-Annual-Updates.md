Check MeSH RDF release notes: https://hhs.github.io/meshrdf/release-notes

1. Download the official MeSH RDF dataset https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets#get-the-official-mesh-rdf-dataset

2. **ALWAYS** perform the checks and resolve any issues in MTW - ie. duplicates, locks, pending changes etc.

3. **Export required output files from MTW** - ie. UMLS TSV, MARC, stats etc.

4. **BACKUP** your <**mesh**> dataset using Fuseki interface

5. Validate the backup and the official MeSH RDF dataset - run:
    
        riot --validate mesh_YYYY-MM-DD_....nt.gz
        riot --validate mesh.nt.gz

   No output = data is OK

6. Extract the translation from the backup using **mesh-nt2trx** tool - run:
    
        mesh-nt2trx %FUSEKI_BASE%\backups\mesh_YYYY-MM-DD_....nq.gz

7. **Stop MTW Server and MTW Worker services**

8. Go to your <**FUSEKI_DATA_DIR**> and DELETE the <**mesh**> directories under datatabases and indexes dirs

9. **Update MTW config file**  for new target year/period

    <MTW_HOME_DIR>\instance\conf\mtw.ini 

10. Follow the steps in [Import the RDF datasets](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets#import-the-rdf-datasets)

11. Clear the MTW cache - delete all files in *instance/cache*

12. Start MTW Server and MTW Worker services

13. **Reset the Initial stats in Manage dashboard**
