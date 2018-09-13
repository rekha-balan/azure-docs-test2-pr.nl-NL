---
title: Configure Deployment Sources for App Services on Azure Stack | Microsoft Docs
description: How a Service Administrator can configure deployment sources (Git, GitHub, BitBucket, DropBox and OneDrive) for App Service on Azure Stack
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: a324c4ad30c8763d62ce2b30f8173ae416e4def5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563133"
---
# <a name="configure-deployment-sources"></a><span data-ttu-id="14819-103">Configure deployment sources</span><span class="sxs-lookup"><span data-stu-id="14819-103">Configure deployment sources</span></span>

<span data-ttu-id="14819-104">App Service on Azure Stack supports on-demand deployment from multiple Source Control Providers.</span><span class="sxs-lookup"><span data-stu-id="14819-104">App Service on Azure Stack supports on-demand deployment from multiple Source Control Providers.</span></span>  <span data-ttu-id="14819-105">This feature enables application developers to be able to deploy direct from their source control repositories.</span><span class="sxs-lookup"><span data-stu-id="14819-105">This feature enables application developers to be able to deploy direct from their source control repositories.</span></span>  <span data-ttu-id="14819-106">In order for tenants to be able to configure App Service to connect to their repositories, Administrators must first configure the integration between App Service on Azure Stack and the Source Control Provider.</span><span class="sxs-lookup"><span data-stu-id="14819-106">In order for tenants to be able to configure App Service to connect to their repositories, Administrators must first configure the integration between App Service on Azure Stack and the Source Control Provider.</span></span>  <span data-ttu-id="14819-107">The Source Control Providers supported, in addition to local Git, are:</span><span class="sxs-lookup"><span data-stu-id="14819-107">The Source Control Providers supported, in addition to local Git, are:</span></span>

* <span data-ttu-id="14819-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="14819-108">GitHub</span></span>
* <span data-ttu-id="14819-109">BitBucket</span><span class="sxs-lookup"><span data-stu-id="14819-109">BitBucket</span></span>
* <span data-ttu-id="14819-110">OneDrive</span><span class="sxs-lookup"><span data-stu-id="14819-110">OneDrive</span></span>
* <span data-ttu-id="14819-111">DropBox</span><span class="sxs-lookup"><span data-stu-id="14819-111">DropBox</span></span>

## <a name="view-deployment-sources-in-app-service-administration"></a><span data-ttu-id="14819-112">View Deployment Sources in App Service Administration</span><span class="sxs-lookup"><span data-stu-id="14819-112">View Deployment Sources in App Service Administration</span></span>

1. <span data-ttu-id="14819-113">Log in to the Azure Stack portal as the service administrator.</span><span class="sxs-lookup"><span data-stu-id="14819-113">Log in to the Azure Stack portal as the service administrator.</span></span>
2. <span data-ttu-id="14819-114">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.  ![App Service Resource Provider Admin][1]</span><span class="sxs-lookup"><span data-stu-id="14819-114">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.  ![App Service Resource Provider Admin][1]</span></span>
3. <span data-ttu-id="14819-115">Click **Source control configuration**.</span><span class="sxs-lookup"><span data-stu-id="14819-115">Click **Source control configuration**.</span></span>  <span data-ttu-id="14819-116">Here you see the list of all Deployment Sources configured.</span><span class="sxs-lookup"><span data-stu-id="14819-116">Here you see the list of all Deployment Sources configured.</span></span>
    <span data-ttu-id="14819-117">![App Service Resource Provider Admin Source Control Configuration][2]</span><span class="sxs-lookup"><span data-stu-id="14819-117">![App Service Resource Provider Admin Source Control Configuration][2]</span></span>

## <a name="configure-github"></a><span data-ttu-id="14819-118">Configure GitHub</span><span class="sxs-lookup"><span data-stu-id="14819-118">Configure GitHub</span></span>

> [!NOTE]
> <span data-ttu-id="14819-119">You require a GitHub account to complete this task.</span><span class="sxs-lookup"><span data-stu-id="14819-119">You require a GitHub account to complete this task.</span></span>  <span data-ttu-id="14819-120">You may wish to use an account for your organization rather than a personal account.</span><span class="sxs-lookup"><span data-stu-id="14819-120">You may wish to use an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="14819-121">Log in to GitHub, browse to https://www.github.com/settings/developers and click **Register a new application** ![GitHub - Register a new application][3]</span><span class="sxs-lookup"><span data-stu-id="14819-121">Log in to GitHub, browse to https://www.github.com/settings/developers and click **Register a new application** ![GitHub - Register a new application][3]</span></span>
2. <span data-ttu-id="14819-122">Enter an **Application name** for example - App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="14819-122">Enter an **Application name** for example - App Service on Azure Stack</span></span>
3. <span data-ttu-id="14819-123">Enter the **Homepage URL**.</span><span class="sxs-lookup"><span data-stu-id="14819-123">Enter the **Homepage URL**.</span></span>  <span data-ttu-id="14819-124">**The Homepage URL must be the Azure Stack Portal address** for example - https://portal.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="14819-124">**The Homepage URL must be the Azure Stack Portal address** for example - https://portal.azurestack.local</span></span>
4. <span data-ttu-id="14819-125">Enter an **Application Description**</span><span class="sxs-lookup"><span data-stu-id="14819-125">Enter an **Application Description**</span></span>
5. <span data-ttu-id="14819-126">Enter the **Authorization callback URL**.</span><span class="sxs-lookup"><span data-stu-id="14819-126">Enter the **Authorization callback URL**.</span></span>  <span data-ttu-id="14819-127">In a default Azure Stack deployment, the Url is in the form https://portal.azurestack.local/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![GitHub - Register a new application with values populated][4]</span><span class="sxs-lookup"><span data-stu-id="14819-127">In a default Azure Stack deployment, the Url is in the form https://portal.azurestack.local/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![GitHub - Register a new application with values populated][4]</span></span>
6. <span data-ttu-id="14819-128">Click **Register application**.</span><span class="sxs-lookup"><span data-stu-id="14819-128">Click **Register application**.</span></span>  <span data-ttu-id="14819-129">You will now be presented with a page listing the **Client ID** and **Client Secret** for the application.</span><span class="sxs-lookup"><span data-stu-id="14819-129">You will now be presented with a page listing the **Client ID** and **Client Secret** for the application.</span></span>
    <span data-ttu-id="14819-130">![GitHub - Completed application registration][5]</span><span class="sxs-lookup"><span data-stu-id="14819-130">![GitHub - Completed application registration][5]</span></span>
7.  <span data-ttu-id="14819-131">In a new browser tab or window Log in to the Azure Stack Portal as the service administrator.</span><span class="sxs-lookup"><span data-stu-id="14819-131">In a new browser tab or window Log in to the Azure Stack Portal as the service administrator.</span></span> 
8.  <span data-ttu-id="14819-132">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span><span class="sxs-lookup"><span data-stu-id="14819-132">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span> 
9. <span data-ttu-id="14819-133">Click **Source control configuration**.</span><span class="sxs-lookup"><span data-stu-id="14819-133">Click **Source control configuration**.</span></span>
10. <span data-ttu-id="14819-134">Copy and paste the **Client Id** and **Client Secret** into the corresponding input boxes for GitHub.</span><span class="sxs-lookup"><span data-stu-id="14819-134">Copy and paste the **Client Id** and **Client Secret** into the corresponding input boxes for GitHub.</span></span>
11. <span data-ttu-id="14819-135">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14819-135">Click **Save**.</span></span>
12. <span data-ttu-id="14819-136">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span><span class="sxs-lookup"><span data-stu-id="14819-136">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>


## <a name="configure-bitbucket"></a><span data-ttu-id="14819-137">Configure BitBucket</span><span class="sxs-lookup"><span data-stu-id="14819-137">Configure BitBucket</span></span>

> [!NOTE]
> <span data-ttu-id="14819-138">You require a BitBucket account to complete this task.</span><span class="sxs-lookup"><span data-stu-id="14819-138">You require a BitBucket account to complete this task.</span></span>  <span data-ttu-id="14819-139">You may wish to use an account for your organization rather than a personal account.</span><span class="sxs-lookup"><span data-stu-id="14819-139">You may wish to use an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="14819-140">Log in to BitBucket and browse to **Integrations** under your account  ![BitBucket Dashboard - Integrations][7]</span><span class="sxs-lookup"><span data-stu-id="14819-140">Log in to BitBucket and browse to **Integrations** under your account  ![BitBucket Dashboard - Integrations][7]</span></span>
2. <span data-ttu-id="14819-141">Click **OAuth** under Access Management and **Add consumer** ![BitBucket Add OAuth Consumer][8]</span><span class="sxs-lookup"><span data-stu-id="14819-141">Click **OAuth** under Access Management and **Add consumer** ![BitBucket Add OAuth Consumer][8]</span></span>
3. <span data-ttu-id="14819-142">Enter a **Name** for the consumer, for example App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="14819-142">Enter a **Name** for the consumer, for example App Service on Azure Stack</span></span>
4. <span data-ttu-id="14819-143">Enter a **Description** for the application</span><span class="sxs-lookup"><span data-stu-id="14819-143">Enter a **Description** for the application</span></span>
5. <span data-ttu-id="14819-144">Enter the **Callback URL**.</span><span class="sxs-lookup"><span data-stu-id="14819-144">Enter the **Callback URL**.</span></span>  <span data-ttu-id="14819-145">In a default Azure Stack deployment, the Callback Url is in the form https://portal.azurestack.local/TokenAuthorize, if you are running under a different domain substitute your domain for azurestack.local.</span><span class="sxs-lookup"><span data-stu-id="14819-145">In a default Azure Stack deployment, the Callback Url is in the form https://portal.azurestack.local/TokenAuthorize, if you are running under a different domain substitute your domain for azurestack.local.</span></span>  <span data-ttu-id="14819-146">The Url must follow the capitalization as listed here for BitBucket integration to succeed.</span><span class="sxs-lookup"><span data-stu-id="14819-146">The Url must follow the capitalization as listed here for BitBucket integration to succeed.</span></span>
6. <span data-ttu-id="14819-147">Enter the **URL** - this Url should be the Azure Stack Portal URL, for example https://portal.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="14819-147">Enter the **URL** - this Url should be the Azure Stack Portal URL, for example https://portal.azurestack.local</span></span>
7. <span data-ttu-id="14819-148">Select the **Permissions** required  **Repositories**: **Read** **Webhooks**: **Read and write**</span><span class="sxs-lookup"><span data-stu-id="14819-148">Select the **Permissions** required  **Repositories**: **Read** **Webhooks**: **Read and write**</span></span>
8. <span data-ttu-id="14819-149">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14819-149">Click **Save**.</span></span>  <span data-ttu-id="14819-150">You will now see this new application, along with the **Key** and **Secret** under **OAuth consumers**.</span><span class="sxs-lookup"><span data-stu-id="14819-150">You will now see this new application, along with the **Key** and **Secret** under **OAuth consumers**.</span></span>
    <span data-ttu-id="14819-151">![BitBucket Application Listing][9]</span><span class="sxs-lookup"><span data-stu-id="14819-151">![BitBucket Application Listing][9]</span></span>
9.  <span data-ttu-id="14819-152">In a new browser tab or window Log in to the Azure Stack Portal as the service administrator.</span><span class="sxs-lookup"><span data-stu-id="14819-152">In a new browser tab or window Log in to the Azure Stack Portal as the service administrator.</span></span> 
10.  <span data-ttu-id="14819-153">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span><span class="sxs-lookup"><span data-stu-id="14819-153">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span> 
11. <span data-ttu-id="14819-154">Click **Source control configuration**.</span><span class="sxs-lookup"><span data-stu-id="14819-154">Click **Source control configuration**.</span></span>
12. <span data-ttu-id="14819-155">Copy and paste the **Key** into the **Client Id** input box and **Secret** into the **Client Secret** input box for BitBucket.</span><span class="sxs-lookup"><span data-stu-id="14819-155">Copy and paste the **Key** into the **Client Id** input box and **Secret** into the **Client Secret** input box for BitBucket.</span></span>
13. <span data-ttu-id="14819-156">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14819-156">Click **Save**.</span></span>
14. <span data-ttu-id="14819-157">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span><span class="sxs-lookup"><span data-stu-id="14819-157">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>

## <a name="configure-onedrive"></a><span data-ttu-id="14819-158">Configure OneDrive</span><span class="sxs-lookup"><span data-stu-id="14819-158">Configure OneDrive</span></span>

> [!NOTE]
> <span data-ttu-id="14819-159">OneDrive for Business Accounts are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="14819-159">OneDrive for Business Accounts are not currently supported.</span></span>  <span data-ttu-id="14819-160">You need to have a Microsoft Account linked to a OneDrive account to complete this task.</span><span class="sxs-lookup"><span data-stu-id="14819-160">You need to have a Microsoft Account linked to a OneDrive account to complete this task.</span></span>  <span data-ttu-id="14819-161">You may wish to use an account for your organization rather than a personal account.</span><span class="sxs-lookup"><span data-stu-id="14819-161">You may wish to use an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="14819-162">Browse to https://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm and Log in using your Microsoft Account.</span><span class="sxs-lookup"><span data-stu-id="14819-162">Browse to https://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm and Log in using your Microsoft Account.</span></span>
2. <span data-ttu-id="14819-163">Click **Add an app** under **My applications**
![OneDrive Applications][10]</span><span class="sxs-lookup"><span data-stu-id="14819-163">Click **Add an app** under **My applications**
![OneDrive Applications][10]</span></span>
3. <span data-ttu-id="14819-164">Enter a **Name** for the New Application Registration, enter **App Service on Azure Stack**, and click **Create Application**</span><span class="sxs-lookup"><span data-stu-id="14819-164">Enter a **Name** for the New Application Registration, enter **App Service on Azure Stack**, and click **Create Application**</span></span>
4. <span data-ttu-id="14819-165">The next screen lists the properties of your new application.</span><span class="sxs-lookup"><span data-stu-id="14819-165">The next screen lists the properties of your new application.</span></span> <span data-ttu-id="14819-166">Record the **Application Id**
![OneDrive Application Properties][11]</span><span class="sxs-lookup"><span data-stu-id="14819-166">Record the **Application Id**
![OneDrive Application Properties][11]</span></span>
5. <span data-ttu-id="14819-167">Under **Application Secrets** click **Generate New Password** and record the **New password generated** - this is your application secret.</span><span class="sxs-lookup"><span data-stu-id="14819-167">Under **Application Secrets** click **Generate New Password** and record the **New password generated** - this is your application secret.</span></span>
> [!NOTE]
> <span data-ttu-id="14819-168">Make sure to make a note of the new password as it is not retrievable once you click OK at this stage.</span><span class="sxs-lookup"><span data-stu-id="14819-168">Make sure to make a note of the new password as it is not retrievable once you click OK at this stage.</span></span>
6. <span data-ttu-id="14819-169">Under **Platforms** click **Add Platform** and select **Web**</span><span class="sxs-lookup"><span data-stu-id="14819-169">Under **Platforms** click **Add Platform** and select **Web**</span></span>
7. <span data-ttu-id="14819-170">Enter the **Redirect URI**.</span><span class="sxs-lookup"><span data-stu-id="14819-170">Enter the **Redirect URI**.</span></span>  <span data-ttu-id="14819-171">In a default Azure Stack deployment, the Redirect URI is in the form https://portal.azurestack.local/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![OneDrive Application - Add Web Platform][12]</span><span class="sxs-lookup"><span data-stu-id="14819-171">In a default Azure Stack deployment, the Redirect URI is in the form https://portal.azurestack.local/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![OneDrive Application - Add Web Platform][12]</span></span>
8. <span data-ttu-id="14819-172">Set the **Microsoft Graph Permissions** - **Delegated Permissions**</span><span class="sxs-lookup"><span data-stu-id="14819-172">Set the **Microsoft Graph Permissions** - **Delegated Permissions**</span></span>
    - <span data-ttu-id="14819-173">**Files.ReadWrite.AppFolder**</span><span class="sxs-lookup"><span data-stu-id="14819-173">**Files.ReadWrite.AppFolder**</span></span>
    - <span data-ttu-id="14819-174">**User.Read**</span><span class="sxs-lookup"><span data-stu-id="14819-174">**User.Read**</span></span>  
      <span data-ttu-id="14819-175">![OneDrive Application - Graph Permissions][13]</span><span class="sxs-lookup"><span data-stu-id="14819-175">![OneDrive Application - Graph Permissions][13]</span></span>
10. <span data-ttu-id="14819-176">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14819-176">Click **Save**.</span></span>
11.  <span data-ttu-id="14819-177">In a new browser tab or window Log in to the Azure Stack Portal as the service administrator.</span><span class="sxs-lookup"><span data-stu-id="14819-177">In a new browser tab or window Log in to the Azure Stack Portal as the service administrator.</span></span> 
12.  <span data-ttu-id="14819-178">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span><span class="sxs-lookup"><span data-stu-id="14819-178">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span> 
13. <span data-ttu-id="14819-179">Click **Source control configuration**.</span><span class="sxs-lookup"><span data-stu-id="14819-179">Click **Source control configuration**.</span></span>
14. <span data-ttu-id="14819-180">Copy and paste the **Application Id** into the **Client Id** input box and **Password** into the **Client Secret** input box for OneDrive.</span><span class="sxs-lookup"><span data-stu-id="14819-180">Copy and paste the **Application Id** into the **Client Id** input box and **Password** into the **Client Secret** input box for OneDrive.</span></span>
15. <span data-ttu-id="14819-181">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14819-181">Click **Save**.</span></span>
16. <span data-ttu-id="14819-182">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span><span class="sxs-lookup"><span data-stu-id="14819-182">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>

## <a name="configure-dropbox"></a><span data-ttu-id="14819-183">Configure DropBox</span><span class="sxs-lookup"><span data-stu-id="14819-183">Configure DropBox</span></span>

> [!NOTE]
> <span data-ttu-id="14819-184">You need to have a DropBox account to complete this task.</span><span class="sxs-lookup"><span data-stu-id="14819-184">You need to have a DropBox account to complete this task.</span></span>  <span data-ttu-id="14819-185">You may wish to use an account for your organization rather than a personal account.</span><span class="sxs-lookup"><span data-stu-id="14819-185">You may wish to use an account for your organization rather than a personal account.</span></span>

1. <span data-ttu-id="14819-186">Browse to https://www.dropbox.com/developers/apps and Log in using your DropBox Account</span><span class="sxs-lookup"><span data-stu-id="14819-186">Browse to https://www.dropbox.com/developers/apps and Log in using your DropBox Account</span></span>
2. <span data-ttu-id="14819-187">Click **Create app** 
![Dropbox applications][14]</span><span class="sxs-lookup"><span data-stu-id="14819-187">Click **Create app** 
![Dropbox applications][14]</span></span>
3. <span data-ttu-id="14819-188">Select **DropBox API**</span><span class="sxs-lookup"><span data-stu-id="14819-188">Select **DropBox API**</span></span>
4. <span data-ttu-id="14819-189">Set the access level to **App Folder**</span><span class="sxs-lookup"><span data-stu-id="14819-189">Set the access level to **App Folder**</span></span>
5. <span data-ttu-id="14819-190">Enter a **Name** for your application.</span><span class="sxs-lookup"><span data-stu-id="14819-190">Enter a **Name** for your application.</span></span>
<span data-ttu-id="14819-191">![Dropbox application registration][15]</span><span class="sxs-lookup"><span data-stu-id="14819-191">![Dropbox application registration][15]</span></span>
6. <span data-ttu-id="14819-192">Click **Create App**.</span><span class="sxs-lookup"><span data-stu-id="14819-192">Click **Create App**.</span></span>  <span data-ttu-id="14819-193">You will now be presented with a page listing the settings for the App including **App key** and **App secret**.</span><span class="sxs-lookup"><span data-stu-id="14819-193">You will now be presented with a page listing the settings for the App including **App key** and **App secret**.</span></span>
7. <span data-ttu-id="14819-194">Check the **App folder name** is set to **App Service on Azure Stack**</span><span class="sxs-lookup"><span data-stu-id="14819-194">Check the **App folder name** is set to **App Service on Azure Stack**</span></span>
8. <span data-ttu-id="14819-195">Set the **OAuth 2 Redirect URI** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="14819-195">Set the **OAuth 2 Redirect URI** and click **Add**.</span></span>  <span data-ttu-id="14819-196">In a default Azure Stack deployment, the Redirect URI is in the form https://portal.azurestack.local/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![Dropbox application configuration][16]</span><span class="sxs-lookup"><span data-stu-id="14819-196">In a default Azure Stack deployment, the Redirect URI is in the form https://portal.azurestack.local/tokenauthorize, if you are running under a different domain substitute your domain for azurestack.local ![Dropbox application configuration][16]</span></span>
9.  <span data-ttu-id="14819-197">In a new browser tab or window Log in to the Azure Stack Portal as the service administrator.</span><span class="sxs-lookup"><span data-stu-id="14819-197">In a new browser tab or window Log in to the Azure Stack Portal as the service administrator.</span></span> 
10.  <span data-ttu-id="14819-198">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span><span class="sxs-lookup"><span data-stu-id="14819-198">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span> 
11. <span data-ttu-id="14819-199">Click **Source control configuration**.</span><span class="sxs-lookup"><span data-stu-id="14819-199">Click **Source control configuration**.</span></span>
12. <span data-ttu-id="14819-200">Copy and paste the **Application Key** into the **Client Id** input box and **App secret** into the **Client Secret** input box for DropBox.</span><span class="sxs-lookup"><span data-stu-id="14819-200">Copy and paste the **Application Key** into the **Client Id** input box and **App secret** into the **Client Secret** input box for DropBox.</span></span>
13. <span data-ttu-id="14819-201">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="14819-201">Click **Save**.</span></span>
14. <span data-ttu-id="14819-202">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span><span class="sxs-lookup"><span data-stu-id="14819-202">If you do not wish to configure any other Deployment Sources, proceed to [Schedule Repair of Management Roles](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).</span></span>

## <a name="schedule-repair-of-management-roles"></a><span data-ttu-id="14819-203">Schedule repair of management roles</span><span class="sxs-lookup"><span data-stu-id="14819-203">Schedule repair of management roles</span></span>
<span data-ttu-id="14819-204">In order for the settings updated in the configuration of the various deployment sources to be applied, the Management Roles need to be repaired.</span><span class="sxs-lookup"><span data-stu-id="14819-204">In order for the settings updated in the configuration of the various deployment sources to be applied, the Management Roles need to be repaired.</span></span>  <span data-ttu-id="14819-205">This process ensures that the configuration values are applied correctly and the configured Deployment Sources are made available to tenants.</span><span class="sxs-lookup"><span data-stu-id="14819-205">This process ensures that the configuration values are applied correctly and the configured Deployment Sources are made available to tenants.</span></span>

1. <span data-ttu-id="14819-206">In a new browser tab or window Log in to the Azure Stack Portal as the service administrator.</span><span class="sxs-lookup"><span data-stu-id="14819-206">In a new browser tab or window Log in to the Azure Stack Portal as the service administrator.</span></span>
2. <span data-ttu-id="14819-207">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span><span class="sxs-lookup"><span data-stu-id="14819-207">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span>
3. <span data-ttu-id="14819-208">Click **Source control configuration**</span><span class="sxs-lookup"><span data-stu-id="14819-208">Click **Source control configuration**</span></span>
4. <span data-ttu-id="14819-209">Copy and paste the **Client Id** and **Client Secret** into the corresponding input boxes for GitHub.</span><span class="sxs-lookup"><span data-stu-id="14819-209">Copy and paste the **Client Id** and **Client Secret** into the corresponding input boxes for GitHub.</span></span>
5. <span data-ttu-id="14819-210">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="14819-210">Click **Save**</span></span>
6. <span data-ttu-id="14819-211">Click **Roles**</span><span class="sxs-lookup"><span data-stu-id="14819-211">Click **Roles**</span></span>
7. <span data-ttu-id="14819-212">Click **Management Server**</span><span class="sxs-lookup"><span data-stu-id="14819-212">Click **Management Server**</span></span>
8. <span data-ttu-id="14819-213">Click **Repair All** and select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="14819-213">Click **Repair All** and select **Yes**.</span></span>  <span data-ttu-id="14819-214">This operation schedules a repair on all Management Servers to complete the integration.</span><span class="sxs-lookup"><span data-stu-id="14819-214">This operation schedules a repair on all Management Servers to complete the integration.</span></span>  <span data-ttu-id="14819-215">The repair operations are managed to minimize downtime.</span><span class="sxs-lookup"><span data-stu-id="14819-215">The repair operations are managed to minimize downtime.</span></span>
    <span data-ttu-id="14819-216">![App Service Resource Provider Admin - Roles - Management Server Repair All][6]</span><span class="sxs-lookup"><span data-stu-id="14819-216">![App Service Resource Provider Admin - Roles - Management Server Repair All][6]</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-source-control-configuration.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-developer-applications.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-populated.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-complete.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-roles-management-server-repair-all.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-dashboard.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer-complete.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-applications.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-registration.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-platform.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-graph-permissions.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-applications.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-registration.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-configuration.png
















