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
layout: fact
hideInToc: true
---

# Intro to Containers

Intro, Basics, Best Practices

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space (or right arrow) for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/kinow" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
layout: intro
hideInToc: true
---

# Bruno P. Kinoshita

Research Engineer

<div class="absolute bottom-0px pt-6">
  <p>
  Computational Earth Sciences | Earth Sciences Department<br />
  Barcelona Supercomputing Center - Centro Nacional de Supercomputación<br />
  Address: C/ Jordi Girona, 31, 08034 Barcelona | Torre Girona, 2nd Floor<br />
  BSC Website: https://www.bsc.es/<br /></p>
</div>

---
layout: default
hideInToc: true
---

# Agenda

<Toc />

---
layout: default
---

# Containerization

Containerization is a way to run applications in an isolated environment.

It can take place at **OS level** and at **application level**.

This talk is about containerization at OS level, more specifically about Docker and Singularity.

<v-click>

## Prerequisites

If you would like to try the examples in these slides, you will need:

- Docker installed
- Be able to run `docker run hello-world`
- Singularity (CE) installed (optional)
- Docker and Singularity compose tools (optional)
- ~10 GB at least to spare, as well as good Internet connectivity.

</v-click>

---
layout: default
level: 2
---

# Some context and history

Containers are based on features of Kernel that have been available for
quite some years (`chroot`, and Linux namespaces such as `cgroups`).

Containers did not start with Docker, but Docker was responsible for
its widespread use in software development.

<!-- Namespaces are a feature of the Linux kernel that partitions kernel
resources such that one set of processes sees one set of resources while
another set of processes sees a different set of resources. -->

<v-clicks>

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

</v-clicks>

<!-- Refs:
  - https://blog.aquasec.com/a-brief-history-of-containers-from-1970s-chroot-to-docker-2016
  - https://en.wikipedia.org/wiki/Linux_namespaces
  - https://github.com/opencontainers/runc
-->

<!--
  - The first hypervisor providing full virtualization appeared in January 1967 - IBM
    https://en.wikipedia.org/wiki/Hypervisor#Mainframe_origins
-->

---
layout: default
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
  - In both memory, computing, and carbon[^2][^3]

[^1]: [Containers vs VMs (virtual machines) (Google Cloud)](https://cloud.google.com/discover/containers-vs-vms)
[^2]: [Anusooya, G. & Varadarajan, Vijayakumar. (2021)](https://www.researchgate.net/figure/Overall-comparisons-between-container-and-VM-Table12_fig7_333096446)
[^3]: 

---
layout: two-cols
level: 2
---

![](/images/containers-vms.png) [^1]

::right::

![](/images/container-vm-footprint.png) [^2]

[^1]: [The Difference Between Virtual Machines and Containers](https://www.trendmicro.com/zh_hk/devops/22/e/the-difference-between-virtual-machines-and-containers.html)
[^2]: [G. Anusooya Vijayakumar Varadarajan (2021), Comparative results of 4 containers vs 1 VM (Table 9)](https://www.researchgate.net/figure/Comparative-results-of-4-containers-vs-1-VM-Table9_fig4_333096446)
---
layout: default
level: 2
---

# Running Docker containers with the command-line

---
layout: default
level: 2
---

# Using a Dockerfile

---
layout: default
level: 2
---

# Creating a Singularity container

---
layout: default
level: 2
---

# Testing on the HPC

---
layout: default
level: 2
---

# Container orchestration ({Docker, Singularity} Compose, Kubernetes, …)

---
layout: default
---

# Best practices

---
layout: default
---

# Security
