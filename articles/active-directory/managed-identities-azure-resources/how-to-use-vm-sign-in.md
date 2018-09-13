---
title: How to use managed identities for Azure resources on an Azure VM for sign in
description: Step by step instructions and examples for using an Azure VM managed identities for Azure resources service principal for script client sign in and resource access.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/01/2017
ms.author: daveba
ms.openlocfilehash: 0f8789d64b550d9f0a45aa65728fbc1db64d6def
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968523"
---
# <a name="how-to-use-managed-identities-for-azure-resources-on-an-azure-vm-for-sign-in"></a><span data-ttu-id="89a3a-103">How to use managed identities for Azure resources on an Azure VM for sign in</span><span class="sxs-lookup"><span data-stu-id="89a3a-103">How to use managed identities for Azure resources on an Azure VM for sign in</span></span> 

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]  
<span data-ttu-id="89a3a-104">This article provides PowerShell and CLI script examples for sign-in using managed identities for Azure resources service principal, and guidance on important topics such as error handling.</span><span class="sxs-lookup"><span data-stu-id="89a3a-104">This article provides PowerShell and CLI script examples for sign-in using managed identities for Azure resources service principal, and guidance on important topics such as error handling.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89a3a-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="89a3a-105">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

<span data-ttu-id="89a3a-106">If you plan to use the Azure PowerShell or Azure CLI examples in this article, be sure to install the latest version of [Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="89a3a-106">If you plan to use the Azure PowerShell or Azure CLI examples in this article, be sure to install the latest version of [Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

> [!IMPORTANT]
> - <span data-ttu-id="89a3a-107">All sample script in this article assumes the command-line client is running on a VM with managed identities for Azure resources enabled.</span><span class="sxs-lookup"><span data-stu-id="89a3a-107">All sample script in this article assumes the command-line client is running on a VM with managed identities for Azure resources enabled.</span></span> <span data-ttu-id="89a3a-108">Use the VM "Connect" feature in the Azure portal, to remotely connect to your VM.</span><span class="sxs-lookup"><span data-stu-id="89a3a-108">Use the VM "Connect" feature in the Azure portal, to remotely connect to your VM.</span></span> <span data-ttu-id="89a3a-109">For details on enabling managed identities for Azure resources on a VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md), or one of the variant articles (using PowerShell, CLI, a template, or an Azure SDK).</span><span class="sxs-lookup"><span data-stu-id="89a3a-109">For details on enabling managed identities for Azure resources on a VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md), or one of the variant articles (using PowerShell, CLI, a template, or an Azure SDK).</span></span> 
> - <span data-ttu-id="89a3a-110">To prevent errors during resource access, the VM's managed identity must be given at least "Reader" access at the appropriate scope (the VM or higher) to allow Azure Resource Manager operations on the VM.</span><span class="sxs-lookup"><span data-stu-id="89a3a-110">To prevent errors during resource access, the VM's managed identity must be given at least "Reader" access at the appropriate scope (the VM or higher) to allow Azure Resource Manager operations on the VM.</span></span> <span data-ttu-id="89a3a-111">See [Assign managed identities for Azure resources access to a resource using the Azure portal](howto-assign-access-portal.md) for details.</span><span class="sxs-lookup"><span data-stu-id="89a3a-111">See [Assign managed identities for Azure resources access to a resource using the Azure portal](howto-assign-access-portal.md) for details.</span></span>

## <a name="overview"></a><span data-ttu-id="89a3a-112">Overview</span><span class="sxs-lookup"><span data-stu-id="89a3a-112">Overview</span></span>

<span data-ttu-id="89a3a-113">Managed identities for Azure resources provides a [service principal object](../develop/developer-glossary.md#service-principal-object) , which is [created upon enabling managed identities for Azure resources](overview.md#how-does-it-work) on the VM.</span><span class="sxs-lookup"><span data-stu-id="89a3a-113">Managed identities for Azure resources provides a [service principal object](../develop/developer-glossary.md#service-principal-object) , which is [created upon enabling managed identities for Azure resources](overview.md#how-does-it-work) on the VM.</span></span> <span data-ttu-id="89a3a-114">The service principal can be given access to Azure resources, and used as an identity by script/command-line clients for sign in and resource access.</span><span class="sxs-lookup"><span data-stu-id="89a3a-114">The service principal can be given access to Azure resources, and used as an identity by script/command-line clients for sign in and resource access.</span></span> <span data-ttu-id="89a3a-115">Traditionally, in order to access secured resources under its own identity, a script client would need to:</span><span class="sxs-lookup"><span data-stu-id="89a3a-115">Traditionally, in order to access secured resources under its own identity, a script client would need to:</span></span>  

   - <span data-ttu-id="89a3a-116">be registered and consented with Azure AD as a confidential/web client application</span><span class="sxs-lookup"><span data-stu-id="89a3a-116">be registered and consented with Azure AD as a confidential/web client application</span></span>
   - <span data-ttu-id="89a3a-117">sign in under its service principal, using the app's credentials (which are likely embedded in the script)</span><span class="sxs-lookup"><span data-stu-id="89a3a-117">sign in under its service principal, using the app's credentials (which are likely embedded in the script)</span></span>

<span data-ttu-id="89a3a-118">With managed identities for Azure resources, your script client no longer needs to do either, as it can sign in under the managed identities for Azure resources service principal.</span><span class="sxs-lookup"><span data-stu-id="89a3a-118">With managed identities for Azure resources, your script client no longer needs to do either, as it can sign in under the managed identities for Azure resources service principal.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="89a3a-119">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="89a3a-119">Azure CLI</span></span>

<span data-ttu-id="89a3a-120">The following script demonstrates how to:</span><span class="sxs-lookup"><span data-stu-id="89a3a-120">The following script demonstrates how to:</span></span>

1. <span data-ttu-id="89a3a-121">Sign in to Azure AD under the VM's managed identity for Azure resources service principal</span><span class="sxs-lookup"><span data-stu-id="89a3a-121">Sign in to Azure AD under the VM's managed identity for Azure resources service principal</span></span>  
2. <span data-ttu-id="89a3a-122">Call Azure Resource Manager and get the VM's service principal ID.</span><span class="sxs-lookup"><span data-stu-id="89a3a-122">Call Azure Resource Manager and get the VM's service principal ID.</span></span> <span data-ttu-id="89a3a-123">CLI takes care of managing token acquisition/use for you automatically.</span><span class="sxs-lookup"><span data-stu-id="89a3a-123">CLI takes care of managing token acquisition/use for you automatically.</span></span> <span data-ttu-id="89a3a-124">Be sure to substitute your virtual machine name for `<VM-NAME>`.</span><span class="sxs-lookup"><span data-stu-id="89a3a-124">Be sure to substitute your virtual machine name for `<VM-NAME>`.</span></span>  

   ```azurecli
   az login --identity
   
   spID=$(az resource list -n <VM-NAME> --query [*].identity.principalId --out tsv)
   echo The managed identity for Azure resources service principal ID is $spID
   ```

## <a name="azure-powershell"></a><span data-ttu-id="89a3a-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89a3a-125">Azure PowerShell</span></span>

<span data-ttu-id="89a3a-126">The following script demonstrates how to:</span><span class="sxs-lookup"><span data-stu-id="89a3a-126">The following script demonstrates how to:</span></span>

1. <span data-ttu-id="89a3a-127">Sign in to Azure AD under the VM's managed identity for Azure resources service principal</span><span class="sxs-lookup"><span data-stu-id="89a3a-127">Sign in to Azure AD under the VM's managed identity for Azure resources service principal</span></span>  
2. <span data-ttu-id="89a3a-128">Call an Azure Resource Manager cmdlet to get information about the VM.</span><span class="sxs-lookup"><span data-stu-id="89a3a-128">Call an Azure Resource Manager cmdlet to get information about the VM.</span></span> <span data-ttu-id="89a3a-129">PowerShell takes care of managing token use for you automatically.</span><span class="sxs-lookup"><span data-stu-id="89a3a-129">PowerShell takes care of managing token use for you automatically.</span></span>  

   ```azurepowershell
   Add-AzureRmAccount -identity

   # Call Azure Resource Manager to get the service principal ID for the VM's managed identity for Azure resources. 
   $vmInfoPs = Get-AzureRMVM -ResourceGroupName <RESOURCE-GROUP> -Name <VM-NAME>
   $spID = $vmInfoPs.Identity.PrincipalId
   echo "The managed identity for Azure resources service principal ID is $spID"
   ```

## <a name="resource-ids-for-azure-services"></a><span data-ttu-id="89a3a-130">Resource IDs for Azure services</span><span class="sxs-lookup"><span data-stu-id="89a3a-130">Resource IDs for Azure services</span></span>

<span data-ttu-id="89a3a-131">See [Azure services that support Azure AD authentication](services-support-msi.md#azure-services-that-support-azure-ad-authentication) for a list of resources that support Azure AD and have been tested with managed identities for Azure resources, and their respective resource IDs.</span><span class="sxs-lookup"><span data-stu-id="89a3a-131">See [Azure services that support Azure AD authentication](services-support-msi.md#azure-services-that-support-azure-ad-authentication) for a list of resources that support Azure AD and have been tested with managed identities for Azure resources, and their respective resource IDs.</span></span>

## <a name="error-handling-guidance"></a><span data-ttu-id="89a3a-132">Error handling guidance</span><span class="sxs-lookup"><span data-stu-id="89a3a-132">Error handling guidance</span></span> 

<span data-ttu-id="89a3a-133">Responses such as the following may indicate that the VM's managed identity for Azure resources has not been correctly configured:</span><span class="sxs-lookup"><span data-stu-id="89a3a-133">Responses such as the following may indicate that the VM's managed identity for Azure resources has not been correctly configured:</span></span>

- <span data-ttu-id="89a3a-134">PowerShell: *Invoke-WebRequest : Unable to connect to the remote server*</span><span class="sxs-lookup"><span data-stu-id="89a3a-134">PowerShell: *Invoke-WebRequest : Unable to connect to the remote server*</span></span>
- <span data-ttu-id="89a3a-135">CLI: *MSI: Failed to retrieve a token from 'http://localhost:50342/oauth2/token' with an error of 'HTTPConnectionPool(host='localhost', port=50342)*</span><span class="sxs-lookup"><span data-stu-id="89a3a-135">CLI: *MSI: Failed to retrieve a token from 'http://localhost:50342/oauth2/token' with an error of 'HTTPConnectionPool(host='localhost', port=50342)*</span></span> 

<span data-ttu-id="89a3a-136">If you receive one of these errors, return to the Azure VM in the [Azure portal](https://portal.azure.com) and:</span><span class="sxs-lookup"><span data-stu-id="89a3a-136">If you receive one of these errors, return to the Azure VM in the [Azure portal](https://portal.azure.com) and:</span></span>

- <span data-ttu-id="89a3a-137">Go to the **Identity** page and ensure **System assigned** is set to "Yes."</span><span class="sxs-lookup"><span data-stu-id="89a3a-137">Go to the **Identity** page and ensure **System assigned** is set to "Yes."</span></span>
- <span data-ttu-id="89a3a-138">Go to the **Extensions** page and ensure the managed identities for Azure resources extension **(planned for deprecation in January 2019)** deployed successfully.</span><span class="sxs-lookup"><span data-stu-id="89a3a-138">Go to the **Extensions** page and ensure the managed identities for Azure resources extension **(planned for deprecation in January 2019)** deployed successfully.</span></span>

<span data-ttu-id="89a3a-139">If either is incorrect, you may need to redeploy the managed identities for Azure resources on your resource again, or troubleshoot the deployment failure.</span><span class="sxs-lookup"><span data-stu-id="89a3a-139">If either is incorrect, you may need to redeploy the managed identities for Azure resources on your resource again, or troubleshoot the deployment failure.</span></span> <span data-ttu-id="89a3a-140">See [Configure Managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md) if you need assistance with VM configuration.</span><span class="sxs-lookup"><span data-stu-id="89a3a-140">See [Configure Managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md) if you need assistance with VM configuration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89a3a-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="89a3a-141">Next steps</span></span>

- <span data-ttu-id="89a3a-142">To enable managed identities for Azure resources on an Azure VM, see [Configure managed identities for Azure resources on an Azure VM using PowerShell](qs-configure-powershell-windows-vm.md), or [Configure managed identities for Azure resources on an Azure VM using Azure CLI](qs-configure-cli-windows-vm.md)</span><span class="sxs-lookup"><span data-stu-id="89a3a-142">To enable managed identities for Azure resources on an Azure VM, see [Configure managed identities for Azure resources on an Azure VM using PowerShell](qs-configure-powershell-windows-vm.md), or [Configure managed identities for Azure resources on an Azure VM using Azure CLI](qs-configure-cli-windows-vm.md)</span></span>






