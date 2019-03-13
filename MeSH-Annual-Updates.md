# MeSH Annual Updates #

1. Export the annual datasets - ie. UMLS TSV, MARC etc.

2. Backup your <**mesh**> dataset using Fuseki interface

3. ALWAYS validate the backup - run:
    
        riot --validate mesh_YYYY-MM-DD_....nt.gz 

4. Extract the translation from the backup using **mesh-nt2trx** tool - run:
    
        mesh-nt2trx %FUSEKI_BASE%\backups\mesh_YYYY-MM-DD_....nq.gz

5. **Stop MTW Server and MTW Worker services**

6. **Update MTW config file for new target year** 

        <MTW_HOME_DIR>\instance\conf\mtw.ini 

7. **Perform steps 4 to 8** in [Loading MeSH datasets](https://bitbucket.org/filakx/mesh-translation-workflow-dev/wiki/Loading-MeSH-datasets)

8. Start MTW Server and MTW Worker services