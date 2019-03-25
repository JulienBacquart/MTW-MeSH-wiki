* Always start Fuseki from your <**FUSEKI_DATA_DIR**>

* In testing or development environments open Command prompt and run:
    
        fuseki-server --localhost

* For production/deployment set up a service (https://jena.apache.org/documentation/fuseki2/fuseki-run.html)
   
    ie. on Windows using [NSSM](https://nssm.cc/):
     
        java -Xmx8192M -jar %FUSEKI_HOME%\fuseki-server.jar --localhost
   
* Check if the server is running:
    
    http://localhost:3030

> The server needs to "warm-up" - load data into memory - which might take up to 10 minutes