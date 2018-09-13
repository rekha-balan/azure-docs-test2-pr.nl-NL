---
title: Use Azure Automation to trigger a job | Microsoft Docs
description: Learn how to use Azure Automation for triggering StorSimple Data Manager Jobs (private preview)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 950be01bb0121b000f7d5cd9607320cbb4ca1de7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549578"
---
# <a name="use-azure-automation-to-trigger-a-job-private-preview"></a><span data-ttu-id="667db-103">Use Azure Automation to trigger a job (Private Preview)</span><span class="sxs-lookup"><span data-stu-id="667db-103">Use Azure Automation to trigger a job (Private Preview)</span></span>

<span data-ttu-id="667db-104">This articles describes how to use Azure Automation to trigger a StorSimple Data Manager job.</span><span class="sxs-lookup"><span data-stu-id="667db-104">This articles describes how to use Azure Automation to trigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="667db-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="667db-105">Prerequisites</span></span>

<span data-ttu-id="667db-106">Before you begin, ensure that you have:</span><span class="sxs-lookup"><span data-stu-id="667db-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="667db-107">Azure Powershell installed.</span><span class="sxs-lookup"><span data-stu-id="667db-107">Azure Powershell installed.</span></span> <span data-ttu-id="667db-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="667db-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="667db-109">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span><span class="sxs-lookup"><span data-stu-id="667db-109">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="667db-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span><span class="sxs-lookup"><span data-stu-id="667db-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="667db-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from the github repository.</span><span class="sxs-lookup"><span data-stu-id="667db-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from the github repository.</span></span>
*   <span data-ttu-id="667db-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from the github repository.</span><span class="sxs-lookup"><span data-stu-id="667db-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from the github repository.</span></span>
*   <span data-ttu-id="667db-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from the github repository.</span><span class="sxs-lookup"><span data-stu-id="667db-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="667db-114">Step-by-step</span><span class="sxs-lookup"><span data-stu-id="667db-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-the-automation-job-to-run-the-job-definition"></a><span data-ttu-id="667db-115">Get Azure Active Directory permissions for the automation job to run the job definition</span><span class="sxs-lookup"><span data-stu-id="667db-115">Get Azure Active Directory permissions for the automation job to run the job definition</span></span>

1. <span data-ttu-id="667db-116">To retrieve the configuration parameters for Active Directory, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="667db-116">To retrieve the configuration parameters for Active Directory, do the following steps:</span></span>

    1. <span data-ttu-id="667db-117">Open Windows PowerShell in your local machine.</span><span class="sxs-lookup"><span data-stu-id="667db-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="667db-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span><span class="sxs-lookup"><span data-stu-id="667db-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="667db-119">Run the `Get-ConfigurationParams.ps1` script (in the folder you downloaded above).</span><span class="sxs-lookup"><span data-stu-id="667db-119">Run the `Get-ConfigurationParams.ps1` script (in the folder you downloaded above).</span></span> <span data-ttu-id="667db-120">Type the following command in the PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="667db-120">Type the following command in the PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="667db-121">The ActiveDirectoryKey is a password that you use later.</span><span class="sxs-lookup"><span data-stu-id="667db-121">The ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="667db-122">Enter a password of your choice.</span><span class="sxs-lookup"><span data-stu-id="667db-122">Enter a password of your choice.</span></span> <span data-ttu-id="667db-123">AppName can be any string.</span><span class="sxs-lookup"><span data-stu-id="667db-123">AppName can be any string.</span></span>

2. <span data-ttu-id="667db-124">This script outputs the following values that should be used while triggering the automation runbook.</span><span class="sxs-lookup"><span data-stu-id="667db-124">This script outputs the following values that should be used while triggering the automation runbook.</span></span> <span data-ttu-id="667db-125">Make a note of these values.</span><span class="sxs-lookup"><span data-stu-id="667db-125">Make a note of these values.</span></span>

    - <span data-ttu-id="667db-126">Client ID</span><span class="sxs-lookup"><span data-stu-id="667db-126">Client ID</span></span>
    - <span data-ttu-id="667db-127">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="667db-127">Tenant ID</span></span>
    - <span data-ttu-id="667db-128">Active Directory key (same as the one entered above)</span><span class="sxs-lookup"><span data-stu-id="667db-128">Active Directory key (same as the one entered above)</span></span>
    - <span data-ttu-id="667db-129">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="667db-129">Subscription ID</span></span>

### <a name="set-up-the-automation-account"></a><span data-ttu-id="667db-130">Set up the Automation Account</span><span class="sxs-lookup"><span data-stu-id="667db-130">Set up the Automation Account</span></span>

1. <span data-ttu-id="667db-131">Log on to Azure and open your Automation account.</span><span class="sxs-lookup"><span data-stu-id="667db-131">Log on to Azure and open your Automation account.</span></span>
2. <span data-ttu-id="667db-132">Click **Assets** tile to open the list of assets.</span><span class="sxs-lookup"><span data-stu-id="667db-132">Click **Assets** tile to open the list of assets.</span></span>
3. <span data-ttu-id="667db-133">Click **Modules** tile to open the list of modules.</span><span class="sxs-lookup"><span data-stu-id="667db-133">Click **Modules** tile to open the list of modules.</span></span>
4. <span data-ttu-id="667db-134">Click **+ Add a module** button and the Add module blade is launched.</span><span class="sxs-lookup"><span data-stu-id="667db-134">Click **+ Add a module** button and the Add module blade is launched.</span></span>

    ![Automation account settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="667db-136">After you have selected the `DataTransformationApp.zip` file from your local computer, click **OK** to import the module.</span><span class="sxs-lookup"><span data-stu-id="667db-136">After you have selected the `DataTransformationApp.zip` file from your local computer, click **OK** to import the module.</span></span>

   <span data-ttu-id="667db-137">When Azure Automation imports a module to your account, it extracts metadata about the module.</span><span class="sxs-lookup"><span data-stu-id="667db-137">When Azure Automation imports a module to your account, it extracts metadata about the module.</span></span> <span data-ttu-id="667db-138">This operation may take a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="667db-138">This operation may take a couple of minutes.</span></span>

   ![Automation account settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="667db-140">You receive a notification that the module is being deployed and another notification when the process is complete.</span><span class="sxs-lookup"><span data-stu-id="667db-140">You receive a notification that the module is being deployed and another notification when the process is complete.</span></span>  <span data-ttu-id="667db-141">You can also check the status in **Modules** tile.</span><span class="sxs-lookup"><span data-stu-id="667db-141">You can also check the status in **Modules** tile.</span></span>

### <a name="to-import-the-runbook-that-triggers-the-job-definition"></a><span data-ttu-id="667db-142">To import the runbook that triggers the job definition</span><span class="sxs-lookup"><span data-stu-id="667db-142">To import the runbook that triggers the job definition</span></span>

1. <span data-ttu-id="667db-143">In the Azure portal, open your Automation account.</span><span class="sxs-lookup"><span data-stu-id="667db-143">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="667db-144">Click **Runbooks** tile to open the list of runbooks.</span><span class="sxs-lookup"><span data-stu-id="667db-144">Click **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="667db-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span><span class="sxs-lookup"><span data-stu-id="667db-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Import an existing runbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="667db-147">Click **Runbook file** and select the file to import `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="667db-147">Click **Runbook file** and select the file to import `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="667db-148">Click **Create** to import the runbook.</span><span class="sxs-lookup"><span data-stu-id="667db-148">Click **Create** to import the runbook.</span></span> <span data-ttu-id="667db-149">The new runbook appears in the list of runbooks for the Automation account.</span><span class="sxs-lookup"><span data-stu-id="667db-149">The new runbook appears in the list of runbooks for the Automation account.</span></span>
7. <span data-ttu-id="667db-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="667db-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="667db-151">Click **Publish** and then **Yes** when prompted for confirmation.</span><span class="sxs-lookup"><span data-stu-id="667db-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="to-run-the-runbook"></a><span data-ttu-id="667db-152">To run the runbook:</span><span class="sxs-lookup"><span data-stu-id="667db-152">To run the runbook:</span></span>
1. <span data-ttu-id="667db-153">In the Azure portal, open your Automation account.</span><span class="sxs-lookup"><span data-stu-id="667db-153">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="667db-154">Click the **Runbooks** tile to open the list of runbooks.</span><span class="sxs-lookup"><span data-stu-id="667db-154">Click the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="667db-155">Click **Trigger-DataTransformation-Job**.</span><span class="sxs-lookup"><span data-stu-id="667db-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="667db-156">Click **Start** to start the runbook.</span><span class="sxs-lookup"><span data-stu-id="667db-156">Click **Start** to start the runbook.</span></span>

   ![Start runbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="667db-158">In the **Start runbook** blade, enter all the parameters.</span><span class="sxs-lookup"><span data-stu-id="667db-158">In the **Start runbook** blade, enter all the parameters.</span></span> <span data-ttu-id="667db-159">Click **OK** to submit the Data Transformation job.</span><span class="sxs-lookup"><span data-stu-id="667db-159">Click **OK** to submit the Data Transformation job.</span></span>

   ![Start runbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="667db-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="667db-161">Next steps</span></span>

<span data-ttu-id="667db-162">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="667db-162">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>




