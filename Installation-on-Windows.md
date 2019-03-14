## Install Java 8 JRE 

* Apache Jena/Fuseki requires Java 8 JRE https://www.oracle.com/technetwork/java/javase/downloads/

* Test the installation - open Command prompt and run:

        java -version

## Install Apache Jena/Fuseki

1. Download Jena/Fuseki binary files at https://jena.apache.org/download/index.cgi

2. Unpack the distribution files to <**JENA_HOME_DIR**>, <**FUSEKI_HOME_DIR**>

3. Create a directory to store your data <**FUSEKI_DATA_DIR**>

4. Create/Set environmental (ENV) variables:

    JENAROOT     <JENA_HOME_DIR>    
    JENA_HOME    <JENA_HOME_DIR>    
    FUSEKI_HOME  <FUSEKI_HOME_DIR>    
    FUSEKI_BASE  <FUSEKI_DATA_DIR>

5. Add to your PATH variable

        ;%JENA_HOME%\bat;%FUSEKI_HOME%

6. Modify fuseki-server.bat in your <FUSEKI_HOME_DIR>

    Change:
      
        java -Xmx1200M -jar fuseki-server.jar %*
        
    to:
        
        java -Xmx8192M -jar %FUSEKI_HOME%\fuseki-server.jar %*

7. Test the installation - open Command prompt and run:
 
        fuseki-server --version

## Install SQLite database engine

1. Download SQLite3 binary files at https://www.sqlite.org/download.html

2. Unpack the distribution file to your <**SQLITE_HOME_DIR**>

3. Create/Set environmental (ENV) variable

    SQLITE_HOME  <SQLITE_HOME_DIR>

4. Add to your PATH variable

        ;%SQLITE_HOME%

5. Test the installation - open Command prompt and run:

        sqlite3 --version

## Install MTW Server

1. Download distribution file from [Releases](https://github.com/filak/MTW-MeSH/releases)

2. Unpack dist file to <**MTW_HOME_DIR**>

3. Install the **services**
    
    Go to your <**MTW_HOME_DIR**>

    Run:

          mtw-server-win-service.exe install
        
          mtw-server-win-worker.exe install

4. Set Admin credentials using **set-mtw-admin.exe** - run:

        set-mtw-admin --login <YOUR_ADMIN_LOGIN> --pwd <YOUR_ADMIN_PASSWORD>

5. Create the **management database**
    
    Go to  <**MTW_HOME_DIR**>\instance\db
    
    Run:

        sqlite3 mtw.db < mtw_schema.sql

6. Customize the **config file** - important values are marked with **!**
     
    <**MTW_HOME_DIR**>\instance\conf\mtw.ini

7. Create/Set environmental (ENV) variable

    MTW_HOME  <MTW_HOME_DIR>

8. Add to your PATH variable

        ;%MTW_HOME%\tools
    
9. Start the services
    
    Go to your <**MTW_HOME_DIR**>
    
    Run:
    
        mtw-server-win-service.exe start

        mtw-server-win-worker.exe start

    Note host:port
    
    > mtw-server-win-service - MTW Server - localhost:55930
    
    > mtw-server-win-worker - MTW Server Worker - localhost:55933    
    
10. Check if MTW server is running
    
    http://localhost:55930/mtw


## Continue to [Loading MeSH datasets](https://github.com/filak/MTW-MeSH/wiki/Loading-MeSH-datasets) ##