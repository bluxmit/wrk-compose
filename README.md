# Alnoda workspaces compose 

This repo contains example of docker-compose that can be used to launch 
self-hosted Alnoda workspaces with docker compoose. 

To launch Alnoda workspace on a cloud server with basic authentication: 

- Make sure server has docker and docker compose 
- Clone repository 

```
git clone https://github.com/bluxmit/wrk-compose.git
```

- Set environmental variable `WRK_HOST` - public server IP which allows access over the Internet

```
export ENV=34.194.12
```

- start workspace 

```
cd basic-auth; docker-compose up -d
```
