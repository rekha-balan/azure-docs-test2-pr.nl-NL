---
title: Execute commands in running containers in Azure Container Instances
description: Learn how execute a command in a container that's currently running in Azure Container Instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 03/30/2018
ms.author: marsma
ms.openlocfilehash: 43211f620efb16cbcd722d3d386b1bb862fc6280
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866539"
---
# <a name="execute-a-command-in-a-running-azure-container-instance"></a><span data-ttu-id="83408-103">Execute a command in a running Azure container instance</span><span class="sxs-lookup"><span data-stu-id="83408-103">Execute a command in a running Azure container instance</span></span>

<span data-ttu-id="83408-104">Azure Container Instances supports executing a command in a running container.</span><span class="sxs-lookup"><span data-stu-id="83408-104">Azure Container Instances supports executing a command in a running container.</span></span> <span data-ttu-id="83408-105">Running a command in a container you've already started is especially helpful during application development and troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="83408-105">Running a command in a container you've already started is especially helpful during application development and troubleshooting.</span></span> <span data-ttu-id="83408-106">The most common use of this feature is to launch an interactive shell so that you can debug issues in a running container.</span><span class="sxs-lookup"><span data-stu-id="83408-106">The most common use of this feature is to launch an interactive shell so that you can debug issues in a running container.</span></span>

## <a name="run-a-command-with-azure-cli"></a><span data-ttu-id="83408-107">Run a command with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="83408-107">Run a command with Azure CLI</span></span>

<span data-ttu-id="83408-108">Execute a command in a running container with [az container exec][az-container-exec] in the [Azure CLI][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="83408-108">Execute a command in a running container with [az container exec][az-container-exec] in the [Azure CLI][azure-cli]:</span></span>

```azurecli
az container exec --resource-group <group-name> --name <container-group-name> --exec-command "<command>"
```

<span data-ttu-id="83408-109">For example, to launch a Bash shell in an Nginx container:</span><span class="sxs-lookup"><span data-stu-id="83408-109">For example, to launch a Bash shell in an Nginx container:</span></span>

```azurecli
az container exec --resource-group myResourceGroup --name mynginx --exec-command "/bin/bash"
```

<span data-ttu-id="83408-110">In the example output below, the Bash shell is launched in a running Linux container, providing a terminal in which `ls` is executed:</span><span class="sxs-lookup"><span data-stu-id="83408-110">In the example output below, the Bash shell is launched in a running Linux container, providing a terminal in which `ls` is executed:</span></span>

```console
$ az container exec --resource-group myResourceGroup --name mynginx --exec-command "/bin/bash"
root@caas-83e6c883014b427f9b277a2bba3b7b5f-708716530-2qv47:/# ls
bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
boot  etc  lib   media  opt  root  sbin  sys  usr
root@caas-83e6c883014b427f9b277a2bba3b7b5f-708716530-2qv47:/# exit
exit
Bye.
```

<span data-ttu-id="83408-111">In this example, Command Prompt is launched in a running Nanoserver container:</span><span class="sxs-lookup"><span data-stu-id="83408-111">In this example, Command Prompt is launched in a running Nanoserver container:</span></span>

```console
$ az container exec --resource-group myResourceGroup --name myiis --exec-command "cmd.exe"
Microsoft Windows [Version 10.0.14393]
(c) 2016 Microsoft Corporation. All rights reserved.

C:\>dir
 Volume in drive C has no label.
 Volume Serial Number is 76E0-C852

 Directory of C:\

03/23/2018  09:13 PM    <DIR>          inetpub
11/20/2016  11:32 AM             1,894 License.txt
03/23/2018  09:13 PM    <DIR>          Program Files
07/16/2016  12:09 PM    <DIR>          Program Files (x86)
03/13/2018  08:50 PM           171,616 ServiceMonitor.exe
03/23/2018  09:13 PM    <DIR>          Users
03/23/2018  09:12 PM    <DIR>          var
03/23/2018  09:22 PM    <DIR>          Windows
               2 File(s)        173,510 bytes
               6 Dir(s)  21,171,609,600 bytes free

C:\>exit
Bye.
```

## <a name="multi-container-groups"></a><span data-ttu-id="83408-112">Multi-container groups</span><span class="sxs-lookup"><span data-stu-id="83408-112">Multi-container groups</span></span>

<span data-ttu-id="83408-113">If your [container group](container-instances-container-groups.md) has multiple containers, such as an application container and a logging sidecar, specify the name of the container in which to run the command with `--container-name`.</span><span class="sxs-lookup"><span data-stu-id="83408-113">If your [container group](container-instances-container-groups.md) has multiple containers, such as an application container and a logging sidecar, specify the name of the container in which to run the command with `--container-name`.</span></span>

<span data-ttu-id="83408-114">For example, in the container group *mynginx* are two containers, *nginx-app* and *logger*.</span><span class="sxs-lookup"><span data-stu-id="83408-114">For example, in the container group *mynginx* are two containers, *nginx-app* and *logger*.</span></span> <span data-ttu-id="83408-115">To launch a shell on the *nginx-app* container:</span><span class="sxs-lookup"><span data-stu-id="83408-115">To launch a shell on the *nginx-app* container:</span></span>

```azurecli
az container exec --resource-group myResourceGroup --name mynginx --container-name nginx-app --exec-command "/bin/bash"
```

## <a name="restrictions"></a><span data-ttu-id="83408-116">Restrictions</span><span class="sxs-lookup"><span data-stu-id="83408-116">Restrictions</span></span>

<span data-ttu-id="83408-117">Azure Container Instances currently supports launching a single process with [az container exec][az-container-exec], and you cannot pass command arguments.</span><span class="sxs-lookup"><span data-stu-id="83408-117">Azure Container Instances currently supports launching a single process with [az container exec][az-container-exec], and you cannot pass command arguments.</span></span> <span data-ttu-id="83408-118">For example, you cannot chain commands like in `sh -c "echo FOO && echo BAR"`, or execute `echo FOO`.</span><span class="sxs-lookup"><span data-stu-id="83408-118">For example, you cannot chain commands like in `sh -c "echo FOO && echo BAR"`, or execute `echo FOO`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83408-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="83408-119">Next steps</span></span>

<span data-ttu-id="83408-120">Learn about other troubleshooting tools and common deployment issues in [Troubleshoot container and deployment issues in Azure Container Instances](container-instances-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="83408-120">Learn about other troubleshooting tools and common deployment issues in [Troubleshoot container and deployment issues in Azure Container Instances](container-instances-troubleshooting.md).</span></span>

<!-- LINKS - internal -->
[az-container-create]: /cli/azure/container#az-container-create
[az-container-exec]: /cli/azure/container#az-container-exec
[azure-cli]: /cli/azure