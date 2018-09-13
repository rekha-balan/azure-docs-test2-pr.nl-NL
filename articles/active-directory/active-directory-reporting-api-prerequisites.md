---
title: Prerequisites to access the Azure AD reporting API. | Microsoft Docs
description: Learn about the prerequisites to access the Azure AD reporting API
services: active-directory
documentationcenter: ''
author: dhanyahk
manager: femila
editor: ''
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/25/2016
ms.author: dhanyahk;markvi
ms.openlocfilehash: 7d5c56b8eb263a1c85ffcbe91ddde89b6222c6a2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551995"
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="409bb-104">Prerequisites to access the Azure AD reporting API</span><span class="sxs-lookup"><span data-stu-id="409bb-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="409bb-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span><span class="sxs-lookup"><span data-stu-id="409bb-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="409bb-106">You can call these APIs from a variety of programming languages and tools.</span><span class="sxs-lookup"><span data-stu-id="409bb-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="409bb-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span><span class="sxs-lookup"><span data-stu-id="409bb-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="409bb-108">To prepare your access to the reporting API, you must:</span><span class="sxs-lookup"><span data-stu-id="409bb-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="409bb-109">Create an application in your Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="409bb-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="409bb-110">Grant the application appropriate permissions to access the Azure AD data</span><span class="sxs-lookup"><span data-stu-id="409bb-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="409bb-111">Gather configuration settings from your directory</span><span class="sxs-lookup"><span data-stu-id="409bb-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="409bb-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="409bb-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="409bb-113">Create an Azure AD application</span><span class="sxs-lookup"><span data-stu-id="409bb-113">Create an Azure AD application</span></span>
<span data-ttu-id="409bb-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="409bb-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="409bb-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span><span class="sxs-lookup"><span data-stu-id="409bb-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="409bb-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="409bb-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="409bb-118">From the **active directory** list, select your directory.</span><span class="sxs-lookup"><span data-stu-id="409bb-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="409bb-119">In the menu on the top, click **Applications**.</span><span class="sxs-lookup"><span data-stu-id="409bb-119">In the menu on the top, click **Applications**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="409bb-121">On the bottom bar, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="409bb-121">On the bottom bar, click **Add**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="409bb-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span><span class="sxs-lookup"><span data-stu-id="409bb-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="409bb-125">On the **Tell us about your application** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="409bb-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="409bb-127">a.</span><span class="sxs-lookup"><span data-stu-id="409bb-127">a.</span></span> <span data-ttu-id="409bb-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span><span class="sxs-lookup"><span data-stu-id="409bb-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="409bb-129">b.</span><span class="sxs-lookup"><span data-stu-id="409bb-129">b.</span></span> <span data-ttu-id="409bb-130">Select **Web application and/or web API**.</span><span class="sxs-lookup"><span data-stu-id="409bb-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="409bb-131">c.</span><span class="sxs-lookup"><span data-stu-id="409bb-131">c.</span></span> <span data-ttu-id="409bb-132">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="409bb-132">Click **Next**.</span></span>
7. <span data-ttu-id="409bb-133">On the **App properties** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="409bb-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="409bb-135">a.</span><span class="sxs-lookup"><span data-stu-id="409bb-135">a.</span></span> <span data-ttu-id="409bb-136">In the **Sign-on URL** textbox, type `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="409bb-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="409bb-137">b.</span><span class="sxs-lookup"><span data-stu-id="409bb-137">b.</span></span> <span data-ttu-id="409bb-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="409bb-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="409bb-139">c.</span><span class="sxs-lookup"><span data-stu-id="409bb-139">c.</span></span> <span data-ttu-id="409bb-140">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="409bb-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="409bb-141">Grant your application permission to use the API</span><span class="sxs-lookup"><span data-stu-id="409bb-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="409bb-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="409bb-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="409bb-144">From the **active directory** list, select your directory.</span><span class="sxs-lookup"><span data-stu-id="409bb-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="409bb-145">In the menu on the top, click **Applications**.</span><span class="sxs-lookup"><span data-stu-id="409bb-145">In the menu on the top, click **Applications**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="409bb-147">In the applications list, select your newly created application.</span><span class="sxs-lookup"><span data-stu-id="409bb-147">In the applications list, select your newly created application.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="409bb-149">In the menu on the top, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="409bb-149">In the menu on the top, click **Configure**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="409bb-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span><span class="sxs-lookup"><span data-stu-id="409bb-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="409bb-153">On the bottom bar, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="409bb-153">On the bottom bar, click **Save**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="409bb-155">Gather configuration settings from your directory</span><span class="sxs-lookup"><span data-stu-id="409bb-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="409bb-156">This section shows you how to get the following settings from your directory:</span><span class="sxs-lookup"><span data-stu-id="409bb-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="409bb-157">Domain name</span><span class="sxs-lookup"><span data-stu-id="409bb-157">Domain name</span></span>
* <span data-ttu-id="409bb-158">Client ID</span><span class="sxs-lookup"><span data-stu-id="409bb-158">Client ID</span></span>
* <span data-ttu-id="409bb-159">Client secret</span><span class="sxs-lookup"><span data-stu-id="409bb-159">Client secret</span></span>

<span data-ttu-id="409bb-160">You need these values when configuring calls to the reporting API.</span><span class="sxs-lookup"><span data-stu-id="409bb-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="409bb-161">Get your domain name</span><span class="sxs-lookup"><span data-stu-id="409bb-161">Get your domain name</span></span>
1. <span data-ttu-id="409bb-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="409bb-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="409bb-164">From the **active directory** list, select your directory.</span><span class="sxs-lookup"><span data-stu-id="409bb-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="409bb-165">In the menu on the top, click **Domains**.</span><span class="sxs-lookup"><span data-stu-id="409bb-165">In the menu on the top, click **Domains**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="409bb-167">In the **Domain Name** column, copy your domain name.</span><span class="sxs-lookup"><span data-stu-id="409bb-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="409bb-169">Get the application's client ID</span><span class="sxs-lookup"><span data-stu-id="409bb-169">Get the application's client ID</span></span>
1. <span data-ttu-id="409bb-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="409bb-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="409bb-172">From the **active directory** list, select your directory.</span><span class="sxs-lookup"><span data-stu-id="409bb-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="409bb-173">In the menu on the top, click **Applications**.</span><span class="sxs-lookup"><span data-stu-id="409bb-173">In the menu on the top, click **Applications**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="409bb-175">In the applications list, select your newly created application.</span><span class="sxs-lookup"><span data-stu-id="409bb-175">In the applications list, select your newly created application.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="409bb-177">In the menu on the top, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="409bb-177">In the menu on the top, click **Configure**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="409bb-179">Copy your **Client ID**.</span><span class="sxs-lookup"><span data-stu-id="409bb-179">Copy your **Client ID**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="409bb-181">Get the application's client secret</span><span class="sxs-lookup"><span data-stu-id="409bb-181">Get the application's client secret</span></span>
<span data-ttu-id="409bb-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span><span class="sxs-lookup"><span data-stu-id="409bb-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="409bb-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="409bb-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="409bb-185">From the **active directory** list, select your directory.</span><span class="sxs-lookup"><span data-stu-id="409bb-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="409bb-186">In the menu on the top, click **Applications**.</span><span class="sxs-lookup"><span data-stu-id="409bb-186">In the menu on the top, click **Applications**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="409bb-188">In the applications list, select your newly created application.</span><span class="sxs-lookup"><span data-stu-id="409bb-188">In the applications list, select your newly created application.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="409bb-190">In the menu on the top, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="409bb-190">In the menu on the top, click **Configure**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="409bb-192">In the **Keys** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="409bb-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="409bb-194">a.</span><span class="sxs-lookup"><span data-stu-id="409bb-194">a.</span></span> <span data-ttu-id="409bb-195">From the duration list, select a duration</span><span class="sxs-lookup"><span data-stu-id="409bb-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="409bb-196">b.</span><span class="sxs-lookup"><span data-stu-id="409bb-196">b.</span></span> <span data-ttu-id="409bb-197">On the bottom bar, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="409bb-197">On the bottom bar, click **Save**.</span></span>
   
    ![Register application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="409bb-199">c.</span><span class="sxs-lookup"><span data-stu-id="409bb-199">c.</span></span> <span data-ttu-id="409bb-200">Copy the key value.</span><span class="sxs-lookup"><span data-stu-id="409bb-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="409bb-201">Next Steps</span><span class="sxs-lookup"><span data-stu-id="409bb-201">Next Steps</span></span>
* <span data-ttu-id="409bb-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span><span class="sxs-lookup"><span data-stu-id="409bb-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="409bb-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="409bb-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="409bb-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="409bb-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  



























