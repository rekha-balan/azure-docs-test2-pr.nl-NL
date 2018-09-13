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
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="565d9-103">Managing Azure Virtual Machines using Azure Automation</span><span class="sxs-lookup"><span data-stu-id="565d9-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="565d9-104">This guide introduces you to the Azure Automation service and how it can be used to simplify managing your Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="565d9-104">This guide introduces you to the Azure Automation service and how it can be used to simplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="565d9-105">What is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="565d9-105">What is Azure Automation?</span></span>
<span data-ttu-id="565d9-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span><span class="sxs-lookup"><span data-stu-id="565d9-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="565d9-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time-to-value for your organization.</span><span class="sxs-lookup"><span data-stu-id="565d9-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="565d9-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales to meet your needs as your organization grows.</span><span class="sxs-lookup"><span data-stu-id="565d9-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="565d9-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span><span class="sxs-lookup"><span data-stu-id="565d9-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="565d9-110">You can lower operational overhead and free up IT and DevOps staff to focus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="565d9-110">You can lower operational overhead and free up IT and DevOps staff to focus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="565d9-111">How can Azure Automation help manage Azure virtual machines?</span><span class="sxs-lookup"><span data-stu-id="565d9-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="565d9-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="565d9-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="565d9-113">Azure Automation includes the Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within the service.</span><span class="sxs-lookup"><span data-stu-id="565d9-113">Azure Automation includes the Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within the service.</span></span> <span data-ttu-id="565d9-114">You can also pair the cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and third-party systems.</span><span class="sxs-lookup"><span data-stu-id="565d9-114">You can also pair the cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="565d9-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="565d9-115">Next steps</span></span>
<span data-ttu-id="565d9-116">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure virtual machines, learn more:</span><span class="sxs-lookup"><span data-stu-id="565d9-116">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="565d9-117">Azure Automation Overview</span><span class="sxs-lookup"><span data-stu-id="565d9-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="565d9-118">My first runbook</span><span class="sxs-lookup"><span data-stu-id="565d9-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="565d9-119">Azure Automation learning map</span><span class="sxs-lookup"><span data-stu-id="565d9-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

