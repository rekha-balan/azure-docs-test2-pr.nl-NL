---
title: Learn Data Lake Analytics and U-SQL using the Azure portal Interactive tutorials | Microsoft Docs
description: 'Quick start with learning Data Lake Analytics and U-SQL. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 31399d47-e937-4c43-ab0a-6aea8875378d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 7ce99648295a29c861cd02aed454359fd52aa51f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549252"
---
# <a name="use-azure-data-lake-analytics-interactive-tutorials"></a><span data-ttu-id="7dc7c-103">Use Azure Data Lake Analytics interactive tutorials</span><span class="sxs-lookup"><span data-stu-id="7dc7c-103">Use Azure Data Lake Analytics interactive tutorials</span></span>
<span data-ttu-id="7dc7c-104">The Azure portal provides an interactive tutorial for you to get started with Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-104">The Azure portal provides an interactive tutorial for you to get started with Data Lake Analytics.</span></span> <span data-ttu-id="7dc7c-105">This article shows you how to go through the tutorial for analyzing website logs.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-105">This article shows you how to go through the tutorial for analyzing website logs.</span></span>

> [!NOTE]
> <span data-ttu-id="7dc7c-106">If you want to go through the same tutorial using Visual Studio, see [Analyze website logs using Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="7dc7c-106">If you want to go through the same tutorial using Visual Studio, see [Analyze website logs using Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
> <span data-ttu-id="7dc7c-107">More interactive tutorials to be added to the portal.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-107">More interactive tutorials to be added to the portal.</span></span>
> 
> 

<span data-ttu-id="7dc7c-108">For other tutorials, see:</span><span class="sxs-lookup"><span data-stu-id="7dc7c-108">For other tutorials, see:</span></span>

* [<span data-ttu-id="7dc7c-109">Get started with Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="7dc7c-109">Get started with Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="7dc7c-110">Get started with Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7dc7c-110">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="7dc7c-111">Get started with Data Lake Analytics using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="7dc7c-111">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
* [<span data-ttu-id="7dc7c-112">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7dc7c-112">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md) 

<span data-ttu-id="7dc7c-113">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="7dc7c-113">**Prerequisites**</span></span>

<span data-ttu-id="7dc7c-114">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="7dc7c-114">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="7dc7c-115">**A Data Lake Analytics account**.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-115">**A Data Lake Analytics account**.</span></span>  <span data-ttu-id="7dc7c-116">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7dc7c-116">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="7dc7c-117">Create Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="7dc7c-117">Create Data Lake Analytics account</span></span>
<span data-ttu-id="7dc7c-118">You must have a Data Lake Analytics account before you can run any jobs.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-118">You must have a Data Lake Analytics account before you can run any jobs.</span></span>

<span data-ttu-id="7dc7c-119">Each Data Lake Analytics account has an [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md) account dependency, the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-119">Each Data Lake Analytics account has an [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md) account dependency, the default Data Lake Store account.</span></span>  <span data-ttu-id="7dc7c-120">In this tutorial, you will create the default Data Lake Store account with the Analytics account, but you can create it beforehand as well.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-120">In this tutorial, you will create the default Data Lake Store account with the Analytics account, but you can create it beforehand as well.</span></span>

<span data-ttu-id="7dc7c-121">**To create a Data Lake Analytics account**</span><span class="sxs-lookup"><span data-stu-id="7dc7c-121">**To create a Data Lake Analytics account**</span></span>

1. <span data-ttu-id="7dc7c-122">Sign on to the [Azure portal](https://portal.azure.com/signin/index/?Microsoft_Azure_Kona=true&Microsoft_Azure_DataLake=true&hubsExtension_ItemHideKey=AzureDataLake_BigStorage%2cAzureKona_BigCompute).</span><span class="sxs-lookup"><span data-stu-id="7dc7c-122">Sign on to the [Azure portal](https://portal.azure.com/signin/index/?Microsoft_Azure_Kona=true&Microsoft_Azure_DataLake=true&hubsExtension_ItemHideKey=AzureDataLake_BigStorage%2cAzureKona_BigCompute).</span></span>
2. <span data-ttu-id="7dc7c-123">Click **Microsoft Azure** in the upper left corner to open the StartBoard.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-123">Click **Microsoft Azure** in the upper left corner to open the StartBoard.</span></span>
3. <span data-ttu-id="7dc7c-124">Click the **Marketplace** tile.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-124">Click the **Marketplace** tile.</span></span>  
4. <span data-ttu-id="7dc7c-125">Type **Azure Data Lake Analytics** in the search box on the **Everything** blade, and the press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-125">Type **Azure Data Lake Analytics** in the search box on the **Everything** blade, and the press **ENTER**.</span></span> <span data-ttu-id="7dc7c-126">You shall see **Azure Data Lake Analytics** in the list.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-126">You shall see **Azure Data Lake Analytics** in the list.</span></span>
5. <span data-ttu-id="7dc7c-127">Click **Azure Data Lake Analytics** from the list.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-127">Click **Azure Data Lake Analytics** from the list.</span></span>
6. <span data-ttu-id="7dc7c-128">Click **Create** on the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-128">Click **Create** on the bottom of the blade.</span></span>
7. <span data-ttu-id="7dc7c-129">Type or select:</span><span class="sxs-lookup"><span data-stu-id="7dc7c-129">Type or select:</span></span>
   
    ![Azure Data Lake Analytics portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-portal/data-lake-analytics-portal-create-adla.png)
   
   * <span data-ttu-id="7dc7c-131">**Name**: Name the Analytics account.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-131">**Name**: Name the Analytics account.</span></span>
   * <span data-ttu-id="7dc7c-132">**Data Lake Store**: Each Data Lake Analytics account has a dependent Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-132">**Data Lake Store**: Each Data Lake Analytics account has a dependent Data Lake Store account.</span></span> <span data-ttu-id="7dc7c-133">The Data Lake Analytics account and the dependent Data Lake Store account must be located in the same Azure data center.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-133">The Data Lake Analytics account and the dependent Data Lake Store account must be located in the same Azure data center.</span></span> <span data-ttu-id="7dc7c-134">Follow the instruction to create a Data Lake Store account, or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-134">Follow the instruction to create a Data Lake Store account, or select an existing one.</span></span>
   * <span data-ttu-id="7dc7c-135">**Subscription**: Choose the Azure subscription used for the Analytics account.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-135">**Subscription**: Choose the Azure subscription used for the Analytics account.</span></span>
   * <span data-ttu-id="7dc7c-136">**Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-136">**Resource Group**.</span></span> <span data-ttu-id="7dc7c-137">Select an existing Azure Resource Group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-137">Select an existing Azure Resource Group or create a new one.</span></span> <span data-ttu-id="7dc7c-138">Applications are typically made up of many components, for example a web app, database, database server, storage, and third party services.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-138">Applications are typically made up of many components, for example a web app, database, database server, storage, and third party services.</span></span> <span data-ttu-id="7dc7c-139">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-139">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="7dc7c-140">You can deploy, update, monitor, or delete the resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-140">You can deploy, update, monitor, or delete the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="7dc7c-141">You use a template for deployment and that template can work for different environments such as testing, staging,and production.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-141">You use a template for deployment and that template can work for different environments such as testing, staging,and production.</span></span> <span data-ttu-id="7dc7c-142">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-142">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="7dc7c-143">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7dc7c-143">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 
   * <span data-ttu-id="7dc7c-144">**Location**.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-144">**Location**.</span></span> <span data-ttu-id="7dc7c-145">Select an Azure data center for the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-145">Select an Azure data center for the Data Lake Analytics account.</span></span> 
8. <span data-ttu-id="7dc7c-146">Select **Pin to Startboard**.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-146">Select **Pin to Startboard**.</span></span> <span data-ttu-id="7dc7c-147">This is required for following this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-147">This is required for following this tutorial.</span></span>
9. <span data-ttu-id="7dc7c-148">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-148">Click **Create**.</span></span> <span data-ttu-id="7dc7c-149">It takes you to the portal StartBoard.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-149">It takes you to the portal StartBoard.</span></span> <span data-ttu-id="7dc7c-150">A new tile is added to the Home page with the label showing "Deploying Azure Data Lake Analytics."</span><span class="sxs-lookup"><span data-stu-id="7dc7c-150">A new tile is added to the Home page with the label showing "Deploying Azure Data Lake Analytics."</span></span> <span data-ttu-id="7dc7c-151">It takes a few moments to create a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-151">It takes a few moments to create a Data Lake Analytics account.</span></span> <span data-ttu-id="7dc7c-152">When the account is created, the portal opens the account on a new blade.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-152">When the account is created, the portal opens the account on a new blade.</span></span>
   
    ![Azure Data Lake Analytics portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-portal/data-lake-analytics-portal-blade.png)

## <a name="run-website-log-analysis-interactive-tutorial"></a><span data-ttu-id="7dc7c-154">Run Website Log Analysis interactive tutorial</span><span class="sxs-lookup"><span data-stu-id="7dc7c-154">Run Website Log Analysis interactive tutorial</span></span>
<span data-ttu-id="7dc7c-155">**To open the Website Log Analytics interactive tutorial**</span><span class="sxs-lookup"><span data-stu-id="7dc7c-155">**To open the Website Log Analytics interactive tutorial**</span></span>

1. <span data-ttu-id="7dc7c-156">From the Portal, click **Microsoft Azure** from the left menu to open the StartBoard.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-156">From the Portal, click **Microsoft Azure** from the left menu to open the StartBoard.</span></span>
2. <span data-ttu-id="7dc7c-157">Click the tile that is linked to your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-157">Click the tile that is linked to your Data Lake Analytics account.</span></span>
3. <span data-ttu-id="7dc7c-158">Click **Explore interactive tutorials** from the **Essentials** bar.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-158">Click **Explore interactive tutorials** from the **Essentials** bar.</span></span>
   
    ![Data Lake Analytics interactive tutorials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-use-interactive-tutorials/data-lake-analytics-explore-interactive-tutorials.png)
4. <span data-ttu-id="7dc7c-160">If you see an orange warning saying "Samples not set up, click ...", click **Copy Sample Data** to copy the sample data to the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-160">If you see an orange warning saying "Samples not set up, click ...", click **Copy Sample Data** to copy the sample data to the default Data Lake Store account.</span></span> <span data-ttu-id="7dc7c-161">The interactive tutorial needs the data to run.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-161">The interactive tutorial needs the data to run.</span></span>
5. <span data-ttu-id="7dc7c-162">From the **Interactive Tutorials** blade, click **Website Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-162">From the **Interactive Tutorials** blade, click **Website Log Analytics**.</span></span> <span data-ttu-id="7dc7c-163">The portal opens the tutorial in a new portal blade.</span><span class="sxs-lookup"><span data-stu-id="7dc7c-163">The portal opens the tutorial in a new portal blade.</span></span>
6. <span data-ttu-id="7dc7c-164">Click **Introduction** and then follow the instructions</span><span class="sxs-lookup"><span data-stu-id="7dc7c-164">Click **Introduction** and then follow the instructions</span></span>

## <a name="see-also"></a><span data-ttu-id="7dc7c-165">See also</span><span class="sxs-lookup"><span data-stu-id="7dc7c-165">See also</span></span>
* [<span data-ttu-id="7dc7c-166">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7dc7c-166">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="7dc7c-167">Get started with Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="7dc7c-167">Get started with Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="7dc7c-168">Get started with Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7dc7c-168">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="7dc7c-169">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7dc7c-169">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="7dc7c-170">Analyze Website logs using Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7dc7c-170">Analyze Website logs using Azure Data Lake Analytics</span></span>](data-lake-analytics-analyze-weblogs.md)




