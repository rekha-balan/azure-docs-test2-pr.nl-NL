---
title: Deploy Azure Firewall using a template
description: Deploy Azure Firewall using a template
services: firewall
author: vhorne
manager: jpconnock
ms.service: firewall
ms.topic: article
ms.date: 7/11/2018
ms.author: victorh
ms.openlocfilehash: 1a732e22d72c36afe11030e42bae529baa35df1a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856720"
---
# <a name="deploy-azure-firewall-using-a-template"></a><span data-ttu-id="c65f9-103">Deploy Azure Firewall using a template</span><span class="sxs-lookup"><span data-stu-id="c65f9-103">Deploy Azure Firewall using a template</span></span>

[!INCLUDE [firewall-preview-notice](../../includes/firewall-preview-notice.md)]

<span data-ttu-id="c65f9-104">The examples in the Azure Firewall articles assume that you have already enabled the Azure Firewall public preview.</span><span class="sxs-lookup"><span data-stu-id="c65f9-104">The examples in the Azure Firewall articles assume that you have already enabled the Azure Firewall public preview.</span></span> <span data-ttu-id="c65f9-105">For more information, see [Enable the Azure Firewall public preview](public-preview.md).</span><span class="sxs-lookup"><span data-stu-id="c65f9-105">For more information, see [Enable the Azure Firewall public preview](public-preview.md).</span></span>

<span data-ttu-id="c65f9-106">This template creates a firewall and a test network environment.</span><span class="sxs-lookup"><span data-stu-id="c65f9-106">This template creates a firewall and a test network environment.</span></span> <span data-ttu-id="c65f9-107">The network has one VNet, with three subnets: *AzureFirewallSubnet*, *ServersSubnet*, and a *JumpboxSubnet*.</span><span class="sxs-lookup"><span data-stu-id="c65f9-107">The network has one VNet, with three subnets: *AzureFirewallSubnet*, *ServersSubnet*, and a *JumpboxSubnet*.</span></span> <span data-ttu-id="c65f9-108">The ServersSubnet and JumpboxSubnet each have one 2-core Windows Server in them.</span><span class="sxs-lookup"><span data-stu-id="c65f9-108">The ServersSubnet and JumpboxSubnet each have one 2-core Windows Server in them.</span></span>

<span data-ttu-id="c65f9-109">The firewall is in the AzureFirewallSubnet and is configured with an Application Rule Collection with a single rule that allows access to www.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="c65f9-109">The firewall is in the AzureFirewallSubnet and is configured with an Application Rule Collection with a single rule that allows access to www.microsoft.com.</span></span>

<span data-ttu-id="c65f9-110">A user defined route is created that points the network traffic from the ServersSubnet through the firewall, where the firewall rules are applied.</span><span class="sxs-lookup"><span data-stu-id="c65f9-110">A user defined route is created that points the network traffic from the ServersSubnet through the firewall, where the firewall rules are applied.</span></span>

<span data-ttu-id="c65f9-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="c65f9-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="template-location"></a><span data-ttu-id="c65f9-112">Template location</span><span class="sxs-lookup"><span data-stu-id="c65f9-112">Template location</span></span>

<span data-ttu-id="c65f9-113">The template is located at:</span><span class="sxs-lookup"><span data-stu-id="c65f9-113">The template is located at:</span></span>

[https://github.com/Azure/azure-quickstart-templates/tree/master/101-azurefirewall-sandbox](https://github.com/Azure/azure-quickstart-templates/tree/master/101-azurefirewall-sandbox)

<span data-ttu-id="c65f9-114">Read the introduction, and when ready to deploy, click **Deploy to Azure**.</span><span class="sxs-lookup"><span data-stu-id="c65f9-114">Read the introduction, and when ready to deploy, click **Deploy to Azure**.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="c65f9-115">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="c65f9-115">Clean up resources</span></span>

<span data-ttu-id="c65f9-116">First explore the resources that were created with the firewall, and then when no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, firewall, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="c65f9-116">First explore the resources that were created with the firewall, and then when no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, firewall, and all related resources.</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="next-steps"></a><span data-ttu-id="c65f9-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="c65f9-117">Next steps</span></span>

<span data-ttu-id="c65f9-118">Next, you can monitor the Azure Firewall logs:</span><span class="sxs-lookup"><span data-stu-id="c65f9-118">Next, you can monitor the Azure Firewall logs:</span></span>

- [<span data-ttu-id="c65f9-119">Tutorial: Monitor Azure Firewall logs</span><span class="sxs-lookup"><span data-stu-id="c65f9-119">Tutorial: Monitor Azure Firewall logs</span></span>](./tutorial-diagnostics.md)

