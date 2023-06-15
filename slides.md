---
theme: default
class: text-center
highlighter: prism
lineNumbers: false
info: |
  Presentation from the BSC about Containers.
drawings:
  persist: false
transition: slide-left
title: Intro to Containers
layout: de-title
venue: Online
date: 'yes'
hideInToc: true
fonts:
  sans: 'Calibri'
  fallback: false
slides-title: Intro to Containers
slides-date: '15/06/2023'
slides-venue: 'BSC-CES - MWT'
slides-author: 'Bruno P. Kinoshita'
---

# Intro to Containers

---
layout: de-default
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
layout: de-default
hideInToc: true
---

# Agenda

<Toc :maxDepth="2"></Toc>

---
layout: de-intro
hideInToc: true
---

# Containerization

---
layout: de-default
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

> ※ NOTE: The example code snippets in this presentation may take several minutes to complete.
> If you are attending a session of this presentation, try running `docker pull
> image_name:version` before the presentation begins.

---
layout: de-default
---

# Containerization

Containerization is a way to run applications in an isolated environment.

It can take place at **OS level** and at **application level**.

This talk is about **containerization at OS level**, more specifically about containers with Docker (with a little about Singularity).

![](/images/containers-vms.png) [^1]

[^1]: [Trend Micro (2022). The Difference Between Virtual Machines and Containers](https://www.trendmicro.com/zh_hk/devops/22/e/the-difference-between-virtual-machines-and-containers.html)

---
layout: de-default
level: 2
---

# Some context and history

Containers are based on features of Kernel that have been available for
quite some years (`chroot`, and Linux namespaces such as `cgroups`).

Containers did not start with Docker, but Docker was responsible for
its recent widespread use in software development.

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


[^1]: https://blog.aquasec.com/a-brief-history-of-containers-from-1970s-chroot-to-docker-2016
[^2]:  https://en.wikipedia.org/wiki/Linux_namespaces
[^3]:  https://github.com/opencontainers/runc

<!--
Namespaces are a feature of the Linux kernel that partitions kernel
resources such that one set of processes sees one set of resources while
another set of processes sees a different set of resources. 

The first hypervisor providing full virtualization appeared in January 1967 - IBM
https://en.wikipedia.org/wiki/Hypervisor#Mainframe_origins
-->

---
layout: de-default
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
layout: de-default
level: 2
---

Refs: [^1][^2] (networking plays an important role, valid for cloud, HPC may have different numbers.)

<div style="display: grid; grid-template: 40% / 50% 50%; max-height: 85%;">
<img src="/images/container-vm-footprint.png" alt="Container footprint image 1">
<img src="/images/container-vm-footprint2.png" style="max-height: inherit;" alt="Container footprint image 2">
</div>

[^1]: [G. Anusooya Vijayakumar Varadarajan (2021), Reduced carbon emission and (…) using container over virtual machine](https://www.researchgate.net/figure/Comparative-results-of-4-containers-vs-1-VM-Table9_fig4_333096446)
[^2]: [Roberto Morabito (2015), Power Consumption of Virtualization Technologies: an Empirical Investigation](https://arxiv.org/abs/1511.01232)

---
layout: de-intro
level: 2
hideInToc: true
---

# Demo (follow along!)

<!--
Ask how many are following the demo.
-->

---
layout: de-default
level: 2
---

# Running Docker containers with the command-line

Try these commands!

```bash
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
$ docker run -ti -e WORLD=Earth python:2.7.18-alpine3.11 python2 -c 'import os; print "Hello " + os.environ["WORLD"]'
Hello Earth
```

You can try other images.

```bash
$ docker run -ti -u 1000:1000 mambaorg/micromamba:bullseye-slim
$ docker run -ti ubuntu:latest /bin/bash
```

---
layout: de-default
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
layout: de-default
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

<!--
You don't need to try all these commands. The slides are available.
-->

---
layout: de-default
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

<!--
No need to try.
-->

---
layout: de-default
level: 2
hideInToc: true
---

# More useful commands

```bash
# Run a container that will auto-delete itself when its process exits
$ docker run --rm python:2.7.18-alpine3.11

# Run a container with a name, as a daemon (in the background)
$ docker run -d --rm --name python2test python:2.7.18-alpine3.11
27909a75647fbd8bb700fcdc2e25019958a8d0ecda74227a1f74793e8caf4cab
```

<!--
If you keep running commands, you will only get more containers...
-->

---
layout: de-default
level: 2
---

# Creating images with Dockerfile

*File: Dockerfile*

```dockerfile
FROM python:2.7.18-alpine3.11
WORKDIR /app

COPY hello.txt .

RUN cat <<EOF > script.py
#!/usr/bin/python2

with open('hello.txt') as f:
  msg = f.read()
  print(msg)
  with open('/tmp/output.txt', 'w+') as o:
    o.write(msg)
    o.flush()

EOF

CMD ["python2", "script.py"]
```

`RUN`, `ADD`, and `COPY` create new layers. Layers are cached for
performance.

<!--
Paste this into the chat.
-->

---
layout: de-default
level: 2
hideInToc: true
---

# Creating images with Dockerfile

```bash 
$ echo "Hello World" > hello.txt
# The dot at the end is for the local dir, where Dockerfile is
$ docker build -t test-python:latest .
[+] Building 0.7s (9/9) FINISHED                                                
 => [internal] load .dockerignore                                          0.0s
 => => transferring context: 2B                                            0.0s
 => [internal] load build definition from Dockerfile                       0.0s
 => => transferring dockerfile: 231B                                       0.0s
 => [internal] load metadata for docker.io/library/python:2.7.18-alpine3.  0.0s
 => CACHED [1/4] FROM docker.io/library/python:2.7.18-alpine3.11           0.0s
 => [internal] load build context                                          0.0s
 => => transferring context: 48B                                           0.0s
 => [2/4] WORKDIR /app                                                     0.2s
 => [3/4] COPY hello.txt .                                                 0.0s
 => [4/4] RUN cat <<EOF > script.py                                        0.3s
 => exporting to image                                                     0.1s
 => => exporting layers                                                    0.1s
 => => writing image sha256:de797699e542f0fd08cd4321d434754334df8399d5b3c  0.0s
 => => naming to docker.io/library/test-python:latest                      0.0s
```

<!--
Remember to show that layers are cached.
-->

---
layout: de-default
level: 2
hideInToc: true
---

# Creating images with Dockerfile

What if you run that command again?

```bash {11,12,13}
$ docker build -t test-python:latest .
[+] Building 0.1s (9/9) FINISHED                                                
=> [internal] load build definition from Dockerfile                       0.0s
=> => transferring dockerfile: 231B                                       0.0s
=> [internal] load .dockerignore                                          0.0s
=> => transferring context: 2B                                            0.0s
=> [internal] load metadata for docker.io/library/python:2.7.18-alpine3.  0.0s
=> [1/4] FROM docker.io/library/python:2.7.18-alpine3.11                  0.0s
=> [internal] load build context                                          0.0s
=> => transferring context: 30B                                           0.0s
=> CACHED [2/4] WORKDIR /app                                              0.0s
=> CACHED [3/4] COPY hello.txt .                                          0.0s
=> CACHED [4/4] RUN cat <<EOF > script.py                                 0.0s
=> exporting to image                                                     0.0s
=> => exporting layers                                                    0.0s
=> => writing image sha256:de797699e542f0fd08cd4321d434754334df8399d5b3c  0.0s
=> => naming to docker.io/library/test-python:latest                      0.0s
```

---
layout: de-default
level: 2
hideInToc: true
---

# Creating images with Dockerfile

Your image should be available in your local environment now.

```bash
$ docker image ls test-python
REPOSITORY    TAG       IMAGE ID       CREATED          SIZE
test-python   latest    39b47fff6145   45 minutes ago   71.1MB
```

But no container.

```bash
$ docker ps -a --filter ancestor=test-python:latest
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

<v-click>

Yet!

```bash
# You can use `docker container run` too (newer syntax)
$ docker run --name test-python2 test-python:latest
Hello World

# Or `docker container ps` ...
$ docker ps -a --filter ancestor=test-python:latest
CONTAINER ID   IMAGE                COMMAND               CREATED              STATUS                          PORTS     NAMES
48ec9a91370e   test-python:latest   "python2 script.py"   About a minute ago   Exited (0) About a minute ago             test-python2
```

</v-click>

---
layout: de-default
level: 2
---

# Volumes and persisting data

The container runs a script with Python 2. This script writes to the stdout
and to a file on `/tmp/output.txt`.

But what if you wanted to access `output.txt`?

```bash
$ ls
Dockerfile  hello.txt
```

<v-click>

You can use a volume (similar to volumes in VM's like VirtualBox!), and
map the `/tmp` inside the container to a local directory.

```bash
$ docker run --rm -ti -v ${PWD}:/tmp test-python:latest
Hello World

$ ls
Dockerfile  hello.txt  output.txt

```

</v-click>

<!--
Any questions?
-->

---
layout: de-default
level: 2
hideInToc: true
---

# Volumes and persisting data

You can even modify the `hello.txt` file.

```bash
$ echo "Hola Món" > earth.txt
# In the host machine, it is `earth.txt`, but mapped as `hello.txt` in the guest.
$ docker run --rm -ti -v ${PWD}/earth.txt:/app/hello.txt test-python:latest
Hola Món

```

<br/>

<blockquote style="font-size: 20px">

※ NOTE:  Avoid persisting data inside your container, see best practices slides.

</blockquote>

Organize your container so that users can control input and output
<br/>
(imagine your container is a stateless math function)

If a container goes down, for whatever reason, start a new one using the same
shared volume. You can have multiple containers sharing the same volume, you
can mount volumes as readonly, and more.

---
layout: de-default
level: 2
---

# Networking

Quick example to show how to expose a port in Docker.

You can modify the command (`CMD`) executed by a container.

```bash
$ docker run --rm -ti test-python:latest python2 -m SimpleHTTPServer
Serving HTTP on 0.0.0.0 port 8000 ...
# CTRL + C

# Run is now as a daemon
$ docker run --rm -d test-python:latest python2 -m SimpleHTTPServer
cc38293a5265e609d76cd440b95e775175e6da72d03cccc098d8a35483e3878a

# Note the `PORT` column!
$ docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED          STATUS          PORTS     NAMES
cc38293a5265   test-python:latest   "python2 -m SimpleHT…"   34 seconds ago   Up 33 seconds             nifty_elion

$ docker stop cc38293a5265
cc38293a5265
```

<!--
You do not need to run all these commands.
-->

---
layout: de-default
level: 2
hideInToc: true
---

# Networking

```bash
# Specify a port to bind with `-p $HOST:$GUEST`
$ docker run --rm -d -p 7000:8000 test-python:latest python2 -m SimpleHTTPServer
34be3a39dc27516805d9698581e34edbc0da6f1f0e7843090cd3218830dd1c88

# Look at `PORT` now!
$ docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED              STATUS              PORTS                                       NAMES
34be3a39dc27   test-python:latest   "python2 -m SimpleHT…"   About a minute ago   Up About a minute   0.0.0.0:7000->8000/tcp, :::7000->8000/tcp   amazing_chebyshev
```

<v-click>

<img src="/images/docker-browser.png" style="max-height: 50%; float: right"  alt="Docker in a browser window"/>

</v-click>

<!--
Copy the command at the top to the chat.
-->

---
layout: de-default
level: 2
---

# Creating a Singularity container

You can write a Singularity file, download from Singularity Hub or Docker Hub, or use
a local Docker image.

```bash
# The chroot way... you can write to it with --writable
$ singularity build --sandbox test-python docker-daemon://test-python:latest
...

# Or build a single container file to be loaded into memory... (what I normally use)
$ sudo singularity build test-python.sif docker-daemon://test-python:latest
INFO:    Starting build...
2023/06/14 18:29:13  info unpack layer: sha256:c1f002e71ff26f48d9071266c88531cc7740de5f12a710395e68ea604ed4ff6a
2023/06/14 18:29:13  info unpack layer: sha256:7dfeae6c1959458377be7cb43c8d4bba4d64c09f2aa569b9806ef90ffa4bfae8
2023/06/14 18:29:13  info unpack layer: sha256:eae0303b3277085a9830077a7ff6e679ef772961676015d0418df72ac5de3582
2023/06/14 18:29:13  info unpack layer: sha256:e1a35eb1d0f6bcf41aef81ad625a2024de331991fc453573b6a4ab644f42aaf7
2023/06/14 18:29:14  info unpack layer: sha256:cdbb2ced0e763d99157788e6b3b1b04f63f442467a34cbfb35cd7ab6825f70da
2023/06/14 18:29:14  info unpack layer: sha256:f1cfa610d290fd7eaac1a5f60f8494c9703e042a2240b3b36eafa5e37c3f8ff5
2023/06/14 18:29:14  info unpack layer: sha256:fe2555b8984cba0a403a87269a257667fddc0f527231de75245d8fe9f2cf3c0d
INFO:    Creating SIF file...
INFO:    Build complete: test-python.sif
```

---
layout: de-default
level: 2
hideInToc: true
---

# Creating a Singularity container


The latter command gives you `test-python.sif` file. You can run the container now.

<br/>

```bash
$ singularity run test-python.sif 
/usr/local/bin/python2: can't open file 'script.py': [Errno 2] No such file or directory
```

<br/>

<v-click>

> ※ NOTE: You can convert Docker to Singularity. That does not mean everything will work
> automatically.
> Portability requires careful design (other examples: MPI, GPU.)

</v-click>

<br/>

<v-click>

```bash
$ singularity run --pwd /app test-python.sif
Hello World

$ singularity shell test-python.sif
Singularity> 
```

</v-click>

<v-click>

Singularity will mount your `$HOME` or `$PWD` (depending on the version)
and use as the working directory. In the default configuration, the system
default bind points are `$HOME`, `/sys:/sys` , `/proc:/proc`, `/tmp:/tmp`,
`/var/tmp:/var/tmp`, `/etc/resolv.conf:/etc/resolv.conf`, `/etc/passwd:/etc/passwd`,
and `$PWD`.

</v-click>

---
layout: de-default
level: 2
---

# Testing on the HPC

An exercise for you. Try running this, or another Docker → Singularity container
on your HPC.

Something like

```bash
# Upload it to some offline node, for example (or save to a NFS partition to use with computing nodes.)
bruno@bscearth000:~> scp test-python.sif bsc32...@mn2.bsc.es:/home/bsc32/bsc32..../

# Jump onto that host and load the Singularity module
bruno@bscearth000:~> ssh bsc32....@mn2.bsc.es
bsc32....@login2:~> module load Singularity

# Run the container
bsc32....@login2:~> singularity run --pwd /app test-python.sif
Hello World

```

That's that! You have a container that you can use on your laptop, in the cloud,
or in an HPC. For other solutions that involve MPI or GPU they may not
be as portable.

But containerization is a useful skill to have in your tool-belt, especially if
you collaborate with people from external institutions.

---
layout: de-default
level: 2
---

# Deploying containers

- You can deploy images locally (as you have seen in this talk)
- You can deploy images to Docker Hub or Singularity Hub
- You can deploy Singularity images to Singularity Registries (they can be installed as modules)
- You can deploy images to Quay.io
- You can deploy images to Biocontainers
- AWS has a registry for containers, as well as Google Cloud, OpenStack
- You can deploy to Docker Swarm
- You can deploy images to Kubernetes
- You can deploy images to GitHub Packages (limitations for free projects apply)
- …

---
layout: de-default
level: 2
---

# Container orchestration ({Docker, Singularity} Compose, Kubernetes, …)

Docker Swarm and Kubernetes are example of container orchestration tools.

They provide tools for deploying pods and using containers, and for scaling,
networking, securing, and maintaining containerized applications.

Docker Compose, and Singularity Compose are tools that also can be used to
manage clusters of containers. Users can declare how the containers must
be created and interlinked (networking, volumes). Useful when deploying more
than 1 container locally or remotely (especially if sharing with others).

There are other tools, some offered by cloud providers like AWS.

---
layout: de-intro
---

# Best practices

---
layout: de-default
level: 3
hideInToc: true
---

# Docker development

<div style="font-size: 0.9rem">

1. Keep your images small
    - (For Cloud environments it is important, but for HPC not so much)
    - Use a smaller image for production, but additional debug tooling added for troubleshooting
    - Use [multistage builds](https://docs.docker.com/build/building/multi-stage/) (※ [^1]!) and leverage the [build cache](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#leverage-build-cache)
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
12. Portability and reproducibility are hard. Test it! (Developing containers is software development!)

</div>

[^1]: This is omitted from the current version of this presentation, but it is an important
Docker concept.

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
layout: de-default
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
layout: de-thank-you
slides-email: bruno.depaulakinoshita
---

---
layout: de-default
hideInToc: true
---

# Security

- Use official images
- Use the right context
- Use [secrets](https://docs.docker.com/engine/swarm/secrets/) to store sensitive application data
- If you are using a `:latest` base image, rebuild your image to get the latest updates
- Use security scanning tools to check your image for vulnerabilities
- WIP, more to come!

---
layout: de-default
hideInToc: true
---

# Singularity and Docker

Pro Singularity

- Singularity has a single file, simplified I/O
- Simplified security model, more compatible with HPC
- Easier to work with Slurm (Docker has a daemon )

Con Singularity

- Docker has a wider user/knowledge base
- Docker is used by many types of software developers
- Docker has more containers ready-to-use

Other possible issues

- Singularity had a big rewrite from C to Go
- Singularity modified its file format (OCI should change it)
- Singularity, Singularity CE & Apptainer

Most HPC centers have their own set of instructions for users
to use Singularity, e.g. [Running MPI apps on Singularity at BSC MN4](https://www.bsc.es/supportkc/blog/)

---
layout: de-default
hideInToc: true
---

# HPC Examples

- hzdr.de recipe for Slurm in Docker <https://codebase.helmholtz.cloud/fwcc/slurm-in-docker>
- Sweden's PDC center for HPC instructions on using Singularity <https://www.pdc.kth.se/support/documents/software/singularity.html>
- NeSI (New Zealand) Knowledge Base entry on using Singularity <https://support.nesi.org.nz/hc/en-gb/articles/360001107916-Singularity>
- NCAR recipes for WRF with Docker <https://github.com/NCAR/WRF_DOCKER> & <https://github.com/NCAR/container-wrf>
- Singularity docs for MPI <https://docs.sylabs.io/guides/latest/user-guide/mpi.html>
- Auburn HPC docs about MPI and Slurm with Singularity <https://hpc.auburn.edu/hpc/docs/hpcdocs/build/html/easley/containers.html#parallel-mpi-code>
- Pawsey repository with container recipes (conda, mpi, OpenFoam, etc.) <https://github.com/PawseySC/pawsey-containers/tree/master>
- IFCA (ES) Docker containers for Distributed Training of Deep Learning Algorithms in HPC Clusters <https://github.com/IFCA/workflow-DL-HPC/>
- CANOPIE-HPC 2023 <https://canopie-hpc.org/cfp/>

---
layout: de-default
hideInToc: true
---

# Workflow Managers

- cwltool, reference CWL runner, uses containers (docker/udocker/podman/singularity) to isolate tasks (Cylc does so without containers)
- Snakemake supports Docker and singularity too
- Workflow Managers normally support Docker, and then add support to Singularity later. Science/Research Workflow Managers may be an exception to this rule.
- In some workflow managers users must decide if, and how to use containers (e.g. Autosubmit, Cylc, ecFlow)

---
layout: de-default
hideInToc: true
---

# Other

- https://container-in-hpc.org/ (they have a Slack channel too)
- #containers channel in Slack/Mattermost/etc.
-
