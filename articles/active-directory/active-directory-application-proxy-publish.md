---
title: Publish apps with Azure AD Application Proxy | Microsoft Docs
description: Publish on-premises applications to the cloud with Azure AD Application Proxy in the classic portal.
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
ms.topic: get-started-article
ms.date: 11/30/2016
ms.author: kgremban
ms.openlocfilehash: c6ebfcfd65150677f653201bc9d29688f88344bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555282"
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="96506-103">Publish applications using Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="96506-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-proxy-publish-azure-portal.md)
> * [Azure classic portal](active-directory-application-proxy-publish.md)

<span data-ttu-id="96506-106">Azure AD Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="96506-106">Azure AD Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="96506-107">By this point, you should already have [enabled Application Proxy in the Azure classic portal](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="96506-107">By this point, you should already have [enabled Application Proxy in the Azure classic portal](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="96506-108">This article walks you through the steps to publish applications that are running on your local network and provide secure remote access from outside your network.</span><span class="sxs-lookup"><span data-stu-id="96506-108">This article walks you through the steps to publish applications that are running on your local network and provide secure remote access from outside your network.</span></span> <span data-ttu-id="96506-109">After you complete this article, you'll be ready to configure the application with personalized information or security requirements.</span><span class="sxs-lookup"><span data-stu-id="96506-109">After you complete this article, you'll be ready to configure the application with personalized information or security requirements.</span></span>

> [!NOTE]
> Application Proxy is a feature that is available only if you upgraded to the Premium or Basic edition of Azure Active Directory. For more information, see [Azure Active Directory editions](active-directory-editions.md).
> 
> 

## <a name="publish-an-app-using-the-wizard"></a><span data-ttu-id="96506-112">Publish an app using the wizard</span><span class="sxs-lookup"><span data-stu-id="96506-112">Publish an app using the wizard</span></span>
1. <span data-ttu-id="96506-113">Sign in as an administrator in the [Azure classic portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="96506-113">Sign in as an administrator in the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="96506-114">Go to Active Directory and select the directory where you enabled Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="96506-114">Go to Active Directory and select the directory where you enabled Application Proxy.</span></span>
   
    ![Active Directory - icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-publish/ad_icon.png)
3. <span data-ttu-id="96506-116">Click the **Applications** tab, and then click the **Add** button at the bottom of the screen</span><span class="sxs-lookup"><span data-stu-id="96506-116">Click the **Applications** tab, and then click the **Add** button at the bottom of the screen</span></span>
   
    ![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. <span data-ttu-id="96506-118">Select **Publish an application that will be accessible from outside your network**.</span><span class="sxs-lookup"><span data-stu-id="96506-118">Select **Publish an application that will be accessible from outside your network**.</span></span>
   
    ![Publish an application that will be accessible from outside your network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. <span data-ttu-id="96506-120">Provide the following information about your application:</span><span class="sxs-lookup"><span data-stu-id="96506-120">Provide the following information about your application:</span></span>
   
   * <span data-ttu-id="96506-121">**Name**: The user-friendly name for your application.</span><span class="sxs-lookup"><span data-stu-id="96506-121">**Name**: The user-friendly name for your application.</span></span> <span data-ttu-id="96506-122">It must be unique within your directory.</span><span class="sxs-lookup"><span data-stu-id="96506-122">It must be unique within your directory.</span></span>
   * <span data-ttu-id="96506-123">**Internal URL**: The address that the Application Proxy Connector uses to access the application from inside your private network.</span><span class="sxs-lookup"><span data-stu-id="96506-123">**Internal URL**: The address that the Application Proxy Connector uses to access the application from inside your private network.</span></span> <span data-ttu-id="96506-124">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span><span class="sxs-lookup"><span data-stu-id="96506-124">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="96506-125">In this way, you can publish different sites on the same server, and give each one its own name and access rules.</span><span class="sxs-lookup"><span data-stu-id="96506-125">In this way, you can publish different sites on the same server, and give each one its own name and access rules.</span></span>
     
     > [!TIP]
     > If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application. For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.
     > 
     > 
   * <span data-ttu-id="96506-128">**Preauthentication Method**: How Application Proxy verifies users before giving them access to your application.</span><span class="sxs-lookup"><span data-stu-id="96506-128">**Preauthentication Method**: How Application Proxy verifies users before giving them access to your application.</span></span> <span data-ttu-id="96506-129">Choose one of the options from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="96506-129">Choose one of the options from the drop-down menu.</span></span>
     
     * <span data-ttu-id="96506-130">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span><span class="sxs-lookup"><span data-stu-id="96506-130">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span>
     * <span data-ttu-id="96506-131">Passthrough: Users don't have to authenticate to access the application.</span><span class="sxs-lookup"><span data-stu-id="96506-131">Passthrough: Users don't have to authenticate to access the application.</span></span>
     
     ![Application properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. <span data-ttu-id="96506-133">To finish the wizard, click the check mark at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="96506-133">To finish the wizard, click the check mark at the bottom of the screen.</span></span> <span data-ttu-id="96506-134">The application is now defined in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96506-134">The application is now defined in Azure AD.</span></span>

## <a name="assign-users-and-groups-to-the-application"></a><span data-ttu-id="96506-135">Assign users and groups to the application</span><span class="sxs-lookup"><span data-stu-id="96506-135">Assign users and groups to the application</span></span>
<span data-ttu-id="96506-136">In order for your users to access your published application, you need to assign them either individually or in groups.</span><span class="sxs-lookup"><span data-stu-id="96506-136">In order for your users to access your published application, you need to assign them either individually or in groups.</span></span> <span data-ttu-id="96506-137">(Remember to assign yourself access, too.) This requires that each user have a license for Azure Basic or higher.</span><span class="sxs-lookup"><span data-stu-id="96506-137">(Remember to assign yourself access, too.) This requires that each user have a license for Azure Basic or higher.</span></span> <span data-ttu-id="96506-138">You can assign licenses individually or to groups.</span><span class="sxs-lookup"><span data-stu-id="96506-138">You can assign licenses individually or to groups.</span></span> <span data-ttu-id="96506-139">See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="96506-139">See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) for more details.</span></span> 

<span data-ttu-id="96506-140">For apps that require preauthentication, this grants permissions to use the app.</span><span class="sxs-lookup"><span data-stu-id="96506-140">For apps that require preauthentication, this grants permissions to use the app.</span></span> <span data-ttu-id="96506-141">For apps that don't require preauthentication, users can still be assigned to the app so that it appears in their application list, such as MyApps.</span><span class="sxs-lookup"><span data-stu-id="96506-141">For apps that don't require preauthentication, users can still be assigned to the app so that it appears in their application list, such as MyApps.</span></span>

1. <span data-ttu-id="96506-142">After finishing the Add App wizard, you see the Quick Start page for your application.</span><span class="sxs-lookup"><span data-stu-id="96506-142">After finishing the Add App wizard, you see the Quick Start page for your application.</span></span> <span data-ttu-id="96506-143">To manage who has access to the app, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="96506-143">To manage who has access to the app, select **Users and groups**.</span></span>
   
    ![Application Proxy quick start assign users - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. <span data-ttu-id="96506-145">Search for specific groups in your directory, or show all your users.</span><span class="sxs-lookup"><span data-stu-id="96506-145">Search for specific groups in your directory, or show all your users.</span></span> <span data-ttu-id="96506-146">To display the search results, click the check mark.</span><span class="sxs-lookup"><span data-stu-id="96506-146">To display the search results, click the check mark.</span></span>
   
      ![Search for groups or users - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. <span data-ttu-id="96506-148">Select each user or group you want to assign to this app and click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="96506-148">Select each user or group you want to assign to this app and click **Assign**.</span></span> <span data-ttu-id="96506-149">You are asked to confirm this action.</span><span class="sxs-lookup"><span data-stu-id="96506-149">You are asked to confirm this action.</span></span>

> [!NOTE]
> For Integrated Windows Authentication apps, you can assign only users and groups that are synced from your on-premises Active Directory. Users who sign in with a Microsoft account and guests cannot be assigned for apps published with Azure Active Directory Application Proxy. Make sure your users sign in with credentials that are part of the same domain as the app you are publishing.
> 
> 

## <a name="test-your-published-application"></a><span data-ttu-id="96506-153">Test your published application</span><span class="sxs-lookup"><span data-stu-id="96506-153">Test your published application</span></span>
<span data-ttu-id="96506-154">Once you have published your application, you can test it out by navigating to the URL that you published.</span><span class="sxs-lookup"><span data-stu-id="96506-154">Once you have published your application, you can test it out by navigating to the URL that you published.</span></span> <span data-ttu-id="96506-155">Make sure that you can access it, that it renders correctly, and that everything works as expected.</span><span class="sxs-lookup"><span data-stu-id="96506-155">Make sure that you can access it, that it renders correctly, and that everything works as expected.</span></span> <span data-ttu-id="96506-156">If you have trouble or get an error message, try the [troubleshooting guide](active-directory-application-proxy-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="96506-156">If you have trouble or get an error message, try the [troubleshooting guide](active-directory-application-proxy-troubleshoot.md).</span></span>

## <a name="configure-your-application"></a><span data-ttu-id="96506-157">Configure your application</span><span class="sxs-lookup"><span data-stu-id="96506-157">Configure your application</span></span>
<span data-ttu-id="96506-158">You can modify published apps or set up advanced options on the Configure page.</span><span class="sxs-lookup"><span data-stu-id="96506-158">You can modify published apps or set up advanced options on the Configure page.</span></span> <span data-ttu-id="96506-159">On this page, you can customize your app by changing the name or uploading a logo.</span><span class="sxs-lookup"><span data-stu-id="96506-159">On this page, you can customize your app by changing the name or uploading a logo.</span></span> <span data-ttu-id="96506-160">You can also manage access rules like the preauthentication method or multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="96506-160">You can also manage access rules like the preauthentication method or multi-factor authentication.</span></span>

![Advanced configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

<span data-ttu-id="96506-162">After you publish applications using Azure Active Directory Application Proxy, they appear in the Applications list in Azure AD, and you can manage them there.</span><span class="sxs-lookup"><span data-stu-id="96506-162">After you publish applications using Azure Active Directory Application Proxy, they appear in the Applications list in Azure AD, and you can manage them there.</span></span>

<span data-ttu-id="96506-163">If you disable Application Proxy services after you have published applications, they are no longer accessible from outside your private network.</span><span class="sxs-lookup"><span data-stu-id="96506-163">If you disable Application Proxy services after you have published applications, they are no longer accessible from outside your private network.</span></span> <span data-ttu-id="96506-164">This does not delete the applications.</span><span class="sxs-lookup"><span data-stu-id="96506-164">This does not delete the applications.</span></span>

<span data-ttu-id="96506-165">To view an application and make sure that it is accessible, double-click the name of the application.</span><span class="sxs-lookup"><span data-stu-id="96506-165">To view an application and make sure that it is accessible, double-click the name of the application.</span></span> <span data-ttu-id="96506-166">If the Application Proxy service is disabled and the application is not available, a warning message appears at the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="96506-166">If the Application Proxy service is disabled and the application is not available, a warning message appears at the top of the screen.</span></span>

<span data-ttu-id="96506-167">To delete an application, select an application in the list and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="96506-167">To delete an application, select an application in the list and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96506-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="96506-168">Next steps</span></span>
* [<span data-ttu-id="96506-169">Publish applications using your own domain name</span><span class="sxs-lookup"><span data-stu-id="96506-169">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="96506-170">Enable single-sign on</span><span class="sxs-lookup"><span data-stu-id="96506-170">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="96506-171">Enable conditional access</span><span class="sxs-lookup"><span data-stu-id="96506-171">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="96506-172">Working with claims aware applications</span><span class="sxs-lookup"><span data-stu-id="96506-172">Working with claims aware applications</span></span>](active-directory-application-proxy-claims-aware-apps.md)

<span data-ttu-id="96506-173">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="96506-173">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>








