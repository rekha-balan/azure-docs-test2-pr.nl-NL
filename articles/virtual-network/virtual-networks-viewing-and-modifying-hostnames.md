---
title: Viewing and Modifying Hostnames | Microsoft Docs
description: How to view and change hostnames for Azure virtual machines, web and worker roles for name resolution
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 9a3a1e1b58dcb828e2d2d09c18f1aab6d46051aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671072"
---
# <a name="viewing-and-modifying-hostnames"></a><span data-ttu-id="4d27e-103">Viewing and modifying hostnames</span><span class="sxs-lookup"><span data-stu-id="4d27e-103">Viewing and modifying hostnames</span></span>
<span data-ttu-id="4d27e-104">To allow your role instances to be referenced by host name, you must set the value for the host name in the service configuration file for each role.</span><span class="sxs-lookup"><span data-stu-id="4d27e-104">To allow your role instances to be referenced by host name, you must set the value for the host name in the service configuration file for each role.</span></span> <span data-ttu-id="4d27e-105">You do that by adding the desired host name to the **vmName** attribute of the **Role** element.</span><span class="sxs-lookup"><span data-stu-id="4d27e-105">You do that by adding the desired host name to the **vmName** attribute of the **Role** element.</span></span> <span data-ttu-id="4d27e-106">The value of the **vmName** attribute is used as a base for the host name of each role instance.</span><span class="sxs-lookup"><span data-stu-id="4d27e-106">The value of the **vmName** attribute is used as a base for the host name of each role instance.</span></span> <span data-ttu-id="4d27e-107">For example, if **vmName** is *webrole* and there are three instances of that role, the host names of the instances will be *webrole0*, *webrole1*, and *webrole2*.</span><span class="sxs-lookup"><span data-stu-id="4d27e-107">For example, if **vmName** is *webrole* and there are three instances of that role, the host names of the instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span> <span data-ttu-id="4d27e-108">You do not need to specify a host name for virtual machines in the configuration file, because the host name for a virtual machine is populated based on the virtual machine name.</span><span class="sxs-lookup"><span data-stu-id="4d27e-108">You do not need to specify a host name for virtual machines in the configuration file, because the host name for a virtual machine is populated based on the virtual machine name.</span></span> <span data-ttu-id="4d27e-109">For more information about configuring a Microsoft Azure service, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span><span class="sxs-lookup"><span data-stu-id="4d27e-109">For more information about configuring a Microsoft Azure service, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span></span>

## <a name="viewing-hostnames"></a><span data-ttu-id="4d27e-110">Viewing hostnames</span><span class="sxs-lookup"><span data-stu-id="4d27e-110">Viewing hostnames</span></span>
<span data-ttu-id="4d27e-111">You can view the host names of virtual machines and role instances in a cloud service by using any of the tools below.</span><span class="sxs-lookup"><span data-stu-id="4d27e-111">You can view the host names of virtual machines and role instances in a cloud service by using any of the tools below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4d27e-112">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4d27e-112">Azure Portal</span></span>
<span data-ttu-id="4d27e-113">You can use the [Azure portal](http://portal.azure.com) to view the host names for virtual machines on the overview blade for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="4d27e-113">You can use the [Azure portal](http://portal.azure.com) to view the host names for virtual machines on the overview blade for a virtual machine.</span></span> <span data-ttu-id="4d27e-114">Keep in mind that the blade shows a value for **Name** and **Host Name**.</span><span class="sxs-lookup"><span data-stu-id="4d27e-114">Keep in mind that the blade shows a value for **Name** and **Host Name**.</span></span> <span data-ttu-id="4d27e-115">Although they are initially the same, changing the host name will not change the name of the virtual machine or role instance.</span><span class="sxs-lookup"><span data-stu-id="4d27e-115">Although they are initially the same, changing the host name will not change the name of the virtual machine or role instance.</span></span>

<span data-ttu-id="4d27e-116">Role instances can also be viewed in the Azure portal, but when you list the instances in a cloud service, the host name is not displayed.</span><span class="sxs-lookup"><span data-stu-id="4d27e-116">Role instances can also be viewed in the Azure portal, but when you list the instances in a cloud service, the host name is not displayed.</span></span> <span data-ttu-id="4d27e-117">You will see a name for each instance, but that name does not represent the host name.</span><span class="sxs-lookup"><span data-stu-id="4d27e-117">You will see a name for each instance, but that name does not represent the host name.</span></span>

### <a name="service-configuration-file"></a><span data-ttu-id="4d27e-118">Service configuration file</span><span class="sxs-lookup"><span data-stu-id="4d27e-118">Service configuration file</span></span>
<span data-ttu-id="4d27e-119">You can download the service configuration file for a deployed service from the **Configure** blade of the service in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4d27e-119">You can download the service configuration file for a deployed service from the **Configure** blade of the service in the Azure portal.</span></span> <span data-ttu-id="4d27e-120">You can then look for the **vmName** attribute for the **Role name** element to see the host name.</span><span class="sxs-lookup"><span data-stu-id="4d27e-120">You can then look for the **vmName** attribute for the **Role name** element to see the host name.</span></span> <span data-ttu-id="4d27e-121">Keep in mind that this host name is used as a base for the host name of each role instance.</span><span class="sxs-lookup"><span data-stu-id="4d27e-121">Keep in mind that this host name is used as a base for the host name of each role instance.</span></span> <span data-ttu-id="4d27e-122">For example, if **vmName** is *webrole* and there are three instances of that role, the host names of the instances will be *webrole0*, *webrole1*, and *webrole2*.</span><span class="sxs-lookup"><span data-stu-id="4d27e-122">For example, if **vmName** is *webrole* and there are three instances of that role, the host names of the instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span>

### <a name="remote-desktop"></a><span data-ttu-id="4d27e-123">Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="4d27e-123">Remote Desktop</span></span>
<span data-ttu-id="4d27e-124">After you enable Remote Desktop (Windows), Windows PowerShell remoting (Windows), or SSH (Linux and Windows) connections to your virtual machines or role instances, you can view the host name from an active Remote Desktop connection in various ways:</span><span class="sxs-lookup"><span data-stu-id="4d27e-124">After you enable Remote Desktop (Windows), Windows PowerShell remoting (Windows), or SSH (Linux and Windows) connections to your virtual machines or role instances, you can view the host name from an active Remote Desktop connection in various ways:</span></span>

* <span data-ttu-id="4d27e-125">Type hostname at the command prompt or SSH terminal.</span><span class="sxs-lookup"><span data-stu-id="4d27e-125">Type hostname at the command prompt or SSH terminal.</span></span>
* <span data-ttu-id="4d27e-126">Type ipconfig /all at the command prompt (Windows only).</span><span class="sxs-lookup"><span data-stu-id="4d27e-126">Type ipconfig /all at the command prompt (Windows only).</span></span>
* <span data-ttu-id="4d27e-127">View the computer name in the system settings (Windows only).</span><span class="sxs-lookup"><span data-stu-id="4d27e-127">View the computer name in the system settings (Windows only).</span></span>

### <a name="azure-service-management-rest-api"></a><span data-ttu-id="4d27e-128">Azure Service Management REST API</span><span class="sxs-lookup"><span data-stu-id="4d27e-128">Azure Service Management REST API</span></span>
<span data-ttu-id="4d27e-129">From a REST client, follow these instructions:</span><span class="sxs-lookup"><span data-stu-id="4d27e-129">From a REST client, follow these instructions:</span></span>

1. <span data-ttu-id="4d27e-130">Ensure that you have a client certificate to connect to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4d27e-130">Ensure that you have a client certificate to connect to the Azure portal.</span></span> <span data-ttu-id="4d27e-131">To obtain a client certificate, follow the steps presented in [How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d27e-131">To obtain a client certificate, follow the steps presented in [How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span> 
2. <span data-ttu-id="4d27e-132">Set a header entry named x-ms-version with a value of 2013-11-01.</span><span class="sxs-lookup"><span data-stu-id="4d27e-132">Set a header entry named x-ms-version with a value of 2013-11-01.</span></span>
3. <span data-ttu-id="4d27e-133">Send a request in the following format: https://management.core.windows.net/\<subscrition-id\>/services/hostedservices/\<service-name\>?embed-detail=true</span><span class="sxs-lookup"><span data-stu-id="4d27e-133">Send a request in the following format: https://management.core.windows.net/\<subscrition-id\>/services/hostedservices/\<service-name\>?embed-detail=true</span></span>
4. <span data-ttu-id="4d27e-134">Look for the **HostName** element for each **RoleInstance** element.</span><span class="sxs-lookup"><span data-stu-id="4d27e-134">Look for the **HostName** element for each **RoleInstance** element.</span></span>

> [!WARNING]
> <span data-ttu-id="4d27e-135">You can also view the internal domain suffix for your cloud service from the REST call response by checking the **InternalDnsSuffix** element, or by running ipconfig /all from a command prompt in a Remote Desktop session (Windows), or by running cat /etc/resolv.conf from an SSH terminal (Linux).</span><span class="sxs-lookup"><span data-stu-id="4d27e-135">You can also view the internal domain suffix for your cloud service from the REST call response by checking the **InternalDnsSuffix** element, or by running ipconfig /all from a command prompt in a Remote Desktop session (Windows), or by running cat /etc/resolv.conf from an SSH terminal (Linux).</span></span>
> 
> 

## <a name="modifying-a-hostname"></a><span data-ttu-id="4d27e-136">Modifying a hostname</span><span class="sxs-lookup"><span data-stu-id="4d27e-136">Modifying a hostname</span></span>
<span data-ttu-id="4d27e-137">You can modify the host name for any virtual machine or role instance by uploading a modified service configuration file, or by renaming the computer from a Remote Desktop session.</span><span class="sxs-lookup"><span data-stu-id="4d27e-137">You can modify the host name for any virtual machine or role instance by uploading a modified service configuration file, or by renaming the computer from a Remote Desktop session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d27e-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d27e-138">Next steps</span></span>
[<span data-ttu-id="4d27e-139">Name Resolution (DNS)</span><span class="sxs-lookup"><span data-stu-id="4d27e-139">Name Resolution (DNS)</span></span>](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[<span data-ttu-id="4d27e-140">Azure Service Configuration Schema (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="4d27e-140">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[<span data-ttu-id="4d27e-141">Azure Virtual Network Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="4d27e-141">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="4d27e-142">Specify DNS settings using network configuration files</span><span class="sxs-lookup"><span data-stu-id="4d27e-142">Specify DNS settings using network configuration files</span></span>](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

