---
title: Analyze data in Data Lake Store by using Power BI | Microsoft Docs
description: Use Power BI to analyze data stored in Azure Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: e2a9b5cb5021092c43ff3386df7fe33f3863c1d1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556780"
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a><span data-ttu-id="5c53a-103">Analyze data in Data Lake Store by using Power BI</span><span class="sxs-lookup"><span data-stu-id="5c53a-103">Analyze data in Data Lake Store by using Power BI</span></span>
<span data-ttu-id="5c53a-104">In this article you will learn how to use Power BI Desktop to analyze and visualize data stored in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5c53a-104">In this article you will learn how to use Power BI Desktop to analyze and visualize data stored in Azure Data Lake Store.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c53a-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5c53a-105">Prerequisites</span></span>
<span data-ttu-id="5c53a-106">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="5c53a-106">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="5c53a-107">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-107">**An Azure subscription**.</span></span> <span data-ttu-id="5c53a-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c53a-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5c53a-109">**Azure Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="5c53a-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c53a-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="5c53a-111">This article assumes that you have already created a Data Lake Store account, called **mybidatalakestore**, and uploaded a sample data file (**Drivers.txt**) to it.</span><span class="sxs-lookup"><span data-stu-id="5c53a-111">This article assumes that you have already created a Data Lake Store account, called **mybidatalakestore**, and uploaded a sample data file (**Drivers.txt**) to it.</span></span> <span data-ttu-id="5c53a-112">This sample file is available for download from [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="5c53a-112">This sample file is available for download from [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span>
* <span data-ttu-id="5c53a-113">**Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-113">**Power BI Desktop**.</span></span> <span data-ttu-id="5c53a-114">You can download this from [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="5c53a-114">You can download this from [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331).</span></span> 

## <a name="create-a-report-in-power-bi-desktop"></a><span data-ttu-id="5c53a-115">Create a report in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="5c53a-115">Create a report in Power BI Desktop</span></span>
1. <span data-ttu-id="5c53a-116">Launch Power BI Desktop on your computer.</span><span class="sxs-lookup"><span data-stu-id="5c53a-116">Launch Power BI Desktop on your computer.</span></span>
2. <span data-ttu-id="5c53a-117">From the **Home** ribbon, click **Get Data**, and then click More.</span><span class="sxs-lookup"><span data-stu-id="5c53a-117">From the **Home** ribbon, click **Get Data**, and then click More.</span></span> <span data-ttu-id="5c53a-118">In the **Get Data** dialog box, click **Azure**, click **Azure Data Lake Store**, and then click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-118">In the **Get Data** dialog box, click **Azure**, click **Azure Data Lake Store**, and then click **Connect**.</span></span>
   
    <span data-ttu-id="5c53a-119">![Connect to Data Lake Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect to Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5c53a-119">![Connect to Data Lake Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect to Data Lake Store")</span></span>
3. <span data-ttu-id="5c53a-120">If you see a dialog box about the connector being in a development phase, opt to continue.</span><span class="sxs-lookup"><span data-stu-id="5c53a-120">If you see a dialog box about the connector being in a development phase, opt to continue.</span></span>
4. <span data-ttu-id="5c53a-121">In the **Microsoft Azure Data Lake Store** dialog box, provide the URL to your Data Lake Store account, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-121">In the **Microsoft Azure Data Lake Store** dialog box, provide the URL to your Data Lake Store account, and then click **OK**.</span></span>
   
    <span data-ttu-id="5c53a-122">![URL for Data Lake Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL for Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5c53a-122">![URL for Data Lake Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL for Data Lake Store")</span></span>
5. <span data-ttu-id="5c53a-123">In the next dialog box, click **Sign in** to sign into Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="5c53a-123">In the next dialog box, click **Sign in** to sign into Data Lake Store account.</span></span> <span data-ttu-id="5c53a-124">You will be redirected to your organization's sign in page.</span><span class="sxs-lookup"><span data-stu-id="5c53a-124">You will be redirected to your organization's sign in page.</span></span> <span data-ttu-id="5c53a-125">Follow the prompts to sign into the account.</span><span class="sxs-lookup"><span data-stu-id="5c53a-125">Follow the prompts to sign into the account.</span></span>
   
    <span data-ttu-id="5c53a-126">![Sign into Data Lake Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Sign into Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5c53a-126">![Sign into Data Lake Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Sign into Data Lake Store")</span></span>
6. <span data-ttu-id="5c53a-127">After you have successfully signed in, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-127">After you have successfully signed in, click **Connect**.</span></span>
   
    <span data-ttu-id="5c53a-128">![Connect to Data Lake Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect to Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5c53a-128">![Connect to Data Lake Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect to Data Lake Store")</span></span>
7. <span data-ttu-id="5c53a-129">The next dialog box shows the file that you uploaded to your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="5c53a-129">The next dialog box shows the file that you uploaded to your Data Lake Store account.</span></span> <span data-ttu-id="5c53a-130">Verify the info and then click **Load**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-130">Verify the info and then click **Load**.</span></span>
   
    <span data-ttu-id="5c53a-131">![Load data from Data Lake Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Load data from Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="5c53a-131">![Load data from Data Lake Store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Load data from Data Lake Store")</span></span>
8. <span data-ttu-id="5c53a-132">After the data has been successfully loaded into Power BI, you will see the following fields in the **Fields** tab.</span><span class="sxs-lookup"><span data-stu-id="5c53a-132">After the data has been successfully loaded into Power BI, you will see the following fields in the **Fields** tab.</span></span>
   
    <span data-ttu-id="5c53a-133">![Imported fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/imported-fields.png "Imported fields")</span><span class="sxs-lookup"><span data-stu-id="5c53a-133">![Imported fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/imported-fields.png "Imported fields")</span></span>
   
    <span data-ttu-id="5c53a-134">However, to visualize and analyze the data, we prefer the data to be available per the following fields</span><span class="sxs-lookup"><span data-stu-id="5c53a-134">However, to visualize and analyze the data, we prefer the data to be available per the following fields</span></span>
   
    <span data-ttu-id="5c53a-135">![Desired fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/desired-fields.png "Desired fields")</span><span class="sxs-lookup"><span data-stu-id="5c53a-135">![Desired fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/desired-fields.png "Desired fields")</span></span>
   
    <span data-ttu-id="5c53a-136">In the next steps, we will update the query to convert the imported data in the desired format.</span><span class="sxs-lookup"><span data-stu-id="5c53a-136">In the next steps, we will update the query to convert the imported data in the desired format.</span></span>
9. <span data-ttu-id="5c53a-137">From the **Home** ribbon, click **Edit Queries**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-137">From the **Home** ribbon, click **Edit Queries**.</span></span>
   
    <span data-ttu-id="5c53a-138">![Edit queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/edit-queries.png "Edit queries")</span><span class="sxs-lookup"><span data-stu-id="5c53a-138">![Edit queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/edit-queries.png "Edit queries")</span></span>
10. <span data-ttu-id="5c53a-139">In the Query Editor, under the **Content** column, click **Binary**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-139">In the Query Editor, under the **Content** column, click **Binary**.</span></span>
    
    <span data-ttu-id="5c53a-140">![Edit queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/convert-query1.png "Edit queries")</span><span class="sxs-lookup"><span data-stu-id="5c53a-140">![Edit queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/convert-query1.png "Edit queries")</span></span>
11. <span data-ttu-id="5c53a-141">You will see a file icon, that represents the **Drivers.txt** file that you uploaded.</span><span class="sxs-lookup"><span data-stu-id="5c53a-141">You will see a file icon, that represents the **Drivers.txt** file that you uploaded.</span></span> <span data-ttu-id="5c53a-142">Right-click the file, and click **CSV**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-142">Right-click the file, and click **CSV**.</span></span>    
    
    <span data-ttu-id="5c53a-143">![Edit queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/convert-query2.png "Edit queries")</span><span class="sxs-lookup"><span data-stu-id="5c53a-143">![Edit queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/convert-query2.png "Edit queries")</span></span>
12. <span data-ttu-id="5c53a-144">You should see an output as shown below.</span><span class="sxs-lookup"><span data-stu-id="5c53a-144">You should see an output as shown below.</span></span> <span data-ttu-id="5c53a-145">Your data is now available in a format that you can use to create visualizations.</span><span class="sxs-lookup"><span data-stu-id="5c53a-145">Your data is now available in a format that you can use to create visualizations.</span></span>
    
    <span data-ttu-id="5c53a-146">![Edit queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/convert-query3.png "Edit queries")</span><span class="sxs-lookup"><span data-stu-id="5c53a-146">![Edit queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/convert-query3.png "Edit queries")</span></span>
13. <span data-ttu-id="5c53a-147">From the **Home** ribbon, click **Close and Apply**, and then click **Close and Apply**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-147">From the **Home** ribbon, click **Close and Apply**, and then click **Close and Apply**.</span></span>
    
    <span data-ttu-id="5c53a-148">![Edit queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/load-edited-query.png "Edit queries")</span><span class="sxs-lookup"><span data-stu-id="5c53a-148">![Edit queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/load-edited-query.png "Edit queries")</span></span>
14. <span data-ttu-id="5c53a-149">Once the query is updated, the **Fields** tab will show the new fields available for visualization.</span><span class="sxs-lookup"><span data-stu-id="5c53a-149">Once the query is updated, the **Fields** tab will show the new fields available for visualization.</span></span>
    
    <span data-ttu-id="5c53a-150">![Updated fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/updated-query-fields.png "Updated fields")</span><span class="sxs-lookup"><span data-stu-id="5c53a-150">![Updated fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/updated-query-fields.png "Updated fields")</span></span>
15. <span data-ttu-id="5c53a-151">Let us create a pie chart to represent the drivers in each city for a given country.</span><span class="sxs-lookup"><span data-stu-id="5c53a-151">Let us create a pie chart to represent the drivers in each city for a given country.</span></span> <span data-ttu-id="5c53a-152">To do so, make the following selections.</span><span class="sxs-lookup"><span data-stu-id="5c53a-152">To do so, make the following selections.</span></span>
    
    1. <span data-ttu-id="5c53a-153">From the Visualizations tab, click the symbol for a pie chart.</span><span class="sxs-lookup"><span data-stu-id="5c53a-153">From the Visualizations tab, click the symbol for a pie chart.</span></span>
       
        <span data-ttu-id="5c53a-154">![Create pie chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/create-pie-chart.png "Create pie chart")</span><span class="sxs-lookup"><span data-stu-id="5c53a-154">![Create pie chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/create-pie-chart.png "Create pie chart")</span></span>
    2. <span data-ttu-id="5c53a-155">The columns that we are going to use are **Column 4** (name of the city) and **Column 7** (name of the country).</span><span class="sxs-lookup"><span data-stu-id="5c53a-155">The columns that we are going to use are **Column 4** (name of the city) and **Column 7** (name of the country).</span></span> <span data-ttu-id="5c53a-156">Drag these columns from **Fields** tab to **Visualizations** tab as shown below.</span><span class="sxs-lookup"><span data-stu-id="5c53a-156">Drag these columns from **Fields** tab to **Visualizations** tab as shown below.</span></span>
       
        <span data-ttu-id="5c53a-157">![Create visualizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/create-visualizations.png "Create visualizations")</span><span class="sxs-lookup"><span data-stu-id="5c53a-157">![Create visualizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/create-visualizations.png "Create visualizations")</span></span>
    3. <span data-ttu-id="5c53a-158">The pie chart should now resemble like the one shown below.</span><span class="sxs-lookup"><span data-stu-id="5c53a-158">The pie chart should now resemble like the one shown below.</span></span>
       
        <span data-ttu-id="5c53a-159">![Pie chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/pie-chart.png "Create visualizations")</span><span class="sxs-lookup"><span data-stu-id="5c53a-159">![Pie chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/pie-chart.png "Create visualizations")</span></span>
16. <span data-ttu-id="5c53a-160">By selecting a specific country from the page level filters, you can now see the number of drivers in each city of the selected country.</span><span class="sxs-lookup"><span data-stu-id="5c53a-160">By selecting a specific country from the page level filters, you can now see the number of drivers in each city of the selected country.</span></span> <span data-ttu-id="5c53a-161">For example, under the **Visualizations** tab, under **Page level filters**, select **Brazil**.</span><span class="sxs-lookup"><span data-stu-id="5c53a-161">For example, under the **Visualizations** tab, under **Page level filters**, select **Brazil**.</span></span>
    
    <span data-ttu-id="5c53a-162">![Select a country](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/select-country.png "Select a country")</span><span class="sxs-lookup"><span data-stu-id="5c53a-162">![Select a country](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/select-country.png "Select a country")</span></span>
17. <span data-ttu-id="5c53a-163">The pie chart is automatically updated to display the drivers in the cities of Brazil.</span><span class="sxs-lookup"><span data-stu-id="5c53a-163">The pie chart is automatically updated to display the drivers in the cities of Brazil.</span></span>
    
    <span data-ttu-id="5c53a-164">![Drivers in a country](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/driver-per-country.png "Drivers per country")</span><span class="sxs-lookup"><span data-stu-id="5c53a-164">![Drivers in a country](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-power-bi/driver-per-country.png "Drivers per country")</span></span>
18. <span data-ttu-id="5c53a-165">From the **File** menu, click **Save** to save the visualization as a Power BI Desktop file.</span><span class="sxs-lookup"><span data-stu-id="5c53a-165">From the **File** menu, click **Save** to save the visualization as a Power BI Desktop file.</span></span>

## <a name="publish-report-to-power-bi-service"></a><span data-ttu-id="5c53a-166">Publish report to Power BI service</span><span class="sxs-lookup"><span data-stu-id="5c53a-166">Publish report to Power BI service</span></span>
<span data-ttu-id="5c53a-167">Once you have created the visualizations in Power BI Desktop, you can share it with others by publishing it to the Power BI service.</span><span class="sxs-lookup"><span data-stu-id="5c53a-167">Once you have created the visualizations in Power BI Desktop, you can share it with others by publishing it to the Power BI service.</span></span> <span data-ttu-id="5c53a-168">For instructions on how to do that, see [Publish from Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).</span><span class="sxs-lookup"><span data-stu-id="5c53a-168">For instructions on how to do that, see [Publish from Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).</span></span>

## <a name="see-also"></a><span data-ttu-id="5c53a-169">See also</span><span class="sxs-lookup"><span data-stu-id="5c53a-169">See also</span></span>
* [<span data-ttu-id="5c53a-170">Analyze data in Data Lake Store using Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5c53a-170">Analyze data in Data Lake Store using Data Lake Analytics</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)



















