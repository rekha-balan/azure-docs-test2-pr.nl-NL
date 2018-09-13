---
title: Get insights from Azure Security Center data with Power BI | Microsoft Docs
description: The Azure Security Center Power BI content pack makes it easy to find  security alerts, recommendations, attacked resources and trends, based on a dataset that has been created for your reporting.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: ''
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 568e1108a13f56f9ea097b87586040e8ee8d9746
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552134"
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a><span data-ttu-id="93363-103">Get insights from Azure Security Center data with Power BI</span><span class="sxs-lookup"><span data-stu-id="93363-103">Get insights from Azure Security Center data with Power BI</span></span>
<span data-ttu-id="93363-104">The [Power BI Dashboard](http://aka.ms/azure-security-center-power-bi) for Azure Security Center enables you to visualize, analyze, and filter recommendations and security alerts from anywhere, including your mobile device.</span><span class="sxs-lookup"><span data-stu-id="93363-104">The [Power BI Dashboard](http://aka.ms/azure-security-center-power-bi) for Azure Security Center enables you to visualize, analyze, and filter recommendations and security alerts from anywhere, including your mobile device.</span></span> <span data-ttu-id="93363-105">Use the Power BI dashboard to reveal trends and attack patterns - view security alerts by resource or source IP address and unaddressed security risks by resource or age.</span><span class="sxs-lookup"><span data-stu-id="93363-105">Use the Power BI dashboard to reveal trends and attack patterns - view security alerts by resource or source IP address and unaddressed security risks by resource or age.</span></span>

<span data-ttu-id="93363-106">You can also mash up Security Center recommendations and security alerts with other data in interesting ways, for example using data from [Azure Audit Logs](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) and [Azure SQL Database Auditing](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="93363-106">You can also mash up Security Center recommendations and security alerts with other data in interesting ways, for example using data from [Azure Audit Logs](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) and [Azure SQL Database Auditing](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/).</span></span> <span data-ttu-id="93363-107">Both offer Power BI Dashboards, and you can also export this data to Excel for easy reporting on the security state of your cloud resources.</span><span class="sxs-lookup"><span data-stu-id="93363-107">Both offer Power BI Dashboards, and you can also export this data to Excel for easy reporting on the security state of your cloud resources.</span></span>

## <a name="using-azure-security-center-dashboard-to-access-power-bi"></a><span data-ttu-id="93363-108">Using Azure Security Center dashboard to access Power BI</span><span class="sxs-lookup"><span data-stu-id="93363-108">Using Azure Security Center dashboard to access Power BI</span></span>
<span data-ttu-id="93363-109">You can also use the Azure Security Center dashboard to access Power BI reports.</span><span class="sxs-lookup"><span data-stu-id="93363-109">You can also use the Azure Security Center dashboard to access Power BI reports.</span></span> <span data-ttu-id="93363-110">Follow the steps to perform this task:</span><span class="sxs-lookup"><span data-stu-id="93363-110">Follow the steps to perform this task:</span></span>

1. <span data-ttu-id="93363-111">In the **Azure Security Center** dashboard, click **Power BI** button.</span><span class="sxs-lookup"><span data-stu-id="93363-111">In the **Azure Security Center** dashboard, click **Power BI** button.</span></span>

    ![Connect to Azure Security Center using Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig1-new10-2017.png)
2. <span data-ttu-id="93363-113">The **Power BI** blade opens on the right side as shown in the following screen:</span><span class="sxs-lookup"><span data-stu-id="93363-113">The **Power BI** blade opens on the right side as shown in the following screen:</span></span>

    ![Connect to Azure Security Center using Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. <span data-ttu-id="93363-115">If you are creating the Power BI dashboard for the first time, you can choose one of the following options in the **Explore in Power BI** blade:</span><span class="sxs-lookup"><span data-stu-id="93363-115">If you are creating the Power BI dashboard for the first time, you can choose one of the following options in the **Explore in Power BI** blade:</span></span>

   * <span data-ttu-id="93363-116">**Security insights dashboard**: choose this option if you want to create a dashboard that includes security status, threads, and detections.</span><span class="sxs-lookup"><span data-stu-id="93363-116">**Security insights dashboard**: choose this option if you want to create a dashboard that includes security status, threads, and detections.</span></span> <span data-ttu-id="93363-117">This option is a more common for DevOps role that is responsible for analyzing their protection status and detected alerts across subscriptions.</span><span class="sxs-lookup"><span data-stu-id="93363-117">This option is a more common for DevOps role that is responsible for analyzing their protection status and detected alerts across subscriptions.</span></span>
   * <span data-ttu-id="93363-118">**Policy management dashboard**: choose this option if you want to explore management and enforcement policy.</span><span class="sxs-lookup"><span data-stu-id="93363-118">**Policy management dashboard**: choose this option if you want to explore management and enforcement policy.</span></span>  <span data-ttu-id="93363-119">This option is a more common for Central IT who are more focused on governance.</span><span class="sxs-lookup"><span data-stu-id="93363-119">This option is a more common for Central IT who are more focused on governance.</span></span> <span data-ttu-id="93363-120">They can use this dashboard to gain visibility and insights on security policy adherence across their organization.</span><span class="sxs-lookup"><span data-stu-id="93363-120">They can use this dashboard to gain visibility and insights on security policy adherence across their organization.</span></span>
   * <span data-ttu-id="93363-121">If you already have a Power BI dashboard, click **Go to your current Power BI dashboard**.</span><span class="sxs-lookup"><span data-stu-id="93363-121">If you already have a Power BI dashboard, click **Go to your current Power BI dashboard**.</span></span>
4. <span data-ttu-id="93363-122">For this example, click **Security insights dashboard** option.</span><span class="sxs-lookup"><span data-stu-id="93363-122">For this example, click **Security insights dashboard** option.</span></span> <span data-ttu-id="93363-123">If this is the first time, you are creating a Power BI dashboard for Security Center you are prompted to install the content pack.</span><span class="sxs-lookup"><span data-stu-id="93363-123">If this is the first time, you are creating a Power BI dashboard for Security Center you are prompted to install the content pack.</span></span> <span data-ttu-id="93363-124">Click **Get** button in the **Content packs for Power BI** window as shown in the following screen:</span><span class="sxs-lookup"><span data-stu-id="93363-124">Click **Get** button in the **Content packs for Power BI** window as shown in the following screen:</span></span>

    ![Azure Security Center Security Insights dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. <span data-ttu-id="93363-126">The **Connect to Azure Security Center Security Insights** window appear.</span><span class="sxs-lookup"><span data-stu-id="93363-126">The **Connect to Azure Security Center Security Insights** window appear.</span></span> <span data-ttu-id="93363-127">Make sure the **Authentication** method is **oAuth2** as shown below and click **Sign in** button.</span><span class="sxs-lookup"><span data-stu-id="93363-127">Make sure the **Authentication** method is **oAuth2** as shown below and click **Sign in** button.</span></span>

    ![Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. <span data-ttu-id="93363-129">You may be asked to authenticate again with your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="93363-129">You may be asked to authenticate again with your Azure credentials.</span></span> <span data-ttu-id="93363-130">After authenticating your dashboard will be created.</span><span class="sxs-lookup"><span data-stu-id="93363-130">After authenticating your dashboard will be created.</span></span> <span data-ttu-id="93363-131">Once the dashboard is created you see a report with the similar structure as shown in the following screen:</span><span class="sxs-lookup"><span data-stu-id="93363-131">Once the dashboard is created you see a report with the similar structure as shown in the following screen:</span></span>

    ![Power BI Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> <span data-ttu-id="93363-133">A refresh of the report is scheduled to take place on a daily basis.</span><span class="sxs-lookup"><span data-stu-id="93363-133">A refresh of the report is scheduled to take place on a daily basis.</span></span> <span data-ttu-id="93363-134">In case you experience a failure on this refresh, read [Potential Refresh Issues with the Azure Security Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), for more information on how to troubleshoot.</span><span class="sxs-lookup"><span data-stu-id="93363-134">In case you experience a failure on this refresh, read [Potential Refresh Issues with the Azure Security Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), for more information on how to troubleshoot.</span></span>
>
>

<span data-ttu-id="93363-135">Here you can see the number of security alerts and recommendations, as well as the number of VMs, Azure SQL databases, and network resources being monitored by Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="93363-135">Here you can see the number of security alerts and recommendations, as well as the number of VMs, Azure SQL databases, and network resources being monitored by Azure Security Center.</span></span>

<span data-ttu-id="93363-136">A link to Azure Security Center redirects you to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="93363-136">A link to Azure Security Center redirects you to the Azure portal.</span></span> <span data-ttu-id="93363-137">The charts make it easy to visualize information about security recommendations and alerts, including:</span><span class="sxs-lookup"><span data-stu-id="93363-137">The charts make it easy to visualize information about security recommendations and alerts, including:</span></span>

* <span data-ttu-id="93363-138">Resource Security State</span><span class="sxs-lookup"><span data-stu-id="93363-138">Resource Security State</span></span>
* <span data-ttu-id="93363-139">Pending Recommendations</span><span class="sxs-lookup"><span data-stu-id="93363-139">Pending Recommendations</span></span>
* <span data-ttu-id="93363-140">VM Recommendations</span><span class="sxs-lookup"><span data-stu-id="93363-140">VM Recommendations</span></span>
* <span data-ttu-id="93363-141">Alerts over Time</span><span class="sxs-lookup"><span data-stu-id="93363-141">Alerts over Time</span></span>
* <span data-ttu-id="93363-142">Attacked Resources</span><span class="sxs-lookup"><span data-stu-id="93363-142">Attacked Resources</span></span>
* <span data-ttu-id="93363-143">Attacked IPs</span><span class="sxs-lookup"><span data-stu-id="93363-143">Attacked IPs</span></span>

<span data-ttu-id="93363-144">Behind each chart, there are additional insights.</span><span class="sxs-lookup"><span data-stu-id="93363-144">Behind each chart, there are additional insights.</span></span> <span data-ttu-id="93363-145">Select a tile to see more information.</span><span class="sxs-lookup"><span data-stu-id="93363-145">Select a tile to see more information.</span></span> <span data-ttu-id="93363-146">For example, the **Resource Security State** tile shows you additional details about pending recommendations by resources as shown in the following screen:</span><span class="sxs-lookup"><span data-stu-id="93363-146">For example, the **Resource Security State** tile shows you additional details about pending recommendations by resources as shown in the following screen:</span></span>

![Recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

<span data-ttu-id="93363-148">If you click on any line of this graph, the others are going to gray out and you focus only on the one you selected.</span><span class="sxs-lookup"><span data-stu-id="93363-148">If you click on any line of this graph, the others are going to gray out and you focus only on the one you selected.</span></span> <span data-ttu-id="93363-149">To return to the dashboard, click **Azure Security Center** under the **Dashboards** option on the left pane of this page.</span><span class="sxs-lookup"><span data-stu-id="93363-149">To return to the dashboard, click **Azure Security Center** under the **Dashboards** option on the left pane of this page.</span></span>

> [!NOTE]
> <span data-ttu-id="93363-150">If you’d like to customize your reports by adding additional fields or changing existing visuals, you can edit the report.</span><span class="sxs-lookup"><span data-stu-id="93363-150">If you’d like to customize your reports by adding additional fields or changing existing visuals, you can edit the report.</span></span> <span data-ttu-id="93363-151">Read [Interact with a report in Editing View in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) for more information.</span><span class="sxs-lookup"><span data-stu-id="93363-151">Read [Interact with a report in Editing View in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) for more information.</span></span>
>
>

<span data-ttu-id="93363-152">The **Alerts over Time, Attacked Resources** and **Attacker IPs** tiles will have the similar output when you click on each one of it.</span><span class="sxs-lookup"><span data-stu-id="93363-152">The **Alerts over Time, Attacked Resources** and **Attacker IPs** tiles will have the similar output when you click on each one of it.</span></span> <span data-ttu-id="93363-153">This happens because the report aggregates information regarding all those three variables and calls it **Resources under Attack** as shown in the following screen:</span><span class="sxs-lookup"><span data-stu-id="93363-153">This happens because the report aggregates information regarding all those three variables and calls it **Resources under Attack** as shown in the following screen:</span></span>

![Resources under attack](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

<span data-ttu-id="93363-155">At this point you can also save a copy of this report, print it or publish it on the web by using the options available in the **File** menu.</span><span class="sxs-lookup"><span data-stu-id="93363-155">At this point you can also save a copy of this report, print it or publish it on the web by using the options available in the **File** menu.</span></span>

![File menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a><span data-ttu-id="93363-157">Exploring your Azure Security Center data with Power BI services</span><span class="sxs-lookup"><span data-stu-id="93363-157">Exploring your Azure Security Center data with Power BI services</span></span>
<span data-ttu-id="93363-158">Connect to the [Power BI Content Pack Services](https://msit.powerbi.com/groups/me/getdata/services) in Power BI and execute the following steps:</span><span class="sxs-lookup"><span data-stu-id="93363-158">Connect to the [Power BI Content Pack Services](https://msit.powerbi.com/groups/me/getdata/services) in Power BI and execute the following steps:</span></span>

1. <span data-ttu-id="93363-159">In the **Content Pack for Power BI** window you will see two options as shown below.</span><span class="sxs-lookup"><span data-stu-id="93363-159">In the **Content Pack for Power BI** window you will see two options as shown below.</span></span>

    ![Content pack for Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > <span data-ttu-id="93363-161">If already executed the first part of this article you will see only one option, which is Azure Security Center Policy Management.</span><span class="sxs-lookup"><span data-stu-id="93363-161">If already executed the first part of this article you will see only one option, which is Azure Security Center Policy Management.</span></span>
   >
   >
2. <span data-ttu-id="93363-162">For the purpose of this example, click **Get** in the **Azure Security Center Policy Management** tile.</span><span class="sxs-lookup"><span data-stu-id="93363-162">For the purpose of this example, click **Get** in the **Azure Security Center Policy Management** tile.</span></span>
3. <span data-ttu-id="93363-163">In the **Connect to Azure Security Center Policy Management** window, make sure to select **oAuth2** under **Authentication Method** drop down as shown below and click **Sign in** button.</span><span class="sxs-lookup"><span data-stu-id="93363-163">In the **Connect to Azure Security Center Policy Management** window, make sure to select **oAuth2** under **Authentication Method** drop down as shown below and click **Sign in** button.</span></span>

    ![Policy Management window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. <span data-ttu-id="93363-165">You will be redirected to an authentication page where you should type the credentials that you are using to connect to Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="93363-165">You will be redirected to an authentication page where you should type the credentials that you are using to connect to Azure Security Center.</span></span> <span data-ttu-id="93363-166">After the authentication process is complete, Power BI will start importing data to build your reports.</span><span class="sxs-lookup"><span data-stu-id="93363-166">After the authentication process is complete, Power BI will start importing data to build your reports.</span></span> <span data-ttu-id="93363-167">During this time you may see the following message on the right corner of your browser:</span><span class="sxs-lookup"><span data-stu-id="93363-167">During this time you may see the following message on the right corner of your browser:</span></span>

    ![Connect to Azure Security Center using Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > <span data-ttu-id="93363-169">when the dashboard is being created for the first time it can take longer than usual, mainly for scenarios where you have multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="93363-169">when the dashboard is being created for the first time it can take longer than usual, mainly for scenarios where you have multiple subscriptions.</span></span>
   >
   >
5. <span data-ttu-id="93363-170">Once the process is finished, your Azure Security Center Power BI dashboard will load with the **Policy Management** report similar to the one shown below:</span><span class="sxs-lookup"><span data-stu-id="93363-170">Once the process is finished, your Azure Security Center Power BI dashboard will load with the **Policy Management** report similar to the one shown below:</span></span>

    ![Policy Management dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a><span data-ttu-id="93363-172">See also</span><span class="sxs-lookup"><span data-stu-id="93363-172">See also</span></span>
<span data-ttu-id="93363-173">In this document, you learned how to use Power BI in Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="93363-173">In this document, you learned how to use Power BI in Azure Security Center.</span></span> <span data-ttu-id="93363-174">To learn more about Azure Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="93363-174">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="93363-175">[Azure Security Center Planning and Operations Guide](security-center-planning-and-operations-guide.md) — Learn how to plan Azure Security Center adoption.</span><span class="sxs-lookup"><span data-stu-id="93363-175">[Azure Security Center Planning and Operations Guide](security-center-planning-and-operations-guide.md) — Learn how to plan Azure Security Center adoption.</span></span>
* <span data-ttu-id="93363-176">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security settings in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="93363-176">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security settings in Azure Security Center</span></span>
* <span data-ttu-id="93363-177">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts</span><span class="sxs-lookup"><span data-stu-id="93363-177">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts</span></span>
* <span data-ttu-id="93363-178">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service</span><span class="sxs-lookup"><span data-stu-id="93363-178">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service</span></span>
* <span data-ttu-id="93363-179">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance</span><span class="sxs-lookup"><span data-stu-id="93363-179">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance</span></span>












