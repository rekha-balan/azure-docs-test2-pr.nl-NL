---
title: Tutorial - Archive Azure Active Directory logs to an Azure storage account (preview) | Microsoft Docs
description: Learn how to set up Azure Diagnostics to push Azure Active Directory logs to a storage account (preview)
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
ms.openlocfilehash: 061a4f2d1b6a1661e341166ec0a1541af073c1f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968715"
---
# <a name="tutorial-archive-azure-ad-logs-to-an-azure-storage-account-preview"></a><span data-ttu-id="61307-103">Tutorial: Archive Azure AD logs to an Azure storage account (preview)</span><span class="sxs-lookup"><span data-stu-id="61307-103">Tutorial: Archive Azure AD logs to an Azure storage account (preview)</span></span>

<span data-ttu-id="61307-104">In this tutorial, you learn how to set up Azure Monitor diagnostics settings to route Azure Active Directory (Azure AD) logs to an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="61307-104">In this tutorial, you learn how to set up Azure Monitor diagnostics settings to route Azure Active Directory (Azure AD) logs to an Azure storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61307-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="61307-105">Prerequisites</span></span> 

<span data-ttu-id="61307-106">To use this feature, you need:</span><span class="sxs-lookup"><span data-stu-id="61307-106">To use this feature, you need:</span></span>

* <span data-ttu-id="61307-107">An Azure subscription with an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="61307-107">An Azure subscription with an Azure storage account.</span></span> <span data-ttu-id="61307-108">If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="61307-108">If you don't have an Azure subscription, you can [sign up for a free trial](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="61307-109">An Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="61307-109">An Azure AD tenant.</span></span>
* <span data-ttu-id="61307-110">A user who's a *global administrator* or *security administrator* for the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="61307-110">A user who's a *global administrator* or *security administrator* for the Azure AD tenant.</span></span>

## <a name="archive-logs-to-an-azure-storage-account"></a><span data-ttu-id="61307-111">Archive logs to an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="61307-111">Archive logs to an Azure storage account</span></span>

1. <span data-ttu-id="61307-112">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61307-112">Sign in to the [Azure portal](https://portal.azure.com).</span></span> 

2. <span data-ttu-id="61307-113">Select **Azure Active Directory** > **Activity** > **Audit logs**.</span><span class="sxs-lookup"><span data-stu-id="61307-113">Select **Azure Active Directory** > **Activity** > **Audit logs**.</span></span> 

3. <span data-ttu-id="61307-114">Select **Export Settings**.</span><span class="sxs-lookup"><span data-stu-id="61307-114">Select **Export Settings**.</span></span> 

4. <span data-ttu-id="61307-115">In the **Diagnostics settings** pane, do either of the following:</span><span class="sxs-lookup"><span data-stu-id="61307-115">In the **Diagnostics settings** pane, do either of the following:</span></span>
    * <span data-ttu-id="61307-116">To change existing settings, select **Edit setting**.</span><span class="sxs-lookup"><span data-stu-id="61307-116">To change existing settings, select **Edit setting**.</span></span>
    * <span data-ttu-id="61307-117">To add new settings, select **Add diagnostics setting**.</span><span class="sxs-lookup"><span data-stu-id="61307-117">To add new settings, select **Add diagnostics setting**.</span></span>  
      <span data-ttu-id="61307-118">You can have up to three settings.</span><span class="sxs-lookup"><span data-stu-id="61307-118">You can have up to three settings.</span></span> 

    ![Export settings](./media/quickstart-azure-monitor-route-logs-to-storage-account/ExportSettings.png)

5. <span data-ttu-id="61307-120">Enter a friendly name for the setting to remind you of its purpose (for example, *Send to Azure storage account*).</span><span class="sxs-lookup"><span data-stu-id="61307-120">Enter a friendly name for the setting to remind you of its purpose (for example, *Send to Azure storage account*).</span></span> 

6. <span data-ttu-id="61307-121">Select the **Archive to a storage account** check box, and then select **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="61307-121">Select the **Archive to a storage account** check box, and then select **Storage account**.</span></span> 

7. <span data-ttu-id="61307-122">Select the Azure subscription and storage account that you want to route the logs to.</span><span class="sxs-lookup"><span data-stu-id="61307-122">Select the Azure subscription and storage account that you want to route the logs to.</span></span>
 
8. <span data-ttu-id="61307-123">Select **OK** to exit the configuration.</span><span class="sxs-lookup"><span data-stu-id="61307-123">Select **OK** to exit the configuration.</span></span>

9. <span data-ttu-id="61307-124">Do either or both of the following:</span><span class="sxs-lookup"><span data-stu-id="61307-124">Do either or both of the following:</span></span>
    * <span data-ttu-id="61307-125">To send audit logs to the storage account, select the **AuditLogs** check box.</span><span class="sxs-lookup"><span data-stu-id="61307-125">To send audit logs to the storage account, select the **AuditLogs** check box.</span></span> 
    * <span data-ttu-id="61307-126">To send sign-in logs to the storage account, select the **SignInLogs** check box.</span><span class="sxs-lookup"><span data-stu-id="61307-126">To send sign-in logs to the storage account, select the **SignInLogs** check box.</span></span>

10. <span data-ttu-id="61307-127">Use the slider to set the retention of your log data.</span><span class="sxs-lookup"><span data-stu-id="61307-127">Use the slider to set the retention of your log data.</span></span> <span data-ttu-id="61307-128">By default, this value is *0*, which means that logs are retained in the storage account indefinitely.</span><span class="sxs-lookup"><span data-stu-id="61307-128">By default, this value is *0*, which means that logs are retained in the storage account indefinitely.</span></span> <span data-ttu-id="61307-129">If you set a different value, events older than the number of days selected are automatically cleaned up.</span><span class="sxs-lookup"><span data-stu-id="61307-129">If you set a different value, events older than the number of days selected are automatically cleaned up.</span></span>

11. <span data-ttu-id="61307-130">Select **Save** to save the setting.</span><span class="sxs-lookup"><span data-stu-id="61307-130">Select **Save** to save the setting.</span></span>

    ![Diagnostics settings](./media/quickstart-azure-monitor-route-logs-to-storage-account/DiagnosticSettings.png)

12. <span data-ttu-id="61307-132">After about 15 minutes, verify that the logs are pushed to your storage account.</span><span class="sxs-lookup"><span data-stu-id="61307-132">After about 15 minutes, verify that the logs are pushed to your storage account.</span></span> <span data-ttu-id="61307-133">Go to the [Azure portal](https://portal.azure.com), select **Storage accounts**, select the storage account that you used earlier, and then select **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="61307-133">Go to the [Azure portal](https://portal.azure.com), select **Storage accounts**, select the storage account that you used earlier, and then select **Blobs**.</span></span> 

13. <span data-ttu-id="61307-134">For **Audit logs**, select **insights-log-audit**.</span><span class="sxs-lookup"><span data-stu-id="61307-134">For **Audit logs**, select **insights-log-audit**.</span></span> <span data-ttu-id="61307-135">For **Sign-in logs**, select **insights-logs-signin**.</span><span class="sxs-lookup"><span data-stu-id="61307-135">For **Sign-in logs**, select **insights-logs-signin**.</span></span>
    <span data-ttu-id="61307-136">![Storage account](./media/quickstart-azure-monitor-route-logs-to-storage-account/StorageAccount.png)</span><span class="sxs-lookup"><span data-stu-id="61307-136">![Storage account](./media/quickstart-azure-monitor-route-logs-to-storage-account/StorageAccount.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="61307-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="61307-137">Next steps</span></span>

* [<span data-ttu-id="61307-138">Interpret audit logs schema in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="61307-138">Interpret audit logs schema in Azure Monitor</span></span>](reference-azure-monitor-audit-log-schema.md)
* [<span data-ttu-id="61307-139">Interpret sign-in logs schema in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="61307-139">Interpret sign-in logs schema in Azure Monitor</span></span>](reference-azure-monitor-sign-ins-log-schema.md)
* [<span data-ttu-id="61307-140">Frequently asked questions and known issues</span><span class="sxs-lookup"><span data-stu-id="61307-140">Frequently asked questions and known issues</span></span>](overview-activity-logs-in-azure-monitor.md#frequently-asked-questions)
