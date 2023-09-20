* In testing or development environments

    Go to your <**FUSEKI_DATA_DIR**> open CMD and run:
    
        fuseki-server --localhost

* For production/deployment set up a service (https://jena.apache.org/documentation/fuseki2/fuseki-run.html)
   
    ie. on Windows using [NSSM](https://nssm.cc/) - run:

        nssm.exe install ApacheJenaFuseki

    Set:
    - Path:   java
    - Startup dir:   %FUSEKI_BASE%
    - Arguments:   -Xmx8192M -jar %FUSEKI_HOME%\fuseki-server.jar --localhost
   
* Check if the server is running:
    
    http://localhost:3030

> The server needs to "warm-up" - load data into memory - which might take up to 5-10 minutes