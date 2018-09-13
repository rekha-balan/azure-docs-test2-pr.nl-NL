---
title: Publish apps with Azure AD Application Proxy | Microsoft Docs
description: Publish on-premises applications to the cloud with Azure AD Application Proxy in the Azure portal.
services: active-directory
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.topic: conceptual
ms.date: 08/20/2018
ms.author: barbkess
ms.reviewer: japere
ms.custom: it-pro
ms.openlocfilehash: 973a6201a227e6c2e295e6e5ea2f40c302572504
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966244"
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="e8c24-103">Publish applications using Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="e8c24-103">Publish applications using Azure AD Application Proxy</span></span>

<span data-ttu-id="e8c24-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="e8c24-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="e8c24-105">You can publish these applications through the Azure portal to provide secure remote access from outside your network.</span><span class="sxs-lookup"><span data-stu-id="e8c24-105">You can publish these applications through the Azure portal to provide secure remote access from outside your network.</span></span>

<span data-ttu-id="e8c24-106">This article walks you through the steps to publish an on-premises app with Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="e8c24-106">This article walks you through the steps to publish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="e8c24-107">After you complete this article, your users will be able to access your app remotely.</span><span class="sxs-lookup"><span data-stu-id="e8c24-107">After you complete this article, your users will be able to access your app remotely.</span></span> <span data-ttu-id="e8c24-108">And you'll be ready to configure extra features for the application like single sign-on, personalized information, and security requirements.</span><span class="sxs-lookup"><span data-stu-id="e8c24-108">And you'll be ready to configure extra features for the application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="e8c24-109">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](application-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="e8c24-109">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](application-proxy.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e8c24-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="e8c24-110">Before you begin</span></span>

<span data-ttu-id="e8c24-111">This article assumes you have already installed and registered a connector.</span><span class="sxs-lookup"><span data-stu-id="e8c24-111">This article assumes you have already installed and registered a connector.</span></span> <span data-ttu-id="e8c24-112">If you still need to do those steps, see [Get started with Application Proxy and install the Connector](application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="e8c24-112">If you still need to do those steps, see [Get started with Application Proxy and install the Connector](application-proxy-enable.md).</span></span>

## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="e8c24-113">Publish an on-premises app for remote access</span><span class="sxs-lookup"><span data-stu-id="e8c24-113">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="e8c24-114">Follow these steps to publish your apps with Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="e8c24-114">Follow these steps to publish your apps with Application Proxy.</span></span> <span data-ttu-id="e8c24-115">If you haven't already downloaded and configured a connector for your organization, go to [Get started with Application Proxy and install the connector](application-proxy-enable.md) first, and then publish your app.</span><span class="sxs-lookup"><span data-stu-id="e8c24-115">If you haven't already downloaded and configured a connector for your organization, go to [Get started with Application Proxy and install the connector](application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="e8c24-116">If you're testing out Application Proxy for the first time, choose an application that's set up for password-based authentication.</span><span class="sxs-lookup"><span data-stu-id="e8c24-116">If you're testing out Application Proxy for the first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="e8c24-117">Application Proxy supports other types of authentication, but password-based apps are the easiest to get up and running quickly.</span><span class="sxs-lookup"><span data-stu-id="e8c24-117">Application Proxy supports other types of authentication, but password-based apps are the easiest to get up and running quickly.</span></span> 

1. <span data-ttu-id="e8c24-118">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e8c24-118">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e8c24-119">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span><span class="sxs-lookup"><span data-stu-id="e8c24-119">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Add an enterprise application](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="e8c24-121">Select **All**, then select **On-premises application**.</span><span class="sxs-lookup"><span data-stu-id="e8c24-121">Select **All**, then select **On-premises application**.</span></span>  

  ![Add your own application](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="e8c24-123">Provide the following information about your application:</span><span class="sxs-lookup"><span data-stu-id="e8c24-123">Provide the following information about your application:</span></span>

   - <span data-ttu-id="e8c24-124">**Name**: The name of the application that will appear on the access panel and in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e8c24-124">**Name**: The name of the application that will appear on the access panel and in the Azure portal.</span></span> 

   - <span data-ttu-id="e8c24-125">**Internal URL**: The URL that you use to access the application from inside your private network.</span><span class="sxs-lookup"><span data-stu-id="e8c24-125">**Internal URL**: The URL that you use to access the application from inside your private network.</span></span> <span data-ttu-id="e8c24-126">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span><span class="sxs-lookup"><span data-stu-id="e8c24-126">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="e8c24-127">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span><span class="sxs-lookup"><span data-stu-id="e8c24-127">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="e8c24-128">If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application.</span><span class="sxs-lookup"><span data-stu-id="e8c24-128">If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="e8c24-129">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.</span><span class="sxs-lookup"><span data-stu-id="e8c24-129">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.</span></span> <span data-ttu-id="e8c24-130">This internal URL doesn't have to be the landing page your users see.</span><span class="sxs-lookup"><span data-stu-id="e8c24-130">This internal URL doesn't have to be the landing page your users see.</span></span> <span data-ttu-id="e8c24-131">For more information, see [Set a custom home page for published apps](application-proxy-configure-custom-home-page.md).</span><span class="sxs-lookup"><span data-stu-id="e8c24-131">For more information, see [Set a custom home page for published apps](application-proxy-configure-custom-home-page.md).</span></span>

   - <span data-ttu-id="e8c24-132">**External URL**: The address your users will go to in order to access the app from outside your network.</span><span class="sxs-lookup"><span data-stu-id="e8c24-132">**External URL**: The address your users will go to in order to access the app from outside your network.</span></span> <span data-ttu-id="e8c24-133">If you don't want to use the default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](application-proxy-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="e8c24-133">If you don't want to use the default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](application-proxy-configure-custom-domain.md).</span></span>
   - <span data-ttu-id="e8c24-134">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span><span class="sxs-lookup"><span data-stu-id="e8c24-134">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span></span> 

     - <span data-ttu-id="e8c24-135">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span><span class="sxs-lookup"><span data-stu-id="e8c24-135">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span> <span data-ttu-id="e8c24-136">We recommend keeping this option as the default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="e8c24-136">We recommend keeping this option as the default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="e8c24-137">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span><span class="sxs-lookup"><span data-stu-id="e8c24-137">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span></span> <span data-ttu-id="e8c24-138">You can still set up authentication requirements on the backend.</span><span class="sxs-lookup"><span data-stu-id="e8c24-138">You can still set up authentication requirements on the backend.</span></span>
   - <span data-ttu-id="e8c24-139">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span><span class="sxs-lookup"><span data-stu-id="e8c24-139">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="e8c24-140">If you don't have any connector groups created yet, your app is assigned to **Default**.</span><span class="sxs-lookup"><span data-stu-id="e8c24-140">If you don't have any connector groups created yet, your app is assigned to **Default**.</span></span>

>[!NOTE]
><span data-ttu-id="e8c24-141">If your application uses websockets to connect, make sure that you have connector version 1.5.612.0 or higher with websocket support and the assigned Connector Group only uses these connectors.</span><span class="sxs-lookup"><span data-stu-id="e8c24-141">If your application uses websockets to connect, make sure that you have connector version 1.5.612.0 or higher with websocket support and the assigned Connector Group only uses these connectors.</span></span>

   ![Configure your application](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="e8c24-143">If necessary, configure additional settings.</span><span class="sxs-lookup"><span data-stu-id="e8c24-143">If necessary, configure additional settings.</span></span> <span data-ttu-id="e8c24-144">For most applications, you should keep these settings in their default states.</span><span class="sxs-lookup"><span data-stu-id="e8c24-144">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="e8c24-145">**Backend Application Timeout**: Set this value to **Long** only if your application is slow to authenticate and connect.</span><span class="sxs-lookup"><span data-stu-id="e8c24-145">**Backend Application Timeout**: Set this value to **Long** only if your application is slow to authenticate and connect.</span></span> 
   - <span data-ttu-id="e8c24-146">**Use HTTP-Only Cookie**: Set this value to **Yes** to have Application Proxy cookies include the HTTPOnly flag in the HTTP response header.</span><span class="sxs-lookup"><span data-stu-id="e8c24-146">**Use HTTP-Only Cookie**: Set this value to **Yes** to have Application Proxy cookies include the HTTPOnly flag in the HTTP response header.</span></span>
   - <span data-ttu-id="e8c24-147">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required the original host header in the authentication request.</span><span class="sxs-lookup"><span data-stu-id="e8c24-147">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required the original host header in the authentication request.</span></span>
   - <span data-ttu-id="e8c24-148">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links to other on-premises applications, and don't use custom domains.</span><span class="sxs-lookup"><span data-stu-id="e8c24-148">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links to other on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="e8c24-149">For more information, see [Link translation with Application Proxy](application-proxy-configure-hard-coded-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="e8c24-149">For more information, see [Link translation with Application Proxy](application-proxy-configure-hard-coded-link-translation.md).</span></span>
   
   ![Configure your application](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="e8c24-151">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="e8c24-151">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="e8c24-152">Add a test user</span><span class="sxs-lookup"><span data-stu-id="e8c24-152">Add a test user</span></span> 

<span data-ttu-id="e8c24-153">To test that your app was published correctly, add a test user account.</span><span class="sxs-lookup"><span data-stu-id="e8c24-153">To test that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="e8c24-154">Verify that this account already has permissions to access the app from inside the corporate network.</span><span class="sxs-lookup"><span data-stu-id="e8c24-154">Verify that this account already has permissions to access the app from inside the corporate network.</span></span>

1. <span data-ttu-id="e8c24-155">Back on the Quick start blade, select **Assign a user for testing**.</span><span class="sxs-lookup"><span data-stu-id="e8c24-155">Back on the Quick start blade, select **Assign a user for testing**.</span></span>

  ![Assign a user for testing](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="e8c24-157">On the Users and groups blade, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="e8c24-157">On the Users and groups blade, select **Add**.</span></span>

  ![Add a user or group](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="e8c24-159">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span><span class="sxs-lookup"><span data-stu-id="e8c24-159">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span></span> 
4. <span data-ttu-id="e8c24-160">Select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="e8c24-160">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="e8c24-161">Test your published app</span><span class="sxs-lookup"><span data-stu-id="e8c24-161">Test your published app</span></span>

<span data-ttu-id="e8c24-162">In your browser, navigate to the external URL that you configured during the publish step.</span><span class="sxs-lookup"><span data-stu-id="e8c24-162">In your browser, navigate to the external URL that you configured during the publish step.</span></span> <span data-ttu-id="e8c24-163">You should see the start screen, and be able to sign in with the test account you set up.</span><span class="sxs-lookup"><span data-stu-id="e8c24-163">You should see the start screen, and be able to sign in with the test account you set up.</span></span>

![Test your published app](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="e8c24-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8c24-165">Next steps</span></span>
- <span data-ttu-id="e8c24-166">[Download connectors](application-proxy-enable.md) and [create connector groups](application-proxy-connector-groups.md) to publish applications on separate networks and locations.</span><span class="sxs-lookup"><span data-stu-id="e8c24-166">[Download connectors](application-proxy-enable.md) and [create connector groups](application-proxy-connector-groups.md) to publish applications on separate networks and locations.</span></span>

- <span data-ttu-id="e8c24-167">[Set up single sign-on](application-proxy-configure-single-sign-on-password-vaulting.md) for your newly published app</span><span class="sxs-lookup"><span data-stu-id="e8c24-167">[Set up single sign-on](application-proxy-configure-single-sign-on-password-vaulting.md) for your newly published app</span></span>
