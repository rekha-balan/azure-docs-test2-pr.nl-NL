---
title: Using Docker VM Extension for Linux | Microsoft Docs
description: Describes Docker and the Azure Virtual Machines extensions, and how to create Azure Virtual Machines that are docker hosts using the Azure CLI in classic deployment model.
services: virtual-machines-linux
documentationcenter: ''
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: cdaae550485f1e7f9aa71ba019f6968c0b9122a8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661001"
---
# <a name="using-the-docker-vm-extension-with-the-azure-classic-portal"></a><span data-ttu-id="b809f-103">Using the Docker VM Extension with the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="b809f-103">Using the Docker VM Extension with the Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="b809f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b809f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b809f-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="b809f-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b809f-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="b809f-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="b809f-107">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span><span class="sxs-lookup"><span data-stu-id="b809f-107">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="b809f-108">You can use the Docker VM extension managed by [Azure Linux Agent] to create a Docker VM that hosts any number of containers for your applications on Azure.</span><span class="sxs-lookup"><span data-stu-id="b809f-108">You can use the Docker VM extension managed by [Azure Linux Agent] to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="b809f-109">This topic describes how to create a Docker VM from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="b809f-109">This topic describes how to create a Docker VM from the Azure classic portal.</span></span> <span data-ttu-id="b809f-110">To see how to create a Docker VM at the command line, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)].</span><span class="sxs-lookup"><span data-stu-id="b809f-110">To see how to create a Docker VM at the command line, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="b809f-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="b809f-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-the-image-gallery"></a><span data-ttu-id="b809f-112">Create a new VM from the Image Gallery</span><span class="sxs-lookup"><span data-stu-id="b809f-112">Create a new VM from the Image Gallery</span></span>
<span data-ttu-id="b809f-113">The first step requires an Azure VM from a Linux image that supports the Docker VM Extension, using an Ubuntu 14.04 LTS image from the Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span><span class="sxs-lookup"><span data-stu-id="b809f-113">The first step requires an Azure VM from a Linux image that supports the Docker VM Extension, using an Ubuntu 14.04 LTS image from the Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="b809f-114">In the portal, click **+ New** in the bottom left corner to create a new VM instance and select an Ubuntu 14.04 LTS image from the selections available or from the complete Image Gallery, as shown below.</span><span class="sxs-lookup"><span data-stu-id="b809f-114">In the portal, click **+ New** in the bottom left corner to create a new VM instance and select an Ubuntu 14.04 LTS image from the selections available or from the complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="b809f-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support the Docker VM Extension.</span><span class="sxs-lookup"><span data-stu-id="b809f-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support the Docker VM Extension.</span></span>
> 
> 

![Create a new Ubuntu Image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/portal-use-docker/chooseubuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="b809f-117">Create Docker Certificates</span><span class="sxs-lookup"><span data-stu-id="b809f-117">Create Docker Certificates</span></span>
<span data-ttu-id="b809f-118">After the VM has been created, ensure that Docker is installed on your client computer.</span><span class="sxs-lookup"><span data-stu-id="b809f-118">After the VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="b809f-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span><span class="sxs-lookup"><span data-stu-id="b809f-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="b809f-120">Create the certificate and key files for Docker communication according to [Running Docker with https] and place them in the **`~/.docker`** directory on your client computer.</span><span class="sxs-lookup"><span data-stu-id="b809f-120">Create the certificate and key files for Docker communication according to [Running Docker with https] and place them in the **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="b809f-121">The Docker VM Extension in the portal currently requires credentials that are base64 encoded.</span><span class="sxs-lookup"><span data-stu-id="b809f-121">The Docker VM Extension in the portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="b809f-122">At the command line, use **`base64`** or another favorite encoding tool to create base64-encoded topics.</span><span class="sxs-lookup"><span data-stu-id="b809f-122">At the command line, use **`base64`** or another favorite encoding tool to create base64-encoded topics.</span></span> <span data-ttu-id="b809f-123">Doing this with a simple set of certificate and key files might look similar to this:</span><span class="sxs-lookup"><span data-stu-id="b809f-123">Doing this with a simple set of certificate and key files might look similar to this:</span></span>

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-the-docker-vm-extension"></a><span data-ttu-id="b809f-124">Add the Docker VM Extension</span><span class="sxs-lookup"><span data-stu-id="b809f-124">Add the Docker VM Extension</span></span>
<span data-ttu-id="b809f-125">To add the Docker VM Extension, locate the VM instance you created and scroll down to **Extensions** and click it to bring up VM Extensions, as shown below.</span><span class="sxs-lookup"><span data-stu-id="b809f-125">To add the Docker VM Extension, locate the VM instance you created and scroll down to **Extensions** and click it to bring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="b809f-126">This functionality is supported in the preview portal only: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="b809f-126">This functionality is supported in the preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="b809f-127">Add an Extension</span><span class="sxs-lookup"><span data-stu-id="b809f-127">Add an Extension</span></span>
<span data-ttu-id="b809f-128">Click the **+ Add** to display the possible VM Extensions you can add to this VM.</span><span class="sxs-lookup"><span data-stu-id="b809f-128">Click the **+ Add** to display the possible VM Extensions you can add to this VM.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/portal-use-docker/ClickAdd.png)

### <a name="select-the-docker-vm-extension"></a><span data-ttu-id="b809f-129">Select the Docker VM Extension</span><span class="sxs-lookup"><span data-stu-id="b809f-129">Select the Docker VM Extension</span></span>
<span data-ttu-id="b809f-130">Choose the Docker VM Extension, which brings up the Docker description and important links, and then click **Create** at the bottom to begin the installation procedure.</span><span class="sxs-lookup"><span data-stu-id="b809f-130">Choose the Docker VM Extension, which brings up the Docker description and important links, and then click **Create** at the bottom to begin the installation procedure.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/portal-use-docker/ChooseDockerExtension.png)

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="b809f-131">Add your Certificate and Key Files:</span><span class="sxs-lookup"><span data-stu-id="b809f-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="b809f-132">In the form fields, enter the base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in the following graphic.</span><span class="sxs-lookup"><span data-stu-id="b809f-132">In the form fields, enter the base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in the following graphic.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="b809f-133">Note that (as in the preceding image) the 2376 is filled in by default.</span><span class="sxs-lookup"><span data-stu-id="b809f-133">Note that (as in the preceding image) the 2376 is filled in by default.</span></span> <span data-ttu-id="b809f-134">You can enter any endpoint here, but the next step will be to open up the matching endpoint.</span><span class="sxs-lookup"><span data-stu-id="b809f-134">You can enter any endpoint here, but the next step will be to open up the matching endpoint.</span></span> <span data-ttu-id="b809f-135">If you change the default, make sure to open up the matching endpoint in the next step.</span><span class="sxs-lookup"><span data-stu-id="b809f-135">If you change the default, make sure to open up the matching endpoint in the next step.</span></span>
> 
> 

## <a name="add-the-docker-communication-endpoint"></a><span data-ttu-id="b809f-136">Add the Docker Communication Endpoint</span><span class="sxs-lookup"><span data-stu-id="b809f-136">Add the Docker Communication Endpoint</span></span>
<span data-ttu-id="b809f-137">When viewing the resource group you've created, select the Network Security Group associated with your VM, and click **Inbound Security Rules** to view the rules as shown here.</span><span class="sxs-lookup"><span data-stu-id="b809f-137">When viewing the resource group you've created, select the Network Security Group associated with your VM, and click **Inbound Security Rules** to view the rules as shown here.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="b809f-138">Click **+ Add** to add another rule, and in the default case, enter a name for the endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span><span class="sxs-lookup"><span data-stu-id="b809f-138">Click **+ Add** to add another rule, and in the default case, enter a name for the endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="b809f-139">Set the protocol value showing **TCP**, and Click **OK** to create the rule.</span><span class="sxs-lookup"><span data-stu-id="b809f-139">Set the protocol value showing **TCP**, and Click **OK** to create the rule.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="b809f-140">Test your Docker Client and Azure Docker Host</span><span class="sxs-lookup"><span data-stu-id="b809f-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="b809f-141">Locate and copy the name of your VM's domain, and at the command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by the subdomain for your VM).</span><span class="sxs-lookup"><span data-stu-id="b809f-141">Locate and copy the name of your VM's domain, and at the command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by the subdomain for your VM).</span></span>

<span data-ttu-id="b809f-142">The result should appear similar to this:</span><span class="sxs-lookup"><span data-stu-id="b809f-142">The result should appear similar to this:</span></span>

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

<span data-ttu-id="b809f-143">Once you complete the above steps, you now have a fully functional Docker host running on an Azure VM, configured to be connected to remotely from other clients.</span><span class="sxs-lookup"><span data-stu-id="b809f-143">Once you complete the above steps, you now have a fully functional Docker host running on an Azure VM, configured to be connected to remotely from other clients.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="b809f-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="b809f-144">Next steps</span></span>
<span data-ttu-id="b809f-145">You are ready to go to the [Docker User Guide] and use your Docker VM.</span><span class="sxs-lookup"><span data-stu-id="b809f-145">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="b809f-146">If you want to automate creating Docker hosts on Azure VMs through command line interface, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]</span><span class="sxs-lookup"><span data-stu-id="b809f-146">If you want to automate creating Docker hosts on Azure VMs through command line interface, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from the Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add the Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[Azure Linux Agent]:../agent-user-guide.md
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md

[Running Docker with https]:http://docs.docker.com/articles/https/
[Docker User Guide]:https://docs.docker.com/userguide/








