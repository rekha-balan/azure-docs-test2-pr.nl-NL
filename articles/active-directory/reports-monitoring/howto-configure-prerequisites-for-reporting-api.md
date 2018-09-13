---
title: Prerequisites to access the Azure Active Directory reporting API | Microsoft Docs
description: Learn about the prerequisites to access the Azure AD reporting API
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 05/07/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 8d610dc74b7e2ef10295bc0a3407cf7c3d781b51
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969334"
---
# <a name="prerequisites-to-access-the-azure-active-directory-reporting-api"></a><span data-ttu-id="b21ee-103">Prerequisites to access the Azure Active Directory reporting API</span><span class="sxs-lookup"><span data-stu-id="b21ee-103">Prerequisites to access the Azure Active Directory reporting API</span></span>

<span data-ttu-id="b21ee-104">The [Azure Active Directory (Azure AD) reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span><span class="sxs-lookup"><span data-stu-id="b21ee-104">The [Azure Active Directory (Azure AD) reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="b21ee-105">You can call these APIs from a variety of programming languages and tools.</span><span class="sxs-lookup"><span data-stu-id="b21ee-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="b21ee-106">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span><span class="sxs-lookup"><span data-stu-id="b21ee-106">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span>

<span data-ttu-id="b21ee-107">To prepare your access to the reporting API, you need to:</span><span class="sxs-lookup"><span data-stu-id="b21ee-107">To prepare your access to the reporting API, you need to:</span></span>

1. <span data-ttu-id="b21ee-108">Assign roles</span><span class="sxs-lookup"><span data-stu-id="b21ee-108">Assign roles</span></span>
2. <span data-ttu-id="b21ee-109">Register an application</span><span class="sxs-lookup"><span data-stu-id="b21ee-109">Register an application</span></span>
3. <span data-ttu-id="b21ee-110">Grant permissions</span><span class="sxs-lookup"><span data-stu-id="b21ee-110">Grant permissions</span></span>
4. <span data-ttu-id="b21ee-111">Gather configuration settings</span><span class="sxs-lookup"><span data-stu-id="b21ee-111">Gather configuration settings</span></span>



## <a name="assign-roles"></a><span data-ttu-id="b21ee-112">Assign roles</span><span class="sxs-lookup"><span data-stu-id="b21ee-112">Assign roles</span></span>

<span data-ttu-id="b21ee-113">To get access to the reporting data through the API, you need to have one of the following roles assigned:</span><span class="sxs-lookup"><span data-stu-id="b21ee-113">To get access to the reporting data through the API, you need to have one of the following roles assigned:</span></span>

- <span data-ttu-id="b21ee-114">Security Reader</span><span class="sxs-lookup"><span data-stu-id="b21ee-114">Security Reader</span></span>

- <span data-ttu-id="b21ee-115">Security Admin</span><span class="sxs-lookup"><span data-stu-id="b21ee-115">Security Admin</span></span>

- <span data-ttu-id="b21ee-116">Global Admin</span><span class="sxs-lookup"><span data-stu-id="b21ee-116">Global Admin</span></span>




## <a name="register-an-application"></a><span data-ttu-id="b21ee-117">Register an application</span><span class="sxs-lookup"><span data-stu-id="b21ee-117">Register an application</span></span>

<span data-ttu-id="b21ee-118">You need to register an app even if you're accessing the reporting API using a script.</span><span class="sxs-lookup"><span data-stu-id="b21ee-118">You need to register an app even if you're accessing the reporting API using a script.</span></span> <span data-ttu-id="b21ee-119">This gives you an **Application ID**, which is required for an authorization call and it enables your code to receive tokens.</span><span class="sxs-lookup"><span data-stu-id="b21ee-119">This gives you an **Application ID**, which is required for an authorization call and it enables your code to receive tokens.</span></span>

<span data-ttu-id="b21ee-120">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure portal with an Azure administrator account that is also a member of the **Global Administrator** directory role in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="b21ee-120">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure portal with an Azure administrator account that is also a member of the **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b21ee-121">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span><span class="sxs-lookup"><span data-stu-id="b21ee-121">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="b21ee-122">**To register an Azure Active Directory application:**</span><span class="sxs-lookup"><span data-stu-id="b21ee-122">**To register an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="b21ee-123">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-123">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Azure Active Directory**.</span></span>
   
    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/01.png) 

2. <span data-ttu-id="b21ee-125">On the **Azure Active Directory** page, click **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-125">On the **Azure Active Directory** page, click **App registrations**.</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/02.png) 

3. <span data-ttu-id="b21ee-127">On the **App registrations** page, in the toolbar on the top, click **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-127">On the **App registrations** page, in the toolbar on the top, click **New application registration**.</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/03.png)

4. <span data-ttu-id="b21ee-129">On the **Create** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b21ee-129">On the **Create** page, perform the following steps:</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/04.png)

    <span data-ttu-id="b21ee-131">a.</span><span class="sxs-lookup"><span data-stu-id="b21ee-131">a.</span></span> <span data-ttu-id="b21ee-132">In the **Name** textbox, type `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="b21ee-132">In the **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="b21ee-133">b.</span><span class="sxs-lookup"><span data-stu-id="b21ee-133">b.</span></span> <span data-ttu-id="b21ee-134">As **Application type**, select **Web app / API**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-134">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="b21ee-135">c.</span><span class="sxs-lookup"><span data-stu-id="b21ee-135">c.</span></span> <span data-ttu-id="b21ee-136">In the **Sign-on URL** textbox, type `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="b21ee-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="b21ee-137">d.</span><span class="sxs-lookup"><span data-stu-id="b21ee-137">d.</span></span> <span data-ttu-id="b21ee-138">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-138">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="b21ee-139">Grant permissions</span><span class="sxs-lookup"><span data-stu-id="b21ee-139">Grant permissions</span></span> 

<span data-ttu-id="b21ee-140">Depending on API you want to access, you need to grant your app the following permissions:</span><span class="sxs-lookup"><span data-stu-id="b21ee-140">Depending on API you want to access, you need to grant your app the following permissions:</span></span>  

| <span data-ttu-id="b21ee-141">API</span><span class="sxs-lookup"><span data-stu-id="b21ee-141">API</span></span> | <span data-ttu-id="b21ee-142">Permission</span><span class="sxs-lookup"><span data-stu-id="b21ee-142">Permission</span></span> |
| --- | --- |
| <span data-ttu-id="b21ee-143">Windows Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b21ee-143">Windows Azure Active Directory</span></span> | <span data-ttu-id="b21ee-144">Read directory data</span><span class="sxs-lookup"><span data-stu-id="b21ee-144">Read directory data</span></span> |
| <span data-ttu-id="b21ee-145">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="b21ee-145">Microsoft Graph</span></span> | <span data-ttu-id="b21ee-146">Read all audit log data</span><span class="sxs-lookup"><span data-stu-id="b21ee-146">Read all audit log data</span></span> |


![Register application](./media/howto-configure-prerequisites-for-reporting-api/36.png)


<span data-ttu-id="b21ee-148">The following section lists the steps for both APIs.</span><span class="sxs-lookup"><span data-stu-id="b21ee-148">The following section lists the steps for both APIs.</span></span> <span data-ttu-id="b21ee-149">If you don't want to access one of the APIs, you can skip the related steps.</span><span class="sxs-lookup"><span data-stu-id="b21ee-149">If you don't want to access one of the APIs, you can skip the related steps.</span></span>
 

<span data-ttu-id="b21ee-150">**To grant your application permissions to use the APIs:**</span><span class="sxs-lookup"><span data-stu-id="b21ee-150">**To grant your application permissions to use the APIs:**</span></span>

1. <span data-ttu-id="b21ee-151">On the **App registrations** page, in the apps list, click **Reporting API application**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-151">On the **App registrations** page, in the apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="b21ee-152">On the **Reporting API application** page, in the toolbar on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-152">On the **Reporting API application** page, in the toolbar on the top, click **Settings**.</span></span> 

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/05.png)

3. <span data-ttu-id="b21ee-154">On the **Settings** page, click **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-154">On the **Settings** page, click **Required permissions**.</span></span> 

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/06.png)

4. <span data-ttu-id="b21ee-156">On the **Required permissions** page, in the **API** list, click **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-156">On the **Required permissions** page, in the **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/07.png)

5. <span data-ttu-id="b21ee-158">On the **Enable Access** page, select **Read directory data** and, deselect **Sign in and read user profile**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-158">On the **Enable Access** page, select **Read directory data** and, deselect **Sign in and read user profile**.</span></span> 

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/08.png)

6. <span data-ttu-id="b21ee-160">In the toolbar on the top, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-160">In the toolbar on the top, click **Save**.</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/15.png)

7. <span data-ttu-id="b21ee-162">On the **Required permissions** page, in the toolbar on the top, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-162">On the **Required permissions** page, in the toolbar on the top, click **Add**.</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/32.png)

8. <span data-ttu-id="b21ee-164">On the **Add API access** page, click **Select an API**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-164">On the **Add API access** page, click **Select an API**.</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/31.png)

9. <span data-ttu-id="b21ee-166">On the **Select an API** page, click **Microsoft Graph**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-166">On the **Select an API** page, click **Microsoft Graph**, and then click **Select**.</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/33.png)

10. <span data-ttu-id="b21ee-168">On the **Enable Access** page, select **Read all audit log data**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-168">On the **Enable Access** page, select **Read all audit log data**, and then click **Select**.</span></span>  

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/34.png)


11. <span data-ttu-id="b21ee-170">On the **Add API access** page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-170">On the **Add API access** page, click **Done**.</span></span>  

12. <span data-ttu-id="b21ee-171">On the **Required permissions** page, in the toolbar on the top.</span><span class="sxs-lookup"><span data-stu-id="b21ee-171">On the **Required permissions** page, in the toolbar on the top.</span></span> <span data-ttu-id="b21ee-172">click **Grant Permissions**, and then click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-172">click **Grant Permissions**, and then click **Yes**.</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/17.png)


## <a name="gather-configuration-settings"></a><span data-ttu-id="b21ee-174">Gather configuration settings</span><span class="sxs-lookup"><span data-stu-id="b21ee-174">Gather configuration settings</span></span> 

<span data-ttu-id="b21ee-175">This section shows you how to get the following settings from your directory:</span><span class="sxs-lookup"><span data-stu-id="b21ee-175">This section shows you how to get the following settings from your directory:</span></span>

- <span data-ttu-id="b21ee-176">Domain name</span><span class="sxs-lookup"><span data-stu-id="b21ee-176">Domain name</span></span>
- <span data-ttu-id="b21ee-177">Client ID</span><span class="sxs-lookup"><span data-stu-id="b21ee-177">Client ID</span></span>
- <span data-ttu-id="b21ee-178">Client secret</span><span class="sxs-lookup"><span data-stu-id="b21ee-178">Client secret</span></span>

<span data-ttu-id="b21ee-179">You need these values when configuring calls to the reporting API.</span><span class="sxs-lookup"><span data-stu-id="b21ee-179">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="b21ee-180">Get your domain name</span><span class="sxs-lookup"><span data-stu-id="b21ee-180">Get your domain name</span></span>

<span data-ttu-id="b21ee-181">**To get your domain name:**</span><span class="sxs-lookup"><span data-stu-id="b21ee-181">**To get your domain name:**</span></span>

1. <span data-ttu-id="b21ee-182">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-182">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Azure Active Directory**.</span></span>
   
    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/01.png) 

2. <span data-ttu-id="b21ee-184">On the **Azure Active Directory** page, click **Custom domain names**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-184">On the **Azure Active Directory** page, click **Custom domain names**.</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/09.png) 

3. <span data-ttu-id="b21ee-186">Copy your domain name from the list of domains.</span><span class="sxs-lookup"><span data-stu-id="b21ee-186">Copy your domain name from the list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="b21ee-187">Get your application's client ID</span><span class="sxs-lookup"><span data-stu-id="b21ee-187">Get your application's client ID</span></span>

<span data-ttu-id="b21ee-188">**To get your application's client ID:**</span><span class="sxs-lookup"><span data-stu-id="b21ee-188">**To get your application's client ID:**</span></span>

1. <span data-ttu-id="b21ee-189">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-189">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Azure Active Directory**.</span></span>
   
    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/01.png) 

2. <span data-ttu-id="b21ee-191">On the **App registrations** page, in the apps list, click **Reporting API application**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-191">On the **App registrations** page, in the apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="b21ee-192">On the **Reporting API application** page, at the **Application ID**, click **Click to copy**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-192">On the **Reporting API application** page, at the **Application ID**, click **Click to copy**.</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="b21ee-194">Get your application's client secret</span><span class="sxs-lookup"><span data-stu-id="b21ee-194">Get your application's client secret</span></span>
<span data-ttu-id="b21ee-195">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span><span class="sxs-lookup"><span data-stu-id="b21ee-195">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

<span data-ttu-id="b21ee-196">**To get your application's client secret:**</span><span class="sxs-lookup"><span data-stu-id="b21ee-196">**To get your application's client secret:**</span></span>

1. <span data-ttu-id="b21ee-197">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-197">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Azure Active Directory**.</span></span>
   
    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/01.png) 

2. <span data-ttu-id="b21ee-199">On the **App registrations** page, in the apps list, click **Reporting API application**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-199">On the **App registrations** page, in the apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="b21ee-200">On the **Reporting API application** page, in the toolbar on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-200">On the **Reporting API application** page, in the toolbar on the top, click **Settings**.</span></span> 

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/05.png)

4. <span data-ttu-id="b21ee-202">On the **Settings** page, in the **APIR Access** section, click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-202">On the **Settings** page, in the **APIR Access** section, click **Keys**.</span></span> 

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/12.png)


5. <span data-ttu-id="b21ee-204">On the **Keys** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b21ee-204">On the **Keys** page, perform the following steps:</span></span>

    ![Register application](./media/howto-configure-prerequisites-for-reporting-api/14.png)

    <span data-ttu-id="b21ee-206">a.</span><span class="sxs-lookup"><span data-stu-id="b21ee-206">a.</span></span> <span data-ttu-id="b21ee-207">In the **Description** textbox, type `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="b21ee-207">In the **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="b21ee-208">b.</span><span class="sxs-lookup"><span data-stu-id="b21ee-208">b.</span></span> <span data-ttu-id="b21ee-209">As **Expires**, select **In 2 years**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-209">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="b21ee-210">c.</span><span class="sxs-lookup"><span data-stu-id="b21ee-210">c.</span></span> <span data-ttu-id="b21ee-211">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b21ee-211">Click **Save**.</span></span>

    <span data-ttu-id="b21ee-212">d.</span><span class="sxs-lookup"><span data-stu-id="b21ee-212">d.</span></span> <span data-ttu-id="b21ee-213">Copy the key value.</span><span class="sxs-lookup"><span data-stu-id="b21ee-213">Copy the key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b21ee-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="b21ee-214">Next steps</span></span>

* [<span data-ttu-id="b21ee-215">Get data using the Azure Active Directory reporting API with certificates</span><span class="sxs-lookup"><span data-stu-id="b21ee-215">Get data using the Azure Active Directory reporting API with certificates</span></span>](tutorial-access-api-with-certificates.md)
* [<span data-ttu-id="b21ee-216">Get a first impression of the reporting APIs</span><span class="sxs-lookup"><span data-stu-id="b21ee-216">Get a first impression of the reporting APIs</span></span>](concept-reporting-api.md)
* [<span data-ttu-id="b21ee-217">Audit API reference</span><span class="sxs-lookup"><span data-stu-id="b21ee-217">Audit API reference</span></span>](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/directoryaudit) 
* [<span data-ttu-id="b21ee-218">Sign-in activity report API reference</span><span class="sxs-lookup"><span data-stu-id="b21ee-218">Sign-in activity report API reference</span></span>](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/signin)
