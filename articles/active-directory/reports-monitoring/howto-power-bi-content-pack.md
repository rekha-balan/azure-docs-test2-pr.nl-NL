---
title: How to use the Azure Active Directory Power BI Content Pack | Microsoft Docs
description: Learn how to use the Azure Active Directory Power BI Content Pack
services: active-directory
author: priyamohanram
manager: mtillman
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: ''
ms.topic: conceptual
ms.tgt_pltfrm: ''
ms.workload: identity
ms.component: report-monitor
ms.date: 12/06/2017
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 752e71f3c6b22a6d9f1e2392b58c01deef9de89c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965697"
---
# <a name="how-to-use-the-azure-active-directory-power-bi-content-pack"></a><span data-ttu-id="96614-103">How to use the Azure Active Directory Power BI Content Pack</span><span class="sxs-lookup"><span data-stu-id="96614-103">How to use the Azure Active Directory Power BI Content Pack</span></span>

|  |
|--|
|<span data-ttu-id="96614-104">Currently, the Azure AD Power BI content pack uses the Azure AD Graph APIs to retrieve data from your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="96614-104">Currently, the Azure AD Power BI content pack uses the Azure AD Graph APIs to retrieve data from your Azure AD tenant.</span></span> <span data-ttu-id="96614-105">As a result, you may see some disparity between the data available in the content pack and the data retrieved using the [Microsoft Graph APIs for reporting](concept-reporting-api.md).</span><span class="sxs-lookup"><span data-stu-id="96614-105">As a result, you may see some disparity between the data available in the content pack and the data retrieved using the [Microsoft Graph APIs for reporting](concept-reporting-api.md).</span></span> |
|  |

<span data-ttu-id="96614-106">Understanding how your users adopt and use Azure Active Directory features is critical for you as an IT admin. It allows you to plan your IT infrastructure and communication to increase usage and to get the most out of AAD features.</span><span class="sxs-lookup"><span data-stu-id="96614-106">Understanding how your users adopt and use Azure Active Directory features is critical for you as an IT admin. It allows you to plan your IT infrastructure and communication to increase usage and to get the most out of AAD features.</span></span> <span data-ttu-id="96614-107">Power BI Content Pack for Azure Active Directory gives you the ability to further analyze your data to understand how you can use this data to gather richer insights into what’s going on with their Azure Active Directory for the various capabilities you heavily rely on.</span><span class="sxs-lookup"><span data-stu-id="96614-107">Power BI Content Pack for Azure Active Directory gives you the ability to further analyze your data to understand how you can use this data to gather richer insights into what’s going on with their Azure Active Directory for the various capabilities you heavily rely on.</span></span>  <span data-ttu-id="96614-108">With the integration of Azure Active Directory APIs into Power BI, you can easily download the pre-built content packs and gain insights to all the activities within your Azure Active Directory using rich visualization experience Power BI offers.</span><span class="sxs-lookup"><span data-stu-id="96614-108">With the integration of Azure Active Directory APIs into Power BI, you can easily download the pre-built content packs and gain insights to all the activities within your Azure Active Directory using rich visualization experience Power BI offers.</span></span> <span data-ttu-id="96614-109">You can create your own dashboard and share it easily with anyone in your organization.</span><span class="sxs-lookup"><span data-stu-id="96614-109">You can create your own dashboard and share it easily with anyone in your organization.</span></span> 

<span data-ttu-id="96614-110">This topic provides you with step-by-step instructions on how to install and use the content pack in your environment.</span><span class="sxs-lookup"><span data-stu-id="96614-110">This topic provides you with step-by-step instructions on how to install and use the content pack in your environment.</span></span>

## <a name="installation"></a><span data-ttu-id="96614-111">Installation</span><span class="sxs-lookup"><span data-stu-id="96614-111">Installation</span></span>  

<span data-ttu-id="96614-112">**To install the Power BI Content Pack:**</span><span class="sxs-lookup"><span data-stu-id="96614-112">**To install the Power BI Content Pack:**</span></span>

1. <span data-ttu-id="96614-113">Log into [Power BI](https://app.powerbi.com/groups/me/getdata/services) with your Power BI Account (this is the same account as your O365 or Azure AD Account).</span><span class="sxs-lookup"><span data-stu-id="96614-113">Log into [Power BI](https://app.powerbi.com/groups/me/getdata/services) with your Power BI Account (this is the same account as your O365 or Azure AD Account).</span></span>

2. <span data-ttu-id="96614-114">At the bottom of the left navigation pane, select **Get Data**.</span><span class="sxs-lookup"><span data-stu-id="96614-114">At the bottom of the left navigation pane, select **Get Data**.</span></span>

    ![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/01.png)
 
3. <span data-ttu-id="96614-116">In the **Services** box, click **Get**.</span><span class="sxs-lookup"><span data-stu-id="96614-116">In the **Services** box, click **Get**.</span></span>
   
    ![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/02.png)

4.  <span data-ttu-id="96614-118">Search for **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="96614-118">Search for **Azure Active Directory**.</span></span>

    ![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/03.png)
 
5.  <span data-ttu-id="96614-120">When prompted, type your Azure AD Tenant ID, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="96614-120">When prompted, type your Azure AD Tenant ID, and then click **Next**.</span></span>

    > [!TIP] 
    > <span data-ttu-id="96614-121">A quick way to get the Tenant ID for your Office 365 / Azure AD tenant is to sign in to the Azure AD portal, drill down to the directory, and copy the **Directory ID** from the [**Properties** page](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Properties).</span><span class="sxs-lookup"><span data-stu-id="96614-121">A quick way to get the Tenant ID for your Office 365 / Azure AD tenant is to sign in to the Azure AD portal, drill down to the directory, and copy the **Directory ID** from the [**Properties** page](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Properties).</span></span>

    ![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/04.png) 

6.  <span data-ttu-id="96614-123">Click **Sign-in**.</span><span class="sxs-lookup"><span data-stu-id="96614-123">Click **Sign-in**.</span></span> 
 
    ![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/05.png) 



7.  <span data-ttu-id="96614-125">Enter your username and password, and then click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="96614-125">Enter your username and password, and then click **Sign in**.</span></span>
 
    ![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/06.png) 

8.  <span data-ttu-id="96614-127">On the app consent dialog, click **Accept**.</span><span class="sxs-lookup"><span data-stu-id="96614-127">On the app consent dialog, click **Accept**.</span></span>
 
9.  <span data-ttu-id="96614-128">When your Azure Active Directory Activity logs dashboard has been created, click it.</span><span class="sxs-lookup"><span data-stu-id="96614-128">When your Azure Active Directory Activity logs dashboard has been created, click it.</span></span>
 
    ![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a><span data-ttu-id="96614-130">What can I do with this content pack?</span><span class="sxs-lookup"><span data-stu-id="96614-130">What can I do with this content pack?</span></span>

<span data-ttu-id="96614-131">Before we jump into what you can do with this content pack, here’s quick preview of the various reports in the content pack.</span><span class="sxs-lookup"><span data-stu-id="96614-131">Before we jump into what you can do with this content pack, here’s quick preview of the various reports in the content pack.</span></span> <span data-ttu-id="96614-132">Report data goes back to the **last 30 days**.</span><span class="sxs-lookup"><span data-stu-id="96614-132">Report data goes back to the **last 30 days**.</span></span>

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a><span data-ttu-id="96614-133">Reports included in this version of Azure Active Directory logs Content Pack</span><span class="sxs-lookup"><span data-stu-id="96614-133">Reports included in this version of Azure Active Directory logs Content Pack</span></span>

<span data-ttu-id="96614-134">**App Usage and Trend report**:  Get insights into the apps used in your organization and which ones are being used the most and when.</span><span class="sxs-lookup"><span data-stu-id="96614-134">**App Usage and Trend report**:  Get insights into the apps used in your organization and which ones are being used the most and when.</span></span> <span data-ttu-id="96614-135">You can use this report to gather insights into how an app you recently rolled out in your organization is being used or find out which apps are popular.</span><span class="sxs-lookup"><span data-stu-id="96614-135">You can use this report to gather insights into how an app you recently rolled out in your organization is being used or find out which apps are popular.</span></span> <span data-ttu-id="96614-136">By doing this, you can improve usage if you see if the app is not being used.</span><span class="sxs-lookup"><span data-stu-id="96614-136">By doing this, you can improve usage if you see if the app is not being used.</span></span>

<span data-ttu-id="96614-137">**Sign-ins by location and users**: Get insights into all the sign-ins performed using Azure Identity and gives insights into the identity of the users.</span><span class="sxs-lookup"><span data-stu-id="96614-137">**Sign-ins by location and users**: Get insights into all the sign-ins performed using Azure Identity and gives insights into the identity of the users.</span></span> <span data-ttu-id="96614-138">With this, you can dig deeper into individual sign-ins and answer questions like:</span><span class="sxs-lookup"><span data-stu-id="96614-138">With this, you can dig deeper into individual sign-ins and answer questions like:</span></span>

- <span data-ttu-id="96614-139">From where did this user sign-ins?</span><span class="sxs-lookup"><span data-stu-id="96614-139">From where did this user sign-ins?</span></span>
- <span data-ttu-id="96614-140">Which user has the most sign-ins and where do they sign-in from?</span><span class="sxs-lookup"><span data-stu-id="96614-140">Which user has the most sign-ins and where do they sign-in from?</span></span> 
- <span data-ttu-id="96614-141">Was the sign-in successful?</span><span class="sxs-lookup"><span data-stu-id="96614-141">Was the sign-in successful?</span></span>  
 
<span data-ttu-id="96614-142">You can drill into details by clicking on a specific date or location.</span><span class="sxs-lookup"><span data-stu-id="96614-142">You can drill into details by clicking on a specific date or location.</span></span>

<span data-ttu-id="96614-143">**Unique users per app**:  Get a view of all unique users using a given app.</span><span class="sxs-lookup"><span data-stu-id="96614-143">**Unique users per app**:  Get a view of all unique users using a given app.</span></span> <span data-ttu-id="96614-144">This includes only users who have “*successfully*” signed into an application.</span><span class="sxs-lookup"><span data-stu-id="96614-144">This includes only users who have “*successfully*” signed into an application.</span></span>

<span data-ttu-id="96614-145">**Device sign-ins**: Get a view of the type of OS and browsers are being used by users in your organization with detailed information on the users including:</span><span class="sxs-lookup"><span data-stu-id="96614-145">**Device sign-ins**: Get a view of the type of OS and browsers are being used by users in your organization with detailed information on the users including:</span></span>

- <span data-ttu-id="96614-146">User Name</span><span class="sxs-lookup"><span data-stu-id="96614-146">User Name</span></span>
- <span data-ttu-id="96614-147">IP Address</span><span class="sxs-lookup"><span data-stu-id="96614-147">IP Address</span></span>
- <span data-ttu-id="96614-148">Location</span><span class="sxs-lookup"><span data-stu-id="96614-148">Location</span></span> 
- <span data-ttu-id="96614-149">Sign-in status</span><span class="sxs-lookup"><span data-stu-id="96614-149">Sign-in status</span></span> 

<span data-ttu-id="96614-150">With this report, you can understand the various device profiles used within your organization and determine device policies based on what’s used</span><span class="sxs-lookup"><span data-stu-id="96614-150">With this report, you can understand the various device profiles used within your organization and determine device policies based on what’s used</span></span>

<span data-ttu-id="96614-151">**SSPR Funnel**: Get an understanding on how password resets are being done in your organization.</span><span class="sxs-lookup"><span data-stu-id="96614-151">**SSPR Funnel**: Get an understanding on how password resets are being done in your organization.</span></span> <span data-ttu-id="96614-152">Get a peek into how many password resets were attempted through the SSPR tool and how many of them were successful.</span><span class="sxs-lookup"><span data-stu-id="96614-152">Get a peek into how many password resets were attempted through the SSPR tool and how many of them were successful.</span></span> <span data-ttu-id="96614-153">Dig deeper into the Password resets failure using the SSPR funnel and understand why certain failures occurred.</span><span class="sxs-lookup"><span data-stu-id="96614-153">Dig deeper into the Password resets failure using the SSPR funnel and understand why certain failures occurred.</span></span> <span data-ttu-id="96614-154">This report gives a deeper understanding of how the SSPR tool is used within your organization so you can make the right decisions.</span><span class="sxs-lookup"><span data-stu-id="96614-154">This report gives a deeper understanding of how the SSPR tool is used within your organization so you can make the right decisions.</span></span>

## <a name="customizing-azure-ad-activity-content-pack"></a><span data-ttu-id="96614-155">Customizing Azure AD Activity content pack</span><span class="sxs-lookup"><span data-stu-id="96614-155">Customizing Azure AD Activity content pack</span></span>

<span data-ttu-id="96614-156">**Change Visualization**:  You can change a report visualization by clicking **Edit Report** and select the visualization you want.</span><span class="sxs-lookup"><span data-stu-id="96614-156">**Change Visualization**:  You can change a report visualization by clicking **Edit Report** and select the visualization you want.</span></span>
 
![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/09.png) 
 
![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/10.png) 

<span data-ttu-id="96614-159">**Include additional fields**:  You can add a field to the report or remove it by selecting the visual to which you want to add/remove the field.</span><span class="sxs-lookup"><span data-stu-id="96614-159">**Include additional fields**:  You can add a field to the report or remove it by selecting the visual to which you want to add/remove the field.</span></span> <span data-ttu-id="96614-160">In the example below, I am adding “sign-in status” field to the table view.</span><span class="sxs-lookup"><span data-stu-id="96614-160">In the example below, I am adding “sign-in status” field to the table view.</span></span> 
 
![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/11.png) 

<span data-ttu-id="96614-162">**Pin visualizations to your dashboard**:  You can customize your dashboard and include your own visualizations to the report and pin it to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="96614-162">**Pin visualizations to your dashboard**:  You can customize your dashboard and include your own visualizations to the report and pin it to the dashboard.</span></span> <span data-ttu-id="96614-163">In the example below, I added a new filter called “Sign-in Status” and included it in the report.</span><span class="sxs-lookup"><span data-stu-id="96614-163">In the example below, I added a new filter called “Sign-in Status” and included it in the report.</span></span> <span data-ttu-id="96614-164">I also changed the visualization from bar chart to a line chart and can pin this new visual to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="96614-164">I also changed the visualization from bar chart to a line chart and can pin this new visual to the dashboard.</span></span>

![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/12.png) 

![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/13.png) 
 

 


<span data-ttu-id="96614-167">**Sharing your dashboard**: Once you have created the content you want, you can share the dashboard with the users in your organization.</span><span class="sxs-lookup"><span data-stu-id="96614-167">**Sharing your dashboard**: Once you have created the content you want, you can share the dashboard with the users in your organization.</span></span> <span data-ttu-id="96614-168">Please remember that once you share the report, they can see the fields you have selected in the report.</span><span class="sxs-lookup"><span data-stu-id="96614-168">Please remember that once you share the report, they can see the fields you have selected in the report.</span></span>
 
![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a><span data-ttu-id="96614-170">Scheduling a daily refresh of your Power BI report</span><span class="sxs-lookup"><span data-stu-id="96614-170">Scheduling a daily refresh of your Power BI report</span></span>

<span data-ttu-id="96614-171">To schedule a daily refresh of your Power BI report, go to **Datasets > Settings > Schedule Refresh** and set it as shown below.</span><span class="sxs-lookup"><span data-stu-id="96614-171">To schedule a daily refresh of your Power BI report, go to **Datasets > Settings > Schedule Refresh** and set it as shown below.</span></span>
 
![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/15.png) 

## <a name="updating-to-newer-version-of-content-pack"></a><span data-ttu-id="96614-173">Updating to newer version of content pack</span><span class="sxs-lookup"><span data-stu-id="96614-173">Updating to newer version of content pack</span></span>

<span data-ttu-id="96614-174">If you want to update your content pack to get a newer version:</span><span class="sxs-lookup"><span data-stu-id="96614-174">If you want to update your content pack to get a newer version:</span></span>

- <span data-ttu-id="96614-175">Download the new content pack and set it up as per instructions listed in this article.</span><span class="sxs-lookup"><span data-stu-id="96614-175">Download the new content pack and set it up as per instructions listed in this article.</span></span>

- <span data-ttu-id="96614-176">Once you have set it up, go to **Data Source > Settings > Data source credentials** and re-enter your credentials as shown below</span><span class="sxs-lookup"><span data-stu-id="96614-176">Once you have set it up, go to **Data Source > Settings > Data source credentials** and re-enter your credentials as shown below</span></span>

    ![Azure Active Directory Power BI Content Pack](./media/howto-power-bi-content-pack/16.png) 

<span data-ttu-id="96614-178">As soon as the new version of the content pack is working, you can remove the old version if needed by deleting the underlying reports and datasets associated with that content pack.</span><span class="sxs-lookup"><span data-stu-id="96614-178">As soon as the new version of the content pack is working, you can remove the old version if needed by deleting the underlying reports and datasets associated with that content pack.</span></span>

## <a name="still-having-issues"></a><span data-ttu-id="96614-179">Still having issues?</span><span class="sxs-lookup"><span data-stu-id="96614-179">Still having issues?</span></span> 

<span data-ttu-id="96614-180">Check out our [troubleshooting guide](troubleshoot-content-pack.md).</span><span class="sxs-lookup"><span data-stu-id="96614-180">Check out our [troubleshooting guide](troubleshoot-content-pack.md).</span></span> <span data-ttu-id="96614-181">For general help with Power BI, check out these [help articles](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).</span><span class="sxs-lookup"><span data-stu-id="96614-181">For general help with Power BI, check out these [help articles](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).</span></span>
 

## <a name="next-steps"></a><span data-ttu-id="96614-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="96614-182">Next steps</span></span>

<span data-ttu-id="96614-183">For an overview of reporting, see the [Azure Active Directory reporting](overview-reports.md).</span><span class="sxs-lookup"><span data-stu-id="96614-183">For an overview of reporting, see the [Azure Active Directory reporting](overview-reports.md).</span></span>
