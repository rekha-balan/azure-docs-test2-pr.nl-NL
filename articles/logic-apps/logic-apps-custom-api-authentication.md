---
title: Add authentication to custom APIs - Azure Logic Apps | Microsoft Docs
description: Set up authentication for calling custom APIs from Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.topic: article
ms.date: 09/22/2017
ms.openlocfilehash: b329fb1416d28b0732e7b9ea4612f5bac8580b3a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857423"
---
# <a name="secure-calls-to-custom-apis-from-azure-logic-apps"></a><span data-ttu-id="b5e25-103">Secure calls to custom APIs from Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b5e25-103">Secure calls to custom APIs from Azure Logic Apps</span></span>

<span data-ttu-id="b5e25-104">To secure calls to your APIs, you can set up Azure Active Directory (Azure AD) authentication through the Azure portal so you don't have to update your code.</span><span class="sxs-lookup"><span data-stu-id="b5e25-104">To secure calls to your APIs, you can set up Azure Active Directory (Azure AD) authentication through the Azure portal so you don't have to update your code.</span></span> <span data-ttu-id="b5e25-105">Or, you can require and enforce authentication through your API's code.</span><span class="sxs-lookup"><span data-stu-id="b5e25-105">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="authentication-options-for-your-api"></a><span data-ttu-id="b5e25-106">Authentication options for your API</span><span class="sxs-lookup"><span data-stu-id="b5e25-106">Authentication options for your API</span></span>

<span data-ttu-id="b5e25-107">You can secure calls to your custom API in these ways:</span><span class="sxs-lookup"><span data-stu-id="b5e25-107">You can secure calls to your custom API in these ways:</span></span>

* <span data-ttu-id="b5e25-108">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/fundamentals/active-directory-whatis.md) through the Azure portal, so you don't have to update your code or redeploy your API.</span><span class="sxs-lookup"><span data-stu-id="b5e25-108">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/fundamentals/active-directory-whatis.md) through the Azure portal, so you don't have to update your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b5e25-109">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span><span class="sxs-lookup"><span data-stu-id="b5e25-109">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="b5e25-110">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span><span class="sxs-lookup"><span data-stu-id="b5e25-110">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

* <span data-ttu-id="b5e25-111">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span><span class="sxs-lookup"><span data-stu-id="b5e25-111">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a><span data-ttu-id="b5e25-112">Authenticate calls to your API without changing code</span><span class="sxs-lookup"><span data-stu-id="b5e25-112">Authenticate calls to your API without changing code</span></span>

<span data-ttu-id="b5e25-113">Here are the general steps for this method:</span><span class="sxs-lookup"><span data-stu-id="b5e25-113">Here are the general steps for this method:</span></span>

1. <span data-ttu-id="b5e25-114">Create two Azure Active Directory (Azure AD) application identities: one for your logic app and one for your web app (or API app).</span><span class="sxs-lookup"><span data-stu-id="b5e25-114">Create two Azure Active Directory (Azure AD) application identities: one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="b5e25-115">To authenticate calls to your API, use the credentials (client ID and secret) for the service principal that's associated with the Azure AD application identity for your logic app.</span><span class="sxs-lookup"><span data-stu-id="b5e25-115">To authenticate calls to your API, use the credentials (client ID and secret) for the service principal that's associated with the Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="b5e25-116">Include the application IDs in your logic app definition.</span><span class="sxs-lookup"><span data-stu-id="b5e25-116">Include the application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="b5e25-117">Part 1: Create an Azure AD application identity for your logic app</span><span class="sxs-lookup"><span data-stu-id="b5e25-117">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="b5e25-118">Your logic app uses this Azure AD application identity to authenticate against Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5e25-118">Your logic app uses this Azure AD application identity to authenticate against Azure AD.</span></span> <span data-ttu-id="b5e25-119">You only have to set up this identity one time for your directory.</span><span class="sxs-lookup"><span data-stu-id="b5e25-119">You only have to set up this identity one time for your directory.</span></span> <span data-ttu-id="b5e25-120">For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app.</span><span class="sxs-lookup"><span data-stu-id="b5e25-120">For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="b5e25-121">You can set up these identities in the Azure portal or use [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="b5e25-121">You can set up these identities in the Azure portal or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="b5e25-122">**Create the application identity for your logic app in the Azure portal**</span><span class="sxs-lookup"><span data-stu-id="b5e25-122">**Create the application identity for your logic app in the Azure portal**</span></span>

1. <span data-ttu-id="b5e25-123">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-123">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="b5e25-124">Confirm that you're in the same directory as your web app or API app.</span><span class="sxs-lookup"><span data-stu-id="b5e25-124">Confirm that you're in the same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="b5e25-125">To switch directories, choose your profile and select another directory.</span><span class="sxs-lookup"><span data-stu-id="b5e25-125">To switch directories, choose your profile and select another directory.</span></span> <span data-ttu-id="b5e25-126">Or, choose **Overview** > **Switch directory**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-126">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="b5e25-127">On the directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-127">On the directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="b5e25-128">By default, the app registrations list shows all app registrations in your directory.</span><span class="sxs-lookup"><span data-stu-id="b5e25-128">By default, the app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="b5e25-129">To view only your app registrations, next to the search box, select **My apps**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-129">To view only your app registrations, next to the search box, select **My apps**.</span></span> 

   ![Create new app registration](./media/logic-apps-custom-api-authentication/new-app-registration-azure-portal.png)

4. <span data-ttu-id="b5e25-131">Give your application identity a name, leave **Application type** set to **Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-131">Give your application identity a name, leave **Application type** set to **Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Provide name and sign-on URL for application identity](./media/logic-apps-custom-api-authentication/logic-app-identity-azure-portal.png)

   <span data-ttu-id="b5e25-133">The application identity that you created for your logic app now appears in the app registrations list.</span><span class="sxs-lookup"><span data-stu-id="b5e25-133">The application identity that you created for your logic app now appears in the app registrations list.</span></span>

   ![Application identity for your logic app](./media/logic-apps-custom-api-authentication/logic-app-identity-created.png)

5. <span data-ttu-id="b5e25-135">In the app registrations list, select your new application identity.</span><span class="sxs-lookup"><span data-stu-id="b5e25-135">In the app registrations list, select your new application identity.</span></span> <span data-ttu-id="b5e25-136">Copy and save the **Application ID** to use as the "client ID" for your logic app in Part 3.</span><span class="sxs-lookup"><span data-stu-id="b5e25-136">Copy and save the **Application ID** to use as the "client ID" for your logic app in Part 3.</span></span>

   ![Copy and save application ID for logic app](./media/logic-apps-custom-api-authentication/logic-app-application-id.png)

6. <span data-ttu-id="b5e25-138">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-138">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="b5e25-139">Under **API Access**, choose **Keys**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-139">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="b5e25-140">Under **Description**, provide a name for your key.</span><span class="sxs-lookup"><span data-stu-id="b5e25-140">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="b5e25-141">Under **Expires**, select a duration for your key.</span><span class="sxs-lookup"><span data-stu-id="b5e25-141">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="b5e25-142">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span><span class="sxs-lookup"><span data-stu-id="b5e25-142">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

   ![Create key for logic app identity](./media/logic-apps-custom-api-authentication/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="b5e25-144">On the toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-144">On the toolbar, choose **Save**.</span></span> <span data-ttu-id="b5e25-145">Under **Value**, your key now appears.</span><span class="sxs-lookup"><span data-stu-id="b5e25-145">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="b5e25-146">**Make sure to copy and save your key** for later use because the key is hidden when you leave the **Keys** page.</span><span class="sxs-lookup"><span data-stu-id="b5e25-146">**Make sure to copy and save your key** for later use because the key is hidden when you leave the **Keys** page.</span></span>

   <span data-ttu-id="b5e25-147">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span><span class="sxs-lookup"><span data-stu-id="b5e25-147">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

   ![Copy and save key for later](./media/logic-apps-custom-api-authentication/logic-app-copy-key-secret-password.png)

<a name="powershell"></a>

<span data-ttu-id="b5e25-149">**Create the application identity for your logic app in PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b5e25-149">**Create the application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="b5e25-150">You can perform this task through Azure Resource Manager with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5e25-150">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="b5e25-151">In PowerShell, run these commands:</span><span class="sxs-lookup"><span data-stu-id="b5e25-151">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="b5e25-152">Make sure to copy the **Tenant ID** (GUID for your Azure AD tenant), the **Application ID**, and the password that you used.</span><span class="sxs-lookup"><span data-stu-id="b5e25-152">Make sure to copy the **Tenant ID** (GUID for your Azure AD tenant), the **Application ID**, and the password that you used.</span></span>

<span data-ttu-id="b5e25-153">For more information, learn how to [create a service principal with PowerShell to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="b5e25-153">For more information, learn how to [create a service principal with PowerShell to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="b5e25-154">Part 2: Create an Azure AD application identity for your web app or API app</span><span class="sxs-lookup"><span data-stu-id="b5e25-154">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="b5e25-155">If your web app or API app is already deployed, you can turn on authentication and create the application identity in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b5e25-155">If your web app or API app is already deployed, you can turn on authentication and create the application identity in the Azure portal.</span></span> <span data-ttu-id="b5e25-156">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="b5e25-156">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="b5e25-157">**Create the application identity and turn on authentication in the Azure portal for deployed apps**</span><span class="sxs-lookup"><span data-stu-id="b5e25-157">**Create the application identity and turn on authentication in the Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="b5e25-158">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span><span class="sxs-lookup"><span data-stu-id="b5e25-158">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="b5e25-159">Under **Settings**, choose **Authentication/Authorization**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-159">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="b5e25-160">Under **App Service Authentication**, turn authentication **On**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-160">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="b5e25-161">Under **Authentication Providers**, choose **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-161">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Turn on authentication](./media/logic-apps-custom-api-authentication/custom-web-api-app-authentication.png)

3. <span data-ttu-id="b5e25-163">Now create an application identity for your web app or API app as shown here.</span><span class="sxs-lookup"><span data-stu-id="b5e25-163">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="b5e25-164">On the **Azure Active Directory Settings** page, set **Management mode** to **Express**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-164">On the **Azure Active Directory Settings** page, set **Management mode** to **Express**.</span></span> <span data-ttu-id="b5e25-165">Choose **Create New AD App**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-165">Choose **Create New AD App**.</span></span> <span data-ttu-id="b5e25-166">Give your application identity a name, and choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-166">Give your application identity a name, and choose **OK**.</span></span> 

   ![Create application identity for your web app or API app](./media/logic-apps-custom-api-authentication/custom-api-application-identity.png)

4. <span data-ttu-id="b5e25-168">On the **Authentication / Authorization** page, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-168">On the **Authentication / Authorization** page, choose **Save**.</span></span>

<span data-ttu-id="b5e25-169">Now you must find the client ID and tenant ID for the application identity that's associated with your web app or API app.</span><span class="sxs-lookup"><span data-stu-id="b5e25-169">Now you must find the client ID and tenant ID for the application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="b5e25-170">You use these IDs in Part 3.</span><span class="sxs-lookup"><span data-stu-id="b5e25-170">You use these IDs in Part 3.</span></span> <span data-ttu-id="b5e25-171">So continue with these steps for the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b5e25-171">So continue with these steps for the Azure portal.</span></span>

<span data-ttu-id="b5e25-172">**Find application identity's client ID and tenant ID for your web app or API app in the Azure portal**</span><span class="sxs-lookup"><span data-stu-id="b5e25-172">**Find application identity's client ID and tenant ID for your web app or API app in the Azure portal**</span></span>

1. <span data-ttu-id="b5e25-173">Under **Authentication Providers**, choose **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-173">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Choose "Azure Active Directory"](./media/logic-apps-custom-api-authentication/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="b5e25-175">On the **Azure Active Directory Settings** page, set **Management mode** to **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-175">On the **Azure Active Directory Settings** page, set **Management mode** to **Advanced**.</span></span>

3. <span data-ttu-id="b5e25-176">Copy the **Client ID**, and save that GUID for use in Part 3.</span><span class="sxs-lookup"><span data-stu-id="b5e25-176">Copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="b5e25-177">If **Client ID** and **Issuer Url** don't appear, try refreshing the Azure portal, and repeat Step 1.</span><span class="sxs-lookup"><span data-stu-id="b5e25-177">If **Client ID** and **Issuer Url** don't appear, try refreshing the Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="b5e25-178">Under **Issuer Url**, copy and save just the GUID for Part 3.</span><span class="sxs-lookup"><span data-stu-id="b5e25-178">Under **Issuer Url**, copy and save just the GUID for Part 3.</span></span> <span data-ttu-id="b5e25-179">You can also use this GUID in your web app or API app's deployment template, if necessary.</span><span class="sxs-lookup"><span data-stu-id="b5e25-179">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="b5e25-180">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="b5e25-180">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="b5e25-181">Without saving your changes, close the **Azure Active Directory Settings** page.</span><span class="sxs-lookup"><span data-stu-id="b5e25-181">Without saving your changes, close the **Azure Active Directory Settings** page.</span></span>

<a name="authen-deploy"></a>

<span data-ttu-id="b5e25-182">**Turn on authentication when you deploy with an Azure Resource Manager template**</span><span class="sxs-lookup"><span data-stu-id="b5e25-182">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="b5e25-183">You must still create an Azure AD application identity for your web app or API app that differs from the app identity for your logic app.</span><span class="sxs-lookup"><span data-stu-id="b5e25-183">You must still create an Azure AD application identity for your web app or API app that differs from the app identity for your logic app.</span></span> <span data-ttu-id="b5e25-184">To create the application identity, follow the previous steps in Part 2 for the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b5e25-184">To create the application identity, follow the previous steps in Part 2 for the Azure portal.</span></span> 

<span data-ttu-id="b5e25-185">You can also follow the steps in Part 1, but make sure to use your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span><span class="sxs-lookup"><span data-stu-id="b5e25-185">You can also follow the steps in Part 1, but make sure to use your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="b5e25-186">From these steps, you have to save both the client ID and tenant ID for use in your app's deployment template and also for Part 3.</span><span class="sxs-lookup"><span data-stu-id="b5e25-186">From these steps, you have to save both the client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="b5e25-187">When you create the Azure AD application identity for your web app or API app, you must use the Azure portal, not PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5e25-187">When you create the Azure AD application identity for your web app or API app, you must use the Azure portal, not PowerShell.</span></span> <span data-ttu-id="b5e25-188">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span><span class="sxs-lookup"><span data-stu-id="b5e25-188">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span></span>

<span data-ttu-id="b5e25-189">After you get the client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span><span class="sxs-lookup"><span data-stu-id="b5e25-189">After you get the client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

``` json
"resources": [ {
    "apiVersion": "2015-08-01",
    "name": "web",
    "type": "config",
    "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
    "properties": {
        "siteAuthEnabled": true,
        "siteAuthSettings": {
            "clientId": "{client-ID}",
            "issuer": "https://sts.windows.net/{tenant-ID}/",
        }
    }
} ]
```

<span data-ttu-id="b5e25-190">To automatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view the complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy to Azure** here:</span><span class="sxs-lookup"><span data-stu-id="b5e25-190">To automatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view the complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy to Azure** here:</span></span>

<span data-ttu-id="b5e25-191">[![Deploy to Azure](media/logic-apps-custom-api-authentication/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b5e25-191">[![Deploy to Azure](media/logic-apps-custom-api-authentication/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a><span data-ttu-id="b5e25-192">Part 3: Populate the Authorization section in your logic app</span><span class="sxs-lookup"><span data-stu-id="b5e25-192">Part 3: Populate the Authorization section in your logic app</span></span>

<span data-ttu-id="b5e25-193">The previous template already has this authorization section set up, but if you are directly authoring the logic app, you must include the full authorization section.</span><span class="sxs-lookup"><span data-stu-id="b5e25-193">The previous template already has this authorization section set up, but if you are directly authoring the logic app, you must include the full authorization section.</span></span>

<span data-ttu-id="b5e25-194">Open your logic app definition in code view, go to the **HTTP** action section, find the **Authorization** section, and include this line:</span><span class="sxs-lookup"><span data-stu-id="b5e25-194">Open your logic app definition in code view, go to the **HTTP** action section, find the **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="b5e25-195">Element</span><span class="sxs-lookup"><span data-stu-id="b5e25-195">Element</span></span> | <span data-ttu-id="b5e25-196">Required</span><span class="sxs-lookup"><span data-stu-id="b5e25-196">Required</span></span> | <span data-ttu-id="b5e25-197">Description</span><span class="sxs-lookup"><span data-stu-id="b5e25-197">Description</span></span> | 
| ------- | -------- | ----------- | 
| <span data-ttu-id="b5e25-198">tenant</span><span class="sxs-lookup"><span data-stu-id="b5e25-198">tenant</span></span> | <span data-ttu-id="b5e25-199">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-199">Yes</span></span> | <span data-ttu-id="b5e25-200">The GUID for the Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="b5e25-200">The GUID for the Azure AD tenant</span></span> | 
| <span data-ttu-id="b5e25-201">audience</span><span class="sxs-lookup"><span data-stu-id="b5e25-201">audience</span></span> | <span data-ttu-id="b5e25-202">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-202">Yes</span></span> | <span data-ttu-id="b5e25-203">The GUID for the target resource that you want to access, which is the client ID from the application identity for your web app or API app</span><span class="sxs-lookup"><span data-stu-id="b5e25-203">The GUID for the target resource that you want to access, which is the client ID from the application identity for your web app or API app</span></span> | 
| <span data-ttu-id="b5e25-204">clientId</span><span class="sxs-lookup"><span data-stu-id="b5e25-204">clientId</span></span> | <span data-ttu-id="b5e25-205">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-205">Yes</span></span> | <span data-ttu-id="b5e25-206">The GUID for the client requesting access, which is the client ID from the application identity for your logic app</span><span class="sxs-lookup"><span data-stu-id="b5e25-206">The GUID for the client requesting access, which is the client ID from the application identity for your logic app</span></span> | 
| <span data-ttu-id="b5e25-207">secret</span><span class="sxs-lookup"><span data-stu-id="b5e25-207">secret</span></span> | <span data-ttu-id="b5e25-208">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-208">Yes</span></span> | <span data-ttu-id="b5e25-209">The key or password from the application identity for the client that's requesting the access token</span><span class="sxs-lookup"><span data-stu-id="b5e25-209">The key or password from the application identity for the client that's requesting the access token</span></span> | 
| <span data-ttu-id="b5e25-210">type</span><span class="sxs-lookup"><span data-stu-id="b5e25-210">type</span></span> | <span data-ttu-id="b5e25-211">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-211">Yes</span></span> | <span data-ttu-id="b5e25-212">The authentication type.</span><span class="sxs-lookup"><span data-stu-id="b5e25-212">The authentication type.</span></span> <span data-ttu-id="b5e25-213">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="b5e25-213">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> | 
|||| 

<span data-ttu-id="b5e25-214">For example:</span><span class="sxs-lookup"><span data-stu-id="b5e25-214">For example:</span></span>

``` json
{
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="b5e25-215">Secure API calls through code</span><span class="sxs-lookup"><span data-stu-id="b5e25-215">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="b5e25-216">Certificate authentication</span><span class="sxs-lookup"><span data-stu-id="b5e25-216">Certificate authentication</span></span>

<span data-ttu-id="b5e25-217">To validate the incoming requests from your logic app to your web app or API app, you can use client certificates.</span><span class="sxs-lookup"><span data-stu-id="b5e25-217">To validate the incoming requests from your logic app to your web app or API app, you can use client certificates.</span></span> <span data-ttu-id="b5e25-218">To set up your code, learn [how to configure TLS mutual authentication](../app-service/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="b5e25-218">To set up your code, learn [how to configure TLS mutual authentication](../app-service/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="b5e25-219">In the **Authorization** section, include this line:</span><span class="sxs-lookup"><span data-stu-id="b5e25-219">In the **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="b5e25-220">Element</span><span class="sxs-lookup"><span data-stu-id="b5e25-220">Element</span></span> | <span data-ttu-id="b5e25-221">Required</span><span class="sxs-lookup"><span data-stu-id="b5e25-221">Required</span></span> | <span data-ttu-id="b5e25-222">Description</span><span class="sxs-lookup"><span data-stu-id="b5e25-222">Description</span></span> | 
| ------- | -------- | ----------- | 
| <span data-ttu-id="b5e25-223">type</span><span class="sxs-lookup"><span data-stu-id="b5e25-223">type</span></span> | <span data-ttu-id="b5e25-224">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-224">Yes</span></span> | <span data-ttu-id="b5e25-225">The authentication type.</span><span class="sxs-lookup"><span data-stu-id="b5e25-225">The authentication type.</span></span> <span data-ttu-id="b5e25-226">For SSL client certificates, the value must be `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="b5e25-226">For SSL client certificates, the value must be `ClientCertificate`.</span></span> | 
| <span data-ttu-id="b5e25-227">password</span><span class="sxs-lookup"><span data-stu-id="b5e25-227">password</span></span> | <span data-ttu-id="b5e25-228">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-228">Yes</span></span> | <span data-ttu-id="b5e25-229">The password for accessing the client certificate (PFX file)</span><span class="sxs-lookup"><span data-stu-id="b5e25-229">The password for accessing the client certificate (PFX file)</span></span> | 
| <span data-ttu-id="b5e25-230">pfx</span><span class="sxs-lookup"><span data-stu-id="b5e25-230">pfx</span></span> | <span data-ttu-id="b5e25-231">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-231">Yes</span></span> | <span data-ttu-id="b5e25-232">The base64-encoded contents of the client certificate (PFX file)</span><span class="sxs-lookup"><span data-stu-id="b5e25-232">The base64-encoded contents of the client certificate (PFX file)</span></span> | 
|||| 

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="b5e25-233">Basic authentication</span><span class="sxs-lookup"><span data-stu-id="b5e25-233">Basic authentication</span></span>

<span data-ttu-id="b5e25-234">To validate incoming requests from your logic app to your web app or API app, you can use basic authentication, such as a username and password.</span><span class="sxs-lookup"><span data-stu-id="b5e25-234">To validate incoming requests from your logic app to your web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="b5e25-235">Basic authentication is a common pattern, and you can use this authentication in any language used to build your web app or API app.</span><span class="sxs-lookup"><span data-stu-id="b5e25-235">Basic authentication is a common pattern, and you can use this authentication in any language used to build your web app or API app.</span></span>

<span data-ttu-id="b5e25-236">In the **Authorization** section, include this line:</span><span class="sxs-lookup"><span data-stu-id="b5e25-236">In the **Authorization** section, include this line:</span></span>

<span data-ttu-id="b5e25-237">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="b5e25-237">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="b5e25-238">Element</span><span class="sxs-lookup"><span data-stu-id="b5e25-238">Element</span></span> | <span data-ttu-id="b5e25-239">Required</span><span class="sxs-lookup"><span data-stu-id="b5e25-239">Required</span></span> | <span data-ttu-id="b5e25-240">Description</span><span class="sxs-lookup"><span data-stu-id="b5e25-240">Description</span></span> | 
| ------- | -------- | ----------- | 
| <span data-ttu-id="b5e25-241">type</span><span class="sxs-lookup"><span data-stu-id="b5e25-241">type</span></span> | <span data-ttu-id="b5e25-242">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-242">Yes</span></span> | <span data-ttu-id="b5e25-243">The authentication type that you want to use.</span><span class="sxs-lookup"><span data-stu-id="b5e25-243">The authentication type that you want to use.</span></span> <span data-ttu-id="b5e25-244">For basic authentication, the value must be `Basic`.</span><span class="sxs-lookup"><span data-stu-id="b5e25-244">For basic authentication, the value must be `Basic`.</span></span> | 
| <span data-ttu-id="b5e25-245">username</span><span class="sxs-lookup"><span data-stu-id="b5e25-245">username</span></span> | <span data-ttu-id="b5e25-246">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-246">Yes</span></span> | <span data-ttu-id="b5e25-247">The username that you want to use for authentication</span><span class="sxs-lookup"><span data-stu-id="b5e25-247">The username that you want to use for authentication</span></span> | 
| <span data-ttu-id="b5e25-248">password</span><span class="sxs-lookup"><span data-stu-id="b5e25-248">password</span></span> | <span data-ttu-id="b5e25-249">Yes</span><span class="sxs-lookup"><span data-stu-id="b5e25-249">Yes</span></span> | <span data-ttu-id="b5e25-250">The password that you want to use for authentication</span><span class="sxs-lookup"><span data-stu-id="b5e25-250">The password that you want to use for authentication</span></span> | 
|||| 

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="b5e25-251">Azure Active Directory authentication through code</span><span class="sxs-lookup"><span data-stu-id="b5e25-251">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="b5e25-252">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span><span class="sxs-lookup"><span data-stu-id="b5e25-252">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="b5e25-253">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span><span class="sxs-lookup"><span data-stu-id="b5e25-253">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

<span data-ttu-id="b5e25-254">To restrict API access to your logic app through code, extract the header that has the JSON web token (JWT).</span><span class="sxs-lookup"><span data-stu-id="b5e25-254">To restrict API access to your logic app through code, extract the header that has the JSON web token (JWT).</span></span> <span data-ttu-id="b5e25-255">Check the caller's identity, and reject requests that don't match.</span><span class="sxs-lookup"><span data-stu-id="b5e25-255">Check the caller's identity, and reject requests that don't match.</span></span>

<!-- Going further, to implement this authentication entirely in your own code, 
and not use the Azure portal, learn how to 
[authenticate with on-premises Active Directory in your Azure app](../app-service/app-service-authentication-overview.md).

To create an application identity for your logic app and use that identity to call your API, 
you must follow the previous steps. -->

## <a name="next-steps"></a><span data-ttu-id="b5e25-256">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5e25-256">Next steps</span></span>

* [<span data-ttu-id="b5e25-257">Deploy and call custom APIs from logic app workflows</span><span class="sxs-lookup"><span data-stu-id="b5e25-257">Deploy and call custom APIs from logic app workflows</span></span>](../logic-apps/logic-apps-custom-api-host-deploy-call.md)