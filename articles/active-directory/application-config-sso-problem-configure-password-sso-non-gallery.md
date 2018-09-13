---
title: Problem configuring password single sign-on for a non-gallery application | Microsoft Docs
description: Understand the common problems people face when configuring Password Single Sign-on for custom non-gallery applications that are not listed in the Azure AD Application Gallery
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: e2ee7460aa1204c6470f1ec481ecb01a00858cce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564316"
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a>Problem configuring password single sign-on for a non-gallery application

This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.

## <a name="how-to-capture-sign-in-fields-for-an-application"></a>How to capture sign-in fields for an application

Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.

There are two ways you can capture sign-in fields for your custom applications:

-   Automatic sign-in field capture

-   Manual sign-in field capture

**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field. The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.

**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in. Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected. Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.

In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a>How to automatically capture sign-in fields for an application

To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.

5.  click **All Applications** to view a list of all your applications.

  * If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**

6.  Select the application you want to configure single sign-on.

7.  Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.

8.  Select the mode **Password-based Sign-on.**

9.  Enter the **Sign-on URL**. This is the URL where users enter their username and password to sign in to. **Ensure the sign in fields are visible at the URL you provide**.

10. Click the **Save** button.

11. Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a>How to manually capture sign-in fields for an application

To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.** To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.

To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.

5.  click **All Applications** to view a list of all your applications.

   * If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**

6.  Select the application you want to configure single sign-on.

7.  Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.

8.  Select the mode **Password-based Sign-on.**

9.  Enter the **Sign-on URL**. This is the URL where users enter their username and password to sign in to. **Ensure the sign in fields are visible at the URL you provide**.

10. Click the **Save** button.

11. Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension. In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.

12. click **Configure &lt;appname&gt; Password Single Sign-on Settings**.

13. Select the **Manually detect sign-in fields** configuration option.

14. Click **Ok**.

15. Click **Save**.

16. Follow the on screen instructions to use the Access Panel.

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a>I see a “We couldn’t find any sign-in fields at that URL” error

You see this error when automatic detection of sign-in fields fails. To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a>I see an “Unable to save Single Sign-on configuration” error

In certain rare cases, updating the single sign-on configuration can fail. TO resolve this try saving the single sign-on configuration again.

If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a>I cannot manually detect sign in fields for my application

Some of the behaviors you might see when manual detection is not working include:

-   The manual capture process appeared to work, but the fields captured were not correct

-   The right fields don’t get highlighted when performing the capture process

-   The capture process takes me to the application’s login page as expected, but nothing happens

-   Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.

check the following if you encounter any of these issues:

-   Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.

-   Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**. The access panel extension is not supported in these modes.

-   Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**. The access panel extension is not supported in these modes.

-   Try the manual capture process again, ensuring the red markers are over the correct fields.

-   If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again. But, this time after completing the process, press the **F12** button to open your browser’s developer console. Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**. This force a page redirect which end the capture process and store the fields that have been captured.

If none of these approaches work for you, we can help. Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).

## <a name="how-to-install-the-access-panel-browser-extension"></a>How to install the Access Panel Browser extension

To install the Access Panel Browser extension, follow the steps below:

1.  Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.

2.  click a **password-SSO application** in the Access Panel.

3.  In the prompt asking to install the software, select **Install Now**.

4.  Based on your browser you be directed to the download link. **Add** the extension to your browser.

5.  If your browser asks, select to either **Enable** or **Allow** the extension.

6.  Once installed, **restart** your browser session.

7.  Sign in into the Access Panel and see if you can **launch** your password-SSO applications.

You may also download the extension for Chrome and Firefox from the direct links below:

-   [Chrome Access Panel Extension](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Firefox Access Panel Extension](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a>How to see the details of a portal notification

You can see the details of any portal notification by following the steps below:

1.  click the **Notifications** icon (the bell) in the upper right of the Azure Portal

2.  Select any notification in an **Error** state (those with a red (!) next to them).

  >!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.
  >
  >

3.  This open the **Notification Details** blade.

4.  Use this information yourself to understand more details about the problem.

5.  If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.

6.  Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a>How to get help by sending notification details to a support engineer

It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly. You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.

## <a name="notification-details-explained"></a>Notification Details Explained

The below explains more what each of the notification items means, and gives examples of each of them.

### <a name="essential-notification-items"></a>Essential Notification Items

-   **Title** – the descriptive title of the notification

    -   Example – **Application proxy settings**

-   **Description** – the description of what occurred as a result of the operation

    -   Example – **Internal url entered is already being used by another application**

-   **Notification Id** – the unique id of the notification

    -   Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Client Request Id** – the specific request id made by your browser

    -   Example – **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Time Stamp UTC** – the timestamp during which the notification occurred, in UTC

    -   Example – **2017-03-23T19:50:43.7583681Z**

-   **Internal Transaction Id** – the internal ID we can use to look the error up in our systems

    -   Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – the user who performed the operation

    -   Example – **tperkins@f128.info**

-   **Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of

    -   Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **User object Id** – the unique ID of the user who performed the operation

    -   Example – **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Detailed Notification Items

-   **Display Name** – **(can be empty)** a more detailed display name for the error

    -   Example *– **Application proxy settings**

-   **Status** – the specific status of the notification

    -   Example *– **Failed**

-   **Object Id** – **(can be empty)** the object ID against which the operation was performed

    -   Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Details** – the detailed description of what occurred as a result of the operation

    -   Example – **Internal url 'http://bing.com/' is invalid since it is already in use**

-   **Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer

    -   Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Next steps
[Provide single sign-on to your apps with Application Proxy](active-directory-application-proxy-sso-using-kcd.md)

