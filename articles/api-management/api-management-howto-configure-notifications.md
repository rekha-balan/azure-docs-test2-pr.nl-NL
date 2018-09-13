---
title: Configure notifications and email templates in Azure API Management | Microsoft Docs
description: Learn how to configure notifications and email templates in Azure API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5b8664f85fa17d2e264458f598259620b12e0e84
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660534"
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="361e7-103">How to configure notifications and email templates in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="361e7-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="361e7-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span><span class="sxs-lookup"><span data-stu-id="361e7-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="361e7-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span><span class="sxs-lookup"><span data-stu-id="361e7-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="361e7-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span><span class="sxs-lookup"><span data-stu-id="361e7-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="361e7-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="361e7-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="361e7-108">This takes you to the API Management publisher portal.</span><span class="sxs-lookup"><span data-stu-id="361e7-108">This takes you to the API Management publisher portal.</span></span>

![Publisher portal][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="361e7-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="361e7-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="361e7-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span><span class="sxs-lookup"><span data-stu-id="361e7-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![Publisher notifications][api-management-publisher-notifications]

<span data-ttu-id="361e7-113">The following list of events can be configured for notifications.</span><span class="sxs-lookup"><span data-stu-id="361e7-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="361e7-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span><span class="sxs-lookup"><span data-stu-id="361e7-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="361e7-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span><span class="sxs-lookup"><span data-stu-id="361e7-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="361e7-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span><span class="sxs-lookup"><span data-stu-id="361e7-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="361e7-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span><span class="sxs-lookup"><span data-stu-id="361e7-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="361e7-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span><span class="sxs-lookup"><span data-stu-id="361e7-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="361e7-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span><span class="sxs-lookup"><span data-stu-id="361e7-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="361e7-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span><span class="sxs-lookup"><span data-stu-id="361e7-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="361e7-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span><span class="sxs-lookup"><span data-stu-id="361e7-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="361e7-122">To specify the email addresses to be notified, enter them in the email address text box.</span><span class="sxs-lookup"><span data-stu-id="361e7-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="361e7-123">If you have multiple email addresses, separate them using commas.</span><span class="sxs-lookup"><span data-stu-id="361e7-123">If you have multiple email addresses, separate them using commas.</span></span>

![Notification recipients][api-management-email-addresses]

<span data-ttu-id="361e7-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="361e7-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="361e7-126">Only administrators are displayed in the list.</span><span class="sxs-lookup"><span data-stu-id="361e7-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="361e7-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span><span class="sxs-lookup"><span data-stu-id="361e7-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="361e7-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span><span class="sxs-lookup"><span data-stu-id="361e7-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="361e7-129"><a name="email-templates"> </a>Configure email templates</span><span class="sxs-lookup"><span data-stu-id="361e7-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="361e7-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span><span class="sxs-lookup"><span data-stu-id="361e7-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="361e7-131">The following email templates are provided.</span><span class="sxs-lookup"><span data-stu-id="361e7-131">The following email templates are provided.</span></span>

* <span data-ttu-id="361e7-132">Application gallery submission approved</span><span class="sxs-lookup"><span data-stu-id="361e7-132">Application gallery submission approved</span></span>
* <span data-ttu-id="361e7-133">Developer farewell letter</span><span class="sxs-lookup"><span data-stu-id="361e7-133">Developer farewell letter</span></span>
* <span data-ttu-id="361e7-134">Developer quota limit approaching notification</span><span class="sxs-lookup"><span data-stu-id="361e7-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="361e7-135">Invite user</span><span class="sxs-lookup"><span data-stu-id="361e7-135">Invite user</span></span>
* <span data-ttu-id="361e7-136">New comment added to an issue</span><span class="sxs-lookup"><span data-stu-id="361e7-136">New comment added to an issue</span></span>
* <span data-ttu-id="361e7-137">New issue received</span><span class="sxs-lookup"><span data-stu-id="361e7-137">New issue received</span></span>
* <span data-ttu-id="361e7-138">New subscription activated</span><span class="sxs-lookup"><span data-stu-id="361e7-138">New subscription activated</span></span>
* <span data-ttu-id="361e7-139">Subscription renewed confirmation</span><span class="sxs-lookup"><span data-stu-id="361e7-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="361e7-140">Subscription request declines</span><span class="sxs-lookup"><span data-stu-id="361e7-140">Subscription request declines</span></span>
* <span data-ttu-id="361e7-141">Subscription request received</span><span class="sxs-lookup"><span data-stu-id="361e7-141">Subscription request received</span></span>

<span data-ttu-id="361e7-142">These templates can be modified as desired.</span><span class="sxs-lookup"><span data-stu-id="361e7-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="361e7-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span><span class="sxs-lookup"><span data-stu-id="361e7-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![Email templates][api-management-email-templates]

<span data-ttu-id="361e7-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="361e7-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![Email templates list][api-management-email-templates-list]

<span data-ttu-id="361e7-147">Each email template has a subject in plain text, and a body definition in HTML format.</span><span class="sxs-lookup"><span data-stu-id="361e7-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="361e7-148">Each item can be customized as desired.</span><span class="sxs-lookup"><span data-stu-id="361e7-148">Each item can be customized as desired.</span></span>

![Email template editor][api-management-email-template]

<span data-ttu-id="361e7-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span><span class="sxs-lookup"><span data-stu-id="361e7-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="361e7-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span><span class="sxs-lookup"><span data-stu-id="361e7-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="361e7-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span><span class="sxs-lookup"><span data-stu-id="361e7-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="361e7-153">The parameters are not replaced with actual values when previewing or sending a test.</span><span class="sxs-lookup"><span data-stu-id="361e7-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="361e7-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span><span class="sxs-lookup"><span data-stu-id="361e7-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance






