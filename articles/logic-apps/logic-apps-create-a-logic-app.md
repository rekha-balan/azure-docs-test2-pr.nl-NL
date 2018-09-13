---
title: Create your first workflow between cloud apps & cloud services - Azure Logic Apps | Microsoft Docs
description: Automate business processes for system integration and enterprise application integration (EAI) scenarios by creating and running workflows in Azure Logic Apps
author: jeffhollan
manager: anneta
editor: ''
services: logic-apps
keywords: workflow, cloud apps, cloud services, business processes, system integration, enterprise application integration, EAI
documentationcenter: ''
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: jehollan; estfan; LADocs
ms.openlocfilehash: 0e3342ab30ddd4797a0726b78032a3870dca7a74
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556600"
---
# <a name="create-your-first-logic-app-workflow-to-automate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="fbe2c-104">Create your first logic app workflow to automate processes between cloud apps and cloud services</span><span class="sxs-lookup"><span data-stu-id="fbe2c-104">Create your first logic app workflow to automate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="fbe2c-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="fbe2c-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="fbe2c-106">This first example shows how to create a basic logic app workflow that checks an RSS feed for new content on a website.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-106">This first example shows how to create a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="fbe2c-107">When new items appear in the website's feed, the logic app sends email from an Outlook or Gmail account.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-107">When new items appear in the website's feed, the logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="fbe2c-108">To create and run a logic app, you need these items:</span><span class="sxs-lookup"><span data-stu-id="fbe2c-108">To create and run a logic app, you need these items:</span></span>

* <span data-ttu-id="fbe2c-109">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-109">An Azure subscription.</span></span> <span data-ttu-id="fbe2c-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fbe2c-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="fbe2c-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="fbe2c-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="fbe2c-112">Your Azure subscription is used for billing logic app usage.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="fbe2c-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="fbe2c-114">Also, this example requires these items:</span><span class="sxs-lookup"><span data-stu-id="fbe2c-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="fbe2c-115">An Outlook.com, Office 365 Outlook, or Gmail account</span><span class="sxs-lookup"><span data-stu-id="fbe2c-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="fbe2c-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="fbe2c-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="fbe2c-118">A link to a website's RSS feed.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-118">A link to a website's RSS feed.</span></span> <span data-ttu-id="fbe2c-119">This example uses the RSS feed for the [MSDN Channel 9 website](https://channel9.msdn.com/): `https://s.ch9.ms/Feeds/RSS`</span><span class="sxs-lookup"><span data-stu-id="fbe2c-119">This example uses the RSS feed for the [MSDN Channel 9 website](https://channel9.msdn.com/): `https://s.ch9.ms/Feeds/RSS`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="fbe2c-120">Add a trigger that starts your workflow</span><span class="sxs-lookup"><span data-stu-id="fbe2c-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="fbe2c-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is the first item that your logic app needs.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is the first item that your logic app needs.</span></span>

1. <span data-ttu-id="fbe2c-122">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="fbe2c-122">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="fbe2c-123">From the left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span><span class="sxs-lookup"><span data-stu-id="fbe2c-123">From the left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Azure portal, New, Enterprise Integration, Logic App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="fbe2c-125">You can also choose **New**, then in the search box, type `logic app`, and press Enter.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-125">You can also choose **New**, then in the search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="fbe2c-126">Then choose **Logic App** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="fbe2c-127">Name your logic app and select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="fbe2c-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="fbe2c-129">Finally, select the datacenter location for hosting your logic app.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-129">Finally, select the datacenter location for hosting your logic app.</span></span> <span data-ttu-id="fbe2c-130">When you're ready, choose **Pin to dashboard** and then **Create**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-130">When you're ready, choose **Pin to dashboard** and then **Create**.</span></span>

     ![Logic app details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="fbe2c-132">When you select **Pin to dashboard**, your logic app appears on the Azure dashboard after deployment, and opens automatically.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-132">When you select **Pin to dashboard**, your logic app appears on the Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="fbe2c-133">If your logic app doesn't appear on the dashboard, on the **All resources** tile, choose **See More**, and select your logic app.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-133">If your logic app doesn't appear on the dashboard, on the **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="fbe2c-134">Or on the left menu, choose **More services**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-134">Or on the left menu, choose **More services**.</span></span> <span data-ttu-id="fbe2c-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="fbe2c-136">When you open your logic app for the first time, the Logic App Designer shows templates that you can use to get started.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-136">When you open your logic app for the first time, the Logic App Designer shows templates that you can use to get started.</span></span> <span data-ttu-id="fbe2c-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="fbe2c-138">The Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-138">The Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="fbe2c-139">In the search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span><span class="sxs-lookup"><span data-stu-id="fbe2c-139">In the search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![RSS trigger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="fbe2c-141">Enter the link for the website's RSS feed that you want to track.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-141">Enter the link for the website's RSS feed that you want to track.</span></span> 

     <span data-ttu-id="fbe2c-142">You can also change **Frequency** and **Interval**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="fbe2c-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="fbe2c-144">For this example, let's check every day for new   items posted to the MSDN Channel 9 website.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-144">For this example, let's check every day for new   items posted to the MSDN Channel 9 website.</span></span>

     ![Set up trigger with RSS feed, frequency, and interval](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="fbe2c-146">Save your work for now.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-146">Save your work for now.</span></span> <span data-ttu-id="fbe2c-147">(On the designer command bar, choose **Save**.)</span><span class="sxs-lookup"><span data-stu-id="fbe2c-147">(On the designer command bar, choose **Save**.)</span></span>

   ![Save your logic app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="fbe2c-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in the specified RSS feed.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in the specified RSS feed.</span></span> 
   <span data-ttu-id="fbe2c-150">To make this example more useful, we add an action that your logic app performs after your trigger fires.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-150">To make this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-to-your-trigger"></a><span data-ttu-id="fbe2c-151">Add an action that responds to your trigger</span><span class="sxs-lookup"><span data-stu-id="fbe2c-151">Add an action that responds to your trigger</span></span>

<span data-ttu-id="fbe2c-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="fbe2c-153">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-153">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="fbe2c-154">For our example, we now add an action that sends email when new items appear in the website's RSS feed.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-154">For our example, we now add an action that sends email when new items appear in the website's RSS feed.</span></span>

1. <span data-ttu-id="fbe2c-155">In the designer, under your trigger, choose **New step** > **Add an action** as shown here:</span><span class="sxs-lookup"><span data-stu-id="fbe2c-155">In the designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Add an action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="fbe2c-157">The designer shows [available connectors](../connectors/apis-list.md) so that you can select an action to perform when your trigger fires.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-157">The designer shows [available connectors](../connectors/apis-list.md) so that you can select an action to perform when your trigger fires.</span></span>

2. <span data-ttu-id="fbe2c-158">Based on your email account, follow the steps for Outlook or Gmail.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-158">Based on your email account, follow the steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="fbe2c-159">To send email from your Outlook account, in the search box, enter `outlook`.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-159">To send email from your Outlook account, in the search box, enter `outlook`.</span></span> <span data-ttu-id="fbe2c-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="fbe2c-161">Under **Actions**, select **Send an email**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-161">Under **Actions**, select **Send an email**.</span></span>

       ![Select Outlook "Send an email" action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="fbe2c-163">To send email from your Gmail account, in the search box, enter `gmail`.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-163">To send email from your Gmail account, in the search box, enter `gmail`.</span></span> 
   <span data-ttu-id="fbe2c-164">Under **Actions**, select **Send email**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-164">Under **Actions**, select **Send email**.</span></span>

       ![Choose "Gmail - Send email"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="fbe2c-166">When you're prompted for credentials, sign in with the username and password for your email account.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-166">When you're prompted for credentials, sign in with the username and password for your email account.</span></span> 

4. <span data-ttu-id="fbe2c-167">Provide the details for this action, like the destination email address, and choose the parameters for the data to include in the email, for example:</span><span class="sxs-lookup"><span data-stu-id="fbe2c-167">Provide the details for this action, like the destination email address, and choose the parameters for the data to include in the email, for example:</span></span>

   ![Select data to include in email](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="fbe2c-169">So if you chose Outlook,  your logic app might look like this example:</span><span class="sxs-lookup"><span data-stu-id="fbe2c-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Completed logic app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="fbe2c-171">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-171">Save your changes.</span></span> <span data-ttu-id="fbe2c-172">(On the designer command bar, choose **Save**.)</span><span class="sxs-lookup"><span data-stu-id="fbe2c-172">(On the designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="fbe2c-173">You can now manually run your logic app for testing.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="fbe2c-174">On the designer command bar, choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-174">On the designer command bar, choose **Run**.</span></span> <span data-ttu-id="fbe2c-175">Otherwise, you can let your logic app check the specified RSS feed based on the schedule that you set up.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-175">Otherwise, you can let your logic app check the specified RSS feed based on the schedule that you set up.</span></span>

   <span data-ttu-id="fbe2c-176">If your logic app finds new items, the logic app sends email that includes your selected data.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-176">If your logic app finds new items, the logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="fbe2c-177">If no new items are found, your logic app skips the action that sends email.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-177">If no new items are found, your logic app skips the action that sends email.</span></span>

7. <span data-ttu-id="fbe2c-178">To monitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-178">To monitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Monitor and view logic app run and trigger history](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="fbe2c-180">If you don't find the data that you expect, on the command bar, try choosing **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-180">If you don't find the data that you expect, on the command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="fbe2c-181">To learn more about your logic app's status or run and trigger history, or to diagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="fbe2c-181">To learn more about your logic app's status or run and trigger history, or to diagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="fbe2c-182">Your logic app continues running until you turn off your app.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="fbe2c-183">To turn off your app for now, on your logic app menu, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-183">To turn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="fbe2c-184">On the command bar, choose **Disable**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-184">On the command bar, choose **Disable**.</span></span>

<span data-ttu-id="fbe2c-185">Congratulations, you just set up and run your first basic logic app.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="fbe2c-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="fbe2c-187">Manage your logic app</span><span class="sxs-lookup"><span data-stu-id="fbe2c-187">Manage your logic app</span></span>

<span data-ttu-id="fbe2c-188">To manage your app, you can perform tasks like check the status, edit, view history, turn off, or delete your logic app.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-188">To manage your app, you can perform tasks like check the status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="fbe2c-189">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="fbe2c-189">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="fbe2c-190">On the left menu, choose **More services**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-190">On the left menu, choose **More services**.</span></span> <span data-ttu-id="fbe2c-191">Under **Enterprise Integration**, choose **Logic Apps**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="fbe2c-192">Select your logic app.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-192">Select your logic app.</span></span> 

   <span data-ttu-id="fbe2c-193">In the logic app menu, you can find these logic app management tasks:</span><span class="sxs-lookup"><span data-stu-id="fbe2c-193">In the logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="fbe2c-194">Task</span><span class="sxs-lookup"><span data-stu-id="fbe2c-194">Task</span></span>|<span data-ttu-id="fbe2c-195">Steps</span><span class="sxs-lookup"><span data-stu-id="fbe2c-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="fbe2c-196">View your app's status, execution history, and general information</span><span class="sxs-lookup"><span data-stu-id="fbe2c-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="fbe2c-197">Choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="fbe2c-198">Edit your app</span><span class="sxs-lookup"><span data-stu-id="fbe2c-198">Edit your app</span></span> | <span data-ttu-id="fbe2c-199">Choose **Logic App Designer**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="fbe2c-200">View your app's workflow JSON definition</span><span class="sxs-lookup"><span data-stu-id="fbe2c-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="fbe2c-201">Choose **Logic App Code View**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="fbe2c-202">View operations performed on your logic app</span><span class="sxs-lookup"><span data-stu-id="fbe2c-202">View operations performed on your logic app</span></span> | <span data-ttu-id="fbe2c-203">Choose **Activity log**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="fbe2c-204">View past versions for your logic app</span><span class="sxs-lookup"><span data-stu-id="fbe2c-204">View past versions for your logic app</span></span> | <span data-ttu-id="fbe2c-205">Choose **Versions**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="fbe2c-206">Turn off your app temporarily</span><span class="sxs-lookup"><span data-stu-id="fbe2c-206">Turn off your app temporarily</span></span> | <span data-ttu-id="fbe2c-207">Choose **Overview**, then on the command bar, choose **Disable**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-207">Choose **Overview**, then on the command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="fbe2c-208">Delete your app</span><span class="sxs-lookup"><span data-stu-id="fbe2c-208">Delete your app</span></span> | <span data-ttu-id="fbe2c-209">Choose **Overview**, then on the command bar, choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-209">Choose **Overview**, then on the command bar, choose **Delete**.</span></span> <span data-ttu-id="fbe2c-210">Enter your logic app's name, and choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="fbe2c-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="fbe2c-211">Get help</span><span class="sxs-lookup"><span data-stu-id="fbe2c-211">Get help</span></span>

<span data-ttu-id="fbe2c-212">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="fbe2c-212">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="fbe2c-213">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="fbe2c-213">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbe2c-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbe2c-214">Next steps</span></span>

*  [<span data-ttu-id="fbe2c-215">Add conditions and run workflows</span><span class="sxs-lookup"><span data-stu-id="fbe2c-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="fbe2c-216">Logic app templates</span><span class="sxs-lookup"><span data-stu-id="fbe2c-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="fbe2c-217">Create logic apps from Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="fbe2c-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)











