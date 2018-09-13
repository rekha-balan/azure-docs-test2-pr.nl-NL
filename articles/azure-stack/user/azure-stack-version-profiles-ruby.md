---
title: Using API version profiles with Ruby in Azure Stack | Microsoft Docs
description: Learn about using API version profiles with Ruby in Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: B82E4979-FB78-4522-B9A1-84222D4F854B
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: sijuman
ms.openlocfilehash: a000a54f79e479567168992cdd0786eb9e8b5c32
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856118"
---
# <a name="use-api-version-profiles-with-ruby-in-azure-stack"></a><span data-ttu-id="937ff-103">Use API version profiles with Ruby in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="937ff-103">Use API version profiles with Ruby in Azure Stack</span></span>

<span data-ttu-id="937ff-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="937ff-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

## <a name="ruby-and-api-version-profiles"></a><span data-ttu-id="937ff-105">Ruby and API version profiles</span><span class="sxs-lookup"><span data-stu-id="937ff-105">Ruby and API version profiles</span></span>

<span data-ttu-id="937ff-106">The Ruby SDK for the Azure Stack Resource Manager provides tools to help you build and manage your infrastructure.</span><span class="sxs-lookup"><span data-stu-id="937ff-106">The Ruby SDK for the Azure Stack Resource Manager provides tools to help you build and manage your infrastructure.</span></span> <span data-ttu-id="937ff-107">Resource providers in the SDK include compute, virtual networks, and storage with the Ruby language.</span><span class="sxs-lookup"><span data-stu-id="937ff-107">Resource providers in the SDK include compute, virtual networks, and storage with the Ruby language.</span></span> <span data-ttu-id="937ff-108">API profiles in the Ruby SDK enable hybrid cloud development by helping you switch between global Azure resources and resources on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="937ff-108">API profiles in the Ruby SDK enable hybrid cloud development by helping you switch between global Azure resources and resources on Azure Stack.</span></span>

<span data-ttu-id="937ff-109">An API profile is a combination of resource providers and service versions.</span><span class="sxs-lookup"><span data-stu-id="937ff-109">An API profile is a combination of resource providers and service versions.</span></span> <span data-ttu-id="937ff-110">You can use an API profile to combine different resource types.</span><span class="sxs-lookup"><span data-stu-id="937ff-110">You can use an API profile to combine different resource types.</span></span>

 - <span data-ttu-id="937ff-111">To make use of the latest versions of all the services, use the **Latest** profile of the Azure SDK rollup gem.</span><span class="sxs-lookup"><span data-stu-id="937ff-111">To make use of the latest versions of all the services, use the **Latest** profile of the Azure SDK rollup gem.</span></span>
 - <span data-ttu-id="937ff-112">To use the services compatible with the Azure Stack, use the **V2017_03_09** profile of the Azure SDK rollup gem.</span><span class="sxs-lookup"><span data-stu-id="937ff-112">To use the services compatible with the Azure Stack, use the **V2017_03_09** profile of the Azure SDK rollup gem.</span></span>
 - <span data-ttu-id="937ff-113">To use the latest api-version of a service, use the **Latest** profile of the specific gem.</span><span class="sxs-lookup"><span data-stu-id="937ff-113">To use the latest api-version of a service, use the **Latest** profile of the specific gem.</span></span> <span data-ttu-id="937ff-114">For example, if you would like to use the latest api-version of compute service alone, use the **Latest** profile of the **Compute** gem.</span><span class="sxs-lookup"><span data-stu-id="937ff-114">For example, if you would like to use the latest api-version of compute service alone, use the **Latest** profile of the **Compute** gem.</span></span>
 - <span data-ttu-id="937ff-115">To use specific api-version for a service, use the specific API versions defined inside the gem.</span><span class="sxs-lookup"><span data-stu-id="937ff-115">To use specific api-version for a service, use the specific API versions defined inside the gem.</span></span>

> [!Note]   
> <span data-ttu-id="937ff-116">You can combine all of the options in the same application.</span><span class="sxs-lookup"><span data-stu-id="937ff-116">You can combine all of the options in the same application.</span></span>

## <a name="install-the-azure-ruby-sdk"></a><span data-ttu-id="937ff-117">Install the Azure Ruby SDK</span><span class="sxs-lookup"><span data-stu-id="937ff-117">Install the Azure Ruby SDK</span></span>

 - <span data-ttu-id="937ff-118">Follow official instructions to install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span><span class="sxs-lookup"><span data-stu-id="937ff-118">Follow official instructions to install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
 - <span data-ttu-id="937ff-119">Follow official instructions to install [Ruby](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="937ff-119">Follow official instructions to install [Ruby](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
    - <span data-ttu-id="937ff-120">While installing choose **Add Ruby to PATH variable**</span><span class="sxs-lookup"><span data-stu-id="937ff-120">While installing choose **Add Ruby to PATH variable**</span></span>
    - <span data-ttu-id="937ff-121">Install Dev kit during Ruby installation when prompted.</span><span class="sxs-lookup"><span data-stu-id="937ff-121">Install Dev kit during Ruby installation when prompted.</span></span>
    - <span data-ttu-id="937ff-122">Next, install bundler using the following command:</span><span class="sxs-lookup"><span data-stu-id="937ff-122">Next, install bundler using the following command:</span></span>  
      `Gem install bundler`
 - <span data-ttu-id="937ff-123">If not available, create a subscription and save the Subscription ID to be used later.</span><span class="sxs-lookup"><span data-stu-id="937ff-123">If not available, create a subscription and save the Subscription ID to be used later.</span></span> <span data-ttu-id="937ff-124">Instructions to create a subscription are [here](https://docs.microsoft.com/azure/azure-stack/azure-stack-subscribe-plan-provision-vm).</span><span class="sxs-lookup"><span data-stu-id="937ff-124">Instructions to create a subscription are [here](https://docs.microsoft.com/azure/azure-stack/azure-stack-subscribe-plan-provision-vm).</span></span> 
 - <span data-ttu-id="937ff-125">Create a service principal and save its ID and secret.</span><span class="sxs-lookup"><span data-stu-id="937ff-125">Create a service principal and save its ID and secret.</span></span> <span data-ttu-id="937ff-126">Instructions to create a service principal for Azure Stack are [here](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals).</span><span class="sxs-lookup"><span data-stu-id="937ff-126">Instructions to create a service principal for Azure Stack are [here](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals).</span></span> 
 - <span data-ttu-id="937ff-127">Make sure your service principal has contributor/owner role on your subscription.</span><span class="sxs-lookup"><span data-stu-id="937ff-127">Make sure your service principal has contributor/owner role on your subscription.</span></span> <span data-ttu-id="937ff-128">Instructions on how to assign role to service principal are [here](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals).</span><span class="sxs-lookup"><span data-stu-id="937ff-128">Instructions on how to assign role to service principal are [here](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals).</span></span>

## <a name="install-the-rubygem-packages"></a><span data-ttu-id="937ff-129">Install the rubygem packages</span><span class="sxs-lookup"><span data-stu-id="937ff-129">Install the rubygem packages</span></span>

<span data-ttu-id="937ff-130">You can install the azure rubygem packages directly.</span><span class="sxs-lookup"><span data-stu-id="937ff-130">You can install the azure rubygem packages directly.</span></span>

````Ruby  
gem install azure_mgmt_compute
gem install azure_mgmt_storage
gem install azure_mgmt_resources
gem install azure_mgmt_network
Or use them in your Gemfile.
gem 'azure_mgmt_storage'
gem 'azure_mgmt_compute'
gem 'azure_mgmt_resources'
gem 'azure_mgmt_network'
````

<span data-ttu-id="937ff-131">Be aware the Azure Resource Manager Ruby SDK is in preview and will likely have breaking interface changes in upcoming releases.</span><span class="sxs-lookup"><span data-stu-id="937ff-131">Be aware the Azure Resource Manager Ruby SDK is in preview and will likely have breaking interface changes in upcoming releases.</span></span> <span data-ttu-id="937ff-132">An increased number in Minor version may indicate breaking changes.</span><span class="sxs-lookup"><span data-stu-id="937ff-132">An increased number in Minor version may indicate breaking changes.</span></span>

## <a name="usage-of-the-azuresdk-gem"></a><span data-ttu-id="937ff-133">Usage of the azure_sdk gem</span><span class="sxs-lookup"><span data-stu-id="937ff-133">Usage of the azure_sdk gem</span></span>

<span data-ttu-id="937ff-134">The gem, azure_sdk, is a rollup of all the supported gems in the Ruby SDK.</span><span class="sxs-lookup"><span data-stu-id="937ff-134">The gem, azure_sdk, is a rollup of all the supported gems in the Ruby SDK.</span></span> <span data-ttu-id="937ff-135">This gem consists of a **Latest** profile, which supports the latest version of all services.</span><span class="sxs-lookup"><span data-stu-id="937ff-135">This gem consists of a **Latest** profile, which supports the latest version of all services.</span></span> <span data-ttu-id="937ff-136">It introduces a versioned profile **V2017_03_09** profile, which is built for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="937ff-136">It introduces a versioned profile **V2017_03_09** profile, which is built for Azure Stack.</span></span>

<span data-ttu-id="937ff-137">You can install the azure_sdk rollup gem with the following command:</span><span class="sxs-lookup"><span data-stu-id="937ff-137">You can install the azure_sdk rollup gem with the following command:</span></span>  

````Ruby  
  gem install 'azure_sdk
````

## <a name="prerequisite"></a><span data-ttu-id="937ff-138">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="937ff-138">Prerequisite</span></span>

<span data-ttu-id="937ff-139">In order to use Ruby Azure SDK with Azure Stack, you must supply the following values, and then set values with environment variables.</span><span class="sxs-lookup"><span data-stu-id="937ff-139">In order to use Ruby Azure SDK with Azure Stack, you must supply the following values, and then set values with environment variables.</span></span> <span data-ttu-id="937ff-140">See the instructions after the table for your operating system on setting the environmental variables.</span><span class="sxs-lookup"><span data-stu-id="937ff-140">See the instructions after the table for your operating system on setting the environmental variables.</span></span> 

| <span data-ttu-id="937ff-141">Value</span><span class="sxs-lookup"><span data-stu-id="937ff-141">Value</span></span> | <span data-ttu-id="937ff-142">Environment variables</span><span class="sxs-lookup"><span data-stu-id="937ff-142">Environment variables</span></span> | <span data-ttu-id="937ff-143">Description</span><span class="sxs-lookup"><span data-stu-id="937ff-143">Description</span></span> | 
| --- | --- | --- | --- |
| <span data-ttu-id="937ff-144">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="937ff-144">Tenant ID</span></span> | <span data-ttu-id="937ff-145">AZURE_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="937ff-145">AZURE_TENANT_ID</span></span> | <span data-ttu-id="937ff-146">The value of your Azure Stack [tenant ID](https://docs.microsoft.com/azure/azure-stack/azure-stack-identity-overview).</span><span class="sxs-lookup"><span data-stu-id="937ff-146">The value of your Azure Stack [tenant ID](https://docs.microsoft.com/azure/azure-stack/azure-stack-identity-overview).</span></span> |
| <span data-ttu-id="937ff-147">Client ID</span><span class="sxs-lookup"><span data-stu-id="937ff-147">Client ID</span></span> | <span data-ttu-id="937ff-148">AZURE_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="937ff-148">AZURE_CLIENT_ID</span></span> | <span data-ttu-id="937ff-149">The service principal application ID saved when service principal was created on the previous section of this document.</span><span class="sxs-lookup"><span data-stu-id="937ff-149">The service principal application ID saved when service principal was created on the previous section of this document.</span></span>  |
| <span data-ttu-id="937ff-150">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="937ff-150">Subscription ID</span></span> | <span data-ttu-id="937ff-151">AZURE_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="937ff-151">AZURE_SUBSCRIPTION_ID</span></span> | <span data-ttu-id="937ff-152">The [subscription ID](https://docs.microsoft.com/azure/azure-stack/azure-stack-plan-offer-quota-overview#subscriptions) is how you access offers in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="937ff-152">The [subscription ID](https://docs.microsoft.com/azure/azure-stack/azure-stack-plan-offer-quota-overview#subscriptions) is how you access offers in Azure Stack.</span></span> |
| <span data-ttu-id="937ff-153">Client Secret</span><span class="sxs-lookup"><span data-stu-id="937ff-153">Client Secret</span></span> | <span data-ttu-id="937ff-154">AZURE_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="937ff-154">AZURE_CLIENT_SECRET</span></span> | <span data-ttu-id="937ff-155">The service principal application Secret saved when service principal was created.</span><span class="sxs-lookup"><span data-stu-id="937ff-155">The service principal application Secret saved when service principal was created.</span></span> |
| <span data-ttu-id="937ff-156">Resource Manager Endpoint</span><span class="sxs-lookup"><span data-stu-id="937ff-156">Resource Manager Endpoint</span></span> | <span data-ttu-id="937ff-157">ARM_ENDPOINT</span><span class="sxs-lookup"><span data-stu-id="937ff-157">ARM_ENDPOINT</span></span> | <span data-ttu-id="937ff-158">See [The Azure Stack resource manager endpoin](#The-azure-stack-resource-manager-endpoint).</span><span class="sxs-lookup"><span data-stu-id="937ff-158">See [The Azure Stack resource manager endpoin](#The-azure-stack-resource-manager-endpoint).</span></span>  |

### <a name="the-azure-stack-resource-manager-endpoint"></a><span data-ttu-id="937ff-159">The Azure Stack resource manager endpoint</span><span class="sxs-lookup"><span data-stu-id="937ff-159">The Azure Stack resource manager endpoint</span></span>

<span data-ttu-id="937ff-160">The Microsoft Azure Resource Manager is a management framework that allows administrators to deploy, manage and monitor Azure resources.</span><span class="sxs-lookup"><span data-stu-id="937ff-160">The Microsoft Azure Resource Manager is a management framework that allows administrators to deploy, manage and monitor Azure resources.</span></span> <span data-ttu-id="937ff-161">Azure Resource Manager can handle these tasks as a group, rather than individually, in a single operation.</span><span class="sxs-lookup"><span data-stu-id="937ff-161">Azure Resource Manager can handle these tasks as a group, rather than individually, in a single operation.</span></span>

<span data-ttu-id="937ff-162">You can get the metadata information from the Resource Manager endpoint.</span><span class="sxs-lookup"><span data-stu-id="937ff-162">You can get the metadata information from the Resource Manager endpoint.</span></span> <span data-ttu-id="937ff-163">The endpoint returns a JSON file with the information required to run your code.</span><span class="sxs-lookup"><span data-stu-id="937ff-163">The endpoint returns a JSON file with the information required to run your code.</span></span>

  > [!Note]  
  > <span data-ttu-id="937ff-164">The **ResourceManagerUrl** in the Azure Stack Development Kit (ASDK) is: `https://management.local.azurestack.external/`</span><span class="sxs-lookup"><span data-stu-id="937ff-164">The **ResourceManagerUrl** in the Azure Stack Development Kit (ASDK) is: `https://management.local.azurestack.external/`</span></span>  
  > <span data-ttu-id="937ff-165">The **ResourceManagerUrl** in integrated systems is: `https://management.<location>.ext-<machine-name>.masd.stbtest.microsoft.com/`</span><span class="sxs-lookup"><span data-stu-id="937ff-165">The **ResourceManagerUrl** in integrated systems is: `https://management.<location>.ext-<machine-name>.masd.stbtest.microsoft.com/`</span></span>  
  > <span data-ttu-id="937ff-166">To retrieve the metadata required: `<ResourceManagerUrl>/metadata/endpoints?api-version=1.0`</span><span class="sxs-lookup"><span data-stu-id="937ff-166">To retrieve the metadata required: `<ResourceManagerUrl>/metadata/endpoints?api-version=1.0`</span></span>
  
  <span data-ttu-id="937ff-167">Sample JSON file:</span><span class="sxs-lookup"><span data-stu-id="937ff-167">Sample JSON file:</span></span>

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

### <a name="set-environmental-variables"></a><span data-ttu-id="937ff-168">Set environmental variables</span><span class="sxs-lookup"><span data-stu-id="937ff-168">Set environmental variables</span></span>

<span data-ttu-id="937ff-169">**Microsoft Windows**</span><span class="sxs-lookup"><span data-stu-id="937ff-169">**Microsoft Windows**</span></span>  
<span data-ttu-id="937ff-170">To set the environment variables, in Windows Command Prompt, use the following format:</span><span class="sxs-lookup"><span data-stu-id="937ff-170">To set the environment variables, in Windows Command Prompt, use the following format:</span></span>  
`set AZURE_TENANT_ID=<YOUR_TENANT_ID>`

<span data-ttu-id="937ff-171">**macOS, Linux, and Unix-based systems**</span><span class="sxs-lookup"><span data-stu-id="937ff-171">**macOS, Linux, and Unix-based systems**</span></span>  
<span data-ttu-id="937ff-172">In Unix based systems, you could use the command such as:</span><span class="sxs-lookup"><span data-stu-id="937ff-172">In Unix based systems, you could use the command such as:</span></span>  
`export AZURE_TENANT_ID=<YOUR_TENANT_ID>`

## <a name="existing-api-profiles"></a><span data-ttu-id="937ff-173">Existing API profiles</span><span class="sxs-lookup"><span data-stu-id="937ff-173">Existing API profiles</span></span>

<span data-ttu-id="937ff-174">The azure_sdk rollup gem has the following two profiles:</span><span class="sxs-lookup"><span data-stu-id="937ff-174">The azure_sdk rollup gem has the following two profiles:</span></span>

1. <span data-ttu-id="937ff-175">**V2017_03_09**</span><span class="sxs-lookup"><span data-stu-id="937ff-175">**V2017_03_09**</span></span>  
  <span data-ttu-id="937ff-176">Profile built for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="937ff-176">Profile built for Azure Stack.</span></span> <span data-ttu-id="937ff-177">Use this profile for services to be most compatible with the Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="937ff-177">Use this profile for services to be most compatible with the Azure Stack.</span></span>
2. <span data-ttu-id="937ff-178">**Latest**</span><span class="sxs-lookup"><span data-stu-id="937ff-178">**Latest**</span></span>  
  <span data-ttu-id="937ff-179">Profile consists of latest versions of all services.</span><span class="sxs-lookup"><span data-stu-id="937ff-179">Profile consists of latest versions of all services.</span></span> <span data-ttu-id="937ff-180">Use the latest versions of all the services.</span><span class="sxs-lookup"><span data-stu-id="937ff-180">Use the latest versions of all the services.</span></span>

<span data-ttu-id="937ff-181">For more information about Azure Stack and API profiles, see a [Summary of API profiles](azure-stack-version-profiles.md#summary-of-api-profiles).</span><span class="sxs-lookup"><span data-stu-id="937ff-181">For more information about Azure Stack and API profiles, see a [Summary of API profiles](azure-stack-version-profiles.md#summary-of-api-profiles).</span></span>

## <a name="azure-ruby-sdk-api-profile-usage"></a><span data-ttu-id="937ff-182">Azure Ruby SDK API profile usage</span><span class="sxs-lookup"><span data-stu-id="937ff-182">Azure Ruby SDK API profile usage</span></span>

<span data-ttu-id="937ff-183">The following lines should be used to instantiate a profile client.</span><span class="sxs-lookup"><span data-stu-id="937ff-183">The following lines should be used to instantiate a profile client.</span></span> <span data-ttu-id="937ff-184">This parameter is only required for Azure Stack or other private clouds.</span><span class="sxs-lookup"><span data-stu-id="937ff-184">This parameter is only required for Azure Stack or other private clouds.</span></span> <span data-ttu-id="937ff-185">Global Azure already has these settings by default.</span><span class="sxs-lookup"><span data-stu-id="937ff-185">Global Azure already has these settings by default.</span></span>

````Ruby  
active_directory_settings = get_active_directory_settings(ENV['ARM_ENDPOINT'])

provider = MsRestAzure::ApplicationTokenProvider.new(
    ENV['AZURE_TENANT_ID'],
    ENV['AZURE_CLIENT_ID'],
    ENV['AZURE_CLIENT_SECRET'],
    active_directory_settings
)
credentials = MsRest::TokenCredentials.new(provider)
options = {
    credentials: credentials,
    subscription_id: subscription_id,
    active_directory_settings: active_directory_settings,
    base_url: ENV['ARM_ENDPOINT']
}

# Target profile built for Azure Stack
client = Azure::Resources::Profiles::V2017_03_09::Mgmt::Client.new(options)
````

<span data-ttu-id="937ff-186">The profile client can be used to access individual resource providers, such as compute, storage, and network.</span><span class="sxs-lookup"><span data-stu-id="937ff-186">The profile client can be used to access individual resource providers, such as compute, storage, and network.</span></span>

````Ruby  
# To access the operations associated with Compute
profile_client.compute.virtual_machines.get 'RESOURCE_GROUP_NAME', 'VIRTUAL_MACHINE_NAME'

# Option 1: To access the models associated with Compute
purchase_plan_obj = profile_client.compute.model_classes.purchase_plan.new

# Option 2: To access the models associated with Compute
# Notice Namespace: Azure::Profiles::<Profile Name>::<Service Name>::Mgmt::Models::<Model Name>
purchase_plan_obj = Azure::Profiles::V2017_03_09::Compute::Mgmt::Models::PurchasePlan.new
````

## <a name="define-azurestack-environment-setting-functions"></a><span data-ttu-id="937ff-187">Define AzureStack environment setting functions</span><span class="sxs-lookup"><span data-stu-id="937ff-187">Define AzureStack environment setting functions</span></span>

<span data-ttu-id="937ff-188">To authenticate the service principal to the Azure Stack environment, define the endpoints using **get_active_directory_settings()**.</span><span class="sxs-lookup"><span data-stu-id="937ff-188">To authenticate the service principal to the Azure Stack environment, define the endpoints using **get_active_directory_settings()**.</span></span> <span data-ttu-id="937ff-189">This method uses the **ARM_Endpoint** environment variable that you set when establishing your environmental variables.</span><span class="sxs-lookup"><span data-stu-id="937ff-189">This method uses the **ARM_Endpoint** environment variable that you set when establishing your environmental variables.</span></span>

````Ruby  
# Get Authentication endpoints using Arm Metadata Endpoints
def get_active_directory_settings(armEndpoint)
    settings = MsRestAzure::ActiveDirectoryServiceSettings.new
    response = Net::HTTP.get_response(URI("#{armEndpoint}/metadata/endpoints?api-version=1.0"))
    status_code = response.code
    response_content = response.body
    unless status_code == "200"
        error_model = JSON.load(response_content)
        fail MsRestAzure::AzureOperationError.new("Getting Azure Stack Metadata Endpoints", response, error_model)
    end
    result = JSON.load(response_content)
    settings.authentication_endpoint = result['authentication']['loginEndpoint'] unless result['authentication']['loginEndpoint'].nil?
    settings.token_audience = result['authentication']['audiences'][0] unless result['authentication']['audiences'][0].nil?
    settings
end
````

## <a name="samples-using-api-profiles"></a><span data-ttu-id="937ff-190">Samples using API profiles</span><span class="sxs-lookup"><span data-stu-id="937ff-190">Samples using API profiles</span></span>

<span data-ttu-id="937ff-191">You can use the following samples found in GitHub repositoreis as a reference creating solutions with Ruby and Azure Stack API profiles:</span><span class="sxs-lookup"><span data-stu-id="937ff-191">You can use the following samples found in GitHub repositoreis as a reference creating solutions with Ruby and Azure Stack API profiles:</span></span>

 - [<span data-ttu-id="937ff-192">Manage Azure resources and resource groups with Ruby</span><span class="sxs-lookup"><span data-stu-id="937ff-192">Manage Azure resources and resource groups with Ruby</span></span>](https://github.com/Azure-Samples/resource-manager-ruby-resources-and-groups/tree/master/Hybrid)
 - [<span data-ttu-id="937ff-193">Manage virtual machines using Ruby</span><span class="sxs-lookup"><span data-stu-id="937ff-193">Manage virtual machines using Ruby</span></span>](https://github.com/Azure-Samples/compute-ruby-manage-vm/tree/master/Hybrid)
 - [<span data-ttu-id="937ff-194">Deploy an SSH Enabled VM with a Template in Ruby</span><span class="sxs-lookup"><span data-stu-id="937ff-194">Deploy an SSH Enabled VM with a Template in Ruby</span></span>](https://github.com/Azure-Samples/resource-manager-ruby-template-deployment/tree/master/Hybrid)

### <a name="sample-resource-manager-and-groups"></a><span data-ttu-id="937ff-195">Sample Resource Manager and groups</span><span class="sxs-lookup"><span data-stu-id="937ff-195">Sample Resource Manager and groups</span></span>

<span data-ttu-id="937ff-196">To run the sample, ensure that you have installed Ruby.</span><span class="sxs-lookup"><span data-stu-id="937ff-196">To run the sample, ensure that you have installed Ruby.</span></span> <span data-ttu-id="937ff-197">If you are using Visual Studio Code, download the Ruby SDK as an extension as well.</span><span class="sxs-lookup"><span data-stu-id="937ff-197">If you are using Visual Studio Code, download the Ruby SDK as an extension as well.</span></span> 

> [!Note]  
> <span data-ttu-id="937ff-198">You can get the repository for the sample at "[Manage Azure resources and resource groups with Ruby](https://github.com/Azure-Samples/resource-manager-ruby-resources-and-groups/tree/master/Hybrid)".</span><span class="sxs-lookup"><span data-stu-id="937ff-198">You can get the repository for the sample at "[Manage Azure resources and resource groups with Ruby](https://github.com/Azure-Samples/resource-manager-ruby-resources-and-groups/tree/master/Hybrid)".</span></span>

1. <span data-ttu-id="937ff-199">Clone the repository.</span><span class="sxs-lookup"><span data-stu-id="937ff-199">Clone the repository.</span></span>

    ````Bash
    git clone https://github.com/Azure-Samples/resource-manager-ruby-resources-and-groups.git
    ````

2. <span data-ttu-id="937ff-200">Install the dependencies using bundle.</span><span class="sxs-lookup"><span data-stu-id="937ff-200">Install the dependencies using bundle.</span></span>

    ````Bash
    cd resource-manager-ruby-resources-and-groups\Hybrid\
    bundle install
    ````

3. <span data-ttu-id="937ff-201">Create an Azure Service Principal using PowerShell and retrieve the values needed.</span><span class="sxs-lookup"><span data-stu-id="937ff-201">Create an Azure Service Principal using PowerShell and retrieve the values needed.</span></span> 

  <span data-ttu-id="937ff-202">For instructions on creating a service principal, see [Use Azure PowerShell to create a service principal with a certificate](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals).</span><span class="sxs-lookup"><span data-stu-id="937ff-202">For instructions on creating a service principal, see [Use Azure PowerShell to create a service principal with a certificate](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals).</span></span>

  <span data-ttu-id="937ff-203">Values needed are:</span><span class="sxs-lookup"><span data-stu-id="937ff-203">Values needed are:</span></span>
  - <span data-ttu-id="937ff-204">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="937ff-204">Tenant ID</span></span>
  - <span data-ttu-id="937ff-205">Client ID</span><span class="sxs-lookup"><span data-stu-id="937ff-205">Client ID</span></span>
  - <span data-ttu-id="937ff-206">Client Secret</span><span class="sxs-lookup"><span data-stu-id="937ff-206">Client Secret</span></span>
  - <span data-ttu-id="937ff-207">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="937ff-207">Subscription ID</span></span>
  - <span data-ttu-id="937ff-208">Resource Manager Endpoint</span><span class="sxs-lookup"><span data-stu-id="937ff-208">Resource Manager Endpoint</span></span>

  <span data-ttu-id="937ff-209">Set the following environment variables using the information you retrieved from the Service Principal you created.</span><span class="sxs-lookup"><span data-stu-id="937ff-209">Set the following environment variables using the information you retrieved from the Service Principal you created.</span></span>

  - <span data-ttu-id="937ff-210">export AZURE_TENANT_ID={your tenant id}</span><span class="sxs-lookup"><span data-stu-id="937ff-210">export AZURE_TENANT_ID={your tenant id}</span></span>
  - <span data-ttu-id="937ff-211">export AZURE_CLIENT_ID={your client id}</span><span class="sxs-lookup"><span data-stu-id="937ff-211">export AZURE_CLIENT_ID={your client id}</span></span>
  - <span data-ttu-id="937ff-212">export AZURE_CLIENT_SECRET={your client secret}</span><span class="sxs-lookup"><span data-stu-id="937ff-212">export AZURE_CLIENT_SECRET={your client secret}</span></span>
  - <span data-ttu-id="937ff-213">export AZURE_SUBSCRIPTION_ID={your subscription id}</span><span class="sxs-lookup"><span data-stu-id="937ff-213">export AZURE_SUBSCRIPTION_ID={your subscription id}</span></span>
  - <span data-ttu-id="937ff-214">export ARM_ENDPOINT={your AzureStack Resource manager url}</span><span class="sxs-lookup"><span data-stu-id="937ff-214">export ARM_ENDPOINT={your AzureStack Resource manager url}</span></span>

  > [!Note]  
  > <span data-ttu-id="937ff-215">On Windows, use set instead of export.</span><span class="sxs-lookup"><span data-stu-id="937ff-215">On Windows, use set instead of export.</span></span>

4. <span data-ttu-id="937ff-216">Ensure the location variable is set to your AzureStack location.</span><span class="sxs-lookup"><span data-stu-id="937ff-216">Ensure the location variable is set to your AzureStack location.</span></span> <span data-ttu-id="937ff-217">For example LOCAL="local"</span><span class="sxs-lookup"><span data-stu-id="937ff-217">For example LOCAL="local"</span></span>

5. <span data-ttu-id="937ff-218">Add in the following line of code if you using Azure Stack or other private clouds to target the right active directory endpoints.</span><span class="sxs-lookup"><span data-stu-id="937ff-218">Add in the following line of code if you using Azure Stack or other private clouds to target the right active directory endpoints.</span></span>

  ````Ruby  
  active_directory_settings = get_active_directory_settings(ENV['ARM_ENDPOINT'])
  ````

6. <span data-ttu-id="937ff-219">Inside of the options variable, add the active directory settings and the base URL to work with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="937ff-219">Inside of the options variable, add the active directory settings and the base URL to work with Azure Stack.</span></span> 

  ````Ruby  
  options = {
    credentials: credentials,
    subscription_id: subscription_id,
    active_directory_settings: active_directory_settings,
    base_url: ENV['ARM_ENDPOINT']
  }
  ````

7. <span data-ttu-id="937ff-220">Create Profile client that targets the Azure Stack profile:</span><span class="sxs-lookup"><span data-stu-id="937ff-220">Create Profile client that targets the Azure Stack profile:</span></span>

  ````Ruby  
    client = Azure::Resources::Profiles::V2017_03_09::Mgmt::Client.new(options)
  ````

8. <span data-ttu-id="937ff-221">To authenticate the service principal with Azure Stack, the endpoints should be defined using **get_active_directory_settings()**.</span><span class="sxs-lookup"><span data-stu-id="937ff-221">To authenticate the service principal with Azure Stack, the endpoints should be defined using **get_active_directory_settings()**.</span></span> <span data-ttu-id="937ff-222">This method uses the **ARM_Endpoint** environment variable that you set when establishing your environmental variables.</span><span class="sxs-lookup"><span data-stu-id="937ff-222">This method uses the **ARM_Endpoint** environment variable that you set when establishing your environmental variables.</span></span>

  ````Ruby  
  def get_active_directory_settings(armEndpoint)
    settings = MsRestAzure::ActiveDirectoryServiceSettings.new
    response = Net::HTTP.get_response(URI("#{armEndpoint}/metadata/endpoints?api-version=1.0"))
    status_code = response.code
    response_content = response.body
    unless status_code == "200"
      error_model = JSON.load(response_content)
      fail MsRestAzure::AzureOperationError.new("Getting Azure Stack Metadata Endpoints", response, error_model)
    end
    result = JSON.load(response_content)
    settings.authentication_endpoint = result['authentication']['loginEndpoint'] unless result['authentication']['loginEndpoint'].nil?
    settings.token_audience = result['authentication']['audiences'][0] unless result['authentication']['audiences'][0].nil?
    settings
  end
  ````

9. <span data-ttu-id="937ff-223">Run the sample.</span><span class="sxs-lookup"><span data-stu-id="937ff-223">Run the sample.</span></span>

  ````Ruby
    bundle exec ruby example.rb
  ````

## 

## <a name="next-steps"></a><span data-ttu-id="937ff-224">Next steps</span><span class="sxs-lookup"><span data-stu-id="937ff-224">Next steps</span></span>

* [<span data-ttu-id="937ff-225">Install PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="937ff-225">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)
* [<span data-ttu-id="937ff-226">Configure the Azure Stack user's PowerShell environment</span><span class="sxs-lookup"><span data-stu-id="937ff-226">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
