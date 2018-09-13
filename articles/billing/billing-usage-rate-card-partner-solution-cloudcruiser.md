---
title: Cloud Cruiser and Microsoft Azure Billing API Integration | Microsoft Docs
description: Provides a unique perspective from Microsoft Azure Billing partner Cloud Cruiser, on their experiences integrating the Azure Billing APIs into their product.  This is especially useful for Azure and Cloud Cruiser customers that are interested in using/trying Cloud Cruiser for Microsoft Azure Pack.
services: ''
documentationcenter: ''
author: BryanLa
manager: ruchic
editor: ''
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: f41809b4435b0d34942bee674577d6ac78fe936d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555136"
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a><span data-ttu-id="5624d-104">Cloud Cruiser and Microsoft Azure Billing API Integration</span><span class="sxs-lookup"><span data-stu-id="5624d-104">Cloud Cruiser and Microsoft Azure Billing API Integration</span></span>
<span data-ttu-id="5624d-105">This article describes how the information collected from the new Microsoft Azure Billing APIs can be used in Cloud Cruiser for workflow cost simulation and analysis.</span><span class="sxs-lookup"><span data-stu-id="5624d-105">This article describes how the information collected from the new Microsoft Azure Billing APIs can be used in Cloud Cruiser for workflow cost simulation and analysis.</span></span>

## <a name="azure-ratecard-api"></a><span data-ttu-id="5624d-106">Azure RateCard API</span><span class="sxs-lookup"><span data-stu-id="5624d-106">Azure RateCard API</span></span>
<span data-ttu-id="5624d-107">The RateCard API provides rate information from Azure.</span><span class="sxs-lookup"><span data-stu-id="5624d-107">The RateCard API provides rate information from Azure.</span></span> <span data-ttu-id="5624d-108">After authenticating with the proper credentials, you can query the API to collect metadata about the services available on Azure, along with the rates associated with your Offer ID.</span><span class="sxs-lookup"><span data-stu-id="5624d-108">After authenticating with the proper credentials, you can query the API to collect metadata about the services available on Azure, along with the rates associated with your Offer ID.</span></span>

<span data-ttu-id="5624d-109">The following is a sample response from the API showing the prices for the A0 (Windows) instance:</span><span class="sxs-lookup"><span data-stu-id="5624d-109">The following is a sample response from the API showing the prices for the A0 (Windows) instance:</span></span>

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-to-azure-ratecard-api"></a><span data-ttu-id="5624d-110">Cloud Cruiser’s Interface to Azure RateCard API</span><span class="sxs-lookup"><span data-stu-id="5624d-110">Cloud Cruiser’s Interface to Azure RateCard API</span></span>
<span data-ttu-id="5624d-111">Cloud Cruiser can leverage the RateCard API information in different ways.</span><span class="sxs-lookup"><span data-stu-id="5624d-111">Cloud Cruiser can leverage the RateCard API information in different ways.</span></span> <span data-ttu-id="5624d-112">For this article, we will show how it can be used to make IaaS workload cost simulation and analysis.</span><span class="sxs-lookup"><span data-stu-id="5624d-112">For this article, we will show how it can be used to make IaaS workload cost simulation and analysis.</span></span>

<span data-ttu-id="5624d-113">To demonstrate this use case, imagine a workload of several instances running on Microsoft Azure Pack (WAP).</span><span class="sxs-lookup"><span data-stu-id="5624d-113">To demonstrate this use case, imagine a workload of several instances running on Microsoft Azure Pack (WAP).</span></span> <span data-ttu-id="5624d-114">The goal is to simulate this same workload on Azure, and estimate the costs of doing such migration.</span><span class="sxs-lookup"><span data-stu-id="5624d-114">The goal is to simulate this same workload on Azure, and estimate the costs of doing such migration.</span></span> <span data-ttu-id="5624d-115">In order to create this simulation, there are two main tasks to be performed:</span><span class="sxs-lookup"><span data-stu-id="5624d-115">In order to create this simulation, there are two main tasks to be performed:</span></span>

1. <span data-ttu-id="5624d-116">**Import and process the service information collected from the RateCard API.**</span><span class="sxs-lookup"><span data-stu-id="5624d-116">**Import and process the service information collected from the RateCard API.**</span></span> <span data-ttu-id="5624d-117">This task is also performed on the workbooks, where the extract from the RateCard API is transformed and published to a new rate plan.</span><span class="sxs-lookup"><span data-stu-id="5624d-117">This task is also performed on the workbooks, where the extract from the RateCard API is transformed and published to a new rate plan.</span></span> <span data-ttu-id="5624d-118">This new rate plan will be used on the simulations to estimate the Azure prices.</span><span class="sxs-lookup"><span data-stu-id="5624d-118">This new rate plan will be used on the simulations to estimate the Azure prices.</span></span>
2. <span data-ttu-id="5624d-119">**Normalize WAP services and Azure services for IaaS.**</span><span class="sxs-lookup"><span data-stu-id="5624d-119">**Normalize WAP services and Azure services for IaaS.**</span></span> <span data-ttu-id="5624d-120">By default, WAP services are based on individual resources (CPU, Memory Size, Disk Size, etc.) while Azure services are based on instance size (A0, A1, A2, etc.).</span><span class="sxs-lookup"><span data-stu-id="5624d-120">By default, WAP services are based on individual resources (CPU, Memory Size, Disk Size, etc.) while Azure services are based on instance size (A0, A1, A2, etc.).</span></span> <span data-ttu-id="5624d-121">This first task can be performed by Cloud Cruiser’s ETL engine, called workbooks, where these resources can be bundled on instance sizes, analogous to Azure instance services.</span><span class="sxs-lookup"><span data-stu-id="5624d-121">This first task can be performed by Cloud Cruiser’s ETL engine, called workbooks, where these resources can be bundled on instance sizes, analogous to Azure instance services.</span></span>

### <a name="import-data-from-the-ratecard-api"></a><span data-ttu-id="5624d-122">Import data from the RateCard API</span><span class="sxs-lookup"><span data-stu-id="5624d-122">Import data from the RateCard API</span></span>
<span data-ttu-id="5624d-123">Cloud Cruiser workbooks provide an automated way to collect and process information from the RateCard API.</span><span class="sxs-lookup"><span data-stu-id="5624d-123">Cloud Cruiser workbooks provide an automated way to collect and process information from the RateCard API.</span></span>  <span data-ttu-id="5624d-124">ETL (extract-transform-load) workbooks allow you to configure the collection, transformation, and publishing of data into the Cloud Cruiser database.</span><span class="sxs-lookup"><span data-stu-id="5624d-124">ETL (extract-transform-load) workbooks allow you to configure the collection, transformation, and publishing of data into the Cloud Cruiser database.</span></span>

<span data-ttu-id="5624d-125">Each workbook can have one or multiple collections, allowing you to correlate information from different sources to complement or augment the usage data.</span><span class="sxs-lookup"><span data-stu-id="5624d-125">Each workbook can have one or multiple collections, allowing you to correlate information from different sources to complement or augment the usage data.</span></span> <span data-ttu-id="5624d-126">The following two screenshots show how to create a new *collection* in an existing workbook, and importing information into the *collection* from the RateCard API:</span><span class="sxs-lookup"><span data-stu-id="5624d-126">The following two screenshots show how to create a new *collection* in an existing workbook, and importing information into the *collection* from the RateCard API:</span></span>

<span data-ttu-id="5624d-127">![Figure 1 - Creating a new collection][1]</span><span class="sxs-lookup"><span data-stu-id="5624d-127">![Figure 1 - Creating a new collection][1]</span></span>

<span data-ttu-id="5624d-128">![Figure 2 - Import data from the new collection][2]</span><span class="sxs-lookup"><span data-stu-id="5624d-128">![Figure 2 - Import data from the new collection][2]</span></span>

<span data-ttu-id="5624d-129">After importing the data into the workbook, it’s possible to create multiple steps and transformation processes, to modify and model the data.</span><span class="sxs-lookup"><span data-stu-id="5624d-129">After importing the data into the workbook, it’s possible to create multiple steps and transformation processes, to modify and model the data.</span></span> <span data-ttu-id="5624d-130">For this example, since we are only interested in infrastructure-as-a-Service (IaaS) we can use the transformation steps to remove unnecessary rows, or records, related to services other than IaaS.</span><span class="sxs-lookup"><span data-stu-id="5624d-130">For this example, since we are only interested in infrastructure-as-a-Service (IaaS) we can use the transformation steps to remove unnecessary rows, or records, related to services other than IaaS.</span></span>

<span data-ttu-id="5624d-131">The following screenshot shows the transformation steps used to process the data collected from RateCard API:</span><span class="sxs-lookup"><span data-stu-id="5624d-131">The following screenshot shows the transformation steps used to process the data collected from RateCard API:</span></span>

<span data-ttu-id="5624d-132">![Figure 3 - Transformation steps to process collected data from RateCard API][3]</span><span class="sxs-lookup"><span data-stu-id="5624d-132">![Figure 3 - Transformation steps to process collected data from RateCard API][3]</span></span>

### <a name="defining-new-services-and-rate-plans"></a><span data-ttu-id="5624d-133">Defining New Services and Rate Plans</span><span class="sxs-lookup"><span data-stu-id="5624d-133">Defining New Services and Rate Plans</span></span>
<span data-ttu-id="5624d-134">There are different ways to define services on Cloud Cruiser.</span><span class="sxs-lookup"><span data-stu-id="5624d-134">There are different ways to define services on Cloud Cruiser.</span></span> <span data-ttu-id="5624d-135">One of the options is to import the services from the usage data.</span><span class="sxs-lookup"><span data-stu-id="5624d-135">One of the options is to import the services from the usage data.</span></span> <span data-ttu-id="5624d-136">This method is commonly used when working with public clouds, where the services are already defined by the provider.</span><span class="sxs-lookup"><span data-stu-id="5624d-136">This method is commonly used when working with public clouds, where the services are already defined by the provider.</span></span>

<span data-ttu-id="5624d-137">A Rate Plan is a set of rates or prices that can be applied to different services, based on effective dates, or group of customers, among other options.</span><span class="sxs-lookup"><span data-stu-id="5624d-137">A Rate Plan is a set of rates or prices that can be applied to different services, based on effective dates, or group of customers, among other options.</span></span> <span data-ttu-id="5624d-138">Rate Plans can also be used on Cloud Cruiser to create simulation or “What-if” scenarios, to understand how changes in services can affect the total cost of a workload.</span><span class="sxs-lookup"><span data-stu-id="5624d-138">Rate Plans can also be used on Cloud Cruiser to create simulation or “What-if” scenarios, to understand how changes in services can affect the total cost of a workload.</span></span>

<span data-ttu-id="5624d-139">In this example, we will use the service information from the RateCard API to define new services in Cloud Cruiser.</span><span class="sxs-lookup"><span data-stu-id="5624d-139">In this example, we will use the service information from the RateCard API to define new services in Cloud Cruiser.</span></span> <span data-ttu-id="5624d-140">In the same way, we can use the rates associated to the services to create a new Rate Plan on Cloud Cruiser.</span><span class="sxs-lookup"><span data-stu-id="5624d-140">In the same way, we can use the rates associated to the services to create a new Rate Plan on Cloud Cruiser.</span></span>

<span data-ttu-id="5624d-141">At the end of the transformation process, it is possible to create a new step and publish the data from the RateCard API as new services and rates.</span><span class="sxs-lookup"><span data-stu-id="5624d-141">At the end of the transformation process, it is possible to create a new step and publish the data from the RateCard API as new services and rates.</span></span>

<span data-ttu-id="5624d-142">![Figure 4 - Publishing the data from the RateCard API as new Services and Rates][4]</span><span class="sxs-lookup"><span data-stu-id="5624d-142">![Figure 4 - Publishing the data from the RateCard API as new Services and Rates][4]</span></span>

### <a name="verify-azure-services-and-rates"></a><span data-ttu-id="5624d-143">Verify Azure Services and Rates</span><span class="sxs-lookup"><span data-stu-id="5624d-143">Verify Azure Services and Rates</span></span>
<span data-ttu-id="5624d-144">After publishing the services and rates, you can verify the list of imported services in Cloud Cruiser’s *Services* tab:</span><span class="sxs-lookup"><span data-stu-id="5624d-144">After publishing the services and rates, you can verify the list of imported services in Cloud Cruiser’s *Services* tab:</span></span>

<span data-ttu-id="5624d-145">![Figure 5 - Verifying the new Services][5]</span><span class="sxs-lookup"><span data-stu-id="5624d-145">![Figure 5 - Verifying the new Services][5]</span></span>

<span data-ttu-id="5624d-146">On the *Rate Plans* tab, you can check the new rate plan called “AzureSimulation” with the rates imported from the RateCard API.</span><span class="sxs-lookup"><span data-stu-id="5624d-146">On the *Rate Plans* tab, you can check the new rate plan called “AzureSimulation” with the rates imported from the RateCard API.</span></span>

<span data-ttu-id="5624d-147">![Figure 6 - Verifying the new Rate Plan and associated rates][6]</span><span class="sxs-lookup"><span data-stu-id="5624d-147">![Figure 6 - Verifying the new Rate Plan and associated rates][6]</span></span>

### <a name="normalize-wap-and-azure-services"></a><span data-ttu-id="5624d-148">Normalize WAP and Azure Services</span><span class="sxs-lookup"><span data-stu-id="5624d-148">Normalize WAP and Azure Services</span></span>
<span data-ttu-id="5624d-149">By default, WAP provides usage information based on the use of compute, memory, and network resources.</span><span class="sxs-lookup"><span data-stu-id="5624d-149">By default, WAP provides usage information based on the use of compute, memory, and network resources.</span></span> <span data-ttu-id="5624d-150">In Cloud Cruiser, you can define your services based directly on the allocation or metered usage of these resources.</span><span class="sxs-lookup"><span data-stu-id="5624d-150">In Cloud Cruiser, you can define your services based directly on the allocation or metered usage of these resources.</span></span> <span data-ttu-id="5624d-151">For example, you can set a basic rate for each hour of CPU usage, or charge the GB of memory allocated to an instance.</span><span class="sxs-lookup"><span data-stu-id="5624d-151">For example, you can set a basic rate for each hour of CPU usage, or charge the GB of memory allocated to an instance.</span></span>

<span data-ttu-id="5624d-152">For this example, in order to compare costs between WAP and Azure, we need to aggregate the resource usage on WAP into bundles, which can then be mapped to Azure services.</span><span class="sxs-lookup"><span data-stu-id="5624d-152">For this example, in order to compare costs between WAP and Azure, we need to aggregate the resource usage on WAP into bundles, which can then be mapped to Azure services.</span></span> <span data-ttu-id="5624d-153">This transformation can be implemented easily in the workbooks:</span><span class="sxs-lookup"><span data-stu-id="5624d-153">This transformation can be implemented easily in the workbooks:</span></span>

<span data-ttu-id="5624d-154">![Figure 7 - Transforming WAP data to normalize services][7]</span><span class="sxs-lookup"><span data-stu-id="5624d-154">![Figure 7 - Transforming WAP data to normalize services][7]</span></span>

<span data-ttu-id="5624d-155">The last step at the workbook is to publish the data into the Cloud Cruiser database.</span><span class="sxs-lookup"><span data-stu-id="5624d-155">The last step at the workbook is to publish the data into the Cloud Cruiser database.</span></span> <span data-ttu-id="5624d-156">During this step, the usage data is now bundled into services (that map to the Azure Services) and tied to default rates to create the charges.</span><span class="sxs-lookup"><span data-stu-id="5624d-156">During this step, the usage data is now bundled into services (that map to the Azure Services) and tied to default rates to create the charges.</span></span>

<span data-ttu-id="5624d-157">After finishing the workbook, you can automate the processing of the data, by adding a task on the scheduler and specifying the frequency and time for the workbook to run.</span><span class="sxs-lookup"><span data-stu-id="5624d-157">After finishing the workbook, you can automate the processing of the data, by adding a task on the scheduler and specifying the frequency and time for the workbook to run.</span></span>

<span data-ttu-id="5624d-158">![Figure 8 - Workbook scheduling][8]</span><span class="sxs-lookup"><span data-stu-id="5624d-158">![Figure 8 - Workbook scheduling][8]</span></span>

### <a name="create-reports-for-workload-cost-simulation-analysis"></a><span data-ttu-id="5624d-159">Create Reports for Workload Cost Simulation Analysis</span><span class="sxs-lookup"><span data-stu-id="5624d-159">Create Reports for Workload Cost Simulation Analysis</span></span>
<span data-ttu-id="5624d-160">After the usage is collected and charges are loaded into the Cloud Cruiser database, we can leverage the Cloud Cruiser Insights module to create the workload cost simulation that we desire.</span><span class="sxs-lookup"><span data-stu-id="5624d-160">After the usage is collected and charges are loaded into the Cloud Cruiser database, we can leverage the Cloud Cruiser Insights module to create the workload cost simulation that we desire.</span></span>

<span data-ttu-id="5624d-161">In order to demonstrate this scenario, we created the following report:</span><span class="sxs-lookup"><span data-stu-id="5624d-161">In order to demonstrate this scenario, we created the following report:</span></span>

<span data-ttu-id="5624d-162">![Cost Comparison][9]</span><span class="sxs-lookup"><span data-stu-id="5624d-162">![Cost Comparison][9]</span></span>

<span data-ttu-id="5624d-163">The top graph shows a cost comparison by services, comparing the price of running the workload for each specific service between WAP (dark blue) and Azure (light blue).</span><span class="sxs-lookup"><span data-stu-id="5624d-163">The top graph shows a cost comparison by services, comparing the price of running the workload for each specific service between WAP (dark blue) and Azure (light blue).</span></span>

<span data-ttu-id="5624d-164">The bottom graph shows the same data but broken down by department.</span><span class="sxs-lookup"><span data-stu-id="5624d-164">The bottom graph shows the same data but broken down by department.</span></span> <span data-ttu-id="5624d-165">This shows the costs for each department to run their workload on WAP and Azure, along with the difference between them in the Savings bar (green).</span><span class="sxs-lookup"><span data-stu-id="5624d-165">This shows the costs for each department to run their workload on WAP and Azure, along with the difference between them in the Savings bar (green).</span></span>

## <a name="azure-usage-api"></a><span data-ttu-id="5624d-166">Azure Usage API</span><span class="sxs-lookup"><span data-stu-id="5624d-166">Azure Usage API</span></span>
### <a name="introduction"></a><span data-ttu-id="5624d-167">Introduction</span><span class="sxs-lookup"><span data-stu-id="5624d-167">Introduction</span></span>
<span data-ttu-id="5624d-168">Microsoft recently introduced the Azure Usage API, allowing subscribers to programmatically pull in usage data to gain insights into their consumption.</span><span class="sxs-lookup"><span data-stu-id="5624d-168">Microsoft recently introduced the Azure Usage API, allowing subscribers to programmatically pull in usage data to gain insights into their consumption.</span></span> <span data-ttu-id="5624d-169">This is great news for Cloud Cruiser customers that can take advantage of the richer dataset available through this API.</span><span class="sxs-lookup"><span data-stu-id="5624d-169">This is great news for Cloud Cruiser customers that can take advantage of the richer dataset available through this API.</span></span>

<span data-ttu-id="5624d-170">Cloud Cruiser can leverage the integration with the Usage API in several ways.</span><span class="sxs-lookup"><span data-stu-id="5624d-170">Cloud Cruiser can leverage the integration with the Usage API in several ways.</span></span> <span data-ttu-id="5624d-171">The granularity (hourly usage information) and resource metadata information available through the API provides the necessary dataset to support flexible Showback or Chargeback models.</span><span class="sxs-lookup"><span data-stu-id="5624d-171">The granularity (hourly usage information) and resource metadata information available through the API provides the necessary dataset to support flexible Showback or Chargeback models.</span></span> 

<span data-ttu-id="5624d-172">In this tutorial, we will present one example of how Cloud Cruiser can benefit from the Usage API information.</span><span class="sxs-lookup"><span data-stu-id="5624d-172">In this tutorial, we will present one example of how Cloud Cruiser can benefit from the Usage API information.</span></span> <span data-ttu-id="5624d-173">More specifically, we will create a Resource Group on Azure, associate tags for the account structure, then describe the process of pulling and processing the tag information into Cloud Cruiser.</span><span class="sxs-lookup"><span data-stu-id="5624d-173">More specifically, we will create a Resource Group on Azure, associate tags for the account structure, then describe the process of pulling and processing the tag information into Cloud Cruiser.</span></span>

<span data-ttu-id="5624d-174">The final goal is to be able to create reports like the following one, and be able to analyze cost and consumption based on the account structure populated by the tags.</span><span class="sxs-lookup"><span data-stu-id="5624d-174">The final goal is to be able to create reports like the following one, and be able to analyze cost and consumption based on the account structure populated by the tags.</span></span>

<span data-ttu-id="5624d-175">![Figure 10 - Report with breakdowns using tags][10]</span><span class="sxs-lookup"><span data-stu-id="5624d-175">![Figure 10 - Report with breakdowns using tags][10]</span></span>

### <a name="microsoft-azure-tags"></a><span data-ttu-id="5624d-176">Microsoft Azure Tags</span><span class="sxs-lookup"><span data-stu-id="5624d-176">Microsoft Azure Tags</span></span>
<span data-ttu-id="5624d-177">The data available through the Azure Usage API includes not only consumption information, but also resource metadata including any tags associated with it.</span><span class="sxs-lookup"><span data-stu-id="5624d-177">The data available through the Azure Usage API includes not only consumption information, but also resource metadata including any tags associated with it.</span></span> <span data-ttu-id="5624d-178">Tags provide an easy way to organize your resources, but in order to be effective, you need to ensure that:</span><span class="sxs-lookup"><span data-stu-id="5624d-178">Tags provide an easy way to organize your resources, but in order to be effective, you need to ensure that:</span></span>

* <span data-ttu-id="5624d-179">Tags are correctly applied to the resources at provision time</span><span class="sxs-lookup"><span data-stu-id="5624d-179">Tags are correctly applied to the resources at provision time</span></span>
* <span data-ttu-id="5624d-180">Tags are properly used on the Showback/Chargeback process to tie the usage to the organization’s account structure.</span><span class="sxs-lookup"><span data-stu-id="5624d-180">Tags are properly used on the Showback/Chargeback process to tie the usage to the organization’s account structure.</span></span>

<span data-ttu-id="5624d-181">Both of these requirements can be challenging, especially when there is a manual process on the provision or charging side.</span><span class="sxs-lookup"><span data-stu-id="5624d-181">Both of these requirements can be challenging, especially when there is a manual process on the provision or charging side.</span></span> <span data-ttu-id="5624d-182">Mistyped, incorrect or even missing tags are common complaints from customers when using tags and these errors can make life on the charging side very difficult.</span><span class="sxs-lookup"><span data-stu-id="5624d-182">Mistyped, incorrect or even missing tags are common complaints from customers when using tags and these errors can make life on the charging side very difficult.</span></span>

<span data-ttu-id="5624d-183">With the new Azure Usage API, Cloud Cruiser can pull resource tagging information, and through a sophisticated ETL tool called workbooks, fix these common tagging errors.</span><span class="sxs-lookup"><span data-stu-id="5624d-183">With the new Azure Usage API, Cloud Cruiser can pull resource tagging information, and through a sophisticated ETL tool called workbooks, fix these common tagging errors.</span></span> <span data-ttu-id="5624d-184">Through transformation using regular expressions and data correlation, Cloud Cruiser can identify incorrectly tagged resources and apply the correct tags, ensuring the correct association of the resources with the consumer.</span><span class="sxs-lookup"><span data-stu-id="5624d-184">Through transformation using regular expressions and data correlation, Cloud Cruiser can identify incorrectly tagged resources and apply the correct tags, ensuring the correct association of the resources with the consumer.</span></span>

<span data-ttu-id="5624d-185">On the charging side, Cloud Cruiser automates the Showback/Chargeback process, and can leverage the tag information to tie the usage to the appropriate consumer (Department, Division, Project, etc.).</span><span class="sxs-lookup"><span data-stu-id="5624d-185">On the charging side, Cloud Cruiser automates the Showback/Chargeback process, and can leverage the tag information to tie the usage to the appropriate consumer (Department, Division, Project, etc.).</span></span> <span data-ttu-id="5624d-186">This automation provides a huge improvement and can ensure a consistent and auditable charging process.</span><span class="sxs-lookup"><span data-stu-id="5624d-186">This automation provides a huge improvement and can ensure a consistent and auditable charging process.</span></span>

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a><span data-ttu-id="5624d-187">Creating a Resource Group with tags on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5624d-187">Creating a Resource Group with tags on Microsoft Azure</span></span>
<span data-ttu-id="5624d-188">The first step in this tutorial is to create a Resource Group in the Azure portal, then create new tags to associate to the resources.</span><span class="sxs-lookup"><span data-stu-id="5624d-188">The first step in this tutorial is to create a Resource Group in the Azure portal, then create new tags to associate to the resources.</span></span> <span data-ttu-id="5624d-189">For this example, we will be creating the following tags: Department, Environment, Owner, Project.</span><span class="sxs-lookup"><span data-stu-id="5624d-189">For this example, we will be creating the following tags: Department, Environment, Owner, Project.</span></span>

<span data-ttu-id="5624d-190">The screenshot below shows a sample Resource Group with the associated tags.</span><span class="sxs-lookup"><span data-stu-id="5624d-190">The screenshot below shows a sample Resource Group with the associated tags.</span></span>

<span data-ttu-id="5624d-191">![Figure 11 - Resource Group with associated tags on Azure portal][11]</span><span class="sxs-lookup"><span data-stu-id="5624d-191">![Figure 11 - Resource Group with associated tags on Azure portal][11]</span></span>

<span data-ttu-id="5624d-192">The next step is to pull the information from the Usage API into Cloud Cruiser.</span><span class="sxs-lookup"><span data-stu-id="5624d-192">The next step is to pull the information from the Usage API into Cloud Cruiser.</span></span> <span data-ttu-id="5624d-193">The Usage API currently provides responses in JSON format.</span><span class="sxs-lookup"><span data-stu-id="5624d-193">The Usage API currently provides responses in JSON format.</span></span> <span data-ttu-id="5624d-194">Here is a sample of the data retrieved:</span><span class="sxs-lookup"><span data-stu-id="5624d-194">Here is a sample of the data retrieved:</span></span>

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-the-usage-api-into-cloud-cruiser"></a><span data-ttu-id="5624d-195">Import data from the Usage API into Cloud Cruiser</span><span class="sxs-lookup"><span data-stu-id="5624d-195">Import data from the Usage API into Cloud Cruiser</span></span>
<span data-ttu-id="5624d-196">Cloud Cruiser workbooks provide an automated way to collect and process information from the Usage API.</span><span class="sxs-lookup"><span data-stu-id="5624d-196">Cloud Cruiser workbooks provide an automated way to collect and process information from the Usage API.</span></span> <span data-ttu-id="5624d-197">An ETL (extract-transform-load) workbook allows you to configure the collection, transformation, and publishing of data into the Cloud Cruiser database.</span><span class="sxs-lookup"><span data-stu-id="5624d-197">An ETL (extract-transform-load) workbook allows you to configure the collection, transformation, and publishing of data into the Cloud Cruiser database.</span></span>

<span data-ttu-id="5624d-198">Each workbook can have one or multiple collections.</span><span class="sxs-lookup"><span data-stu-id="5624d-198">Each workbook can have one or multiple collections.</span></span> <span data-ttu-id="5624d-199">This allows you to correlate information from different sources to complement or augment the usage data.</span><span class="sxs-lookup"><span data-stu-id="5624d-199">This allows you to correlate information from different sources to complement or augment the usage data.</span></span> <span data-ttu-id="5624d-200">For this example, we will create a new sheet in the Azure template workbook (*UsageAPI)* and set a new *collection* to import information from the Usage API.</span><span class="sxs-lookup"><span data-stu-id="5624d-200">For this example, we will create a new sheet in the Azure template workbook (*UsageAPI)* and set a new *collection* to import information from the Usage API.</span></span>

<span data-ttu-id="5624d-201">![Figure 3 - Usage API data imported into the UsageAPI sheet][12]</span><span class="sxs-lookup"><span data-stu-id="5624d-201">![Figure 3 - Usage API data imported into the UsageAPI sheet][12]</span></span>

<span data-ttu-id="5624d-202">Notice that this workbook already has other sheets to import services from Azure (*ImportServices*), and process the consumption information from the Billing API (*PublishData*).</span><span class="sxs-lookup"><span data-stu-id="5624d-202">Notice that this workbook already has other sheets to import services from Azure (*ImportServices*), and process the consumption information from the Billing API (*PublishData*).</span></span>

<span data-ttu-id="5624d-203">Next we will use the Usage API to populate the *UsageAPI* sheet, and correlate the information with the consumption data from the Billing API on the *PublishData* sheet.</span><span class="sxs-lookup"><span data-stu-id="5624d-203">Next we will use the Usage API to populate the *UsageAPI* sheet, and correlate the information with the consumption data from the Billing API on the *PublishData* sheet.</span></span>

### <a name="processing-the-tag-information-from-the-usage-api"></a><span data-ttu-id="5624d-204">Processing the tag information from the Usage API</span><span class="sxs-lookup"><span data-stu-id="5624d-204">Processing the tag information from the Usage API</span></span>
<span data-ttu-id="5624d-205">After importing the data into the workbook, we will create transformation steps in the *UsageAPI* sheet in order to process the information from the API.</span><span class="sxs-lookup"><span data-stu-id="5624d-205">After importing the data into the workbook, we will create transformation steps in the *UsageAPI* sheet in order to process the information from the API.</span></span> <span data-ttu-id="5624d-206">First step is to use a “JSON split” processor to extract the tags from a single field, then create fields for each one of them (Department, Project, Owner, and Environment).</span><span class="sxs-lookup"><span data-stu-id="5624d-206">First step is to use a “JSON split” processor to extract the tags from a single field, then create fields for each one of them (Department, Project, Owner, and Environment).</span></span>

<span data-ttu-id="5624d-207">![Figure 4 - Create new fields for the tag information][13]</span><span class="sxs-lookup"><span data-stu-id="5624d-207">![Figure 4 - Create new fields for the tag information][13]</span></span>

<span data-ttu-id="5624d-208">Notice the “Networking” service is missing the tag information (yellow box), but we can verify that it is part of the same Resource Group by looking at the *ResourceGroupName* field.</span><span class="sxs-lookup"><span data-stu-id="5624d-208">Notice the “Networking” service is missing the tag information (yellow box), but we can verify that it is part of the same Resource Group by looking at the *ResourceGroupName* field.</span></span> <span data-ttu-id="5624d-209">Since we have the tags for the other resources from this Resource Group, we can use this information to apply the missing tags to this resource later in the process.</span><span class="sxs-lookup"><span data-stu-id="5624d-209">Since we have the tags for the other resources from this Resource Group, we can use this information to apply the missing tags to this resource later in the process.</span></span>

<span data-ttu-id="5624d-210">The next step is to create a lookup table associating the information from the tags to the *ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="5624d-210">The next step is to create a lookup table associating the information from the tags to the *ResourceGroupName*.</span></span> <span data-ttu-id="5624d-211">This lookup table will be used on the next step to enrich the consumption data with tag information.</span><span class="sxs-lookup"><span data-stu-id="5624d-211">This lookup table will be used on the next step to enrich the consumption data with tag information.</span></span>

### <a name="adding-the-tag-information-to-the-consumption-data"></a><span data-ttu-id="5624d-212">Adding the tag information to the consumption data</span><span class="sxs-lookup"><span data-stu-id="5624d-212">Adding the tag information to the consumption data</span></span>
<span data-ttu-id="5624d-213">Now we can jump to the *PublishData* sheet, which processes the consumption information from the Billing API, and add the fields extracted from the tags.</span><span class="sxs-lookup"><span data-stu-id="5624d-213">Now we can jump to the *PublishData* sheet, which processes the consumption information from the Billing API, and add the fields extracted from the tags.</span></span> <span data-ttu-id="5624d-214">This process is performed by looking at the lookup table created on the previous step, using the *ResourceGroupName* as the key for the lookups.</span><span class="sxs-lookup"><span data-stu-id="5624d-214">This process is performed by looking at the lookup table created on the previous step, using the *ResourceGroupName* as the key for the lookups.</span></span>

<span data-ttu-id="5624d-215">![Figure 5 - Populating the account structure with the information from the lookups][14]</span><span class="sxs-lookup"><span data-stu-id="5624d-215">![Figure 5 - Populating the account structure with the information from the lookups][14]</span></span>

<span data-ttu-id="5624d-216">Notice that the appropriate account structure fields for the “Networking” service were applied, fixing the issue with the missing tags.</span><span class="sxs-lookup"><span data-stu-id="5624d-216">Notice that the appropriate account structure fields for the “Networking” service were applied, fixing the issue with the missing tags.</span></span> <span data-ttu-id="5624d-217">We also populated the account structure fields for resources other than our target Resource Group with “Other”, in order to differentiate them on the reports.</span><span class="sxs-lookup"><span data-stu-id="5624d-217">We also populated the account structure fields for resources other than our target Resource Group with “Other”, in order to differentiate them on the reports.</span></span>

<span data-ttu-id="5624d-218">Now we just need to add a step to publish the usage data.</span><span class="sxs-lookup"><span data-stu-id="5624d-218">Now we just need to add a step to publish the usage data.</span></span> <span data-ttu-id="5624d-219">During this step, the appropriate rates for each service defined on our Rate Plan will be applied to the usage information, with the resulting charge loaded into the database.</span><span class="sxs-lookup"><span data-stu-id="5624d-219">During this step, the appropriate rates for each service defined on our Rate Plan will be applied to the usage information, with the resulting charge loaded into the database.</span></span>

<span data-ttu-id="5624d-220">The best part is that you only have to go through this process once.</span><span class="sxs-lookup"><span data-stu-id="5624d-220">The best part is that you only have to go through this process once.</span></span> <span data-ttu-id="5624d-221">When the workbook is completed, you just need to add it to the scheduler and it will run hourly or daily at the scheduled time.</span><span class="sxs-lookup"><span data-stu-id="5624d-221">When the workbook is completed, you just need to add it to the scheduler and it will run hourly or daily at the scheduled time.</span></span> <span data-ttu-id="5624d-222">Then it’s just a matter of creating new reports, or customizing existing ones, in order to analyze the data to get meaningful insights from your cloud usage.</span><span class="sxs-lookup"><span data-stu-id="5624d-222">Then it’s just a matter of creating new reports, or customizing existing ones, in order to analyze the data to get meaningful insights from your cloud usage.</span></span>

### <a name="next-steps"></a><span data-ttu-id="5624d-223">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5624d-223">Next Steps</span></span>
* <span data-ttu-id="5624d-224">For detailed instructions on creating Cloud Cruiser workbooks and reports, please refer to Cloud Cruiser’s online [documentation](http://docs.cloudcruiser.com/) (valid login required).</span><span class="sxs-lookup"><span data-stu-id="5624d-224">For detailed instructions on creating Cloud Cruiser workbooks and reports, please refer to Cloud Cruiser’s online [documentation](http://docs.cloudcruiser.com/) (valid login required).</span></span>  <span data-ttu-id="5624d-225">For more information about Cloud Cruiser, please contact [info@cloudcruiser.com](mailto:info@cloudcruiser.com).</span><span class="sxs-lookup"><span data-stu-id="5624d-225">For more information about Cloud Cruiser, please contact [info@cloudcruiser.com](mailto:info@cloudcruiser.com).</span></span>
* <span data-ttu-id="5624d-226">See [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md) for an overview of the Azure Resource Usage and RateCard APIs.</span><span class="sxs-lookup"><span data-stu-id="5624d-226">See [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md) for an overview of the Azure Resource Usage and RateCard APIs.</span></span>
* <span data-ttu-id="5624d-227">Check out the [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more information on both APIs, which are part of the set of APIs provided by the Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5624d-227">Check out the [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more information on both APIs, which are part of the set of APIs provided by the Azure Resource Manager.</span></span>
* <span data-ttu-id="5624d-228">If you would like to dive right into the sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span><span class="sxs-lookup"><span data-stu-id="5624d-228">If you would like to dive right into the sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span></span>

### <a name="learn-more"></a><span data-ttu-id="5624d-229">Learn More</span><span class="sxs-lookup"><span data-stu-id="5624d-229">Learn More</span></span>
* <span data-ttu-id="5624d-230">See the [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) article to learn more about the Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5624d-230">See the [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) article to learn more about the Azure Resource Manager.</span></span>

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Figure 1 - Creating a new collection"
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Figure 2 - Import data from the new collection"
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Figure 3 - Transformation steps to process collected data from RateCard API"
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Figure 4 - Publishing the data from the RateCard API as new Services and Rates"
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Figure 5 - Verifying the new Services"
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Figure 6 - Verifying the new Rate Plan and associated rates"
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Figure 7 - Transforming WAP data to normalize services"
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Figure 8 - Workbook scheduling"
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Figure 9 - Sample Report for the Workload cost comparison scenario"
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Figure 10 - Report with breakdowns using tags"
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Figure 11 - Resource Group with associated tags on Azure portal"
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Figure 12 - Usage API data imported into the UsageAPI sheet"
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Figure 13 - Create new fields for the tag information"
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Figure 14 - Populating the account structure with the information from the lookups"














