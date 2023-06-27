# Alnoda workspaces compose 

This repo contains example of docker-compose that can be used to launch 
self-hosted Alnoda workspaces with docker compose. 

To start Alnoda workspace on a cloud server with basic authentication: 

- Make sure server has docker and docker compose 
- Make sure ports 8020 - 8040 are not blocked by the firewall. For example in Ubuntu/Debian 

```
ufw allow 8020:8040/tcp
```

- Clone repository 

```
git clone https://github.com/bluxmit/wrk-compose.git
```

- Set environmental variable `WRK_HOST` - public server IP which allows access over the Internet

```
export WRK_HOST=34.194.12
```

- start workspace 

```
cd basic-auth; docker-compose up -d
```

Now you can open browser on __http://[WRK_HOST]:8020__
