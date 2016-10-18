# Learning Caddy

This project is used to learn [caddy server](https://caddyserver.com/).

## Start

To run the project on windows 64-bit simply hit
```
start.cmd
```

For mac use
```
start
```

## Features / Setup

- run caddy on `localhost:2020`
- server files from `www` directory
- log to `logs/access.log` 
- protect `/secrets` with basic auth
- proxy all requests from `/hypem` to `http://hypem.com` 

## Resources

- caddy homepage: https://caddyserver.com/
- caddy github: https://github.com/mholt/caddy
- caddy docs: https://caddyserver.com/docs
- install caddy via bash: https://getcaddy.com/
