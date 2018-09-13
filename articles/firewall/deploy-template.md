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
# <a name="deploy-azure-firewall-using-a-template"></a>Deploy Azure Firewall using a template

[!INCLUDE [firewall-preview-notice](../../includes/firewall-preview-notice.md)]

The examples in the Azure Firewall articles assume that you have already enabled the Azure Firewall public preview. For more information, see [Enable the Azure Firewall public preview](public-preview.md).

This template creates a firewall and a test network environment. The network has one VNet, with three subnets: *AzureFirewallSubnet*, *ServersSubnet*, and a *JumpboxSubnet*. The ServersSubnet and JumpboxSubnet each have one 2-core Windows Server in them.

The firewall is in the AzureFirewallSubnet and is configured with an Application Rule Collection with a single rule that allows access to www.microsoft.com.

A user defined route is created that points the network traffic from the ServersSubnet through the firewall, where the firewall rules are applied.

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

## <a name="template-location"></a>Template location

The template is located at:

[https://github.com/Azure/azure-quickstart-templates/tree/master/101-azurefirewall-sandbox](https://github.com/Azure/azure-quickstart-templates/tree/master/101-azurefirewall-sandbox)

Read the introduction, and when ready to deploy, click **Deploy to Azure**.

## <a name="clean-up-resources"></a>Clean up resources

First explore the resources that were created with the firewall, and then when no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, firewall, and all related resources.

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="next-steps"></a>Next steps

Next, you can monitor the Azure Firewall logs:

- [Tutorial: Monitor Azure Firewall logs](./tutorial-diagnostics.md)

