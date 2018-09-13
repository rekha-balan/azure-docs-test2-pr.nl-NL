---
title: Using the Docker VM Extension for Linux on Azure
description: Describes Docker and the Azure Virtual Machines extensions, and shows how to programmatically create Virtual Machines on Azure that are docker hosts from the command line using the Azure CLI.
services: virtual-machines-linux
documentationcenter: ''
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: df092cf0c8403d49d69ba876d794f6c2b116006d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549249"
---
# <a name="using-the-docker-vm-extension-from-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="71e8e-103">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="71e8e-103">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="71e8e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="71e8e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="71e8e-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="71e8e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="71e8e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="71e8e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="71e8e-107">For information about using the Docker VM extension with the Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71e8e-107">For information about using the Docker VM extension with the Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="71e8e-108">This topic describes how to create a VM with the Docker VM Extension from the service management (asm) mode in Azure CLI on any platform.</span><span class="sxs-lookup"><span data-stu-id="71e8e-108">This topic describes how to create a VM with the Docker VM Extension from the service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="71e8e-109">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span><span class="sxs-lookup"><span data-stu-id="71e8e-109">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="71e8e-110">You can use the Docker VM extension and the [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create a Docker VM that hosts any number of containers for your applications on Azure.</span><span class="sxs-lookup"><span data-stu-id="71e8e-110">You can use the Docker VM extension and the [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="71e8e-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="71e8e-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-to-use-the-docker-vm-extension-with-azure"></a><span data-ttu-id="71e8e-112">How to use the Docker VM Extension with Azure</span><span class="sxs-lookup"><span data-stu-id="71e8e-112">How to use the Docker VM Extension with Azure</span></span>
<span data-ttu-id="71e8e-113">To use the Docker VM extension with Azure, you must install a version of the [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing the current version is 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="71e8e-113">To use the Docker VM extension with Azure, you must install a version of the [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing the current version is 0.10.0).</span></span> <span data-ttu-id="71e8e-114">You can install the Azure CLI on Mac, Linux, and Windows.</span><span class="sxs-lookup"><span data-stu-id="71e8e-114">You can install the Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="71e8e-115">The complete process to use Docker on Azure is simple:</span><span class="sxs-lookup"><span data-stu-id="71e8e-115">The complete process to use Docker on Azure is simple:</span></span>

* <span data-ttu-id="71e8e-116">Install the Azure CLI and its dependencies on the computer from which you want to control Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span><span class="sxs-lookup"><span data-stu-id="71e8e-116">Install the Azure CLI and its dependencies on the computer from which you want to control Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="71e8e-117">Use the Azure CLI Docker commands to create a VM Docker host in Azure</span><span class="sxs-lookup"><span data-stu-id="71e8e-117">Use the Azure CLI Docker commands to create a VM Docker host in Azure</span></span>
* <span data-ttu-id="71e8e-118">Use the local Docker commands to manage your Docker containers in your Docker VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="71e8e-118">Use the local Docker commands to manage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="71e8e-119">Install the Azure Command-Line Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="71e8e-119">Install the Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="71e8e-120">To install and configure the Azure CLI, see [How to install the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="71e8e-120">To install and configure the Azure CLI, see [How to install the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="71e8e-121">To confirm the installation, type `azure` at the command prompt and after a short moment you should see the Azure CLI ASCII art, which lists the basic commands available to you.</span><span class="sxs-lookup"><span data-stu-id="71e8e-121">To confirm the installation, type `azure` at the command prompt and after a short moment you should see the Azure CLI ASCII art, which lists the basic commands available to you.</span></span> <span data-ttu-id="71e8e-122">If the installation worked correctly, you should be able to type `azure help vm` and see that one of the listed commands is "docker".</span><span class="sxs-lookup"><span data-stu-id="71e8e-122">If the installation worked correctly, you should be able to type `azure help vm` and see that one of the listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="71e8e-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use to automate the creation of a docker client that you can use to work with Azure VMs as docker hosts.</span><span class="sxs-lookup"><span data-stu-id="71e8e-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use to automate the creation of a docker client that you can use to work with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-the-azure-cli-to-to-your-azure-account"></a><span data-ttu-id="71e8e-124">Connect the Azure CLI to to your Azure Account</span><span class="sxs-lookup"><span data-stu-id="71e8e-124">Connect the Azure CLI to to your Azure Account</span></span>
<span data-ttu-id="71e8e-125">Before you can use the Azure CLI you must associate your Azure account credentials with the Azure CLI on your platform.</span><span class="sxs-lookup"><span data-stu-id="71e8e-125">Before you can use the Azure CLI you must associate your Azure account credentials with the Azure CLI on your platform.</span></span> <span data-ttu-id="71e8e-126">The section [How to connect to your Azure subscription](../../../xplat-cli-connect.md) explains how to either download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span><span class="sxs-lookup"><span data-stu-id="71e8e-126">The section [How to connect to your Azure subscription](../../../xplat-cli-connect.md) explains how to either download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="71e8e-127">There are some differences in behavior when using one or the other methods of authentication, so do be sure to read the document above to understand the different functionality.</span><span class="sxs-lookup"><span data-stu-id="71e8e-127">There are some differences in behavior when using one or the other methods of authentication, so do be sure to read the document above to understand the different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-the-docker-vm-extension-for-azure"></a><span data-ttu-id="71e8e-128">Install Docker and use the Docker VM Extension for Azure</span><span class="sxs-lookup"><span data-stu-id="71e8e-128">Install Docker and use the Docker VM Extension for Azure</span></span>
<span data-ttu-id="71e8e-129">Follow the [Docker installation instructions](https://docs.docker.com/installation/#installation) to install Docker locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="71e8e-129">Follow the [Docker installation instructions](https://docs.docker.com/installation/#installation) to install Docker locally on your computer.</span></span>

<span data-ttu-id="71e8e-130">To use Docker with an Azure Virtual Machine, the Linux image used for the VM must have the [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span><span class="sxs-lookup"><span data-stu-id="71e8e-130">To use Docker with an Azure Virtual Machine, the Linux image used for the VM must have the [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="71e8e-131">Currently, there are only two types of images that provide this:</span><span class="sxs-lookup"><span data-stu-id="71e8e-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="71e8e-132">An Ubuntu image from the Azure Image Gallery or</span><span class="sxs-lookup"><span data-stu-id="71e8e-132">An Ubuntu image from the Azure Image Gallery or</span></span>
* <span data-ttu-id="71e8e-133">A custom Linux image that you have created with the Azure Linux VM Agent installed and configured.</span><span class="sxs-lookup"><span data-stu-id="71e8e-133">A custom Linux image that you have created with the Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="71e8e-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how to build a custom Linux VM with the Azure VM Agent.</span><span class="sxs-lookup"><span data-stu-id="71e8e-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how to build a custom Linux VM with the Azure VM Agent.</span></span>

### <a name="using-the-azure-image-gallery"></a><span data-ttu-id="71e8e-135">Using the Azure Image Gallery</span><span class="sxs-lookup"><span data-stu-id="71e8e-135">Using the Azure Image Gallery</span></span>
<span data-ttu-id="71e8e-136">From a Bash or Terminal session, use the following Azure CLI command to locate the most recent Ubuntu image in the VM gallery to use by typing</span><span class="sxs-lookup"><span data-stu-id="71e8e-136">From a Bash or Terminal session, use the following Azure CLI command to locate the most recent Ubuntu image in the VM gallery to use by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="71e8e-137">and select one of the image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use the following command to create a new VM using that image.</span><span class="sxs-lookup"><span data-stu-id="71e8e-137">and select one of the image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use the following command to create a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="71e8e-138">where:</span><span class="sxs-lookup"><span data-stu-id="71e8e-138">where:</span></span>

* <span data-ttu-id="71e8e-139">*&lt;vm-cloudservice name&gt;* is the name of the VM that will become the Docker container host computer in Azure</span><span class="sxs-lookup"><span data-stu-id="71e8e-139">*&lt;vm-cloudservice name&gt;* is the name of the VM that will become the Docker container host computer in Azure</span></span>
* <span data-ttu-id="71e8e-140">*&lt;username&gt;* is the username of the default root user of the VM</span><span class="sxs-lookup"><span data-stu-id="71e8e-140">*&lt;username&gt;* is the username of the default root user of the VM</span></span>
* <span data-ttu-id="71e8e-141">*&lt;password&gt;* is the password of the *username* account that meets the standards of complexity for Azure</span><span class="sxs-lookup"><span data-stu-id="71e8e-141">*&lt;password&gt;* is the password of the *username* account that meets the standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="71e8e-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of the following characters: `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="71e8e-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of the following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="71e8e-143">No, the period at the end of the preceding sentence is NOT a special character.</span><span class="sxs-lookup"><span data-stu-id="71e8e-143">No, the period at the end of the preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="71e8e-144">If the command was successful, you should see something like the following, depending on the precise arguments and options you used:</span><span class="sxs-lookup"><span data-stu-id="71e8e-144">If the command was successful, you should see something like the following, depending on the precise arguments and options you used:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="71e8e-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (the state value is `ReadyRole`) the Docker daemon (the Docker service) starts and you can connect to the Docker container host.</span><span class="sxs-lookup"><span data-stu-id="71e8e-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (the state value is `ReadyRole`) the Docker daemon (the Docker service) starts and you can connect to the Docker container host.</span></span>
> 
> 

<span data-ttu-id="71e8e-146">To test the Docker VM you have created in Azure, type</span><span class="sxs-lookup"><span data-stu-id="71e8e-146">To test the Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="71e8e-147">where *&lt;vm-name-you-used&gt;* is the name of the virtual machine that you used in your call to `azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="71e8e-147">where *&lt;vm-name-you-used&gt;* is the name of the virtual machine that you used in your call to `azure vm docker create`.</span></span> <span data-ttu-id="71e8e-148">You should see something similar to the following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span><span class="sxs-lookup"><span data-stu-id="71e8e-148">You should see something similar to the following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="71e8e-149">Now you can try to connect using your docker client to obtain information (in some Docker client setups, such as that on Mac, you may have to use `sudo`):</span><span class="sxs-lookup"><span data-stu-id="71e8e-149">Now you can try to connect using your docker client to obtain information (in some Docker client setups, such as that on Mac, you may have to use `sudo`):</span></span>

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

<span data-ttu-id="71e8e-150">Just to be certain that it's all working, you can examine the VM for the Docker extension:</span><span class="sxs-lookup"><span data-stu-id="71e8e-150">Just to be certain that it's all working, you can examine the VM for the Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="71e8e-151">Docker Host VM Authentication</span><span class="sxs-lookup"><span data-stu-id="71e8e-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="71e8e-152">In addition to creating the Docker VM, the `azure vm docker create` command also automatically creates the necessary certificates to allow your Docker client computer to connect to the Azure container host using HTTPS, and the certificates are stored on both the client and host machines, as appropriate.</span><span class="sxs-lookup"><span data-stu-id="71e8e-152">In addition to creating the Docker VM, the `azure vm docker create` command also automatically creates the necessary certificates to allow your Docker client computer to connect to the Azure container host using HTTPS, and the certificates are stored on both the client and host machines, as appropriate.</span></span> <span data-ttu-id="71e8e-153">On subsequent attempts, the existing certificates are reused and shared with the new host.</span><span class="sxs-lookup"><span data-stu-id="71e8e-153">On subsequent attempts, the existing certificates are reused and shared with the new host.</span></span>

<span data-ttu-id="71e8e-154">By default, certificates are placed in `~/.docker`, and Docker will be configured to run on port **2376**.</span><span class="sxs-lookup"><span data-stu-id="71e8e-154">By default, certificates are placed in `~/.docker`, and Docker will be configured to run on port **2376**.</span></span> <span data-ttu-id="71e8e-155">If you would like to use a different port or directory, then you may use one of the following `azure vm docker create` command line options to configure your Docker container host VM to use a different port or different certificates for connecting clients:</span><span class="sxs-lookup"><span data-stu-id="71e8e-155">If you would like to use a different port or directory, then you may use one of the following `azure vm docker create` command line options to configure your Docker container host VM to use a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port to use for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="71e8e-156">The Docker daemon on the host is configured to listen for and authenticate client connections on the specified port using the certificates generated by the `azure vm docker create` command.</span><span class="sxs-lookup"><span data-stu-id="71e8e-156">The Docker daemon on the host is configured to listen for and authenticate client connections on the specified port using the certificates generated by the `azure vm docker create` command.</span></span> <span data-ttu-id="71e8e-157">The client machine must have these certificates to gain access to the Docker host.</span><span class="sxs-lookup"><span data-stu-id="71e8e-157">The client machine must have these certificates to gain access to the Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="71e8e-158">A networked host running without these certificates will be vulnerable to anyone that can to connect to the machine.</span><span class="sxs-lookup"><span data-stu-id="71e8e-158">A networked host running without these certificates will be vulnerable to anyone that can to connect to the machine.</span></span> <span data-ttu-id="71e8e-159">Before you modify the default configuration, ensure that you understand the risks to your computers and applications.</span><span class="sxs-lookup"><span data-stu-id="71e8e-159">Before you modify the default configuration, ensure that you understand the risks to your computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="71e8e-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="71e8e-160">Next steps</span></span>
* <span data-ttu-id="71e8e-161">You are ready to go to the [Docker User Guide] and use your Docker VM.</span><span class="sxs-lookup"><span data-stu-id="71e8e-161">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="71e8e-162">To create a Docker-enabled VM in the new portal, see [How to use the Docker VM Extension with the Portal].</span><span class="sxs-lookup"><span data-stu-id="71e8e-162">To create a Docker-enabled VM in the new portal, see [How to use the Docker VM Extension with the Portal].</span></span>
* <span data-ttu-id="71e8e-163">The Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file to take a developer-modeled application across any environment and generate a consistent deployment.</span><span class="sxs-lookup"><span data-stu-id="71e8e-163">The Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file to take a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="71e8e-164">See [Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine].</span><span class="sxs-lookup"><span data-stu-id="71e8e-164">See [Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How to use the Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 to another azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 to another azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md
[How to use the Docker VM Extension with the Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Docker User Guide]:https://docs.docker.com/userguide/

[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine]:../docker-compose-quickstart.md

