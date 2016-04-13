title: Phil's Docker Presentation
theme: pgporada/cleaver-dark
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

# Docker: There and Back Again
<img src='images/detroit.png' style='margin: 0 auto; display: block'></img>

--

### Who am I?
* **Name**: Phil Porada
<img src='images/us.jpg' style='margin: 0 auto; display: block; width: 400px; height: 400px'></img>

--

### Who am I?
* **Name**: Phil Porada
* **Occupation**: Linux Engineer
<img src='images/pumpkin.jpg' style='margin: 0 auto; display: block; width: 400px; height: 400px'></img>

--

### Who am I?
* **Name**: Phil Porada
* **Occupation**: Linux Engineer
* **Workplace**: GreenLancer located in downtown Detroit, MI
<img src='images/gl-logo.png' style='margin: 0 auto; display: block; width: 800px; height: 200px'></img>

--

### Who am I?
* **Name**: Phil Porada
* **Occupation**: Linux Engineer
* **Workplace**: GreenLancer located in downtown Detroit, MI
* **Beer**: Yes, please! <img src='images/beers.png' style='margin: 0 auto; display: block; width: 64px; height: 64px;'>
<img src='images/hopslam.jpg' style='margin: 0 auto; display: block; width: 800px; height: 400px'></img>

--

### Agenda
* <font color="#ff000">Requirements, Terminology, Intro to Docker, & Expectation Management</font>
* Docker Commands, Troubleshooting
* Troubleshooting
* ===== DEMO =====
* Writing your own Dockerfiles
* Developer Workflow
* ===== DEMO =====
* Docker Security
* Docker Networking
* Cleanup
* ===== DEMO =====
* Day to day Docker usage @ GreenLancer
* Questions and Answers

--

### Docker Requirements

| <font color="#00cc00">Runtime Dependency</font> | <font color="#00cc00">Version</font> |
| --- | --- |
| iptables    | >= 1.4 |
| git         | >= 1.7 |
| procps (ps) | any |
| xz compression engine | >= 4.9 |
<hr style="height:2pt; visibility:hidden;" />

| <font color="#00cc00">Kernel Version</font> | <font color="#00cc00">Does it work?</font> | <font color="#00cc00">Notes</font> |
| --- | --- | --- |
| >= 3.10 | Yes | Installed on RHEL/CentOS7 out of the box. |
| >= 3.16 | Yes | Needed for multi-host networking on Swarm. Can be acquired via ELRepo |
| < 3.10  | No | Do not use an older version of Docker. This technology evolves quickly. |

* Docker Dependencies: https://docs.docker.com/engine/installation/binaries/
* CentOS 6 ELRepo kernel: https://docs.docker.com/engine/installation/binaries/

--

### Docker Terminology
<hr style="height:2pt; visibility:hidden;" />

|  Docker Term | Definition  |
| :-- | -- |
| Layer | Read-only files that have run to provision the system. |
| Image | Basis of all containers. |
| Container | A running image. |
| Registry | Centralized place to store containers. |
| Manifest | Contains the name, tag, history, etc of an image. |
| Container ID/CID |A SHA256 checksum of the entire image manifest. |

<img src='images/multilayer-container.png' style='margin: 0 auto; display: block; width: 600px; height: 500px'></img>

--

### What is Docker?
* Words

--

### What Docker is NOT
* Containers are not VMs nor will ever be
    * **VMs**: Think of each VM as an individual house
    * **Containers**: Think of them as units in an apartment

--

### Agenda
* Requirements, Terminology, Intro to Docker, & Expectation Management
* <font color="#ff000">Docker Commands</font>
* Troubleshooting
* ===== DEMO-1 =====
* Writing your own Dockerfiles
* Developer Workflow
* ===== DEMO-2 =====
* Docker Security
* Docker Networking
* Cleanup
* ===== DEMO-3 =====
* Day to day Docker usage @ GreenLancer
* Questions and Answers

--

### Commands
#### docker ps
Process oriented API that shows running docker containers
```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
a870e1ec8f92           httpd               "httpd-foreground"   2 seconds ago       Up 1 seconds        80/tcp              jovial_jones
```

--

### Troubleshooting

Show docker containers in any state
```
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
a870e1ec8f92           httpd                 "httpd-foreground"  2 seconds ago       Up 1 seconds        80/tcp              jovial_jones
0601aae9ccaa           467fe3d6319c       "/bin/sh -c 'mkdir -p"    1 hour ago         Exited (1) 1 hour ago                 cocky_perlman
44e21f1e0eae           centos:centos7     "-it bash"                1 hour ago         Created                               naughty_stallman
```

--

### Starting containers
####docker run $CID
* Run a container in the foreground
```
$ docker run httpd
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 10.250.1.3. Set the 'ServerName' directive globally to suppress this message
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 10.250.1.3. Set the 'ServerName' directive globally to suppress this message
[Mon Apr 11 23:59:08.108723 2016] [mpm_event:notice] [pid 1:tid 140473353303936] AH00489: Apache/2.4.18 (Unix) configured -- resuming normal operations
[Mon Apr 11 23:59:08.108784 2016] [core:notice] [pid 1:tid 140473353303936] AH00094: Command line: 'httpd -D FOREGROUND'
```

* Run a container in the background
```
$ docker run -d httpd
e6902788cd79fd5782f2fdb464b9d061f12395aad1aa7a7487822764de3f811c

$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS               NAMES
e6902788cd79        httpd               "httpd-foreground"   5 hours ago         Up 5 hours          80/tcp              awesome_payne
```

--

### Troubleshooting
#### docker logs $CONTAINER
* Get logs from a container
```
$ docker logs e69
```

--

### Agenda
* Requirements, Terminology, Intro to Docker, & Expectation Management
* Docker Commands
* Troubleshooting
* <font color="#ff0000">===== DEMO-1 =====</font>
* Writing your own Dockerfiles
* Developer Workflow
* ===== DEMO-2 =====
* Docker Security
* Docker Networking
* Cleanup
* ===== DEMO-3 =====
* Day to day Docker usage @ GreenLancer
* Questions and Answers

-- center

# DEMO-1

--

### Agenda
* Requirements, Terminology, Intro to Docker, & Expectation Management
* Docker Commands
* Troubleshooting
* ===== DEMO-1 =====
* <font color="#ff0000">Writing your own Dockerfiles</font>
* Developer Workflow
* ===== DEMO-2 =====
* Docker Security
* Docker Networking
* Cleanup
* ===== DEMO-3 =====
* Developer Workflow
* Day to day Docker usage @ GreenLancer
* How to get help
* Questions and Answers

--

### Writing your own Dockerfiles

--

### Agenda
* Requirements, Terminology, Intro to Docker, & Expectation Management
* Docker Commands
* Troubleshooting
* ===== DEMO-1 =====
* Writing your own Dockerfiles
* Developer Workflow
* <font color='#ff0000'>===== DEMO-2 =====</font>
* Docker Security
* Docker Networking
* Cleanup
* ===== DEMO-3 =====
* Day to day Docker usage @ GreenLancer
* How to get help
* Questions and Answers

-- center

# DEMO-2

--

### Agenda
* Requirements, Terminology, Intro to Docker, & Expectation Management
* Docker Commands
* Troubleshooting
* ===== DEMO-1 =====
* Writing your own Dockerfiles
* Developer Workflow
* ===== DEMO-2 =====
* <font color='#ff0000'>Docker Security</font>
* Docker Networking
* Cleanup
* ===== DEMO-3 =====
* Day to day Docker usage @ GreenLancer
* How to get help
* Questions and Answers

--

### Docker Networking

--

### Cleanup

Docker images can eat up a lot of space, especially if you're constantly rebuilding and tagging.
```
$ docker images
REPOSITORY                              TAG                  IMAGE ID            CREATED             SIZE
greenlancer/jenkins-slave               latest               3bd6965573c9        5 hours ago         854.2 MB
greenlancer/jenkins-slave               0.4.0                c41c6fd546e9        30 hours ago        716.1 MB
greenlancer/jenkins-slave               0.3.0                122f48e241e5        30 hours ago        535.5 MB
greenlancer/jenkins-slave               0.2.0                7d930fd16086        30 hours ago        401.6 MB
greenlancer/jenkins-slave               0.1.0                e67c2d82f3d5        31 hours ago        401.6 MB
```

The total size of that on disk is



--

### Docker Security
#### Terminology
<hr style="height:2pt; visibility:hidden;" />

|  Docker Term | Explanation  |
| :-- | -- |
| Namespaces | Provides a view of the system that make the container appear to have all of the hosts resources. Examples are PIDs, Mounts, IPC, and Network. |
| User Namespaces | Distinguish container privileged vs host privileged root user. |
| Cgroups | |
| Capabilities | |
| AppArmor & SELinux | Allow containers to actually contain. |
| Seccomp | Acts as a syscall firewall. When a userland process wants to communicate with the kernel, communication travels through the syscall interface. This includes opening files, loading kernel modules, etc|

--

### How do we actually use this in our day to day jobs?

--

### How to get help
* Freenode IRC: #docker
* https://github.com/docker/docker/issues
* Google.

--

### Agenda
* Requirements, Terminology, Intro to Docker, & Expectation Management
* Docker Commands
* Troubleshooting
* ===== DEMO-1 =====
* Writing your own Dockerfiles
* Developer Workflow
* ===== DEMO-2 =====
* Docker Security
* Docker Networking
* Cleanup
* ===== DEMO-3 =====
* Day to day Docker usage @ GreenLancer
* How to get help
* <font color="#ff000">Questions and Answers</font>

-- center

# Q/A
<img src='images/qa.jpg' style='margin: 0 auto; display: block; width: 600px; height: 500px'></img>
