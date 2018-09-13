---
title: Row-level security with Power BI Embedded
description: Details about row-level security with Power BI Embedded
services: power-bi-embedded
documentationcenter: ''
author: guyinacube
manager: erikre
editor: ''
tags: ''
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: bc7418688049d035e037c4cec8358a4809faf510
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550445"
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="af7ca-103">Row level security with Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="af7ca-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="af7ca-104">Row level security (RLS) can be used to restrict user access to particular data within a report or dataset, allowing for multiple different users to use the same report while all seeing different data.</span><span class="sxs-lookup"><span data-stu-id="af7ca-104">Row level security (RLS) can be used to restrict user access to particular data within a report or dataset, allowing for multiple different users to use the same report while all seeing different data.</span></span> <span data-ttu-id="af7ca-105">Power BI Embedded now supports datasets configured with RLS.</span><span class="sxs-lookup"><span data-stu-id="af7ca-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="af7ca-106">In order to take advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span><span class="sxs-lookup"><span data-stu-id="af7ca-106">In order to take advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="af7ca-107">Let’s take a closer look at each:</span><span class="sxs-lookup"><span data-stu-id="af7ca-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="af7ca-108">**Users** –  These are the actual end-users viewing reports.</span><span class="sxs-lookup"><span data-stu-id="af7ca-108">**Users** –  These are the actual end-users viewing reports.</span></span> <span data-ttu-id="af7ca-109">In Power BI Embedded, users are identified by the username property in an App Token.</span><span class="sxs-lookup"><span data-stu-id="af7ca-109">In Power BI Embedded, users are identified by the username property in an App Token.</span></span>

<span data-ttu-id="af7ca-110">**Roles** – Users belong to roles.</span><span class="sxs-lookup"><span data-stu-id="af7ca-110">**Roles** – Users belong to roles.</span></span> <span data-ttu-id="af7ca-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span><span class="sxs-lookup"><span data-stu-id="af7ca-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="af7ca-112">In Power BI Embedded, users are identified by the roles property in an App Token.</span><span class="sxs-lookup"><span data-stu-id="af7ca-112">In Power BI Embedded, users are identified by the roles property in an App Token.</span></span>

<span data-ttu-id="af7ca-113">**Rules** – Roles have rules, and those rules are the actual filters that are going to be applied to the data.</span><span class="sxs-lookup"><span data-stu-id="af7ca-113">**Rules** – Roles have rules, and those rules are the actual filters that are going to be applied to the data.</span></span> <span data-ttu-id="af7ca-114">This could be as simple as “Country = USA” or something much more dynamic.</span><span class="sxs-lookup"><span data-stu-id="af7ca-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="af7ca-115">Example</span><span class="sxs-lookup"><span data-stu-id="af7ca-115">Example</span></span>

<span data-ttu-id="af7ca-116">For the rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span><span class="sxs-lookup"><span data-stu-id="af7ca-116">For the rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="af7ca-117">Our example uses the [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span><span class="sxs-lookup"><span data-stu-id="af7ca-117">Our example uses the [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="af7ca-118">Our Retail Analysis sample shows sales for all the stores in a particular retail chain.</span><span class="sxs-lookup"><span data-stu-id="af7ca-118">Our Retail Analysis sample shows sales for all the stores in a particular retail chain.</span></span> <span data-ttu-id="af7ca-119">Without RLS, no matter which district manager signs in and views the report, they’ll see the same data.</span><span class="sxs-lookup"><span data-stu-id="af7ca-119">Without RLS, no matter which district manager signs in and views the report, they’ll see the same data.</span></span> <span data-ttu-id="af7ca-120">Senior management has determined each district manager should only see the sales for the stores they manage, and to do this, we can use RLS.</span><span class="sxs-lookup"><span data-stu-id="af7ca-120">Senior management has determined each district manager should only see the sales for the stores they manage, and to do this, we can use RLS.</span></span>

<span data-ttu-id="af7ca-121">RLS is authored in Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="af7ca-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="af7ca-122">When the dataset and report are opened, we can switch to diagram view to see the schema:</span><span class="sxs-lookup"><span data-stu-id="af7ca-122">When the dataset and report are opened, we can switch to diagram view to see the schema:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="af7ca-123">Here are a few things to notice with this schema:</span><span class="sxs-lookup"><span data-stu-id="af7ca-123">Here are a few things to notice with this schema:</span></span>

* <span data-ttu-id="af7ca-124">All measures, like **Total Sales**, are stored in the **Sales** fact table.</span><span class="sxs-lookup"><span data-stu-id="af7ca-124">All measures, like **Total Sales**, are stored in the **Sales** fact table.</span></span>
* <span data-ttu-id="af7ca-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span><span class="sxs-lookup"><span data-stu-id="af7ca-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="af7ca-126">The arrows on the relationship lines indicate which way filters can flow from one table to another.</span><span class="sxs-lookup"><span data-stu-id="af7ca-126">The arrows on the relationship lines indicate which way filters can flow from one table to another.</span></span> <span data-ttu-id="af7ca-127">For example, if a filter is placed on **Time[Date]**, in the current schema it would only filter down values in the **Sales** table.</span><span class="sxs-lookup"><span data-stu-id="af7ca-127">For example, if a filter is placed on **Time[Date]**, in the current schema it would only filter down values in the **Sales** table.</span></span> <span data-ttu-id="af7ca-128">No other tables would be affected by this filter since all of the arrows on the relationship lines point to the sales table and not away.</span><span class="sxs-lookup"><span data-stu-id="af7ca-128">No other tables would be affected by this filter since all of the arrows on the relationship lines point to the sales table and not away.</span></span>
* <span data-ttu-id="af7ca-129">The **District** table indicates who the manager is for each district:</span><span class="sxs-lookup"><span data-stu-id="af7ca-129">The **District** table indicates who the manager is for each district:</span></span>
  
  ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="af7ca-130">Based on this schema, if we apply a filter to the **District Manager** column in the District table, and if that filter matches the user viewing the report, that filter will also filter down the **Store** and **Sales** tables to only show data for that particular district manager.</span><span class="sxs-lookup"><span data-stu-id="af7ca-130">Based on this schema, if we apply a filter to the **District Manager** column in the District table, and if that filter matches the user viewing the report, that filter will also filter down the **Store** and **Sales** tables to only show data for that particular district manager.</span></span>

<span data-ttu-id="af7ca-131">Here’s how:</span><span class="sxs-lookup"><span data-stu-id="af7ca-131">Here’s how:</span></span>

1. <span data-ttu-id="af7ca-132">On the Modeling tab, click **Manage Roles**.</span><span class="sxs-lookup"><span data-stu-id="af7ca-132">On the Modeling tab, click **Manage Roles**.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="af7ca-133">Create a new role called **Manager**.</span><span class="sxs-lookup"><span data-stu-id="af7ca-133">Create a new role called **Manager**.</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="af7ca-134">In the **District** table enter the following DAX expression: **[District Manager] = USERNAME()**</span><span class="sxs-lookup"><span data-stu-id="af7ca-134">In the **District** table enter the following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="af7ca-135">To make sure the rules are working, on the **Modeling** tab, click **View as Roles**, and then enter the following:</span><span class="sxs-lookup"><span data-stu-id="af7ca-135">To make sure the rules are working, on the **Modeling** tab, click **View as Roles**, and then enter the following:</span></span>  
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="af7ca-136">The reports will now show data as if you were signed in as **Andrew Ma**.</span><span class="sxs-lookup"><span data-stu-id="af7ca-136">The reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="af7ca-137">Applying the filter, the way we did here, will filter down all records in the **District**, **Store**, and **Sales** tables.</span><span class="sxs-lookup"><span data-stu-id="af7ca-137">Applying the filter, the way we did here, will filter down all records in the **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="af7ca-138">However, because of the filter direction on the relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span><span class="sxs-lookup"><span data-stu-id="af7ca-138">However, because of the filter direction on the relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="af7ca-139">That may be ok for this requirement, however, if we don’t want managers to see items for which they don’t have any sales, we could turn on bidirectional cross-filtering for the relationship and flow the security filter in both directions.</span><span class="sxs-lookup"><span data-stu-id="af7ca-139">That may be ok for this requirement, however, if we don’t want managers to see items for which they don’t have any sales, we could turn on bidirectional cross-filtering for the relationship and flow the security filter in both directions.</span></span> <span data-ttu-id="af7ca-140">This can be done by editing the relationship between **Sales** and **Item**, like this:</span><span class="sxs-lookup"><span data-stu-id="af7ca-140">This can be done by editing the relationship between **Sales** and **Item**, like this:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="af7ca-141">Now, filters can also flow from the Sales table to the **Item** table:</span><span class="sxs-lookup"><span data-stu-id="af7ca-141">Now, filters can also flow from the Sales table to the **Item** table:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="af7ca-142">If you're using DirectQuery mode for your data, you will need to enable bidirectional-cross filtering by selecting these two options:</span><span class="sxs-lookup"><span data-stu-id="af7ca-142">If you're using DirectQuery mode for your data, you will need to enable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="af7ca-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="af7ca-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="af7ca-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span><span class="sxs-lookup"><span data-stu-id="af7ca-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="af7ca-145">To learn more about bidirectional cross-filtering, download the [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span><span class="sxs-lookup"><span data-stu-id="af7ca-145">To learn more about bidirectional cross-filtering, download the [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="af7ca-146">This wraps up all the work that needs to be done in Power BI Desktop, but there’s one more piece of work that needs to be done to make the RLS rules we defined work in Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="af7ca-146">This wraps up all the work that needs to be done in Power BI Desktop, but there’s one more piece of work that needs to be done to make the RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="af7ca-147">Users are authenticated and authorized by your application and App tokens are used to grant that user access to a specific Power BI Embedded report.</span><span class="sxs-lookup"><span data-stu-id="af7ca-147">Users are authenticated and authorized by your application and App tokens are used to grant that user access to a specific Power BI Embedded report.</span></span> <span data-ttu-id="af7ca-148">Power BI Embedded doesn’t have any specific information on who your user is.</span><span class="sxs-lookup"><span data-stu-id="af7ca-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="af7ca-149">For RLS to work, you’ll need to pass some additional context as part of your app token:</span><span class="sxs-lookup"><span data-stu-id="af7ca-149">For RLS to work, you’ll need to pass some additional context as part of your app token:</span></span>

* <span data-ttu-id="af7ca-150">**username** (optional) – Used with RLS this is a string that can be used to help identify the user when applying RLS rules.</span><span class="sxs-lookup"><span data-stu-id="af7ca-150">**username** (optional) – Used with RLS this is a string that can be used to help identify the user when applying RLS rules.</span></span> <span data-ttu-id="af7ca-151">See Using Row Level Security with Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="af7ca-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="af7ca-152">**roles** – A string containing the roles to select when applying Row Level Security rules.</span><span class="sxs-lookup"><span data-stu-id="af7ca-152">**roles** – A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="af7ca-153">If passing more than one role, they should be passed as a string array.</span><span class="sxs-lookup"><span data-stu-id="af7ca-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="af7ca-154">You create the token by using the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span><span class="sxs-lookup"><span data-stu-id="af7ca-154">You create the token by using the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="af7ca-155">If the username property is present, you must also pass at least one value in roles.</span><span class="sxs-lookup"><span data-stu-id="af7ca-155">If the username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="af7ca-156">For example, you could change the EmbedSample.</span><span class="sxs-lookup"><span data-stu-id="af7ca-156">For example, you could change the EmbedSample.</span></span> <span data-ttu-id="af7ca-157">DashboardController line 55 could be updated from</span><span class="sxs-lookup"><span data-stu-id="af7ca-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="af7ca-158">to</span><span class="sxs-lookup"><span data-stu-id="af7ca-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="af7ca-159">The full app token will look something like this:</span><span class="sxs-lookup"><span data-stu-id="af7ca-159">The full app token will look something like this:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="af7ca-160">Now, with all the pieces together, when someone logs into our application to view this report, they’ll only be able to see the data that they are allowed to see, as defined by our row-level security.</span><span class="sxs-lookup"><span data-stu-id="af7ca-160">Now, with all the pieces together, when someone logs into our application to view this report, they’ll only be able to see the data that they are allowed to see, as defined by our row-level security.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/power-bi-embedded/media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="af7ca-161">See also</span><span class="sxs-lookup"><span data-stu-id="af7ca-161">See also</span></span>

[<span data-ttu-id="af7ca-162">Row-level security (RLS) with Power</span><span class="sxs-lookup"><span data-stu-id="af7ca-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="af7ca-163">Authenticating and authorizing in Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="af7ca-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="af7ca-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="af7ca-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="af7ca-165">JavaScript Embed Sample</span><span class="sxs-lookup"><span data-stu-id="af7ca-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="af7ca-166">More questions?</span><span class="sxs-lookup"><span data-stu-id="af7ca-166">More questions?</span></span> [<span data-ttu-id="af7ca-167">Try the Power BI Community</span><span class="sxs-lookup"><span data-stu-id="af7ca-167">Try the Power BI Community</span></span>](http://community.powerbi.com/)














