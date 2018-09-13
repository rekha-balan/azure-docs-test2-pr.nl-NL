---
title: Manage Azure Web App using Azure Automation | Microsoft Docs
description: Learn about how the Azure Automation service can be used to manage Azure Web App.
services: app-service\web, automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: ''
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 4fcfa2e7ec2e8257407026ed4cca0e15fd0b5bb6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556392"
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="68f1a-103">Managing Azure Web App using Azure Automation</span><span class="sxs-lookup"><span data-stu-id="68f1a-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="68f1a-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure Web App.</span><span class="sxs-lookup"><span data-stu-id="68f1a-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="68f1a-105">What is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="68f1a-105">What is Azure Automation?</span></span>
<span data-ttu-id="68f1a-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span><span class="sxs-lookup"><span data-stu-id="68f1a-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="68f1a-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span><span class="sxs-lookup"><span data-stu-id="68f1a-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="68f1a-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="68f1a-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="68f1a-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span><span class="sxs-lookup"><span data-stu-id="68f1a-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="68f1a-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="68f1a-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="68f1a-111">How can Azure Automation help manage Azure Web App?</span><span class="sxs-lookup"><span data-stu-id="68f1a-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="68f1a-112">Web App can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="68f1a-112">Web App can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="68f1a-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within the service.</span><span class="sxs-lookup"><span data-stu-id="68f1a-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within the service.</span></span> <span data-ttu-id="68f1a-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services to automate complex tasks across Azure services and 3rd party systems.</span><span class="sxs-lookup"><span data-stu-id="68f1a-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="68f1a-115">Here are some examples of managing App Services with Automation:</span><span class="sxs-lookup"><span data-stu-id="68f1a-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="68f1a-116">Scripts for managing Web Apps</span><span class="sxs-lookup"><span data-stu-id="68f1a-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="68f1a-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="68f1a-117">Next steps</span></span>
<span data-ttu-id="68f1a-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Web App, follow these links to learn more about Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="68f1a-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Web App, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="68f1a-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="68f1a-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

