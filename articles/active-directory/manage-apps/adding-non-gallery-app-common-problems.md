---
title: Problem adding a non-gallery application | Microsoft Docs
description: Understand the common problems people face when adding custom non-gallery applications
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: barbkess
ms.openlocfilehash: 63eab7821e57aa807522f32f3b7596af9625f5fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965529"
---
# <a name="problem-adding-a-non-gallery-application"></a>Problem adding a non-gallery application

This article helps you understand the common problems people face when adding **custom non-gallery applications** and what you can do to resolve them. 

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a>I clicked the “add” button and my application took a long time to appear

Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory. While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.

If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state. If you want more details about the error to learn more to or share with a support engineer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a>I clicked the “add” button and my application didn’t appear

Sometimes, due to transient issues, networking problems, or a bug, adding an application fail. You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure portal and you see a red (!) icon next to your **Create application** notification. This indicates there was an error when creating the application.

If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state. If you want more details about the error to learn more to or share with a support engineer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.

## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a>I don’t know how to set up my application once I’ve added it

If you need help learning about custom applications, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.

## <a name="how-to-see-the-details-of-a-portal-notification"></a>How to see the details of a portal notification

You can see the details of any portal notification by following the steps below:

1.  click the **Notifications** icon (the bell) in the upper right of the Azure portal

2.  Select any notification in an **Error** state (those with a red (!) next to them).

   >[!NOTE]
   >You cannot click notifications in a **Successful** or **In Progress** state.
   >
   >

4.  Use the information under **Notification Details** to understand more details about the problem.

5.  If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.

6.  Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a>How to get help by sending notification details to a support engineer

It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly. You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.

## <a name="notification-details-explained"></a>Notification Details Explained

See the following descriptions for more details about the notifications.

### <a name="essential-notification-items"></a>Essential Notification Items

-   **Title** – the descriptive title of the notification
   *  Example – **Application proxy settings**

-   **Description** – the description of what occurred as a result of the operation

   *  Example – **Internal url entered is already being used by another application**

-   **Notification ID** – the unique ID of the notification

   *  Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Client Request ID** – the specific request ID made by your browser

   *  Example – **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Time Stamp UTC** – the timestamp during which the notification occurred, in UTC

   *  Example – **2017-03-23T19:50:43.7583681Z**

-   **Internal Transaction ID** – the internal ID we can use to look the error up in our systems

   *  Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – the user who performed the operation

   *  Example – **tperkins@f128.info**

-   **Tenant ID** – the unique ID of the tenant that the user who performed the operation was a member of

   *  Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **User object ID** – the unique ID of the user who performed the operation

 *  Example – **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Detailed Notification Items

-   **Display Name** – **(can be empty)** a more detailed display name for the error

  *  Example – **Application proxy settings**

-   **Status** – the specific status of the notification

   *  Example – **Failed**

-   **Object ID** – **(can be empty)** the object ID against which the operation was performed

   *  Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Details** – the detailed description of what occurred as a result of the operation

   *  Example – **Internal url 'http://bing.com/' is invalid since it is already in use**

-   **Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group 
-   engineer

   *  Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Next steps
[Managing Applications with Azure Active Directory](what-is-application-management.md)



