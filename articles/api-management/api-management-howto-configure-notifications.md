---
title: Configure notifications and email templates in Azure API Management | Microsoft Docs
description: Learn how to configure notifications and email templates in Azure API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2018
ms.author: apimpm
ms.openlocfilehash: 60788f76dac58ead10e43e892d587a86bdd3fcad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804614"
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="c7a15-103">How to configure notifications and email templates in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="c7a15-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="c7a15-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span><span class="sxs-lookup"><span data-stu-id="c7a15-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="c7a15-105">This article shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span><span class="sxs-lookup"><span data-stu-id="c7a15-105">This article shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7a15-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c7a15-106">Prerequisites</span></span>

<span data-ttu-id="c7a15-107">If you do not have an API Management service instance, complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="c7a15-107">If you do not have an API Management service instance, complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>

## <span data-ttu-id="c7a15-108"><a name="publisher-notifications"> </a>Configure notifications</span><span class="sxs-lookup"><span data-stu-id="c7a15-108"><a name="publisher-notifications"> </a>Configure notifications</span></span>

1. <span data-ttu-id="c7a15-109">Select your **API MANAGEMENT** instance.</span><span class="sxs-lookup"><span data-stu-id="c7a15-109">Select your **API MANAGEMENT** instance.</span></span>
2. <span data-ttu-id="c7a15-110">Click **Notifications** to view the available notifications.</span><span class="sxs-lookup"><span data-stu-id="c7a15-110">Click **Notifications** to view the available notifications.</span></span>

    ![Publisher notifications][api-management-publisher-notifications]

    <span data-ttu-id="c7a15-112">The following list of events can be configured for notifications.</span><span class="sxs-lookup"><span data-stu-id="c7a15-112">The following list of events can be configured for notifications.</span></span>

    * <span data-ttu-id="c7a15-113">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span><span class="sxs-lookup"><span data-stu-id="c7a15-113">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
    * <span data-ttu-id="c7a15-114">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c7a15-114">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
    * <span data-ttu-id="c7a15-115">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span><span class="sxs-lookup"><span data-stu-id="c7a15-115">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
    * <span data-ttu-id="c7a15-116">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span><span class="sxs-lookup"><span data-stu-id="c7a15-116">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
    * <span data-ttu-id="c7a15-117">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c7a15-117">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
    * <span data-ttu-id="c7a15-118">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span><span class="sxs-lookup"><span data-stu-id="c7a15-118">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
    * <span data-ttu-id="c7a15-119">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span><span class="sxs-lookup"><span data-stu-id="c7a15-119">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

    <span data-ttu-id="c7a15-120">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span><span class="sxs-lookup"><span data-stu-id="c7a15-120">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

3. <span data-ttu-id="c7a15-121">To specify the email addresses to be notified, enter them in the email address text box.</span><span class="sxs-lookup"><span data-stu-id="c7a15-121">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="c7a15-122">If you have multiple email addresses, separate them using commas.</span><span class="sxs-lookup"><span data-stu-id="c7a15-122">If you have multiple email addresses, separate them using commas.</span></span>

    ![Notification recipients][api-management-email-addresses]
4. <span data-ttu-id="c7a15-124">Press **Add**.</span><span class="sxs-lookup"><span data-stu-id="c7a15-124">Press **Add**.</span></span>

## <span data-ttu-id="c7a15-125"><a name="email-templates"> </a>Configure notification templates</span><span class="sxs-lookup"><span data-stu-id="c7a15-125"><a name="email-templates"> </a>Configure notification templates</span></span>
<span data-ttu-id="c7a15-126">API Management provides notification templates for the email messages that are sent in the course of administering and using the service.</span><span class="sxs-lookup"><span data-stu-id="c7a15-126">API Management provides notification templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="c7a15-127">The following email templates are provided.</span><span class="sxs-lookup"><span data-stu-id="c7a15-127">The following email templates are provided.</span></span>

* <span data-ttu-id="c7a15-128">Application gallery submission approved</span><span class="sxs-lookup"><span data-stu-id="c7a15-128">Application gallery submission approved</span></span>
* <span data-ttu-id="c7a15-129">Developer farewell letter</span><span class="sxs-lookup"><span data-stu-id="c7a15-129">Developer farewell letter</span></span>
* <span data-ttu-id="c7a15-130">Developer quota limit approaching notification</span><span class="sxs-lookup"><span data-stu-id="c7a15-130">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="c7a15-131">Invite user</span><span class="sxs-lookup"><span data-stu-id="c7a15-131">Invite user</span></span>
* <span data-ttu-id="c7a15-132">New comment added to an issue</span><span class="sxs-lookup"><span data-stu-id="c7a15-132">New comment added to an issue</span></span>
* <span data-ttu-id="c7a15-133">New issue received</span><span class="sxs-lookup"><span data-stu-id="c7a15-133">New issue received</span></span>
* <span data-ttu-id="c7a15-134">New subscription activated</span><span class="sxs-lookup"><span data-stu-id="c7a15-134">New subscription activated</span></span>
* <span data-ttu-id="c7a15-135">Subscription renewed confirmation</span><span class="sxs-lookup"><span data-stu-id="c7a15-135">Subscription renewed confirmation</span></span>
* <span data-ttu-id="c7a15-136">Subscription request declines</span><span class="sxs-lookup"><span data-stu-id="c7a15-136">Subscription request declines</span></span>
* <span data-ttu-id="c7a15-137">Subscription request received</span><span class="sxs-lookup"><span data-stu-id="c7a15-137">Subscription request received</span></span>

<span data-ttu-id="c7a15-138">These templates can be modified as desired.</span><span class="sxs-lookup"><span data-stu-id="c7a15-138">These templates can be modified as desired.</span></span>

<span data-ttu-id="c7a15-139">To view and configure the email templates for your API Management instance, click **Notifications templates**.</span><span class="sxs-lookup"><span data-stu-id="c7a15-139">To view and configure the email templates for your API Management instance, click **Notifications templates**.</span></span>

![Email templates][api-management-email-templates]

<span data-ttu-id="c7a15-141">Each email template has a subject in plain text, and a body definition in HTML format.</span><span class="sxs-lookup"><span data-stu-id="c7a15-141">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="c7a15-142">Each item can be customized as desired.</span><span class="sxs-lookup"><span data-stu-id="c7a15-142">Each item can be customized as desired.</span></span>

![Email template editor][api-management-email-template]

<span data-ttu-id="c7a15-144">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span><span class="sxs-lookup"><span data-stu-id="c7a15-144">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="c7a15-145">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span><span class="sxs-lookup"><span data-stu-id="c7a15-145">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

> [!NOTE] 
> <span data-ttu-id="c7a15-146">The parameters are not replaced with actual values when previewing or sending a test.</span><span class="sxs-lookup"><span data-stu-id="c7a15-146">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="c7a15-147">To save the changes to the email template, click **Save**, or to cancel the changes click **Discard**.</span><span class="sxs-lookup"><span data-stu-id="c7a15-147">To save the changes to the email template, click **Save**, or to cancel the changes click **Discard**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: get-started-create-service-instance.md
[Create an API Management service instance]: get-started-create-service-instance.md
