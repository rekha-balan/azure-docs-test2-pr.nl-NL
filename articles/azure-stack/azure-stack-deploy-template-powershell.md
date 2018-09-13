---
title: Deploy templates with PowerShell in Azure Stack | Microsoft Docs
description: Learn how to deploy a virtual machine using a Resource Manager template and PowerShell.
services: azure-stack
documentationcenter: ''
author: heathl17
manager: byronr
editor: ''
ms.assetid: 12fe32d7-0a1a-4c02-835d-7b97f151ed0f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/3/2016
ms.author: helaw
ms.openlocfilehash: c5ac70a25e3b80a50c01464895c400f83d1d124d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563855"
---
# <a name="deploy-templates-in-azure-stack-using-powershell"></a><span data-ttu-id="4d46a-103">Deploy templates in Azure Stack using PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d46a-103">Deploy templates in Azure Stack using PowerShell</span></span>
<span data-ttu-id="4d46a-104">Use PowerShell to deploy Azure Resource Manager templates to the Azure Stack POC.</span><span class="sxs-lookup"><span data-stu-id="4d46a-104">Use PowerShell to deploy Azure Resource Manager templates to the Azure Stack POC.</span></span>  <span data-ttu-id="4d46a-105">Resource Manager templates deploy and provision all resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="4d46a-105">Resource Manager templates deploy and provision all resources for your application in a single, coordinated operation.</span></span>

## <a name="run-azurerm-powershell-cmdlets"></a><span data-ttu-id="4d46a-106">Run AzureRM PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="4d46a-106">Run AzureRM PowerShell cmdlets</span></span>
<span data-ttu-id="4d46a-107">In this example, you run a script to deploy a virtual machine to Azure Stack POC using a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="4d46a-107">In this example, you run a script to deploy a virtual machine to Azure Stack POC using a Resource Manager template.</span></span>  <span data-ttu-id="4d46a-108">Before proceeding, ensure you have [configured PowerShell](azure-stack-powershell-configure.md)</span><span class="sxs-lookup"><span data-stu-id="4d46a-108">Before proceeding, ensure you have [configured PowerShell](azure-stack-powershell-configure.md)</span></span>  

<span data-ttu-id="4d46a-109">The VHD used in this example template is WindowsServer-2012-R2-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="4d46a-109">The VHD used in this example template is WindowsServer-2012-R2-Datacenter.</span></span>

1. <span data-ttu-id="4d46a-110">Go to <http://aka.ms/AzureStackGitHub>, search for the **101-simple-windows-vm** template, and save it to the following location: c:\\templates\\azuredeploy-101-simple-windows-vm.json.</span><span class="sxs-lookup"><span data-stu-id="4d46a-110">Go to <http://aka.ms/AzureStackGitHub>, search for the **101-simple-windows-vm** template, and save it to the following location: c:\\templates\\azuredeploy-101-simple-windows-vm.json.</span></span>
2. <span data-ttu-id="4d46a-111">In PowerShell, run the following deployment script.</span><span class="sxs-lookup"><span data-stu-id="4d46a-111">In PowerShell, run the following deployment script.</span></span> <span data-ttu-id="4d46a-112">Replace *username* and *password* with your username and password.</span><span class="sxs-lookup"><span data-stu-id="4d46a-112">Replace *username* and *password* with your username and password.</span></span> <span data-ttu-id="4d46a-113">On subsequent uses, increment the value for the *$myNum* parameter to prevent overwriting your deployment.</span><span class="sxs-lookup"><span data-stu-id="4d46a-113">On subsequent uses, increment the value for the *$myNum* parameter to prevent overwriting your deployment.</span></span>
   
   ```PowerShell
       # Set Deployment Variables
       $myNum = "001" #Modify this per deployment
       $RGName = "myRG$myNum"
       $myLocation = "local"
   
       # Create Resource Group for Template Deployment
       New-AzureRmResourceGroup -Name $RGName -Location $myLocation
   
       # Deploy Simple IaaS Template
       New-AzureRmResourceGroupDeployment `
           -Name myDeployment$myNum `
           -ResourceGroupName $RGName `
           -TemplateFile c:\templates\azuredeploy-101-simple-windows-vm.json `
           -NewStorageAccountName mystorage$myNum `
           -DnsNameForPublicIP mydns$myNum `
           -AdminUsername <username> `
           -AdminPassword ("<password>" | ConvertTo-SecureString -AsPlainText -Force) `
           -VmName myVM$myNum `
           -WindowsOSVersion 2012-R2-Datacenter
   ```
3. <span data-ttu-id="4d46a-114">Open the Azure Stack portal, click **Browse**, click **Virtual machines**, and look for your new virtual machine (*myDeployment001*).</span><span class="sxs-lookup"><span data-stu-id="4d46a-114">Open the Azure Stack portal, click **Browse**, click **Virtual machines**, and look for your new virtual machine (*myDeployment001*).</span></span>

## <a name="video-example-hybrid-virtual-machine-deployment"></a><span data-ttu-id="4d46a-115">Video example: hybrid virtual machine deployment</span><span class="sxs-lookup"><span data-stu-id="4d46a-115">Video example: hybrid virtual machine deployment</span></span>
>[!VIDEO https://channel9.msdn.com/Blogs/azurestack/Microsoft-Azure-Stack-TP1-POC-Hybrid-VM-Deployment/player]


## <a name="next-steps"></a><span data-ttu-id="4d46a-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d46a-116">Next steps</span></span>
[<span data-ttu-id="4d46a-117">Deploy templates with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d46a-117">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

