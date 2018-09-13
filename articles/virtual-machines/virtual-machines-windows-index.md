---
title: Technical articles for classic Windows VMs | Microsoft Azure
description: A complete list of Microsoft Azure documentation articles for Windows virtual machines in the classic deployment model
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
tags: azure-service-management
editor: ''
ms.assetid: 7f9a508b-34ec-4bdb-92d1-8844480369d5
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: danlep
ms.openlocfilehash: b0f97779c2cf8bf3e7535afa8a2ab1ee45958ad1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553035"
---
# <a name="technical-articles-for-windows-vms-in-the-classic-deployment-model"></a><span data-ttu-id="62bf4-103">Technical articles for Windows VMs in the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="62bf4-103">Technical articles for Windows VMs in the classic deployment model</span></span>
<span data-ttu-id="62bf4-104">Find all the documentation you need to create and manage Windows-based Azure virtual machines in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="62bf4-104">Find all the documentation you need to create and manage Windows-based Azure virtual machines in the classic deployment model.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="62bf4-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="62bf4-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="62bf4-106">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="62bf4-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="62bf4-107">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="62bf4-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="overview"></a><span data-ttu-id="62bf4-108">Overview</span><span class="sxs-lookup"><span data-stu-id="62bf4-108">Overview</span></span>
[<span data-ttu-id="62bf4-109">About virtual machines</span><span class="sxs-lookup"><span data-stu-id="62bf4-109">About virtual machines</span></span>](windows/about.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-110">Frequently asked question about Azure Virtual Machines created with the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="62bf4-110">Frequently asked question about Azure Virtual Machines created with the classic deployment model</span></span>](windows/classic/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-111">Compare VMs, websites, and cloud services</span><span class="sxs-lookup"><span data-stu-id="62bf4-111">Compare VMs, websites, and cloud services</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)

[<span data-ttu-id="62bf4-112">Virtual Machines and Containers in Azure</span><span class="sxs-lookup"><span data-stu-id="62bf4-112">Virtual Machines and Containers in Azure</span></span>](windows/containers.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="environment-setup"></a><span data-ttu-id="62bf4-113">Environment setup</span><span class="sxs-lookup"><span data-stu-id="62bf4-113">Environment setup</span></span>
[<span data-ttu-id="62bf4-114">Free account</span><span class="sxs-lookup"><span data-stu-id="62bf4-114">Free account</span></span>](https://azure.microsoft.com/free/)

[<span data-ttu-id="62bf4-115">Install Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="62bf4-115">Install Azure PowerShell</span></span>](/powershell/azureps-cmdlets-docs)

[<span data-ttu-id="62bf4-116">Install Azure CLI</span><span class="sxs-lookup"><span data-stu-id="62bf4-116">Install Azure CLI</span></span>](../cli-install-nodejs.md)

## <a name="get-started"></a><span data-ttu-id="62bf4-117">Get started</span><span class="sxs-lookup"><span data-stu-id="62bf4-117">Get started</span></span>
[<span data-ttu-id="62bf4-118">Learning path for Windows VMs</span><span class="sxs-lookup"><span data-stu-id="62bf4-118">Learning path for Windows VMs</span></span>](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)

[<span data-ttu-id="62bf4-119">Create a Windows virtual machine in the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="62bf4-119">Create a Windows virtual machine in the Azure classic portal</span></span>](windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-120">How to log on to a classic virtual machine running Windows Server</span><span class="sxs-lookup"><span data-stu-id="62bf4-120">How to log on to a classic virtual machine running Windows Server</span></span>](windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="plan"></a><span data-ttu-id="62bf4-121">Plan</span><span class="sxs-lookup"><span data-stu-id="62bf4-121">Plan</span></span>
[<span data-ttu-id="62bf4-122">About images for classic virtual machines</span><span class="sxs-lookup"><span data-stu-id="62bf4-122">About images for classic virtual machines</span></span>](windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-123">Sizes for virtual machines</span><span class="sxs-lookup"><span data-stu-id="62bf4-123">Sizes for virtual machines</span></span>](windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-124">About H-series and compute-intensive A-series VMs</span><span class="sxs-lookup"><span data-stu-id="62bf4-124">About H-series and compute-intensive A-series VMs</span></span>](windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-125">Planned maintenance for Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="62bf4-125">Planned maintenance for Azure virtual machines</span></span>](windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-126">Azure infrastructure services implementation guidelines</span><span class="sxs-lookup"><span data-stu-id="62bf4-126">Azure infrastructure services implementation guidelines</span></span>](windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-127">Create an availability set for virtual machines</span><span class="sxs-lookup"><span data-stu-id="62bf4-127">Create an availability set for virtual machines</span></span>](windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="deploy"></a><span data-ttu-id="62bf4-128">Deploy</span><span class="sxs-lookup"><span data-stu-id="62bf4-128">Deploy</span></span>
[<span data-ttu-id="62bf4-129">Create a custom virtual machine running Windows</span><span class="sxs-lookup"><span data-stu-id="62bf4-129">Create a custom virtual machine running Windows</span></span>](windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-130">Capture a Windows virtual machine created in the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="62bf4-130">Capture a Windows virtual machine created in the classic deployment model</span></span>](windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-131">Create and upload a classic Windows Server VHD using PowerShell</span><span class="sxs-lookup"><span data-stu-id="62bf4-131">Create and upload a classic Windows Server VHD using PowerShell</span></span>](windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-132">Automating Azure virtual machine deployment with Chef</span><span class="sxs-lookup"><span data-stu-id="62bf4-132">Automating Azure virtual machine deployment with Chef</span></span>](windows/chef-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-133">Create and configure a classic Windows Virtual Machine in Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="62bf4-133">Create and configure a classic Windows Virtual Machine in Azure PowerShell</span></span>](windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-134">Injecting custom data into an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="62bf4-134">Injecting custom data into an Azure virtual machine</span></span>](windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="manage"></a><span data-ttu-id="62bf4-135">Manage</span><span class="sxs-lookup"><span data-stu-id="62bf4-135">Manage</span></span>
[<span data-ttu-id="62bf4-136">Manage your virtual machines by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="62bf4-136">Manage your virtual machines by using Azure PowerShell</span></span>](windows/classic/manage-psh.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-137">Connect classic VNets to new VNets</span><span class="sxs-lookup"><span data-stu-id="62bf4-137">Connect classic VNets to new VNets</span></span>](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)

[<span data-ttu-id="62bf4-138">About the virtual machine agent and extensions</span><span class="sxs-lookup"><span data-stu-id="62bf4-138">About the virtual machine agent and extensions</span></span>](windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-139">Manage virtual machine extensions</span><span class="sxs-lookup"><span data-stu-id="62bf4-139">Manage virtual machine extensions</span></span>](windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-140">Custom Script extension for classic Windows virtual machines</span><span class="sxs-lookup"><span data-stu-id="62bf4-140">Custom Script extension for classic Windows virtual machines</span></span>](windows/classic/extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-141">Platform-supported migration from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="62bf4-141">Platform-supported migration from classic to Azure Resource Manager</span></span>](windows/migration-classic-resource-manager-deep-dive.md)

## <a name="configure"></a><span data-ttu-id="62bf4-142">Configure</span><span class="sxs-lookup"><span data-stu-id="62bf4-142">Configure</span></span>
[<span data-ttu-id="62bf4-143">How to reset a password or the Remote Desktop service for a Windows VM</span><span class="sxs-lookup"><span data-stu-id="62bf4-143">How to reset a password or the Remote Desktop service for a Windows VM</span></span>](windows/reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-144">About virtual machine extensions and features</span><span class="sxs-lookup"><span data-stu-id="62bf4-144">About virtual machine extensions and features</span></span>](windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-145">How to install and configure Symantec Endpoint Protection on a Windows VM</span><span class="sxs-lookup"><span data-stu-id="62bf4-145">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>](windows/classic/install-symantec.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-146">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span><span class="sxs-lookup"><span data-stu-id="62bf4-146">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>](windows/classic/install-trend.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-147">How to configure an availability set for virtual machines in the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="62bf4-147">How to configure an availability set for virtual machines in the classic deployment model</span></span>](windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-148">How to set up endpoints on a classic Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="62bf4-148">How to set up endpoints on a classic Azure virtual machine</span></span>](windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a><span data-ttu-id="62bf4-149">Storage</span><span class="sxs-lookup"><span data-stu-id="62bf4-149">Storage</span></span>
[<span data-ttu-id="62bf4-150">About disks and VHDs for Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="62bf4-150">About disks and VHDs for Azure virtual machines</span></span>](../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-151">How to attach a data disk to a classic Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="62bf4-151">How to attach a data disk to a classic Windows virtual machine</span></span>](windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-152">How to detach a data disk from a classic Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="62bf4-152">How to detach a data disk from a classic Windows virtual machine</span></span>](windows/classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-153">Use the D drive as a data drive on a Windows VM</span><span class="sxs-lookup"><span data-stu-id="62bf4-153">Use the D drive as a data drive on a Windows VM</span></span>](windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="networking"></a><span data-ttu-id="62bf4-154">Networking</span><span class="sxs-lookup"><span data-stu-id="62bf4-154">Networking</span></span>
[<span data-ttu-id="62bf4-155">Virtual Network Overview</span><span class="sxs-lookup"><span data-stu-id="62bf4-155">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="62bf4-156">Connect virtual machines created with the classic deployment model with a virtual network or cloud service</span><span class="sxs-lookup"><span data-stu-id="62bf4-156">Connect virtual machines created with the classic deployment model with a virtual network or cloud service</span></span>](windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-157">Manage NSGs using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="62bf4-157">Manage NSGs using Azure PowerShell</span></span>](../virtual-network/virtual-networks-create-nsg-classic-ps.md)

[<span data-ttu-id="62bf4-158">Create a load balancer</span><span class="sxs-lookup"><span data-stu-id="62bf4-158">Create a load balancer</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)

## <a name="develop"></a><span data-ttu-id="62bf4-159">Develop</span><span class="sxs-lookup"><span data-stu-id="62bf4-159">Develop</span></span>
[<span data-ttu-id="62bf4-160">Create and Manage Azure Virtual Machines in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62bf4-160">Create and Manage Azure Virtual Machines in Visual Studio</span></span>](windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-161">Creating a virtual machine for a web application with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62bf4-161">Creating a virtual machine for a web application with Visual Studio</span></span>](windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-162">How to run a compute-intensive task in Java on a virtual machine</span><span class="sxs-lookup"><span data-stu-id="62bf4-162">How to run a compute-intensive task in Java on a virtual machine</span></span>](windows/classic/java-run-compute-intensive-task.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-163">Django Hello World web application on a Windows Server VM</span><span class="sxs-lookup"><span data-stu-id="62bf4-163">Django Hello World web application on a Windows Server VM</span></span>](windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="workloads"></a><span data-ttu-id="62bf4-164">Workloads</span><span class="sxs-lookup"><span data-stu-id="62bf4-164">Workloads</span></span>
[<span data-ttu-id="62bf4-165">HPC Pack</span><span class="sxs-lookup"><span data-stu-id="62bf4-165">HPC Pack</span></span>](windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-166">MongoDB</span><span class="sxs-lookup"><span data-stu-id="62bf4-166">MongoDB</span></span>](windows/classic/install-mongodb.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-167">MySQL</span><span class="sxs-lookup"><span data-stu-id="62bf4-167">MySQL</span></span>](windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-168">Oracle</span><span class="sxs-lookup"><span data-stu-id="62bf4-168">Oracle</span></span>](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html#support)

[<span data-ttu-id="62bf4-169">SAP</span><span class="sxs-lookup"><span data-stu-id="62bf4-169">SAP</span></span>](windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-170">SQL Server</span><span class="sxs-lookup"><span data-stu-id="62bf4-170">SQL Server</span></span>](./windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[<span data-ttu-id="62bf4-171">Tomcat</span><span class="sxs-lookup"><span data-stu-id="62bf4-171">Tomcat</span></span>](windows/classic/java-run-tomcat-app-server.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="reference"></a><span data-ttu-id="62bf4-172">Reference</span><span class="sxs-lookup"><span data-stu-id="62bf4-172">Reference</span></span>
[<span data-ttu-id="62bf4-173">Azure CLI commands in Service Management mode</span><span class="sxs-lookup"><span data-stu-id="62bf4-173">Azure CLI commands in Service Management mode</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)

[<span data-ttu-id="62bf4-174">Service Management REST API</span><span class="sxs-lookup"><span data-stu-id="62bf4-174">Service Management REST API</span></span>](https://msdn.microsoft.com/library/azure/ee460799.aspx)

[<span data-ttu-id="62bf4-175">Service Management .NET API</span><span class="sxs-lookup"><span data-stu-id="62bf4-175">Service Management .NET API</span></span>](https://msdn.microsoft.com/library/azure/mt420161.aspx)

[<span data-ttu-id="62bf4-176">Azure Service Management PowerShell cmdlet reference documentation</span><span class="sxs-lookup"><span data-stu-id="62bf4-176">Azure Service Management PowerShell cmdlet reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn708504.aspx)

## <a name="troubleshooting"></a><span data-ttu-id="62bf4-177">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="62bf4-177">Troubleshooting</span></span>
[<span data-ttu-id="62bf4-178">Troubleshoot Remote Desktop connections to an Azure virtual machine running Windows</span><span class="sxs-lookup"><span data-stu-id="62bf4-178">Troubleshoot Remote Desktop connections to an Azure virtual machine running Windows</span></span>](windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-179">Troubleshoot Access to an Application Running on an Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="62bf4-179">Troubleshoot Access to an Application Running on an Azure Virtual Machine</span></span>](windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-180">Troubleshoot allocation failures when you create, restart, or resize VMs in Azure</span><span class="sxs-lookup"><span data-stu-id="62bf4-180">Troubleshoot allocation failures when you create, restart, or resize VMs in Azure</span></span>](windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="62bf4-181">Troubleshoot classic deployment issues with creating a new Windows virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="62bf4-181">Troubleshoot classic deployment issues with creating a new Windows virtual machine in Azure</span></span>](windows/classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

[<span data-ttu-id="62bf4-182">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span><span class="sxs-lookup"><span data-stu-id="62bf4-182">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>](windows/classic/virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
