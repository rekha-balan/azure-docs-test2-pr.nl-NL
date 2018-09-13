---
title: Azure Blockchain Workbench troubleshooting
description: How to troubleshoot a Azure Blockchain Workbench application.
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 4/21/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: zeyadr
manager: femila
ms.openlocfilehash: 419ed6dc76101366e47ae94067f7b671a10c94e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857027"
---
# <a name="azure-blockchain-workbench-troubleshooting"></a><span data-ttu-id="2a54e-103">Azure Blockchain Workbench troubleshooting</span><span class="sxs-lookup"><span data-stu-id="2a54e-103">Azure Blockchain Workbench troubleshooting</span></span>

<span data-ttu-id="2a54e-104">A PowerShell script is available to assist with developer debugging or support.</span><span class="sxs-lookup"><span data-stu-id="2a54e-104">A PowerShell script is available to assist with developer debugging or support.</span></span> <span data-ttu-id="2a54e-105">The script generates a summary and collects detailed logs for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="2a54e-105">The script generates a summary and collects detailed logs for troubleshooting.</span></span> <span data-ttu-id="2a54e-106">Collected logs include:</span><span class="sxs-lookup"><span data-stu-id="2a54e-106">Collected logs include:</span></span>

* <span data-ttu-id="2a54e-107">Blockchain network, such as Ethereum</span><span class="sxs-lookup"><span data-stu-id="2a54e-107">Blockchain network, such as Ethereum</span></span>
* <span data-ttu-id="2a54e-108">Blockchain Workbench microservices</span><span class="sxs-lookup"><span data-stu-id="2a54e-108">Blockchain Workbench microservices</span></span>
* <span data-ttu-id="2a54e-109">Application Insights</span><span class="sxs-lookup"><span data-stu-id="2a54e-109">Application Insights</span></span>
* <span data-ttu-id="2a54e-110">Azure Monitoring (OMS)</span><span class="sxs-lookup"><span data-stu-id="2a54e-110">Azure Monitoring (OMS)</span></span>

<span data-ttu-id="2a54e-111">You can use the information to determine next steps and determine root cause of issues.</span><span class="sxs-lookup"><span data-stu-id="2a54e-111">You can use the information to determine next steps and determine root cause of issues.</span></span> 

## <a name="troubleshooting-script"></a><span data-ttu-id="2a54e-112">Troubleshooting script</span><span class="sxs-lookup"><span data-stu-id="2a54e-112">Troubleshooting script</span></span>

<span data-ttu-id="2a54e-113">The PowerShell troubleshooting script is available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="2a54e-113">The PowerShell troubleshooting script is available on GitHub.</span></span> <span data-ttu-id="2a54e-114">[Download a zip file](https://github.com/Azure-Samples/blockchain/archive/master.zip) or clone the sample from GitHub.</span><span class="sxs-lookup"><span data-stu-id="2a54e-114">[Download a zip file](https://github.com/Azure-Samples/blockchain/archive/master.zip) or clone the sample from GitHub.</span></span>

```
git clone https://github.com/Azure-Samples/blockchain.git
```

## <a name="run-the-script"></a><span data-ttu-id="2a54e-115">Run the script</span><span class="sxs-lookup"><span data-stu-id="2a54e-115">Run the script</span></span>
[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<span data-ttu-id="2a54e-116">Run the `collectBlockchainWorkbenchTroubleshooting.ps1` script to collect logs and create a ZIP file containing a folder of troubleshooting information.</span><span class="sxs-lookup"><span data-stu-id="2a54e-116">Run the `collectBlockchainWorkbenchTroubleshooting.ps1` script to collect logs and create a ZIP file containing a folder of troubleshooting information.</span></span> <span data-ttu-id="2a54e-117">For example:</span><span class="sxs-lookup"><span data-stu-id="2a54e-117">For example:</span></span>

``` powershell
collectBlockchainWorkbenchTroubleshooting.ps1 -SubscriptionID "<subscription_id>" -ResourceGroupName "workbench-resource-group-name"
```
<span data-ttu-id="2a54e-118">The script accepts the following parameters:</span><span class="sxs-lookup"><span data-stu-id="2a54e-118">The script accepts the following parameters:</span></span>

| <span data-ttu-id="2a54e-119">Parameter</span><span class="sxs-lookup"><span data-stu-id="2a54e-119">Parameter</span></span>  | <span data-ttu-id="2a54e-120">Description</span><span class="sxs-lookup"><span data-stu-id="2a54e-120">Description</span></span> | <span data-ttu-id="2a54e-121">Required</span><span class="sxs-lookup"><span data-stu-id="2a54e-121">Required</span></span> |
|---------|---------|----|
| <span data-ttu-id="2a54e-122">SubscriptionID</span><span class="sxs-lookup"><span data-stu-id="2a54e-122">SubscriptionID</span></span> | <span data-ttu-id="2a54e-123">SubscriptionID to create or locate all resources.</span><span class="sxs-lookup"><span data-stu-id="2a54e-123">SubscriptionID to create or locate all resources.</span></span> | <span data-ttu-id="2a54e-124">Yes</span><span class="sxs-lookup"><span data-stu-id="2a54e-124">Yes</span></span> |
| <span data-ttu-id="2a54e-125">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2a54e-125">ResourceGroupName</span></span> | <span data-ttu-id="2a54e-126">Name of the Azure Resource Group where Blockchain Workbench has been deployed.</span><span class="sxs-lookup"><span data-stu-id="2a54e-126">Name of the Azure Resource Group where Blockchain Workbench has been deployed.</span></span> | <span data-ttu-id="2a54e-127">Yes</span><span class="sxs-lookup"><span data-stu-id="2a54e-127">Yes</span></span> |
| <span data-ttu-id="2a54e-128">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="2a54e-128">OutputDirectory</span></span> | <span data-ttu-id="2a54e-129">Path to create the output .ZIP file.</span><span class="sxs-lookup"><span data-stu-id="2a54e-129">Path to create the output .ZIP file.</span></span> <span data-ttu-id="2a54e-130">If not specified, defaults to the current directory.</span><span class="sxs-lookup"><span data-stu-id="2a54e-130">If not specified, defaults to the current directory.</span></span> | <span data-ttu-id="2a54e-131">No</span><span class="sxs-lookup"><span data-stu-id="2a54e-131">No</span></span> |
| <span data-ttu-id="2a54e-132">LookbackHours</span><span class="sxs-lookup"><span data-stu-id="2a54e-132">LookbackHours</span></span> | <span data-ttu-id="2a54e-133">Number of hours to use when pulling telemetry.</span><span class="sxs-lookup"><span data-stu-id="2a54e-133">Number of hours to use when pulling telemetry.</span></span> <span data-ttu-id="2a54e-134">Default value is 24 hours.</span><span class="sxs-lookup"><span data-stu-id="2a54e-134">Default value is 24 hours.</span></span> <span data-ttu-id="2a54e-135">Maximum value is 90 hours</span><span class="sxs-lookup"><span data-stu-id="2a54e-135">Maximum value is 90 hours</span></span> | <span data-ttu-id="2a54e-136">No</span><span class="sxs-lookup"><span data-stu-id="2a54e-136">No</span></span> |
| <span data-ttu-id="2a54e-137">OmsSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="2a54e-137">OmsSubscriptionId</span></span> | <span data-ttu-id="2a54e-138">The subscription ID where OMS is deployed.</span><span class="sxs-lookup"><span data-stu-id="2a54e-138">The subscription ID where OMS is deployed.</span></span> <span data-ttu-id="2a54e-139">Only pass this parameter if the OMS for the blockchain network is deployed outside of Blockchain Workbench's resource group.</span><span class="sxs-lookup"><span data-stu-id="2a54e-139">Only pass this parameter if the OMS for the blockchain network is deployed outside of Blockchain Workbench's resource group.</span></span>| <span data-ttu-id="2a54e-140">No</span><span class="sxs-lookup"><span data-stu-id="2a54e-140">No</span></span> |
| <span data-ttu-id="2a54e-141">OmsResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2a54e-141">OmsResourceGroup</span></span> |<span data-ttu-id="2a54e-142">The resource group where OMS is deployed.</span><span class="sxs-lookup"><span data-stu-id="2a54e-142">The resource group where OMS is deployed.</span></span> <span data-ttu-id="2a54e-143">Only pass this parameter if the OMS for the blockchain network is deployed outside of Blockchain Workbench's resource group.</span><span class="sxs-lookup"><span data-stu-id="2a54e-143">Only pass this parameter if the OMS for the blockchain network is deployed outside of Blockchain Workbench's resource group.</span></span>| <span data-ttu-id="2a54e-144">No</span><span class="sxs-lookup"><span data-stu-id="2a54e-144">No</span></span> |
| <span data-ttu-id="2a54e-145">OmsWorkspaceName</span><span class="sxs-lookup"><span data-stu-id="2a54e-145">OmsWorkspaceName</span></span> | <span data-ttu-id="2a54e-146">The OMS workspace name.</span><span class="sxs-lookup"><span data-stu-id="2a54e-146">The OMS workspace name.</span></span> <span data-ttu-id="2a54e-147">Only pass this parameter if the OMS for the blockchain network is deployed outside of Blockchain Workbench's resource group</span><span class="sxs-lookup"><span data-stu-id="2a54e-147">Only pass this parameter if the OMS for the blockchain network is deployed outside of Blockchain Workbench's resource group</span></span> | <span data-ttu-id="2a54e-148">No</span><span class="sxs-lookup"><span data-stu-id="2a54e-148">No</span></span> |

## <a name="what-is-collected"></a><span data-ttu-id="2a54e-149">What is collected?</span><span class="sxs-lookup"><span data-stu-id="2a54e-149">What is collected?</span></span>

<span data-ttu-id="2a54e-150">The output ZIP file contains the following folder structure:</span><span class="sxs-lookup"><span data-stu-id="2a54e-150">The output ZIP file contains the following folder structure:</span></span>

| <span data-ttu-id="2a54e-151">Folder or File</span><span class="sxs-lookup"><span data-stu-id="2a54e-151">Folder or File</span></span> | <span data-ttu-id="2a54e-152">Description</span><span class="sxs-lookup"><span data-stu-id="2a54e-152">Description</span></span>  |
|---------|---------|
| <span data-ttu-id="2a54e-153">\Summary.txt</span><span class="sxs-lookup"><span data-stu-id="2a54e-153">\Summary.txt</span></span> | <span data-ttu-id="2a54e-154">Summary of the system</span><span class="sxs-lookup"><span data-stu-id="2a54e-154">Summary of the system</span></span> |
| <span data-ttu-id="2a54e-155">\Metrics\blockchain</span><span class="sxs-lookup"><span data-stu-id="2a54e-155">\Metrics\blockchain</span></span> | <span data-ttu-id="2a54e-156">Metrics about the blockchain</span><span class="sxs-lookup"><span data-stu-id="2a54e-156">Metrics about the blockchain</span></span> |
| <span data-ttu-id="2a54e-157">\Metrics\Workbench</span><span class="sxs-lookup"><span data-stu-id="2a54e-157">\Metrics\Workbench</span></span> | <span data-ttu-id="2a54e-158">Metrics about the workbench</span><span class="sxs-lookup"><span data-stu-id="2a54e-158">Metrics about the workbench</span></span> |
| <span data-ttu-id="2a54e-159">\Details\Blockchain</span><span class="sxs-lookup"><span data-stu-id="2a54e-159">\Details\Blockchain</span></span> | <span data-ttu-id="2a54e-160">Detailed logs about the blockchain</span><span class="sxs-lookup"><span data-stu-id="2a54e-160">Detailed logs about the blockchain</span></span> |
| <span data-ttu-id="2a54e-161">\Details\Workbench</span><span class="sxs-lookup"><span data-stu-id="2a54e-161">\Details\Workbench</span></span> | <span data-ttu-id="2a54e-162">Detailed logs about the workbench</span><span class="sxs-lookup"><span data-stu-id="2a54e-162">Detailed logs about the workbench</span></span> |

<span data-ttu-id="2a54e-163">The summary file gives you a snapshot of the overall state of the application and health of the application.</span><span class="sxs-lookup"><span data-stu-id="2a54e-163">The summary file gives you a snapshot of the overall state of the application and health of the application.</span></span> <span data-ttu-id="2a54e-164">The summary provides recommended actions, highlights top errors, and metadata about running services.</span><span class="sxs-lookup"><span data-stu-id="2a54e-164">The summary provides recommended actions, highlights top errors, and metadata about running services.</span></span>

<span data-ttu-id="2a54e-165">The **Metrics** folder contains metrics of various system components over time.</span><span class="sxs-lookup"><span data-stu-id="2a54e-165">The **Metrics** folder contains metrics of various system components over time.</span></span> <span data-ttu-id="2a54e-166">For example, the output file `\Details\Workbench\apiMetrics.txt` contains a summary of different response codes, and response times throughout the collection period.</span><span class="sxs-lookup"><span data-stu-id="2a54e-166">For example, the output file `\Details\Workbench\apiMetrics.txt` contains a summary of different response codes, and response times throughout the collection period.</span></span> <span data-ttu-id="2a54e-167">The **Details** folder contains detailed logs for troubleshooting specific issues with Workbench or the underlying blockchain network.</span><span class="sxs-lookup"><span data-stu-id="2a54e-167">The **Details** folder contains detailed logs for troubleshooting specific issues with Workbench or the underlying blockchain network.</span></span> <span data-ttu-id="2a54e-168">For example, `\Details\Workbench\Exceptions.csv` contains a list of the most recent exceptions that have occurred in the system, which is useful for troubleshooting errors with smart contracts or interactions with the blockchain.</span><span class="sxs-lookup"><span data-stu-id="2a54e-168">For example, `\Details\Workbench\Exceptions.csv` contains a list of the most recent exceptions that have occurred in the system, which is useful for troubleshooting errors with smart contracts or interactions with the blockchain.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2a54e-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a54e-169">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2a54e-170">Azure Blockchain Workbench architecture</span><span class="sxs-lookup"><span data-stu-id="2a54e-170">Azure Blockchain Workbench architecture</span></span>](blockchain-workbench-architecture.md)