---
title: Connect a Cloud Service to a custom Domain Controller | Microsoft Docs
description: Learn how to connect your web/worker roles to a custom AD Domain using PowerShell and AD Domain Extension
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/04/2017
ms.author: adegeo
ms.openlocfilehash: 39ee9cc1027958d85b2af2781adab0fe06c9a433
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552471"
---
# <a name="connecting-azure-cloud-services-roles-to-a-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="2726c-103">Connecting Azure Cloud Services Roles to a custom AD Domain Controller hosted in Azure</span><span class="sxs-lookup"><span data-stu-id="2726c-103">Connecting Azure Cloud Services Roles to a custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="2726c-104">We will first set up a Virtual Network (VNet) in Azure.</span><span class="sxs-lookup"><span data-stu-id="2726c-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="2726c-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) to the VNet.</span><span class="sxs-lookup"><span data-stu-id="2726c-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) to the VNet.</span></span> <span data-ttu-id="2726c-106">Next, we will add existing cloud service roles to the pre-created VNet and subsequently connect them to the Domain Controller.</span><span class="sxs-lookup"><span data-stu-id="2726c-106">Next, we will add existing cloud service roles to the pre-created VNet and subsequently connect them to the Domain Controller.</span></span>

<span data-ttu-id="2726c-107">Before we get started, couple of things to keep in mind:</span><span class="sxs-lookup"><span data-stu-id="2726c-107">Before we get started, couple of things to keep in mind:</span></span>

1. <span data-ttu-id="2726c-108">This tutorial uses PowerShell, so please make sure you have Azure PowerShell installed and ready to go.</span><span class="sxs-lookup"><span data-stu-id="2726c-108">This tutorial uses PowerShell, so please make sure you have Azure PowerShell installed and ready to go.</span></span> <span data-ttu-id="2726c-109">To get help with setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="2726c-109">To get help with setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
2. <span data-ttu-id="2726c-110">Your AD Domain Controller and Web/Worker Role instances need to be in the VNet.</span><span class="sxs-lookup"><span data-stu-id="2726c-110">Your AD Domain Controller and Web/Worker Role instances need to be in the VNet.</span></span>

<span data-ttu-id="2726c-111">Follow this step-by-step guide and if you run into any issues, leave us a comment below.</span><span class="sxs-lookup"><span data-stu-id="2726c-111">Follow this step-by-step guide and if you run into any issues, leave us a comment below.</span></span> <span data-ttu-id="2726c-112">Someone will get back to you (yes, we do read comments).</span><span class="sxs-lookup"><span data-stu-id="2726c-112">Someone will get back to you (yes, we do read comments).</span></span>

<span data-ttu-id="2726c-113">The network that is referenced by the cloud service must be a **classic virtual network**.</span><span class="sxs-lookup"><span data-stu-id="2726c-113">The network that is referenced by the cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="2726c-114">Create a Virtual Network</span><span class="sxs-lookup"><span data-stu-id="2726c-114">Create a Virtual Network</span></span>
<span data-ttu-id="2726c-115">You can create a Virtual Network in Azure using the Azure classic portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2726c-115">You can create a Virtual Network in Azure using the Azure classic portal or PowerShell.</span></span> <span data-ttu-id="2726c-116">For this tutorial, we will use PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2726c-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="2726c-117">To create a Virtual Network using the Azure classic portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="2726c-117">To create a Virtual Network using the Azure classic portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="2726c-118">Create a Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="2726c-118">Create a Virtual Machine</span></span>
<span data-ttu-id="2726c-119">Once you have completed setting up the Virtual Network, you will need to create an AD Domain Controller.</span><span class="sxs-lookup"><span data-stu-id="2726c-119">Once you have completed setting up the Virtual Network, you will need to create an AD Domain Controller.</span></span> <span data-ttu-id="2726c-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="2726c-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="2726c-121">To do this, create a virtual machine through PowerShell using the commands below:</span><span class="sxs-lookup"><span data-stu-id="2726c-121">To do this, create a virtual machine through PowerShell using the commands below:</span></span>

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it to the Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-to-a-domain-controller"></a><span data-ttu-id="2726c-122">Promote your Virtual Machine to a Domain Controller</span><span class="sxs-lookup"><span data-stu-id="2726c-122">Promote your Virtual Machine to a Domain Controller</span></span>
<span data-ttu-id="2726c-123">To configure the Virtual Machine as an AD Domain Controller, you will need to log in to the VM and configure it.</span><span class="sxs-lookup"><span data-stu-id="2726c-123">To configure the Virtual Machine as an AD Domain Controller, you will need to log in to the VM and configure it.</span></span>

<span data-ttu-id="2726c-124">To log in to the VM, you can get the RDP file through PowerShell, use the commands below.</span><span class="sxs-lookup"><span data-stu-id="2726c-124">To log in to the VM, you can get the RDP file through PowerShell, use the commands below.</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="2726c-125">Once you are logged into the VM, setup your Virtual Machine as an AD Domain Controller by following the step-by-step guide on [How to setup your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="2726c-125">Once you are logged into the VM, setup your Virtual Machine as an AD Domain Controller by following the step-by-step guide on [How to setup your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-to-the-virtual-network"></a><span data-ttu-id="2726c-126">Add your Cloud Service to the Virtual Network</span><span class="sxs-lookup"><span data-stu-id="2726c-126">Add your Cloud Service to the Virtual Network</span></span>
<span data-ttu-id="2726c-127">Next, you need to add your cloud service deployment to the VNet you just created.</span><span class="sxs-lookup"><span data-stu-id="2726c-127">Next, you need to add your cloud service deployment to the VNet you just created.</span></span> <span data-ttu-id="2726c-128">To do this, modify your cloud service cscfg by adding the relevant sections to your cscfg using Visual Studio or the editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="2726c-128">To do this, modify your cloud service cscfg by adding the relevant sections to your cscfg using Visual Studio or the editor of your choice.</span></span>

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

<span data-ttu-id="2726c-129">Next build your cloud services project and deploy it to Azure.</span><span class="sxs-lookup"><span data-stu-id="2726c-129">Next build your cloud services project and deploy it to Azure.</span></span> <span data-ttu-id="2726c-130">To get help with deploying your cloud services package to Azure, see [How to Create and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="2726c-130">To get help with deploying your cloud services package to Azure, see [How to Create and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-to-the-domain"></a><span data-ttu-id="2726c-131">Connect your web/worker role(s) to the domain</span><span class="sxs-lookup"><span data-stu-id="2726c-131">Connect your web/worker role(s) to the domain</span></span>
<span data-ttu-id="2726c-132">Once your cloud service project is deployed on Azure, connect your role instances to the custom AD domain using the AD Domain Extension.</span><span class="sxs-lookup"><span data-stu-id="2726c-132">Once your cloud service project is deployed on Azure, connect your role instances to the custom AD domain using the AD Domain Extension.</span></span> <span data-ttu-id="2726c-133">To add the AD Domain Extension to your existing cloud services deployment and join the custom domain, execute the following commands in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2726c-133">To add the AD Domain Extension to your existing cloud services deployment and join the custom domain, execute the following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension to the cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="2726c-134">And that's it.</span><span class="sxs-lookup"><span data-stu-id="2726c-134">And that's it.</span></span>

<span data-ttu-id="2726c-135">Your cloud services should now be joined to your custom domain controller.</span><span class="sxs-lookup"><span data-stu-id="2726c-135">Your cloud services should now be joined to your custom domain controller.</span></span> <span data-ttu-id="2726c-136">If you would like to learn more about the different options available for how to configure AD Domain Extension, use the PowerShell help as shown below.</span><span class="sxs-lookup"><span data-stu-id="2726c-136">If you would like to learn more about the different options available for how to configure AD Domain Extension, use the PowerShell help as shown below.</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
