---
title: "Hello World!"
date: 2022-11-09T01:10:40+01:00
draft: false
tags:
    - Hello World!
comments: false
toc: false
featured: true
---
<!--
# Look this cool title!
## Other
### AAAA
#### tester

This is my first time using Hugo! This is a `monospaced text`

---

This is a section break with a box to highlight content like commands!
```
pixbuf_width / allocated_width = pixbuf_height / allocated_height
```
---
In this section, I can write links like google home page: [google](https://www.google.es)

---
Now, look this cute puppy:

![image alt text](/puppy.png)
<!-- Comentario -->	


<!--
---

Bloque de código en CSS:

```css
.custom-menu-tucked .custom-menu-screen {
    -webkit-transform: translateY(-44px);
    -moz-transform: translateY(-44px);
    -ms-transform: translateY(-44px);
    transform: translateY(-44px);
}
/* Retoques*/

.pure-menu {
    background-color: #FE0809;
    color: white;
    width: 100%;
    position: sticky;
}

.pure-menu a {
    color: white;
}

.pure-menu a:hover not(:first-child){
    background-color: green;/*#D40A0B;*/
}  
```
-->
# Hello World!
Welcome to our new IT site! Here we are going to post our projects. What is better beginning 
than releasing a website. We have three servers, one is reserved to important things, other
is where we locate all our projects and there is another one which is the f****** jungle.
And, guess what? For this moment, we are going to be allocated there, in lab server. Maybe, if everything
is OK, we migrate to a normal server. All commands named in this blog is refered to Linux SO´s.

How is suppose I´m goint to do that? Well, keep reading.

# First, we need a domain
It´s important to mention our server structure. Eurielec has his own DNS server, which depends of UPM network. It dump the domains
to the UPM server which publishes it. Eurielec has only one server connected to UPM´s network, stark.
Stark is connected over port 80. All other servers are connected by other ports to him. Well, how to add a new domain?

## Register the domain
Open a terminal with `Ctrl + Alt + t`  and write:
```
ssh ha100da@ha100da´s IP -p ha100da´s access port
```
Now, we are connected via ssh to ha100da´s server.

---

List all containers:

```
sudo docker ps
```
See there´s a bind dns server´s docker. If you want to check there´s no domain called as we want.
In our case, we are creating this page, so the domain is `it.eurielec.etsit.upm.es`. If you
want to check it, try this command `curl domain`. For example, `curl it.eurielec.etsit.upm.es`,
the output will be something similar to this: `curl: (6) Could not resolve host: ittutorial.eurielec.etsit.upm.es`.

---

Go to `/data/bind_dns_server/data/bind/etc/eurielec.db` and write in service´s section your
domain. Update the serial (line 17) with the `date +%s` output´s
```
docker exec -it bind_dns_server named-checkzone eurielec.etsit.upm.es /etc/bind/euriel$
```
With this command we are synchronizing the time.
Now restart the docker to upload the domain to the server and allow it to dump to UPM´s server.

---

Restart the container:
```
docker restart bind_dns_server
```
It´s done! Check your domain with the command `curl it.eurielec.etsit.upm.es`.

---

Go to Stark and change to `/opt/docker/traefik/docker-compose.yml` 
