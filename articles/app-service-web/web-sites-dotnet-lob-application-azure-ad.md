---
title: Create a line-of-business Azure app with Azure Active Directory authentication | Microsoft Docs
description: Learn how to create an ASP.NET MVC line-of-business app in Azure App Service that authenticates with Azure Active Directory
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: ''
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 1e12e2910b6ff18bcca9a369c118e7daf5cadb0a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553433"
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="49b72-103">Create a line-of-business Azure app with Azure Active Directory authentication</span><span class="sxs-lookup"><span data-stu-id="49b72-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="49b72-104">This article shows you how to create a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using the [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span><span class="sxs-lookup"><span data-stu-id="49b72-104">This article shows you how to create a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using the [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="49b72-105">It also shows how to use the [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to query directory data in the application.</span><span class="sxs-lookup"><span data-stu-id="49b72-105">It also shows how to use the [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to query directory data in the application.</span></span>

<span data-ttu-id="49b72-106">The Azure Active Directory tenant that you use can be an Azure-only directory.</span><span class="sxs-lookup"><span data-stu-id="49b72-106">The Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="49b72-107">Or, it can be [synced with your on-premise Active Directory](../active-directory/active-directory-aadconnect.md) to create a single sign-on experience for workers that are on-premises and remote.</span><span class="sxs-lookup"><span data-stu-id="49b72-107">Or, it can be [synced with your on-premise Active Directory](../active-directory/active-directory-aadconnect.md) to create a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="49b72-108">This article uses the default directory for your Azure account.</span><span class="sxs-lookup"><span data-stu-id="49b72-108">This article uses the default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="49b72-109">What you will build</span><span class="sxs-lookup"><span data-stu-id="49b72-109">What you will build</span></span>
<span data-ttu-id="49b72-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with the following features:</span><span class="sxs-lookup"><span data-stu-id="49b72-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with the following features:</span></span>

* <span data-ttu-id="49b72-111">Authenticates users against Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49b72-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="49b72-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="49b72-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="49b72-113">Use the ASP.NET MVC *No Authentication* template</span><span class="sxs-lookup"><span data-stu-id="49b72-113">Use the ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="49b72-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span><span class="sxs-lookup"><span data-stu-id="49b72-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="49b72-115">What you need</span><span class="sxs-lookup"><span data-stu-id="49b72-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="49b72-116">You need the following to complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="49b72-116">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="49b72-117">An Azure Active Directory tenant with users in various groups</span><span class="sxs-lookup"><span data-stu-id="49b72-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="49b72-118">Permissions to create applications on the Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="49b72-118">Permissions to create applications on the Azure Active Directory tenant</span></span>
* <span data-ttu-id="49b72-119">Visual Studio 2013 Update 4 or later</span><span class="sxs-lookup"><span data-stu-id="49b72-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="49b72-120">Azure SDK 2.8.1 or later</span><span class="sxs-lookup"><span data-stu-id="49b72-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-to-azure"></a><span data-ttu-id="49b72-121">Create and deploy a web app to Azure</span><span class="sxs-lookup"><span data-stu-id="49b72-121">Create and deploy a web app to Azure</span></span>
1. <span data-ttu-id="49b72-122">From Visual Studio, click **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="49b72-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="49b72-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="49b72-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="49b72-124">Select the **MVC** template, then change the authentication to **No Authentication**.</span><span class="sxs-lookup"><span data-stu-id="49b72-124">Select the **MVC** template, then change the authentication to **No Authentication**.</span></span> <span data-ttu-id="49b72-125">Make sure **Host in the Cloud** is selected and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="49b72-125">Make sure **Host in the Cloud** is selected and click **OK**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="49b72-126">In the **Create App Service** dialog, click **Add an account** (and then **Add an account** in the dropdown) to log in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="49b72-126">In the **Create App Service** dialog, click **Add an account** (and then **Add an account** in the dropdown) to log in to your Azure account.</span></span>
5. <span data-ttu-id="49b72-127">Once logged in configure your web app.</span><span class="sxs-lookup"><span data-stu-id="49b72-127">Once logged in configure your web app.</span></span> <span data-ttu-id="49b72-128">Create a resource group and a new App Service plan by clicking the respective **New** button.</span><span class="sxs-lookup"><span data-stu-id="49b72-128">Create a resource group and a new App Service plan by clicking the respective **New** button.</span></span> <span data-ttu-id="49b72-129">Click **Explore additional Azure services** to continue.</span><span class="sxs-lookup"><span data-stu-id="49b72-129">Click **Explore additional Azure services** to continue.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="49b72-130">In the **Services** tab, click **+** to add a SQL Database for your app.</span><span class="sxs-lookup"><span data-stu-id="49b72-130">In the **Services** tab, click **+** to add a SQL Database for your app.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="49b72-131">In **Configure SQL Database**, click **New** to create a SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="49b72-131">In **Configure SQL Database**, click **New** to create a SQL Server instance.</span></span>
8. <span data-ttu-id="49b72-132">In **Configure SQL Server**, configure your SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="49b72-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="49b72-133">Then, click **OK**, **OK**, and **Create** to kick off the app creation in Azure.</span><span class="sxs-lookup"><span data-stu-id="49b72-133">Then, click **OK**, **OK**, and **Create** to kick off the app creation in Azure.</span></span>
9. <span data-ttu-id="49b72-134">In **Azure App Service Activity**, you can see when the app creation is finished.</span><span class="sxs-lookup"><span data-stu-id="49b72-134">In **Azure App Service Activity**, you can see when the app creation is finished.</span></span> <span data-ttu-id="49b72-135">Click **Publish &lt;*appname*> to this Web App now**, then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="49b72-135">Click **Publish &lt;*appname*> to this Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="49b72-136">Once Visual Studio finishes, it opens the publish app in the browser.</span><span class="sxs-lookup"><span data-stu-id="49b72-136">Once Visual Studio finishes, it opens the publish app in the browser.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="49b72-137">Configure authentication and directory access</span><span class="sxs-lookup"><span data-stu-id="49b72-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="49b72-138">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="49b72-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="49b72-139">From the left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span><span class="sxs-lookup"><span data-stu-id="49b72-139">From the left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="49b72-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="49b72-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="49b72-141">Click **Save** in the command bar.</span><span class="sxs-lookup"><span data-stu-id="49b72-141">Click **Save** in the command bar.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="49b72-142">Once the authentication settings are saved successfully, try navigating to your app again in the browser.</span><span class="sxs-lookup"><span data-stu-id="49b72-142">Once the authentication settings are saved successfully, try navigating to your app again in the browser.</span></span> <span data-ttu-id="49b72-143">Your default settings enforce authentication on the whole app.</span><span class="sxs-lookup"><span data-stu-id="49b72-143">Your default settings enforce authentication on the whole app.</span></span> <span data-ttu-id="49b72-144">If you aren't already logged in, you are redirected to a login screen.</span><span class="sxs-lookup"><span data-stu-id="49b72-144">If you aren't already logged in, you are redirected to a login screen.</span></span> <span data-ttu-id="49b72-145">Once logged in, you see your app secured by HTTPS.</span><span class="sxs-lookup"><span data-stu-id="49b72-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="49b72-146">Next, you need to enable access to directory data.</span><span class="sxs-lookup"><span data-stu-id="49b72-146">Next, you need to enable access to directory data.</span></span> 
5. <span data-ttu-id="49b72-147">Navigate to the [classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="49b72-147">Navigate to the [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="49b72-148">From the left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span><span class="sxs-lookup"><span data-stu-id="49b72-148">From the left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="49b72-149">This is the Azure Active Directory application that App Service created for you to enable the Authorization / Authentication feature.</span><span class="sxs-lookup"><span data-stu-id="49b72-149">This is the Azure Active Directory application that App Service created for you to enable the Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="49b72-150">Click **Users** and **Groups** to make sure that you have some users and groups in the directory.</span><span class="sxs-lookup"><span data-stu-id="49b72-150">Click **Users** and **Groups** to make sure that you have some users and groups in the directory.</span></span> <span data-ttu-id="49b72-151">If not, create a few test users and groups.</span><span class="sxs-lookup"><span data-stu-id="49b72-151">If not, create a few test users and groups.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="49b72-152">Click **Configure** to configure this application.</span><span class="sxs-lookup"><span data-stu-id="49b72-152">Click **Configure** to configure this application.</span></span>
9. <span data-ttu-id="49b72-153">Scroll down to the **Keys** section and add a key by selecting a duration.</span><span class="sxs-lookup"><span data-stu-id="49b72-153">Scroll down to the **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="49b72-154">Then, click **Delegated Permissions** and select **Read directory data**.</span><span class="sxs-lookup"><span data-stu-id="49b72-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="49b72-155">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="49b72-155">Click **Save**.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="49b72-156">Once your settings are saved, scroll back up to the **Keys** section and click the **Copy** button to copy the client key.</span><span class="sxs-lookup"><span data-stu-id="49b72-156">Once your settings are saved, scroll back up to the **Keys** section and click the **Copy** button to copy the client key.</span></span> 
    
     ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="49b72-157">If you navigate away from this page now, you won't be able to access this client key ever again.</span><span class="sxs-lookup"><span data-stu-id="49b72-157">If you navigate away from this page now, you won't be able to access this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="49b72-158">Next, you need to configure your web app with this key.</span><span class="sxs-lookup"><span data-stu-id="49b72-158">Next, you need to configure your web app with this key.</span></span> <span data-ttu-id="49b72-159">Log in to the [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="49b72-159">Log in to the [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="49b72-160">At the top of the page, click **Read/Write** to make changes in the Azure Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="49b72-160">At the top of the page, click **Read/Write** to make changes in the Azure Resource Explorer.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="49b72-161">Find the authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="49b72-161">Find the authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="49b72-162">Click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="49b72-162">Click **Edit**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="49b72-163">In the editing pane, set the `clientSecret` and `additionalLoginParams` properties as follows.</span><span class="sxs-lookup"><span data-stu-id="49b72-163">In the editing pane, set the `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from the Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="49b72-164">Click **Put** at the top to submit your changes.</span><span class="sxs-lookup"><span data-stu-id="49b72-164">Click **Put** at the top to submit your changes.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="49b72-165">Now, to test if you have the authorization token to access the Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span><span class="sxs-lookup"><span data-stu-id="49b72-165">Now, to test if you have the authorization token to access the Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="49b72-166">If you configured everything correctly, you should see the `access_token` property in the JSON response.</span><span class="sxs-lookup"><span data-stu-id="49b72-166">If you configured everything correctly, you should see the `access_token` property in the JSON response.</span></span>
    
    <span data-ttu-id="49b72-167">The `~/.auth/me` URL path is managed by App Service Authentication / Authorization to give you all the information related to your authenticated session.</span><span class="sxs-lookup"><span data-stu-id="49b72-167">The `~/.auth/me` URL path is managed by App Service Authentication / Authorization to give you all the information related to your authenticated session.</span></span> <span data-ttu-id="49b72-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49b72-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="49b72-169">The `access_token` has an expiration period.</span><span class="sxs-lookup"><span data-stu-id="49b72-169">The `access_token` has an expiration period.</span></span> <span data-ttu-id="49b72-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="49b72-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="49b72-171">For more information on how to use it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="49b72-171">For more information on how to use it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="49b72-172">Next, you will do something useful with directory data.</span><span class="sxs-lookup"><span data-stu-id="49b72-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-to-your-app"></a><span data-ttu-id="49b72-173">Add line-of-business functionality to your app</span><span class="sxs-lookup"><span data-stu-id="49b72-173">Add line-of-business functionality to your app</span></span>
<span data-ttu-id="49b72-174">Now, you create a simple CRUD work items tracker.</span><span class="sxs-lookup"><span data-stu-id="49b72-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="49b72-175">In the ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with the following code:</span><span class="sxs-lookup"><span data-stu-id="49b72-175">In the ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with the following code:</span></span>
   
     <span data-ttu-id="49b72-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="49b72-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="49b72-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="49b72-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="49b72-178">}</span><span class="sxs-lookup"><span data-stu-id="49b72-178">}</span></span>
   
     <span data-ttu-id="49b72-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="49b72-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="49b72-180">}</span><span class="sxs-lookup"><span data-stu-id="49b72-180">}</span></span>
2. <span data-ttu-id="49b72-181">Build the project to make your new model accessible to the scaffolding logic in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="49b72-181">Build the project to make your new model accessible to the scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="49b72-182">Add a new scaffolded item `WorkItemsController` to the ~\Controllers folder (right-click **Controllers**, point to **Add**, and select **New scaffolded item**).</span><span class="sxs-lookup"><span data-stu-id="49b72-182">Add a new scaffolded item `WorkItemsController` to the ~\Controllers folder (right-click **Controllers**, point to **Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="49b72-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="49b72-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="49b72-184">Select the model that you created, then click **+** and then **Add** to add a data context, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="49b72-184">Select the model that you created, then click **+** and then **Add** to add a data context, and then click **Add**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="49b72-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find the `Html.BeginForm` helper method and make the following highlighted changes:</span><span class="sxs-lookup"><span data-stu-id="49b72-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find the `Html.BeginForm` helper method and make the following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back to List&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit the selected user/group to be asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="49b72-186">Note that `token` and `tenant` are used by the `AadPicker` object to make Azure Active Directory Graph API calls.</span><span class="sxs-lookup"><span data-stu-id="49b72-186">Note that `token` and `tenant` are used by the `AadPicker` object to make Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="49b72-187">You'll add `AadPicker` later.</span><span class="sxs-lookup"><span data-stu-id="49b72-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="49b72-188">You can just as well get `token` and `tenant` from the client side with `~/.auth/me`, but that would be an additional server call.</span><span class="sxs-lookup"><span data-stu-id="49b72-188">You can just as well get `token` and `tenant` from the client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="49b72-189">For example:</span><span class="sxs-lookup"><span data-stu-id="49b72-189">For example:</span></span>
   > 
   > <span data-ttu-id="49b72-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="49b72-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="49b72-191">Make the same changes with ~\Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="49b72-191">Make the same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="49b72-192">The `AadPicker` object is defined in a script that you need to add to your project.</span><span class="sxs-lookup"><span data-stu-id="49b72-192">The `AadPicker` object is defined in a script that you need to add to your project.</span></span> <span data-ttu-id="49b72-193">Right-click the ~\Scripts folder, point to **Add**, and click **JavaScript file**.</span><span class="sxs-lookup"><span data-stu-id="49b72-193">Right-click the ~\Scripts folder, point to **Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="49b72-194">Type `AadPickerLibrary` for the filename and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="49b72-194">Type `AadPickerLibrary` for the filename and click **OK**.</span></span>
9. <span data-ttu-id="49b72-195">Copy the content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="49b72-195">Copy the content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="49b72-196">In the script, the `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to search for users and groups that match the input.</span><span class="sxs-lookup"><span data-stu-id="49b72-196">In the script, the `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to search for users and groups that match the input.</span></span>  
10. <span data-ttu-id="49b72-197">~\Scripts\AadPickerLibrary.js also uses the [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="49b72-197">~\Scripts\AadPickerLibrary.js also uses the [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="49b72-198">So you need to add jQuery UI to your project.</span><span class="sxs-lookup"><span data-stu-id="49b72-198">So you need to add jQuery UI to your project.</span></span> <span data-ttu-id="49b72-199">Right-click your project in and click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="49b72-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="49b72-200">In the NuGet Package Manager, click Browse, type **jquery-ui** in the search bar, and click **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="49b72-200">In the NuGet Package Manager, click Browse, type **jquery-ui** in the search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="49b72-201">In the right pane, click **Install**, then click **OK** to proceed.</span><span class="sxs-lookup"><span data-stu-id="49b72-201">In the right pane, click **Install**, then click **OK** to proceed.</span></span>
13. <span data-ttu-id="49b72-202">Open ~\App_Start\BundleConfig.cs and make the following highlighted changes:</span><span class="sxs-lookup"><span data-stu-id="49b72-202">Open ~\App_Start\BundleConfig.cs and make the following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
        // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="49b72-203">There are more performant ways to manage JavaScript and CSS files in your app.</span><span class="sxs-lookup"><span data-stu-id="49b72-203">There are more performant ways to manage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="49b72-204">However, for simplicity you're just going to piggyback on the bundles that are loaded with every view.</span><span class="sxs-lookup"><span data-stu-id="49b72-204">However, for simplicity you're just going to piggyback on the bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="49b72-205">Finally, in ~\Global.asax, add the following line of code in the `Application_Start()` method.</span><span class="sxs-lookup"><span data-stu-id="49b72-205">Finally, in ~\Global.asax, add the following line of code in the `Application_Start()` method.</span></span> <span data-ttu-id="49b72-206">`Ctrl`+`.` on each naming resolution error to fix it.</span><span class="sxs-lookup"><span data-stu-id="49b72-206">`Ctrl`+`.` on each naming resolution error to fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="49b72-207">You need this line of code because the default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of the actions.</span><span class="sxs-lookup"><span data-stu-id="49b72-207">You need this line of code because the default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of the actions.</span></span> <span data-ttu-id="49b72-208">Due to the behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span><span class="sxs-lookup"><span data-stu-id="49b72-208">Due to the behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="49b72-209">Azure Active Directory does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by the anti-forgery token.</span><span class="sxs-lookup"><span data-stu-id="49b72-209">Azure Active Directory does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by the anti-forgery token.</span></span>
    > * <span data-ttu-id="49b72-210">If Azure Active Directory is directory synced with AD FS, the AD FS trust by default does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS to send this claim.</span><span class="sxs-lookup"><span data-stu-id="49b72-210">If Azure Active Directory is directory synced with AD FS, the AD FS trust by default does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS to send this claim.</span></span>
    > 
    > <span data-ttu-id="49b72-211">`ClaimTypes.NameIdentifies` specifies the claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span><span class="sxs-lookup"><span data-stu-id="49b72-211">`ClaimTypes.NameIdentifies` specifies the claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="49b72-212">Now, publish your changes.</span><span class="sxs-lookup"><span data-stu-id="49b72-212">Now, publish your changes.</span></span> <span data-ttu-id="49b72-213">Right-click your project and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="49b72-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="49b72-214">Click **Settings**, make sure there is a connection string to your SQL Database, select **Update Database** to make the schema changes for your model, and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="49b72-214">Click **Settings**, make sure there is a connection string to your SQL Database, select **Update Database** to make the schema changes for your model, and click **Publish**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="49b72-215">In the browser, navigate to https://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span><span class="sxs-lookup"><span data-stu-id="49b72-215">In the browser, navigate to https://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="49b72-216">Click in the **AssignedToName** box.</span><span class="sxs-lookup"><span data-stu-id="49b72-216">Click in the **AssignedToName** box.</span></span> <span data-ttu-id="49b72-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span><span class="sxs-lookup"><span data-stu-id="49b72-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="49b72-218">You can type to filter, or use the `Up` or `Down` key or click to select the user or group.</span><span class="sxs-lookup"><span data-stu-id="49b72-218">You can type to filter, or use the `Up` or `Down` key or click to select the user or group.</span></span> 
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="49b72-219">Click **Create** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="49b72-219">Click **Create** to save the changes.</span></span> <span data-ttu-id="49b72-220">Then, click **Edit** on the created work item to observe the same behavior.</span><span class="sxs-lookup"><span data-stu-id="49b72-220">Then, click **Edit** on the created work item to observe the same behavior.</span></span>

<span data-ttu-id="49b72-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span><span class="sxs-lookup"><span data-stu-id="49b72-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="49b72-222">There's a lot more you can do with the Graph API.</span><span class="sxs-lookup"><span data-stu-id="49b72-222">There's a lot more you can do with the Graph API.</span></span> <span data-ttu-id="49b72-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="49b72-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="49b72-224">Next Step</span><span class="sxs-lookup"><span data-stu-id="49b72-224">Next Step</span></span>
<span data-ttu-id="49b72-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from the Azure Active Directory team.</span><span class="sxs-lookup"><span data-stu-id="49b72-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from the Azure Active Directory team.</span></span> <span data-ttu-id="49b72-226">It shows you how to enable roles for your Azure Active Directory application, and then authorize users with the `[Authorize]` decoration.</span><span class="sxs-lookup"><span data-stu-id="49b72-226">It shows you how to enable roles for your Azure Active Directory application, and then authorize users with the `[Authorize]` decoration.</span></span>

<span data-ttu-id="49b72-227">If your line-of-business app needs access to on-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="49b72-227">If your line-of-business app needs access to on-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="49b72-228">Further resources</span><span class="sxs-lookup"><span data-stu-id="49b72-228">Further resources</span></span>
* [<span data-ttu-id="49b72-229">Authentication and authorization in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="49b72-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="49b72-230">Authenticate with on-premises Active Directory in your Azure app</span><span class="sxs-lookup"><span data-stu-id="49b72-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="49b72-231">Create a line-of-business app in Azure with AD FS authentication</span><span class="sxs-lookup"><span data-stu-id="49b72-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="49b72-232">App Service Auth and the Azure AD Graph API</span><span class="sxs-lookup"><span data-stu-id="49b72-232">App Service Auth and the Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="49b72-233">Microsoft Azure Active Directory Samples and Documentation</span><span class="sxs-lookup"><span data-stu-id="49b72-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="49b72-234">Azure Active Directory Supported Token and Claim Types</span><span class="sxs-lookup"><span data-stu-id="49b72-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)

[Protect the Application with SSL and the Authorize Attribute]: web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md#protect-the-application-with-ssl-and-the-authorize-attribute


















