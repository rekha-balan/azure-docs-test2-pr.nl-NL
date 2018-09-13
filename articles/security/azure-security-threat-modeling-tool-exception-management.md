---
title: Exception Management - Microsoft Threat Modeling Tool - Azure | Microsoft Docs
description: mitigations for threats exposed in the Threat Modeling Tool
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: rodsan
ms.openlocfilehash: 201e5e2bc4fe923a5a7d5685d877994e827fc466
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549967"
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="71490-103">Security Frame: Exception Management | Mitigations</span><span class="sxs-lookup"><span data-stu-id="71490-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="71490-104">Product/Service</span><span class="sxs-lookup"><span data-stu-id="71490-104">Product/Service</span></span> | <span data-ttu-id="71490-105">Article</span><span class="sxs-lookup"><span data-stu-id="71490-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="71490-106">WCF</span><span class="sxs-lookup"><span data-stu-id="71490-106">WCF</span></span> | <ul><li>[<span data-ttu-id="71490-107">WCF- Do not include serviceDebug node in configuration file</span><span class="sxs-lookup"><span data-stu-id="71490-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="71490-108">WCF- Do not include serviceMetadata node in configuration file</span><span class="sxs-lookup"><span data-stu-id="71490-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="71490-109">Web API</span><span class="sxs-lookup"><span data-stu-id="71490-109">Web API</span></span> | <ul><li>[<span data-ttu-id="71490-110">Ensure that proper exception handling is done in ASP.NET Web API </span><span class="sxs-lookup"><span data-stu-id="71490-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="71490-111">Web Application</span><span class="sxs-lookup"><span data-stu-id="71490-111">Web Application</span></span> | <ul><li>[<span data-ttu-id="71490-112">Do not expose security details in error messages </span><span class="sxs-lookup"><span data-stu-id="71490-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="71490-113">Implement Default error handling page </span><span class="sxs-lookup"><span data-stu-id="71490-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="71490-114">Set Deployment Method to Retail in IIS</span><span class="sxs-lookup"><span data-stu-id="71490-114">Set Deployment Method to Retail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="71490-115">Exceptions should fail safely</span><span class="sxs-lookup"><span data-stu-id="71490-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <a id="servicedebug"></a><span data-ttu-id="71490-116">WCF- Do not include serviceDebug node in configuration file</span><span class="sxs-lookup"><span data-stu-id="71490-116">WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="71490-117">Title</span><span class="sxs-lookup"><span data-stu-id="71490-117">Title</span></span>                   | <span data-ttu-id="71490-118">Details</span><span class="sxs-lookup"><span data-stu-id="71490-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="71490-119">Component</span><span class="sxs-lookup"><span data-stu-id="71490-119">Component</span></span>               | <span data-ttu-id="71490-120">WCF</span><span class="sxs-lookup"><span data-stu-id="71490-120">WCF</span></span> | 
| <span data-ttu-id="71490-121">SDL Phase</span><span class="sxs-lookup"><span data-stu-id="71490-121">SDL Phase</span></span>               | <span data-ttu-id="71490-122">Build</span><span class="sxs-lookup"><span data-stu-id="71490-122">Build</span></span> |  
| <span data-ttu-id="71490-123">Applicable Technologies</span><span class="sxs-lookup"><span data-stu-id="71490-123">Applicable Technologies</span></span> | <span data-ttu-id="71490-124">Generic, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="71490-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="71490-125">Attributes</span><span class="sxs-lookup"><span data-stu-id="71490-125">Attributes</span></span>              | <span data-ttu-id="71490-126">N/A</span><span class="sxs-lookup"><span data-stu-id="71490-126">N/A</span></span>  |
| <span data-ttu-id="71490-127">References</span><span class="sxs-lookup"><span data-stu-id="71490-127">References</span></span>              | <span data-ttu-id="71490-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="71490-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="71490-129">Steps</span><span class="sxs-lookup"><span data-stu-id="71490-129">Steps</span></span> | <span data-ttu-id="71490-130">Windows Communication Framework (WCF) services can be configured to expose debugging information.</span><span class="sxs-lookup"><span data-stu-id="71490-130">Windows Communication Framework (WCF) services can be configured to expose debugging information.</span></span> <span data-ttu-id="71490-131">Debug information should not be used in production environments.</span><span class="sxs-lookup"><span data-stu-id="71490-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="71490-132">The `<serviceDebug>` tag defines whether the debug information feature is enabled for a WCF service.</span><span class="sxs-lookup"><span data-stu-id="71490-132">The `<serviceDebug>` tag defines whether the debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="71490-133">If the attribute includeExceptionDetailInFaults is set to true, exception information from the application will be returned to clients.</span><span class="sxs-lookup"><span data-stu-id="71490-133">If the attribute includeExceptionDetailInFaults is set to true, exception information from the application will be returned to clients.</span></span> <span data-ttu-id="71490-134">Attackers can leverage the additional information they gain from debugging output to mount attacks targeted on the framework, database, or other resources used by the application.</span><span class="sxs-lookup"><span data-stu-id="71490-134">Attackers can leverage the additional information they gain from debugging output to mount attacks targeted on the framework, database, or other resources used by the application.</span></span> |

### <a name="example"></a><span data-ttu-id="71490-135">Example</span><span class="sxs-lookup"><span data-stu-id="71490-135">Example</span></span>
<span data-ttu-id="71490-136">The following configuration file includes the `<serviceDebug>` tag:</span><span class="sxs-lookup"><span data-stu-id="71490-136">The following configuration file includes the `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="71490-137">Disable debugging information in the service.</span><span class="sxs-lookup"><span data-stu-id="71490-137">Disable debugging information in the service.</span></span> <span data-ttu-id="71490-138">This can be accomplished by removing the `<serviceDebug>` tag from your application's configuration file.</span><span class="sxs-lookup"><span data-stu-id="71490-138">This can be accomplished by removing the `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <a id="servicemetadata"></a><span data-ttu-id="71490-139">WCF- Do not include serviceMetadata node in configuration file</span><span class="sxs-lookup"><span data-stu-id="71490-139">WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="71490-140">Title</span><span class="sxs-lookup"><span data-stu-id="71490-140">Title</span></span>                   | <span data-ttu-id="71490-141">Details</span><span class="sxs-lookup"><span data-stu-id="71490-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="71490-142">Component</span><span class="sxs-lookup"><span data-stu-id="71490-142">Component</span></span>               | <span data-ttu-id="71490-143">WCF</span><span class="sxs-lookup"><span data-stu-id="71490-143">WCF</span></span> | 
| <span data-ttu-id="71490-144">SDL Phase</span><span class="sxs-lookup"><span data-stu-id="71490-144">SDL Phase</span></span>               | <span data-ttu-id="71490-145">Build</span><span class="sxs-lookup"><span data-stu-id="71490-145">Build</span></span> |  
| <span data-ttu-id="71490-146">Applicable Technologies</span><span class="sxs-lookup"><span data-stu-id="71490-146">Applicable Technologies</span></span> | <span data-ttu-id="71490-147">Generic</span><span class="sxs-lookup"><span data-stu-id="71490-147">Generic</span></span> |
| <span data-ttu-id="71490-148">Attributes</span><span class="sxs-lookup"><span data-stu-id="71490-148">Attributes</span></span>              | <span data-ttu-id="71490-149">Generic, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="71490-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="71490-150">References</span><span class="sxs-lookup"><span data-stu-id="71490-150">References</span></span>              | <span data-ttu-id="71490-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="71490-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="71490-152">Steps</span><span class="sxs-lookup"><span data-stu-id="71490-152">Steps</span></span> | <span data-ttu-id="71490-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit the service.</span><span class="sxs-lookup"><span data-stu-id="71490-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit the service.</span></span> <span data-ttu-id="71490-154">The `<serviceMetadata>` tag enables the metadata publishing feature.</span><span class="sxs-lookup"><span data-stu-id="71490-154">The `<serviceMetadata>` tag enables the metadata publishing feature.</span></span> <span data-ttu-id="71490-155">Service metadata could contain sensitive information that should not be publicly accessible.</span><span class="sxs-lookup"><span data-stu-id="71490-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="71490-156">At a minimum, only allow trusted users to access the metadata and ensure that unnecessary information is not exposed.</span><span class="sxs-lookup"><span data-stu-id="71490-156">At a minimum, only allow trusted users to access the metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="71490-157">Better yet, entirely disable the ability to publish metadata.</span><span class="sxs-lookup"><span data-stu-id="71490-157">Better yet, entirely disable the ability to publish metadata.</span></span> <span data-ttu-id="71490-158">A safe WCF configuration will not contain the `<serviceMetadata>` tag.</span><span class="sxs-lookup"><span data-stu-id="71490-158">A safe WCF configuration will not contain the `<serviceMetadata>` tag.</span></span> |

## <a id="exception"></a><span data-ttu-id="71490-159">Ensure that proper exception handling is done in ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="71490-159">Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="71490-160">Title</span><span class="sxs-lookup"><span data-stu-id="71490-160">Title</span></span>                   | <span data-ttu-id="71490-161">Details</span><span class="sxs-lookup"><span data-stu-id="71490-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="71490-162">Component</span><span class="sxs-lookup"><span data-stu-id="71490-162">Component</span></span>               | <span data-ttu-id="71490-163">Web API</span><span class="sxs-lookup"><span data-stu-id="71490-163">Web API</span></span> | 
| <span data-ttu-id="71490-164">SDL Phase</span><span class="sxs-lookup"><span data-stu-id="71490-164">SDL Phase</span></span>               | <span data-ttu-id="71490-165">Build</span><span class="sxs-lookup"><span data-stu-id="71490-165">Build</span></span> |  
| <span data-ttu-id="71490-166">Applicable Technologies</span><span class="sxs-lookup"><span data-stu-id="71490-166">Applicable Technologies</span></span> | <span data-ttu-id="71490-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="71490-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="71490-168">Attributes</span><span class="sxs-lookup"><span data-stu-id="71490-168">Attributes</span></span>              | <span data-ttu-id="71490-169">N/A</span><span class="sxs-lookup"><span data-stu-id="71490-169">N/A</span></span>  |
| <span data-ttu-id="71490-170">References</span><span class="sxs-lookup"><span data-stu-id="71490-170">References</span></span>              | <span data-ttu-id="71490-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="71490-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="71490-172">Steps</span><span class="sxs-lookup"><span data-stu-id="71490-172">Steps</span></span> | <span data-ttu-id="71490-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="71490-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="71490-174">Example</span><span class="sxs-lookup"><span data-stu-id="71490-174">Example</span></span>
<span data-ttu-id="71490-175">To control the status code returned by the API, `HttpResponseException` can be used as shown below:</span><span class="sxs-lookup"><span data-stu-id="71490-175">To control the status code returned by the API, `HttpResponseException` can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a><span data-ttu-id="71490-176">Example</span><span class="sxs-lookup"><span data-stu-id="71490-176">Example</span></span>
<span data-ttu-id="71490-177">For further control on the exception response, the `HttpResponseMessage` class can be used as shown below:</span><span class="sxs-lookup"><span data-stu-id="71490-177">For further control on the exception response, the `HttpResponseMessage` class can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
<span data-ttu-id="71490-178">To catch unhandled exceptions that are not of the type `HttpResponseException`, Exception Filters can be used.</span><span class="sxs-lookup"><span data-stu-id="71490-178">To catch unhandled exceptions that are not of the type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="71490-179">Exception filters implement the `System.Web.Http.Filters.IExceptionFilter` interface.</span><span class="sxs-lookup"><span data-stu-id="71490-179">Exception filters implement the `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="71490-180">The simplest way to write an exception filter is to derive from the `System.Web.Http.Filters.ExceptionFilterAttribute` class and override the OnException method.</span><span class="sxs-lookup"><span data-stu-id="71490-180">The simplest way to write an exception filter is to derive from the `System.Web.Http.Filters.ExceptionFilterAttribute` class and override the OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="71490-181">Example</span><span class="sxs-lookup"><span data-stu-id="71490-181">Example</span></span>
<span data-ttu-id="71490-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span><span class="sxs-lookup"><span data-stu-id="71490-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```
<span data-ttu-id="71490-183">There are several ways to register a Web API exception filter:</span><span class="sxs-lookup"><span data-stu-id="71490-183">There are several ways to register a Web API exception filter:</span></span>
# <a name="by-action"></a><span data-ttu-id="71490-184">By action</span><span class="sxs-lookup"><span data-stu-id="71490-184">By action</span></span>
# <a name="by-controller"></a><span data-ttu-id="71490-185">By controller</span><span class="sxs-lookup"><span data-stu-id="71490-185">By controller</span></span>
# <a name="globally"></a><span data-ttu-id="71490-186">Globally</span><span class="sxs-lookup"><span data-stu-id="71490-186">Globally</span></span> 

### <a name="example"></a><span data-ttu-id="71490-187">Example</span><span class="sxs-lookup"><span data-stu-id="71490-187">Example</span></span>
<span data-ttu-id="71490-188">To apply the filter to a specific action, add the filter as an attribute to the action:</span><span class="sxs-lookup"><span data-stu-id="71490-188">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span> 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a><span data-ttu-id="71490-189">Example</span><span class="sxs-lookup"><span data-stu-id="71490-189">Example</span></span>
<span data-ttu-id="71490-190">To apply the filter to all of the actions on a `controller`, add the filter as an attribute to the `controller` class:</span><span class="sxs-lookup"><span data-stu-id="71490-190">To apply the filter to all of the actions on a `controller`, add the filter as an attribute to the `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="71490-191">Example</span><span class="sxs-lookup"><span data-stu-id="71490-191">Example</span></span>
<span data-ttu-id="71490-192">To apply the filter globally to all Web API controllers, add an instance of the filter to the `GlobalConfiguration.Configuration.Filters` collection.</span><span class="sxs-lookup"><span data-stu-id="71490-192">To apply the filter globally to all Web API controllers, add an instance of the filter to the `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="71490-193">Exception filters in this collection apply to any Web API controller action.</span><span class="sxs-lookup"><span data-stu-id="71490-193">Exception filters in this collection apply to any Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="71490-194">Example</span><span class="sxs-lookup"><span data-stu-id="71490-194">Example</span></span>
<span data-ttu-id="71490-195">For model validation, the model state can be passed to CreateErrorResponse method as shown below:</span><span class="sxs-lookup"><span data-stu-id="71490-195">For model validation, the model state can be passed to CreateErrorResponse method as shown below:</span></span> 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

<span data-ttu-id="71490-196">Check the links in the references section for additional details about exceptional handling and model validation in ASP.Net Web API</span><span class="sxs-lookup"><span data-stu-id="71490-196">Check the links in the references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <a id="messages"></a><span data-ttu-id="71490-197">Do not expose security details in error messages</span><span class="sxs-lookup"><span data-stu-id="71490-197">Do not expose security details in error messages</span></span>

| <span data-ttu-id="71490-198">Title</span><span class="sxs-lookup"><span data-stu-id="71490-198">Title</span></span>                   | <span data-ttu-id="71490-199">Details</span><span class="sxs-lookup"><span data-stu-id="71490-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="71490-200">Component</span><span class="sxs-lookup"><span data-stu-id="71490-200">Component</span></span>               | <span data-ttu-id="71490-201">Web Application</span><span class="sxs-lookup"><span data-stu-id="71490-201">Web Application</span></span> | 
| <span data-ttu-id="71490-202">SDL Phase</span><span class="sxs-lookup"><span data-stu-id="71490-202">SDL Phase</span></span>               | <span data-ttu-id="71490-203">Build</span><span class="sxs-lookup"><span data-stu-id="71490-203">Build</span></span> |  
| <span data-ttu-id="71490-204">Applicable Technologies</span><span class="sxs-lookup"><span data-stu-id="71490-204">Applicable Technologies</span></span> | <span data-ttu-id="71490-205">Generic</span><span class="sxs-lookup"><span data-stu-id="71490-205">Generic</span></span> |
| <span data-ttu-id="71490-206">Attributes</span><span class="sxs-lookup"><span data-stu-id="71490-206">Attributes</span></span>              | <span data-ttu-id="71490-207">N/A</span><span class="sxs-lookup"><span data-stu-id="71490-207">N/A</span></span>  |
| <span data-ttu-id="71490-208">References</span><span class="sxs-lookup"><span data-stu-id="71490-208">References</span></span>              | <span data-ttu-id="71490-209">N/A</span><span class="sxs-lookup"><span data-stu-id="71490-209">N/A</span></span>  |
| <span data-ttu-id="71490-210">Steps</span><span class="sxs-lookup"><span data-stu-id="71490-210">Steps</span></span> | <p><span data-ttu-id="71490-211">Generic error messages are provided directly to the user without including sensitive application data.</span><span class="sxs-lookup"><span data-stu-id="71490-211">Generic error messages are provided directly to the user without including sensitive application data.</span></span> <span data-ttu-id="71490-212">Examples of sensitive data include:</span><span class="sxs-lookup"><span data-stu-id="71490-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="71490-213">Server names</span><span class="sxs-lookup"><span data-stu-id="71490-213">Server names</span></span></li><li><span data-ttu-id="71490-214">Connection strings</span><span class="sxs-lookup"><span data-stu-id="71490-214">Connection strings</span></span></li><li><span data-ttu-id="71490-215">Usernames</span><span class="sxs-lookup"><span data-stu-id="71490-215">Usernames</span></span></li><li><span data-ttu-id="71490-216">Passwords</span><span class="sxs-lookup"><span data-stu-id="71490-216">Passwords</span></span></li><li><span data-ttu-id="71490-217">SQL procedures</span><span class="sxs-lookup"><span data-stu-id="71490-217">SQL procedures</span></span></li><li><span data-ttu-id="71490-218">Details of dynamic SQL failures</span><span class="sxs-lookup"><span data-stu-id="71490-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="71490-219">Stack trace and lines of code</span><span class="sxs-lookup"><span data-stu-id="71490-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="71490-220">Variables stored in memory</span><span class="sxs-lookup"><span data-stu-id="71490-220">Variables stored in memory</span></span></li><li><span data-ttu-id="71490-221">Drive and folder locations</span><span class="sxs-lookup"><span data-stu-id="71490-221">Drive and folder locations</span></span></li><li><span data-ttu-id="71490-222">Application install points</span><span class="sxs-lookup"><span data-stu-id="71490-222">Application install points</span></span></li><li><span data-ttu-id="71490-223">Host configuration settings</span><span class="sxs-lookup"><span data-stu-id="71490-223">Host configuration settings</span></span></li><li><span data-ttu-id="71490-224">Other internal application details</span><span class="sxs-lookup"><span data-stu-id="71490-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="71490-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span><span class="sxs-lookup"><span data-stu-id="71490-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="71490-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful to a malicious user profiling your application.</span><span class="sxs-lookup"><span data-stu-id="71490-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful to a malicious user profiling your application.</span></span> <span data-ttu-id="71490-227">Do not directly display the contents of a class derived from the .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly to the user.</span><span class="sxs-lookup"><span data-stu-id="71490-227">Do not directly display the contents of a class derived from the .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly to the user.</span></span></p><ul><li><span data-ttu-id="71490-228">Provide generic error messages directly to the user that abstract away specific details found directly in the exception/error message</span><span class="sxs-lookup"><span data-stu-id="71490-228">Provide generic error messages directly to the user that abstract away specific details found directly in the exception/error message</span></span></li><li><span data-ttu-id="71490-229">Do not display the contents of a .NET exception class directly to the user</span><span class="sxs-lookup"><span data-stu-id="71490-229">Do not display the contents of a .NET exception class directly to the user</span></span></li><li><span data-ttu-id="71490-230">Trap all error messages and if appropriate inform the user via a generic error message sent to the application client</span><span class="sxs-lookup"><span data-stu-id="71490-230">Trap all error messages and if appropriate inform the user via a generic error message sent to the application client</span></span></li><li><span data-ttu-id="71490-231">Do not expose the contents of the Exception class directly to the user, especially the return value from `.ToString()`, or the values of the Message or StackTrace properties.</span><span class="sxs-lookup"><span data-stu-id="71490-231">Do not expose the contents of the Exception class directly to the user, especially the return value from `.ToString()`, or the values of the Message or StackTrace properties.</span></span> <span data-ttu-id="71490-232">Securely log this information and display a more innocuous message to the user</span><span class="sxs-lookup"><span data-stu-id="71490-232">Securely log this information and display a more innocuous message to the user</span></span></li></ul>|

## <a id="default"></a><span data-ttu-id="71490-233">Implement Default error handling page</span><span class="sxs-lookup"><span data-stu-id="71490-233">Implement Default error handling page</span></span>

| <span data-ttu-id="71490-234">Title</span><span class="sxs-lookup"><span data-stu-id="71490-234">Title</span></span>                   | <span data-ttu-id="71490-235">Details</span><span class="sxs-lookup"><span data-stu-id="71490-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="71490-236">Component</span><span class="sxs-lookup"><span data-stu-id="71490-236">Component</span></span>               | <span data-ttu-id="71490-237">Web Application</span><span class="sxs-lookup"><span data-stu-id="71490-237">Web Application</span></span> | 
| <span data-ttu-id="71490-238">SDL Phase</span><span class="sxs-lookup"><span data-stu-id="71490-238">SDL Phase</span></span>               | <span data-ttu-id="71490-239">Build</span><span class="sxs-lookup"><span data-stu-id="71490-239">Build</span></span> |  
| <span data-ttu-id="71490-240">Applicable Technologies</span><span class="sxs-lookup"><span data-stu-id="71490-240">Applicable Technologies</span></span> | <span data-ttu-id="71490-241">Generic</span><span class="sxs-lookup"><span data-stu-id="71490-241">Generic</span></span> |
| <span data-ttu-id="71490-242">Attributes</span><span class="sxs-lookup"><span data-stu-id="71490-242">Attributes</span></span>              | <span data-ttu-id="71490-243">N/A</span><span class="sxs-lookup"><span data-stu-id="71490-243">N/A</span></span>  |
| <span data-ttu-id="71490-244">References</span><span class="sxs-lookup"><span data-stu-id="71490-244">References</span></span>              | <span data-ttu-id="71490-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="71490-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="71490-246">Steps</span><span class="sxs-lookup"><span data-stu-id="71490-246">Steps</span></span> | <p><span data-ttu-id="71490-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span><span class="sxs-lookup"><span data-stu-id="71490-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="71490-248">Administrators can choose whether or not the application should display a friendly message to the client, detailed error message to the client, or detailed error message to localhost only.</span><span class="sxs-lookup"><span data-stu-id="71490-248">Administrators can choose whether or not the application should display a friendly message to the client, detailed error message to the client, or detailed error message to localhost only.</span></span> <span data-ttu-id="71490-249">The <customErrors> tag in the web.config has three modes:</span><span class="sxs-lookup"><span data-stu-id="71490-249">The <customErrors> tag in the web.config has three modes:</span></span></p><ul><li><span data-ttu-id="71490-250">**On:** Specifies that custom errors are enabled.</span><span class="sxs-lookup"><span data-stu-id="71490-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="71490-251">If no defaultRedirect attribute is specified, users see a generic error.</span><span class="sxs-lookup"><span data-stu-id="71490-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="71490-252">The custom errors are shown to the remote clients and to the local host</span><span class="sxs-lookup"><span data-stu-id="71490-252">The custom errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="71490-253">**Off:** Specifies that custom errors are disabled.</span><span class="sxs-lookup"><span data-stu-id="71490-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="71490-254">The detailed ASP.NET errors are shown to the remote clients and to the local host</span><span class="sxs-lookup"><span data-stu-id="71490-254">The detailed ASP.NET errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="71490-255">**RemoteOnly:** Specifies that custom errors are shown only to the remote clients, and that ASP.NET errors are shown to the local host.</span><span class="sxs-lookup"><span data-stu-id="71490-255">**RemoteOnly:** Specifies that custom errors are shown only to the remote clients, and that ASP.NET errors are shown to the local host.</span></span> <span data-ttu-id="71490-256">This is the default value</span><span class="sxs-lookup"><span data-stu-id="71490-256">This is the default value</span></span></li></ul><p><span data-ttu-id="71490-257">Open the `web.config` file for the application/site and ensure that the tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span><span class="sxs-lookup"><span data-stu-id="71490-257">Open the `web.config` file for the application/site and ensure that the tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <a id="deployment"></a><span data-ttu-id="71490-258">Set Deployment Method to Retail in IIS</span><span class="sxs-lookup"><span data-stu-id="71490-258">Set Deployment Method to Retail in IIS</span></span>

| <span data-ttu-id="71490-259">Title</span><span class="sxs-lookup"><span data-stu-id="71490-259">Title</span></span>                   | <span data-ttu-id="71490-260">Details</span><span class="sxs-lookup"><span data-stu-id="71490-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="71490-261">Component</span><span class="sxs-lookup"><span data-stu-id="71490-261">Component</span></span>               | <span data-ttu-id="71490-262">Web Application</span><span class="sxs-lookup"><span data-stu-id="71490-262">Web Application</span></span> | 
| <span data-ttu-id="71490-263">SDL Phase</span><span class="sxs-lookup"><span data-stu-id="71490-263">SDL Phase</span></span>               | <span data-ttu-id="71490-264">Deployment</span><span class="sxs-lookup"><span data-stu-id="71490-264">Deployment</span></span> |  
| <span data-ttu-id="71490-265">Applicable Technologies</span><span class="sxs-lookup"><span data-stu-id="71490-265">Applicable Technologies</span></span> | <span data-ttu-id="71490-266">Generic</span><span class="sxs-lookup"><span data-stu-id="71490-266">Generic</span></span> |
| <span data-ttu-id="71490-267">Attributes</span><span class="sxs-lookup"><span data-stu-id="71490-267">Attributes</span></span>              | <span data-ttu-id="71490-268">N/A</span><span class="sxs-lookup"><span data-stu-id="71490-268">N/A</span></span>  |
| <span data-ttu-id="71490-269">References</span><span class="sxs-lookup"><span data-stu-id="71490-269">References</span></span>              | <span data-ttu-id="71490-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="71490-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="71490-271">Steps</span><span class="sxs-lookup"><span data-stu-id="71490-271">Steps</span></span> | <p><span data-ttu-id="71490-272">The `<deployment retail>` switch is intended for use by production IIS servers.</span><span class="sxs-lookup"><span data-stu-id="71490-272">The `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="71490-273">This switch is used to help applications run with the best possible performance and least possible security information leakages by disabling the application's ability to generate trace output on a page, disabling the ability to display detailed error messages to end users, and disabling the debug switch.</span><span class="sxs-lookup"><span data-stu-id="71490-273">This switch is used to help applications run with the best possible performance and least possible security information leakages by disabling the application's ability to generate trace output on a page, disabling the ability to display detailed error messages to end users, and disabling the debug switch.</span></span></p><p><span data-ttu-id="71490-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span><span class="sxs-lookup"><span data-stu-id="71490-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="71490-275">It is recommended that the deployment method on any production server be set to retail.</span><span class="sxs-lookup"><span data-stu-id="71490-275">It is recommended that the deployment method on any production server be set to retail.</span></span> <span data-ttu-id="71490-276">open the machine.config file and ensure that `<deployment retail="true" />` remains set to true.</span><span class="sxs-lookup"><span data-stu-id="71490-276">open the machine.config file and ensure that `<deployment retail="true" />` remains set to true.</span></span></p>|

## <a id="fail"></a><span data-ttu-id="71490-277">Exceptions should fail safely</span><span class="sxs-lookup"><span data-stu-id="71490-277">Exceptions should fail safely</span></span>

| <span data-ttu-id="71490-278">Title</span><span class="sxs-lookup"><span data-stu-id="71490-278">Title</span></span>                   | <span data-ttu-id="71490-279">Details</span><span class="sxs-lookup"><span data-stu-id="71490-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="71490-280">Component</span><span class="sxs-lookup"><span data-stu-id="71490-280">Component</span></span>               | <span data-ttu-id="71490-281">Web Application</span><span class="sxs-lookup"><span data-stu-id="71490-281">Web Application</span></span> | 
| <span data-ttu-id="71490-282">SDL Phase</span><span class="sxs-lookup"><span data-stu-id="71490-282">SDL Phase</span></span>               | <span data-ttu-id="71490-283">Build</span><span class="sxs-lookup"><span data-stu-id="71490-283">Build</span></span> |  
| <span data-ttu-id="71490-284">Applicable Technologies</span><span class="sxs-lookup"><span data-stu-id="71490-284">Applicable Technologies</span></span> | <span data-ttu-id="71490-285">Generic</span><span class="sxs-lookup"><span data-stu-id="71490-285">Generic</span></span> |
| <span data-ttu-id="71490-286">Attributes</span><span class="sxs-lookup"><span data-stu-id="71490-286">Attributes</span></span>              | <span data-ttu-id="71490-287">N/A</span><span class="sxs-lookup"><span data-stu-id="71490-287">N/A</span></span>  |
| <span data-ttu-id="71490-288">References</span><span class="sxs-lookup"><span data-stu-id="71490-288">References</span></span>              | [<span data-ttu-id="71490-289">Fail securely</span><span class="sxs-lookup"><span data-stu-id="71490-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="71490-290">Steps</span><span class="sxs-lookup"><span data-stu-id="71490-290">Steps</span></span> | <span data-ttu-id="71490-291">Application should fail safely.</span><span class="sxs-lookup"><span data-stu-id="71490-291">Application should fail safely.</span></span> <span data-ttu-id="71490-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span><span class="sxs-lookup"><span data-stu-id="71490-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="71490-293">There are lot of logical errors due to which security issues creep in, when the exception block is written carelessly.</span><span class="sxs-lookup"><span data-stu-id="71490-293">There are lot of logical errors due to which security issues creep in, when the exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="71490-294">Example</span><span class="sxs-lookup"><span data-stu-id="71490-294">Example</span></span>
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check to enable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
<span data-ttu-id="71490-295">The above method will always return True, if some exception happens.</span><span class="sxs-lookup"><span data-stu-id="71490-295">The above method will always return True, if some exception happens.</span></span> <span data-ttu-id="71490-296">If the end user provides a malformed URL, that the browser respects, but the `Uri()` constructor doesn't, this will throw an exception, and the victim will be taken to the valid but malformed URL.</span><span class="sxs-lookup"><span data-stu-id="71490-296">If the end user provides a malformed URL, that the browser respects, but the `Uri()` constructor doesn't, this will throw an exception, and the victim will be taken to the valid but malformed URL.</span></span> 