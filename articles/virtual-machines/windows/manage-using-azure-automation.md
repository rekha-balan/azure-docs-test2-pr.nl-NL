---
title: Manage VMs using Azure Automation | Microsoft Docs
description: Learn about how the Azure Automation service can be used to manage Azure virtual machines at scale.
services: virtual-machines-windows, automation
documentationcenter: ''
author: jodoglevy
manager: timlt
editor: ''
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: 2cf12d20e80fff981cb7614c82ba5941de4a77ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548866"
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a>Managing Azure Virtual Machines using Azure Automation
This guide introduces you to the Azure Automation service and how it can be used to simplify managing your Azure virtual machines.

## <a name="what-is-azure-automation"></a>What is Azure Automation?
[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation. By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time-to-value for your organization.

Azure Automation provides a highly reliable and highly available workflow execution engine that scales to meet your needs as your organization grows. In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.

You can lower operational overhead and free up IT and DevOps staff to focus on work that adds business value by running your cloud management tasks automatically with Azure Automation.

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a>How can Azure Automation help manage Azure virtual machines?
Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx). Azure Automation includes the Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within the service. You can also pair the cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and third-party systems.

## <a name="next-steps"></a>Next steps
Now that you've learned the basics of Azure Automation and how it can be used to manage Azure virtual machines, learn more:

* [Azure Automation Overview](../../automation/automation-intro.md)
* [My first runbook](../../automation/automation-first-runbook-graphical.md)
* [Azure Automation learning map](https://azure.microsoft.com/documentation/learning-paths/automation/)

