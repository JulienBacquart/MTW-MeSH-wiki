## For testing and development

Run [standalone server](https://jena.apache.org/documentation/fuseki2/fuseki-webapp.html#fuseki-standalone-server)

- Go to your <**FUSEKI_DATA_DIR**> open CMD and run: 
    
      fuseki-server --localhost

## For production/deployment 

Run [Fuseki service](https://jena.apache.org/documentation/fuseki2/fuseki-webapp.html#fuseki-service)

Windows service - **Use the [NSSM](https://nssm.cc) service manager**

    nssm.exe install ApacheJenaFuseki

Set:
```
    - Path:   java
    - Startup dir:   %FUSEKI_BASE%
    - Arguments:   -Xmx8192M -jar %FUSEKI_HOME%/fuseki-server.jar --localhost
```
   
## Check if the server is running
    
http://localhost:3030

> The server needs to "warm-up" - load data into memory - which might take up to 5-10 minutes