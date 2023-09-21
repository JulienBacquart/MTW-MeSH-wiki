# Examples #

> Always copy the contents of the *static* dir to *home/htdocs/assets-mtw* and keep the dirs in sync when upgrading MTW !

## Apache HTTP Server ##

> Production

```
<VirtualHost *:443>
  ServerName mtw.example.com
  DocumentRoot "home/htdocs"
  SSLEngine on
  UseCanonicalName On
  ProxyPreserveHost On

  ErrorLog "logs/mtw-error.log"
  CustomLog "logs/mtw-access.log" common

  <Directory "home/htdocs">
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
  </Directory>

  <Location "/mtw">
    ProxyPass "http://localhost:55930/mtw"
    ProxyPassReverse "http://localhost:55930/mtw"
  </Location>

</VirtualHost>

```

## Caddy Server v1 ##

> Testing

https://github.com/caddyserver/caddy/releases/tag/v1.0.4

```
mtw.example.com:443 {
    root home/htdocs
    log / logs/mtw-access.txt "{remote} - {user} [{when}] \"{method} {uri} {proto}\" {status} {size}"
    errors logs/mtw-error.txt
    ## development only:
    tls self_signed
    ## production ie.:
    # tls certs/crt.txt certs/key.txt
    gzip
    proxy /mtw localhost:55930 {
        transparent
        keepalive 0
    }
}

```


