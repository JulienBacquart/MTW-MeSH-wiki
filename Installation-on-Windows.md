## Install Java 8

* Apache Jena/Fuseki 3 requires Java 8 - https://adoptopenjdk.net/

> Command prompt = **CMD**

* Test the installation - open **CMD** and run:

        java -version

## Install Apache Jena/Fuseki

1. Download Jena and Fuseki binary files https://jena.apache.org/download/index.cgi

- Apache Jena Fuseki - ie. apache-jena-fuseki-4.9.0.zip
- Apache Jena libraries - ie. apache-jena-4.9.0.zip

2. Unpack the distribution files to <**JENA_HOME_DIR**>, <**FUSEKI_HOME_DIR**>

3. Create a directory to store your data <**FUSEKI_DATA_DIR**>

4. Create/Set environmental (ENV) variables:

    JENAROOT     <JENA_HOME_DIR>    
    JENA_HOME    <JENA_HOME_DIR>    
    FUSEKI_HOME  <FUSEKI_HOME_DIR>    
    FUSEKI_BASE  <FUSEKI_DATA_DIR>
   
    Ie. run in **CMD**:
 
```
setx /M JENAROOT c:\Programs\apache-jena-4.9.0
setx /M JENA_HOME c:\Programs\apache-jena-4.9.0
setx /M FUSEKI_HOME c:\Programs\apache-jena-fuseki-4.9.0
setx /M FUSEKI_BASE d:\apache-jena-data
 ```

5. Add to your **PATH** variable

        ;%JENA_HOME%\bat;%FUSEKI_HOME%

6. Modify **fuseki-server.bat** in your <FUSEKI_HOME_DIR>

    Change:
      
        java -Xmx1200M -jar fuseki-server.jar %*
        
    to (use 4096 MB or more):
        
        java -Xmx8192M -jar %FUSEKI_HOME%\fuseki-server.jar %*

7. Test the installation

    Go to your <**FUSEKI_DATA_DIR**>

    open **CMD** and run:
 
         jena_version.bat

         fuseki-server --version

8. For production see https://github.com/filak/MTW-MeSH/wiki/Running-Fuseki-server

## Install SQLite database engine

1. Download SQLite3 binary files at https://www.sqlite.org/download.html

    - use _Precompiled Binaries for Windows_ for your platform
   
    - do not forget to download the **sqlite-tools-...** package

2. Unpack the files to your <**SQLITE_HOME_DIR**>

3. Create/Set environmental (ENV) variable

    SQLITE_HOME  <SQLITE_HOME_DIR>

4. Add to your PATH variable

        ;%SQLITE_HOME%

5. Test the installation - open Command prompt and run:

        sqlite3 --version

## Install MTW as Windows service

1. Download distribution file **MTW-X.X.X.zip** from [Releases](https://github.com/filak/MTW-MeSH/releases/latest)

2. Unpack dist file to <**MTW_HOME_DIR**>

3. Install the **services** - MTW-Server and MTW-Worker

    Install [NSSM](https://nssm.cc) service manager
    
    Go to your <**MTW_HOME_DIR**> open **CMD** and run for both server and worker:

          nssm install <SERVICE_NAME>-<PORT>
        
    - Application - Path - select the EXE file ie.:

          C:\Programs\...\dist\mtw-server.exe

          C:\Programs\...\dist\mtw-worker.exe 

    - Application - Startup dir:

          C:\Programs\...\dist   

    - (optional) Application - Arguments - you can change host, port, threads count and config file:

            --config CONFIG    Config file path - default: conf/mtw-dist.ini
            --host HOST        Host - default: 127.0.0.1
            --port PORT        Port number - default: 55930 (server), 55933 (worker)
            --threads THREADS  Number of threads - default: 64
            --debug            Run in debug mode - DO NOT use in production !

4. Set Admin credentials using **set-mtw-admin.exe** - open **CMD** and run:

        set-mtw-admin --login <YOUR_ADMIN_LOGIN> --pwd <YOUR_ADMIN_PASSWORD>

5. Create the **management database**
    
    Go to  <**MTW_HOME_DIR**>\instance\db
    
    Open **CMD** and run:

        sqlite3 mtw.db < mtw_schema.sql

6. Customize the **config file** - important values are marked with **!**
     
    <**MTW_HOME_DIR**>\instance\conf\mtw-dist.ini

    https://github.com/filak/MTW-MeSH/blob/master/flask-app/instance/conf/mtw-dist.ini

7. Create/Set environmental (ENV) variable

    MTW_HOME  <MTW_HOME_DIR>

        setx /M MTW_HOME C:\Programs\...\dist\  

8. Add to your PATH variable

        ;%MTW_HOME%\tools
    
9. Start the services using Windows Services manager
    
10. Check the logs for any startup errors: <**MTW_HOME_DIR**>\instance\logs

11. **You need to setup a proxy** on you web server - see the [Deployment](https://github.com/filak/MTW-MeSH/wiki#deployment) instructions 

Continue to [Loading MeSH datasets](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets)