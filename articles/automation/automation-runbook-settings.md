---
title: Runbook settings | Microsoft Docs
description: Describes the configuration settings for a runbook in Azure Automation and how to change them using both the Azure Management Portal and Windows PowerShell.
services: automation
documentationcenter: ''
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 20ecbc270e61d234e026e6ba2634c7aad63b3355
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552851"
---
# <a name="runbook-settings"></a><span data-ttu-id="8499b-103">Runbook settings</span><span class="sxs-lookup"><span data-stu-id="8499b-103">Runbook settings</span></span>
<span data-ttu-id="8499b-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span><span class="sxs-lookup"><span data-stu-id="8499b-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span></span> <span data-ttu-id="8499b-105">Each of these settings is described below followed by procedures on how to modify them.</span><span class="sxs-lookup"><span data-stu-id="8499b-105">Each of these settings is described below followed by procedures on how to modify them.</span></span>

## <a name="settings"></a><span data-ttu-id="8499b-106">Settings</span><span class="sxs-lookup"><span data-stu-id="8499b-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="8499b-107">Name and description</span><span class="sxs-lookup"><span data-stu-id="8499b-107">Name and description</span></span>
<span data-ttu-id="8499b-108">You cannot change the name of a runbook after it has been created.</span><span class="sxs-lookup"><span data-stu-id="8499b-108">You cannot change the name of a runbook after it has been created.</span></span> <span data-ttu-id="8499b-109">The Description is optional and can be up to 512 characters.</span><span class="sxs-lookup"><span data-stu-id="8499b-109">The Description is optional and can be up to 512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="8499b-110">Tags</span><span class="sxs-lookup"><span data-stu-id="8499b-110">Tags</span></span>
<span data-ttu-id="8499b-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span><span class="sxs-lookup"><span data-stu-id="8499b-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span></span> <span data-ttu-id="8499b-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span><span class="sxs-lookup"><span data-stu-id="8499b-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span></span> <span data-ttu-id="8499b-113">You can specify multiple tags for a runbook by separating them with commas.</span><span class="sxs-lookup"><span data-stu-id="8499b-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="8499b-114">Logging</span><span class="sxs-lookup"><span data-stu-id="8499b-114">Logging</span></span>
<span data-ttu-id="8499b-115">By default, Verbose and Progress records are not written to job history.</span><span class="sxs-lookup"><span data-stu-id="8499b-115">By default, Verbose and Progress records are not written to job history.</span></span> <span data-ttu-id="8499b-116">You can change the settings for a particular runbook to log these records.</span><span class="sxs-lookup"><span data-stu-id="8499b-116">You can change the settings for a particular runbook to log these records.</span></span> <span data-ttu-id="8499b-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="8499b-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="8499b-118">Changing runbook settings</span><span class="sxs-lookup"><span data-stu-id="8499b-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-the-azure-portal"></a><span data-ttu-id="8499b-119">Changing runbook settings with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8499b-119">Changing runbook settings with the Azure portal</span></span>
<span data-ttu-id="8499b-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span><span class="sxs-lookup"><span data-stu-id="8499b-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span></span>

1. <span data-ttu-id="8499b-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span><span class="sxs-lookup"><span data-stu-id="8499b-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="8499b-122">Select the **Runbooks** tab.</span><span class="sxs-lookup"><span data-stu-id="8499b-122">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="8499b-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span><span class="sxs-lookup"><span data-stu-id="8499b-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span></span> <span data-ttu-id="8499b-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span><span class="sxs-lookup"><span data-stu-id="8499b-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="8499b-125">Changing runbook settings with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8499b-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="8499b-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span><span class="sxs-lookup"><span data-stu-id="8499b-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span></span> <span data-ttu-id="8499b-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span><span class="sxs-lookup"><span data-stu-id="8499b-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span></span> <span data-ttu-id="8499b-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="8499b-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="8499b-129">The following sample commands show how to set the properties for a runbook.</span><span class="sxs-lookup"><span data-stu-id="8499b-129">The following sample commands show how to set the properties for a runbook.</span></span> <span data-ttu-id="8499b-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span><span class="sxs-lookup"><span data-stu-id="8499b-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="8499b-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="8499b-131">Next steps</span></span>
* <span data-ttu-id="8499b-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="8499b-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="8499b-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="8499b-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

