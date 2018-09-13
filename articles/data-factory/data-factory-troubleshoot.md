---
title: Troubleshoot Azure Data Factory issues
description: Learn how to troubleshoot issues with using Azure Data Factory.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: spelluru
ms.openlocfilehash: 89eb44df3bf990ecf3142ffee528aebcc0bf720a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562924"
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="d7e46-103">Troubleshoot Data Factory issues</span><span class="sxs-lookup"><span data-stu-id="d7e46-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="d7e46-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d7e46-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="d7e46-105">This article does not list all the possible issues when using the service, but it covers some issues and general troubleshooting tips.</span><span class="sxs-lookup"><span data-stu-id="d7e46-105">This article does not list all the possible issues when using the service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="d7e46-106">Troubleshooting tips</span><span class="sxs-lookup"><span data-stu-id="d7e46-106">Troubleshooting tips</span></span>
### <a name="error-the-subscription-is-not-registered-to-use-namespace-microsoftdatafactory"></a><span data-ttu-id="d7e46-107">Error: The subscription is not registered to use namespace 'Microsoft.DataFactory'</span><span class="sxs-lookup"><span data-stu-id="d7e46-107">Error: The subscription is not registered to use namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="d7e46-108">If you receive this error, the Azure Data Factory resource provider has not been registered on your machine.</span><span class="sxs-lookup"><span data-stu-id="d7e46-108">If you receive this error, the Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="d7e46-109">Do the following:</span><span class="sxs-lookup"><span data-stu-id="d7e46-109">Do the following:</span></span>

1. <span data-ttu-id="d7e46-110">Launch Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7e46-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="d7e46-111">Log in to your Azure account using the following command.</span><span class="sxs-lookup"><span data-stu-id="d7e46-111">Log in to your Azure account using the following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="d7e46-112">Run the following command to register the Azure Data Factory provider.</span><span class="sxs-lookup"><span data-stu-id="d7e46-112">Run the following command to register the Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="d7e46-113">Problem: Unauthorized error when running a Data Factory cmdlet</span><span class="sxs-lookup"><span data-stu-id="d7e46-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="d7e46-114">You are probably not using the right Azure account or subscription with the Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7e46-114">You are probably not using the right Azure account or subscription with the Azure PowerShell.</span></span> <span data-ttu-id="d7e46-115">Use the following cmdlets to select the right Azure account and subscription to use with the Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7e46-115">Use the following cmdlets to select the right Azure account and subscription to use with the Azure PowerShell.</span></span>

1. <span data-ttu-id="d7e46-116">Login-AzureRmAccount - Use the right user ID and password</span><span class="sxs-lookup"><span data-stu-id="d7e46-116">Login-AzureRmAccount - Use the right user ID and password</span></span>
2. <span data-ttu-id="d7e46-117">Get-AzureRmSubscription - View all the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="d7e46-117">Get-AzureRmSubscription - View all the subscriptions for the account.</span></span>
3. <span data-ttu-id="d7e46-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select the right subscription.</span><span class="sxs-lookup"><span data-stu-id="d7e46-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select the right subscription.</span></span> <span data-ttu-id="d7e46-119">Use the same one you use to create a data factory on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d7e46-119">Use the same one you use to create a data factory on the Azure portal.</span></span>

### <a name="problem-fail-to-launch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="d7e46-120">Problem: Fail to launch Data Management Gateway Express Setup from Azure portal</span><span class="sxs-lookup"><span data-stu-id="d7e46-120">Problem: Fail to launch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="d7e46-121">The Express setup for the Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span><span class="sxs-lookup"><span data-stu-id="d7e46-121">The Express setup for the Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="d7e46-122">If the Express Setup fails to start, do one of the following:</span><span class="sxs-lookup"><span data-stu-id="d7e46-122">If the Express Setup fails to start, do one of the following:</span></span>

* <span data-ttu-id="d7e46-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span><span class="sxs-lookup"><span data-stu-id="d7e46-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="d7e46-124">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span><span class="sxs-lookup"><span data-stu-id="d7e46-124">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="d7e46-125">Do the same for Firefox (install add-in).</span><span class="sxs-lookup"><span data-stu-id="d7e46-125">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="d7e46-126">Click Open Menu button on the toolbar (three horizontal lines in the top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span><span class="sxs-lookup"><span data-stu-id="d7e46-126">Click Open Menu button on the toolbar (three horizontal lines in the top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="d7e46-127">Use the **Manual Setup** link shown on the same blade in the portal.</span><span class="sxs-lookup"><span data-stu-id="d7e46-127">Use the **Manual Setup** link shown on the same blade in the portal.</span></span> <span data-ttu-id="d7e46-128">You use this approach to download installation file and run it manually.</span><span class="sxs-lookup"><span data-stu-id="d7e46-128">You use this approach to download installation file and run it manually.</span></span> <span data-ttu-id="d7e46-129">After the installation is successful, you see the Data Management Gateway Configuration dialog box.</span><span class="sxs-lookup"><span data-stu-id="d7e46-129">After the installation is successful, you see the Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="d7e46-130">Copy the **key** from the portal screen and use it in the configuration manager to manually register the gateway with the service.</span><span class="sxs-lookup"><span data-stu-id="d7e46-130">Copy the **key** from the portal screen and use it in the configuration manager to manually register the gateway with the service.</span></span>  

### <a name="problem-fail-to-connect-to-on-premises-sql-server"></a><span data-ttu-id="d7e46-131">Problem: Fail to connect to on-premises SQL Server</span><span class="sxs-lookup"><span data-stu-id="d7e46-131">Problem: Fail to connect to on-premises SQL Server</span></span>
<span data-ttu-id="d7e46-132">Launch **Data Management Gateway Configuration Manager** on the gateway machine and use the **Troubleshooting** tab to test the connection to SQL Server from the gateway machine.</span><span class="sxs-lookup"><span data-stu-id="d7e46-132">Launch **Data Management Gateway Configuration Manager** on the gateway machine and use the **Troubleshooting** tab to test the connection to SQL Server from the gateway machine.</span></span> <span data-ttu-id="d7e46-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span><span class="sxs-lookup"><span data-stu-id="d7e46-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="d7e46-134">Problem: Input slices are in Waiting state for ever</span><span class="sxs-lookup"><span data-stu-id="d7e46-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="d7e46-135">The slices could be in **Waiting** state due to various reasons.</span><span class="sxs-lookup"><span data-stu-id="d7e46-135">The slices could be in **Waiting** state due to various reasons.</span></span> <span data-ttu-id="d7e46-136">One of the common reasons is that the **external** property is not set to **true**.</span><span class="sxs-lookup"><span data-stu-id="d7e46-136">One of the common reasons is that the **external** property is not set to **true**.</span></span> <span data-ttu-id="d7e46-137">Any dataset that is produced outside the scope of Azure Data Factory should be marked with **external** property.</span><span class="sxs-lookup"><span data-stu-id="d7e46-137">Any dataset that is produced outside the scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="d7e46-138">This property indicates that the data is external and not backed by any pipelines within the data factory.</span><span class="sxs-lookup"><span data-stu-id="d7e46-138">This property indicates that the data is external and not backed by any pipelines within the data factory.</span></span> <span data-ttu-id="d7e46-139">The data slices are marked as **Ready** once the data is available in the respective store.</span><span class="sxs-lookup"><span data-stu-id="d7e46-139">The data slices are marked as **Ready** once the data is available in the respective store.</span></span>

<span data-ttu-id="d7e46-140">See the following example for the usage of the **external** property.</span><span class="sxs-lookup"><span data-stu-id="d7e46-140">See the following example for the usage of the **external** property.</span></span> <span data-ttu-id="d7e46-141">You can optionally specify **externalData**\* when you set external to true.</span><span class="sxs-lookup"><span data-stu-id="d7e46-141">You can optionally specify **externalData**\* when you set external to true.</span></span>

<span data-ttu-id="d7e46-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span><span class="sxs-lookup"><span data-stu-id="d7e46-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="d7e46-143">To resolve the error, add the **external** property and the optional **externalData** section to the JSON definition of the input table and recreate the table.</span><span class="sxs-lookup"><span data-stu-id="d7e46-143">To resolve the error, add the **external** property and the optional **externalData** section to the JSON definition of the input table and recreate the table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="d7e46-144">Problem: Hybrid copy operation fails</span><span class="sxs-lookup"><span data-stu-id="d7e46-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="d7e46-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps to troubleshoot issues with copying to/from an on-premises data store using the Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="d7e46-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps to troubleshoot issues with copying to/from an on-premises data store using the Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="d7e46-146">Problem: On-demand HDInsight provisioning fails</span><span class="sxs-lookup"><span data-stu-id="d7e46-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="d7e46-147">When using a linked service of type HDInsightOnDemand, you need to specify a linkedServiceName that points to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d7e46-147">When using a linked service of type HDInsightOnDemand, you need to specify a linkedServiceName that points to an Azure Blob Storage.</span></span> <span data-ttu-id="d7e46-148">Data Factory service uses this storage to store logs and supporting files for your on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d7e46-148">Data Factory service uses this storage to store logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="d7e46-149">Sometimes provisioning of an on-demand HDInsight cluster fails with the following error:</span><span class="sxs-lookup"><span data-stu-id="d7e46-149">Sometimes provisioning of an on-demand HDInsight cluster fails with the following error:</span></span>

```
Failed to create cluster. Exception: Unable to complete the cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="d7e46-150">This error usually indicates that the location of the storage account specified in the linkedServiceName is not in the same data center location where the HDInsight provisioning is happening.</span><span class="sxs-lookup"><span data-stu-id="d7e46-150">This error usually indicates that the location of the storage account specified in the linkedServiceName is not in the same data center location where the HDInsight provisioning is happening.</span></span> <span data-ttu-id="d7e46-151">Example: if your data factory is in West US and the Azure storage is in East US, the on-demand provisioning fails in West US.</span><span class="sxs-lookup"><span data-stu-id="d7e46-151">Example: if your data factory is in West US and the Azure storage is in East US, the on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="d7e46-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d7e46-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="d7e46-153">Those additional linked storage accounts should be in the same location as the HDInsight cluster, or it fails with the same error.</span><span class="sxs-lookup"><span data-stu-id="d7e46-153">Those additional linked storage accounts should be in the same location as the HDInsight cluster, or it fails with the same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="d7e46-154">Problem: Custom .NET activity fails</span><span class="sxs-lookup"><span data-stu-id="d7e46-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="d7e46-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="d7e46-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-to-troubleshoot"></a><span data-ttu-id="d7e46-156">Use Azure portal to troubleshoot</span><span class="sxs-lookup"><span data-stu-id="d7e46-156">Use Azure portal to troubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="d7e46-157">Using portal blades</span><span class="sxs-lookup"><span data-stu-id="d7e46-157">Using portal blades</span></span>
<span data-ttu-id="d7e46-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span><span class="sxs-lookup"><span data-stu-id="d7e46-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="d7e46-159">Using Monitor and Manage App</span><span class="sxs-lookup"><span data-stu-id="d7e46-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="d7e46-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span><span class="sxs-lookup"><span data-stu-id="d7e46-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-to-troubleshoot"></a><span data-ttu-id="d7e46-161">Use Azure PowerShell to troubleshoot</span><span class="sxs-lookup"><span data-stu-id="d7e46-161">Use Azure PowerShell to troubleshoot</span></span>
### <a name="use-azure-powershell-to-troubleshoot-an-error"></a><span data-ttu-id="d7e46-162">Use Azure PowerShell to troubleshoot an error</span><span class="sxs-lookup"><span data-stu-id="d7e46-162">Use Azure PowerShell to troubleshoot an error</span></span>
<span data-ttu-id="d7e46-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span><span class="sxs-lookup"><span data-stu-id="d7e46-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png









