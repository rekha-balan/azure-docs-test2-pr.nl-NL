---
title: Use Azure Resource Manager templates in Azure Stack | Microsoft Docs
description: Learn how to use Azure Resource Manager templates in Azure Stack to provision resources.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2018
ms.author: sethm
ms.reviewer: jeffgo
ms.openlocfilehash: a50f91d5cbbc0eac7080437c96144014dad651ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856310"
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a><span data-ttu-id="081bc-103">Use Azure Resource Manager templates in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="081bc-103">Use Azure Resource Manager templates in Azure Stack</span></span>

<span data-ttu-id="081bc-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="081bc-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="081bc-105">You can use Azure Resource Manager templates to deploy and provision all the resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="081bc-105">You can use Azure Resource Manager templates to deploy and provision all the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="081bc-106">You can also redeploy templates to make changes to the resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="081bc-106">You can also redeploy templates to make changes to the resources in a resource group.</span></span>

<span data-ttu-id="081bc-107">These templates can be deployed with the Microsoft Azure Stack portal, PowerShell, the command line, and Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="081bc-107">These templates can be deployed with the Microsoft Azure Stack portal, PowerShell, the command line, and Visual Studio.</span></span>

<span data-ttu-id="081bc-108">The following quickstart templates are available on [GitHub](http://aka.ms/azurestackgithub):</span><span class="sxs-lookup"><span data-stu-id="081bc-108">The following quickstart templates are available on [GitHub](http://aka.ms/azurestackgithub):</span></span>

## <a name="deploy-sharepoint-server-non-high-availability-deployment"></a><span data-ttu-id="081bc-109">Deploy SharePoint Server (non-high-availability deployment)</span><span class="sxs-lookup"><span data-stu-id="081bc-109">Deploy SharePoint Server (non-high-availability deployment)</span></span>

<span data-ttu-id="081bc-110">Use the PowerShell DSC extension to [create a SharePoint Server 2013 farm](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/sharepoint-2013-non-ha) that includes the following resources:</span><span class="sxs-lookup"><span data-stu-id="081bc-110">Use the PowerShell DSC extension to [create a SharePoint Server 2013 farm](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/sharepoint-2013-non-ha) that includes the following resources:</span></span>

* <span data-ttu-id="081bc-111">A virtual network</span><span class="sxs-lookup"><span data-stu-id="081bc-111">A virtual network</span></span>
* <span data-ttu-id="081bc-112">Three storage accounts</span><span class="sxs-lookup"><span data-stu-id="081bc-112">Three storage accounts</span></span>
* <span data-ttu-id="081bc-113">Two external load balancers</span><span class="sxs-lookup"><span data-stu-id="081bc-113">Two external load balancers</span></span>
* <span data-ttu-id="081bc-114">One virtual machine (VM) configured as a domain controller for a new forest with a single domain</span><span class="sxs-lookup"><span data-stu-id="081bc-114">One virtual machine (VM) configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="081bc-115">One VM configured as a SQL Server 2014 stand-alone server</span><span class="sxs-lookup"><span data-stu-id="081bc-115">One VM configured as a SQL Server 2014 stand-alone server</span></span>
* <span data-ttu-id="081bc-116">One VM configured as a one machine SharePoint Server 2013 farm</span><span class="sxs-lookup"><span data-stu-id="081bc-116">One VM configured as a one machine SharePoint Server 2013 farm</span></span>

## <a name="deploy-ad-non-high-availability-deployment"></a><span data-ttu-id="081bc-117">Deploy AD (non-high-availability-deployment)</span><span class="sxs-lookup"><span data-stu-id="081bc-117">Deploy AD (non-high-availability-deployment)</span></span>

<span data-ttu-id="081bc-118">Use the PowerShell DSC extension to [create an AD domain controller server](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/ad-non-ha) that includes the following resources:</span><span class="sxs-lookup"><span data-stu-id="081bc-118">Use the PowerShell DSC extension to [create an AD domain controller server](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/ad-non-ha) that includes the following resources:</span></span>

* <span data-ttu-id="081bc-119">A virtual network</span><span class="sxs-lookup"><span data-stu-id="081bc-119">A virtual network</span></span>
* <span data-ttu-id="081bc-120">One storage account</span><span class="sxs-lookup"><span data-stu-id="081bc-120">One storage account</span></span>
* <span data-ttu-id="081bc-121">One external load balancer</span><span class="sxs-lookup"><span data-stu-id="081bc-121">One external load balancer</span></span>
* <span data-ttu-id="081bc-122">One virtual machine (VM) configured as a domain controller for a new forest with a single domain</span><span class="sxs-lookup"><span data-stu-id="081bc-122">One virtual machine (VM) configured as a domain controller for a new forest with a single domain</span></span>

## <a name="deploy-adsql-non-high-availability-deployment"></a><span data-ttu-id="081bc-123">Deploy AD/SQL (non-high-availability-deployment)</span><span class="sxs-lookup"><span data-stu-id="081bc-123">Deploy AD/SQL (non-high-availability-deployment)</span></span>

<span data-ttu-id="081bc-124">Use the PowerShell DSC extension to [create a SQL Server 2014 stand-alone server](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/sql-2014-non-ha) that includes the following resources:</span><span class="sxs-lookup"><span data-stu-id="081bc-124">Use the PowerShell DSC extension to [create a SQL Server 2014 stand-alone server](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/sql-2014-non-ha) that includes the following resources:</span></span>

* <span data-ttu-id="081bc-125">A virtual network</span><span class="sxs-lookup"><span data-stu-id="081bc-125">A virtual network</span></span>
* <span data-ttu-id="081bc-126">Two storage accounts</span><span class="sxs-lookup"><span data-stu-id="081bc-126">Two storage accounts</span></span>
* <span data-ttu-id="081bc-127">One external load balancer</span><span class="sxs-lookup"><span data-stu-id="081bc-127">One external load balancer</span></span>
* <span data-ttu-id="081bc-128">One virtual machine (VM) configured as a domain controller for a new forest with a single domain</span><span class="sxs-lookup"><span data-stu-id="081bc-128">One virtual machine (VM) configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="081bc-129">One VM configured as a SQL Server 2014 stand-alone server</span><span class="sxs-lookup"><span data-stu-id="081bc-129">One VM configured as a SQL Server 2014 stand-alone server</span></span>

## <a name="vm-dsc-extension-azure-automation-pull-server"></a><span data-ttu-id="081bc-130">VM-DSC-Extension-Azure-Automation-Pull-Server</span><span class="sxs-lookup"><span data-stu-id="081bc-130">VM-DSC-Extension-Azure-Automation-Pull-Server</span></span>

<span data-ttu-id="081bc-131">Use the PowerShell DSC extension to configure an existing virtual machine Local Configuration Manager (LCM) and register it to an Azure Automation Account DSC Pull Server.</span><span class="sxs-lookup"><span data-stu-id="081bc-131">Use the PowerShell DSC extension to configure an existing virtual machine Local Configuration Manager (LCM) and register it to an Azure Automation Account DSC Pull Server.</span></span>

## <a name="create-a-virtual-machine-from-a-user-image"></a><span data-ttu-id="081bc-132">Create a virtual machine from a user image</span><span class="sxs-lookup"><span data-stu-id="081bc-132">Create a virtual machine from a user image</span></span>

<span data-ttu-id="081bc-133">[Create a virtual machine from a custom user image](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/101-vm-from-user-image).</span><span class="sxs-lookup"><span data-stu-id="081bc-133">[Create a virtual machine from a custom user image](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/101-vm-from-user-image).</span></span> <span data-ttu-id="081bc-134">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span><span class="sxs-lookup"><span data-stu-id="081bc-134">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="basic-virtual-machine"></a><span data-ttu-id="081bc-135">Basic virtual machine</span><span class="sxs-lookup"><span data-stu-id="081bc-135">Basic virtual machine</span></span>

<span data-ttu-id="081bc-136">[Deploy a Windows VM](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/101-simple-windows-vm) that includes a virtual network (with DNS), public IP address, and a network interface.</span><span class="sxs-lookup"><span data-stu-id="081bc-136">[Deploy a Windows VM](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/AzureStackTechnicalPreview1/101-simple-windows-vm) that includes a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="cancel-a-running-template-deployment"></a><span data-ttu-id="081bc-137">Cancel a running template deployment</span><span class="sxs-lookup"><span data-stu-id="081bc-137">Cancel a running template deployment</span></span>

<span data-ttu-id="081bc-138">To cancel a running template deployment, use the [Stop-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/stop-azurermresourcegroupdeployment) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="081bc-138">To cancel a running template deployment, use the [Stop-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/stop-azurermresourcegroupdeployment) PowerShell cmdlet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="081bc-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="081bc-139">Next steps</span></span>

* [<span data-ttu-id="081bc-140">Deploy templates with the portal</span><span class="sxs-lookup"><span data-stu-id="081bc-140">Deploy templates with the portal</span></span>](azure-stack-deploy-template-portal.md)
* [<span data-ttu-id="081bc-141">Azure Resource Manager overview</span><span class="sxs-lookup"><span data-stu-id="081bc-141">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
