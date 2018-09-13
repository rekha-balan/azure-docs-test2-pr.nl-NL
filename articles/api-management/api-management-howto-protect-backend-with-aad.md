---
title: Protect a Web API backend with Azure Active Directory and API Management | Microsoft Docs
description: Learn how to protect a Web API backend with Azure Active Directory and API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f0d247547ea7bf20f89423f74247a0ed2a5466fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550305"
---
# <a name="how-to-protect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="db21c-103">How to protect a Web API backend with Azure Active Directory and API Management</span><span class="sxs-lookup"><span data-stu-id="db21c-103">How to protect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="db21c-104">The following video shows how to build a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span><span class="sxs-lookup"><span data-stu-id="db21c-104">The following video shows how to build a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="db21c-105">This article provides an overview and additional information for the steps in the video.</span><span class="sxs-lookup"><span data-stu-id="db21c-105">This article provides an overview and additional information for the steps in the video.</span></span> <span data-ttu-id="db21c-106">This 24 minute video shows you how to:</span><span class="sxs-lookup"><span data-stu-id="db21c-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="db21c-107">Build a Web API backend and secure it with AAD - starting at 1:30</span><span class="sxs-lookup"><span data-stu-id="db21c-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="db21c-108">Import the API into API Management - starting at 7:10</span><span class="sxs-lookup"><span data-stu-id="db21c-108">Import the API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="db21c-109">Configure the Developer portal to call the API - starting at 9:09</span><span class="sxs-lookup"><span data-stu-id="db21c-109">Configure the Developer portal to call the API - starting at 9:09</span></span>
* <span data-ttu-id="db21c-110">Configure a desktop application to call the API - starting at 18:08</span><span class="sxs-lookup"><span data-stu-id="db21c-110">Configure a desktop application to call the API - starting at 18:08</span></span>
* <span data-ttu-id="db21c-111">Configure a JWT validation policy to pre-authorize requests - starting at 20:47</span><span class="sxs-lookup"><span data-stu-id="db21c-111">Configure a JWT validation policy to pre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="db21c-112">Create an Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="db21c-112">Create an Azure AD directory</span></span>
<span data-ttu-id="db21c-113">To secure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="db21c-113">To secure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="db21c-114">In this video a tenant named **APIMDemo** is used.</span><span class="sxs-lookup"><span data-stu-id="db21c-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="db21c-115">To create an AAD tenant, sign-in to the [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span><span class="sxs-lookup"><span data-stu-id="db21c-115">To create an AAD tenant, sign-in to the [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="db21c-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="db21c-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="db21c-118">This directory is used throughout the video.</span><span class="sxs-lookup"><span data-stu-id="db21c-118">This directory is used throughout the video.</span></span>

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="db21c-120">Create a Web API service secured by Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="db21c-120">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="db21c-121">In this step, a Web API backend is created using Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="db21c-121">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="db21c-122">This step of the video starts at 1:30.</span><span class="sxs-lookup"><span data-stu-id="db21c-122">This step of the video starts at 1:30.</span></span> <span data-ttu-id="db21c-123">To create Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from the **Web** templates list.</span><span class="sxs-lookup"><span data-stu-id="db21c-123">To create Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from the **Web** templates list.</span></span> <span data-ttu-id="db21c-124">In this video the project is named **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="db21c-124">In this video the project is named **APIMAADDemo**.</span></span> <span data-ttu-id="db21c-125">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="db21c-125">Click **OK** to create the project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="db21c-127">Click **Web API** from the **Select a template list** to create a Web API project.</span><span class="sxs-lookup"><span data-stu-id="db21c-127">Click **Web API** from the **Select a template list** to create a Web API project.</span></span> <span data-ttu-id="db21c-128">To configure Azure Directory Authentication click **Change Authentication**.</span><span class="sxs-lookup"><span data-stu-id="db21c-128">To configure Azure Directory Authentication click **Change Authentication**.</span></span>

![New project][api-management-new-project]

<span data-ttu-id="db21c-130">Click **Organizational Accounts**, and specify the **Domain** of your AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="db21c-130">Click **Organizational Accounts**, and specify the **Domain** of your AAD tenant.</span></span> <span data-ttu-id="db21c-131">In this example the domain is **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="db21c-131">In this example the domain is **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="db21c-132">The domain of your directory can be obtained from the **Domains** tab of your directory.</span><span class="sxs-lookup"><span data-stu-id="db21c-132">The domain of your directory can be obtained from the **Domains** tab of your directory.</span></span>

![Domains][api-management-aad-domains]

<span data-ttu-id="db21c-134">Configure the desired settings in the **Change Authentication** dialog box and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="db21c-134">Configure the desired settings in the **Change Authentication** dialog box and click **OK**.</span></span>

![Change authentication][api-management-change-authentication]

<span data-ttu-id="db21c-136">When you click **OK** Visual Studio will attempt to register your application with your Azure AD directory and you may be prompted to sign in by Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db21c-136">When you click **OK** Visual Studio will attempt to register your application with your Azure AD directory and you may be prompted to sign in by Visual Studio.</span></span> <span data-ttu-id="db21c-137">Sign in using an administrative account for your directory.</span><span class="sxs-lookup"><span data-stu-id="db21c-137">Sign in using an administrative account for your directory.</span></span>

![Sign in to Visual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="db21c-139">To configure this project as an Azure Web API check the box for **Host in the cloud** and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="db21c-139">To configure this project as an Azure Web API check the box for **Host in the cloud** and then click **OK**.</span></span>

![New project][api-management-new-project-cloud]

<span data-ttu-id="db21c-141">You may be prompted to sign in to Azure, and then you can configure the Web App.</span><span class="sxs-lookup"><span data-stu-id="db21c-141">You may be prompted to sign in to Azure, and then you can configure the Web App.</span></span>

![Configure][api-management-configure-web-app]

<span data-ttu-id="db21c-143">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span><span class="sxs-lookup"><span data-stu-id="db21c-143">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="db21c-144">Click **OK** to configure the Web App and create the project.</span><span class="sxs-lookup"><span data-stu-id="db21c-144">Click **OK** to configure the Web App and create the project.</span></span>

## <a name="add-the-code-to-the-web-api-project"></a><span data-ttu-id="db21c-145">Add the code to the Web API project</span><span class="sxs-lookup"><span data-stu-id="db21c-145">Add the code to the Web API project</span></span>
<span data-ttu-id="db21c-146">The next step in the video adds the code to the Web API project.</span><span class="sxs-lookup"><span data-stu-id="db21c-146">The next step in the video adds the code to the Web API project.</span></span> <span data-ttu-id="db21c-147">This step starts at 4:35.</span><span class="sxs-lookup"><span data-stu-id="db21c-147">This step starts at 4:35.</span></span>

<span data-ttu-id="db21c-148">The Web API in this example implements a basic calculator service using a model and a controller.</span><span class="sxs-lookup"><span data-stu-id="db21c-148">The Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="db21c-149">To add the model for the service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span><span class="sxs-lookup"><span data-stu-id="db21c-149">To add the model for the service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="db21c-150">Name the class `CalcInput` and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="db21c-150">Name the class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="db21c-151">Add the following `using` statement to the top of the `CalcInput.cs` file.</span><span class="sxs-lookup"><span data-stu-id="db21c-151">Add the following `using` statement to the top of the `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="db21c-152">Replace the generated class with the following code.</span><span class="sxs-lookup"><span data-stu-id="db21c-152">Replace the generated class with the following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="db21c-153">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span><span class="sxs-lookup"><span data-stu-id="db21c-153">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="db21c-154">Choose **Web API 2 Controller - Empty** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="db21c-154">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="db21c-155">Type **CalcController** for the Controller name and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="db21c-155">Type **CalcController** for the Controller name and click **Add**.</span></span>

![Add Controller][api-management-add-controller]

<span data-ttu-id="db21c-157">Add the following `using` statement to the top of the `CalcController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="db21c-157">Add the following `using` statement to the top of the `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="db21c-158">Replace the generated controller class with the following code.</span><span class="sxs-lookup"><span data-stu-id="db21c-158">Replace the generated controller class with the following code.</span></span> <span data-ttu-id="db21c-159">This code implements the `Add`, `Subtract`, `Multiply`, and `Divide` operations of the Basic Calculator API.</span><span class="sxs-lookup"><span data-stu-id="db21c-159">This code implements the `Add`, `Subtract`, `Multiply`, and `Divide` operations of the Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="db21c-160">Press **F6** to build and verify the solution.</span><span class="sxs-lookup"><span data-stu-id="db21c-160">Press **F6** to build and verify the solution.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="db21c-161">Publish the project to Azure</span><span class="sxs-lookup"><span data-stu-id="db21c-161">Publish the project to Azure</span></span>
<span data-ttu-id="db21c-162">In this step the Visual Studio project is published to Azure.</span><span class="sxs-lookup"><span data-stu-id="db21c-162">In this step the Visual Studio project is published to Azure.</span></span> <span data-ttu-id="db21c-163">This step of the video starts at 5:45.</span><span class="sxs-lookup"><span data-stu-id="db21c-163">This step of the video starts at 5:45.</span></span>

<span data-ttu-id="db21c-164">To publish the project to Azure, right-click the **APIMAADDemo** project in Visual Studio and choose **Publish**.</span><span class="sxs-lookup"><span data-stu-id="db21c-164">To publish the project to Azure, right-click the **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="db21c-165">Keep the default settings in the **Publish Web** dialog box and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="db21c-165">Keep the default settings in the **Publish Web** dialog box and click **Publish**.</span></span>

![Web Publish][api-management-web-publish]

## <a name="grant-permissions-to-the-azure-ad-backend-service-application"></a><span data-ttu-id="db21c-167">Grant permissions to the Azure AD backend service application</span><span class="sxs-lookup"><span data-stu-id="db21c-167">Grant permissions to the Azure AD backend service application</span></span>
<span data-ttu-id="db21c-168">A new application for the backend service is created in your Azure AD directory as part of the configuring and publishing process of your Web API project.</span><span class="sxs-lookup"><span data-stu-id="db21c-168">A new application for the backend service is created in your Azure AD directory as part of the configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="db21c-169">In this step of the video, starting at 6:13, permissions are granted to the Web API backend.</span><span class="sxs-lookup"><span data-stu-id="db21c-169">In this step of the video, starting at 6:13, permissions are granted to the Web API backend.</span></span>

![Application][api-management-aad-backend-app]

<span data-ttu-id="db21c-171">Click the name of the application to configure the required permissions.</span><span class="sxs-lookup"><span data-stu-id="db21c-171">Click the name of the application to configure the required permissions.</span></span> <span data-ttu-id="db21c-172">Navigate to the **Configure** tab and scroll down to the **permissions to other applications** section.</span><span class="sxs-lookup"><span data-stu-id="db21c-172">Navigate to the **Configure** tab and scroll down to the **permissions to other applications** section.</span></span> <span data-ttu-id="db21c-173">Click the **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check the box for **Read directory data**, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="db21c-173">Click the **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check the box for **Read directory data**, and click **Save**.</span></span>

![Add permissions][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="db21c-175">If **Windows** **Azure Active Directory** is not listed under permissions to other applications, click **Add application** and add it from the list.</span><span class="sxs-lookup"><span data-stu-id="db21c-175">If **Windows** **Azure Active Directory** is not listed under permissions to other applications, click **Add application** and add it from the list.</span></span>
> 
> 

<span data-ttu-id="db21c-176">Make a note of the **App Id URI** for use in a subsequent step when an Azure AD application is configured for the API Management developer portal.</span><span class="sxs-lookup"><span data-stu-id="db21c-176">Make a note of the **App Id URI** for use in a subsequent step when an Azure AD application is configured for the API Management developer portal.</span></span>

![App Id URI][api-management-aad-sso-uri]

## <a name="import-the-web-api-into-api-management"></a><span data-ttu-id="db21c-178">Import the Web API into API Management</span><span class="sxs-lookup"><span data-stu-id="db21c-178">Import the Web API into API Management</span></span>
<span data-ttu-id="db21c-179">APIs are configured from the API publisher portal, which is accessed through the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="db21c-179">APIs are configured from the API publisher portal, which is accessed through the Azure Portal.</span></span> <span data-ttu-id="db21c-180">To reach it, click **Publisher portal** from the toolbar of your API Management service.</span><span class="sxs-lookup"><span data-stu-id="db21c-180">To reach it, click **Publisher portal** from the toolbar of your API Management service.</span></span> <span data-ttu-id="db21c-181">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API][Manage your first API] tutorial.</span><span class="sxs-lookup"><span data-stu-id="db21c-181">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API][Manage your first API] tutorial.</span></span>

![Publisher portal][api-management-management-console]

<span data-ttu-id="db21c-183">Operations can be [added to APIs manually](api-management-howto-add-operations.md), or they can be imported.</span><span class="sxs-lookup"><span data-stu-id="db21c-183">Operations can be [added to APIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="db21c-184">In this video, operations are imported in Swagger format starting at 6:40.</span><span class="sxs-lookup"><span data-stu-id="db21c-184">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="db21c-185">Create a file named `calcapi.json` with following contents and save it to your computer.</span><span class="sxs-lookup"><span data-stu-id="db21c-185">Create a file named `calcapi.json` with following contents and save it to your computer.</span></span> <span data-ttu-id="db21c-186">Ensure that the `host` attribute points to your Web API backend.</span><span class="sxs-lookup"><span data-stu-id="db21c-186">Ensure that the `host` attribute points to your Web API backend.</span></span> <span data-ttu-id="db21c-187">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span><span class="sxs-lookup"><span data-stu-id="db21c-187">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="db21c-188">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span><span class="sxs-lookup"><span data-stu-id="db21c-188">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Import API button][api-management-import-api]

<span data-ttu-id="db21c-190">Perform the following steps to configure the calculator API.</span><span class="sxs-lookup"><span data-stu-id="db21c-190">Perform the following steps to configure the calculator API.</span></span>

1. <span data-ttu-id="db21c-191">Click **From file**, browse to the `calculator.json` file you saved, and click the **Swagger** radio button.</span><span class="sxs-lookup"><span data-stu-id="db21c-191">Click **From file**, browse to the `calculator.json` file you saved, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="db21c-192">Type **calc** into the **Web API URL suffix** textbox.</span><span class="sxs-lookup"><span data-stu-id="db21c-192">Type **calc** into the **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="db21c-193">Click in the **Products (optional)** box and choose **Starter**.</span><span class="sxs-lookup"><span data-stu-id="db21c-193">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="db21c-194">Click **Save** to import the API.</span><span class="sxs-lookup"><span data-stu-id="db21c-194">Click **Save** to import the API.</span></span>

![Add new API][api-management-import-new-api]

<span data-ttu-id="db21c-196">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="db21c-196">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

## <a name="call-the-api-unsuccessfully-from-the-developer-portal"></a><span data-ttu-id="db21c-197">Call the API unsuccessfully from the developer portal</span><span class="sxs-lookup"><span data-stu-id="db21c-197">Call the API unsuccessfully from the developer portal</span></span>
<span data-ttu-id="db21c-198">At this point, the API has been imported into API Management, but cannot yet be called successfully from the developer portal because the backend service is protected with Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="db21c-198">At this point, the API has been imported into API Management, but cannot yet be called successfully from the developer portal because the backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="db21c-199">This is demonstrated in the video starting at 7:40 using the following steps.</span><span class="sxs-lookup"><span data-stu-id="db21c-199">This is demonstrated in the video starting at 7:40 using the following steps.</span></span>

<span data-ttu-id="db21c-200">Click **Developer portal** from the top-right side of the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="db21c-200">Click **Developer portal** from the top-right side of the publisher portal.</span></span>

![Developer portal][api-management-developer-portal-menu]

<span data-ttu-id="db21c-202">Click **APIs** and click the **Calculator** API.</span><span class="sxs-lookup"><span data-stu-id="db21c-202">Click **APIs** and click the **Calculator** API.</span></span>

![Developer portal][api-management-dev-portal-apis]

<span data-ttu-id="db21c-204">Click **Try it**.</span><span class="sxs-lookup"><span data-stu-id="db21c-204">Click **Try it**.</span></span>

![Try it][api-management-dev-portal-try-it]

<span data-ttu-id="db21c-206">Click **Send** and note the response status of **401 Unauthorized**.</span><span class="sxs-lookup"><span data-stu-id="db21c-206">Click **Send** and note the response status of **401 Unauthorized**.</span></span>

![Send][api-management-dev-portal-send-401]

<span data-ttu-id="db21c-208">The request is unauthorized because the backend API is protected by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db21c-208">The request is unauthorized because the backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="db21c-209">Before successfully calling the API the developer portal must be configured to authorize developers using OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="db21c-209">Before successfully calling the API the developer portal must be configured to authorize developers using OAuth 2.0.</span></span> <span data-ttu-id="db21c-210">This process is described in the following sections.</span><span class="sxs-lookup"><span data-stu-id="db21c-210">This process is described in the following sections.</span></span>

## <a name="register-the-developer-portal-as-an-aad-application"></a><span data-ttu-id="db21c-211">Register the developer portal as an AAD application</span><span class="sxs-lookup"><span data-stu-id="db21c-211">Register the developer portal as an AAD application</span></span>
<span data-ttu-id="db21c-212">The first step in configuring the developer portal to authorize developers using OAuth 2.0 is to register the developer portal as an AAD application.</span><span class="sxs-lookup"><span data-stu-id="db21c-212">The first step in configuring the developer portal to authorize developers using OAuth 2.0 is to register the developer portal as an AAD application.</span></span> <span data-ttu-id="db21c-213">This is demonstrated starting at 8:27 in the video.</span><span class="sxs-lookup"><span data-stu-id="db21c-213">This is demonstrated starting at 8:27 in the video.</span></span>

<span data-ttu-id="db21c-214">Navigate to the Azure AD tenant from the first step of this video, in this example **APIMDemo** and navigate to the **Applications** tab.</span><span class="sxs-lookup"><span data-stu-id="db21c-214">Navigate to the Azure AD tenant from the first step of this video, in this example **APIMDemo** and navigate to the **Applications** tab.</span></span>

![New application][api-management-aad-new-application-devportal]

<span data-ttu-id="db21c-216">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span><span class="sxs-lookup"><span data-stu-id="db21c-216">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![New application][api-management-new-aad-application-menu]

<span data-ttu-id="db21c-218">Choose **Web application and/or Web API**, enter a name, and click the next arrow.</span><span class="sxs-lookup"><span data-stu-id="db21c-218">Choose **Web application and/or Web API**, enter a name, and click the next arrow.</span></span> <span data-ttu-id="db21c-219">In this example **APIMDeveloperPortal** is used.</span><span class="sxs-lookup"><span data-stu-id="db21c-219">In this example **APIMDeveloperPortal** is used.</span></span>

![New application][api-management-aad-new-application-devportal-1]

<span data-ttu-id="db21c-221">For **Sign-on URL** enter the URL of your API Management service and append `/signin`.</span><span class="sxs-lookup"><span data-stu-id="db21c-221">For **Sign-on URL** enter the URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="db21c-222">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span><span class="sxs-lookup"><span data-stu-id="db21c-222">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="db21c-223">For **App Id URL** enter the URL of your API Management service and append some unique characters.</span><span class="sxs-lookup"><span data-stu-id="db21c-223">For **App Id URL** enter the URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="db21c-224">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span><span class="sxs-lookup"><span data-stu-id="db21c-224">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="db21c-225">When the  desired **App properties** are configured, click the check mark to create the application.</span><span class="sxs-lookup"><span data-stu-id="db21c-225">When the  desired **App properties** are configured, click the check mark to create the application.</span></span>

![New application][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="db21c-227">Configure an API Management OAuth 2.0 authorization server</span><span class="sxs-lookup"><span data-stu-id="db21c-227">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="db21c-228">The next step is to configure an OAuth 2.0 authorization server in API Management.</span><span class="sxs-lookup"><span data-stu-id="db21c-228">The next step is to configure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="db21c-229">This step is demonstrated in the video starting at 9:43.</span><span class="sxs-lookup"><span data-stu-id="db21c-229">This step is demonstrated in the video starting at 9:43.</span></span>

<span data-ttu-id="db21c-230">Click **Security** from the API Management menu on the left, click **OAuth 2.0**, and then click **Add authorization** server.</span><span class="sxs-lookup"><span data-stu-id="db21c-230">Click **Security** from the API Management menu on the left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Add authorization server][api-management-add-authorization-server]

<span data-ttu-id="db21c-232">Enter a name and an optional description in the **Name** and **Description** fields.</span><span class="sxs-lookup"><span data-stu-id="db21c-232">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> <span data-ttu-id="db21c-233">These fields are used to identify the OAuth 2.0 authorization server within the API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="db21c-233">These fields are used to identify the OAuth 2.0 authorization server within the API Management service instance.</span></span> <span data-ttu-id="db21c-234">In this example **Authorization server demo** is used.</span><span class="sxs-lookup"><span data-stu-id="db21c-234">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="db21c-235">Later when you specify an OAuth 2.0 server to be used for authentication for an API, you will select this name.</span><span class="sxs-lookup"><span data-stu-id="db21c-235">Later when you specify an OAuth 2.0 server to be used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="db21c-236">For the **Client registration page URL** enter a placeholder value such as `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="db21c-236">For the **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="db21c-237">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span><span class="sxs-lookup"><span data-stu-id="db21c-237">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="db21c-238">In this example users do not create and configure their own accounts so a placeholder is used.</span><span class="sxs-lookup"><span data-stu-id="db21c-238">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Add authorization server][api-management-add-authorization-server-1]

<span data-ttu-id="db21c-240">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span><span class="sxs-lookup"><span data-stu-id="db21c-240">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Authorization server][api-management-add-authorization-server-1a]

<span data-ttu-id="db21c-242">These values can be retrieved from the **App Endpoints** page of the AAD application you created for the developer portal.</span><span class="sxs-lookup"><span data-stu-id="db21c-242">These values can be retrieved from the **App Endpoints** page of the AAD application you created for the developer portal.</span></span> <span data-ttu-id="db21c-243">To access the endpoints navigate to the **Configure** tab for the AAD application and click **View endpoints**.</span><span class="sxs-lookup"><span data-stu-id="db21c-243">To access the endpoints navigate to the **Configure** tab for the AAD application and click **View endpoints**.</span></span>

![Application][api-management-aad-devportal-application]

![View endpoints][api-management-aad-view-endpoints]

<span data-ttu-id="db21c-246">Copy the **OAuth 2.0 authorization endpoint** and paste it into the **Authorization endpoint URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="db21c-246">Copy the **OAuth 2.0 authorization endpoint** and paste it into the **Authorization endpoint URL** textbox.</span></span>

![Add authorization server][api-management-add-authorization-server-2]

<span data-ttu-id="db21c-248">Copy the **OAuth 2.0 token endpoint** and paste it into the **Token endpoint URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="db21c-248">Copy the **OAuth 2.0 token endpoint** and paste it into the **Token endpoint URL** textbox.</span></span>

![Add authorization server][api-management-add-authorization-server-2a]

<span data-ttu-id="db21c-250">In addition to pasting in the token endpoint, add an additional body parameter named **resource** and for the value use the **App Id URI** from the AAD application for the backend service that was created when the Visual Studio project was published.</span><span class="sxs-lookup"><span data-stu-id="db21c-250">In addition to pasting in the token endpoint, add an additional body parameter named **resource** and for the value use the **App Id URI** from the AAD application for the backend service that was created when the Visual Studio project was published.</span></span>

![App Id URI][api-management-aad-sso-uri]

<span data-ttu-id="db21c-252">Next, specify the client credentials.</span><span class="sxs-lookup"><span data-stu-id="db21c-252">Next, specify the client credentials.</span></span> <span data-ttu-id="db21c-253">These are the credentials for the resource you want to access, in this case the developer portal.</span><span class="sxs-lookup"><span data-stu-id="db21c-253">These are the credentials for the resource you want to access, in this case the developer portal.</span></span>

![Client credentials][api-management-client-credentials]

<span data-ttu-id="db21c-255">To get the **Client Id**, navigate to the **Configure** tab of the AAD application for the developer portal and copy the **Client Id**.</span><span class="sxs-lookup"><span data-stu-id="db21c-255">To get the **Client Id**, navigate to the **Configure** tab of the AAD application for the developer portal and copy the **Client Id**.</span></span>

<span data-ttu-id="db21c-256">To get the **Client Secret** click the **Select duration** drop-down in the **Keys** section and specify an interval.</span><span class="sxs-lookup"><span data-stu-id="db21c-256">To get the **Client Secret** click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="db21c-257">In this example 1 year is used.</span><span class="sxs-lookup"><span data-stu-id="db21c-257">In this example 1 year is used.</span></span>

![Client ID][api-management-aad-client-id]

<span data-ttu-id="db21c-259">Click **Save** to save the configuration and display the key.</span><span class="sxs-lookup"><span data-stu-id="db21c-259">Click **Save** to save the configuration and display the key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="db21c-260">Make a note of this key.</span><span class="sxs-lookup"><span data-stu-id="db21c-260">Make a note of this key.</span></span> <span data-ttu-id="db21c-261">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span><span class="sxs-lookup"><span data-stu-id="db21c-261">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="db21c-262">Copy the key to the clipboard, switch back to the publisher portal, paste the key into the **Client Secret** textbox, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="db21c-262">Copy the key to the clipboard, switch back to the publisher portal, paste the key into the **Client Secret** textbox, and click **Save**.</span></span>

![Add authorization server][api-management-add-authorization-server-3]

<span data-ttu-id="db21c-264">Immediately following the client credentials is an authorization code grant.</span><span class="sxs-lookup"><span data-stu-id="db21c-264">Immediately following the client credentials is an authorization code grant.</span></span> <span data-ttu-id="db21c-265">Copy this authorization code and switch back to your Azure AD developer portal application configure page, and paste the authorization grant into the **Reply URL** field, and click **Save** again.</span><span class="sxs-lookup"><span data-stu-id="db21c-265">Copy this authorization code and switch back to your Azure AD developer portal application configure page, and paste the authorization grant into the **Reply URL** field, and click **Save** again.</span></span>

![Reply URL][api-management-aad-reply-url]

<span data-ttu-id="db21c-267">The next step is to configure the permissions for the developer portal AAD application.</span><span class="sxs-lookup"><span data-stu-id="db21c-267">The next step is to configure the permissions for the developer portal AAD application.</span></span> <span data-ttu-id="db21c-268">Click **Application Permissions** and check the box for **Read directory data**.</span><span class="sxs-lookup"><span data-stu-id="db21c-268">Click **Application Permissions** and check the box for **Read directory data**.</span></span> <span data-ttu-id="db21c-269">Click **Save** to save this change, and then click **Add application**.</span><span class="sxs-lookup"><span data-stu-id="db21c-269">Click **Save** to save this change, and then click **Add application**.</span></span>

![Add permissions][api-management-add-devportal-permissions]

<span data-ttu-id="db21c-271">Click the search icon, type **APIM** into the Starting with box, select **APIMAADDemo**, and click the check mark to save.</span><span class="sxs-lookup"><span data-stu-id="db21c-271">Click the search icon, type **APIM** into the Starting with box, select **APIMAADDemo**, and click the check mark to save.</span></span>

![Add permissions][api-management-aad-add-app-permissions]

<span data-ttu-id="db21c-273">Click **Delegated Permissions** for **APIMAADDemo** and check the box for **Access APIMAADDemo**, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="db21c-273">Click **Delegated Permissions** for **APIMAADDemo** and check the box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="db21c-274">This allows the developer portal application to access the backend service.</span><span class="sxs-lookup"><span data-stu-id="db21c-274">This allows the developer portal application to access the backend service.</span></span>

![Add permissions][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-the-calculator-api"></a><span data-ttu-id="db21c-276">Enable OAuth 2.0 user authorization for the Calculator API</span><span class="sxs-lookup"><span data-stu-id="db21c-276">Enable OAuth 2.0 user authorization for the Calculator API</span></span>
<span data-ttu-id="db21c-277">Now that the OAuth 2.0 server is configured, you can specify it in the security settings for your API.</span><span class="sxs-lookup"><span data-stu-id="db21c-277">Now that the OAuth 2.0 server is configured, you can specify it in the security settings for your API.</span></span> <span data-ttu-id="db21c-278">This step is demonstrated in the video starting at 14:30.</span><span class="sxs-lookup"><span data-stu-id="db21c-278">This step is demonstrated in the video starting at 14:30.</span></span>

<span data-ttu-id="db21c-279">Click **APIs** in the left menu, and click  **Calculator** to view and configure its settings.</span><span class="sxs-lookup"><span data-stu-id="db21c-279">Click **APIs** in the left menu, and click  **Calculator** to view and configure its settings.</span></span>

![Calculator API][api-management-calc-api]

<span data-ttu-id="db21c-281">Navigate to the **Security** tab, check the **OAuth 2.0** checkbox, select the desired authorization server from the **Authorization server** drop-down, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="db21c-281">Navigate to the **Security** tab, check the **OAuth 2.0** checkbox, select the desired authorization server from the **Authorization server** drop-down, and click **Save**.</span></span>

![Calculator API][api-management-enable-aad-calculator]

## <a name="successfully-call-the-calculator-api-from-the-developer-portal"></a><span data-ttu-id="db21c-283">Successfully call the Calculator API from the developer portal</span><span class="sxs-lookup"><span data-stu-id="db21c-283">Successfully call the Calculator API from the developer portal</span></span>
<span data-ttu-id="db21c-284">Now that the OAuth 2.0 authorization is configured on the API, its operations can be successfully called from the developer center.</span><span class="sxs-lookup"><span data-stu-id="db21c-284">Now that the OAuth 2.0 authorization is configured on the API, its operations can be successfully called from the developer center.</span></span> <span data-ttu-id="db21c-285">THis step is demonstrated in the video starting at 15:00.</span><span class="sxs-lookup"><span data-stu-id="db21c-285">THis step is demonstrated in the video starting at 15:00.</span></span>

<span data-ttu-id="db21c-286">Navigate back to the **Add two integers** operation of the calculator service in the developer portal and click **Try it**.</span><span class="sxs-lookup"><span data-stu-id="db21c-286">Navigate back to the **Add two integers** operation of the calculator service in the developer portal and click **Try it**.</span></span> <span data-ttu-id="db21c-287">Note the new item in the **Authorization** section corresponding to the authorization server you just added.</span><span class="sxs-lookup"><span data-stu-id="db21c-287">Note the new item in the **Authorization** section corresponding to the authorization server you just added.</span></span>

![Calculator API][api-management-calc-authorization-server]

<span data-ttu-id="db21c-289">Select **Authorization code** from the authorization drop-down list and enter the credentials of the account to use.</span><span class="sxs-lookup"><span data-stu-id="db21c-289">Select **Authorization code** from the authorization drop-down list and enter the credentials of the account to use.</span></span> <span data-ttu-id="db21c-290">If you are already signed in with the account you may not be prompted.</span><span class="sxs-lookup"><span data-stu-id="db21c-290">If you are already signed in with the account you may not be prompted.</span></span>

![Calculator API][api-management-devportal-authorization-code]

<span data-ttu-id="db21c-292">Click **Send** and note the **Response status** of **200 OK** and the results of the operation in the response content.</span><span class="sxs-lookup"><span data-stu-id="db21c-292">Click **Send** and note the **Response status** of **200 OK** and the results of the operation in the response content.</span></span>

![Calculator API][api-management-devportal-response]

## <a name="configure-a-desktop-application-to-call-the-api"></a><span data-ttu-id="db21c-294">Configure a desktop application to call the API</span><span class="sxs-lookup"><span data-stu-id="db21c-294">Configure a desktop application to call the API</span></span>
<span data-ttu-id="db21c-295">The next procedure in the video starts at 16:30 and configures a simple desktop application to call the API.</span><span class="sxs-lookup"><span data-stu-id="db21c-295">The next procedure in the video starts at 16:30 and configures a simple desktop application to call the API.</span></span> <span data-ttu-id="db21c-296">The first step is to register the desktop application in Azure AD and give it access to the directory and to the backend service.</span><span class="sxs-lookup"><span data-stu-id="db21c-296">The first step is to register the desktop application in Azure AD and give it access to the directory and to the backend service.</span></span> <span data-ttu-id="db21c-297">At 18:25 there is a demonstration of the desktop application calling an operation on the calculator API.</span><span class="sxs-lookup"><span data-stu-id="db21c-297">At 18:25 there is a demonstration of the desktop application calling an operation on the calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-to-pre-authorize-requests"></a><span data-ttu-id="db21c-298">Configure a JWT validation policy to pre-authorize requests</span><span class="sxs-lookup"><span data-stu-id="db21c-298">Configure a JWT validation policy to pre-authorize requests</span></span>
<span data-ttu-id="db21c-299">The final procedure in the video starts at 20:48 and shows you how to use the [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy to pre-authorize requests by validating the access tokens of each incoming request.</span><span class="sxs-lookup"><span data-stu-id="db21c-299">The final procedure in the video starts at 20:48 and shows you how to use the [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy to pre-authorize requests by validating the access tokens of each incoming request.</span></span> <span data-ttu-id="db21c-300">If the request is not validated by the Validate JWT policy, the request is blocked by API Management and is not passed along to the backend.</span><span class="sxs-lookup"><span data-stu-id="db21c-300">If the request is not validated by the Validate JWT policy, the request is blocked by API Management and is not passed along to the backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.windows.net/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="db21c-301">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span><span class="sxs-lookup"><span data-stu-id="db21c-301">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="db21c-302">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span><span class="sxs-lookup"><span data-stu-id="db21c-302">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db21c-303">Next steps</span><span class="sxs-lookup"><span data-stu-id="db21c-303">Next steps</span></span>
* <span data-ttu-id="db21c-304">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span><span class="sxs-lookup"><span data-stu-id="db21c-304">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="db21c-305">For other ways to secure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="db21c-305">For other ways to secure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md












































