---
title: Manage Azure RemoteApp using Azure Automation | Microsoft Docs
description: Learn about how the Azure Automation service can be used to manage Azure RemoteApp.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: ''
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: 59ac11f153c0bd74a1106400dbbf5790968b657c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662595"
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="d5794-103">Managing Azure RemoteApp using Azure Automation</span><span class="sxs-lookup"><span data-stu-id="d5794-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d5794-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="d5794-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d5794-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="d5794-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d5794-106">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d5794-106">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="d5794-107">What is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="d5794-107">What is Azure Automation?</span></span>
<span data-ttu-id="d5794-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span><span class="sxs-lookup"><span data-stu-id="d5794-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="d5794-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span><span class="sxs-lookup"><span data-stu-id="d5794-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="d5794-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="d5794-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="d5794-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span><span class="sxs-lookup"><span data-stu-id="d5794-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="d5794-112">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="d5794-112">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="d5794-113">How can Azure Automation help manage Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="d5794-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="d5794-114">RemoteApp can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5794-114">RemoteApp can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="d5794-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of the box, so that you can perform all of your RemoteApp management tasks within the service.</span><span class="sxs-lookup"><span data-stu-id="d5794-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of the box, so that you can perform all of your RemoteApp management tasks within the service.</span></span> <span data-ttu-id="d5794-116">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span><span class="sxs-lookup"><span data-stu-id="d5794-116">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5794-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5794-117">Next steps</span></span>
<span data-ttu-id="d5794-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure RemoteApp, follow these links to learn more about Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="d5794-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure RemoteApp, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="d5794-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="d5794-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

