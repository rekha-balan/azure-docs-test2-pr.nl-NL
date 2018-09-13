---
title: Linux and Open-Source Computing on Azure | Microsoft Docs
description: Lists Linux and Open-Source Computing articles on Azure, including basic Linux usage, some fundamental concepts about running or uploading Linux images on Azure, and other content about specific technologies and optimizations.
services: virtual-machines-linux
documentationcenter: ''
author: squillace
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: a7e608b5-26ea-41e0-b46b-1a483a257754
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/27/2016
ms.author: rasquill
ms.openlocfilehash: d19fa547a8ee34507f64418bac30bfb472b52aef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554799"
---
# <a name="linux-and-open-source-computing-on-azure"></a><span data-ttu-id="4a139-103">Linux and open-source computing on Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-103">Linux and open-source computing on Azure</span></span>
<span data-ttu-id="4a139-104">Find all the documentation you need to create and manage Linux-based virtual machines in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="4a139-104">Find all the documentation you need to create and manage Linux-based virtual machines in the classic deployment model.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4a139-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4a139-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4a139-106">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="4a139-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4a139-107">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="4a139-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="get-started"></a><span data-ttu-id="4a139-108">Get Started</span><span class="sxs-lookup"><span data-stu-id="4a139-108">Get Started</span></span>
* [<span data-ttu-id="4a139-109">Introduction for Linux on Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-109">Introduction for Linux on Azure</span></span>](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4a139-110">Frequently asked question about Azure Virtual Machines created with the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="4a139-110">Frequently asked question about Azure Virtual Machines created with the classic deployment model</span></span>](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-111">About images for virtual machines</span><span class="sxs-lookup"><span data-stu-id="4a139-111">About images for virtual machines</span></span>](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* <span data-ttu-id="4a139-112">[Uploading your own Distro Image](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (and also instructions using an [Azure-Endorsed Distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))</span><span class="sxs-lookup"><span data-stu-id="4a139-112">[Uploading your own Distro Image](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (and also instructions using an [Azure-Endorsed Distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))</span></span>
* [<span data-ttu-id="4a139-113">Log on to a Linux VM Using the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="4a139-113">Log on to a Linux VM Using the Azure classic portal</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a><span data-ttu-id="4a139-114">Set up</span><span class="sxs-lookup"><span data-stu-id="4a139-114">Set up</span></span>
* [<span data-ttu-id="4a139-115">Install Azure Command-Line Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="4a139-115">Install Azure Command-Line Interface (Azure CLI)</span></span>](../../cli-install-nodejs.md)

## <a name="tutorials"></a><span data-ttu-id="4a139-116">Tutorials</span><span class="sxs-lookup"><span data-stu-id="4a139-116">Tutorials</span></span>
* [<span data-ttu-id="4a139-117">Install the LAMP Stack on a Linux virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-117">Install the LAMP Stack on a Linux virtual machine in Azure</span></span>](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4a139-118">Ruby on Rails Web application on an Azure VM</span><span class="sxs-lookup"><span data-stu-id="4a139-118">Ruby on Rails Web application on an Azure VM</span></span>](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [<span data-ttu-id="4a139-119">How to: Install Apache Qpid Proton-C for AMQP and Service Bus</span><span class="sxs-lookup"><span data-stu-id="4a139-119">How to: Install Apache Qpid Proton-C for AMQP and Service Bus</span></span>](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a><span data-ttu-id="4a139-120">Databases</span><span class="sxs-lookup"><span data-stu-id="4a139-120">Databases</span></span>
* [<span data-ttu-id="4a139-121">Optimize Performance of MySQL on Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-121">Optimize Performance of MySQL on Azure</span></span>](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-122">MySQL Clusters</span><span class="sxs-lookup"><span data-stu-id="4a139-122">MySQL Clusters</span></span>](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-123">Running Cassandra with Linux on Azure and Accessing it from Node.js</span><span class="sxs-lookup"><span data-stu-id="4a139-123">Running Cassandra with Linux on Azure and Accessing it from Node.js</span></span>](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-124">Create a Multi-Master cluster of MariaDbs</span><span class="sxs-lookup"><span data-stu-id="4a139-124">Create a Multi-Master cluster of MariaDbs</span></span>](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a><span data-ttu-id="4a139-125">HPC</span><span class="sxs-lookup"><span data-stu-id="4a139-125">HPC</span></span>
* [<span data-ttu-id="4a139-126">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-126">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-127">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-127">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-128">Set up a Linux RDMA cluster to run MPI applications</span><span class="sxs-lookup"><span data-stu-id="4a139-128">Set up a Linux RDMA cluster to run MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a><span data-ttu-id="4a139-129">Docker</span><span class="sxs-lookup"><span data-stu-id="4a139-129">Docker</span></span>
* [<span data-ttu-id="4a139-130">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="4a139-130">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span></span>](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-131">Using the Docker VM Extension from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4a139-131">Using the Docker VM Extension from the Azure portal</span></span>](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-132">How to use docker-machine on Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-132">How to use docker-machine on Azure</span></span>](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a><span data-ttu-id="4a139-133">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4a139-133">Ubuntu</span></span>
* [<span data-ttu-id="4a139-134">How to: MySQL Clusters</span><span class="sxs-lookup"><span data-stu-id="4a139-134">How to: MySQL Clusters</span></span>](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-135">How to: Node.js and Cassandra</span><span class="sxs-lookup"><span data-stu-id="4a139-135">How to: Node.js and Cassandra</span></span>](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a><span data-ttu-id="4a139-136">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="4a139-136">OpenSUSE</span></span>
* [<span data-ttu-id="4a139-137">How to: Install and Run MySQL</span><span class="sxs-lookup"><span data-stu-id="4a139-137">How to: Install and Run MySQL</span></span>](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a><span data-ttu-id="4a139-138">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4a139-138">CoreOS</span></span>
* [<span data-ttu-id="4a139-139">How to: Use CoreOS on Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-139">How to: Use CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a><span data-ttu-id="4a139-140">Planning</span><span class="sxs-lookup"><span data-stu-id="4a139-140">Planning</span></span>
* [<span data-ttu-id="4a139-141">Azure infrastructure services implementation guidelines</span><span class="sxs-lookup"><span data-stu-id="4a139-141">Azure infrastructure services implementation guidelines</span></span>](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4a139-142">Selecting Linux Usernames</span><span class="sxs-lookup"><span data-stu-id="4a139-142">Selecting Linux Usernames</span></span>](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4a139-143">How to configure an availability set for virtual machines in the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="4a139-143">How to configure an availability set for virtual machines in the classic deployment model</span></span>](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-144">How to Schedule Planned Maintenance on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="4a139-144">How to Schedule Planned Maintenance on Azure VMs</span></span>](planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4a139-145">Manage the availability of virtual machines</span><span class="sxs-lookup"><span data-stu-id="4a139-145">Manage the availability of virtual machines</span></span>](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4a139-146">Planned maintenance for Linux virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-146">Planned maintenance for Linux virtual machines in Azure</span></span>](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a><span data-ttu-id="4a139-147">Deployment</span><span class="sxs-lookup"><span data-stu-id="4a139-147">Deployment</span></span>
* [<span data-ttu-id="4a139-148">Create a custom virtual machine running Linux</span><span class="sxs-lookup"><span data-stu-id="4a139-148">Create a custom virtual machine running Linux</span></span>](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-149">The basics: Capturing a Linux VM to Make a Template</span><span class="sxs-lookup"><span data-stu-id="4a139-149">The basics: Capturing a Linux VM to Make a Template</span></span>](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-150">Information for Non-Endorsed Distributions</span><span class="sxs-lookup"><span data-stu-id="4a139-150">Information for Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a><span data-ttu-id="4a139-151">Management</span><span class="sxs-lookup"><span data-stu-id="4a139-151">Management</span></span>
* [<span data-ttu-id="4a139-152">SSH</span><span class="sxs-lookup"><span data-stu-id="4a139-152">SSH</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4a139-153">How to Reset a Password or SSH Properties for Linux</span><span class="sxs-lookup"><span data-stu-id="4a139-153">How to Reset a Password or SSH Properties for Linux</span></span>](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-154">Using Root</span><span class="sxs-lookup"><span data-stu-id="4a139-154">Using Root</span></span>](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a><span data-ttu-id="4a139-155">Azure Resources</span><span class="sxs-lookup"><span data-stu-id="4a139-155">Azure Resources</span></span>
* [<span data-ttu-id="4a139-156">The Azure Linux Agent</span><span class="sxs-lookup"><span data-stu-id="4a139-156">The Azure Linux Agent</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4a139-157">Azure VM Extensions and Features</span><span class="sxs-lookup"><span data-stu-id="4a139-157">Azure VM Extensions and Features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4a139-158">Injecting Custom Data into a VM to use with Cloud-init</span><span class="sxs-lookup"><span data-stu-id="4a139-158">Injecting Custom Data into a VM to use with Cloud-init</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a><span data-ttu-id="4a139-159">Storage</span><span class="sxs-lookup"><span data-stu-id="4a139-159">Storage</span></span>
* [<span data-ttu-id="4a139-160">Attaching a Data Disk to a Linux VM</span><span class="sxs-lookup"><span data-stu-id="4a139-160">Attaching a Data Disk to a Linux VM</span></span>](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-161">Detaching a Data Disk from a Linux VM</span><span class="sxs-lookup"><span data-stu-id="4a139-161">Detaching a Data Disk from a Linux VM</span></span>](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="4a139-162">RAID</span><span class="sxs-lookup"><span data-stu-id="4a139-162">RAID</span></span>](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a><span data-ttu-id="4a139-163">Networking</span><span class="sxs-lookup"><span data-stu-id="4a139-163">Networking</span></span>
* [<span data-ttu-id="4a139-164">How to set up endpoints on a classic virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-164">How to set up endpoints on a classic virtual machine in Azure</span></span>](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a><span data-ttu-id="4a139-165">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="4a139-165">Troubleshooting</span></span>
* [<span data-ttu-id="4a139-166">Troubleshoot Secure Shell (SSH) connections to a Linux-based Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="4a139-166">Troubleshoot Secure Shell (SSH) connections to a Linux-based Azure virtual machine</span></span>](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4a139-167">Troubleshoot classic deployment issues with creating a new Linux virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-167">Troubleshoot classic deployment issues with creating a new Linux virtual machine in Azure</span></span>](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [<span data-ttu-id="4a139-168">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-168">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a><span data-ttu-id="4a139-169">Reference</span><span class="sxs-lookup"><span data-stu-id="4a139-169">Reference</span></span>
* [<span data-ttu-id="4a139-170">Azure CLI commands in Azure Service Management (asm) mode</span><span class="sxs-lookup"><span data-stu-id="4a139-170">Azure CLI commands in Azure Service Management (asm) mode</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="4a139-171">Azure Service Management REST API</span><span class="sxs-lookup"><span data-stu-id="4a139-171">Azure Service Management REST API</span></span>](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a><span data-ttu-id="4a139-172">General Links</span><span class="sxs-lookup"><span data-stu-id="4a139-172">General Links</span></span>
<span data-ttu-id="4a139-173">The following links are for Microsoft blogs, Technet pages, and external sites rather than Azure.com documentation as above.</span><span class="sxs-lookup"><span data-stu-id="4a139-173">The following links are for Microsoft blogs, Technet pages, and external sites rather than Azure.com documentation as above.</span></span> <span data-ttu-id="4a139-174">As both Azure and the open-source computing world are fast-moving targets, it is almost certain that the following links are out of date, *despite* the fact that we shall do our best to continually add newer topics and remove out-of-date ones.</span><span class="sxs-lookup"><span data-stu-id="4a139-174">As both Azure and the open-source computing world are fast-moving targets, it is almost certain that the following links are out of date, *despite* the fact that we shall do our best to continually add newer topics and remove out-of-date ones.</span></span> <span data-ttu-id="4a139-175">If we've missed one, please let us know in the comments, or submit a pull request to our [GitHub repo](https://github.com/Azure/azure-content/).</span><span class="sxs-lookup"><span data-stu-id="4a139-175">If we've missed one, please let us know in the comments, or submit a pull request to our [GitHub repo](https://github.com/Azure/azure-content/).</span></span>

* [<span data-ttu-id="4a139-176">Running ASP.NET 5 on Linux using Docker Containers</span><span class="sxs-lookup"><span data-stu-id="4a139-176">Running ASP.NET 5 on Linux using Docker Containers</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [<span data-ttu-id="4a139-177">How to Deploy a CentOS VM Image from OpenLogic</span><span class="sxs-lookup"><span data-stu-id="4a139-177">How to Deploy a CentOS VM Image from OpenLogic</span></span>](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [<span data-ttu-id="4a139-178">SUSE Update Infrastructure</span><span class="sxs-lookup"><span data-stu-id="4a139-178">SUSE Update Infrastructure</span></span>](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [<span data-ttu-id="4a139-179">SUSE Linux Enterprise Server for SAP Cloud Appliance  Library</span><span class="sxs-lookup"><span data-stu-id="4a139-179">SUSE Linux Enterprise Server for SAP Cloud Appliance  Library</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [<span data-ttu-id="4a139-180">Building Highly Available Linux on Azure in 12 Steps</span><span class="sxs-lookup"><span data-stu-id="4a139-180">Building Highly Available Linux on Azure in 12 Steps</span></span>](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [<span data-ttu-id="4a139-181">Automate Provisioning Linux on Azure with Azure CLI, node.js, jhawk</span><span class="sxs-lookup"><span data-stu-id="4a139-181">Automate Provisioning Linux on Azure with Azure CLI, node.js, jhawk</span></span>](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [<span data-ttu-id="4a139-182">GlusterFS on Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-182">GlusterFS on Azure</span></span>](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a><span data-ttu-id="4a139-183">FreeBSD</span><span class="sxs-lookup"><span data-stu-id="4a139-183">FreeBSD</span></span>
* [<span data-ttu-id="4a139-184">Running FreeBSD in Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-184">Running FreeBSD in Azure</span></span>](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [<span data-ttu-id="4a139-185">Easy Deploy FreeBSD</span><span class="sxs-lookup"><span data-stu-id="4a139-185">Easy Deploy FreeBSD</span></span>](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [<span data-ttu-id="4a139-186">Deploying a Customized FreeBSD Image</span><span class="sxs-lookup"><span data-stu-id="4a139-186">Deploying a Customized FreeBSD Image</span></span>](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [<span data-ttu-id="4a139-187">Kaspersky AV for Linux File Server</span><span class="sxs-lookup"><span data-stu-id="4a139-187">Kaspersky AV for Linux File Server</span></span>](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a><span data-ttu-id="4a139-188">NoSQL</span><span class="sxs-lookup"><span data-stu-id="4a139-188">NoSQL</span></span>
* [<span data-ttu-id="4a139-189">8 Open-source NoSql Databases for Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-189">8 Open-source NoSql Databases for Azure</span></span>](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [<span data-ttu-id="4a139-190">Slideshare (MSOpenTech): Experiences with CouchDb on Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-190">Slideshare (MSOpenTech): Experiences with CouchDb on Azure</span></span>](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [<span data-ttu-id="4a139-191">Running CouchDB-as-a-Service with node.js, CORS, and Grunt</span><span class="sxs-lookup"><span data-stu-id="4a139-191">Running CouchDB-as-a-Service with node.js, CORS, and Grunt</span></span>](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [<span data-ttu-id="4a139-192">Redis on Windows in the Azure Redis Cache Service</span><span class="sxs-lookup"><span data-stu-id="4a139-192">Redis on Windows in the Azure Redis Cache Service</span></span>](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [<span data-ttu-id="4a139-193">Announcing ASP.NET Session State Provider for Redis Preview Release</span><span class="sxs-lookup"><span data-stu-id="4a139-193">Announcing ASP.NET Session State Provider for Redis Preview Release</span></span>](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [<span data-ttu-id="4a139-194">Blog: RavenHQ Now Available in the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4a139-194">Blog: RavenHQ Now Available in the Azure Marketplace</span></span>](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a><span data-ttu-id="4a139-195">Big Data</span><span class="sxs-lookup"><span data-stu-id="4a139-195">Big Data</span></span>
* [<span data-ttu-id="4a139-196">Installing Hadoop on Azure Linux VMs</span><span class="sxs-lookup"><span data-stu-id="4a139-196">Installing Hadoop on Azure Linux VMs</span></span>](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [<span data-ttu-id="4a139-197">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4a139-197">Azure HDInsight</span></span>](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a><span data-ttu-id="4a139-198">Relational database</span><span class="sxs-lookup"><span data-stu-id="4a139-198">Relational database</span></span>
* [<span data-ttu-id="4a139-199">MySQL High Availability Architecture in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-199">MySQL High Availability Architecture in Microsoft Azure</span></span>](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [<span data-ttu-id="4a139-200">Installing Postgres with corosync, pg_bouncer using ILB</span><span class="sxs-lookup"><span data-stu-id="4a139-200">Installing Postgres with corosync, pg_bouncer using ILB</span></span>](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a><span data-ttu-id="4a139-201">Linux high performance computing (HPC)</span><span class="sxs-lookup"><span data-stu-id="4a139-201">Linux high performance computing (HPC)</span></span>
* <span data-ttu-id="4a139-202">[Quickstart template: Spin up a SLURM cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))</span><span class="sxs-lookup"><span data-stu-id="4a139-202">[Quickstart template: Spin up a SLURM cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))</span></span>
* [<span data-ttu-id="4a139-203">Quickstart template: Create an HPC cluster with Linux compute nodes</span><span class="sxs-lookup"><span data-stu-id="4a139-203">Quickstart template: Create an HPC cluster with Linux compute nodes</span></span>](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a><span data-ttu-id="4a139-204">Devops, management, and optimization</span><span class="sxs-lookup"><span data-stu-id="4a139-204">Devops, management, and optimization</span></span>
<span data-ttu-id="4a139-205">As the world of devops, management, and optimization is quite expansive and changing very quickly, you should consider the list below a starting point.</span><span class="sxs-lookup"><span data-stu-id="4a139-205">As the world of devops, management, and optimization is quite expansive and changing very quickly, you should consider the list below a starting point.</span></span>

* [<span data-ttu-id="4a139-206">Video: Azure Virtual Machines : Using Chef, Puppet and Docker for managing Linux VMs</span><span class="sxs-lookup"><span data-stu-id="4a139-206">Video: Azure Virtual Machines : Using Chef, Puppet and Docker for managing Linux VMs</span></span>](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [<span data-ttu-id="4a139-207">Complete guide to automated Kubernetes cluster deployment with CoreOS and Weave</span><span class="sxs-lookup"><span data-stu-id="4a139-207">Complete guide to automated Kubernetes cluster deployment with CoreOS and Weave</span></span>](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [<span data-ttu-id="4a139-208">Kubernetes Visualizer</span><span class="sxs-lookup"><span data-stu-id="4a139-208">Kubernetes Visualizer</span></span>](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [<span data-ttu-id="4a139-209">Jenkins Slave Plug-in for Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-209">Jenkins Slave Plug-in for Azure</span></span>](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [<span data-ttu-id="4a139-210">GitHub repo: Jenkins Storage Plug-in for Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-210">GitHub repo: Jenkins Storage Plug-in for Azure</span></span>](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [<span data-ttu-id="4a139-211">Third Party: Hudson Slave Plug-in for Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-211">Third Party: Hudson Slave Plug-in for Azure</span></span>](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [<span data-ttu-id="4a139-212">Third Party: Hudson Storage Plug-in for Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-212">Third Party: Hudson Storage Plug-in for Azure</span></span>](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [<span data-ttu-id="4a139-213">Video: What is Chef and How does it Work?</span><span class="sxs-lookup"><span data-stu-id="4a139-213">Video: What is Chef and How does it Work?</span></span>](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [<span data-ttu-id="4a139-214">Video: How to Use Azure Automation with Linux VMs</span><span class="sxs-lookup"><span data-stu-id="4a139-214">Video: How to Use Azure Automation with Linux VMs</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [<span data-ttu-id="4a139-215">Blog: How to do Powershell DSC for Linux</span><span class="sxs-lookup"><span data-stu-id="4a139-215">Blog: How to do Powershell DSC for Linux</span></span>](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [<span data-ttu-id="4a139-216">GitHub: Docker Client DSC</span><span class="sxs-lookup"><span data-stu-id="4a139-216">GitHub: Docker Client DSC</span></span>](https://github.com/anweiss/DockerClientDSC)
* [<span data-ttu-id="4a139-217">Packer plugin for Azure</span><span class="sxs-lookup"><span data-stu-id="4a139-217">Packer plugin for Azure</span></span>](https://github.com/msopentech/packer-azure)

