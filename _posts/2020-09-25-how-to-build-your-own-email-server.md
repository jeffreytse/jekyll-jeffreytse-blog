---
layout: post
title: How to build your own email server
author: Jeffrey Tse
categories: computer
tags:
  - linux
  - docker
  - email
  - iredmail
---

## Introduction

Have you ever thought about setting up your own email server, but then
left it behind. However, setting up a email server is not complicated.
In this article, we will build it step by step from scratch.

Here we will need the following environments:

- **Nginx** - an lightweight and open-source web server to offer low
  memory usage and high concurrency.
- **Docker** - a set of platform as a service (PaaS) products that use
  OS-level virtualization to deliver software in packages called
  containers.
- **iRedMail** - The right way to build your mail server with open source
  softwares.

## Installation

we will install and configure all necessary software in order. And
following the steps you will almost get your own email server.

### Install iRedMail

For convenience, we use [docker-compose](https://docs.docker.com/compose/)
to defining and running the iRedMail applications, create the Compose file
with the name **iredmail.yml** and it's content below:

```yml
version: "3"

services:
  ehub_iredmail:
    container_name: iredmail
    image: lejmr/iredmail:mysql-latest
    restart: always
    hostname: mail.example.com
    networks:
      eztnet:
        ipv4_address: 172.20.0.2
    volumes:
      - iredmail_mysql:/var/lib/mysql
      - iredmail_vmail:/var/vmail
      - iredmail_clamav:/var/lib/clamav
    environment:
      DOMAIN: example.com
      HOSTNAME: mail
      MYSQL_ROOT_PASSWORD: password
      SOGO_WORKERS: 1
      TIMEZONE: "Europe/London"
      POSTMASTER_PASSWORD: password
      IREDAPD_PLUGINS: "['reject_null_sender', 'reject_sender_login_mismatch', 'greylisting', 'throttle', 'amavisd_wblist', 'sql_alias_access_policy']"

networks:
  eztnet:
    driver: bridge
    ipam:
      config:
        - subnet: 172.20.0.0/24

volumes:
  iredmail_mysql:
  iredmail_vmail:
  iredmail_clamav:
```

Building and running the service:

```bash
$ sudo docker-compose -f iredmail.yml up
```

Press **Ctrl+C (or Ctrl+\ )** to detach you from the container.

If you encounter **starting server(s) uwsgi failed**, you should do the
uwsgi checking:

![image](https://user-images.githubusercontent.com/9413601/94258050-d8f27b00-ff5e-11ea-825a-99be479017f9.png)

Attach to the container:

```bash
$ sudo docker exec -it iredmail /bin/bash
```

Run uwsgi with specific **iredmail.ini** mannually:

```bash
$ uwsgi --ini /etc/uwsgi/apps-available/iredadmin.ini
```

### Configuring DNS Records

Best practices for email authentication, here I recommend you always
set up these email authentication methods for your domain:

- **SPF** helps servers verify that messages appearing to come from a
  particular domain are sent from servers authorized by the domain
  owner.
- **DKIM** adds a digital signature to every message. This lets
  receiving servers verify that messages aren't forged, and weren't
  changed during transit.
- **DMARC** enforces SPF and DKIM authentication, and lets admins get
  reports about message authentication and delivery.

#### Create A record

```txt
mail.example.com  a
```

#### Create MX record

```txt
mail.example.com  mx
```

#### Create TXT record for SPF

```txt
v=spf1 ip4:<server_ip> ~all
```

or

```txt
v=spf1 mx mx:mail.example.com ~all
```

#### Create TXT record for DMARC

```txt
_dmarc.example.com  txt  v=DMARC1;p=reject;rua=mailto:admin@example.com; adkim=s;aspf=s
```

#### Create TXT record for DKIM

At frist, we need to attach to the container:

Find below setting in Amavisd config file `amavisd.conf` (find its [location on different Linux/BSD distributions](https://docs.iredmail.org/file.locations.html)):

```txt
dkim_key('example.com', "dkim", "/var/lib/dkim/example.com.pem");

@dkim_signature_options_bysender_maps = ( {
    ...
    "example.com"  => { d => "example.com", a => 'rsa-sha256', ttl => 10*24*3600 },
    ...
});
```

And then we need to get the DKIM keys:

```bash
$ amavisd-new showkeys
```

![image](https://user-images.githubusercontent.com/9413601/94256971-308fe700-ff5d-11ea-8209-f37b3227bc1a.png)

Now we copy the DKIM keys and create the TXT record:

```txt
dkim._domainkey.example.com v=DKIM1; p=MIIBIjANBgkqhkiG9...8ZEqo/QIDAQAB
```

Subsequently, we test the txt record:

```bash
$ amavisd-new testkeys
```

or

```bash
$ dig -t txt dkim._domainkey.example.com
```

![image](https://user-images.githubusercontent.com/9413601/94384986-7c69a880-0176-11eb-9c58-3a6c8af86291.png)

![image](https://user-images.githubusercontent.com/9413601/94406825-311abe80-01a5-11eb-8bd9-a3c0d5153433.png)

### Nginx config

Create the nginx site config:

```bash
$ sudo vim /etc/nginx/sites-available/iredadmin
```

Type the following content:

```NGINX
# mail.example.com
server {
  listen 80;

  server_name mail.example.com;
  access_log  /var/log/nginx/mail.example.com.access.log;

  location /.well-known/ {
    root /var/www/acme/;
  }

  location / {
    return 302 https://$host$request_uri;
  }
}

server {
  listen 443;

  # using web sub domain to access
  server_name mail.example.com;
  access_log  /var/log/nginx/mail.example.com.access.log;

  ssl_certificate       /etc/nginx/ssl/mail.example.com/fullchain.cer;
  ssl_certificate_key   /etc/nginx/ssl/mail.example.com/private.key;
  ssl_protocols         TLSv1 TLSv1.1 TLSv1.2;
  ssl_ciphers           HIGH:!aNULL:!MD5;
  ssl_prefer_server_ciphers on;

  location / {
    proxy_set_header        Host $host;
    proxy_set_header        X-Real-IP $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header        X-Forwarded-Proto $scheme;

    proxy_pass   https://172.20.0.2:443;
  }
}
```

Create the nginx stream config:

```bash
$ sudo vim /etc/nginx/streams-available/iredadmin
```

Type the following content:

```NGINX
# mail server proxy
server { listen 25; proxy_pass 172.20.0.2:25; }     # SMTP
server { listen 587; proxy_pass 172.20.0.2:587; }   # SMTP(STARTTLS)
server { listen 143; proxy_pass 172.20.0.2:143; }   # IMAP(STARTTLS)
server { listen 993; proxy_pass 172.20.0.2:993; }   # IMAP
server { listen 110; proxy_pass 172.20.0.2:110; }   # POP3
server { listen 995; proxy_pass 172.20.0.2:995; }   # POP3
```

And then create the symbolic links:

```bash
$ ln -s /etc/nginx/sites-available/iredmail /etc/nginx/sites-enabled/iredmail
$ ln -s /etc/nginx/streams-available/iredmail /etc/nginx/streams-enabled/iredmail
```

Afterwards, don't forget to restart the nginx service:

```bash
$ sudo service nginx force-reload
```

## Finish

Up to this point, all the installation work has been completed, and we
are almost about to get our own email server,

### Login iRedAdmin

Open the iredmail Admin:

```url
https://mail.example.com/iredadmin
```

Login use default account `postmaster@example.com`, and then create your
own email account.

![image](https://user-images.githubusercontent.com/9413601/94383952-12500400-0174-11eb-8169-4b0e6f66d64e.png)

![image](https://user-images.githubusercontent.com/9413601/94410082-8789fc00-01a9-11eb-8bfe-8e03c852be15.png)

### Test Email Server

For better use and no spammyness, we use [this free online service](https://www.mail-tester.com/) to test the emails for Spam, Malformed Content and Mail Server
Configuration problems.

If all goes well, we will get full marks, otherwise, we will get the tips
on current problems:

![image](https://user-images.githubusercontent.com/9413601/94257592-199dc480-ff5e-11ea-93f9-ad7e3c8dc127.png)

## References

- [Sign DKIM signature on outgoing emails for new mail domain](https://docs.iredmail.org/sign.dkim.signature.for.new.domain.html)
- [iRedMail Docker Container](https://github.com/lejmr/iredmail-docker)
