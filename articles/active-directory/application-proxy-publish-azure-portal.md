---
title: Publish apps with Azure AD Application Proxy | Microsoft Docs
description: Publish on-premises applications to the cloud with Azure AD Application Proxy in the Azure portal.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: harshja
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: kgremban
ms.openlocfilehash: 9623c9e141ceec25780a2593cd701dc3c244d868
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670319"
---
# <a name="publish-applications-using-azure-ad-application-proxy---public-preview"></a><span data-ttu-id="1b34d-103">Publish applications using Azure AD Application Proxy - Public Preview</span><span class="sxs-lookup"><span data-stu-id="1b34d-103">Publish applications using Azure AD Application Proxy - Public Preview</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-proxy-publish-azure-portal.md)
> * [Azure classic portal](active-directory-application-proxy-publish.md)

<span data-ttu-id="1b34d-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="1b34d-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="1b34d-107">Through the Azure portal, you can publish applications that are running on your local network and provide secure remote access from outside your network.</span><span class="sxs-lookup"><span data-stu-id="1b34d-107">Through the Azure portal, you can publish applications that are running on your local network and provide secure remote access from outside your network.</span></span>

<span data-ttu-id="1b34d-108">This article walks you through the steps to publish an on-premises app with Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="1b34d-108">This article walks you through the steps to publish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="1b34d-109">After you complete this article, you'll be ready to configure the application with single sign-on, personalized information, or security requirements.</span><span class="sxs-lookup"><span data-stu-id="1b34d-109">After you complete this article, you'll be ready to configure the application with single sign-on, personalized information, or security requirements.</span></span>

<span data-ttu-id="1b34d-110">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1b34d-110">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="1b34d-111">Publish an on-premises app for remote access</span><span class="sxs-lookup"><span data-stu-id="1b34d-111">Publish an on-premises app for remote access</span></span>


> [!TIP]
> If this is your first time using Application Proxy, choose an application that's already set up for password-based authentication. Application Proxy supports other types of authentication, but password-based apps are the easiest to get up and running quickly. 

1. <span data-ttu-id="1b34d-114">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1b34d-114">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1b34d-115">Select **Azure Active Directory** > **Enterprise applications** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="1b34d-115">Select **Azure Active Directory** > **Enterprise applications** > **Add**.</span></span>

  ![Add an enterprise application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="1b34d-117">On the Categories page, select **On-premises application**.</span><span class="sxs-lookup"><span data-stu-id="1b34d-117">On the Categories page, select **On-premises application**.</span></span>  

  ![Add your own application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="1b34d-119">Provide the following information about your application:</span><span class="sxs-lookup"><span data-stu-id="1b34d-119">Provide the following information about your application:</span></span>

   - <span data-ttu-id="1b34d-120">**Name**: The name of the application that will appear on the access panel.</span><span class="sxs-lookup"><span data-stu-id="1b34d-120">**Name**: The name of the application that will appear on the access panel.</span></span> 

   - <span data-ttu-id="1b34d-121">**Internal URL**: The address that the Application Proxy Connector uses to access the application from inside your private network.</span><span class="sxs-lookup"><span data-stu-id="1b34d-121">**Internal URL**: The address that the Application Proxy Connector uses to access the application from inside your private network.</span></span> <span data-ttu-id="1b34d-122">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span><span class="sxs-lookup"><span data-stu-id="1b34d-122">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="1b34d-123">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span><span class="sxs-lookup"><span data-stu-id="1b34d-123">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application. For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.

   - <span data-ttu-id="1b34d-126">**External URL**: The address your users will go to in order to access the app from outside your network.</span><span class="sxs-lookup"><span data-stu-id="1b34d-126">**External URL**: The address your users will go to in order to access the app from outside your network.</span></span>
   - <span data-ttu-id="1b34d-127">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span><span class="sxs-lookup"><span data-stu-id="1b34d-127">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span></span> 

     - <span data-ttu-id="1b34d-128">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span><span class="sxs-lookup"><span data-stu-id="1b34d-128">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span> <span data-ttu-id="1b34d-129">We recommend keeping this option as the default.</span><span class="sxs-lookup"><span data-stu-id="1b34d-129">We recommend keeping this option as the default.</span></span>
     - <span data-ttu-id="1b34d-130">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span><span class="sxs-lookup"><span data-stu-id="1b34d-130">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span></span> <span data-ttu-id="1b34d-131">You can still set up authentication requirements on the backend.</span><span class="sxs-lookup"><span data-stu-id="1b34d-131">You can still set up authentication requirements on the backend.</span></span>
   - <span data-ttu-id="1b34d-132">**Translate URL in Headers?**: Choose whether to translate the URL in the headers, or keep the original.</span><span class="sxs-lookup"><span data-stu-id="1b34d-132">**Translate URL in Headers?**: Choose whether to translate the URL in the headers, or keep the original.</span></span> 
   - <span data-ttu-id="1b34d-133">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span><span class="sxs-lookup"><span data-stu-id="1b34d-133">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="1b34d-134">If you don't have any connector groups created yet, your app is assigned to **Default** and you'll see a warning message asking you to [create a connector group](active-directory-application-proxy-connectors-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1b34d-134">If you don't have any connector groups created yet, your app is assigned to **Default** and you'll see a warning message asking you to [create a connector group](active-directory-application-proxy-connectors-azure-portal.md).</span></span>

   ![Configure your application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-publish-azure-portal/configure-app.png)

8. <span data-ttu-id="1b34d-136">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="1b34d-136">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="1b34d-137">Add a test user</span><span class="sxs-lookup"><span data-stu-id="1b34d-137">Add a test user</span></span> 

<span data-ttu-id="1b34d-138">To test that your app was published correctly, add a user account that you have access to.</span><span class="sxs-lookup"><span data-stu-id="1b34d-138">To test that your app was published correctly, add a user account that you have access to.</span></span> 

1. <span data-ttu-id="1b34d-139">Back on the Quick start blade, select **Assign a user for testing**.</span><span class="sxs-lookup"><span data-stu-id="1b34d-139">Back on the Quick start blade, select **Assign a user for testing**.</span></span>

  ![Assign a user for testing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="1b34d-141">On the Users and groups blade, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="1b34d-141">On the Users and groups blade, select **Add**.</span></span>

  ![Add a user or group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="1b34d-143">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span><span class="sxs-lookup"><span data-stu-id="1b34d-143">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span></span> 
4. <span data-ttu-id="1b34d-144">Select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1b34d-144">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="1b34d-145">Test your published app</span><span class="sxs-lookup"><span data-stu-id="1b34d-145">Test your published app</span></span>

<span data-ttu-id="1b34d-146">In your browser, navigate to the external URL that you configured during the publish step.</span><span class="sxs-lookup"><span data-stu-id="1b34d-146">In your browser, navigate to the external URL that you configured during the publish step.</span></span> <span data-ttu-id="1b34d-147">You should see the start screen, and be able to sign in with the test account you set up.</span><span class="sxs-lookup"><span data-stu-id="1b34d-147">You should see the start screen, and be able to sign in with the test account you set up.</span></span>

![Test your published app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="1b34d-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b34d-149">Next steps</span></span>
- <span data-ttu-id="1b34d-150">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) to publish applications on separate networks and locations.</span><span class="sxs-lookup"><span data-stu-id="1b34d-150">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) to publish applications on separate networks and locations.</span></span>

- <span data-ttu-id="1b34d-151">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly-published app</span><span class="sxs-lookup"><span data-stu-id="1b34d-151">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly-published app</span></span>






