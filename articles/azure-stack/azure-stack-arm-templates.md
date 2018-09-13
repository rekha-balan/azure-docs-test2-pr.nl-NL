---
title: Use Azure Resource Manager templates in Azure Stack | Microsoft Docs
description: Learn how to use Azure Resource Manager templates in Azure Stack to provision resources.
services: azure-stack
documentationcenter: ''
author: heathl17
manager: byronr
editor: ''
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/1/2017
ms.author: helaw
ms.openlocfilehash: 850222bb25d637e4c73e12718fd7965abc9bd37c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554185"
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a><span data-ttu-id="b22f7-103">Use Azure Resource Manager templates in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b22f7-103">Use Azure Resource Manager templates in Azure Stack</span></span>
<span data-ttu-id="b22f7-104">Azure Resource Manager templates deploy and provision all of the resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="b22f7-104">Azure Resource Manager templates deploy and provision all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="b22f7-105">You define the resources for the application and how it will be deployed.</span><span class="sxs-lookup"><span data-stu-id="b22f7-105">You define the resources for the application and how it will be deployed.</span></span>  <span data-ttu-id="b22f7-106">You can also redeploy templates to make changes to the resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="b22f7-106">You can also redeploy templates to make changes to the resources in the resource group.</span></span>

<span data-ttu-id="b22f7-107">These templates can be deployed with the Microsoft Azure Stack portal, PowerShell, the command line, and Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b22f7-107">These templates can be deployed with the Microsoft Azure Stack portal, PowerShell, the command line, and Visual Studio.</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/azurestack/Microsoft-Azure-Stack-TP1--Foundational-Skills-1-Deploying-JSON-Templates/player]


<span data-ttu-id="b22f7-108">The following templates are available on [GitHub](http://aka.ms/azurestackgithub):</span><span class="sxs-lookup"><span data-stu-id="b22f7-108">The following templates are available on [GitHub](http://aka.ms/azurestackgithub):</span></span>

## <a name="deploy-sharepoint-non-high-availability"></a><span data-ttu-id="b22f7-109">Deploy SharePoint (non-high availability)</span><span class="sxs-lookup"><span data-stu-id="b22f7-109">Deploy SharePoint (non-high availability)</span></span>
<span data-ttu-id="b22f7-110">Use the PowerShell DSC extension to create a SharePoint 2013 farm that includes the following:</span><span class="sxs-lookup"><span data-stu-id="b22f7-110">Use the PowerShell DSC extension to create a SharePoint 2013 farm that includes the following:</span></span>

* <span data-ttu-id="b22f7-111">A virtual network</span><span class="sxs-lookup"><span data-stu-id="b22f7-111">A virtual network</span></span>
* <span data-ttu-id="b22f7-112">Three storage accounts</span><span class="sxs-lookup"><span data-stu-id="b22f7-112">Three storage accounts</span></span>
* <span data-ttu-id="b22f7-113">Two external load balancers</span><span class="sxs-lookup"><span data-stu-id="b22f7-113">Two external load balancers</span></span>
* <span data-ttu-id="b22f7-114">One VM configured as a domain controller for a new forest with a single domain</span><span class="sxs-lookup"><span data-stu-id="b22f7-114">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="b22f7-115">One VM configured as a SQL Server 2014 stand-alone server</span><span class="sxs-lookup"><span data-stu-id="b22f7-115">One VM configured as a SQL Server 2014 stand-alone server</span></span>
* <span data-ttu-id="b22f7-116">One VM configured as a one machine SharePoint 2013 farm</span><span class="sxs-lookup"><span data-stu-id="b22f7-116">One VM configured as a one machine SharePoint 2013 farm</span></span>

## <a name="deploy-ad-non-high-availability"></a><span data-ttu-id="b22f7-117">Deploy AD (non-high availability)</span><span class="sxs-lookup"><span data-stu-id="b22f7-117">Deploy AD (non-high availability)</span></span>
<span data-ttu-id="b22f7-118">Use the PowerShell DSC extension to create an AD domain controller server that includes the following:</span><span class="sxs-lookup"><span data-stu-id="b22f7-118">Use the PowerShell DSC extension to create an AD domain controller server that includes the following:</span></span>

* <span data-ttu-id="b22f7-119">A virtual network</span><span class="sxs-lookup"><span data-stu-id="b22f7-119">A virtual network</span></span>
* <span data-ttu-id="b22f7-120">One storage account</span><span class="sxs-lookup"><span data-stu-id="b22f7-120">One storage account</span></span>
* <span data-ttu-id="b22f7-121">One external load balancer</span><span class="sxs-lookup"><span data-stu-id="b22f7-121">One external load balancer</span></span>
* <span data-ttu-id="b22f7-122">One VM configured as a domain controller for a new forest with a single domain</span><span class="sxs-lookup"><span data-stu-id="b22f7-122">One VM configured as a domain controller for a new forest with a single domain</span></span>

## <a name="deploy-adsql-non-high-availability"></a><span data-ttu-id="b22f7-123">Deploy AD/SQL (non-high availability)</span><span class="sxs-lookup"><span data-stu-id="b22f7-123">Deploy AD/SQL (non-high availability)</span></span>
<span data-ttu-id="b22f7-124">Use the PowerShell DSC extension to create a SQL Server 2014 stand-alone server that includes the following:</span><span class="sxs-lookup"><span data-stu-id="b22f7-124">Use the PowerShell DSC extension to create a SQL Server 2014 stand-alone server that includes the following:</span></span>

* <span data-ttu-id="b22f7-125">A virtual network</span><span class="sxs-lookup"><span data-stu-id="b22f7-125">A virtual network</span></span>
* <span data-ttu-id="b22f7-126">Two storage accounts</span><span class="sxs-lookup"><span data-stu-id="b22f7-126">Two storage accounts</span></span>
* <span data-ttu-id="b22f7-127">One external load balancer</span><span class="sxs-lookup"><span data-stu-id="b22f7-127">One external load balancer</span></span>
* <span data-ttu-id="b22f7-128">One VM configured as a domain controller for a new forest with a single domain</span><span class="sxs-lookup"><span data-stu-id="b22f7-128">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="b22f7-129">One VM configured as a SQL Server 2014 stand-alone server</span><span class="sxs-lookup"><span data-stu-id="b22f7-129">One VM configured as a SQL Server 2014 stand-alone server</span></span>

## <a name="vm-dsc-extension-azure-automation-pull-server"></a><span data-ttu-id="b22f7-130">VM-DSC-Extension-Azure-Automation-Pull-Server</span><span class="sxs-lookup"><span data-stu-id="b22f7-130">VM-DSC-Extension-Azure-Automation-Pull-Server</span></span>
<span data-ttu-id="b22f7-131">Use the PowerShell DSC extension to configure an existing virtual machine Local Configuration Manager (LCM) and register it to an Azure Automation Account DSC Pull Server.</span><span class="sxs-lookup"><span data-stu-id="b22f7-131">Use the PowerShell DSC extension to configure an existing virtual machine Local Configuration Manager (LCM) and register it to an Azure Automation Account DSC Pull Server.</span></span>

## <a name="create-a-virtual-machine-from-a-user-image"></a><span data-ttu-id="b22f7-132">Create a virtual machine from a user image</span><span class="sxs-lookup"><span data-stu-id="b22f7-132">Create a virtual machine from a user image</span></span>
<span data-ttu-id="b22f7-133">Create a virtual machine from a custom user image.</span><span class="sxs-lookup"><span data-stu-id="b22f7-133">Create a virtual machine from a custom user image.</span></span> <span data-ttu-id="b22f7-134">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span><span class="sxs-lookup"><span data-stu-id="b22f7-134">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="simple-vm"></a><span data-ttu-id="b22f7-135">Simple VM</span><span class="sxs-lookup"><span data-stu-id="b22f7-135">Simple VM</span></span>
<span data-ttu-id="b22f7-136">Deploy a simple Windows VM that includes a virtual network (with DNS), public IP address, and a network interface.</span><span class="sxs-lookup"><span data-stu-id="b22f7-136">Deploy a simple Windows VM that includes a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="cancel-a-running-template-deployment"></a><span data-ttu-id="b22f7-137">Cancel a running template deployment</span><span class="sxs-lookup"><span data-stu-id="b22f7-137">Cancel a running template deployment</span></span>
<span data-ttu-id="b22f7-138">To cancel a running template deployment, use the `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b22f7-138">To cancel a running template deployment, use the `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b22f7-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="b22f7-139">Next steps</span></span>
[<span data-ttu-id="b22f7-140">Deploy templates with the portal</span><span class="sxs-lookup"><span data-stu-id="b22f7-140">Deploy templates with the portal</span></span>](azure-stack-deploy-template-portal.md)

[<span data-ttu-id="b22f7-141">Azure Resource Manager overview</span><span class="sxs-lookup"><span data-stu-id="b22f7-141">Azure Resource Manager overview</span></span>](../azure-resource-manager/resource-group-overview.md)

