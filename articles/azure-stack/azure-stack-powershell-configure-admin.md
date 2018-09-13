---
title: Connect to Azure Stack with PowerShell as an operator | Microsoft Docs
description: Learn how to connect to Azure Stack with PowerShell as an operator
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: article
ms.date: 09/07/2018
ms.author: mabrigg
ms.reviewer: thoroet
ms.openlocfilehash: e6e1ffdf4384080649a769b2fdf6877ea744ec51
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967613"
---
# <a name="connect-to-azure-stack-with-powershell-as-an-operator"></a><span data-ttu-id="b21ad-103">Connect to Azure Stack with PowerShell as an operator</span><span class="sxs-lookup"><span data-stu-id="b21ad-103">Connect to Azure Stack with PowerShell as an operator</span></span>

<span data-ttu-id="b21ad-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="b21ad-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="b21ad-105">You can configure the Azure Stack to use PowerShell to manage resources such as creating offers, plans, quotas, and alerts.</span><span class="sxs-lookup"><span data-stu-id="b21ad-105">You can configure the Azure Stack to use PowerShell to manage resources such as creating offers, plans, quotas, and alerts.</span></span> <span data-ttu-id="b21ad-106">This topic helps you configure the operator environment.</span><span class="sxs-lookup"><span data-stu-id="b21ad-106">This topic helps you configure the operator environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b21ad-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b21ad-107">Prerequisites</span></span>

<span data-ttu-id="b21ad-108">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span><span class="sxs-lookup"><span data-stu-id="b21ad-108">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn).</span></span> 

 - <span data-ttu-id="b21ad-109">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="b21ad-109">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
 - <span data-ttu-id="b21ad-110">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="b21ad-110">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

## <a name="configure-the-operator-environment-and-sign-in-to-azure-stack"></a><span data-ttu-id="b21ad-111">Configure the operator environment and sign in to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b21ad-111">Configure the operator environment and sign in to Azure Stack</span></span>

<span data-ttu-id="b21ad-112">Configure the Azure Stack operator environment with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b21ad-112">Configure the Azure Stack operator environment with PowerShell.</span></span> <span data-ttu-id="b21ad-113">Run one of the following scripts: Replace the Azure AD tenantName, GraphAudience endpoint, and ArmEndpoint values with your own environment configuration.</span><span class="sxs-lookup"><span data-stu-id="b21ad-113">Run one of the following scripts: Replace the Azure AD tenantName, GraphAudience endpoint, and ArmEndpoint values with your own environment configuration.</span></span>

````PowerShell  
    # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external.
    # To get this value for Azure Stack integrated systems, contact your service provider.
    $ArmEndpoint = "<Admin Resource Manager endpoint for your environment>"

    # Register an AzureRM environment that targets your Azure Stack instance
    Add-AzureRMEnvironment `
        -Name "AzureStackAdmin" -ArmEndpoint $ArmEndpoint

    # After signing in to your environment, Azure Stack cmdlets
    # can be easily targeted at your Azure Stack instance.
    Add-AzureRmAccount -EnvironmentName "AzureStackAdmin"
````

## <a name="test-the-connectivity"></a><span data-ttu-id="b21ad-114">Test the connectivity</span><span class="sxs-lookup"><span data-stu-id="b21ad-114">Test the connectivity</span></span>

<span data-ttu-id="b21ad-115">Now that you've got everything set-up, use PowerShell to create resources within Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b21ad-115">Now that you've got everything set-up, use PowerShell to create resources within Azure Stack.</span></span> <span data-ttu-id="b21ad-116">For example, you can create a resource group for an application and add a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b21ad-116">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="b21ad-117">Use the following command to create a resource group named **MyResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="b21ad-117">Use the following command to create a resource group named **MyResourceGroup**.</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="b21ad-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="b21ad-118">Next steps</span></span>

 - [<span data-ttu-id="b21ad-119">Develop templates for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b21ad-119">Develop templates for Azure Stack</span></span>](user/azure-stack-develop-templates.md)
 - [<span data-ttu-id="b21ad-120">Deploy templates with PowerShell</span><span class="sxs-lookup"><span data-stu-id="b21ad-120">Deploy templates with PowerShell</span></span>](user/azure-stack-deploy-template-powershell.md)
