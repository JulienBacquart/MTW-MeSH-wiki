## Windows service

Install the MTW **services** - MTW-Server and MTW-Worker

Use the [NSSM](https://nssm.cc) service manager
    
1. Go to your <**MTW_HOME_DIR**> open **CMD** and run for both server and worker:

       nssm install <SERVICE_NAME>-<PORT>
        
- Application - Path - select the EXE file ie.:

       C:\Programs\...\dist\mtw-server.exe

       C:\Programs\...\dist\mtw-worker.exe 

- Application - Startup dir:

       C:\Programs\...\dist   

- (optional) Application arguments - you can change host, port, threads count and config file:

```
--config CONFIG    Config file path - default: conf/mtw-dist.ini
--host HOST        Host - default: 127.0.0.1
--port PORT        Port number - default: 55930 (server), 55933 (worker)
--threads THREADS  Number of threads - default: 64
--debug            Run in debug mode - DO NOT use in production !
```

2. Start the services using *Windows Services manager*

3. Check the logs for any startup errors: <**MTW_HOME_DIR**>\instance\logs

