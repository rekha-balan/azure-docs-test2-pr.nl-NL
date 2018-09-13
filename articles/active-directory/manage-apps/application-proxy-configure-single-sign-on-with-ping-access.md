---
title: Header-based authentication with PingAccess for Azure AD Application Proxy | Microsoft Docs
description: Publish applications with PingAccess and App Proxy to support header-based authentication.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 10/11/2017
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: aae73816b883fe782eff27c56174c71f14c253c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857538"
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="b2a96-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span><span class="sxs-lookup"><span data-stu-id="b2a96-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="b2a96-104">Azure Active Directory Application Proxy and PingAccess have partnered together to provide Azure Active Directory customers with access to even more applications.</span><span class="sxs-lookup"><span data-stu-id="b2a96-104">Azure Active Directory Application Proxy and PingAccess have partnered together to provide Azure Active Directory customers with access to even more applications.</span></span> <span data-ttu-id="b2a96-105">PingAccess expands the [existing Application Proxy offerings](application-proxy.md) to include single sign-on access to applications that use headers for authentication.</span><span class="sxs-lookup"><span data-stu-id="b2a96-105">PingAccess expands the [existing Application Proxy offerings](application-proxy.md) to include single sign-on access to applications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="b2a96-106">What is PingAccess for Azure AD?</span><span class="sxs-lookup"><span data-stu-id="b2a96-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="b2a96-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you to give users access and single sign-on to applications that use headers for authentication.</span><span class="sxs-lookup"><span data-stu-id="b2a96-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you to give users access and single sign-on to applications that use headers for authentication.</span></span> <span data-ttu-id="b2a96-108">Application Proxy treats these apps like any other, using Azure AD to authenticate access and then passing traffic through the connector service.</span><span class="sxs-lookup"><span data-stu-id="b2a96-108">Application Proxy treats these apps like any other, using Azure AD to authenticate access and then passing traffic through the connector service.</span></span> <span data-ttu-id="b2a96-109">PingAccess sits in front of the apps and translates the access token from Azure AD into a header so that the application receives the authentication in the format it can read.</span><span class="sxs-lookup"><span data-stu-id="b2a96-109">PingAccess sits in front of the apps and translates the access token from Azure AD into a header so that the application receives the authentication in the format it can read.</span></span>

<span data-ttu-id="b2a96-110">Your users won’t notice anything different when they sign in to use your corporate apps.</span><span class="sxs-lookup"><span data-stu-id="b2a96-110">Your users won’t notice anything different when they sign in to use your corporate apps.</span></span> <span data-ttu-id="b2a96-111">They can still work from anywhere on any device.</span><span class="sxs-lookup"><span data-stu-id="b2a96-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="b2a96-112">Since the Application Proxy connectors direct remote traffic to all apps regardless of their authentication type, they’ll continue to load balance automatically, as well.</span><span class="sxs-lookup"><span data-stu-id="b2a96-112">Since the Application Proxy connectors direct remote traffic to all apps regardless of their authentication type, they’ll continue to load balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="b2a96-113">How do I get access?</span><span class="sxs-lookup"><span data-stu-id="b2a96-113">How do I get access?</span></span>

<span data-ttu-id="b2a96-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span><span class="sxs-lookup"><span data-stu-id="b2a96-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="b2a96-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up to 20 applications.</span><span class="sxs-lookup"><span data-stu-id="b2a96-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up to 20 applications.</span></span> <span data-ttu-id="b2a96-116">If you need to publish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span><span class="sxs-lookup"><span data-stu-id="b2a96-116">If you need to publish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="b2a96-117">For more information, see [Azure Active Directory editions](../fundamentals/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b2a96-117">For more information, see [Azure Active Directory editions](../fundamentals/active-directory-whatis.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="b2a96-118">Publish your application in Azure</span><span class="sxs-lookup"><span data-stu-id="b2a96-118">Publish your application in Azure</span></span>

<span data-ttu-id="b2a96-119">This article is intended for people who are publishing an app with this scenario for the first time.</span><span class="sxs-lookup"><span data-stu-id="b2a96-119">This article is intended for people who are publishing an app with this scenario for the first time.</span></span> <span data-ttu-id="b2a96-120">It walks through how to get started with both Application and PingAccess, in addition to the publishing steps.</span><span class="sxs-lookup"><span data-stu-id="b2a96-120">It walks through how to get started with both Application and PingAccess, in addition to the publishing steps.</span></span> <span data-ttu-id="b2a96-121">If you’ve already configured both services but want a refresher on the publishing steps, you can skip the connector installation and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="b2a96-121">If you’ve already configured both services but want a refresher on the publishing steps, you can skip the connector installation and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="b2a96-122">Since this scenario is a partnership between Azure AD and PingAccess, some of the instructions exist on the Ping Identity site.</span><span class="sxs-lookup"><span data-stu-id="b2a96-122">Since this scenario is a partnership between Azure AD and PingAccess, some of the instructions exist on the Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="b2a96-123">Install an Application Proxy connector</span><span class="sxs-lookup"><span data-stu-id="b2a96-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="b2a96-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="b2a96-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="b2a96-125">The Application Proxy connector is a Windows Server service that directs the traffic from your remote employees to your published apps.</span><span class="sxs-lookup"><span data-stu-id="b2a96-125">The Application Proxy connector is a Windows Server service that directs the traffic from your remote employees to your published apps.</span></span> <span data-ttu-id="b2a96-126">For more detailed installation instructions, see [Enable Application Proxy in the Azure portal](application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="b2a96-126">For more detailed installation instructions, see [Enable Application Proxy in the Azure portal](application-proxy-enable.md).</span></span>

1. <span data-ttu-id="b2a96-127">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span><span class="sxs-lookup"><span data-stu-id="b2a96-127">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="b2a96-128">Select **Azure Active Directory** > **Application proxy**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="b2a96-129">Select **Download Connector** to start the Application Proxy connector download.</span><span class="sxs-lookup"><span data-stu-id="b2a96-129">Select **Download Connector** to start the Application Proxy connector download.</span></span> <span data-ttu-id="b2a96-130">Follow the installation instructions.</span><span class="sxs-lookup"><span data-stu-id="b2a96-130">Follow the installation instructions.</span></span>

   ![Enable Application Proxy and download the connector](./media/application-proxy-configure-single-sign-on-with-ping-access/install-connector.png)

4. <span data-ttu-id="b2a96-132">Downloading the connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-132">Downloading the connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-to-azure-ad-with-application-proxy"></a><span data-ttu-id="b2a96-133">Add your app to Azure AD with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="b2a96-133">Add your app to Azure AD with Application Proxy</span></span>

<span data-ttu-id="b2a96-134">There are two actions you need to take in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b2a96-134">There are two actions you need to take in the Azure portal.</span></span> <span data-ttu-id="b2a96-135">First, you need to publish your application with Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="b2a96-135">First, you need to publish your application with Application Proxy.</span></span> <span data-ttu-id="b2a96-136">Then, you need to collect some information about the app that you can use during the PingAccess steps.</span><span class="sxs-lookup"><span data-stu-id="b2a96-136">Then, you need to collect some information about the app that you can use during the PingAccess steps.</span></span>

<span data-ttu-id="b2a96-137">Follow these steps to publish your app.</span><span class="sxs-lookup"><span data-stu-id="b2a96-137">Follow these steps to publish your app.</span></span> <span data-ttu-id="b2a96-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b2a96-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="b2a96-139">If you didn't in the last section, sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span><span class="sxs-lookup"><span data-stu-id="b2a96-139">If you didn't in the last section, sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="b2a96-140">Select **Azure Active Directory** > **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="b2a96-141">Select **Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="b2a96-141">Select **Add** at the top of the blade.</span></span>
4. <span data-ttu-id="b2a96-142">Select **On-premises application**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="b2a96-143">Fill out the required fields with information about your new app.</span><span class="sxs-lookup"><span data-stu-id="b2a96-143">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="b2a96-144">Use the following guidance for the settings:</span><span class="sxs-lookup"><span data-stu-id="b2a96-144">Use the following guidance for the settings:</span></span>
   - <span data-ttu-id="b2a96-145">**Internal URL**: Normally you provide the URL that takes you to the app’s sign in page when you’re on the corporate network.</span><span class="sxs-lookup"><span data-stu-id="b2a96-145">**Internal URL**: Normally you provide the URL that takes you to the app’s sign in page when you’re on the corporate network.</span></span> <span data-ttu-id="b2a96-146">For this scenario the connector needs to treat the PingAccess proxy as the front page of the app.</span><span class="sxs-lookup"><span data-stu-id="b2a96-146">For this scenario the connector needs to treat the PingAccess proxy as the front page of the app.</span></span> <span data-ttu-id="b2a96-147">Use this format: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="b2a96-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="b2a96-148">The port is 3000 by default, but you can configure it in PingAccess.</span><span class="sxs-lookup"><span data-stu-id="b2a96-148">The port is 3000 by default, but you can configure it in PingAccess.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b2a96-149">For this type of SSO, the internal URL must use https and cannot use http.</span><span class="sxs-lookup"><span data-stu-id="b2a96-149">For this type of SSO, the internal URL must use https and cannot use http.</span></span>

   - <span data-ttu-id="b2a96-150">**Pre-authentication method**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2a96-150">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="b2a96-151">**Translate URL in Headers**: No</span><span class="sxs-lookup"><span data-stu-id="b2a96-151">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="b2a96-152">If this is your first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration.</span><span class="sxs-lookup"><span data-stu-id="b2a96-152">If this is your first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="b2a96-153">If this is your second or later app, this will need to match the Listener you’ve configured in PingAccess.</span><span class="sxs-lookup"><span data-stu-id="b2a96-153">If this is your second or later app, this will need to match the Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="b2a96-154">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="b2a96-154">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="b2a96-155">Select **Add** at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="b2a96-155">Select **Add** at the bottom of the blade.</span></span> <span data-ttu-id="b2a96-156">Your application is added, and the quick start menu opens.</span><span class="sxs-lookup"><span data-stu-id="b2a96-156">Your application is added, and the quick start menu opens.</span></span>
7. <span data-ttu-id="b2a96-157">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span><span class="sxs-lookup"><span data-stu-id="b2a96-157">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="b2a96-158">Make sure this test account has access to the on-premises application.</span><span class="sxs-lookup"><span data-stu-id="b2a96-158">Make sure this test account has access to the on-premises application.</span></span>
8. <span data-ttu-id="b2a96-159">Select **Assign** to save the test user assignment.</span><span class="sxs-lookup"><span data-stu-id="b2a96-159">Select **Assign** to save the test user assignment.</span></span>
9. <span data-ttu-id="b2a96-160">On the app management blade, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-160">On the app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="b2a96-161">Choose **Header-based sign-on** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="b2a96-161">Choose **Header-based sign-on** from the drop-down menu.</span></span> <span data-ttu-id="b2a96-162">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-162">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="b2a96-163">If this is your first time using header-based single sign-on, you need to install PingAccess.</span><span class="sxs-lookup"><span data-stu-id="b2a96-163">If this is your first time using header-based single sign-on, you need to install PingAccess.</span></span> <span data-ttu-id="b2a96-164">To make sure your Azure subscription is automatically associated with your PingAccess installation, use the link on this single sign-on page to download PingAccess.</span><span class="sxs-lookup"><span data-stu-id="b2a96-164">To make sure your Azure subscription is automatically associated with your PingAccess installation, use the link on this single sign-on page to download PingAccess.</span></span> <span data-ttu-id="b2a96-165">You can open the download site now, or come back to this page later.</span><span class="sxs-lookup"><span data-stu-id="b2a96-165">You can open the download site now, or come back to this page later.</span></span> 

   ![Select header-based sign-on](./media/application-proxy-configure-single-sign-on-with-ping-access/sso-header.PNG)

11. <span data-ttu-id="b2a96-167">Close the Enterprise applications blade or scroll all the way to the left to return to the Azure Active Directory menu.</span><span class="sxs-lookup"><span data-stu-id="b2a96-167">Close the Enterprise applications blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
12. <span data-ttu-id="b2a96-168">Select **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-168">Select **App registrations**.</span></span>

   ![Select App registrations](./media/application-proxy-configure-single-sign-on-with-ping-access/app-registrations.png)

13. <span data-ttu-id="b2a96-170">Select the app you just added, then **Reply URLs**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-170">Select the app you just added, then **Reply URLs**.</span></span>

   ![Select Reply URLs](./media/application-proxy-configure-single-sign-on-with-ping-access/reply-urls.png)

14. <span data-ttu-id="b2a96-172">Check to see if the external URL that you assigned to your app in step 5 is in the Reply URLs list.</span><span class="sxs-lookup"><span data-stu-id="b2a96-172">Check to see if the external URL that you assigned to your app in step 5 is in the Reply URLs list.</span></span> <span data-ttu-id="b2a96-173">If it’s not, add it now.</span><span class="sxs-lookup"><span data-stu-id="b2a96-173">If it’s not, add it now.</span></span>
15. <span data-ttu-id="b2a96-174">On the app settings blade, select **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-174">On the app settings blade, select **Required permissions**.</span></span>

  ![Select Required permissions](./media/application-proxy-configure-single-sign-on-with-ping-access/required-permissions.png)

16. <span data-ttu-id="b2a96-176">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-176">Select **Add**.</span></span> <span data-ttu-id="b2a96-177">For the API, choose **Windows Azure Active Directory**, then **Select**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-177">For the API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="b2a96-178">For the permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-178">For the permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![Select permissions](./media/application-proxy-configure-single-sign-on-with-ping-access/select-permissions.png)

17. <span data-ttu-id="b2a96-180">Grant permissions before you close the permissions screen.</span><span class="sxs-lookup"><span data-stu-id="b2a96-180">Grant permissions before you close the permissions screen.</span></span> 
<span data-ttu-id="b2a96-181">![Grant Permissions](./media/application-proxy-configure-single-sign-on-with-ping-access/grantperms.png)</span><span class="sxs-lookup"><span data-stu-id="b2a96-181">![Grant Permissions](./media/application-proxy-configure-single-sign-on-with-ping-access/grantperms.png)</span></span>

### <a name="collect-information-for-the-pingaccess-steps"></a><span data-ttu-id="b2a96-182">Collect information for the PingAccess steps</span><span class="sxs-lookup"><span data-stu-id="b2a96-182">Collect information for the PingAccess steps</span></span>

1. <span data-ttu-id="b2a96-183">On your app settings blade, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-183">On your app settings blade, select **Properties**.</span></span> 

  ![Select Properties](./media/application-proxy-configure-single-sign-on-with-ping-access/properties.png)

2. <span data-ttu-id="b2a96-185">Save the **Application Id** value.</span><span class="sxs-lookup"><span data-stu-id="b2a96-185">Save the **Application Id** value.</span></span> <span data-ttu-id="b2a96-186">This is used for the client ID when you configure PingAccess.</span><span class="sxs-lookup"><span data-stu-id="b2a96-186">This is used for the client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="b2a96-187">On the app settings blade, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-187">On the app settings blade, select **Keys**.</span></span>

  ![Select Keys](./media/application-proxy-configure-single-sign-on-with-ping-access/Keys.png)

4. <span data-ttu-id="b2a96-189">Create a key by entering a key description and choosing an expiration date from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="b2a96-189">Create a key by entering a key description and choosing an expiration date from the drop-down menu.</span></span>
5. <span data-ttu-id="b2a96-190">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-190">Select **Save**.</span></span> <span data-ttu-id="b2a96-191">A GUID appears in the **Value** field.</span><span class="sxs-lookup"><span data-stu-id="b2a96-191">A GUID appears in the **Value** field.</span></span>

  <span data-ttu-id="b2a96-192">Save this value now, as you won’t be able to see it again after you close this window.</span><span class="sxs-lookup"><span data-stu-id="b2a96-192">Save this value now, as you won’t be able to see it again after you close this window.</span></span>

  ![Create a new key](./media/application-proxy-configure-single-sign-on-with-ping-access/create-keys.png)

6. <span data-ttu-id="b2a96-194">Close the App registrations blade or scroll all the way to the left to return to the Azure Active Directory menu.</span><span class="sxs-lookup"><span data-stu-id="b2a96-194">Close the App registrations blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
7. <span data-ttu-id="b2a96-195">Select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-195">Select **Properties**.</span></span>
8. <span data-ttu-id="b2a96-196">Save the **Directory ID** GUID.</span><span class="sxs-lookup"><span data-stu-id="b2a96-196">Save the **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-to-send-custom-fields"></a><span data-ttu-id="b2a96-197">Optional - Update GraphAPI to send custom fields</span><span class="sxs-lookup"><span data-stu-id="b2a96-197">Optional - Update GraphAPI to send custom fields</span></span>

<span data-ttu-id="b2a96-198">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](../develop/v1-id-and-access-tokens.md).</span><span class="sxs-lookup"><span data-stu-id="b2a96-198">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](../develop/v1-id-and-access-tokens.md).</span></span> <span data-ttu-id="b2a96-199">If you need a custom claim that sends other tokens, use Graph Explorer or the manifest for the application in the Azure Portal to set the app field *acceptMappedClaims* to **True**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-199">If you need a custom claim that sends other tokens, use Graph Explorer or the manifest for the application in the Azure Portal to set the app field *acceptMappedClaims* to **True**.</span></span>    

<span data-ttu-id="b2a96-200">This example uses Graph Explorer:</span><span class="sxs-lookup"><span data-stu-id="b2a96-200">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```
<span data-ttu-id="b2a96-201">This example uses the [Azure portal](https://portal.azure.com) to udpate the *acceptedMappedClaims* field:</span><span class="sxs-lookup"><span data-stu-id="b2a96-201">This example uses the [Azure portal](https://portal.azure.com) to udpate the *acceptedMappedClaims* field:</span></span>
1. <span data-ttu-id="b2a96-202">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span><span class="sxs-lookup"><span data-stu-id="b2a96-202">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="b2a96-203">Select **Azure Active Directory** > **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-203">Select **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="b2a96-204">Select your application > **Manifest**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-204">Select your application > **Manifest**.</span></span>
4. <span data-ttu-id="b2a96-205">Select **Edit**, search for the *acceptedMappedClaims* field and change the value to **true**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-205">Select **Edit**, search for the *acceptedMappedClaims* field and change the value to **true**.</span></span>
<span data-ttu-id="b2a96-206">![App manifest](./media/application-proxy-configure-single-sign-on-with-ping-access/application-proxy-ping-access-manifest.PNG)</span><span class="sxs-lookup"><span data-stu-id="b2a96-206">![App manifest](./media/application-proxy-configure-single-sign-on-with-ping-access/application-proxy-ping-access-manifest.PNG)</span></span>
1. <span data-ttu-id="b2a96-207">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="b2a96-207">Select **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="b2a96-208">To use a custom claim, you must also have a custom policy defined and assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="b2a96-208">To use a custom claim, you must also have a custom policy defined and assigned to the application.</span></span>  <span data-ttu-id="b2a96-209">This policy should include all required custom attributes.</span><span class="sxs-lookup"><span data-stu-id="b2a96-209">This policy should include all required custom attributes.</span></span>
>
><span data-ttu-id="b2a96-210">Policy definition and assignment can be done through PowerShell, Azure AD Graph Explorer, or MS Graph.</span><span class="sxs-lookup"><span data-stu-id="b2a96-210">Policy definition and assignment can be done through PowerShell, Azure AD Graph Explorer, or MS Graph.</span></span>  <span data-ttu-id="b2a96-211">If you are doing this in PowerShell, you may need to first use `New-AzureADPolicy `and then assign it to the application with `Set-AzureADServicePrincipalPolicy`.</span><span class="sxs-lookup"><span data-stu-id="b2a96-211">If you are doing this in PowerShell, you may need to first use `New-AzureADPolicy `and then assign it to the application with `Set-AzureADServicePrincipalPolicy`.</span></span>  <span data-ttu-id="b2a96-212">For more information see the [Azure AD Policy documentation](../active-directory-claims-mapping.md#claims-mapping-policy-assignment).</span><span class="sxs-lookup"><span data-stu-id="b2a96-212">For more information see the [Azure AD Policy documentation](../active-directory-claims-mapping.md#claims-mapping-policy-assignment).</span></span>

### <a name="optional---use-a-custom-claim"></a><span data-ttu-id="b2a96-213">Optional - Use a custom claim</span><span class="sxs-lookup"><span data-stu-id="b2a96-213">Optional - Use a custom claim</span></span>
<span data-ttu-id="b2a96-214">To make your application use a custom claim and include additional fields, be sure that you have also [created a custom claims mapping policy and assigned it to the application](../active-directory-claims-mapping.md#claims-mapping-policy-assignment).</span><span class="sxs-lookup"><span data-stu-id="b2a96-214">To make your application use a custom claim and include additional fields, be sure that you have also [created a custom claims mapping policy and assigned it to the application](../active-directory-claims-mapping.md#claims-mapping-policy-assignment).</span></span>

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="b2a96-215">Download PingAccess and configure your app</span><span class="sxs-lookup"><span data-stu-id="b2a96-215">Download PingAccess and configure your app</span></span>

<span data-ttu-id="b2a96-216">Now that you've completed all the Azure Active Directory setup steps, you can move on to configuring PingAccess.</span><span class="sxs-lookup"><span data-stu-id="b2a96-216">Now that you've completed all the Azure Active Directory setup steps, you can move on to configuring PingAccess.</span></span> 

<span data-ttu-id="b2a96-217">The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="b2a96-217">The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="b2a96-218">Those steps walk you through the process of getting a PingAccess account if you don't already have one, installing the PingAccess Server, and creating an Azure AD OIDC Provider connection with the Directory ID that you copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b2a96-218">Those steps walk you through the process of getting a PingAccess account if you don't already have one, installing the PingAccess Server, and creating an Azure AD OIDC Provider connection with the Directory ID that you copied from the Azure portal.</span></span> <span data-ttu-id="b2a96-219">Then, you use the Application ID and Key values to create a Web Session on PingAccess.</span><span class="sxs-lookup"><span data-stu-id="b2a96-219">Then, you use the Application ID and Key values to create a Web Session on PingAccess.</span></span> <span data-ttu-id="b2a96-220">After that, you can set up identity mapping and create a virtual host, site, and application.</span><span class="sxs-lookup"><span data-stu-id="b2a96-220">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="b2a96-221">Test your app</span><span class="sxs-lookup"><span data-stu-id="b2a96-221">Test your app</span></span>

<span data-ttu-id="b2a96-222">When you've completed all these steps, your app should be up and running.</span><span class="sxs-lookup"><span data-stu-id="b2a96-222">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="b2a96-223">To test it, open a browser and navigate to the external URL that you created when you published the app in Azure.</span><span class="sxs-lookup"><span data-stu-id="b2a96-223">To test it, open a browser and navigate to the external URL that you created when you published the app in Azure.</span></span> <span data-ttu-id="b2a96-224">Sign in with the test account that you assigned to the app.</span><span class="sxs-lookup"><span data-stu-id="b2a96-224">Sign in with the test account that you assigned to the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2a96-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="b2a96-225">Next steps</span></span>

- [<span data-ttu-id="b2a96-226">Configure PingAccess for Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2a96-226">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="b2a96-227">How does Azure AD Application Proxy provide single sign-on?</span><span class="sxs-lookup"><span data-stu-id="b2a96-227">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-single-sign-on.md)
- [<span data-ttu-id="b2a96-228">Troubleshoot Application Proxy</span><span class="sxs-lookup"><span data-stu-id="b2a96-228">Troubleshoot Application Proxy</span></span>](application-proxy-troubleshoot.md)
