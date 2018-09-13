---
title: Configure a Docker Host with VirtualBox | Microsoft Docs
description: Step-by-step instructions to configure a default Docker instance using Docker Machine and VirtualBox
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: ''
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 238ceaa0bf10c4ebcf99d8b746e8b326a8289a2c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564155"
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="ed783-103">Configure a Docker Host with VirtualBox</span><span class="sxs-lookup"><span data-stu-id="ed783-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="ed783-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ed783-104">Overview</span></span>
<span data-ttu-id="ed783-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="ed783-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="ed783-106">If you’re using the [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span><span class="sxs-lookup"><span data-stu-id="ed783-106">If you’re using the [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed783-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ed783-107">Prerequisites</span></span>
<span data-ttu-id="ed783-108">The following tools need to be installed.</span><span class="sxs-lookup"><span data-stu-id="ed783-108">The following tools need to be installed.</span></span>

* [<span data-ttu-id="ed783-109">Docker Toolbox</span><span class="sxs-lookup"><span data-stu-id="ed783-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-the-docker-client-with-windows-powershell"></a><span data-ttu-id="ed783-110">Configuring the Docker client with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed783-110">Configuring the Docker client with Windows PowerShell</span></span>
<span data-ttu-id="ed783-111">To configure a Docker client, simply open Windows PowerShell, and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ed783-111">To configure a Docker client, simply open Windows PowerShell, and perform the following steps:</span></span>

1. <span data-ttu-id="ed783-112">Create a default docker host instance.</span><span class="sxs-lookup"><span data-stu-id="ed783-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="ed783-113">Verify the default instance is configured and running.</span><span class="sxs-lookup"><span data-stu-id="ed783-113">Verify the default instance is configured and running.</span></span> <span data-ttu-id="ed783-114">(You should see an instance named \`default' running.</span><span class="sxs-lookup"><span data-stu-id="ed783-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![docker-machine ls output][0]
3. <span data-ttu-id="ed783-116">Set default as the current host, and configure your shell.</span><span class="sxs-lookup"><span data-stu-id="ed783-116">Set default as the current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="ed783-117">Display the active Docker containers.</span><span class="sxs-lookup"><span data-stu-id="ed783-117">Display the active Docker containers.</span></span> <span data-ttu-id="ed783-118">The list should be empty.</span><span class="sxs-lookup"><span data-stu-id="ed783-118">The list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![docker ps output][1]

> [!NOTE]
> <span data-ttu-id="ed783-120">Each time you reboot your development machine, you’ll need to restart your local docker host.</span><span class="sxs-lookup"><span data-stu-id="ed783-120">Each time you reboot your development machine, you’ll need to restart your local docker host.</span></span>
> <span data-ttu-id="ed783-121">To do this, issue the following command at a command prompt: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="ed783-121">To do this, issue the following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-docker-setup/docker-ps.png


