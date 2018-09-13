---
title: Call custom APIs in Azure Logic Apps | Microsoft Docs
description: Call into your own custom APIs hosted on Azure App Service with Azure Logic Apps
author: stepsic-microsoft-com
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: stepsic
ms.openlocfilehash: 116b6b5c04d4c07f82a1de475d7efd9e9a1b915a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551316"
---
# <a name="call-custom-apis-hosted-on-azure-app-service-with-azure-logic-apps"></a><span data-ttu-id="9f33c-103">Call custom APIs hosted on Azure App Service with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9f33c-103">Call custom APIs hosted on Azure App Service with Azure Logic Apps</span></span>

<span data-ttu-id="9f33c-104">Although Azure Logic Apps offers 40+ connectors for various services, you might want to call into your own custom API that can run your own code.</span><span class="sxs-lookup"><span data-stu-id="9f33c-104">Although Azure Logic Apps offers 40+ connectors for various services, you might want to call into your own custom API that can run your own code.</span></span> <span data-ttu-id="9f33c-105">Azure App Service provides one of the easiest and most scalable ways for hosting your own custom web APIs.</span><span class="sxs-lookup"><span data-stu-id="9f33c-105">Azure App Service provides one of the easiest and most scalable ways for hosting your own custom web APIs.</span></span> <span data-ttu-id="9f33c-106">This article covers how to call into any web API hosted in an App Service API app, web app, or mobile app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-106">This article covers how to call into any web API hosted in an App Service API app, web app, or mobile app.</span></span>
<span data-ttu-id="9f33c-107">Learn [how to build APIs as a trigger or action in logic apps](../logic-apps/logic-apps-create-api-app.md).</span><span class="sxs-lookup"><span data-stu-id="9f33c-107">Learn [how to build APIs as a trigger or action in logic apps](../logic-apps/logic-apps-create-api-app.md).</span></span>

## <a name="deploy-your-web-app"></a><span data-ttu-id="9f33c-108">Deploy your web app</span><span class="sxs-lookup"><span data-stu-id="9f33c-108">Deploy your web app</span></span>

<span data-ttu-id="9f33c-109">First, you must deploy your API as a web app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="9f33c-109">First, you must deploy your API as a web app in Azure App Service.</span></span> <span data-ttu-id="9f33c-110">Learn about [basic deployment when you create an ASP.NET web app](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9f33c-110">Learn about [basic deployment when you create an ASP.NET web app](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="9f33c-111">While you can call into any API from a logic app, for the best experience, we recommend that you add Swagger metadata to integrate easily with logic app actions.</span><span class="sxs-lookup"><span data-stu-id="9f33c-111">While you can call into any API from a logic app, for the best experience, we recommend that you add Swagger metadata to integrate easily with logic app actions.</span></span> <span data-ttu-id="9f33c-112">Learn about [adding Swagger metadata](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui).</span><span class="sxs-lookup"><span data-stu-id="9f33c-112">Learn about [adding Swagger metadata](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui).</span></span>

### <a name="api-settings"></a><span data-ttu-id="9f33c-113">API settings</span><span class="sxs-lookup"><span data-stu-id="9f33c-113">API settings</span></span>

<span data-ttu-id="9f33c-114">For Logic App Designer to parse your Swagger, you must enable CORS and set the API Definition properties for your web app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-114">For Logic App Designer to parse your Swagger, you must enable CORS and set the API Definition properties for your web app.</span></span> 

1.  <span data-ttu-id="9f33c-115">In the Azure portal, select your web app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-115">In the Azure portal, select your web app.</span></span>
2.  <span data-ttu-id="9f33c-116">In the blade that opens, find **API**, and select **API definition**.</span><span class="sxs-lookup"><span data-stu-id="9f33c-116">In the blade that opens, find **API**, and select **API definition**.</span></span> <span data-ttu-id="9f33c-117">Set the **API definition location** to your swagger.json file's URL.</span><span class="sxs-lookup"><span data-stu-id="9f33c-117">Set the **API definition location** to your swagger.json file's URL.</span></span>

    <span data-ttu-id="9f33c-118">Usually, this URL is https://{name}.azurewebsites.net/swagger/docs/v1).</span><span class="sxs-lookup"><span data-stu-id="9f33c-118">Usually, this URL is https://{name}.azurewebsites.net/swagger/docs/v1).</span></span>

3.  <span data-ttu-id="9f33c-119">To allow requests from Logic App Designer, under **API**, select **CORS**, and set a CORS policy for '\*'.</span><span class="sxs-lookup"><span data-stu-id="9f33c-119">To allow requests from Logic App Designer, under **API**, select **CORS**, and set a CORS policy for '\*'.</span></span>

## <a name="call-into-your-custom-api"></a><span data-ttu-id="9f33c-120">Call into your custom API</span><span class="sxs-lookup"><span data-stu-id="9f33c-120">Call into your custom API</span></span>

<span data-ttu-id="9f33c-121">If you set up CORS and the API Definition properties, you should be able to easily add Custom API actions to your workflow in the Logic Apps portal.</span><span class="sxs-lookup"><span data-stu-id="9f33c-121">If you set up CORS and the API Definition properties, you should be able to easily add Custom API actions to your workflow in the Logic Apps portal.</span></span> <span data-ttu-id="9f33c-122">In the Logic Apps Designer, you can browse your subscription websites to list the websites that have a defined Swagger URL.</span><span class="sxs-lookup"><span data-stu-id="9f33c-122">In the Logic Apps Designer, you can browse your subscription websites to list the websites that have a defined Swagger URL.</span></span> <span data-ttu-id="9f33c-123">You can also point to a Swagger and list the available actions and inputs by using the HTTP + Swagger action.</span><span class="sxs-lookup"><span data-stu-id="9f33c-123">You can also point to a Swagger and list the available actions and inputs by using the HTTP + Swagger action.</span></span> <span data-ttu-id="9f33c-124">Finally, you can always create a request using the HTTP action to call any API, even APIs that don't have or expose a Swagger doc.</span><span class="sxs-lookup"><span data-stu-id="9f33c-124">Finally, you can always create a request using the HTTP action to call any API, even APIs that don't have or expose a Swagger doc.</span></span>

<span data-ttu-id="9f33c-125">To secure your API, you have a couple different ways to do that:</span><span class="sxs-lookup"><span data-stu-id="9f33c-125">To secure your API, you have a couple different ways to do that:</span></span>

*   <span data-ttu-id="9f33c-126">No code changes required.</span><span class="sxs-lookup"><span data-stu-id="9f33c-126">No code changes required.</span></span> <span data-ttu-id="9f33c-127">You can use Azure Active Directory to protect your API without requiring any code changes or redeployment.</span><span class="sxs-lookup"><span data-stu-id="9f33c-127">You can use Azure Active Directory to protect your API without requiring any code changes or redeployment.</span></span>
*   <span data-ttu-id="9f33c-128">In your API's code, enforce Basic Authentication, Azure Active Directory authentication, or Certificate Authentication.</span><span class="sxs-lookup"><span data-stu-id="9f33c-128">In your API's code, enforce Basic Authentication, Azure Active Directory authentication, or Certificate Authentication.</span></span>

## <a name="secure-calls-to-your-api-without-changing-code"></a><span data-ttu-id="9f33c-129">Secure calls to your API without changing code</span><span class="sxs-lookup"><span data-stu-id="9f33c-129">Secure calls to your API without changing code</span></span>

<span data-ttu-id="9f33c-130">In this section, you will create two Azure Active Directory applications – one for your logic app and one for your web app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-130">In this section, you will create two Azure Active Directory applications – one for your logic app and one for your web app.</span></span> <span data-ttu-id="9f33c-131">Authenticate calls to your web app by using the service principal (client id and secret) associated with your logic app's Azure Active Directory app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-131">Authenticate calls to your web app by using the service principal (client id and secret) associated with your logic app's Azure Active Directory app.</span></span> <span data-ttu-id="9f33c-132">Finally, include the application IDs in your logic app definition.</span><span class="sxs-lookup"><span data-stu-id="9f33c-132">Finally, include the application IDs in your logic app definition.</span></span>

### <a name="part-1-set-up-an-application-identity-for-your-logic-app"></a><span data-ttu-id="9f33c-133">Part 1: Set up an application identity for your logic app</span><span class="sxs-lookup"><span data-stu-id="9f33c-133">Part 1: Set up an application identity for your logic app</span></span>

<span data-ttu-id="9f33c-134">Your logic app uses this application identity to authenticate against Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9f33c-134">Your logic app uses this application identity to authenticate against Azure Active Directory.</span></span> <span data-ttu-id="9f33c-135">You only have to set up this identity once for your directory.</span><span class="sxs-lookup"><span data-stu-id="9f33c-135">You only have to set up this identity once for your directory.</span></span> <span data-ttu-id="9f33c-136">For example, you can choose to use the same identity for all your logic apps, although you can also create unique identities per logic app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-136">For example, you can choose to use the same identity for all your logic apps, although you can also create unique identities per logic app.</span></span> <span data-ttu-id="9f33c-137">You can set up these identities either in the Azure portal or use PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f33c-137">You can set up these identities either in the Azure portal or use PowerShell.</span></span>

#### <a name="create-the-application-identity-in-the-azure-classic-portal"></a><span data-ttu-id="9f33c-138">Create the application identity in the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="9f33c-138">Create the application identity in the Azure classic portal</span></span>

1. <span data-ttu-id="9f33c-139">In the Azure classic portal, go to your [Azure Active Directory](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="9f33c-139">In the Azure classic portal, go to your [Azure Active Directory](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span> 
2. <span data-ttu-id="9f33c-140">Select the directory that you use for your web app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-140">Select the directory that you use for your web app.</span></span>
3. <span data-ttu-id="9f33c-141">Choose the **Applications** tab. In the command bar at the bottom of the page, choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="9f33c-141">Choose the **Applications** tab. In the command bar at the bottom of the page, choose **Add**.</span></span>
5. <span data-ttu-id="9f33c-142">Give your app identity a name, and click the next arrow.</span><span class="sxs-lookup"><span data-stu-id="9f33c-142">Give your app identity a name, and click the next arrow.</span></span>
6. <span data-ttu-id="9f33c-143">Under **App properties**, put in a unique string formatted as a domain, and click the checkmark.</span><span class="sxs-lookup"><span data-stu-id="9f33c-143">Under **App properties**, put in a unique string formatted as a domain, and click the checkmark.</span></span>
7. <span data-ttu-id="9f33c-144">Choose the **Configure** tab. Go to **Client ID**, and copy the client ID for use in your logic app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-144">Choose the **Configure** tab. Go to **Client ID**, and copy the client ID for use in your logic app.</span></span>
8. <span data-ttu-id="9f33c-145">Under **Keys**, open the **Select duration** list, and select the duration time for your key.</span><span class="sxs-lookup"><span data-stu-id="9f33c-145">Under **Keys**, open the **Select duration** list, and select the duration time for your key.</span></span>
9. <span data-ttu-id="9f33c-146">At the bottom of the page, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9f33c-146">At the bottom of the page, click **Save**.</span></span> <span data-ttu-id="9f33c-147">You might have to wait a few seconds.</span><span class="sxs-lookup"><span data-stu-id="9f33c-147">You might have to wait a few seconds.</span></span>
10. <span data-ttu-id="9f33c-148">Make sure to copy the key that now appears under **Keys**, so you can use this key in your logic app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-148">Make sure to copy the key that now appears under **Keys**, so you can use this key in your logic app.</span></span>

#### <a name="create-the-application-identity-using-powershell"></a><span data-ttu-id="9f33c-149">Create the application identity using PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f33c-149">Create the application identity using PowerShell</span></span>

1. `Switch-AzureMode AzureResourceManager`
2. `Add-AzureAccount`
3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://someranddomain.tld" -IdentifierUris "http://someranddomain.tld" -Password "Pass@word1!"`
4. <span data-ttu-id="9f33c-150">Make sure to copy the **Tenant ID**, the **Application ID**, and the password you used.</span><span class="sxs-lookup"><span data-stu-id="9f33c-150">Make sure to copy the **Tenant ID**, the **Application ID**, and the password you used.</span></span>

### <a name="part-2-protect-your-web-app-with-an-azure-active-directory-app-identity"></a><span data-ttu-id="9f33c-151">Part 2: Protect your web app with an Azure Active Directory app identity</span><span class="sxs-lookup"><span data-stu-id="9f33c-151">Part 2: Protect your web app with an Azure Active Directory app identity</span></span>

<span data-ttu-id="9f33c-152">If your web app is already deployed, you can enable authorization in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9f33c-152">If your web app is already deployed, you can enable authorization in the Azure portal.</span></span> <span data-ttu-id="9f33c-153">Otherwise, you can make enabling authorization part of your Azure Resource Manager deployment.</span><span class="sxs-lookup"><span data-stu-id="9f33c-153">Otherwise, you can make enabling authorization part of your Azure Resource Manager deployment.</span></span>

#### <a name="enable-authorization-in-the-azure-portal"></a><span data-ttu-id="9f33c-154">Enable authorization in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9f33c-154">Enable authorization in the Azure portal</span></span>

1. <span data-ttu-id="9f33c-155">Find and select your web app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-155">Find and select your web app.</span></span> <span data-ttu-id="9f33c-156">Under **Settings**, choose **Authentication/Authorization**.</span><span class="sxs-lookup"><span data-stu-id="9f33c-156">Under **Settings**, choose **Authentication/Authorization**.</span></span>
2. <span data-ttu-id="9f33c-157">Under **App Service Authentication**, turn authentication **On**, and choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="9f33c-157">Under **App Service Authentication**, turn authentication **On**, and choose **Save**.</span></span>

<span data-ttu-id="9f33c-158">At this point, an Application is automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="9f33c-158">At this point, an Application is automatically created for you.</span></span> <span data-ttu-id="9f33c-159">You need this Application's Client ID for Part 3, so you must follow these steps:</span><span class="sxs-lookup"><span data-stu-id="9f33c-159">You need this Application's Client ID for Part 3, so you must follow these steps:</span></span>

1. <span data-ttu-id="9f33c-160">In the Azure classic portal, go to your [Azure Active Directory](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="9f33c-160">In the Azure classic portal, go to your [Azure Active Directory](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>
2.  <span data-ttu-id="9f33c-161">Select your directory.</span><span class="sxs-lookup"><span data-stu-id="9f33c-161">Select your directory.</span></span>
3. <span data-ttu-id="9f33c-162">In the search box, find your app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-162">In the search box, find your app.</span></span>
4. <span data-ttu-id="9f33c-163">In the list, select your app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-163">In the list, select your app.</span></span>
5. <span data-ttu-id="9f33c-164">Choose the **Configure** tab where you should see the **Client ID**.</span><span class="sxs-lookup"><span data-stu-id="9f33c-164">Choose the **Configure** tab where you should see the **Client ID**.</span></span>

#### <a name="deploy-your-web-app-using-an-azure-resource-manager-template"></a><span data-ttu-id="9f33c-165">Deploy your web app using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="9f33c-165">Deploy your web app using an Azure Resource Manager template</span></span>

<span data-ttu-id="9f33c-166">First, you must create an Application for your web app that's different from the Application that you use for your logic app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-166">First, you must create an Application for your web app that's different from the Application that you use for your logic app.</span></span> <span data-ttu-id="9f33c-167">Start by following the previous steps in Part 1, but for **HomePage** and **IdentifierUris**, use your web app's actual https://**URL**.</span><span class="sxs-lookup"><span data-stu-id="9f33c-167">Start by following the previous steps in Part 1, but for **HomePage** and **IdentifierUris**, use your web app's actual https://**URL**.</span></span>

> [!NOTE]
> <span data-ttu-id="9f33c-168">When you create the Application for your web app, you must use the [Azure classic portal](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="9f33c-168">When you create the Application for your web app, you must use the [Azure classic portal](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span> <span data-ttu-id="9f33c-169">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span><span class="sxs-lookup"><span data-stu-id="9f33c-169">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span></span>

<span data-ttu-id="9f33c-170">After you have the client ID and tenant ID, include this part as a sub resource of your web app in your deployment template:</span><span class="sxs-lookup"><span data-stu-id="9f33c-170">After you have the client ID and tenant ID, include this part as a sub resource of your web app in your deployment template:</span></span>

```
"resources": [
    {
        "apiVersion": "2015-08-01",
        "name": "web",
        "type": "config",
        "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
        "properties": {
            "siteAuthEnabled": true,
            "siteAuthSettings": {
              "clientId": "<<clientID>>",
              "issuer": "https://sts.windows.net/<<tenantID>>/",
            }
        }
    }
]
```

<span data-ttu-id="9f33c-171">To automatically run a deployment that deploys a blank web app and logic app together that use Azure Active Directory, click **Deploy to Azure**:</span><span class="sxs-lookup"><span data-stu-id="9f33c-171">To automatically run a deployment that deploys a blank web app and logic app together that use Azure Active Directory, click **Deploy to Azure**:</span></span>

<span data-ttu-id="9f33c-172">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="9f33c-172">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

<span data-ttu-id="9f33c-173">For the complete template, see [Logic app calls into a custom API hosted on App Service and protected by Azure Active Directory](https://github.com/Azure/azure-quickstart-templates/blob/master/201-logic-app-custom-api/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9f33c-173">For the complete template, see [Logic app calls into a custom API hosted on App Service and protected by Azure Active Directory](https://github.com/Azure/azure-quickstart-templates/blob/master/201-logic-app-custom-api/azuredeploy.json).</span></span>

### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a><span data-ttu-id="9f33c-174">Part 3: Populate the Authorization section in your logic app</span><span class="sxs-lookup"><span data-stu-id="9f33c-174">Part 3: Populate the Authorization section in your logic app</span></span>

<span data-ttu-id="9f33c-175">In the **Authorization** section of the **HTTP** action:</span><span class="sxs-lookup"><span data-stu-id="9f33c-175">In the **Authorization** section of the **HTTP** action:</span></span>

`{"tenant":"<<tenantId>>", "audience":"<<clientID from Part 2>>", "clientId":"<<clientID from Part 1>>","secret": "<<Password or Key from Part 1>>","type":"ActiveDirectoryOAuth" }`

| <span data-ttu-id="9f33c-176">Element</span><span class="sxs-lookup"><span data-stu-id="9f33c-176">Element</span></span> | <span data-ttu-id="9f33c-177">Description</span><span class="sxs-lookup"><span data-stu-id="9f33c-177">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="9f33c-178">type</span><span class="sxs-lookup"><span data-stu-id="9f33c-178">type</span></span> |<span data-ttu-id="9f33c-179">Type of authentication.</span><span class="sxs-lookup"><span data-stu-id="9f33c-179">Type of authentication.</span></span> <span data-ttu-id="9f33c-180">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="9f33c-180">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="9f33c-181">tenant</span><span class="sxs-lookup"><span data-stu-id="9f33c-181">tenant</span></span> |<span data-ttu-id="9f33c-182">The tenant identifier used to identify the AD tenant.</span><span class="sxs-lookup"><span data-stu-id="9f33c-182">The tenant identifier used to identify the AD tenant.</span></span> |
| <span data-ttu-id="9f33c-183">audience</span><span class="sxs-lookup"><span data-stu-id="9f33c-183">audience</span></span> |<span data-ttu-id="9f33c-184">Required.</span><span class="sxs-lookup"><span data-stu-id="9f33c-184">Required.</span></span> <span data-ttu-id="9f33c-185">The resource you are connecting to.</span><span class="sxs-lookup"><span data-stu-id="9f33c-185">The resource you are connecting to.</span></span> |
| <span data-ttu-id="9f33c-186">clientID</span><span class="sxs-lookup"><span data-stu-id="9f33c-186">clientID</span></span> |<span data-ttu-id="9f33c-187">The client identifier for the Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="9f33c-187">The client identifier for the Azure AD application.</span></span> |
| <span data-ttu-id="9f33c-188">secret</span><span class="sxs-lookup"><span data-stu-id="9f33c-188">secret</span></span> |<span data-ttu-id="9f33c-189">Required.</span><span class="sxs-lookup"><span data-stu-id="9f33c-189">Required.</span></span> <span data-ttu-id="9f33c-190">Secret of the client that is requesting the token.</span><span class="sxs-lookup"><span data-stu-id="9f33c-190">Secret of the client that is requesting the token.</span></span> |

<span data-ttu-id="9f33c-191">The previous template has this authorization section set up already, but if you are authoring the logic app directly, you must include the full authorization section.</span><span class="sxs-lookup"><span data-stu-id="9f33c-191">The previous template has this authorization section set up already, but if you are authoring the logic app directly, you must include the full authorization section.</span></span>

## <a name="secure-your-api-in-code"></a><span data-ttu-id="9f33c-192">Secure your API in code</span><span class="sxs-lookup"><span data-stu-id="9f33c-192">Secure your API in code</span></span>

### <a name="certificate-authentication"></a><span data-ttu-id="9f33c-193">Certificate authentication</span><span class="sxs-lookup"><span data-stu-id="9f33c-193">Certificate authentication</span></span>

<span data-ttu-id="9f33c-194">You can use client certificates to validate the incoming requests to your web app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-194">You can use client certificates to validate the incoming requests to your web app.</span></span> <span data-ttu-id="9f33c-195">For how to set up your code, see [How to configure TLS mutual authentication for web app](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="9f33c-195">For how to set up your code, see [How to configure TLS mutual authentication for web app](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="9f33c-196">In the **Authorization** section, you should include:</span><span class="sxs-lookup"><span data-stu-id="9f33c-196">In the **Authorization** section, you should include:</span></span> 

`{"type": "clientcertificate","password": "test","pfx": "long-pfx-key"}`

| <span data-ttu-id="9f33c-197">Element</span><span class="sxs-lookup"><span data-stu-id="9f33c-197">Element</span></span> | <span data-ttu-id="9f33c-198">Description</span><span class="sxs-lookup"><span data-stu-id="9f33c-198">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="9f33c-199">type</span><span class="sxs-lookup"><span data-stu-id="9f33c-199">type</span></span> |<span data-ttu-id="9f33c-200">Required.</span><span class="sxs-lookup"><span data-stu-id="9f33c-200">Required.</span></span> <span data-ttu-id="9f33c-201">Type of authentication.</span><span class="sxs-lookup"><span data-stu-id="9f33c-201">Type of authentication.</span></span> <span data-ttu-id="9f33c-202">For SSL client certificates, the value must be `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="9f33c-202">For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="9f33c-203">pfx</span><span class="sxs-lookup"><span data-stu-id="9f33c-203">pfx</span></span> |<span data-ttu-id="9f33c-204">Required.</span><span class="sxs-lookup"><span data-stu-id="9f33c-204">Required.</span></span> <span data-ttu-id="9f33c-205">Base64-encoded contents of the PFX file.</span><span class="sxs-lookup"><span data-stu-id="9f33c-205">Base64-encoded contents of the PFX file.</span></span> |
| <span data-ttu-id="9f33c-206">password</span><span class="sxs-lookup"><span data-stu-id="9f33c-206">password</span></span> |<span data-ttu-id="9f33c-207">Required.</span><span class="sxs-lookup"><span data-stu-id="9f33c-207">Required.</span></span> <span data-ttu-id="9f33c-208">Password to access the PFX file.</span><span class="sxs-lookup"><span data-stu-id="9f33c-208">Password to access the PFX file.</span></span> |

### <a name="basic-authentication"></a><span data-ttu-id="9f33c-209">Basic authentication</span><span class="sxs-lookup"><span data-stu-id="9f33c-209">Basic authentication</span></span>

<span data-ttu-id="9f33c-210">To validate the incoming requests, you can use basic authentication, such as username and password.</span><span class="sxs-lookup"><span data-stu-id="9f33c-210">To validate the incoming requests, you can use basic authentication, such as username and password.</span></span> <span data-ttu-id="9f33c-211">Basic authentication is a common pattern, and you can use this authentication in any language used to build your app.</span><span class="sxs-lookup"><span data-stu-id="9f33c-211">Basic authentication is a common pattern, and you can use this authentication in any language used to build your app.</span></span>

<span data-ttu-id="9f33c-212">In the **Authorization** section, you should include:</span><span class="sxs-lookup"><span data-stu-id="9f33c-212">In the **Authorization** section, you should include:</span></span>

<span data-ttu-id="9f33c-213">`{"type": "basic","username": "test","password": "test"}`.</span><span class="sxs-lookup"><span data-stu-id="9f33c-213">`{"type": "basic","username": "test","password": "test"}`.</span></span>

| <span data-ttu-id="9f33c-214">Element</span><span class="sxs-lookup"><span data-stu-id="9f33c-214">Element</span></span> | <span data-ttu-id="9f33c-215">Description</span><span class="sxs-lookup"><span data-stu-id="9f33c-215">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9f33c-216">type</span><span class="sxs-lookup"><span data-stu-id="9f33c-216">type</span></span> |<span data-ttu-id="9f33c-217">Required.</span><span class="sxs-lookup"><span data-stu-id="9f33c-217">Required.</span></span> <span data-ttu-id="9f33c-218">Type of authentication.</span><span class="sxs-lookup"><span data-stu-id="9f33c-218">Type of authentication.</span></span> <span data-ttu-id="9f33c-219">For Basic authentication, the value must be `Basic`.</span><span class="sxs-lookup"><span data-stu-id="9f33c-219">For Basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="9f33c-220">username</span><span class="sxs-lookup"><span data-stu-id="9f33c-220">username</span></span> |<span data-ttu-id="9f33c-221">Required.</span><span class="sxs-lookup"><span data-stu-id="9f33c-221">Required.</span></span> <span data-ttu-id="9f33c-222">Username to authenticate.</span><span class="sxs-lookup"><span data-stu-id="9f33c-222">Username to authenticate.</span></span> |
| <span data-ttu-id="9f33c-223">password</span><span class="sxs-lookup"><span data-stu-id="9f33c-223">password</span></span> |<span data-ttu-id="9f33c-224">Required.</span><span class="sxs-lookup"><span data-stu-id="9f33c-224">Required.</span></span> <span data-ttu-id="9f33c-225">Password to authenticate.</span><span class="sxs-lookup"><span data-stu-id="9f33c-225">Password to authenticate.</span></span> |

### <a name="handle-azure-active-directory-authentication-in-code"></a><span data-ttu-id="9f33c-226">Handle Azure Active Directory authentication in code</span><span class="sxs-lookup"><span data-stu-id="9f33c-226">Handle Azure Active Directory authentication in code</span></span>

<span data-ttu-id="9f33c-227">By default, the Azure Active Directory authentication that you enable in the Azure portal doesn't provide fine-grained authorization.</span><span class="sxs-lookup"><span data-stu-id="9f33c-227">By default, the Azure Active Directory authentication that you enable in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="9f33c-228">For example, this authentication doesn't lock your API to a specific user or app, but just to a particular tenant.</span><span class="sxs-lookup"><span data-stu-id="9f33c-228">For example, this authentication doesn't lock your API to a specific user or app, but just to a particular tenant.</span></span>

<span data-ttu-id="9f33c-229">To restrict your API to your logic app, for example, in code, extract the header that has the JWT.</span><span class="sxs-lookup"><span data-stu-id="9f33c-229">To restrict your API to your logic app, for example, in code, extract the header that has the JWT.</span></span> <span data-ttu-id="9f33c-230">Check the caller's identity, and reject requests that don't match.</span><span class="sxs-lookup"><span data-stu-id="9f33c-230">Check the caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="9f33c-231">Going further, to implement this authentication entirely in your own code, and not use the Azure portal feature, see [Authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="9f33c-231">Going further, to implement this authentication entirely in your own code, and not use the Azure portal feature, see [Authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>
<span data-ttu-id="9f33c-232">To create an Application identity for your logic app and use that identity to call your API, you must follow the previous steps.</span><span class="sxs-lookup"><span data-stu-id="9f33c-232">To create an Application identity for your logic app and use that identity to call your API, you must follow the previous steps.</span></span>
