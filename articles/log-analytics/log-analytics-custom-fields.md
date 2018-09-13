---
title: Custom fields in Log Analytics | Microsoft Docs
description: The Custom Fields feature of Log Analytics allows you to create your own searchable fields from OMS data that add to the properties of a collected record.  This article describes the process to create a custom field and provides a detailed walkthrough with a sample event.
services: log-analytics
documentationcenter: ''
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 802bf774eebc973b74a847379584c62c9e664104
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551990"
---
# <a name="custom-fields-in-log-analytics"></a><span data-ttu-id="021ed-104">Custom fields in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="021ed-104">Custom fields in Log Analytics</span></span>
<span data-ttu-id="021ed-105">The **Custom Fields** feature of Log Analytics allows you to extend existing records in the OMS repository by adding your own searchable fields.</span><span class="sxs-lookup"><span data-stu-id="021ed-105">The **Custom Fields** feature of Log Analytics allows you to extend existing records in the OMS repository by adding your own searchable fields.</span></span>  <span data-ttu-id="021ed-106">Custom fields are automatically populated from data extracted from other properties in the same record.</span><span class="sxs-lookup"><span data-stu-id="021ed-106">Custom fields are automatically populated from data extracted from other properties in the same record.</span></span>

![Custom Fields overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/overview.png)

<span data-ttu-id="021ed-108">For example, the sample record below has useful data buried in the event description.</span><span class="sxs-lookup"><span data-stu-id="021ed-108">For example, the sample record below has useful data buried in the event description.</span></span>  <span data-ttu-id="021ed-109">Extracting this data into separate properties makes it available for such actions as sorting and filtering.</span><span class="sxs-lookup"><span data-stu-id="021ed-109">Extracting this data into separate properties makes it available for such actions as sorting and filtering.</span></span>

![Log Search button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> <span data-ttu-id="021ed-111">In the Preview, you are limited to 100 custom fields in your workspace.</span><span class="sxs-lookup"><span data-stu-id="021ed-111">In the Preview, you are limited to 100 custom fields in your workspace.</span></span>  <span data-ttu-id="021ed-112">This limit will be expanded when this feature reaches general availability.</span><span class="sxs-lookup"><span data-stu-id="021ed-112">This limit will be expanded when this feature reaches general availability.</span></span>
> 
> 

## <a name="creating-a-custom-field"></a><span data-ttu-id="021ed-113">Creating a custom field</span><span class="sxs-lookup"><span data-stu-id="021ed-113">Creating a custom field</span></span>
<span data-ttu-id="021ed-114">When you create a custom field, Log Analytics must understand which data to use to populate its value.</span><span class="sxs-lookup"><span data-stu-id="021ed-114">When you create a custom field, Log Analytics must understand which data to use to populate its value.</span></span>  <span data-ttu-id="021ed-115">It uses a technology from Microsoft Research called FlashExtract to quickly identify this data.</span><span class="sxs-lookup"><span data-stu-id="021ed-115">It uses a technology from Microsoft Research called FlashExtract to quickly identify this data.</span></span>  <span data-ttu-id="021ed-116">Rather than requiring you to provide explicit instructions, Log Analytics learns about the data you want to extract from examples that you provide.</span><span class="sxs-lookup"><span data-stu-id="021ed-116">Rather than requiring you to provide explicit instructions, Log Analytics learns about the data you want to extract from examples that you provide.</span></span>

<span data-ttu-id="021ed-117">The following sections provide the procedure for creating a custom field.</span><span class="sxs-lookup"><span data-stu-id="021ed-117">The following sections provide the procedure for creating a custom field.</span></span>  <span data-ttu-id="021ed-118">At the bottom of this article is a walkthrough of a sample extraction.</span><span class="sxs-lookup"><span data-stu-id="021ed-118">At the bottom of this article is a walkthrough of a sample extraction.</span></span>

> [!NOTE]
> <span data-ttu-id="021ed-119">The custom field is populated as records matching the specified criteria are added to the OMS data store, so it will only appear on records collected after the custom field is created.</span><span class="sxs-lookup"><span data-stu-id="021ed-119">The custom field is populated as records matching the specified criteria are added to the OMS data store, so it will only appear on records collected after the custom field is created.</span></span>  <span data-ttu-id="021ed-120">The custom field will not be added to records that are already in the data store when it’s created.</span><span class="sxs-lookup"><span data-stu-id="021ed-120">The custom field will not be added to records that are already in the data store when it’s created.</span></span>
> 
> 

### <a name="step-1--identify-records-that-will-have-the-custom-field"></a><span data-ttu-id="021ed-121">Step 1 – Identify records that will have the custom field</span><span class="sxs-lookup"><span data-stu-id="021ed-121">Step 1 – Identify records that will have the custom field</span></span>
<span data-ttu-id="021ed-122">The first step is to identify the records that will get the custom field.</span><span class="sxs-lookup"><span data-stu-id="021ed-122">The first step is to identify the records that will get the custom field.</span></span>  <span data-ttu-id="021ed-123">You start with a [standard log search](log-analytics-log-searches.md) and then select a record to act as the model that Log Analytics will learn from.</span><span class="sxs-lookup"><span data-stu-id="021ed-123">You start with a [standard log search](log-analytics-log-searches.md) and then select a record to act as the model that Log Analytics will learn from.</span></span>  <span data-ttu-id="021ed-124">When you specify that you are going to extract data into a custom field, the **Field Extraction Wizard** is opened where you validate and refine the criteria.</span><span class="sxs-lookup"><span data-stu-id="021ed-124">When you specify that you are going to extract data into a custom field, the **Field Extraction Wizard** is opened where you validate and refine the criteria.</span></span>

1. <span data-ttu-id="021ed-125">Go to **Log Search** and use a [query to retrieve the records](log-analytics-log-searches.md) that will have the custom field.</span><span class="sxs-lookup"><span data-stu-id="021ed-125">Go to **Log Search** and use a [query to retrieve the records](log-analytics-log-searches.md) that will have the custom field.</span></span>
2. <span data-ttu-id="021ed-126">Select a record that Log Analytics will use to act as a model for extracting data to populate the custom field.</span><span class="sxs-lookup"><span data-stu-id="021ed-126">Select a record that Log Analytics will use to act as a model for extracting data to populate the custom field.</span></span>  <span data-ttu-id="021ed-127">You will identify the data that you want to extract from this record, and Log Analytics will use this information to determine the logic to populate the custom field for all similar records.</span><span class="sxs-lookup"><span data-stu-id="021ed-127">You will identify the data that you want to extract from this record, and Log Analytics will use this information to determine the logic to populate the custom field for all similar records.</span></span>
3. <span data-ttu-id="021ed-128">Click the button to the left of any text property of the record and select **Extract fields from**.</span><span class="sxs-lookup"><span data-stu-id="021ed-128">Click the button to the left of any text property of the record and select **Extract fields from**.</span></span>
4. <span data-ttu-id="021ed-129">The **Field Extraction Wizard is opened**, and the record you selected is displayed in the **Main Example** column.</span><span class="sxs-lookup"><span data-stu-id="021ed-129">The **Field Extraction Wizard is opened**, and the record you selected is displayed in the **Main Example** column.</span></span>  <span data-ttu-id="021ed-130">The custom field will be defined for those records with the same values in the properties that are selected.</span><span class="sxs-lookup"><span data-stu-id="021ed-130">The custom field will be defined for those records with the same values in the properties that are selected.</span></span>  
5. <span data-ttu-id="021ed-131">If the selection is not exactly what you want, select additional fields to narrow the criteria.</span><span class="sxs-lookup"><span data-stu-id="021ed-131">If the selection is not exactly what you want, select additional fields to narrow the criteria.</span></span>  <span data-ttu-id="021ed-132">In order to change the field values for the criteria, you must cancel and select a different record matching the criteria you want.</span><span class="sxs-lookup"><span data-stu-id="021ed-132">In order to change the field values for the criteria, you must cancel and select a different record matching the criteria you want.</span></span>

### <a name="step-2---perform-initial-extract"></a><span data-ttu-id="021ed-133">Step 2 - Perform initial extract.</span><span class="sxs-lookup"><span data-stu-id="021ed-133">Step 2 - Perform initial extract.</span></span>
<span data-ttu-id="021ed-134">Once you’ve identified the records that will have the custom field, you identify the data that you want to extract.</span><span class="sxs-lookup"><span data-stu-id="021ed-134">Once you’ve identified the records that will have the custom field, you identify the data that you want to extract.</span></span>  <span data-ttu-id="021ed-135">Log Analytics will use this information to identify similar patterns in similar records.</span><span class="sxs-lookup"><span data-stu-id="021ed-135">Log Analytics will use this information to identify similar patterns in similar records.</span></span>  <span data-ttu-id="021ed-136">In the step after this you will be able to validate the results and provide further details for Log Analytics to use in its analysis.</span><span class="sxs-lookup"><span data-stu-id="021ed-136">In the step after this you will be able to validate the results and provide further details for Log Analytics to use in its analysis.</span></span>

1. <span data-ttu-id="021ed-137">Highlight the text in the sample record that you want to populate the custom field.</span><span class="sxs-lookup"><span data-stu-id="021ed-137">Highlight the text in the sample record that you want to populate the custom field.</span></span>  <span data-ttu-id="021ed-138">You will then be presented with a dialog box to provide a name for the field and to perform the initial extract.</span><span class="sxs-lookup"><span data-stu-id="021ed-138">You will then be presented with a dialog box to provide a name for the field and to perform the initial extract.</span></span>  <span data-ttu-id="021ed-139">The characters **\_CF** will automatically be appended.</span><span class="sxs-lookup"><span data-stu-id="021ed-139">The characters **\_CF** will automatically be appended.</span></span>
2. <span data-ttu-id="021ed-140">Click **Extract** to perform an analysis of collected records.</span><span class="sxs-lookup"><span data-stu-id="021ed-140">Click **Extract** to perform an analysis of collected records.</span></span>  
3. <span data-ttu-id="021ed-141">The **Summary** and **Search Results** sections display the results of the extract so you can inspect its accuracy.</span><span class="sxs-lookup"><span data-stu-id="021ed-141">The **Summary** and **Search Results** sections display the results of the extract so you can inspect its accuracy.</span></span>  <span data-ttu-id="021ed-142">**Summary** displays the criteria used to identify records and a count for each of the data values identified.</span><span class="sxs-lookup"><span data-stu-id="021ed-142">**Summary** displays the criteria used to identify records and a count for each of the data values identified.</span></span>  <span data-ttu-id="021ed-143">**Search Results** provides a detailed list of records matching the criteria.</span><span class="sxs-lookup"><span data-stu-id="021ed-143">**Search Results** provides a detailed list of records matching the criteria.</span></span>

### <a name="step-3--verify-accuracy-of-the-extract-and-create-custom-field"></a><span data-ttu-id="021ed-144">Step 3 – Verify accuracy of the extract and create custom field</span><span class="sxs-lookup"><span data-stu-id="021ed-144">Step 3 – Verify accuracy of the extract and create custom field</span></span>
<span data-ttu-id="021ed-145">Once you have performed the initial extract, Log Analytics will display its results based on data that has already been collected.</span><span class="sxs-lookup"><span data-stu-id="021ed-145">Once you have performed the initial extract, Log Analytics will display its results based on data that has already been collected.</span></span>  <span data-ttu-id="021ed-146">If the results look accurate then you can create the custom field with no further work.</span><span class="sxs-lookup"><span data-stu-id="021ed-146">If the results look accurate then you can create the custom field with no further work.</span></span>  <span data-ttu-id="021ed-147">If not, then you can refine the results so that Log Analytics can improve its logic.</span><span class="sxs-lookup"><span data-stu-id="021ed-147">If not, then you can refine the results so that Log Analytics can improve its logic.</span></span>

1. <span data-ttu-id="021ed-148">If any values in the initial extract aren’t correct, then click the **Edit** icon next to an inaccurate record and select **Modify this highlight** in order to modify the selection.</span><span class="sxs-lookup"><span data-stu-id="021ed-148">If any values in the initial extract aren’t correct, then click the **Edit** icon next to an inaccurate record and select **Modify this highlight** in order to modify the selection.</span></span>
2. <span data-ttu-id="021ed-149">The entry is copied to the **Additional examples** section underneath the **Main Example**.</span><span class="sxs-lookup"><span data-stu-id="021ed-149">The entry is copied to the **Additional examples** section underneath the **Main Example**.</span></span>  <span data-ttu-id="021ed-150">You can adjust the highlight here to help Log Analytics understand the selection it should have made.</span><span class="sxs-lookup"><span data-stu-id="021ed-150">You can adjust the highlight here to help Log Analytics understand the selection it should have made.</span></span>
3. <span data-ttu-id="021ed-151">Click **Extract** to use this new information to evaluate all the existing records.</span><span class="sxs-lookup"><span data-stu-id="021ed-151">Click **Extract** to use this new information to evaluate all the existing records.</span></span>  <span data-ttu-id="021ed-152">The results may be modified for records other than the one you just modified based on this new intelligence.</span><span class="sxs-lookup"><span data-stu-id="021ed-152">The results may be modified for records other than the one you just modified based on this new intelligence.</span></span>
4. <span data-ttu-id="021ed-153">Continue to add corrections until all records in the extract correctly identify the data to populate the new custom field.</span><span class="sxs-lookup"><span data-stu-id="021ed-153">Continue to add corrections until all records in the extract correctly identify the data to populate the new custom field.</span></span>
5. <span data-ttu-id="021ed-154">Click **Save Extract** when you are satisfied with the results.</span><span class="sxs-lookup"><span data-stu-id="021ed-154">Click **Save Extract** when you are satisfied with the results.</span></span>  <span data-ttu-id="021ed-155">The custom field is now defined, but it won’t be added to any records yet.</span><span class="sxs-lookup"><span data-stu-id="021ed-155">The custom field is now defined, but it won’t be added to any records yet.</span></span>
6. <span data-ttu-id="021ed-156">Wait for new records matching the specified criteria to be collected and then run the log search again.</span><span class="sxs-lookup"><span data-stu-id="021ed-156">Wait for new records matching the specified criteria to be collected and then run the log search again.</span></span> <span data-ttu-id="021ed-157">New records should have the custom field.</span><span class="sxs-lookup"><span data-stu-id="021ed-157">New records should have the custom field.</span></span>
7. <span data-ttu-id="021ed-158">Use the custom field like any other record property.</span><span class="sxs-lookup"><span data-stu-id="021ed-158">Use the custom field like any other record property.</span></span>  <span data-ttu-id="021ed-159">You can use it to aggregate and group data and even use it to produce new insights.</span><span class="sxs-lookup"><span data-stu-id="021ed-159">You can use it to aggregate and group data and even use it to produce new insights.</span></span>

## <a name="viewing-custom-fields"></a><span data-ttu-id="021ed-160">Viewing custom fields</span><span class="sxs-lookup"><span data-stu-id="021ed-160">Viewing custom fields</span></span>
<span data-ttu-id="021ed-161">You can view a list of all custom fields in your management group from the **Settings** tile of the OMS dashboard.</span><span class="sxs-lookup"><span data-stu-id="021ed-161">You can view a list of all custom fields in your management group from the **Settings** tile of the OMS dashboard.</span></span>  <span data-ttu-id="021ed-162">Select **Data** and then **Custom fields** for a list of all custom fields in your workspace.</span><span class="sxs-lookup"><span data-stu-id="021ed-162">Select **Data** and then **Custom fields** for a list of all custom fields in your workspace.</span></span>  

![Custom fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a><span data-ttu-id="021ed-164">Removing a custom field</span><span class="sxs-lookup"><span data-stu-id="021ed-164">Removing a custom field</span></span>
<span data-ttu-id="021ed-165">There are two ways to remove a custom field.</span><span class="sxs-lookup"><span data-stu-id="021ed-165">There are two ways to remove a custom field.</span></span>  <span data-ttu-id="021ed-166">The first is the **Remove** option for each field when viewing the complete list as described above.</span><span class="sxs-lookup"><span data-stu-id="021ed-166">The first is the **Remove** option for each field when viewing the complete list as described above.</span></span>  <span data-ttu-id="021ed-167">The other method is to retrieve a record and click the button to the left of the field.</span><span class="sxs-lookup"><span data-stu-id="021ed-167">The other method is to retrieve a record and click the button to the left of the field.</span></span>  <span data-ttu-id="021ed-168">The menu will have an option to remove the custom field.</span><span class="sxs-lookup"><span data-stu-id="021ed-168">The menu will have an option to remove the custom field.</span></span>

## <a name="sample-walkthrough"></a><span data-ttu-id="021ed-169">Sample walkthrough</span><span class="sxs-lookup"><span data-stu-id="021ed-169">Sample walkthrough</span></span>
<span data-ttu-id="021ed-170">The following section walks through a complete example of creating a custom field.</span><span class="sxs-lookup"><span data-stu-id="021ed-170">The following section walks through a complete example of creating a custom field.</span></span>  <span data-ttu-id="021ed-171">This example extracts the service name in Windows events that indicate a service changing state.</span><span class="sxs-lookup"><span data-stu-id="021ed-171">This example extracts the service name in Windows events that indicate a service changing state.</span></span>  <span data-ttu-id="021ed-172">This relies on events created by Service Control Manager in the System log on Windows computers.</span><span class="sxs-lookup"><span data-stu-id="021ed-172">This relies on events created by Service Control Manager in the System log on Windows computers.</span></span>  <span data-ttu-id="021ed-173">If you want to follow this example, you must be [collecting Information events for the System log](log-analytics-data-sources-windows-events.md).</span><span class="sxs-lookup"><span data-stu-id="021ed-173">If you want to follow this example, you must be [collecting Information events for the System log](log-analytics-data-sources-windows-events.md).</span></span>

<span data-ttu-id="021ed-174">We enter the following query to return all events from Service Control Manager that have an Event ID of 7036 which is the event that indicates a service starting or stopping.</span><span class="sxs-lookup"><span data-stu-id="021ed-174">We enter the following query to return all events from Service Control Manager that have an Event ID of 7036 which is the event that indicates a service starting or stopping.</span></span>

![Query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/query.png)

<span data-ttu-id="021ed-176">We then select any record with event ID 7036.</span><span class="sxs-lookup"><span data-stu-id="021ed-176">We then select any record with event ID 7036.</span></span>

![Source record](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/source-record.png)

<span data-ttu-id="021ed-178">We want the service name that appears in the **RenderedDescription** property and select the button next to this property.</span><span class="sxs-lookup"><span data-stu-id="021ed-178">We want the service name that appears in the **RenderedDescription** property and select the button next to this property.</span></span>

![Extract fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/extract-fields.png)

<span data-ttu-id="021ed-180">The **Field Extraction Wizard** is opened, and the **EventLog** and **EventID** fields are selected in the **Main Example** column.</span><span class="sxs-lookup"><span data-stu-id="021ed-180">The **Field Extraction Wizard** is opened, and the **EventLog** and **EventID** fields are selected in the **Main Example** column.</span></span>  <span data-ttu-id="021ed-181">This indicates that the custom field will be defined for events from the System log with an event ID of 7036.</span><span class="sxs-lookup"><span data-stu-id="021ed-181">This indicates that the custom field will be defined for events from the System log with an event ID of 7036.</span></span>  <span data-ttu-id="021ed-182">This is sufficient so we don’t need to select any other fields.</span><span class="sxs-lookup"><span data-stu-id="021ed-182">This is sufficient so we don’t need to select any other fields.</span></span>

![Main example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/main-example.png)

<span data-ttu-id="021ed-184">We highlight the name of the service in the **RenderedDescription** property and use **Service** to identify the service name.</span><span class="sxs-lookup"><span data-stu-id="021ed-184">We highlight the name of the service in the **RenderedDescription** property and use **Service** to identify the service name.</span></span>  <span data-ttu-id="021ed-185">The custom field will be called **Service_CF**.</span><span class="sxs-lookup"><span data-stu-id="021ed-185">The custom field will be called **Service_CF**.</span></span>

![Field Title](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/field-title.png)

<span data-ttu-id="021ed-187">We see that the service name is identified properly for some records but not for others.</span><span class="sxs-lookup"><span data-stu-id="021ed-187">We see that the service name is identified properly for some records but not for others.</span></span>   <span data-ttu-id="021ed-188">The **Search Results** show that part of the name for the **WMI Performance Adapter** wasn’t selected.</span><span class="sxs-lookup"><span data-stu-id="021ed-188">The **Search Results** show that part of the name for the **WMI Performance Adapter** wasn’t selected.</span></span>  <span data-ttu-id="021ed-189">The **Summary** shows that four records with **DPRMA** service incorrectly included an extra word, and two records identified **Modules Installer** instead of **Windows Modules Installer**.</span><span class="sxs-lookup"><span data-stu-id="021ed-189">The **Summary** shows that four records with **DPRMA** service incorrectly included an extra word, and two records identified **Modules Installer** instead of **Windows Modules Installer**.</span></span>  

![Search results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/search-results-01.png)

<span data-ttu-id="021ed-191">We start with the **WMI Performance Adapter** record.</span><span class="sxs-lookup"><span data-stu-id="021ed-191">We start with the **WMI Performance Adapter** record.</span></span>  <span data-ttu-id="021ed-192">We click its edit icon and then **Modify this highlight**.</span><span class="sxs-lookup"><span data-stu-id="021ed-192">We click its edit icon and then **Modify this highlight**.</span></span>  

![Modify highlight](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/modify-highlight.png)

<span data-ttu-id="021ed-194">We increase    the highlight to include the word **WMI** and then rerun the extract.</span><span class="sxs-lookup"><span data-stu-id="021ed-194">We increase    the highlight to include the word **WMI** and then rerun the extract.</span></span>  

![Additional example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/additional-example-01.png)

<span data-ttu-id="021ed-196">We can see that the entries for **WMI Performance Adapter** have been corrected, and Log Analytics also used that information to correct the records for **Windows Module Installer**.</span><span class="sxs-lookup"><span data-stu-id="021ed-196">We can see that the entries for **WMI Performance Adapter** have been corrected, and Log Analytics also used that information to correct the records for **Windows Module Installer**.</span></span>  <span data-ttu-id="021ed-197">We can see in the **Summary** section though that **DPMRA** is still not being identified correctly.</span><span class="sxs-lookup"><span data-stu-id="021ed-197">We can see in the **Summary** section though that **DPMRA** is still not being identified correctly.</span></span>

![Search results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/search-results-02.png)

<span data-ttu-id="021ed-199">We scroll to a record with the DPMRA service and use the same process to correct that record.</span><span class="sxs-lookup"><span data-stu-id="021ed-199">We scroll to a record with the DPMRA service and use the same process to correct that record.</span></span>

![Additional example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/additional-example-02.png)

 <span data-ttu-id="021ed-201">When we run the extraction, we can see that all of our results are now accurate.</span><span class="sxs-lookup"><span data-stu-id="021ed-201">When we run the extraction, we can see that all of our results are now accurate.</span></span>

![Search results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/search-results-03.png)

<span data-ttu-id="021ed-203">We can see that **Service_CF** is created but is not yet added to any records.</span><span class="sxs-lookup"><span data-stu-id="021ed-203">We can see that **Service_CF** is created but is not yet added to any records.</span></span>

![Initial count](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/initial-count.png)

<span data-ttu-id="021ed-205">After some time has passed so new events are collected, we can see that that the **Service_CF** field is now being added to records that match our criteria.</span><span class="sxs-lookup"><span data-stu-id="021ed-205">After some time has passed so new events are collected, we can see that that the **Service_CF** field is now being added to records that match our criteria.</span></span>

![Final results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/final-results.png)

<span data-ttu-id="021ed-207">We can now use the custom field like any other record property.</span><span class="sxs-lookup"><span data-stu-id="021ed-207">We can now use the custom field like any other record property.</span></span>  <span data-ttu-id="021ed-208">To illustrate this, we create a query that groups by the new **Service_CF** field to inspect which services are the most active.</span><span class="sxs-lookup"><span data-stu-id="021ed-208">To illustrate this, we create a query that groups by the new **Service_CF** field to inspect which services are the most active.</span></span>

![Group by query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a><span data-ttu-id="021ed-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="021ed-210">Next steps</span></span>
* <span data-ttu-id="021ed-211">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span><span class="sxs-lookup"><span data-stu-id="021ed-211">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span></span>
* <span data-ttu-id="021ed-212">Monitor [custom log files](log-analytics-data-sources-custom-logs.md) that you parse using custom fields.</span><span class="sxs-lookup"><span data-stu-id="021ed-212">Monitor [custom log files](log-analytics-data-sources-custom-logs.md) that you parse using custom fields.</span></span>

















