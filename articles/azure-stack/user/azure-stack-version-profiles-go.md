---
title: Using API version profiles with GO in Azure Stack | Microsoft Docs
description: Learn about using API version profiles with GO in Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: sijuman
ms.openlocfilehash: 9ad4402098e938f72cf4b8c61cce8d0d46b5a147
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867765"
---
# <a name="use-api-version-profiles-with-go-in-azure-stack"></a><span data-ttu-id="390d2-103">Use API version profiles with Go in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="390d2-103">Use API version profiles with Go in Azure Stack</span></span>

<span data-ttu-id="390d2-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="390d2-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

## <a name="go-and-version-profiles"></a><span data-ttu-id="390d2-105">Go and version profiles</span><span class="sxs-lookup"><span data-stu-id="390d2-105">Go and version profiles</span></span>

<span data-ttu-id="390d2-106">A profile is a combination of different resource types with different versions from different services.</span><span class="sxs-lookup"><span data-stu-id="390d2-106">A profile is a combination of different resource types with different versions from different services.</span></span> <span data-ttu-id="390d2-107">Using a profile will help you mix and match between different resource types.</span><span class="sxs-lookup"><span data-stu-id="390d2-107">Using a profile will help you mix and match between different resource types.</span></span> <span data-ttu-id="390d2-108">Profiles can provide:</span><span class="sxs-lookup"><span data-stu-id="390d2-108">Profiles can provide:</span></span>

 - <span data-ttu-id="390d2-109">Stability for your application by locking to specific API versions.</span><span class="sxs-lookup"><span data-stu-id="390d2-109">Stability for your application by locking to specific API versions.</span></span>
 - <span data-ttu-id="390d2-110">Compatibility for your application with Azure Stack and regional Azure datacenters.</span><span class="sxs-lookup"><span data-stu-id="390d2-110">Compatibility for your application with Azure Stack and regional Azure datacenters.</span></span>

<span data-ttu-id="390d2-111">In the Go SDK, profiles are available under the profiles/ path, with their version in the **YYYY-MM-DD** format.</span><span class="sxs-lookup"><span data-stu-id="390d2-111">In the Go SDK, profiles are available under the profiles/ path, with their version in the **YYYY-MM-DD** format.</span></span> <span data-ttu-id="390d2-112">Right now, the latest Azure Stack profile version is **2017-03-09**.</span><span class="sxs-lookup"><span data-stu-id="390d2-112">Right now, the latest Azure Stack profile version is **2017-03-09**.</span></span> <span data-ttu-id="390d2-113">To import a given service from a profile, you need to import its corresponding module from the profile.</span><span class="sxs-lookup"><span data-stu-id="390d2-113">To import a given service from a profile, you need to import its corresponding module from the profile.</span></span> <span data-ttu-id="390d2-114">For example, to import **Compute** service from **2017-03-09** profile:</span><span class="sxs-lookup"><span data-stu-id="390d2-114">For example, to import **Compute** service from **2017-03-09** profile:</span></span>

````go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/compute/mgmt/compute" 
````

## <a name="install-azure-sdk-for-go"></a><span data-ttu-id="390d2-115">Install Azure SDK for Go</span><span class="sxs-lookup"><span data-stu-id="390d2-115">Install Azure SDK for Go</span></span>

  1. <span data-ttu-id="390d2-116">Install Git.</span><span class="sxs-lookup"><span data-stu-id="390d2-116">Install Git.</span></span> <span data-ttu-id="390d2-117">For instructions, see [Getting Started - Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span><span class="sxs-lookup"><span data-stu-id="390d2-117">For instructions, see [Getting Started - Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
  2. <span data-ttu-id="390d2-118">Install the [Go Programming Language](https://golang.org/dl).</span><span class="sxs-lookup"><span data-stu-id="390d2-118">Install the [Go Programming Language](https://golang.org/dl).</span></span>  
  <span data-ttu-id="390d2-119">API profiles for Azure will require Go version 1.9 or newer.</span><span class="sxs-lookup"><span data-stu-id="390d2-119">API profiles for Azure will require Go version 1.9 or newer.</span></span>
  3. <span data-ttu-id="390d2-120">Install the Go Azure SDK and its dependencies by running the following bash command:</span><span class="sxs-lookup"><span data-stu-id="390d2-120">Install the Go Azure SDK and its dependencies by running the following bash command:</span></span>
  ```
    go get -u -d github.com/Azure/azure-sdk-for-go/...
  ```

### <a name="the-go-sdk"></a><span data-ttu-id="390d2-121">The GO SDK</span><span class="sxs-lookup"><span data-stu-id="390d2-121">The GO SDK</span></span>

<span data-ttu-id="390d2-122">You can find more information about the Azure GO SDK at:</span><span class="sxs-lookup"><span data-stu-id="390d2-122">You can find more information about the Azure GO SDK at:</span></span>
- <span data-ttu-id="390d2-123">The Azure Go SDK at [Installing the Azure SDK for Go](https://docs.microsoft.com/go/azure/azure-sdk-go-install).</span><span class="sxs-lookup"><span data-stu-id="390d2-123">The Azure Go SDK at [Installing the Azure SDK for Go](https://docs.microsoft.com/go/azure/azure-sdk-go-install).</span></span>
- <span data-ttu-id="390d2-124">The Azure Go SDK is publicly available on GitHub at [azure-sdk-for-go](https://github.com/Azure/azure-sdk-for-go).</span><span class="sxs-lookup"><span data-stu-id="390d2-124">The Azure Go SDK is publicly available on GitHub at [azure-sdk-for-go](https://github.com/Azure/azure-sdk-for-go).</span></span>

### <a name="go-autorest-dependencies"></a><span data-ttu-id="390d2-125">Go-AutoRest dependencies</span><span class="sxs-lookup"><span data-stu-id="390d2-125">Go-AutoRest dependencies</span></span>

<span data-ttu-id="390d2-126">The GO SDK depends on the Azure Go-AutoRest modules to send REST requests to Azure Resource Manager endpoints.</span><span class="sxs-lookup"><span data-stu-id="390d2-126">The GO SDK depends on the Azure Go-AutoRest modules to send REST requests to Azure Resource Manager endpoints.</span></span> <span data-ttu-id="390d2-127">You will need to import the Azure Go-AutoRest module dependencies from [Azure Go-AutoRest on GitHub](https://github.com/Azure/go-autorest).</span><span class="sxs-lookup"><span data-stu-id="390d2-127">You will need to import the Azure Go-AutoRest module dependencies from [Azure Go-AutoRest on GitHub](https://github.com/Azure/go-autorest).</span></span> <span data-ttu-id="390d2-128">You can find the install bash commands in the **Install** section.</span><span class="sxs-lookup"><span data-stu-id="390d2-128">You can find the install bash commands in the **Install** section.</span></span>

## <a name="how-to-use-go-sdk-profiles-on-azure-stack"></a><span data-ttu-id="390d2-129">How to use GO SDK profiles on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="390d2-129">How to use GO SDK profiles on Azure Stack</span></span>

<span data-ttu-id="390d2-130">To run a sample of Go code on Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="390d2-130">To run a sample of Go code on Azure Stack:</span></span>
  1. <span data-ttu-id="390d2-131">Install Azure SDK for Go and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="390d2-131">Install Azure SDK for Go and its dependencies.</span></span> <span data-ttu-id="390d2-132">For instruction see the previous section, [Install Azure SDK for Go](#install-azure-sdk-for-go).</span><span class="sxs-lookup"><span data-stu-id="390d2-132">For instruction see the previous section, [Install Azure SDK for Go](#install-azure-sdk-for-go).</span></span>
  2. <span data-ttu-id="390d2-133">Get the metadata information from the Resource Manager endpoint.</span><span class="sxs-lookup"><span data-stu-id="390d2-133">Get the metadata information from the Resource Manager endpoint.</span></span> <span data-ttu-id="390d2-134">The endpoint returns a JSON file with the information required to run your Go code.</span><span class="sxs-lookup"><span data-stu-id="390d2-134">The endpoint returns a JSON file with the information required to run your Go code.</span></span>

  > [!Note]  
  > <span data-ttu-id="390d2-135">The **ResourceManagerUrl** in the Azure Stack Development Kit (ASDK) is: `https://management.local.azurestack.external/`</span><span class="sxs-lookup"><span data-stu-id="390d2-135">The **ResourceManagerUrl** in the Azure Stack Development Kit (ASDK) is: `https://management.local.azurestack.external/`</span></span>  
  > <span data-ttu-id="390d2-136">The **ResourceManagerUrl** in integrated systems is: `https://management.<location>.ext-<machine-name>.masd.stbtest.microsoft.com/`</span><span class="sxs-lookup"><span data-stu-id="390d2-136">The **ResourceManagerUrl** in integrated systems is: `https://management.<location>.ext-<machine-name>.masd.stbtest.microsoft.com/`</span></span>  
  > <span data-ttu-id="390d2-137">To retrieve the metadata required: `<ResourceManagerUrl>/metadata/endpoints?api-version=1.0`</span><span class="sxs-lookup"><span data-stu-id="390d2-137">To retrieve the metadata required: `<ResourceManagerUrl>/metadata/endpoints?api-version=1.0`</span></span>
  
  <span data-ttu-id="390d2-138">Sample JSON file:</span><span class="sxs-lookup"><span data-stu-id="390d2-138">Sample JSON file:</span></span>

  ```json
  { "galleryEndpoint": "https://portal.local.azurestack.external:30015/",  
    "graphEndpoint": "https://graph.windows.net/",  
    "portal Endpoint": "https://portal.local.azurestack.external/", 
    "authentication": {
      "loginEndpoint": "https://login.windows.net/", 
      "audiences": ["https://management.<yourtenant>.onmicrosoft.com/3cc5febd-e4b7-4a85-a2ed-1d730e2f5928"]
    }
  }
  ```

  3. <span data-ttu-id="390d2-139">If not available, create a subscription and save the subscription ID to be used later.</span><span class="sxs-lookup"><span data-stu-id="390d2-139">If not available, create a subscription and save the subscription ID to be used later.</span></span> <span data-ttu-id="390d2-140">For information on creating a subscription, see [Create subscriptions to offers in Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-subscribe-plan-provision-vm).</span><span class="sxs-lookup"><span data-stu-id="390d2-140">For information on creating a subscription, see [Create subscriptions to offers in Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-subscribe-plan-provision-vm).</span></span> 
  4. <span data-ttu-id="390d2-141">Create a service principal with "Subscription" scope and **Owner** role.</span><span class="sxs-lookup"><span data-stu-id="390d2-141">Create a service principal with "Subscription" scope and **Owner** role.</span></span> <span data-ttu-id="390d2-142">Save the service principals ID and secret.</span><span class="sxs-lookup"><span data-stu-id="390d2-142">Save the service principals ID and secret.</span></span> <span data-ttu-id="390d2-143">For information on creating a service principal for Azure Stack, see [Create service principal](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals#create-service-principal-for-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="390d2-143">For information on creating a service principal for Azure Stack, see [Create service principal](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals#create-service-principal-for-azure-ad).</span></span> <span data-ttu-id="390d2-144">Your Azure Stack environment is set up.</span><span class="sxs-lookup"><span data-stu-id="390d2-144">Your Azure Stack environment is set up.</span></span>
  5. <span data-ttu-id="390d2-145">Import a service module from Go SDK profile in your code.</span><span class="sxs-lookup"><span data-stu-id="390d2-145">Import a service module from Go SDK profile in your code.</span></span> <span data-ttu-id="390d2-146">The current version of Azure Stack profile is **2017-03-09**.</span><span class="sxs-lookup"><span data-stu-id="390d2-146">The current version of Azure Stack profile is **2017-03-09**.</span></span> <span data-ttu-id="390d2-147">For example, to import network module from **2017-03-09** profile type:</span><span class="sxs-lookup"><span data-stu-id="390d2-147">For example, to import network module from **2017-03-09** profile type:</span></span> 

  ````go
    package main 
    import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/network/mgmt/network"
  ````
  
  6. <span data-ttu-id="390d2-148">In your function, create and authenticate a client with a **New** Client function call.</span><span class="sxs-lookup"><span data-stu-id="390d2-148">In your function, create and authenticate a client with a **New** Client function call.</span></span> <span data-ttu-id="390d2-149">To create a virtual network client, you can use the following code:</span><span class="sxs-lookup"><span data-stu-id="390d2-149">To create a virtual network client, you can use the following code:</span></span>  

  ````go
  package main 

  import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/network/mgmt/network" 

  func main() { 
      vnetClient := network.NewVirtualNetworksClientWithBaseURI("<baseURI>", "(subscriptionID>")
      vnetClient.Authorizer = autorest.NewBearerAuthorizer(token)
  ````

  <span data-ttu-id="390d2-150">Set `<baseURI>` to the **ResourceManagerUrl** value used in step two.</span><span class="sxs-lookup"><span data-stu-id="390d2-150">Set `<baseURI>` to the **ResourceManagerUrl** value used in step two.</span></span>
  <span data-ttu-id="390d2-151">Set `<subscriptionID>` to the **SubscriptionID** value saved from step three.</span><span class="sxs-lookup"><span data-stu-id="390d2-151">Set `<subscriptionID>` to the **SubscriptionID** value saved from step three.</span></span>
  <span data-ttu-id="390d2-152">To create token, see Authentication section below.</span><span class="sxs-lookup"><span data-stu-id="390d2-152">To create token, see Authentication section below.</span></span>  

  7. <span data-ttu-id="390d2-153">Invoke API methods by using the client that you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="390d2-153">Invoke API methods by using the client that you created in the previous step.</span></span> <span data-ttu-id="390d2-154">For example, to create a virtual network by using our client from previous step:</span><span class="sxs-lookup"><span data-stu-id="390d2-154">For example, to create a virtual network by using our client from previous step:</span></span> 
  
````go
package main

import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/network/mgmt/network" 
func main() { 
  vnetC1ient := network.NewVirtualNetworksClientWithBaseURI("<baseURI>", "(subscriptionID>")
  vnetClient .Authorizer = autorest.NewBearerAuthorizer(token)

  vnetClient .CreateOrUpdate( ) 
````
  
  <span data-ttu-id="390d2-155">For a complete example of creating a virtual network on Azure Stack by using Go SDK profile, see [Example](#example).</span><span class="sxs-lookup"><span data-stu-id="390d2-155">For a complete example of creating a virtual network on Azure Stack by using Go SDK profile, see [Example](#example).</span></span>

## <a name="authentication"></a><span data-ttu-id="390d2-156">Authentication</span><span class="sxs-lookup"><span data-stu-id="390d2-156">Authentication</span></span>

<span data-ttu-id="390d2-157">To get the Authorizer property from Azure Active Directory using Go SDK, install the Go-AutoRest modules.</span><span class="sxs-lookup"><span data-stu-id="390d2-157">To get the Authorizer property from Azure Active Directory using Go SDK, install the Go-AutoRest modules.</span></span> <span data-ttu-id="390d2-158">These modules should have been already installed with the "Go SDK" installation; if not, install the [authentication package on GitHub](https://github.com/Azure/go-autorest/tree/master/autorest/adal).</span><span class="sxs-lookup"><span data-stu-id="390d2-158">These modules should have been already installed with the "Go SDK" installation; if not, install the [authentication package on GitHub](https://github.com/Azure/go-autorest/tree/master/autorest/adal).</span></span>

<span data-ttu-id="390d2-159">The Authorizer must be set as the authorizer for the resource client.</span><span class="sxs-lookup"><span data-stu-id="390d2-159">The Authorizer must be set as the authorizer for the resource client.</span></span> <span data-ttu-id="390d2-160">There are different methods to get an Authorizer; for a complete list see here.</span><span class="sxs-lookup"><span data-stu-id="390d2-160">There are different methods to get an Authorizer; for a complete list see here.</span></span>

<span data-ttu-id="390d2-161">This section presents a common way to get authorizer tokens on Azure Stack by using client credentials:</span><span class="sxs-lookup"><span data-stu-id="390d2-161">This section presents a common way to get authorizer tokens on Azure Stack by using client credentials:</span></span>

  1. <span data-ttu-id="390d2-162">If a service principal with owner role on the subscription is available, skip this step.</span><span class="sxs-lookup"><span data-stu-id="390d2-162">If a service principal with owner role on the subscription is available, skip this step.</span></span> <span data-ttu-id="390d2-163">Otherwise create a service principal [instructions]( https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals) and assign it an "owner" role scoped to your subscription [instructions]( https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals#assign-role-to-service-principal).</span><span class="sxs-lookup"><span data-stu-id="390d2-163">Otherwise create a service principal [instructions]( https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals) and assign it an "owner" role scoped to your subscription [instructions]( https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals#assign-role-to-service-principal).</span></span> <span data-ttu-id="390d2-164">Save the service principal application ID and secret.</span><span class="sxs-lookup"><span data-stu-id="390d2-164">Save the service principal application ID and secret.</span></span> 

  2. <span data-ttu-id="390d2-165">Import **adal** package from Go-AutoRest in your code.</span><span class="sxs-lookup"><span data-stu-id="390d2-165">Import **adal** package from Go-AutoRest in your code.</span></span> 
  
  ````go
  package main
  import "github.com/Azure/go-autorest/autorest/adal" 
  ````

  3. <span data-ttu-id="390d2-166">Create an oauthConfig by using NewOAuthConfig method from **adal** module.</span><span class="sxs-lookup"><span data-stu-id="390d2-166">Create an oauthConfig by using NewOAuthConfig method from **adal** module.</span></span> 
  
  ````go
  package main 

  import "github.com/Azure/go-autorest/autorest/ada1" 

  func CreateToken() (adal.OAuthTokenProvider, error) {
      var token adal.OAuthTokenProvider
      oauthConfig, err := adal.NewOAuthConfig(activeDirectoryEndpoint, tenantID)
  ````
   
  <span data-ttu-id="390d2-167">Set `<activeDirectoryEndpoint>` to the value of "loginEndpoint" property from the ResourceManagerUrl metadata retrieved on the previous section of this document.</span><span class="sxs-lookup"><span data-stu-id="390d2-167">Set `<activeDirectoryEndpoint>` to the value of "loginEndpoint" property from the ResourceManagerUrl metadata retrieved on the previous section of this document.</span></span>
  <span data-ttu-id="390d2-168">Set `<tenantID>` value to your Azure Stack tenant ID.</span><span class="sxs-lookup"><span data-stu-id="390d2-168">Set `<tenantID>` value to your Azure Stack tenant ID.</span></span> 

  4. <span data-ttu-id="390d2-169">Finally, create a service principal token by using NewServicePrincipalToken method from adal module.</span><span class="sxs-lookup"><span data-stu-id="390d2-169">Finally, create a service principal token by using NewServicePrincipalToken method from adal module.</span></span> 

  ````go
  package main 

  import "github.com/Azure/go-autorest/autorest/adal" 

  func CreateToken() (adal.OAuthTokenProvider, error) {
      var token adal.OAuthTokenProvider
      oauthConfig, err := adal.NewOAuthConfig(activeDirectoryEndpoint, tenantID)
      token, err = adal.NewServicePrincipalToken(
          *oauthConfig,
          clientID,
          clientSecret,
          activeDirectoryResourceID)
      return token, err
  ````
  
  <span data-ttu-id="390d2-170">Set `<activeDirectoryResourceID>` to one of the values in the "audience" list from the ResourceManagerUrl metadata retrieved on the previous section of this document.</span><span class="sxs-lookup"><span data-stu-id="390d2-170">Set `<activeDirectoryResourceID>` to one of the values in the "audience" list from the ResourceManagerUrl metadata retrieved on the previous section of this document.</span></span>  
  <span data-ttu-id="390d2-171">Set `<clientID>` to the service principal application ID saved when service principal was created on the previous section of this document.</span><span class="sxs-lookup"><span data-stu-id="390d2-171">Set `<clientID>` to the service principal application ID saved when service principal was created on the previous section of this document.</span></span>  
  <span data-ttu-id="390d2-172">Set `<clientSecret>` to the service principal application Secret saved when service principal was created on the previous section of this document.</span><span class="sxs-lookup"><span data-stu-id="390d2-172">Set `<clientSecret>` to the service principal application Secret saved when service principal was created on the previous section of this document.</span></span>  

## <a name="example"></a><span data-ttu-id="390d2-173">Example</span><span class="sxs-lookup"><span data-stu-id="390d2-173">Example</span></span>

<span data-ttu-id="390d2-174">This section shows a sample of Go code to create virtual network on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="390d2-174">This section shows a sample of Go code to create virtual network on Azure Stack.</span></span> <span data-ttu-id="390d2-175">For complete examples of Go SDK see [Azure Go SDk samples repository](https://github.com/Azure-Samples/azure-sdk-for-go-samples).</span><span class="sxs-lookup"><span data-stu-id="390d2-175">For complete examples of Go SDK see [Azure Go SDk samples repository](https://github.com/Azure-Samples/azure-sdk-for-go-samples).</span></span> <span data-ttu-id="390d2-176">Azure Stack samples are available under hybrid/ path inside service folders of the repository.</span><span class="sxs-lookup"><span data-stu-id="390d2-176">Azure Stack samples are available under hybrid/ path inside service folders of the repository.</span></span>

> [!Note]  
> <span data-ttu-id="390d2-177">To run the code in this example, verify that the subscription used has **Network** resource provider listed as **Registered**.</span><span class="sxs-lookup"><span data-stu-id="390d2-177">To run the code in this example, verify that the subscription used has **Network** resource provider listed as **Registered**.</span></span> <span data-ttu-id="390d2-178">To verify it, look for the Subscription in the Azure Stack portal, and click on **Resource providers.**</span><span class="sxs-lookup"><span data-stu-id="390d2-178">To verify it, look for the Subscription in the Azure Stack portal, and click on **Resource providers.**</span></span>

1. <span data-ttu-id="390d2-179">Import required packages in your code.</span><span class="sxs-lookup"><span data-stu-id="390d2-179">Import required packages in your code.</span></span> <span data-ttu-id="390d2-180">You should use the latest available profile on Azure Stack to import the network module.</span><span class="sxs-lookup"><span data-stu-id="390d2-180">You should use the latest available profile on Azure Stack to import the network module.</span></span> 
  
  ````go
  package main

  import (
      "context"
      "fmt"
      "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/network/mgmt/network"
      "github.com/Azure/go-autorest/autorest"
      "github.com/Azure/go-autorest/autorest/adal"
      "github.com/Azure/go-autorest/autorest/to"
  )
  ````

2. <span data-ttu-id="390d2-181">Define your environment variables.</span><span class="sxs-lookup"><span data-stu-id="390d2-181">Define your environment variables.</span></span> <span data-ttu-id="390d2-182">To create a virtual network you need to have a resource group.</span><span class="sxs-lookup"><span data-stu-id="390d2-182">To create a virtual network you need to have a resource group.</span></span> 

  ````go
  var (
      activeDirectoryEndpoint = "yourLoginEndpointFromResourceManagerUrlMetadata"
      tenantID = "yourAzureStackTenantID"
      clientID = "yourServicePrincipalApplicationID"
      clientSecret = "yourServicePrincipalSecret"
      activeDirectoryResourceID = "yourAudienceFromResourceManagerUrlMetadata"
      subscriptionID = "yourSubscriptionID"
      baseURI = "yourResourceManagerURL"
      resourceGroupName = "existingResourceGroupName"
  )
  ````

3. <span data-ttu-id="390d2-183">Now that you have defined your environment variables, add a method to create authentication token by using **adal** package.</span><span class="sxs-lookup"><span data-stu-id="390d2-183">Now that you have defined your environment variables, add a method to create authentication token by using **adal** package.</span></span> <span data-ttu-id="390d2-184">See details about authentication in previous section.</span><span class="sxs-lookup"><span data-stu-id="390d2-184">See details about authentication in previous section.</span></span>
  
  ````go
  //CreateToken creates a service principal token
  func CreateToken() (adal.OAuthTokenProvider, error) {
      var token adal.OAuthTokenProvider
      oauthConfig, err := adal.NewOAuthConfig(activeDirectoryEndpoint, tenantID)
      token, err = adal.NewServicePrincipalToken(
          *oauthConfig,
          clientID,
          clientSecret,
          activeDirectoryResourceID)
      return token, err
  }
  ````

4. <span data-ttu-id="390d2-185">Add the main method.</span><span class="sxs-lookup"><span data-stu-id="390d2-185">Add the main method.</span></span> <span data-ttu-id="390d2-186">The main method first gets a token by using the method that is defined in previous step.</span><span class="sxs-lookup"><span data-stu-id="390d2-186">The main method first gets a token by using the method that is defined in previous step.</span></span> <span data-ttu-id="390d2-187">Then, it creates a client by using network module from profile.</span><span class="sxs-lookup"><span data-stu-id="390d2-187">Then, it creates a client by using network module from profile.</span></span> <span data-ttu-id="390d2-188">Finally, it creates a virtual network.</span><span class="sxs-lookup"><span data-stu-id="390d2-188">Finally, it creates a virtual network.</span></span> 
  
````go
package main

import (
    "context"
    "fmt"
    "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/network/mgmt/network"
    "github.com/Azure/go-autorest/autorest"
    "github.com/Azure/go-autorest/autorest/adal"
    "github.com/Azure/go-autorest/autorest/to"
)

var (
    activeDirectoryEndpoint = "yourLoginEndpointFromResourceManagerUrlMetadata"
    tenantID = "yourAzureStackTenantID"
    clientID = "yourServicePrincipalApplicationID"
    clientSecret = "yourServicePrincipalSecret"
    activeDirectoryResourceID = "yourAudienceFromResourceManagerUrlMetadata"
    subscriptionID = "yourSubscriptionID"
    baseURI = "yourResourceManagerURL"
    resourceGroupName = "existingResourceGroupName"
)

//CreateToken creates a service principal token
func CreateToken() (adal.OAuthTokenProvider, error) {
    var token adal.OAuthTokenProvider
    oauthConfig, err := adal.NewOAuthConfig(activeDirectoryEndpoint, tenantID)
    token, err = adal.NewServicePrincipalToken(
        *oauthConfig,
        clientID,
        clientSecret,
        activeDirectoryResourceID)
    return token, err
}

func main() {
    token, _ := CreateToken()
    vnetClient := network.NewVirtualNetworksClientWithBaseURI(baseURI, subscriptionID)
    vnetClient.Authorizer = autorest.NewBearerAuthorizer(token)
    future, _ := vnetClient.CreateOrUpdate(
        context.Background(),
        resourceGroupName,
        "sampleVnetName",
        network.VirtualNetwork{
            Location: to.StringPtr("local"),
            VirtualNetworkPropertiesFormat: &network.VirtualNetworkPropertiesFormat{
                AddressSpace: &network.AddressSpace{
                    AddressPrefixes: &[]string{"10.0.0.0/8"},
                },
                Subnets: &[]network.Subnet{
                    {
                        Name: to.StringPtr("subnetName"),
                        SubnetPropertiesFormat: &network.SubnetPropertiesFormat{
                            AddressPrefix: to.StringPtr("10.0.0.0/16"),
                        },
                    },
                },
            },
        })
    err := future.WaitForCompletion(context.Background(), vnetClient.Client)
    if err != nil {
        fmt.Printf(err.Error())
        return
    }
}

````

## <a name="next-steps"></a><span data-ttu-id="390d2-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="390d2-189">Next steps</span></span>
* [<span data-ttu-id="390d2-190">Install PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="390d2-190">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)
* [<span data-ttu-id="390d2-191">Configure the Azure Stack user's PowerShell environment</span><span class="sxs-lookup"><span data-stu-id="390d2-191">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
