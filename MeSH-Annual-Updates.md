> You can update more often if required - just repeat the steps.

1. ALWAYS perform the checks and resolve any issues - ie. duplicates, locks, pending changes etc.

2. Export required datasets from MTW - ie. UMLS TSV, MARC etc.

3. Backup your <**mesh**> dataset using Fuseki interface

4. ALWAYS validate the backup - run:
    
        riot --validate mesh_YYYY-MM-DD_....nt.gz 

5. Extract the translation from the backup using **mesh-nt2trx** tool - run:
    
        mesh-nt2trx %FUSEKI_BASE%\backups\mesh_YYYY-MM-DD_....nq.gz

6. **Stop MTW Server and MTW Worker services**

7. **Update MTW config file for new target year** 

    <MTW_HOME_DIR>\instance\conf\mtw.ini 

8. **Perform steps 4 to 8** in [Loading MeSH datasets](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets)

9. Start MTW Server and MTW Worker services