---
title: Get started with Microsoft Power BI Embedded
description: Power BI Embedded, add interactive Power BI reports into your business intelligence application
services: power-bi-embedded
documentationcenter: ''
author: guyinacube
manager: erikre
editor: ''
tags: ''
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 3f04727fdbfc290c8f9c5f19dc14774f869adf57
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671016"
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="faf9f-103">Get started with Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="faf9f-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="faf9f-104">**Power BI Embedded** is an Azure service that enables application developers to add interactive Power BI reports into their own applications.</span><span class="sxs-lookup"><span data-stu-id="faf9f-104">**Power BI Embedded** is an Azure service that enables application developers to add interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="faf9f-105">**Power BI Embedded** works with existing applications without needing redesign or changing the way users sign in.</span><span class="sxs-lookup"><span data-stu-id="faf9f-105">**Power BI Embedded** works with existing applications without needing redesign or changing the way users sign in.</span></span>

<span data-ttu-id="faf9f-106">Resources for **Microsoft Power BI Embedded** are provisioned through the [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="faf9f-106">Resources for **Microsoft Power BI Embedded** are provisioned through the [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="faf9f-107">In this case, the resource you provision is a **Power BI Workspace Collection**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-107">In this case, the resource you provision is a **Power BI Workspace Collection**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="faf9f-108">Create a workspace collection</span><span class="sxs-lookup"><span data-stu-id="faf9f-108">Create a workspace collection</span></span>

<span data-ttu-id="faf9f-109">A **Workspace Collection** is the top-level Azure resource and a container for the content that will be embedded in your application.</span><span class="sxs-lookup"><span data-stu-id="faf9f-109">A **Workspace Collection** is the top-level Azure resource and a container for the content that will be embedded in your application.</span></span> <span data-ttu-id="faf9f-110">A **Workspace Collection** can be created in two ways::</span><span class="sxs-lookup"><span data-stu-id="faf9f-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="faf9f-111">Manually using the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="faf9f-111">Manually using the Azure Portal</span></span>
* <span data-ttu-id="faf9f-112">Programmatically using the Azure Resource Manager(ARM) APIs</span><span class="sxs-lookup"><span data-stu-id="faf9f-112">Programmatically using the Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="faf9f-113">Let's walk through the steps to build a **Workspace Collection** using the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="faf9f-113">Let's walk through the steps to build a **Workspace Collection** using the Azure Portal.</span></span>

1. <span data-ttu-id="faf9f-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="faf9f-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="faf9f-115">Click **+ New** on the top panel.</span><span class="sxs-lookup"><span data-stu-id="faf9f-115">Click **+ New** on the top panel.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="faf9f-116">Under **Data + Analytics** click **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="faf9f-117">On the **Workspace Collection Blade**, enter the required information.</span><span class="sxs-lookup"><span data-stu-id="faf9f-117">On the **Workspace Collection Blade**, enter the required information.</span></span> <span data-ttu-id="faf9f-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="faf9f-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="faf9f-119">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-119">Click **Create**.</span></span>

<span data-ttu-id="faf9f-120">The **Workspace Collection** will take a few moments to provision.</span><span class="sxs-lookup"><span data-stu-id="faf9f-120">The **Workspace Collection** will take a few moments to provision.</span></span> <span data-ttu-id="faf9f-121">When completed, you'll be taken to the **Workspace Collection Blade**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-121">When completed, you'll be taken to the **Workspace Collection Blade**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="faf9f-122">The **Creation Blade** contains the information you need to call the APIs that create workspaces and deploy content to them.</span><span class="sxs-lookup"><span data-stu-id="faf9f-122">The **Creation Blade** contains the information you need to call the APIs that create workspaces and deploy content to them.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="faf9f-123">View Power BI API access keys</span><span class="sxs-lookup"><span data-stu-id="faf9f-123">View Power BI API access keys</span></span>

<span data-ttu-id="faf9f-124">One of the most important pieces of information needed to call the Power BI REST APIs are the **Access Keys**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-124">One of the most important pieces of information needed to call the Power BI REST APIs are the **Access Keys**.</span></span> <span data-ttu-id="faf9f-125">These are used to generate the **app tokens** that are used to authenticate your API requests.</span><span class="sxs-lookup"><span data-stu-id="faf9f-125">These are used to generate the **app tokens** that are used to authenticate your API requests.</span></span> <span data-ttu-id="faf9f-126">To view your **Access Keys**, click **Access Keys** on the **Settings Blade**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-126">To view your **Access Keys**, click **Access Keys** on the **Settings Blade**.</span></span> <span data-ttu-id="faf9f-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="faf9f-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="faf9f-128">You'll'notice that you have two keys.</span><span class="sxs-lookup"><span data-stu-id="faf9f-128">You'll'notice that you have two keys.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="faf9f-129">Copy these keys and store them securely in your application.</span><span class="sxs-lookup"><span data-stu-id="faf9f-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="faf9f-130">It's very important that you treat these keys as you would a password, because they'll provide access to all the content in your **Workspace Collection**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-130">It's very important that you treat these keys as you would a password, because they'll provide access to all the content in your **Workspace Collection**.</span></span>

<span data-ttu-id="faf9f-131">While two keys are listed, only one key is needed at a particular time.</span><span class="sxs-lookup"><span data-stu-id="faf9f-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="faf9f-132">The second key is provided so you can periodically regenerate keys without interrupting access to the service.</span><span class="sxs-lookup"><span data-stu-id="faf9f-132">The second key is provided so you can periodically regenerate keys without interrupting access to the service.</span></span>

<span data-ttu-id="faf9f-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span><span class="sxs-lookup"><span data-stu-id="faf9f-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="faf9f-134">Before you learn how to import a report, the next section describes creating Power BI datasets and reports to embed into an app.</span><span class="sxs-lookup"><span data-stu-id="faf9f-134">Before you learn how to import a report, the next section describes creating Power BI datasets and reports to embed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="faf9f-135">Working with workspaces</span><span class="sxs-lookup"><span data-stu-id="faf9f-135">Working with workspaces</span></span>

<span data-ttu-id="faf9f-136">After you have created your workspace collection, you will need to create a workspace that will house your reports and datasets.</span><span class="sxs-lookup"><span data-stu-id="faf9f-136">After you have created your workspace collection, you will need to create a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="faf9f-137">To create a workspace, you will need to use the [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="faf9f-137">To create a workspace, you will need to use the [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="faf9f-138">Create Power BI datasets and reports to embed into an app using Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="faf9f-138">Create Power BI datasets and reports to embed into an app using Power BI Desktop</span></span>

<span data-ttu-id="faf9f-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need to create the Power BI datasets and reports that you want to embed.</span><span class="sxs-lookup"><span data-stu-id="faf9f-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need to create the Power BI datasets and reports that you want to embed.</span></span> <span data-ttu-id="faf9f-140">Datasets and reports can be created by using **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="faf9f-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span><span class="sxs-lookup"><span data-stu-id="faf9f-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="faf9f-142">Or, to quickly get started, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="faf9f-142">Or, to quickly get started, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="faf9f-143">To learn more about how to use **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="faf9f-143">To learn more about how to use **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="faf9f-144">With **Power BI Desktop**, you connect to your data source by importing a copy of the data into **Power BI Desktop** or connecting directly to the data source using **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-144">With **Power BI Desktop**, you connect to your data source by importing a copy of the data into **Power BI Desktop** or connecting directly to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="faf9f-145">Here are the differences between using **Import** and **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-145">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="faf9f-146">Import</span><span class="sxs-lookup"><span data-stu-id="faf9f-146">Import</span></span> | <span data-ttu-id="faf9f-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="faf9f-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="faf9f-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="faf9f-149">As you work with visualizations, **Power BI Desktop** queries a copy of the data.</span><span class="sxs-lookup"><span data-stu-id="faf9f-149">As you work with visualizations, **Power BI Desktop** queries a copy of the data.</span></span> <span data-ttu-id="faf9f-150">To see any changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span><span class="sxs-lookup"><span data-stu-id="faf9f-150">To see any changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="faf9f-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="faf9f-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="faf9f-152">As you work with visualizations, **Power BI Desktop** queries the underlying data source, which means you're always viewing current data.</span><span class="sxs-lookup"><span data-stu-id="faf9f-152">As you work with visualizations, **Power BI Desktop** queries the underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="faf9f-153">For more about connecting to a data source, see [Connect to a data source](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="faf9f-153">For more about connecting to a data source, see [Connect to a data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="faf9f-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span><span class="sxs-lookup"><span data-stu-id="faf9f-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="faf9f-155">This file contains your report.</span><span class="sxs-lookup"><span data-stu-id="faf9f-155">This file contains your report.</span></span> <span data-ttu-id="faf9f-156">In addition, if you import data the PBIX contains the complete dataset, or if you use **DirectQuery**, the PBIX contains just a dataset schema.</span><span class="sxs-lookup"><span data-stu-id="faf9f-156">In addition, if you import data the PBIX contains the complete dataset, or if you use **DirectQuery**, the PBIX contains just a dataset schema.</span></span> <span data-ttu-id="faf9f-157">You programmatically deploy the PBIX into your workspace using the [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="faf9f-157">You programmatically deploy the PBIX into your workspace using the [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="faf9f-158">**Power BI Embedded** has additional APIs to change the server and database that your dataset is pointing to and set a service account credential that the dataset will use to connect to your database.</span><span class="sxs-lookup"><span data-stu-id="faf9f-158">**Power BI Embedded** has additional APIs to change the server and database that your dataset is pointing to and set a service account credential that the dataset will use to connect to your database.</span></span> <span data-ttu-id="faf9f-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span><span class="sxs-lookup"><span data-stu-id="faf9f-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="faf9f-160">Create Power BI datasets and reports using APIs</span><span class="sxs-lookup"><span data-stu-id="faf9f-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="faf9f-161">Datsets</span><span class="sxs-lookup"><span data-stu-id="faf9f-161">Datsets</span></span>

<span data-ttu-id="faf9f-162">You can create datasets within Power BI Embedded using the REST API.</span><span class="sxs-lookup"><span data-stu-id="faf9f-162">You can create datasets within Power BI Embedded using the REST API.</span></span> <span data-ttu-id="faf9f-163">You can then push data into your dataset.</span><span class="sxs-lookup"><span data-stu-id="faf9f-163">You can then push data into your dataset.</span></span> <span data-ttu-id="faf9f-164">This allows you to work with data without the need of Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="faf9f-164">This allows you to work with data without the need of Power BI Desktop.</span></span> <span data-ttu-id="faf9f-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span><span class="sxs-lookup"><span data-stu-id="faf9f-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="faf9f-166">Reports</span><span class="sxs-lookup"><span data-stu-id="faf9f-166">Reports</span></span>

<span data-ttu-id="faf9f-167">You can create a report from a dataset directly in your application using the JavaScript API.</span><span class="sxs-lookup"><span data-stu-id="faf9f-167">You can create a report from a dataset directly in your application using the JavaScript API.</span></span> <span data-ttu-id="faf9f-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span><span class="sxs-lookup"><span data-stu-id="faf9f-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="faf9f-169">See Also</span><span class="sxs-lookup"><span data-stu-id="faf9f-169">See Also</span></span>

[<span data-ttu-id="faf9f-170">Get started with sample</span><span class="sxs-lookup"><span data-stu-id="faf9f-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="faf9f-171">Authenticating and authorizing in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="faf9f-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="faf9f-172">Embed a report</span><span class="sxs-lookup"><span data-stu-id="faf9f-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="faf9f-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="faf9f-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="faf9f-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="faf9f-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="faf9f-175">JavaScript Embed Sample</span><span class="sxs-lookup"><span data-stu-id="faf9f-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="faf9f-176">More questions?</span><span class="sxs-lookup"><span data-stu-id="faf9f-176">More questions?</span></span> [<span data-ttu-id="faf9f-177">Try the Power BI Community</span><span class="sxs-lookup"><span data-stu-id="faf9f-177">Try the Power BI Community</span></span>](http://community.powerbi.com/)







