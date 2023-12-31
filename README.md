# Alnoda workspaces compose 

This repo contains example of docker-compose that can be used to launch 
self-hosted Alnoda workspaces with docker compose. 

## HTTPS

To start Alnoda workspace on a cloud server with basic authentication over https with self-signed certificate: 

- Make sure server has docker and docker compose 
- Make sure ports 8020 - 8040 are not blocked by the firewall. For example in Ubuntu/Debian 

```
ufw allow 8020:8040/tcp
```

- Clone repository 

```
git clone https://github.com/bluxmit/wrk-compose.git
cd wrk-compose
```

- Set environmental variable `WRK_HOST` - public server IP which allows access over the Internet, i.e.

```
export WRK_HOST=34.194.12
```

- start workspace 

```
cd basic-auth-https; docker-compose up -d
```

Now you can open browser on __https://[WRK_HOST]:8020__

## Other workspaces 

By default latest base Alnoda workspace will run.  

You can start another worksppace with evironmental variable _WRK_IMAGE_, for example 

```
export WRK_IMAGE='alnoda/codeserver-workspace:5.0'
```


## Basic authentication

the default authentication is 

- user: admin
- password: admin

You can create new login workspace with __htpasswd__. 

You can install htpasswd in any of the alnoda workspaces with 

```
sudo apt-get install apache2-utils -y
```

To create new user:password pair:

```
echo $(htpasswd -nB <userName>) | sed -e s/\\$/\\$\\$/g
```

where _<userName>_ - is the name of your user. 

Enter password on prompt and __htpasswd__ wil produce credentials, for example _someuser:$$2y$$05$$t2MSJSPp2V9HdLWYq9z.UeYFz2R3un9ZuiBitSjeiN3Osz6fGNZ7u_ 

You can use to replace in the respective docker-compose yaml file the label of a traefik service `traefik.http.middlewares.basic-auth.basicauth.users=admin:$$2y$$05$$eub6CV.CwUYCCQjNBvSf5uZnzdRmVwGZ/ncxecb9O7WxCR8aLuM3K`.


## HTTP

__Using HTTP to run workspaces on a remote server lacks sufficient security, as it's not encrypted like HTTPS. This method should be avoided unless you're operating workspaces within an internal network.__

You  start Alnoda workspace on a cloud server with basic authentication __over http__ use another docker-compose file: 

```
cd basic-auth-http; docker-compose up -d
```

Now you can open browser on __http://[WRK_HOST]:8020__