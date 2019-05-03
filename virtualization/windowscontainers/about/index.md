---
title: About Windows Containers
description: Learn about Windows containers.
keywords: docker, containers
author: taylorb-microsoft
ms.date: 05/02/2016
ms.topic: article
ms.prod: windows-containers
ms.service: windows-containers
ms.assetid: 8e273856-3620-4e58-9d1a-d1e06550448

---
# Containers on Windows

## What containers are

Containers wrap up an application into its own isolated box. The application in its container has no knowledge of any other applications or processes that exist outside of its box. Everything the application depends on to run successfully also lives inside this container. Wherever the box may move, the application will always be satisfied because it's bundled up with everything it needs to run.

Imagine a kitchen. Inside this single room are all the appliances, furniture, pots and pans, the dish soap and hand towels, everything you need to have a functioning kitchen. This is our container.

![Kitchen analogy](media/box1.png)

We can now take this room and drop it into whatever host apartment we want. All we need to start cooking is to connect the room to power and water.

Why stop there? You can customize this room to be anything you want as long as it has everything it needs to function, whether it's a living room, an office, or a game room. You can put many different kinds of rooms in your host apartment, fill your building with identical rooms, or have a mix of the two.

![Apartment analogy](media/apartment.png)

Containers function very much like these portable rooms. The container is an isolated application that comes with everything it needs to run, and it can be dropped into any kind of host.

Watch this short overview to learn more:
<iframe width="800" height="450" src="https://www.youtube.com/embed/Ryx3o0rD5lY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Container fundamentals

Containers are an isolated, resource controlled, and portable runtime environment that runs on a host machine or virtual machine. An application or process that runs in a container is packaged with all the required dependencies and configuration files, giving it the illusion that nothing exists outside of its container. Because of this, the container will only use the resources its host provisions and won't touch any resources provisioned for other containers.

Let's get to know some terms you'll find useful as you begin to create and work with Windows containers.

- **Container host:** A physical or virtual computer system configured with the Windows container feature. The container host will run one or more Windows containers.

- **Sandbox:** When you start a container, all write actions like file system modifications, registry modifications, or software installations are captured in this ‘sandbox’ layer.

- **Container OS image:** Containers are deployed from images. The container OS image is the first layer in potentially many image layers that make up a container. This image provides the operating system environment. A Container OS Image is immutable. That is, it cannot be modified.

- **Container image:** As you modify a container's file system or registry, like when you install software, these modifications are captured in a sandbox. In some cases, you might want to capture a certain state of the sandbox so you can recreate that state in new containers. This captured state is called a container image. Once the container has stopped, you can either discard the sandbox or convert the sandbox into a new container image. For example, let’s say you've deployed a container from the Windows Server Core OS image. You then install MySQL into this container. If you create a new image from this container, you can deploy that image in a new container to carry over the changes from your first container. This image would only contain the changes you made to the first container (in this case, installing MySQL), but it would work as a layer on top of the container OS image instead of replacing it.

- **Container repository:** Each time you create a container image, the image and its dependencies are stored in a local repository. You can reuse these images many times on the container host. You can also store the container images in a public or private registry, such as Docker Hub, so they can be used across many different container hosts.

![Container fundamentals](media/containerfund.png)

Someone familiar with virtual machines might think containers seem similar to virtual machines. A container runs an operating system, has a file system, and can be accessed over a network much like a physical or virtual computer system. However, the technology and concepts behind containers are vastly different from virtual machines. To learn more about what these concepts are, read Mark Russinovich's [blog post](https://azure.microsoft.com/blog/containers-docker-windows-and-trends/) that explains the differences in more detail.

## Windows container types

Windows containers include two different container types, or runtimes.

Windows Server containers provide application isolation through process and namespace isolation technology. A Windows Server container shares a kernel with the container host and all containers running on the host. These containers don't provide a hostile security boundary and shouldn't be used to isolate untrusted code. Because of the shared kernel space, these containers require the same kernel version and configuration.

Hyper-V isolation expands on the isolation provided by Windows Server Containers by running each container in a highly optimized virtual machine. In this configuration, the container host doesn't share its kernel with other containers on the same host. These containers are designed for hostile multitenant hosting with the same security assurances of a virtual machine. Since these containers don't share the kernel with the host or other containers on the host, they can run kernels with different versions and configurations (within supported versions). For example, all Windows containers on Windows 10 use Hyper-V isolation to utilize the Windows Server kernel version and configuration.

Running a container on Windows with or without Hyper-V Isolation is a runtime decision. You can initially create the container with Hyper-V isolation, and then later at runtime choose to run it as a Windows Server container instead.

## What is Docker?

Docker is an automated process that packages and delivers container images. Docker produces images that can be run anywhere as a container, whether it's on premises, in the cloud, or on a personal machine.

![Containers with Docker](media/docker.png)

Just like any other container, a Windows Server container can be managed with [Docker](https://www.docker.com).

## Containers for developers

Developers can create a Docker image that will deploy identically across all environments in seconds. There's a massive and growing ecosystem of applications packaged in Docker containers. DockerHub, a public containerized-application registry maintained by Docker, has published more than 180,000 applications in its public community repository, and that number is still growing.

When you containerize an app, only the app and the components needed to run the app are combined into an image. Containers are then created from this image as you need them. You can also use an image as a baseline to create another image, making image creation even faster. Multiple containers can share the same image, which means containers start up very quickly and use fewer resources. For example, you can use containers to spin up lightweight and portable app components, also called "microservices," for distributed apps and quickly scale each service separately.

Containers are portable and versatile. They come with everything they need to run your application, and they're compatible with any machine running Windows Server 2016. You can create and test a container locally, then deploy that same container image to your company's private cloud, public cloud, or service provider. The natural agility of containers supports modern app development patterns in large scale, virtualized cloud environments.

With containers, developers can build an app in any language. These apps are completely portable and can run anywhere without code changes on a laptop, desktop, server, private cloud, public cloud, and service provider.  

Containers help developers build and ship higher-quality applications faster.

## Containers for IT professionals

IT professionals can use containers to provide standardized environments for their development, QA, and production teams. They no longer have to worry about complex installation and configuration procedures. By using containers, systems administrators abstract away differences in OS installations and underlying infrastructure.

Containers help admins create infrastructure that's easier to update and maintain.

## Container orchestrators

Because of their small size and application orientation, containers are perfect for agile delivery environments and microservice-based architectures. However, an environment that uses containers and microservers can have hundreds or thousands of components to keep track of. You might be able to manually manage a few dozen virtual machines or physical servers, but there's no way to properly manage a production-scale container environment without automation. This task should fall to your orchestrator, a process that automate and manages a large number of containers and how they interact.

Orchestrators perform the following tasks:

- Scheduling: When given a container image and a resource request, the orchestrator finds a suitable machine on which to run the container.
- Affinity/Anti-affinity: Specify whether a set of containers should run near each other for performance or far apart for availability.
- Health monitoring: Watch for container failures and automatically reschedule them.
- Failover: Keep track of what's running on each machine and reschedule containers from failed machines to healthy nodes.
- Scaling: Add or remove container instances to match demand, manually or automatically.
- Networking: Provide an overlay network that coordinates containers to communicate across multiple host machines.
- Service discovery: Enable containers to locate each other automatically even as they move between host machines and change IP addresses.
- Coordinated application upgrades: Manage container upgrades to avoid application down time and enable rollback if something goes wrong.

Azure offers two container orchestrators: Azure Kubernetes Service (AKS) and Service Fabric.

[Azure Kubernetes Service (AKS)](/azure/aks/) makes it simple to create, configure, and manage a cluster of virtual machines preconfigured to run containerized applications. This enables you to use your existing skills and draw upon a large and growing body of community expertise to deploy and manage container-based applications on Microsoft Azure. By using AKS, you can take advantage of the enterprise-grade features of Azure while still maintaining application portability through Kubernetes and the Docker image format.

[Azure Service Fabric](/azure/service-fabric/) is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers. Service Fabric addresses the significant challenges in developing and managing cloud native applications. Developers and administrators can avoid complex infrastructure problems and focus on implementing mission-critical, demanding workloads that are scalable, reliable, and manageable. Service Fabric represents the next-generation platform for building and managing these enterprise-class, tier-1, cloud-scale applications running in containers.

## Video overview

<iframe src="https://channel9.msdn.com/Blogs/containers/Containers-101-with-Microsoft-and-Docker/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no"></iframe>

## Try Windows Server containers

Ready to begin leveraging the awesome power of containers? Use these resources to get started :

To set up a container on Windows Server, see the [Windows Server quickstart](../quick-start/quick-start-windows-server.md)

To set up a container on Windows 10, see the [Windows 10 quickstart](../quick-start/quick-start-windows-10.md)

