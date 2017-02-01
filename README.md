# Caddy tutorial

This repo is about learning [Caddy](https://caddyserver.com/) web server.

The official documentation can be found here: [https://caddyserver.com/docs](https://caddyserver.com/docs)

## Why Caddy

- easy to setup and use
- https by default with __no conguration__ needed (from let's encrypt)
- HTTP/2, IPv6, Markdown, WebSockets, gzip, basic auth, templates and more right out of the box
- build for designer, bloggers and developers

## Setup

1. Download Caddy: https://caddyserver.com/download
2. Create a config which is namend `Caddyfile` and add the following minimal config
    ```
    localhost:8080 {
        root www
    }
    ```
3. Put your web assets into the `www` folder
4. Start Caddy with `caddy`. If your config file is not in the same 
directory as you are you can use it via the `conf` option like `-conf="DIR_TO_CONF/Caddyfile"`

To start the example servers within this repo (configuration and caddy itself) hit

```
# Mac
./bin/mac/caddy

# Windwos
bin\win64\caddy.exe

# Linux
./bin/linux64/caddy
```

## Feature deep-dive

All configuration is made in the `Caddyfile`. There are a lot of build in features but some need to be added to the binary.
You have to re-download Caddy with the additional features if you want to use one of them, it cant be added afterwards.

The following features are all build-in. If a feature must be added to the binary it is marked with an `A` in the documentation.

### Ext

[Docs](https://caddyserver.com/docs/ext)

Ext allows you to make clearer URLs by allowing to leave out the file extension in the URL

```
ext .html .md
```

With the example above the user can now go to the `hello.html` file with either `/hello.html` or `/hello`.

### Errors

[Docs](https://caddyserver.com/docs/errors)

You can map HTTP errors to specific pages

```
errors {
    404 notfound.html
    503 serviceunavail.html
}
```

### Markdown

[Docs](https://caddyserver.com/docs/markdown)

Caddy can render markdown files out of the box

```
markdown
```

The markdown files can also be served with custom css and js.

### basicauth

[Docs](https://caddyserver.com/docs/basicauth)

You can protect files and directories with simple basic auth

```
basicauth user password {
    /secret
}
```

### Logs

[Docs](https://caddyserver.com/docs/log)

Caddy will log every request when you add the log tag.

```
log / logs/access.log
```

Theres an easy [syntax](https://caddyserver.com/docs/placeholders) to format the logs to your needs.

### gzip

[Docs](https://caddyserver.com/docs/gzip)

gzip enabled gzip support if the client supprots it.

```
gzip
```

### Proxy

[Docs](https://caddyserver.com/docs/proxy)

Caddy can server as proxy

```
proxy /hypem hypem.com:80 {
    without /hypem
}
```

This will proxy all `/hypem` requests to `hypem.com`. If we would not add the `without` tag the request would be proxied with the host in the URL.
Example URL: `http://localhost:8080/hypem/playlist/popular/3day/json/1/data.js`

### Load balancer

[Docs](https://caddyserver.com/docs/proxy)

Load balancer is part of the proxy feature. There are some policy features available as well as health checks to only server to working servers.

```
localhost:2016 {
    proxy / localhost:8080 localhost:8081 {
        policy random
    }
}
```

## Further reading

- [Run Caddy as service with systemd](https://denbeke.be/blog/servers/running-caddy-server-as-a-service-with-systemd/)
- [Install caddy via command line with https://getcaddy.com/](https://getcaddy.com/)
- [Caddy FAQ](https://caddyserver.com/docs/faq)

Made with :heart: at [SinnerSchrader](https://sinnerschrader.com)
