---
theme: default
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  Presentation from the BSC about Containers.
drawings:
  persist: false
transition: slide-left
title: Intro to Containers
layout: bsc-title
venue: Online
date: 'yes'
hideInToc: true
fonts:
  sans: 'Calibri'
  fallback: false
slides-title: Intro to Containers
slides-date: '15/06/2023'
slides-venue: 'BSC-CES - MWT'
---

# Intro to Containers

---
layout: bsc-default
hideInToc: true
---

<div class="center1">

# Bruno P. Kinoshita

Research Engineer

<p>
Computational Earth Sciences | Earth Sciences Department<br />
Barcelona Supercomputing Center - Centro Nacional de Supercomputación<br />
Address: C/ Jordi Girona, 31, 08034 Barcelona | Torre Girona, 2nd Floor<br />
BSC Website: https://www.bsc.es/<br /></p>

</div>

---
layout: bsc-default
hideInToc: true
---

# Agenda

<Toc :maxDepth="2" />

---
layout: bsc-intro
hideInToc: true
---

# Containerization

---
layout: bsc-default
---

## Prerequisites

If you would like to try the examples in these slides, you will need to:

<br/>

- [Install Docker](https://docs.docker.com/engine/install/ubuntu/)
- Be able to run `docker run hello-world`
- Have Singularity (CE > 3.7) installed (optional)
- Have Docker and Singularity compose tools (optional)
- Have ~10 GB at least to spare, as well as good Internet connectivity.

<br/>

> NOTE: The example code snippets in this presentation may take several minutes to complete.
> If you are attending a session of this presentation, try running `docker pull
> image_name:version` before the presentation begins.

---
layout: bsc-default
---

# Containerization

Containerization is a way to run applications in an isolated environment.

It can take place at **OS level** and at **application level**.

This talk is about **containerization at OS level**, more specifically about containers with Docker (with a little about Singularity).

![](/images/containers-vms.png) [^1]

[^1]: [Trend Micro (2022). The Difference Between Virtual Machines and Containers](https://www.trendmicro.com/zh_hk/devops/22/e/the-difference-between-virtual-machines-and-containers.html)

---
layout: bsc-default
level: 2
---

# Some context and history

Containers are based on features of Kernel that have been available for
quite some years (`chroot`, and Linux namespaces such as `cgroups`).

Containers did not start with Docker, but Docker was responsible for
its recent widespread use in software development.

<!-- Namespaces are a feature of the Linux kernel that partitions kernel
resources such that one set of processes sees one set of resources while
another set of processes sees a different set of resources. -->

Refs: [^1][^2][^3]

<div style="font-size: 0.8rem;">

- 1997: Unix V7 adds `chroot`
- 2000: FreeBSD jails
- 2004: Solaris containers
- 2005: Open VZ (Open Virtuoso) (unreleased patch of Linux Kernel)
- 2006: Process Containers (Google)
- 2008: LXC (first container manager!)
- 2013: Docker (used LXC initially, then replaced by libcontainer)
- 2015: Open Container Initiative (Linux Foundation, `runc`)
- 2015: Singularity (Lawrence Berkeley National Lab)
- 2016: udocker (Python tool to execute Docker containers without root)
- 2017: Charliecloud (daemonless, rootless for HPC, created in 2015, but paper from 2017)
- 2018: Podman (daemonless, OS, uses OCI containers and images - compatible with Docker)
- 2019: Spack added the `spack containerize` command (#14202)

</div>


<!--
  - The first hypervisor providing full virtualization appeared in January 1967 - IBM
    https://en.wikipedia.org/wiki/Hypervisor#Mainframe_origins
-->

[^1]: https://blog.aquasec.com/a-brief-history-of-containers-from-1970s-chroot-to-docker-2016
[^2]:  https://en.wikipedia.org/wiki/Linux_namespaces
[^3]:  https://github.com/opencontainers/runc

---
layout: bsc-default
level: 2
---

# Why containers?

- Test software in a safely sandboxed environment
- Faster development lifecycle
  - Faster than managing multiple local envs or VM's
- Isolate applications
- Create portable environments
  - More portable than VM's [^1]
- Scalability
- Cloud computing
- Disaster recovery
- Lower footprint than servers or virtual machines
  - In both memory, computing, and carbon[^2] (more in the next slide)
  - (Or at least for the cloud[^3], I need to find HPC studies)

[^1]: [Containers vs VMs (virtual machines) (Google Cloud)](https://cloud.google.com/discover/containers-vs-vms)
[^2]: [Anusooya, G. & Varadarajan, Vijayakumar. (2021)](https://www.researchgate.net/figure/Overall-comparisons-between-container-and-VM-Table12_fig7_333096446)
[^3]: [Application platform considerations for sustainable workloads on Azure](https://learn.microsoft.com/en-us/azure/well-architected/sustainability/sustainability-application-platform#containerize-workloads-where-applicable)

---
layout: bsc-default
level: 2
---

Refs: [^1][^2] (networking plays an important role, valid for cloud, HPC may have different numbers.)

<div style="max-height: 80%;">
<div style="display: grid; grid-template: 100% / 50% 50%;">
<img src="/images/container-vm-footprint.png" style="height: 80%">
<img src="/images/container-vm-footprint2.png" style="float:right; height: 80%">
</div>
</div>

[^1]: [G. Anusooya Vijayakumar Varadarajan (2021), Reduced carbon emission and optimized power consumption technique using container over virtual machine](https://www.researchgate.net/figure/Comparative-results-of-4-containers-vs-1-VM-Table9_fig4_333096446)
[^2]: [Roberto Morabito (2015), Power Consumption of Virtualization Technologies: an Empirical Investigation](https://arxiv.org/abs/1511.01232)

---
layout: bsc-intro
level: 2
hideInToc: true
---

# Demo (follow along!)

---
layout: bsc-default
level: 2
---

# Running Docker containers with the command-line

Try these commands!

```bash
# Run a terminal in Debian Bullseye slim image with Micromamba
$ docker run -ti -u 1000:1000 mambaorg/micromamba:bullseye-slim
(base) mambauser@5df690afaa1d:/tmp$

# Run a terminal in the latest Ubuntu release
$ docker run -ti ubuntu:latest
root@51a769cec6c0:/#

# Run an old version of Linux Alpine 2.7.18 Python 2.7.3
$ docker run -ti python:2.7.18-alpine3.11
Python 2.7.18 (default, Apr 20 2020, 19:51:05) 
[GCC 9.2.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> 

# Start the terminal instead of Python
$ docker run -ti python:2.7.18-alpine3.11 /bin/ash
/ # 

# Execute some Python 2 code with an environment variable
$ docker run -ti -e WORLD=Earth python:2.7.18-alpine3.11 python2 -c \
  'import os; print "Hello " + os.environ["WORLD"]'
Hello Earth
```

---
layout: bsc-default
level: 2
hideInToc: true
---

# Running Docker containers with the command-line

```bash
# Look at all the mess you made!
$ docker ps -a
CONTAINER ID   IMAGE                               COMMAND                   CREATED          STATUS                        PORTS     NAMES
78ec649e58b2   python:2.7.18-alpine3.11            "python2 -c 'print \"…"   11 seconds ago   Exited (0) 10 seconds ago               dazzling_franklin
18f61a30ceb4   python:2.7.18-alpine3.11            "/bin/ash"                18 seconds ago   Exited (0) 16 seconds ago               heuristic_vaughan
d8a7cace5eb3   python:2.7.18-alpine3.11            "python2"                 20 seconds ago   Exited (0) 18 seconds ago               quirky_germain
64bf9b4b81bc   ubuntu:latest                       "/bin/bash"               32 seconds ago   Exited (130) 29 seconds ago             pedantic_maxwell
f9085a740dd1   mambaorg/micromamba:bullseye-slim   "/usr/local/bin/_ent…"    50 seconds ago   Exited (0) 48 seconds ago               angry_leavitt
3ca48baf860d   mambaorg/micromamba:bullseye-slim   "/usr/local/bin/_ent…"    5 minutes ago    Up 5 minutes                            stoic_moser
```

<br />

```bash
# Show system information
$ docker system df
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          3         3         243.7MB   0B (0%)
Containers      6         1         587.6kB   587.6kB (100%)
Local Volumes   0         0         0B        0B
Build Cache     0         0         0B        0B
```

---
layout: bsc-default
level: 2
hideInToc: true
---

# Other useful commands

```bash
# View all the images you have downloaded
$ docker image ls
...

# Remove the containers you have created
$ docker container prune -f
Deleted Containers:
0e121a312675fafb2933f3def49e488c0b9b20fcb93aafb094e923bcc90a9605
111f533d7cd177f7e8b65e083dfff1335ef39830d94dbf9917a7a1b10882cfc7
bec5117a015484334b9e5368c8be70f1c609d3ac93a55ab3b67a0a92954dcd73
77ee9570b2dcf055c527d7dfdd363cbb3699b66295540be14923189435b68ad4

Total reclaimed space: 587.6kB

# See everything you have running
$ docker ps -a
...

# Or volumes or networks
$ docker network list
$ docker volume list
...
```

---
layout: bsc-default
level: 2
hideInToc: true
---

# Other useful commands

```bash
# You can clean up volumes, networks, images, containers, etc.

$ docker volume prune -f
Deleted Volumes:
95c54fdcf9fa352203d7c1e009a19f2cfeebcef29cca5fb54bed923df60e701c

Total reclaimed space: 478.3MB
```

<br/>

<v-click>

```bash
# Or do what I do from time to time
$ docker system prune -a -f
...
Total reclaimed space: 3.189GB
```

</v-click>

---
layout: bsc-default
level: 2
hideInToc: true
---

# More useful commands

```bash
# Run a container that will auto-delete itself when its process exists
$ docker run --rm python:2.7.18-alpine3.11

# Run a container with a name, as a daemon (in the background)
$ docker run -d --rm --name python2test python:2.7.18-alpine3.11
27909a75647fbd8bb700fcdc2e25019958a8d0ecda74227a1f74793e8caf4cab
...
Total reclaimed space: 3.189GB

```

---
layout: bsc-default
level: 2
---

# Using a Dockerfile

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```

`RUN`, `ADD`, and `COPY` create new layers. Layers are cached for
performance. Other commands create temporary layers that are discarded
after the container is built.

---
layout: bsc-default
level: 3
---

# Multi-stage builds

---
layout: bsc-default
level: 2
---

# Creating a Singularity container

---
layout: bsc-default
level: 2
---

# Testing on the HPC

---
layout: bsc-default
level: 2
---

# Volumes and persisting data

---
layout: bsc-default
level: 2
---

# Deploying containers

---
layout: bsc-default
level: 2
---

# Container orchestration ({Docker, Singularity} Compose, Kubernetes, …)

---
layout: bsc-intro
---

# Best practices

---
layout: bsc-default
level: 3
hideInToc: true
---

# Docker development

1. Keep your images small
    - (For Cloud environments it is important, but for HPC not so much)
    - Use a smaller image for production, but additional debug tooling added for troubleshooting
    - Use [multistage builds](https://docs.docker.com/build/building/multi-stage/) and leverage the [build cache](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#leverage-build-cache)
    - Use `docker image history $image` to view the layers in your image
2. Use official images where possible
3. Create **ephemeral containers**
4. Manage your build context (see `.dockerignore`)
5. Avoid storing application data in the container
    - Use volumes or bind mounts
6. Limit each container to one process and application (whenever that is possible)
7. Add labels to add metadata to your image (license, author, release information, etc.)
8. Use `RUN set -o pipefail && cmd1 | cmd2` if you want to use pipes (Docker uses `/bin/sh -c`)
9. Declare network ports used in `EXPOSE`
10. Expose environment variables for the software with `ENV`
11. `COPY` is preferred over `ADD` whenever possible

<!--
COPY requirements.txt /tmp/
RUN pip install --requirement /tmp/requirements.txt
COPY . /tmp/

Is better than

COPY requirements.txt /tmp/
COPY . /tmp/
RUN pip install --requirement /tmp/requirements.txt

Since COPYing new files will invalidate the RUN pip layer.
-->

---
layout: bsc-default
level: 2
hideInToc: true
---

# References

These slides are based on (links with underscore):

- [Docker development best practices](https://docs.docker.com/develop/dev-best-practices/)
- [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Image-building best practices](https://docs.docker.com/get-started/09_image_best/)
- [Security best practices](https://docs.docker.com/develop/security-best-practices/)
- DestinE Barcelona Coding Sprint CSC presentation
- [Best practices for building and running Docker and Singularity containers](https://www.admin-magazine.com/mobile/HPC/Articles/More-Best-Practices-for-HPC-Containers)

---
layout: bsc-default
---

# Security

- Use official images
- Use the right context
- Use [secrets](https://docs.docker.com/engine/swarm/secrets/) to store sensitive application data
- If you are using a `:latest` base image, rebuild your image to get the latest updates
- Use security scanning tools to check your image for vulnerabilities

---
layout: bsc-thank-you
slides-email: bruno.depaulakinoshita
---
