---
title: Known Issues
description: Known Issues for Windows Server containers
keywords: metadata, containers, version,
author: weijuans
ms. author: weijuans
manager: taylob
ms.date: 05/26/2020
---
# Known Issues

## Know Issues of Windows Server, version 2004

### 1. Performance Issue on Server Core container
In prepping for general availability of Windows Server, version 2004 release, we identified a potential performance issue with .NET Team on the current Server Core container image in the May 27, 2020 release, comparing to the performance improvements we blogged in Dec 2019 [here](https://techcommunity.microsoft.com/t5/containers/making-windows-server-core-containers-40-smaller/ba-p/1058874) and on .NET Team blog [here](https://devblogs.microsoft.com/dotnet/we-made-windows-server-core-container-images-40-smaller/). The performance analysis back then was done on a Windows Server, version 2004 Insider Preview Release Server Core container image. 

The symptoms that we observed are:

If you use the Server Core container image to build your own image and upload to a remote container registry such as Azure Container Registry, and then you pull that image from the registry and run it, you will see a slower performance of the container. However, if you build the image and run the image locally, you will not observe that performance difference.

This issue is now root caused and we are working on the fix. You can find the following links that track the issue:
[microsoft/hcsshim#830](https://github.com/microsoft/hcsshim/issues/830)
[moby/moby#41066](https://github.com/moby/moby/issues/41066)
[containerd/containerd#4301](https://github.com/containerd/containerd/issues/4301)

We are also actively with our partner Mirantis getting that fix in Docker EE.

## Know Issues of Windows Server, version 1909

## Know Issues of Windows Server, version 1903

## Know Issues of Windows Server 2019/Windows Server, version 1809

## Know Issues of Windows Server 2016
