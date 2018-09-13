---
title: Integrate REST API claim exchanges in your Azure Active Directory B2C user journey | Microsoft Docs
description: Integrate REST API claim exchanges in your Azure AD B2C user journey as validation of user input.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 09/30/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: e3d938c4464fc5141b97f85220bf096920e17d00
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855787"
---
# <a name="integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-of-user-input"></a><span data-ttu-id="f8a47-103">Integrate REST API claims exchanges in your Azure AD B2C user journey as validation of user input</span><span class="sxs-lookup"><span data-stu-id="f8a47-103">Integrate REST API claims exchanges in your Azure AD B2C user journey as validation of user input</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="f8a47-104">With the Identity Experience Framework, which underlies Azure Active Directory B2C (Azure AD B2C), you can integrate with a RESTful API in a user journey.</span><span class="sxs-lookup"><span data-stu-id="f8a47-104">With the Identity Experience Framework, which underlies Azure Active Directory B2C (Azure AD B2C), you can integrate with a RESTful API in a user journey.</span></span> <span data-ttu-id="f8a47-105">In this walkthrough, you'll learn how Azure AD B2C interacts with .NET Framework RESTful services (web API).</span><span class="sxs-lookup"><span data-stu-id="f8a47-105">In this walkthrough, you'll learn how Azure AD B2C interacts with .NET Framework RESTful services (web API).</span></span>

## <a name="introduction"></a><span data-ttu-id="f8a47-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="f8a47-106">Introduction</span></span>
<span data-ttu-id="f8a47-107">By using Azure AD B2C, you can add your own business logic to a user journey by calling your own RESTful service.</span><span class="sxs-lookup"><span data-stu-id="f8a47-107">By using Azure AD B2C, you can add your own business logic to a user journey by calling your own RESTful service.</span></span> <span data-ttu-id="f8a47-108">The Identity Experience Framework sends data to the RESTful service in an *Input claims* collection and receives data back from RESTful in an *Output claims* collection.</span><span class="sxs-lookup"><span data-stu-id="f8a47-108">The Identity Experience Framework sends data to the RESTful service in an *Input claims* collection and receives data back from RESTful in an *Output claims* collection.</span></span> <span data-ttu-id="f8a47-109">With RESTful service integration, you can:</span><span class="sxs-lookup"><span data-stu-id="f8a47-109">With RESTful service integration, you can:</span></span>

* <span data-ttu-id="f8a47-110">**Validate user input data**: This action prevents malformed data from persisting into Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8a47-110">**Validate user input data**: This action prevents malformed data from persisting into Azure AD.</span></span> <span data-ttu-id="f8a47-111">If the value from the user is not valid, your RESTful service returns an error message that instructs the user to provide an entry.</span><span class="sxs-lookup"><span data-stu-id="f8a47-111">If the value from the user is not valid, your RESTful service returns an error message that instructs the user to provide an entry.</span></span> <span data-ttu-id="f8a47-112">For example, you can verify that the email address provided by the user exists in your customer's database.</span><span class="sxs-lookup"><span data-stu-id="f8a47-112">For example, you can verify that the email address provided by the user exists in your customer's database.</span></span>
* <span data-ttu-id="f8a47-113">**Overwrite input claims**: For example, if a user enters the first name in all lowercase or all uppercase letters, you can format the name with only the first letter capitalized.</span><span class="sxs-lookup"><span data-stu-id="f8a47-113">**Overwrite input claims**: For example, if a user enters the first name in all lowercase or all uppercase letters, you can format the name with only the first letter capitalized.</span></span>
* <span data-ttu-id="f8a47-114">**Enrich user data by further integrating with corporate line-of-business applications**: Your RESTful service can receive the user's email address, query the customer's database, and return the user's loyalty number to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f8a47-114">**Enrich user data by further integrating with corporate line-of-business applications**: Your RESTful service can receive the user's email address, query the customer's database, and return the user's loyalty number to Azure AD B2C.</span></span> <span data-ttu-id="f8a47-115">The return claims can be stored in the user's Azure AD account, evaluated in the next *Orchestration Steps*, or included in the access token.</span><span class="sxs-lookup"><span data-stu-id="f8a47-115">The return claims can be stored in the user's Azure AD account, evaluated in the next *Orchestration Steps*, or included in the access token.</span></span>
* <span data-ttu-id="f8a47-116">**Run custom business logic**: You can send push notifications, update corporate databases, run a user migration process, manage permissions, audit databases, and perform other actions.</span><span class="sxs-lookup"><span data-stu-id="f8a47-116">**Run custom business logic**: You can send push notifications, update corporate databases, run a user migration process, manage permissions, audit databases, and perform other actions.</span></span>

<span data-ttu-id="f8a47-117">You can design the integration with the RESTful services in the following ways:</span><span class="sxs-lookup"><span data-stu-id="f8a47-117">You can design the integration with the RESTful services in the following ways:</span></span>

* <span data-ttu-id="f8a47-118">**Validation technical profile**: The call to the RESTful service happens within the validation technical profile of the specified technical profile.</span><span class="sxs-lookup"><span data-stu-id="f8a47-118">**Validation technical profile**: The call to the RESTful service happens within the validation technical profile of the specified technical profile.</span></span> <span data-ttu-id="f8a47-119">The validation technical profile validates the user-provided data before the user journey moves forward.</span><span class="sxs-lookup"><span data-stu-id="f8a47-119">The validation technical profile validates the user-provided data before the user journey moves forward.</span></span> <span data-ttu-id="f8a47-120">With the validation technical profile, you can:</span><span class="sxs-lookup"><span data-stu-id="f8a47-120">With the validation technical profile, you can:</span></span>
   * <span data-ttu-id="f8a47-121">Send input claims.</span><span class="sxs-lookup"><span data-stu-id="f8a47-121">Send input claims.</span></span>
   * <span data-ttu-id="f8a47-122">Validate the input claims and throw custom error messages.</span><span class="sxs-lookup"><span data-stu-id="f8a47-122">Validate the input claims and throw custom error messages.</span></span>
   * <span data-ttu-id="f8a47-123">Send back output claims.</span><span class="sxs-lookup"><span data-stu-id="f8a47-123">Send back output claims.</span></span>

* <span data-ttu-id="f8a47-124">**Claims exchange**: This design is similar to the validation technical profile, but it happens within an orchestration step.</span><span class="sxs-lookup"><span data-stu-id="f8a47-124">**Claims exchange**: This design is similar to the validation technical profile, but it happens within an orchestration step.</span></span> <span data-ttu-id="f8a47-125">This definition is limited to:</span><span class="sxs-lookup"><span data-stu-id="f8a47-125">This definition is limited to:</span></span>
   * <span data-ttu-id="f8a47-126">Send input claims.</span><span class="sxs-lookup"><span data-stu-id="f8a47-126">Send input claims.</span></span>
   * <span data-ttu-id="f8a47-127">Send back output claims.</span><span class="sxs-lookup"><span data-stu-id="f8a47-127">Send back output claims.</span></span>

## <a name="restful-walkthrough"></a><span data-ttu-id="f8a47-128">RESTful walkthrough</span><span class="sxs-lookup"><span data-stu-id="f8a47-128">RESTful walkthrough</span></span>
<span data-ttu-id="f8a47-129">In this walkthrough, you develop a .NET Framework web API that validates the user input and provides a user loyalty number.</span><span class="sxs-lookup"><span data-stu-id="f8a47-129">In this walkthrough, you develop a .NET Framework web API that validates the user input and provides a user loyalty number.</span></span> <span data-ttu-id="f8a47-130">For example, your application can grant access to *platinum benefits* based on the loyalty number.</span><span class="sxs-lookup"><span data-stu-id="f8a47-130">For example, your application can grant access to *platinum benefits* based on the loyalty number.</span></span>

<span data-ttu-id="f8a47-131">Overview:</span><span class="sxs-lookup"><span data-stu-id="f8a47-131">Overview:</span></span>
* <span data-ttu-id="f8a47-132">Develop the RESTful service (.NET Framework web API).</span><span class="sxs-lookup"><span data-stu-id="f8a47-132">Develop the RESTful service (.NET Framework web API).</span></span>
* <span data-ttu-id="f8a47-133">Use the RESTful service in the user journey.</span><span class="sxs-lookup"><span data-stu-id="f8a47-133">Use the RESTful service in the user journey.</span></span>
* <span data-ttu-id="f8a47-134">Send input claims and read them in your code.</span><span class="sxs-lookup"><span data-stu-id="f8a47-134">Send input claims and read them in your code.</span></span>
* <span data-ttu-id="f8a47-135">Validate the user's first name.</span><span class="sxs-lookup"><span data-stu-id="f8a47-135">Validate the user's first name.</span></span>
* <span data-ttu-id="f8a47-136">Send back a loyalty number.</span><span class="sxs-lookup"><span data-stu-id="f8a47-136">Send back a loyalty number.</span></span> 
* <span data-ttu-id="f8a47-137">Add the loyalty number to a JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="f8a47-137">Add the loyalty number to a JSON Web Token (JWT).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8a47-138">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f8a47-138">Prerequisites</span></span>
<span data-ttu-id="f8a47-139">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span><span class="sxs-lookup"><span data-stu-id="f8a47-139">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

## <a name="step-1-create-an-aspnet-web-api"></a><span data-ttu-id="f8a47-140">Step 1: Create an ASP.NET web API</span><span class="sxs-lookup"><span data-stu-id="f8a47-140">Step 1: Create an ASP.NET web API</span></span>

1. <span data-ttu-id="f8a47-141">In Visual Studio, create a project by selecting **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-141">In Visual Studio, create a project by selecting **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="f8a47-142">In the **New Project** window, select **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-142">In the **New Project** window, select **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>

3. <span data-ttu-id="f8a47-143">In the **Name** box, type a name for the application (for example, *Contoso.AADB2C.API*), and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-143">In the **Name** box, type a name for the application (for example, *Contoso.AADB2C.API*), and then select **OK**.</span></span>

    ![Create new visual studio project](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-create-project.png)

4. <span data-ttu-id="f8a47-145">In the **New ASP.NET Web Application** window, select a **Web API** or **Azure API app** template.</span><span class="sxs-lookup"><span data-stu-id="f8a47-145">In the **New ASP.NET Web Application** window, select a **Web API** or **Azure API app** template.</span></span>

    ![Select web API template](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-select-web-api.png)

5. <span data-ttu-id="f8a47-147">Make sure that authentication is set to **No Authentication**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-147">Make sure that authentication is set to **No Authentication**.</span></span>

6. <span data-ttu-id="f8a47-148">Select **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="f8a47-148">Select **OK** to create the project.</span></span>

## <a name="step-2-prepare-the-rest-api-endpoint"></a><span data-ttu-id="f8a47-149">Step 2: Prepare the REST API endpoint</span><span class="sxs-lookup"><span data-stu-id="f8a47-149">Step 2: Prepare the REST API endpoint</span></span>

### <a name="step-21-add-data-models"></a><span data-ttu-id="f8a47-150">Step 2.1: Add data models</span><span class="sxs-lookup"><span data-stu-id="f8a47-150">Step 2.1: Add data models</span></span>
<span data-ttu-id="f8a47-151">The models represent the input claims and output claims data in your RESTful service.</span><span class="sxs-lookup"><span data-stu-id="f8a47-151">The models represent the input claims and output claims data in your RESTful service.</span></span> <span data-ttu-id="f8a47-152">Your code reads the input data by deserializing the input claims model from a JSON string to a C# object (your model).</span><span class="sxs-lookup"><span data-stu-id="f8a47-152">Your code reads the input data by deserializing the input claims model from a JSON string to a C# object (your model).</span></span> <span data-ttu-id="f8a47-153">The ASP.NET web API automatically deserializes the output claims model back to JSON and then writes the serialized data to the body of the HTTP response message.</span><span class="sxs-lookup"><span data-stu-id="f8a47-153">The ASP.NET web API automatically deserializes the output claims model back to JSON and then writes the serialized data to the body of the HTTP response message.</span></span> 

<span data-ttu-id="f8a47-154">Create a model that represents input claims by doing the following:</span><span class="sxs-lookup"><span data-stu-id="f8a47-154">Create a model that represents input claims by doing the following:</span></span>

1. <span data-ttu-id="f8a47-155">If Solution Explorer is not already open, select **View** > **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-155">If Solution Explorer is not already open, select **View** > **Solution Explorer**.</span></span> 
2. <span data-ttu-id="f8a47-156">In Solution Explorer, right-click the **Models** folder, select **Add**, and then select **Class**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-156">In Solution Explorer, right-click the **Models** folder, select **Add**, and then select **Class**.</span></span>

    ![Add model](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-add-model.png)

3. <span data-ttu-id="f8a47-158">Name the class `InputClaimsModel`, and then add the following properties to the `InputClaimsModel` class:</span><span class="sxs-lookup"><span data-stu-id="f8a47-158">Name the class `InputClaimsModel`, and then add the following properties to the `InputClaimsModel` class:</span></span>

    ```csharp
    namespace Contoso.AADB2C.API.Models
    {
        public class InputClaimsModel
        {
            public string email { get; set; }
            public string firstName { get; set; }
            public string lastName { get; set; }
        }
    }
    ```

4. <span data-ttu-id="f8a47-159">Create a new model, `OutputClaimsModel`, and then add the following properties to the `OutputClaimsModel` class:</span><span class="sxs-lookup"><span data-stu-id="f8a47-159">Create a new model, `OutputClaimsModel`, and then add the following properties to the `OutputClaimsModel` class:</span></span>

    ```csharp
    namespace Contoso.AADB2C.API.Models
    {
        public class OutputClaimsModel
        {
            public string loyaltyNumber { get; set; }
        }
    }
    ```

5. <span data-ttu-id="f8a47-160">Create one more model, `B2CResponseContent`, which you use to throw input-validation error messages.</span><span class="sxs-lookup"><span data-stu-id="f8a47-160">Create one more model, `B2CResponseContent`, which you use to throw input-validation error messages.</span></span> <span data-ttu-id="f8a47-161">Add the following properties to the `B2CResponseContent` class, provide the missing references, and then save the file:</span><span class="sxs-lookup"><span data-stu-id="f8a47-161">Add the following properties to the `B2CResponseContent` class, provide the missing references, and then save the file:</span></span>

    ```csharp
    namespace Contoso.AADB2C.API.Models
    {
        public class B2CResponseContent
        {
            public string version { get; set; }
            public int status { get; set; }
            public string userMessage { get; set; }

            public B2CResponseContent(string message, HttpStatusCode status)
            {
                this.userMessage = message;
                this.status = (int)status;
                this.version = Assembly.GetExecutingAssembly().GetName().Version.ToString();
            }    
        }
    }
    ```

### <a name="step-22-add-a-controller"></a><span data-ttu-id="f8a47-162">Step 2.2: Add a controller</span><span class="sxs-lookup"><span data-stu-id="f8a47-162">Step 2.2: Add a controller</span></span>
<span data-ttu-id="f8a47-163">In the web API, a _controller_ is an object that handles HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="f8a47-163">In the web API, a _controller_ is an object that handles HTTP requests.</span></span> <span data-ttu-id="f8a47-164">The controller returns output claims or, if the first name is not valid, throws a Conflict HTTP error message.</span><span class="sxs-lookup"><span data-stu-id="f8a47-164">The controller returns output claims or, if the first name is not valid, throws a Conflict HTTP error message.</span></span>

1. <span data-ttu-id="f8a47-165">In Solution Explorer, right-click the **Controllers** folder, select **Add**, and then select **Controller**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-165">In Solution Explorer, right-click the **Controllers** folder, select **Add**, and then select **Controller**.</span></span>

    ![Add new controller](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-add-controller-1.png)

2. <span data-ttu-id="f8a47-167">In the **Add Scaffold** window, select **Web API Controller - Empty**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-167">In the **Add Scaffold** window, select **Web API Controller - Empty**, and then select **Add**.</span></span>

    ![Select Web API 2 Controller - Empty](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-add-controller-2.png)

3. <span data-ttu-id="f8a47-169">In the **Add Controller** window, name the controller **IdentityController**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-169">In the **Add Controller** window, name the controller **IdentityController**, and then select **Add**.</span></span>

    ![Type the controller name](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-add-controller-3.png)

    <span data-ttu-id="f8a47-171">The scaffolding creates a file named *IdentityController.cs* in the *Controllers* folder.</span><span class="sxs-lookup"><span data-stu-id="f8a47-171">The scaffolding creates a file named *IdentityController.cs* in the *Controllers* folder.</span></span>

4. <span data-ttu-id="f8a47-172">If the *IdentityController.cs* file is not open already, double-click it, and then replace the code in the file with the following code:</span><span class="sxs-lookup"><span data-stu-id="f8a47-172">If the *IdentityController.cs* file is not open already, double-click it, and then replace the code in the file with the following code:</span></span>

    ```csharp
    using Contoso.AADB2C.API.Models;
    using Newtonsoft.Json;
    using System;
    using System.NET;
    using System.Web.Http;

    namespace Contoso.AADB2C.API.Controllers
    {
        public class IdentityController: ApiController
        {
            [HttpPost]
            public IHttpActionResult SignUp()
            {
                // If no data came in, then return
                if (this.Request.Content == null) throw new Exception();

                // Read the input claims from the request body
                string input = Request.Content.ReadAsStringAsync().Result;

                // Check the input content value
                if (string.IsNullOrEmpty(input))
                {
                    return Content(HttpStatusCode.Conflict, new B2CResponseContent("Request content is empty", HttpStatusCode.Conflict));
                }

                // Convert the input string into an InputClaimsModel object
                InputClaimsModel inputClaims = JsonConvert.DeserializeObject(input, typeof(InputClaimsModel)) as InputClaimsModel;

                if (inputClaims == null)
                {
                    return Content(HttpStatusCode.Conflict, new B2CResponseContent("Can not deserialize input claims", HttpStatusCode.Conflict));
                }

                // Run an input validation
                if (inputClaims.firstName.ToLower() == "test")
                {
                    return Content(HttpStatusCode.Conflict, new B2CResponseContent("Test name is not valid, please provide a valid name", HttpStatusCode.Conflict));
                }

                // Create an output claims object and set the loyalty number with a random value
                OutputClaimsModel outputClaims = new OutputClaimsModel();
                outputClaims.loyaltyNumber = new Random().Next(100, 1000).ToString();

                // Return the output claim(s)
                return Ok(outputClaims);
            }
        }
    }
    ```

## <a name="step-3-publish-the-project-to-azure"></a><span data-ttu-id="f8a47-173">Step 3: Publish the project to Azure</span><span class="sxs-lookup"><span data-stu-id="f8a47-173">Step 3: Publish the project to Azure</span></span>
1. <span data-ttu-id="f8a47-174">In Solution Explorer, right-click the **Contoso.AADB2C.API** project, and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-174">In Solution Explorer, right-click the **Contoso.AADB2C.API** project, and then select **Publish**.</span></span>

    ![Publish to Microsoft Azure App Service](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-publish-to-azure-1.png)

2. <span data-ttu-id="f8a47-176">In the **Publish** window, select **Microsoft Azure App Service**, and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-176">In the **Publish** window, select **Microsoft Azure App Service**, and then select **Publish**.</span></span>

    ![Create new Microsoft Azure App Service](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-publish-to-azure-2.png)

    <span data-ttu-id="f8a47-178">The **Create App Service** window opens.</span><span class="sxs-lookup"><span data-stu-id="f8a47-178">The **Create App Service** window opens.</span></span> <span data-ttu-id="f8a47-179">In it, you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="f8a47-179">In it, you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

    > [!NOTE]
    ><span data-ttu-id="f8a47-180">For more information about how to publish, see [Create an ASP.NET web app in Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet#publish-to-azure).</span><span class="sxs-lookup"><span data-stu-id="f8a47-180">For more information about how to publish, see [Create an ASP.NET web app in Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet#publish-to-azure).</span></span>

3. <span data-ttu-id="f8a47-181">In the **Web App Name** box, type a unique app name (valid characters are a-z, 0-9, and hyphens (-).</span><span class="sxs-lookup"><span data-stu-id="f8a47-181">In the **Web App Name** box, type a unique app name (valid characters are a-z, 0-9, and hyphens (-).</span></span> <span data-ttu-id="f8a47-182">The URL of the web app is http://<app_name>.azurewebsites.NET, where *app_name* is the name of your web app.</span><span class="sxs-lookup"><span data-stu-id="f8a47-182">The URL of the web app is http://<app_name>.azurewebsites.NET, where *app_name* is the name of your web app.</span></span> <span data-ttu-id="f8a47-183">You can accept the automatically generated name, which is unique.</span><span class="sxs-lookup"><span data-stu-id="f8a47-183">You can accept the automatically generated name, which is unique.</span></span>

    ![Provide App Service properties](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-publish-to-azure-3.png)

4. <span data-ttu-id="f8a47-185">To start creating Azure resources, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-185">To start creating Azure resources, select **Create**.</span></span>  
    <span data-ttu-id="f8a47-186">After the ASP.NET web app has been created, the wizard publishes it to Azure and then starts the app in the default browser.</span><span class="sxs-lookup"><span data-stu-id="f8a47-186">After the ASP.NET web app has been created, the wizard publishes it to Azure and then starts the app in the default browser.</span></span>

6. <span data-ttu-id="f8a47-187">Copy the web app's URL.</span><span class="sxs-lookup"><span data-stu-id="f8a47-187">Copy the web app's URL.</span></span>

## <a name="step-4-add-the-new-loyaltynumber-claim-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="f8a47-188">Step 4: Add the new `loyaltyNumber` claim to the schema of your TrustFrameworkExtensions.xml file</span><span class="sxs-lookup"><span data-stu-id="f8a47-188">Step 4: Add the new `loyaltyNumber` claim to the schema of your TrustFrameworkExtensions.xml file</span></span>
<span data-ttu-id="f8a47-189">The `loyaltyNumber` claim is not yet defined in our schema.</span><span class="sxs-lookup"><span data-stu-id="f8a47-189">The `loyaltyNumber` claim is not yet defined in our schema.</span></span> <span data-ttu-id="f8a47-190">Add a definition within the `<BuildingBlocks>` element, which you can find at the beginning of the *TrustFrameworkExtensions.xml* file.</span><span class="sxs-lookup"><span data-stu-id="f8a47-190">Add a definition within the `<BuildingBlocks>` element, which you can find at the beginning of the *TrustFrameworkExtensions.xml* file.</span></span>

```xml
<BuildingBlocks>
    <ClaimsSchema>
        <ClaimType Id="loyaltyNumber">
            <DisplayName>loyaltyNumber</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Customer loyalty number</UserHelpText>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-5-add-a-claims-provider"></a><span data-ttu-id="f8a47-191">Step 5: Add a claims provider</span><span class="sxs-lookup"><span data-stu-id="f8a47-191">Step 5: Add a claims provider</span></span> 
<span data-ttu-id="f8a47-192">Every claims provider must have one or more technical profiles, which determine the endpoints and protocols needed to communicate with the claims provider.</span><span class="sxs-lookup"><span data-stu-id="f8a47-192">Every claims provider must have one or more technical profiles, which determine the endpoints and protocols needed to communicate with the claims provider.</span></span> 

<span data-ttu-id="f8a47-193">A claims provider can have multiple technical profiles for various reasons.</span><span class="sxs-lookup"><span data-stu-id="f8a47-193">A claims provider can have multiple technical profiles for various reasons.</span></span> <span data-ttu-id="f8a47-194">For example, multiple technical profiles might be defined because the claims provider supports multiple protocols, endpoints can have varying capabilities, or releases can contain claims that have a variety of assurance levels.</span><span class="sxs-lookup"><span data-stu-id="f8a47-194">For example, multiple technical profiles might be defined because the claims provider supports multiple protocols, endpoints can have varying capabilities, or releases can contain claims that have a variety of assurance levels.</span></span> <span data-ttu-id="f8a47-195">It might be acceptable to release sensitive claims in one user journey but not in another.</span><span class="sxs-lookup"><span data-stu-id="f8a47-195">It might be acceptable to release sensitive claims in one user journey but not in another.</span></span> 

<span data-ttu-id="f8a47-196">The following XML snippet contains a claims provider node with two technical profiles:</span><span class="sxs-lookup"><span data-stu-id="f8a47-196">The following XML snippet contains a claims provider node with two technical profiles:</span></span>

* <span data-ttu-id="f8a47-197">**TechnicalProfile Id="REST-API-SignUp"**: Defines your RESTful service.</span><span class="sxs-lookup"><span data-stu-id="f8a47-197">**TechnicalProfile Id="REST-API-SignUp"**: Defines your RESTful service.</span></span> 
   * <span data-ttu-id="f8a47-198">`Proprietary` is described as the protocol for a RESTful-based provider.</span><span class="sxs-lookup"><span data-stu-id="f8a47-198">`Proprietary` is described as the protocol for a RESTful-based provider.</span></span> 
   * <span data-ttu-id="f8a47-199">`InputClaims` defines the claims that will be sent from Azure AD B2C to the REST service.</span><span class="sxs-lookup"><span data-stu-id="f8a47-199">`InputClaims` defines the claims that will be sent from Azure AD B2C to the REST service.</span></span> 

   <span data-ttu-id="f8a47-200">In this example, the content of the claim `givenName` sends to the REST service as `firstName`, the content of the claim `surname` sends to the REST service as `lastName`, and `email` sends as is.</span><span class="sxs-lookup"><span data-stu-id="f8a47-200">In this example, the content of the claim `givenName` sends to the REST service as `firstName`, the content of the claim `surname` sends to the REST service as `lastName`, and `email` sends as is.</span></span> <span data-ttu-id="f8a47-201">The `OutputClaims` element defines the claims that are retrieved from RESTful service back to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f8a47-201">The `OutputClaims` element defines the claims that are retrieved from RESTful service back to Azure AD B2C.</span></span>

* <span data-ttu-id="f8a47-202">**TechnicalProfile Id="LocalAccountSignUpWithLogonEmail"**: Adds a validation technical profile to an existing technical profile (defined in base policy).</span><span class="sxs-lookup"><span data-stu-id="f8a47-202">**TechnicalProfile Id="LocalAccountSignUpWithLogonEmail"**: Adds a validation technical profile to an existing technical profile (defined in base policy).</span></span> <span data-ttu-id="f8a47-203">During the sign-up journey, the validation technical profile invokes the preceding technical profile.</span><span class="sxs-lookup"><span data-stu-id="f8a47-203">During the sign-up journey, the validation technical profile invokes the preceding technical profile.</span></span> <span data-ttu-id="f8a47-204">If the RESTful service returns an HTTP error 409 (a conflict error), the error message is displayed to the user.</span><span class="sxs-lookup"><span data-stu-id="f8a47-204">If the RESTful service returns an HTTP error 409 (a conflict error), the error message is displayed to the user.</span></span> 

<span data-ttu-id="f8a47-205">Locate the `<ClaimsProviders>` node, and then add the following XML snippet under the `<ClaimsProviders>` node:</span><span class="sxs-lookup"><span data-stu-id="f8a47-205">Locate the `<ClaimsProviders>` node, and then add the following XML snippet under the `<ClaimsProviders>` node:</span></span>

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
    
    <!-- Custom Restful service -->
    <TechnicalProfile Id="REST-API-SignUp">
        <DisplayName>Validate user's input data and return loyaltyNumber claim</DisplayName>
        <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
        <Metadata>
        <Item Key="ServiceUrl">https://your-app-name.azurewebsites.NET/api/identity/signup</Item>
        <Item Key="AuthenticationType">None</Item>
        <Item Key="SendClaimsIn">Body</Item>
        </Metadata>
        <InputClaims>
        <InputClaim ClaimTypeReferenceId="email" />
        <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="firstName" />
        <InputClaim ClaimTypeReferenceId="surname" PartnerClaimType="lastName" />
        </InputClaims>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="loyaltyNumber" PartnerClaimType="loyaltyNumber" />
        </OutputClaims>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
    </TechnicalProfile>

<!-- Change LocalAccountSignUpWithLogonEmail technical profile to support your validation technical profile -->
    <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="loyaltyNumber" PartnerClaimType="loyaltyNumber" />
        </OutputClaims>
        <ValidationTechnicalProfiles>
        <ValidationTechnicalProfile ReferenceId="REST-API-SignUp" />
        </ValidationTechnicalProfiles>
    </TechnicalProfile>

    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="step-6-add-the-loyaltynumber-claim-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="f8a47-206">Step 6: Add the `loyaltyNumber` claim to your relying party policy file so the claim is sent to your application</span><span class="sxs-lookup"><span data-stu-id="f8a47-206">Step 6: Add the `loyaltyNumber` claim to your relying party policy file so the claim is sent to your application</span></span>
<span data-ttu-id="f8a47-207">Edit your *SignUpOrSignIn.xml* relying party (RP) file, and modify the TechnicalProfile Id="PolicyProfile" element to add the following: `<OutputClaim ClaimTypeReferenceId="loyaltyNumber" />`.</span><span class="sxs-lookup"><span data-stu-id="f8a47-207">Edit your *SignUpOrSignIn.xml* relying party (RP) file, and modify the TechnicalProfile Id="PolicyProfile" element to add the following: `<OutputClaim ClaimTypeReferenceId="loyaltyNumber" />`.</span></span>

<span data-ttu-id="f8a47-208">After you add the new claim, the relying party code looks like this:</span><span class="sxs-lookup"><span data-stu-id="f8a47-208">After you add the new claim, the relying party code looks like this:</span></span>

```xml
<RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
        <DisplayName>PolicyProfile</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="loyaltyNumber" DefaultValue="" />
        </OutputClaims>
        <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
    </RelyingParty>
</TrustFrameworkPolicy>
```

## <a name="step-7-upload-the-policy-to-your-tenant"></a><span data-ttu-id="f8a47-209">Step 7: Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="f8a47-209">Step 7: Upload the policy to your tenant</span></span>

1. <span data-ttu-id="f8a47-210">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-210">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open **Azure AD B2C**.</span></span>

2. <span data-ttu-id="f8a47-211">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-211">Select **Identity Experience Framework**.</span></span>

3. <span data-ttu-id="f8a47-212">Open **All Policies**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-212">Open **All Policies**.</span></span> 

4. <span data-ttu-id="f8a47-213">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-213">Select **Upload Policy**.</span></span>

5. <span data-ttu-id="f8a47-214">Select the **Overwrite the policy if it exists** check box.</span><span class="sxs-lookup"><span data-stu-id="f8a47-214">Select the **Overwrite the policy if it exists** check box.</span></span>

6. <span data-ttu-id="f8a47-215">Upload the TrustFrameworkExtensions.xml file, and ensure that it passes validation.</span><span class="sxs-lookup"><span data-stu-id="f8a47-215">Upload the TrustFrameworkExtensions.xml file, and ensure that it passes validation.</span></span>

7. <span data-ttu-id="f8a47-216">Repeat the preceding step with the SignUpOrSignIn.xml file.</span><span class="sxs-lookup"><span data-stu-id="f8a47-216">Repeat the preceding step with the SignUpOrSignIn.xml file.</span></span>

## <a name="step-8-test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="f8a47-217">Step 8: Test the custom policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="f8a47-217">Step 8: Test the custom policy by using Run Now</span></span>
1. <span data-ttu-id="f8a47-218">Select **Azure AD B2C Settings**, and then go to **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-218">Select **Azure AD B2C Settings**, and then go to **Identity Experience Framework**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f8a47-219">**Run now** requires at least one application to be preregistered on the tenant.</span><span class="sxs-lookup"><span data-stu-id="f8a47-219">**Run now** requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="f8a47-220">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span><span class="sxs-lookup"><span data-stu-id="f8a47-220">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>

2. <span data-ttu-id="f8a47-221">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="f8a47-221">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span></span>

    ![The B2C_1A_signup_signin window](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-run.png)

3. <span data-ttu-id="f8a47-223">Test the process by typing **Test** in the **Given Name** box.</span><span class="sxs-lookup"><span data-stu-id="f8a47-223">Test the process by typing **Test** in the **Given Name** box.</span></span>  
    <span data-ttu-id="f8a47-224">Azure AD B2C displays an error message at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="f8a47-224">Azure AD B2C displays an error message at the top of the window.</span></span>

    ![Test your policy](media/aadb2c-ief-rest-api-netfw/aadb2c-ief-rest-api-netfw-test.png)

4.  <span data-ttu-id="f8a47-226">In the **Given Name** box, type a name (other than "Test").</span><span class="sxs-lookup"><span data-stu-id="f8a47-226">In the **Given Name** box, type a name (other than "Test").</span></span>  
    <span data-ttu-id="f8a47-227">Azure AD B2C signs up the user and then sends a loyaltyNumber to your application.</span><span class="sxs-lookup"><span data-stu-id="f8a47-227">Azure AD B2C signs up the user and then sends a loyaltyNumber to your application.</span></span> <span data-ttu-id="f8a47-228">Note the number in this JWT.</span><span class="sxs-lookup"><span data-stu-id="f8a47-228">Note the number in this JWT.</span></span>

```
{
  "typ": "JWT",
  "alg": "RS256",
  "kid": "X5eXk4xyojNFum1kl2Ytv8dlNP4-c57dO6QGTVBwaNk"
}.{
  "exp": 1507125903,
  "nbf": 1507122303,
  "ver": "1.0",
  "iss": "https://contoso.b2clogin.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "aud": "e1d2612f-c2bc-4599-8e7b-d874eaca1ee1",
  "acr": "b2c_1a_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1507122303,
  "auth_time": 1507122303,
  "loyaltyNumber": "290",
  "given_name": "Emily",
  "emails": ["B2cdemo@outlook.com"]
}
```

## <a name="optional-download-the-complete-policy-files-and-code"></a><span data-ttu-id="f8a47-229">(Optional) Download the complete policy files and code</span><span class="sxs-lookup"><span data-stu-id="f8a47-229">(Optional) Download the complete policy files and code</span></span>
* <span data-ttu-id="f8a47-230">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span><span class="sxs-lookup"><span data-stu-id="f8a47-230">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span></span> <span data-ttu-id="f8a47-231">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw).</span><span class="sxs-lookup"><span data-stu-id="f8a47-231">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw).</span></span>
* <span data-ttu-id="f8a47-232">You can download the complete code from [Sample Visual Studio solution for reference](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw/).</span><span class="sxs-lookup"><span data-stu-id="f8a47-232">You can download the complete code from [Sample Visual Studio solution for reference](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw/).</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="f8a47-233">Next steps</span><span class="sxs-lookup"><span data-stu-id="f8a47-233">Next steps</span></span>
* [<span data-ttu-id="f8a47-234">Secure your RESTful API with basic authentication (username and password)</span><span class="sxs-lookup"><span data-stu-id="f8a47-234">Secure your RESTful API with basic authentication (username and password)</span></span>](active-directory-b2c-custom-rest-api-netfw-secure-basic.md)
* [<span data-ttu-id="f8a47-235">Secure your RESTful API with client certificates</span><span class="sxs-lookup"><span data-stu-id="f8a47-235">Secure your RESTful API with client certificates</span></span>](active-directory-b2c-custom-rest-api-netfw-secure-cert.md)
