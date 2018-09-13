---
title: Troubleshooting issues with Azure Automation Desired State Configuration (DSC)
description: This article provides information on troubleshooting Desired State Configuration (DSC)
services: automation
ms.service: automation
ms.component: ''
author: georgewallace
ms.author: gwallace
ms.date: 06/19/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 5d2eae67fcff74a7016f7f6125e31a9c8c2bda97
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869030"
---
# <a name="troubleshoot-desired-state-configuration-dsc"></a><span data-ttu-id="7e71b-103">Troubleshoot Desired State Configuration (DSC)</span><span class="sxs-lookup"><span data-stu-id="7e71b-103">Troubleshoot Desired State Configuration (DSC)</span></span>

<span data-ttu-id="7e71b-104">This article provides information on troubleshooting issues with Desired State Configuration (DSC).</span><span class="sxs-lookup"><span data-stu-id="7e71b-104">This article provides information on troubleshooting issues with Desired State Configuration (DSC).</span></span>

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a><span data-ttu-id="7e71b-105">Common errors when working with Desired State Configuration (DSC)</span><span class="sxs-lookup"><span data-stu-id="7e71b-105">Common errors when working with Desired State Configuration (DSC)</span></span>

### <a name="failed-not-found"></a><span data-ttu-id="7e71b-106">Scenario: Node is in failed status with a "Not found" error</span><span class="sxs-lookup"><span data-stu-id="7e71b-106">Scenario: Node is in failed status with a "Not found" error</span></span>

#### <a name="issue"></a><span data-ttu-id="7e71b-107">Issue</span><span class="sxs-lookup"><span data-stu-id="7e71b-107">Issue</span></span>

<span data-ttu-id="7e71b-108">The node has a report with **Failed** status and containing the error:</span><span class="sxs-lookup"><span data-stu-id="7e71b-108">The node has a report with **Failed** status and containing the error:</span></span>

```
The attempt to get the action from server https://<url>//accounts/<account-id>/Nodes(AgentId=<agent-id>)/GetDscAction failed because a valid configuration <guid> cannot be found.
```

#### <a name="cause"></a><span data-ttu-id="7e71b-109">Cause</span><span class="sxs-lookup"><span data-stu-id="7e71b-109">Cause</span></span>

<span data-ttu-id="7e71b-110">This error typically occurs when the node is assigned to a configuration name (for example, ABC) instead of a node configuration name (for example, ABC.WebServer).</span><span class="sxs-lookup"><span data-stu-id="7e71b-110">This error typically occurs when the node is assigned to a configuration name (for example, ABC) instead of a node configuration name (for example, ABC.WebServer).</span></span>

#### <a name="resolution"></a><span data-ttu-id="7e71b-111">Resolution</span><span class="sxs-lookup"><span data-stu-id="7e71b-111">Resolution</span></span>

* <span data-ttu-id="7e71b-112">Make sure that you are assigning the node with "node configuration name" and not the "configuration name".</span><span class="sxs-lookup"><span data-stu-id="7e71b-112">Make sure that you are assigning the node with "node configuration name" and not the "configuration name".</span></span>
* <span data-ttu-id="7e71b-113">You can assign a node configuration to a node using Azure portal or with a PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7e71b-113">You can assign a node configuration to a node using Azure portal or with a PowerShell cmdlet.</span></span>

  * <span data-ttu-id="7e71b-114">In order to assign a node configuration to a node using Azure portal, open the **DSC Nodes** page, then select a node and click on **Assign node configuration** button.</span><span class="sxs-lookup"><span data-stu-id="7e71b-114">In order to assign a node configuration to a node using Azure portal, open the **DSC Nodes** page, then select a node and click on **Assign node configuration** button.</span></span>  
  * <span data-ttu-id="7e71b-115">In order to assign a node configuration to a node using PowerShell cmdlet, use **Set-AzureRmAutomationDscNode** cmdlet</span><span class="sxs-lookup"><span data-stu-id="7e71b-115">In order to assign a node configuration to a node using PowerShell cmdlet, use **Set-AzureRmAutomationDscNode** cmdlet</span></span>

### <a name="no-mof-files"></a><span data-ttu-id="7e71b-116">Scenario: No node configurations (MOF files) were produced when a configuration is compiled</span><span class="sxs-lookup"><span data-stu-id="7e71b-116">Scenario: No node configurations (MOF files) were produced when a configuration is compiled</span></span>

#### <a name="issue"></a><span data-ttu-id="7e71b-117">Issue</span><span class="sxs-lookup"><span data-stu-id="7e71b-117">Issue</span></span>

<span data-ttu-id="7e71b-118">Your DSC compilation job suspends with the error:</span><span class="sxs-lookup"><span data-stu-id="7e71b-118">Your DSC compilation job suspends with the error:</span></span>

```
Compilation completed successfully, but no node configuration.mofs were generated.
```

#### <a name="cause"></a><span data-ttu-id="7e71b-119">Cause</span><span class="sxs-lookup"><span data-stu-id="7e71b-119">Cause</span></span>

<span data-ttu-id="7e71b-120">When the expression following the **Node** keyword in the DSC configuration evaluates to `$null`, then no node configurations are produced.</span><span class="sxs-lookup"><span data-stu-id="7e71b-120">When the expression following the **Node** keyword in the DSC configuration evaluates to `$null`, then no node configurations are produced.</span></span>

#### <a name="resolution"></a><span data-ttu-id="7e71b-121">Resolution</span><span class="sxs-lookup"><span data-stu-id="7e71b-121">Resolution</span></span>

<span data-ttu-id="7e71b-122">Any of the following solutions fix the problem:</span><span class="sxs-lookup"><span data-stu-id="7e71b-122">Any of the following solutions fix the problem:</span></span>

* <span data-ttu-id="7e71b-123">Make sure that the expression next to the **Node** keyword in the configuration definition is not evaluating to $null.</span><span class="sxs-lookup"><span data-stu-id="7e71b-123">Make sure that the expression next to the **Node** keyword in the configuration definition is not evaluating to $null.</span></span>
* <span data-ttu-id="7e71b-124">If you are passing ConfigurationData when compiling the configuration, make sure that you are passing the expected values that the configuration requires from [ConfigurationData](../automation-dsc-compile.md#configurationdata).</span><span class="sxs-lookup"><span data-stu-id="7e71b-124">If you are passing ConfigurationData when compiling the configuration, make sure that you are passing the expected values that the configuration requires from [ConfigurationData](../automation-dsc-compile.md#configurationdata).</span></span>

### <a name="dsc-in-progress"></a><span data-ttu-id="7e71b-125">Scenario: The DSC node report becomes stuck "in progress" state</span><span class="sxs-lookup"><span data-stu-id="7e71b-125">Scenario: The DSC node report becomes stuck "in progress" state</span></span>

#### <a name="issue"></a><span data-ttu-id="7e71b-126">Issue</span><span class="sxs-lookup"><span data-stu-id="7e71b-126">Issue</span></span>

<span data-ttu-id="7e71b-127">The DSC agent outputs:</span><span class="sxs-lookup"><span data-stu-id="7e71b-127">The DSC agent outputs:</span></span>

```
No instance found with given property values
```

#### <a name="cause"></a><span data-ttu-id="7e71b-128">Cause</span><span class="sxs-lookup"><span data-stu-id="7e71b-128">Cause</span></span>

<span data-ttu-id="7e71b-129">You have upgraded your WMF version and have corrupted WMI.</span><span class="sxs-lookup"><span data-stu-id="7e71b-129">You have upgraded your WMF version and have corrupted WMI.</span></span>

#### <a name="resolution"></a><span data-ttu-id="7e71b-130">Resolution</span><span class="sxs-lookup"><span data-stu-id="7e71b-130">Resolution</span></span>

<span data-ttu-id="7e71b-131">To fix the issue follow the instructions in the [DSC known issues and limitations](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) article.</span><span class="sxs-lookup"><span data-stu-id="7e71b-131">To fix the issue follow the instructions in the [DSC known issues and limitations](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) article.</span></span>

### <a name="issue-using-credential"></a><span data-ttu-id="7e71b-132">Scenario: Unable to use a credential in a DSC configuration</span><span class="sxs-lookup"><span data-stu-id="7e71b-132">Scenario: Unable to use a credential in a DSC configuration</span></span>

#### <a name="issue"></a><span data-ttu-id="7e71b-133">Issue</span><span class="sxs-lookup"><span data-stu-id="7e71b-133">Issue</span></span>

<span data-ttu-id="7e71b-134">Your DSC compilation job was suspended with the error:</span><span class="sxs-lookup"><span data-stu-id="7e71b-134">Your DSC compilation job was suspended with the error:</span></span>

```
System.InvalidOperationException error processing property 'Credential' of type <some resource name>: Converting and storing an encrypted password as plaintext is allowed only if PSDscAllowPlainTextPassword is set to true.
```

#### <a name="cause"></a><span data-ttu-id="7e71b-135">Cause</span><span class="sxs-lookup"><span data-stu-id="7e71b-135">Cause</span></span>

<span data-ttu-id="7e71b-136">You have used a credential in a configuration but didn’t provide proper **ConfigurationData** to set **PSDscAllowPlainTextPassword** to true for each node configuration.</span><span class="sxs-lookup"><span data-stu-id="7e71b-136">You have used a credential in a configuration but didn’t provide proper **ConfigurationData** to set **PSDscAllowPlainTextPassword** to true for each node configuration.</span></span>

#### <a name="resolution"></a><span data-ttu-id="7e71b-137">Resolution</span><span class="sxs-lookup"><span data-stu-id="7e71b-137">Resolution</span></span>

* <span data-ttu-id="7e71b-138">Make sure to pass in the proper **ConfigurationData** to set **PSDscAllowPlainTextPassword** to true for each node configuration mentioned in the configuration.</span><span class="sxs-lookup"><span data-stu-id="7e71b-138">Make sure to pass in the proper **ConfigurationData** to set **PSDscAllowPlainTextPassword** to true for each node configuration mentioned in the configuration.</span></span> <span data-ttu-id="7e71b-139">For more information, see [assets in Azure Automation DSC](../automation-dsc-compile.md#assets).</span><span class="sxs-lookup"><span data-stu-id="7e71b-139">For more information, see [assets in Azure Automation DSC](../automation-dsc-compile.md#assets).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e71b-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="7e71b-140">Next steps</span></span>

<span data-ttu-id="7e71b-141">If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:</span><span class="sxs-lookup"><span data-stu-id="7e71b-141">If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:</span></span>

* <span data-ttu-id="7e71b-142">Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)</span><span class="sxs-lookup"><span data-stu-id="7e71b-142">Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)</span></span>
* <span data-ttu-id="7e71b-143">Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.</span><span class="sxs-lookup"><span data-stu-id="7e71b-143">Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.</span></span>
* <span data-ttu-id="7e71b-144">If you need more help, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="7e71b-144">If you need more help, you can file an Azure support incident.</span></span> <span data-ttu-id="7e71b-145">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="7e71b-145">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>