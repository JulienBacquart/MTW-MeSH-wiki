> Command prompt = **CMD**

## Apache Jena/Fuseki installation

Apache Jena/Fuseki 4 requires Java 11 JRE - use ie. https://adoptopenjdk.net/

* Test the installation - open **CMD** and run:

        java -version

1. Download Jena and Fuseki binary files https://jena.apache.org/download/index.cgi

    - Apache Jena Fuseki - ie. apache-jena-fuseki-4.10.0.zip
    - Apache Jena libraries - ie. apache-jena-4.10.0.zip

2. Unpack the distribution files to <**JENA_HOME_DIR**>, <**FUSEKI_HOME_DIR**>

3. Create a directory to store your data <**FUSEKI_DATA_DIR**>

4. Create/Set environmental (ENV) variables:

    JENAROOT     <JENA_HOME_DIR>    
    JENA_HOME    <JENA_HOME_DIR>    
    FUSEKI_HOME  <FUSEKI_HOME_DIR>    
    FUSEKI_BASE  <FUSEKI_DATA_DIR>
   
    - open **CMD** and run:
 
```
setx /M JENAROOT "C:\Programs\apache-jena-4.9.0"
setx /M JENA_HOME "C:\Programs\apache-jena-4.9.0"
setx /M FUSEKI_HOME "C:\Programs\apache-jena-fuseki-4.9.0"
setx /M FUSEKI_BASE "D:\apache-jena-data"
 ```

5. Add to your **PATH** variable

        ;%JENA_HOME%\bat;%FUSEKI_HOME%

6. Modify **fuseki-server.bat** in your <FUSEKI_HOME_DIR>

    Change:
      
        java -Xmx1200M -jar fuseki-server.jar %*
        
    to (use 4096 MB or more):
        
        java -Xmx8192M -jar "%FUSEKI_HOME%\fuseki-server.jar" %*

7. Test the installation - open **CMD** and run:
 

        jena_version.bat

        fuseki-server --version


    The output shall be:

         Apache Jena Fuseki version ...

> For production see [Running Fuseki server](https://github.com/filak/MTW-MeSH/wiki/Running-Fuseki-server)


## MTW Installation

### SQLite database

1. Download SQLite3 binary files at https://www.sqlite.org/download.html

    - use _Precompiled Binaries for Windows_ for your platform
   
    - do not forget to download the **sqlite-tools-...** package

2. Unpack the files to your <**SQLITE_HOME_DIR**>

3. Create/Set environmental (ENV) variable

    SQLITE_HOME  <SQLITE_HOME_DIR>

    Open **CMD** and run:

        setx /M SQLITE_HOME "C:\Programs\sqlite3"     

4. Add to your PATH variable

        ;%SQLITE_HOME%

5. Test the installation - open **CMD** and run:

        sqlite3 --version

### MTW binaries

1. Download distribution file **MTW-X.X.X.zip** from [Releases](https://github.com/filak/MTW-MeSH/releases/latest)

2. Unpack dist file to <**MTW_HOME_DIR**>

3. Create/Set environmental (ENV) variable

    MTW_HOME  <MTW_HOME_DIR>

    Open **CMD** and run:

        setx /M MTW_HOME "C:\Programs\MTW-1.6.5"  

    Append to your PATH variable:

        ;%MTW_HOME%\tools;%MTW_HOME%

4. Set Admin credentials using **set-mtw-admin.exe** - open **CMD** and run:

        set-mtw-admin --login <YOUR_ADMIN_LOGIN> --pwd <YOUR_ADMIN_PASSWORD>

5. Create the **management database**
    
    Go to  <**MTW_HOME_DIR**>\instance\db :

        cd %MTW_HOME%\instance\db
    
    Open **CMD** and run:

        sqlite3 mtw.db < mtw_schema.sql

6. Customize the **config file** - important values are marked with **!**
     
    <**MTW_HOME_DIR**>\instance\conf\mtw-dist.ini

    https://github.com/filak/MTW-MeSH/blob/master/flask-app/instance/conf/mtw-dist.ini

### Test/Start MTW

- MTW Worker - open **CMD** and run: 

        mtw-worker.exe

- MTW Server - open **CMD** and run:

        mtw-server.exe --port 80 --relax

- check the logs for any startup errors: <**MTW_HOME_DIR**>\instance\logs

- open in your browser **http://127.0.0.1/mtw/** and login with your Admin credentials [check the *Admin login* checkbox]

> For production deployment see [Running MTW as a service](https://github.com/filak/MTW-MeSH/wiki/Running-MTW-as-a-service)


Continue to [Loading MeSH datasets](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets)