---
title: Create a Windows VM from a template in Azure | Microsoft Docs
description: Use a Resource Manager template and PowerShell to easily create a new Windows VM.
services: virtual-machines-windows
documentationcenter: ''
author: davidmu1
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93efe888f3117b82f27ded259a0803770f236184
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550890"
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="d0052-103">Create a Windows virtual machine from a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="d0052-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="d0052-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0052-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="d0052-105">The [template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json) deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span><span class="sxs-lookup"><span data-stu-id="d0052-105">The [template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json) deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="d0052-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="d0052-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="d0052-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d0052-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="d0052-108">It should take about five minutes to do the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="d0052-108">It should take about five minutes to do the steps in this article.</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="d0052-109">Step 1: Install Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0052-109">Step 1: Install Azure PowerShell</span></span>

<span data-ttu-id="d0052-110">See [How to install and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span><span class="sxs-lookup"><span data-stu-id="d0052-110">See [How to install and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="step-2-create-a-resource-group"></a><span data-ttu-id="d0052-111">Step 2: Create a resource group</span><span class="sxs-lookup"><span data-stu-id="d0052-111">Step 2: Create a resource group</span></span>

<span data-ttu-id="d0052-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0052-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="d0052-113">Get a list of available locations where resources can be created.</span><span class="sxs-lookup"><span data-stu-id="d0052-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="d0052-114">Create the resource group in the location that you select.</span><span class="sxs-lookup"><span data-stu-id="d0052-114">Create the resource group in the location that you select.</span></span> <span data-ttu-id="d0052-115">This example shows the creation of a resource group named **myResourceGroup** in the **Central US** location:</span><span class="sxs-lookup"><span data-stu-id="d0052-115">This example shows the creation of a resource group named **myResourceGroup** in the **Central US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "Central US"
    ```
   
  <span data-ttu-id="d0052-116">You should see something like this example:</span><span class="sxs-lookup"><span data-stu-id="d0052-116">You should see something like this example:</span></span>

    ```powershell 
    ResourceGroupName : myResourceGroup
    Location          : centralus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/{subscription-id}/resourceGroups/myResourceGroup
    ```

## <a name="step-3-create-the-resources"></a><span data-ttu-id="d0052-117">Step 3: Create the resources</span><span class="sxs-lookup"><span data-stu-id="d0052-117">Step 3: Create the resources</span></span>
<span data-ttu-id="d0052-118">Deploy the template and provide parameter values when prompted.</span><span class="sxs-lookup"><span data-stu-id="d0052-118">Deploy the template and provide parameter values when prompted.</span></span> <span data-ttu-id="d0052-119">This example deploys the 101-vm-simple-windows template in the resource group that you created:</span><span class="sxs-lookup"><span data-stu-id="d0052-119">This example deploys the 101-vm-simple-windows template in the resource group that you created:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -TemplateUri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json" 
```
<span data-ttu-id="d0052-120">You're asked to provide the name of the administrator account on the VM, the password of the account, and the DNS prefix.</span><span class="sxs-lookup"><span data-stu-id="d0052-120">You're asked to provide the name of the administrator account on the VM, the password of the account, and the DNS prefix.</span></span>

<span data-ttu-id="d0052-121">You should see something like this example:</span><span class="sxs-lookup"><span data-stu-id="d0052-121">You should see something like this example:</span></span>

    DeploymentName    : azuredeploy
    ResourceGroupName : myResourceGroup
    ProvisioningState : Succeeded
    Timestamp         : 12/29/2016 8:11:37 PM
    Mode              : Incremental
    TemplateLink      :
       Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/
                        101-vm-simple-windows/azuredeploy.json
       ContentVersion : 1.0.0.0
    Parameters        :
      Name             Type                       Value
      ===============  =========================  ==========
      adminUsername    String                     myAdminUser
      adminPassword    SecureString
      dnsLabelPrefix   String                     myDomain
      windowsOSVersion String                     2016-Datacenter
    Outputs           :
      Name             Type                       Value
      ===============  =========================  ===========
      hostname         String                     myDomain.centralus.cloudapp.azure.com
    DeploymentDebugLogLevel :

> [!NOTE]
> <span data-ttu-id="d0052-122">You can also deploy templates and parameters from local files.</span><span class="sxs-lookup"><span data-stu-id="d0052-122">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="d0052-123">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="d0052-123">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0052-124">Next Steps</span><span class="sxs-lookup"><span data-stu-id="d0052-124">Next Steps</span></span>

- <span data-ttu-id="d0052-125">If there were issues with the deployment, a next step would be to look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="d0052-125">If there were issues with the deployment, a next step would be to look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="d0052-126">Learn how to use Azure PowerShell to create a virtual machine from [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0052-126">Learn how to use Azure PowerShell to create a virtual machine from [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="d0052-127">Learn how to manage the virtual machine that you created by reviewing [Manage virtual machines using Azure Resource Manager and PowerShell](ps-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d0052-127">Learn how to manage the virtual machine that you created by reviewing [Manage virtual machines using Azure Resource Manager and PowerShell](ps-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

