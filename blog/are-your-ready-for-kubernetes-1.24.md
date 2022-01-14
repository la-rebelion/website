---
layout: post
title: Are You Ready for Kubernetes v1.24?
description:  > # this means to ignore newlines until next YAML property
    Kubernetes is removing dockershim, what does it mean? Are you going to be impacted?
tags: [Kubernetes, Docker, Cloud]
---

Back in December 2020 Kubernetes announced deprecation of *dockershim* and Docker as a container runtime, but why?

Docker get born before Kubernetes, then, inevitably Kubernetes platform offered compatibility with the the only container runtime back there, the integration between Kubernetes and Docker was done through dockershim Kubernetes module. But, what happened when multiple container runtime engines emerged? Container Runtime Interface (CRI) plugin was introduced to tackle this problem: to interact with multiple container runtimes, but it was after Kubernetes developed dockershim.

CRI defines the API for container runtimes in Kubernetes. Then, CRI-O saw the light. 

> CRI-O is an implementation of the Kubernetes CRI (Container Runtime Interface) to enable using OCI (Open Container Initiative) compatible runtimes. It is a lightweight alternative to using Docker as the runtime for kubernetes. It allows Kubernetes to use any OCI-compliant runtime as the container runtime for running pods. - [What is CRI-O?](https://cri-o.io)

OCI (Open Container Initiative) is a Linux Foundation project to design open industry standards around container formats and runtimes. In 2015 Docker donated both a draft specification for the base format and runtime and the code associated with a reference implementation of that specification, to the OCI.


## Container, Docker, Image, OCI, CRI, CRI-O, what is all this about!?

Following image from Tutorial Works explains it in a nutshell!

![The relationship between Docker, CRI-O, containerd and runc – in a nutshell](https://www.tutorialworks.com/assets/images/container-ecosystem.drawio.png)

The relationship between Docker, CRI-O, containerd and runc – in a nutshell
*Source: Tutorial Works*

## Does your App have dependencies on Docker?

<meta name="twitter:card" content="summary" />
<div class="center">
<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Fascinating how this docker/docker-shim deprecation has created mass confusion. Probably should have seen it coming.<br><br>So many things called &quot;docker&quot;. The company, the dev experience, images, container instances.</p>&mdash; Joe Beda (@jbeda) <a href="https://twitter.com/jbeda/status/1334309564343177217?ref_src=twsrc%5Etfw">December 3, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>

https://twitter.com/jbeda/status/1334309564343177217

If you are using Docker for building your application containers, you can still run these containers on any container runtime. Don't worry, **this use of Docker does not count as a dependency on Docker as a container runtime.**

Following kubectl helps you to identify what is the Container runtime your cluster is using:

```sh
kubectl get nodes -o wide
NAME        STATUS   ROLES                  AGE    VERSION   INTERNAL-IP    EXTERNAL-IP   OS-IMAGE                KERNEL-VERSION                CONTAINER-RUNTIME
pompeiv51   Ready    control-plane,master   345d   v1.20.2   1xx.1xx.1xx.xxx   <none>        CentOS Linux 7 (Core)   3.10.0-1160.21.1.el7.x86_64   docker://20.10.5
```

And here are some ways to identify if you have dependency on Docker:

1. Review that Pods don't execute Docker commands (like `docker ps`), restart the Docker service (commands such as `systemctl restart docker.service`), or modify Docker-specific files such as `/etc/docker/daemon.json`.
2. If you have private registries or image mirror settings in the Docker configuration file (like `/etc/docker/daemon.json`), then, reconfigure those for another container runtime.
3. Make sure that scripts and apps running outside of your Kubernetes cluster **do not execute Docker commands**. i.e.:  

   * SSH to nodes to troubleshoot;
   * Node startup scripts;
   * Monitoring and security agents installed on nodes directly.


## What are the options available for Container engines other than Docker?

Following the list of container engines, CNCF [graduated](https://landscape.cncf.io/card-mode?project=graduated) or [incubated](https://landscape.cncf.io/card-mode?project=incubating):

## containerd

<img src="https://landscape.cncf.io/logos/containerd.svg" width="100">

An open and reliable container runtime

| Website    | containerd.io                    |
| :------------- | :--------------------- |
| Repository | github.com/containerd/containerd |

| Main languages | Percentage             |
| :-- | :-- |
| Go  | 98% |

## CRI-O

<img src="https://landscape.cncf.io/logos/cri-o.svg" width="100">

Open Container Initiative-based implementation of Kubernetes Container Runtime Interface

| Website        | cri-o.io               |
| :------------- | :--------------------- |
| Repository     | github.com/cri-o/cri-o |

| Main languages | Percentage             |
| :------------- | :--------------------- |
| Go             | 80%                    |
| Shell          | 18%                    |

## Firecracker

<img src="https://landscape.cncf.io/logos/firecracker.svg" width="100">

Secure and fast microVMs for serverless computing.

| Website        | firecracker-microvm.github.io              |
| :------------- | :----------------------------------------- |
| Repository     | github.com/firecracker-microvm/firecracker |

| Main languages | Percentage                                 |
| :------------- | :----------------------------------------- |
| Rust           | 78%                                        |
| Python         | 20%                                        |

## gVisor

<img src="https://landscape.cncf.io/logos/g-visor.svg" width="100">

Application Kernel for Containers

| Website        | gvisor.dev               |
| :------------- | :----------------------- |
| Repository     | github.com/google/gvisor |

| Main languages | Percentage               |
| :------------- | :----------------------- |
| Go             | 76%                      |
| C++            | 19%                      |

## Inclavare

<img src="https://landscape.cncf.io/logos/inclavare-containers.svg" width="100">

A novel container runtime, aka confidential container, for cloud-native confidential computing and enclave runtime ecosystem.

| Website        | inclavare-containers.io                 |
| :------------- | :-------------------------------------- |
| Repository     | github.com/alibaba/inclavare-containers |

| Main languages | Percentage                              |
| :------------- | :-------------------------------------- |
| C              | 57%                                     |
| Go             | 22%                                     |

## Kata

<img src="https://landscape.cncf.io/logos/kata-containers.svg" width="100">

Kata Containers version 2.x see https://github.com/kata-containers/kata-containers.

| Website        | katacontainers.io                  |
| :------------- | :--------------------------------- |
| Repository     | github.com/kata-containers/runtime |

| Main languages | Percentage                         |
| :------------- | :--------------------------------- |
| Go             | 97%                                |

## lxd

<img src="https://landscape.cncf.io/logos/lxd.svg" width="100">

Powerful system container and virtual machine manager

| Website        | linuxcontainers.org/lxd |
| :------------- | :---------------------- |
| Repository     | github.com/lxc/lxd      |

| Main languages | Percentage              |
| :------------- | :---------------------- |
| Go             | 89%                     |
| Shell          | 8%                      |

## rkt

<img src="https://landscape.cncf.io/logos/rkt.svg" width="100">

⚠️ This project has ended, and all development/maintenance activities have halted.

[Project ended] rkt is a pod-native container engine for Linux. It is composable, secure, and built on standards.

| Website        | github.com/rkt/rkt |
| :------------- | :----------------- |
| Repository     | github.com/rkt/rkt |

| Main languages | Percentage         |
| :------------- | :----------------- |
| Go             | 84%                |
| Makefile       | 7%                 |

## runc

<img src="https://landscape.cncf.io/logos/runc.svg" width="100">

CLI tool for spawning and running containers according to the OCI specification

| Website        | opencontainers.org             |
| :------------- | :----------------------------- |
| Repository     | github.com/opencontainers/runc |

| Main languages | Percentage                     |
| :------------- | :----------------------------- |
| Go             | 82%                            |
| Shell          | 13%                            |

## Singularity

<img src="https://landscape.cncf.io/logos/singularity.svg" width="100">

| Website        | sylabs.io                        |
| :------------- | :------------------------------- |
| Repository     | github.com/apptainer/singularity |

| Main languages | Percentage                       |
| :------------- | :------------------------------- |
| Go             | 93%                              |
| C              | 3%                               |

## SmartOS

<img src="https://landscape.cncf.io/logos/smart-os.svg" width="100">

Converged Container and Virtual Machine Hypervisor

| Website        | joyent.com/smartos             |
| :------------- | :----------------------------- |
| Repository     | github.com/joyent/smartos-live |

| Main languages | Percentage                     |
| :------------- | :----------------------------- |
| C              | 55%                            |
| JavaScript     | 32%                            |

Sysbox

<img src="https://landscape.cncf.io/logos/sysbox.svg" width="100">

An open-source, next-generation "runc" that empowers rootless containers to run workloads such as Systemd, Docker, Kubernetes, just like VMs.

| Website        | github.com/nestybox/sysbox |
| :------------- | :------------------------- |
| Repository     | github.com/nestybox/sysbox |

| Main languages | Percentage                 |
| :------------- | :------------------------- |
| Shell          | 94%                        |
| Makefile       | 4%                         |

## WasmEdge Runtime

<img src="https://landscape.cncf.io/logos/wasm-edge-runtime.svg" width="100">

WasmEdge is a lightweight, high-performance, and extensible WebAssembly runtime for cloud native, edge, and decentralized applications. It powers serverless apps, embedded functions, microservices, smart contracts, and IoT devices.

| Website        | wasmedge.org                 |
| :------------- | :--------------------------- |
| Repository     | github.com/WasmEdge/WasmEdge |

| Main languages | Percentage                   |
| :------------- | :--------------------------- |
| C++            | 81%                          |
| Rust           | 9%                           |

## References:

* [Check whether Dockershim deprecation affects you](https://kubernetes.io/docs/tasks/administer-cluster/migrating-from-dockershim/)
* https://kubernetes.io/blog/2016/12/container-runtime-interface-cri-in-kubernetes/
* https://www.tutorialworks.com/difference-docker-containerd-runc-crio-oci/
* https://snyk.io/blog/container-image-formats/
* https://opencontainers.org
* https://cri-o.io
* [How Dockershim’s Forthcoming Deprecation Affects Your Kubernetes](https://www.tripwire.com/state-of-security/security-data-protection/cloud/how-dockershim-forthcoming-deprecation-affects-your-kubernetes/)
* [Check whether Dockershim deprecation affects you](https://kubernetes.io/docs/tasks/administer-cluster/migrating-from-dockershim/check-if-dockershim-deprecation-affects-you/)

[1.](cri-o) 