# Alnoda workspaces compose 

This repo contains example of docker-compose that can be used to launch 
self-hosted Alnoda workspaces with docker compose. 

## HTTP

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

- set authentication as environmental variable WRK_AUTH, for example 

```
export WRK_AUTH=admin:$$2y$$05$$eub6CV.CwUYCCQjNBvSf5uZnzdRmVwGZ/ncxecb9O7WxCR8aLuM3K
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


## Authentication

Authentication in this example `admin:$$2y$$05$$eub6CV.CwUYCCQjNBvSf5uZnzdRmVwGZ/ncxecb9O7WxCR8aLuM3K` is 

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

Enter password on prompt and __htpasswd__ wil produce credential, for example _someuser:$$2y$$05$$t2MSJSPp2V9HdLWYq9z.UeYFz2R3un9ZuiBitSjeiN3Osz6fGNZ7u_ 

Set your own credentials as environmental variable 

```
export WRK_AUTH=someuser:$$2y$$05$$t2MSJSPp2V9HdLWYq9z.UeYFz2R3un9ZuiBitSjeiN3Osz6fGNZ7u
```


## HTTP

__Using HTTP to run workspaces on a remote server lacks sufficient security, as it's not encrypted like HTTPS. This method should be avoided unless you're operating workspaces within an internal network.__

You  start Alnoda workspace on a cloud server with basic authentication __over http__ use another docker-compose file: 

```
cd basic-auth-http; docker-compose up -d
```

Now you can open browser on __http://[WRK_HOST]:8020__