title: Phil's Docker Presentation
theme: sjaakvandenberg/cleaver-dark
progress: true
encoding: utf-8
output: presentation.html
controls: true
author:
    name: Phil Porada
    url: http://greenlancer.com
    email: philporada@gmail.com && pporada@greenlancer.com
    twitter: pgporada

-- center

### Docker: There and Back Again
<img src='images/detroit.png' style='margin: 0 auto; display: block'></img>

--

### Who am I?
* *Name*: Phil Porada
<img src='images/us.jpg' style='margin: 0 auto; display: block; width: 400px; height: 400px'></img>

--

### Who am I?
* *Name*: Phil Porada
* *Occupation*: Linux Engineer
<img src='images/pumpkin.jpg' style='margin: 0 auto; display: block; width: 400px; height: 400px'></img>

--

### Who am I?
* *Name*: Phil Porada
* *Occupation*: Linux Engineer
* *Workplace*: GreenLancer
<img src='images/gl-logo.png' style='margin: 0 auto; display: block; width: 800px; height: 200px'></img>

--

### What is Docker?
* Words

--

### What Docker is NOT
* Containers are not VMs nor will ever be
    * *VMs*: Think of each VM as an individual house
    * *Containers*: Think of them as units in an apartment

--

### Docker Requirements

--

### Basic Docker Commands
Show running docker containers
```sh
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
a870e1ec8f92           httpd               "httpd-foreground"   2 seconds ago       Up 1 seconds        80/tcp              jovial_jones

```

### Troubleshooting
Show docker containers in any state
```sh
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
a870e1ec8f92           httpd                 "httpd-foreground"  2 seconds ago       Up 1 seconds        80/tcp              jovial_jones
0601aae9ccaa           467fe3d6319c       "/bin/sh -c 'mkdir -p"    1 hour ago         Exited (1) 1 hour ago                 cocky_perlman
44e21f1e0eae           centos:centos7     "-it bash"                1 hour ago         Created                               naughty_stallman
```

---

### How can we actually use this in our day to day jobs?

