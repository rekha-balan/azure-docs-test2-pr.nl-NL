---
title: Tutorial - Stream Azure Active Directory logs to an Azure event hub (preview) | Microsoft Docs
description: Learn how to set up Azure Diagnostics to push Azure Active Directory logs to an event hub (preview)
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 045f94b3-6f12-407a-8e9c-ed13ae7b43a3
ms.service: active-directory
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 07/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 1a7f91a0d15dd67d86f83485b4aad01a3bae37b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867382"
---
# <a name="tutorial-stream-azure-ad-logs-to-an-azure-event-hub-preview"></a><span data-ttu-id="7b16b-103">Tutorial: Stream Azure AD logs to an Azure event hub (preview)</span><span class="sxs-lookup"><span data-stu-id="7b16b-103">Tutorial: Stream Azure AD logs to an Azure event hub (preview)</span></span>

<span data-ttu-id="7b16b-104">In this tutorial, learn how to set up Azure Monitor diagnostics settings to stream Azure Active Directory (Azure AD) logs to an Azure event hub.</span><span class="sxs-lookup"><span data-stu-id="7b16b-104">In this tutorial, learn how to set up Azure Monitor diagnostics settings to stream Azure Active Directory (Azure AD) logs to an Azure event hub.</span></span> <span data-ttu-id="7b16b-105">Use this mechanism to integrate your logs with third-party Security Information and Event Management (SIEM) tools, such as Splunk and QRadar.</span><span class="sxs-lookup"><span data-stu-id="7b16b-105">Use this mechanism to integrate your logs with third-party Security Information and Event Management (SIEM) tools, such as Splunk and QRadar.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b16b-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7b16b-106">Prerequisites</span></span> 

<span data-ttu-id="7b16b-107">To use this feature, you need:</span><span class="sxs-lookup"><span data-stu-id="7b16b-107">To use this feature, you need:</span></span>

* <span data-ttu-id="7b16b-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7b16b-108">An Azure subscription.</span></span> <span data-ttu-id="7b16b-109">If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7b16b-109">If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="7b16b-110">An Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="7b16b-110">An Azure AD tenant.</span></span>
* <span data-ttu-id="7b16b-111">A user who's a *global administrator* or *security administrator* for the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="7b16b-111">A user who's a *global administrator* or *security administrator* for the Azure AD tenant.</span></span>
* <span data-ttu-id="7b16b-112">An Event Hubs namespace and an event hub in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7b16b-112">An Event Hubs namespace and an event hub in your Azure subscription.</span></span> <span data-ttu-id="7b16b-113">Learn how to [create an event hub](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span><span class="sxs-lookup"><span data-stu-id="7b16b-113">Learn how to [create an event hub](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

## <a name="archive-logs-to-an-event-hub"></a><span data-ttu-id="7b16b-114">Archive logs to an event hub</span><span class="sxs-lookup"><span data-stu-id="7b16b-114">Archive logs to an event hub</span></span>

1. <span data-ttu-id="7b16b-115">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b16b-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span> 

2. <span data-ttu-id="7b16b-116">Select **Azure Active Directory** > **Activity** > **Audit logs**.</span><span class="sxs-lookup"><span data-stu-id="7b16b-116">Select **Azure Active Directory** > **Activity** > **Audit logs**.</span></span> 

3. <span data-ttu-id="7b16b-117">Select **Export Settings**.</span><span class="sxs-lookup"><span data-stu-id="7b16b-117">Select **Export Settings**.</span></span>  
    
4. <span data-ttu-id="7b16b-118">In the **Diagnostics settings** pane, do either of the following:</span><span class="sxs-lookup"><span data-stu-id="7b16b-118">In the **Diagnostics settings** pane, do either of the following:</span></span>
    * <span data-ttu-id="7b16b-119">To change existing settings, select **Edit setting**.</span><span class="sxs-lookup"><span data-stu-id="7b16b-119">To change existing settings, select **Edit setting**.</span></span>
    * <span data-ttu-id="7b16b-120">To add new settings, select **Add diagnostics setting**.</span><span class="sxs-lookup"><span data-stu-id="7b16b-120">To add new settings, select **Add diagnostics setting**.</span></span>  
      <span data-ttu-id="7b16b-121">You can have up to three settings.</span><span class="sxs-lookup"><span data-stu-id="7b16b-121">You can have up to three settings.</span></span>

      ![Export settings](./media/quickstart-azure-monitor-stream-logs-to-event-hub/ExportSettings.png)

5. <span data-ttu-id="7b16b-123">Select the **Stream to an event hub** check box, and then select **Event Hub/Configure**.</span><span class="sxs-lookup"><span data-stu-id="7b16b-123">Select the **Stream to an event hub** check box, and then select **Event Hub/Configure**.</span></span>

6. <span data-ttu-id="7b16b-124">Select the Azure subscription and Event Hubs namespace that you want to route the logs to.</span><span class="sxs-lookup"><span data-stu-id="7b16b-124">Select the Azure subscription and Event Hubs namespace that you want to route the logs to.</span></span>  
    <span data-ttu-id="7b16b-125">The subscription and Event Hubs namespace must both be associated with the Azure AD tenant that the logs stream from.</span><span class="sxs-lookup"><span data-stu-id="7b16b-125">The subscription and Event Hubs namespace must both be associated with the Azure AD tenant that the logs stream from.</span></span> <span data-ttu-id="7b16b-126">You can also specify an event hub within the Event Hubs namespace to which logs should be sent.</span><span class="sxs-lookup"><span data-stu-id="7b16b-126">You can also specify an event hub within the Event Hubs namespace to which logs should be sent.</span></span> <span data-ttu-id="7b16b-127">If no event hub is specified, an event hub is created in the namespace with the default name **insights-logs-audit**.</span><span class="sxs-lookup"><span data-stu-id="7b16b-127">If no event hub is specified, an event hub is created in the namespace with the default name **insights-logs-audit**.</span></span>

7. <span data-ttu-id="7b16b-128">Select **OK** to exit the event hub configuration.</span><span class="sxs-lookup"><span data-stu-id="7b16b-128">Select **OK** to exit the event hub configuration.</span></span>

8. <span data-ttu-id="7b16b-129">Do either or both of the following:</span><span class="sxs-lookup"><span data-stu-id="7b16b-129">Do either or both of the following:</span></span>
    * <span data-ttu-id="7b16b-130">To send audit logs to the storage account, select the **AuditLogs** check box.</span><span class="sxs-lookup"><span data-stu-id="7b16b-130">To send audit logs to the storage account, select the **AuditLogs** check box.</span></span> 
    * <span data-ttu-id="7b16b-131">To send sign-in logs to the storage account, select the **SignInLogs** check box.</span><span class="sxs-lookup"><span data-stu-id="7b16b-131">To send sign-in logs to the storage account, select the **SignInLogs** check box.</span></span>

9. <span data-ttu-id="7b16b-132">Select **Save** to save the setting.</span><span class="sxs-lookup"><span data-stu-id="7b16b-132">Select **Save** to save the setting.</span></span>

    ![Diagnostics settings](./media/quickstart-azure-monitor-stream-logs-to-event-hub/DiagnosticSettings.png)

10. <span data-ttu-id="7b16b-134">After about 15 minutes, verify that events are displayed in your event hub.</span><span class="sxs-lookup"><span data-stu-id="7b16b-134">After about 15 minutes, verify that events are displayed in your event hub.</span></span> <span data-ttu-id="7b16b-135">To do so, go to the event hub from the portal and verify that the **incoming messages** count is greater than zero.</span><span class="sxs-lookup"><span data-stu-id="7b16b-135">To do so, go to the event hub from the portal and verify that the **incoming messages** count is greater than zero.</span></span> 

    ![Audit logs](./media/quickstart-azure-monitor-stream-logs-to-event-hub/InsightsLogsAudit.png)

## <a name="access-data-from-your-event-hub"></a><span data-ttu-id="7b16b-137">Access data from your event hub</span><span class="sxs-lookup"><span data-stu-id="7b16b-137">Access data from your event hub</span></span>

<span data-ttu-id="7b16b-138">After data is displayed in the event hub, you can access and read the data in two ways:</span><span class="sxs-lookup"><span data-stu-id="7b16b-138">After data is displayed in the event hub, you can access and read the data in two ways:</span></span>

* <span data-ttu-id="7b16b-139">**Configure a supported SIEM tool**.</span><span class="sxs-lookup"><span data-stu-id="7b16b-139">**Configure a supported SIEM tool**.</span></span> <span data-ttu-id="7b16b-140">To read data from the event hub, most tools require the event hub connection string and certain permissions to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7b16b-140">To read data from the event hub, most tools require the event hub connection string and certain permissions to your Azure subscription.</span></span> <span data-ttu-id="7b16b-141">Third-party tools with Azure Monitor integration include, but are not limited to:</span><span class="sxs-lookup"><span data-stu-id="7b16b-141">Third-party tools with Azure Monitor integration include, but are not limited to:</span></span>
    * <span data-ttu-id="7b16b-142">**Splunk**: For more information about integrating Azure AD logs with Splunk, see [Integrate Azure AD logs with Splunk by using Azure Monitor](tutorial-integrate-activity-logs-with-splunk.md).</span><span class="sxs-lookup"><span data-stu-id="7b16b-142">**Splunk**: For more information about integrating Azure AD logs with Splunk, see [Integrate Azure AD logs with Splunk by using Azure Monitor](tutorial-integrate-activity-logs-with-splunk.md).</span></span>
    
    * <span data-ttu-id="7b16b-143">**IBM QRadar**: The DSM and Azure Event Hub Protocol are available for download at [IBM support](http://www.ibm.com/support).</span><span class="sxs-lookup"><span data-stu-id="7b16b-143">**IBM QRadar**: The DSM and Azure Event Hub Protocol are available for download at [IBM support](http://www.ibm.com/support).</span></span> <span data-ttu-id="7b16b-144">For more information about integration with Azure, go to the [IBM QRadar Security Intelligence Platform 7.3.0](https://www.ibm.com/support/knowledgecenter/SS42VS_DSM/c_dsm_guide_microsoft_azure_overview.html?cp=SS42VS_7.3.0) site.</span><span class="sxs-lookup"><span data-stu-id="7b16b-144">For more information about integration with Azure, go to the [IBM QRadar Security Intelligence Platform 7.3.0](https://www.ibm.com/support/knowledgecenter/SS42VS_DSM/c_dsm_guide_microsoft_azure_overview.html?cp=SS42VS_7.3.0) site.</span></span>
    
    * <span data-ttu-id="7b16b-145">**Sumo Logic**: To set up Sumo Logic to consume data from an event hub, see [Install the Azure AD app and view the dashboards](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Install_the_Azure_Active_Directory_App_and_View_the_Dashboards).</span><span class="sxs-lookup"><span data-stu-id="7b16b-145">**Sumo Logic**: To set up Sumo Logic to consume data from an event hub, see [Install the Azure AD app and view the dashboards](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Install_the_Azure_Active_Directory_App_and_View_the_Dashboards).</span></span> 

* <span data-ttu-id="7b16b-146">**Set up custom tooling**.</span><span class="sxs-lookup"><span data-stu-id="7b16b-146">**Set up custom tooling**.</span></span> <span data-ttu-id="7b16b-147">If your current SIEM isn't supported in Azure Monitor diagnostics yet, you can set up custom tooling by using the Event Hubs API.</span><span class="sxs-lookup"><span data-stu-id="7b16b-147">If your current SIEM isn't supported in Azure Monitor diagnostics yet, you can set up custom tooling by using the Event Hubs API.</span></span> <span data-ttu-id="7b16b-148">To learn more, see the [Getting started receiving messages from an event hub](https://docs.microsoft.com/azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph).</span><span class="sxs-lookup"><span data-stu-id="7b16b-148">To learn more, see the [Getting started receiving messages from an event hub](https://docs.microsoft.com/azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph).</span></span>


## <a name="next-steps"></a><span data-ttu-id="7b16b-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b16b-149">Next steps</span></span>

* [<span data-ttu-id="7b16b-150">Integrate Azure AD logs with Splunk by using Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="7b16b-150">Integrate Azure AD logs with Splunk by using Azure Monitor</span></span>](tutorial-integrate-activity-logs-with-splunk.md)
* [<span data-ttu-id="7b16b-151">Integrate Azure AD logs with SumoLogic by using Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="7b16b-151">Integrate Azure AD logs with SumoLogic by using Azure Monitor</span></span>](howto-integrate-activity-logs-with-sumologic.md)
* [<span data-ttu-id="7b16b-152">Interpret audit logs schema in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="7b16b-152">Interpret audit logs schema in Azure Monitor</span></span>](reference-azure-monitor-audit-log-schema.md)
* [<span data-ttu-id="7b16b-153">Interpret sign-in logs schema in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="7b16b-153">Interpret sign-in logs schema in Azure Monitor</span></span>](reference-azure-monitor-sign-ins-log-schema.md)
