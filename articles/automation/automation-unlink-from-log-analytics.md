---
title: Unlink Azure Automation account from Log Analytics | Microsoft Docs
description: This article provides an overview of how to unlink your Azure Automation account from an OMS workspace.
services: automation
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 06439c6e743f01c81881104c0efd4c15a3ddc643
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564050"
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="08b07-103">How to unlink your Automation account from a Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="08b07-103">How to unlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="08b07-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="08b07-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="08b07-105">Update Management</span><span class="sxs-lookup"><span data-stu-id="08b07-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="08b07-106">Change Tracking</span><span class="sxs-lookup"><span data-stu-id="08b07-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="08b07-107">Start/Stop VMs during off-hours</span><span class="sxs-lookup"><span data-stu-id="08b07-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="08b07-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="08b07-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span></span>  <span data-ttu-id="08b07-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span><span class="sxs-lookup"><span data-stu-id="08b07-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="08b07-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span><span class="sxs-lookup"><span data-stu-id="08b07-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span></span>  

<span data-ttu-id="08b07-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span><span class="sxs-lookup"><span data-stu-id="08b07-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="08b07-112">Unlink workspace</span><span class="sxs-lookup"><span data-stu-id="08b07-112">Unlink workspace</span></span>

1. <span data-ttu-id="08b07-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span><span class="sxs-lookup"><span data-stu-id="08b07-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="08b07-114">![Unlink workspace option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="08b07-114">![Unlink workspace option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="08b07-115">On the Unlink workspace blade, click **Unlink worksapce**.</span><span class="sxs-lookup"><span data-stu-id="08b07-115">On the Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="08b07-116">![Unlink workspace blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="08b07-116">![Unlink workspace blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="08b07-117">You will receive a prompt verifying you wish to proceed.</span><span class="sxs-lookup"><span data-stu-id="08b07-117">You will receive a prompt verifying you wish to proceed.</span></span><br><br>
3. <span data-ttu-id="08b07-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="08b07-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="08b07-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span><span class="sxs-lookup"><span data-stu-id="08b07-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="08b07-120">Update schedules.</span><span class="sxs-lookup"><span data-stu-id="08b07-120">Update schedules.</span></span>  <span data-ttu-id="08b07-121">Each will have names that match the update deployments you created)</span><span class="sxs-lookup"><span data-stu-id="08b07-121">Each will have names that match the update deployments you created)</span></span>

* <span data-ttu-id="08b07-122">Hybrid worker groups created for the solution.</span><span class="sxs-lookup"><span data-stu-id="08b07-122">Hybrid worker groups created for the solution.</span></span>  <span data-ttu-id="08b07-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="08b07-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="08b07-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span><span class="sxs-lookup"><span data-stu-id="08b07-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="08b07-125">Start and stop VM runbook schedules</span><span class="sxs-lookup"><span data-stu-id="08b07-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="08b07-126">Start and stop VM runbooks</span><span class="sxs-lookup"><span data-stu-id="08b07-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="08b07-127">Variables</span><span class="sxs-lookup"><span data-stu-id="08b07-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="08b07-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="08b07-128">Next steps</span></span>

<span data-ttu-id="08b07-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="08b07-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 

