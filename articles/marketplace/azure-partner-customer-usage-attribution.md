---
title: Azure partner and customer usage attribution
description: Overview of how to track customer usage for Azure Marketplace solutions
services: Azure, Marketplace, Compute, Storage, Networking, Blockchain, Security
documentationcenter: ''
author: ellacroi
manager: nunoc
editor: ''
ms.assetid: e8d228c8-f9e8-4a80-9319-7b94d41c43a6
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: article
ms.date: 07/26/2018
ms.author: ellacroi
ms.openlocfilehash: c3690c9be940a69bd2f8745493d4e2648bac6d9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870319"
---
# <a name="azure-partner-customer-usage-attribution"></a><span data-ttu-id="73039-103">Azure partner customer usage attribution</span><span class="sxs-lookup"><span data-stu-id="73039-103">Azure partner customer usage attribution</span></span>

<span data-ttu-id="73039-104">As a software partner for Azure, your solutions require Azure components or they need to be deployed directly on the Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="73039-104">As a software partner for Azure, your solutions require Azure components or they need to be deployed directly on the Azure infrastructure.</span></span> <span data-ttu-id="73039-105">Customers who deploy a partner solution and provision their own Azure resources can find it difficult to gain visibility into the status of the deployment, and get optics into the impact on Azure growth.</span><span class="sxs-lookup"><span data-stu-id="73039-105">Customers who deploy a partner solution and provision their own Azure resources can find it difficult to gain visibility into the status of the deployment, and get optics into the impact on Azure growth.</span></span> <span data-ttu-id="73039-106">When you add a higher level of visibility, you align with the Microsoft sales teams and gain credit for Microsoft partner programs.</span><span class="sxs-lookup"><span data-stu-id="73039-106">When you add a higher level of visibility, you align with the Microsoft sales teams and gain credit for Microsoft partner programs.</span></span>   

<span data-ttu-id="73039-107">Microsoft now offers a method to help partners better track Azure usage of customer deployments of their software on Azure.</span><span class="sxs-lookup"><span data-stu-id="73039-107">Microsoft now offers a method to help partners better track Azure usage of customer deployments of their software on Azure.</span></span> <span data-ttu-id="73039-108">The new method uses Azure Resource Manager to orchestrate the deployment of Azure services.</span><span class="sxs-lookup"><span data-stu-id="73039-108">The new method uses Azure Resource Manager to orchestrate the deployment of Azure services.</span></span>

<span data-ttu-id="73039-109">As a Microsoft partner, you can associate Azure usage with any Azure resources that you provision on a customer's behalf.</span><span class="sxs-lookup"><span data-stu-id="73039-109">As a Microsoft partner, you can associate Azure usage with any Azure resources that you provision on a customer's behalf.</span></span> <span data-ttu-id="73039-110">You can form the association via the Azure Marketplace, the Quickstart repository, private GitHub repositories, and one-on-one customer engagement.</span><span class="sxs-lookup"><span data-stu-id="73039-110">You can form the association via the Azure Marketplace, the Quickstart repository, private GitHub repositories, and one-on-one customer engagement.</span></span> <span data-ttu-id="73039-111">To enable tracking, two approaches are available:</span><span class="sxs-lookup"><span data-stu-id="73039-111">To enable tracking, two approaches are available:</span></span>

- <span data-ttu-id="73039-112">Azure Resource Manager templates: Resource Manager templates or solution templates to deploy the Azure services to run the partner's software.</span><span class="sxs-lookup"><span data-stu-id="73039-112">Azure Resource Manager templates: Resource Manager templates or solution templates to deploy the Azure services to run the partner's software.</span></span> <span data-ttu-id="73039-113">Partners can create a Resource Manager template to define the infrastructure and configuration of their Azure solution.</span><span class="sxs-lookup"><span data-stu-id="73039-113">Partners can create a Resource Manager template to define the infrastructure and configuration of their Azure solution.</span></span> <span data-ttu-id="73039-114">A Resource Manager template allows you and your customers to deploy your solution throughout its lifecycle.</span><span class="sxs-lookup"><span data-stu-id="73039-114">A Resource Manager template allows you and your customers to deploy your solution throughout its lifecycle.</span></span> <span data-ttu-id="73039-115">You can be confident that your resources are deployed in a consistent state.</span><span class="sxs-lookup"><span data-stu-id="73039-115">You can be confident that your resources are deployed in a consistent state.</span></span> 

- <span data-ttu-id="73039-116">Azure Resource Manager APIs: Partners can call the Resource Manager APIs directly to deploy a Resource Manager template or to generate the API calls to directly provision Azure services.</span><span class="sxs-lookup"><span data-stu-id="73039-116">Azure Resource Manager APIs: Partners can call the Resource Manager APIs directly to deploy a Resource Manager template or to generate the API calls to directly provision Azure services.</span></span> 

## <a name="use-resource-manager-templates"></a><span data-ttu-id="73039-117">Use Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="73039-117">Use Resource Manager templates</span></span>

<span data-ttu-id="73039-118">Many partner solutions are deployed on a customer’s subscription by using Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="73039-118">Many partner solutions are deployed on a customer’s subscription by using Resource Manager templates.</span></span> <span data-ttu-id="73039-119">If you have a Resource Manager template that's available in the Azure Marketplace, on GitHub, or as a Quickstart, the process to modify your template to enable the new tracking method should be straight forward.</span><span class="sxs-lookup"><span data-stu-id="73039-119">If you have a Resource Manager template that's available in the Azure Marketplace, on GitHub, or as a Quickstart, the process to modify your template to enable the new tracking method should be straight forward.</span></span> <span data-ttu-id="73039-120">If you aren't using an Azure Resource Manager template, here are a few links to help you better understand Resource Manager templates and how to create one:</span><span class="sxs-lookup"><span data-stu-id="73039-120">If you aren't using an Azure Resource Manager template, here are a few links to help you better understand Resource Manager templates and how to create one:</span></span> 

*   [<span data-ttu-id="73039-121">Create and deploy your first Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="73039-121">Create and deploy your first Resource Manager template</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-create-first-template)
*   [<span data-ttu-id="73039-122">Create a solution template for Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="73039-122">Create a solution template for Azure Marketplace</span></span>](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-solution-template-creation)

## <a name="add-a-guid-to-your-template"></a><span data-ttu-id="73039-123">Add a GUID to your template</span><span class="sxs-lookup"><span data-stu-id="73039-123">Add a GUID to your template</span></span>

<span data-ttu-id="73039-124">To add a globally unique identifier (GUID), you make a single modification to the main template file:</span><span class="sxs-lookup"><span data-stu-id="73039-124">To add a globally unique identifier (GUID), you make a single modification to the main template file:</span></span>

1. <span data-ttu-id="73039-125">Create a GUID (for example, eb7927c8-dd66-43e1-b0cf-c346a422063).</span><span class="sxs-lookup"><span data-stu-id="73039-125">Create a GUID (for example, eb7927c8-dd66-43e1-b0cf-c346a422063).</span></span>

1. <span data-ttu-id="73039-126">Open the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="73039-126">Open the Resource Manager template.</span></span>

1. <span data-ttu-id="73039-127">Add a new resource in the main template file.</span><span class="sxs-lookup"><span data-stu-id="73039-127">Add a new resource in the main template file.</span></span> <span data-ttu-id="73039-128">The resource needs to be in the **mainTemplate.json** or **azuredeploy.json** file only, and not in any nested or linked templates.</span><span class="sxs-lookup"><span data-stu-id="73039-128">The resource needs to be in the **mainTemplate.json** or **azuredeploy.json** file only, and not in any nested or linked templates.</span></span>

1. <span data-ttu-id="73039-129">Enter the GUID value after the **pid-** prefix (for example, pid-eb7927c8-dd66-43e1-b0cf-c346a422063).</span><span class="sxs-lookup"><span data-stu-id="73039-129">Enter the GUID value after the **pid-** prefix (for example, pid-eb7927c8-dd66-43e1-b0cf-c346a422063).</span></span>

1. <span data-ttu-id="73039-130">Check the template for any errors.</span><span class="sxs-lookup"><span data-stu-id="73039-130">Check the template for any errors.</span></span>

1. <span data-ttu-id="73039-131">Republish the template in the appropriate repositories.</span><span class="sxs-lookup"><span data-stu-id="73039-131">Republish the template in the appropriate repositories.</span></span>

### <a name="sample-template-code"></a><span data-ttu-id="73039-132">Sample template code</span><span class="sxs-lookup"><span data-stu-id="73039-132">Sample template code</span></span>

![Sample template code](media/marketplace-publishers-guide/tracking-sample-code-for-lu-1.PNG)

## <a name="use-the-resource-manager-apis"></a><span data-ttu-id="73039-134">Use the Resource Manager APIs</span><span class="sxs-lookup"><span data-stu-id="73039-134">Use the Resource Manager APIs</span></span>

<span data-ttu-id="73039-135">In some cases, you might prefer to make calls directly against the Resource Manager REST APIs to deploy Azure services.</span><span class="sxs-lookup"><span data-stu-id="73039-135">In some cases, you might prefer to make calls directly against the Resource Manager REST APIs to deploy Azure services.</span></span> <span data-ttu-id="73039-136">[Azure supports multiple SDKs](https://docs.microsoft.com/azure/#pivot=sdkstools) to enable these calls.</span><span class="sxs-lookup"><span data-stu-id="73039-136">[Azure supports multiple SDKs](https://docs.microsoft.com/azure/#pivot=sdkstools) to enable these calls.</span></span> <span data-ttu-id="73039-137">You can use one of the SDKs, or call the REST APIs directly to deploy resources.</span><span class="sxs-lookup"><span data-stu-id="73039-137">You can use one of the SDKs, or call the REST APIs directly to deploy resources.</span></span>

<span data-ttu-id="73039-138">If you're using a Resource Manager template, you should tag your solution by following the instructions described earlier.</span><span class="sxs-lookup"><span data-stu-id="73039-138">If you're using a Resource Manager template, you should tag your solution by following the instructions described earlier.</span></span> <span data-ttu-id="73039-139">If you aren't using a Resource Manager template and making direct API calls, you can still tag your deployment to associate usage of Azure resources.</span><span class="sxs-lookup"><span data-stu-id="73039-139">If you aren't using a Resource Manager template and making direct API calls, you can still tag your deployment to associate usage of Azure resources.</span></span> 

### <a name="tag-a-deployment-with-the-resource-manager-apis"></a><span data-ttu-id="73039-140">Tag a deployment with the Resource Manager APIs</span><span class="sxs-lookup"><span data-stu-id="73039-140">Tag a deployment with the Resource Manager APIs</span></span>

<span data-ttu-id="73039-141">For this tracking approach, when you design your API calls, include a GUID in the user agent header in the request.</span><span class="sxs-lookup"><span data-stu-id="73039-141">For this tracking approach, when you design your API calls, include a GUID in the user agent header in the request.</span></span> <span data-ttu-id="73039-142">Add the GUID for each offer or SKU.</span><span class="sxs-lookup"><span data-stu-id="73039-142">Add the GUID for each offer or SKU.</span></span> <span data-ttu-id="73039-143">Format the string with the **pid-** prefix and include the partner-generated GUID.</span><span class="sxs-lookup"><span data-stu-id="73039-143">Format the string with the **pid-** prefix and include the partner-generated GUID.</span></span> <span data-ttu-id="73039-144">Here's an example of the GUID format for insertion into the user agent:</span><span class="sxs-lookup"><span data-stu-id="73039-144">Here's an example of the GUID format for insertion into the user agent:</span></span> 

![Example GUID format](media/marketplace-publishers-guide/tracking-sample-guid-for-lu-2.PNG)

> [!Note]
> <span data-ttu-id="73039-146">The format of the string is important.</span><span class="sxs-lookup"><span data-stu-id="73039-146">The format of the string is important.</span></span> <span data-ttu-id="73039-147">If the **pid-** prefix isn't included, it's not possible to query the data.</span><span class="sxs-lookup"><span data-stu-id="73039-147">If the **pid-** prefix isn't included, it's not possible to query the data.</span></span> <span data-ttu-id="73039-148">Different SDKs track differently.</span><span class="sxs-lookup"><span data-stu-id="73039-148">Different SDKs track differently.</span></span> <span data-ttu-id="73039-149">To implement this method, review the support and tracking approach for your preferred Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="73039-149">To implement this method, review the support and tracking approach for your preferred Azure SDK.</span></span> 

### <a name="example-the-python-sdk"></a><span data-ttu-id="73039-150">Example: The Python SDK</span><span class="sxs-lookup"><span data-stu-id="73039-150">Example: The Python SDK</span></span>

<span data-ttu-id="73039-151">For Python, use the **config** attribute.</span><span class="sxs-lookup"><span data-stu-id="73039-151">For Python, use the **config** attribute.</span></span> <span data-ttu-id="73039-152">You can only add the attribute to a UserAgent.</span><span class="sxs-lookup"><span data-stu-id="73039-152">You can only add the attribute to a UserAgent.</span></span> <span data-ttu-id="73039-153">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="73039-153">Here's an example:</span></span>

![Add the attribute to a user agent](media/marketplace-publishers-guide/python-for-lu.PNG)

> [!Note]
> <span data-ttu-id="73039-155">Add the attribute for each client.</span><span class="sxs-lookup"><span data-stu-id="73039-155">Add the attribute for each client.</span></span> <span data-ttu-id="73039-156">There's no global static configuration.</span><span class="sxs-lookup"><span data-stu-id="73039-156">There's no global static configuration.</span></span> <span data-ttu-id="73039-157">You might tag a client factory to be sure every client is tracking.</span><span class="sxs-lookup"><span data-stu-id="73039-157">You might tag a client factory to be sure every client is tracking.</span></span> <span data-ttu-id="73039-158">For more information, see this [client factory sample on GitHub](https://github.com/Azure/azure-cli/blob/7402fb2c20be2cdbcaa7bdb2eeb72b7461fbcc30/src/azure-cli-core/azure/cli/core/commands/client_factory.py#L70-L79).</span><span class="sxs-lookup"><span data-stu-id="73039-158">For more information, see this [client factory sample on GitHub](https://github.com/Azure/azure-cli/blob/7402fb2c20be2cdbcaa7bdb2eeb72b7461fbcc30/src/azure-cli-core/azure/cli/core/commands/client_factory.py#L70-L79).</span></span>

#### <a name="tag-a-deployment-by-using-the-azure-powershell"></a><span data-ttu-id="73039-159">Tag a deployment by using the Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="73039-159">Tag a deployment by using the Azure PowerShell</span></span>

<span data-ttu-id="73039-160">If you deploy resources via Azure PowerShell, append your GUID by using the following method:</span><span class="sxs-lookup"><span data-stu-id="73039-160">If you deploy resources via Azure PowerShell, append your GUID by using the following method:</span></span>

```
[Microsoft.Azure.Common.Authentication.AzureSession]::ClientFactory.AddUserAgent("pid-eb7927c8-dd66-43e1-b0cf-c346a422063")
```

#### <a name="tag-a-deployment-by-using-the-azure-cli"></a><span data-ttu-id="73039-161">Tag a deployment by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="73039-161">Tag a deployment by using the Azure CLI</span></span>

<span data-ttu-id="73039-162">When you use the Azure CLI to append your GUID, set the **AZURE_HTTP_USER_AGENT** environment variable.</span><span class="sxs-lookup"><span data-stu-id="73039-162">When you use the Azure CLI to append your GUID, set the **AZURE_HTTP_USER_AGENT** environment variable.</span></span> <span data-ttu-id="73039-163">You can set this variable within the scope of a script.</span><span class="sxs-lookup"><span data-stu-id="73039-163">You can set this variable within the scope of a script.</span></span> <span data-ttu-id="73039-164">You can also set the variable globally for shell scope:</span><span class="sxs-lookup"><span data-stu-id="73039-164">You can also set the variable globally for shell scope:</span></span>

```
export AZURE_HTTP_USER_AGENT='pid-eb7927c8-dd66-43e1-b0cf-c346a422063'
```

## <a name="register-guids-and-offers"></a><span data-ttu-id="73039-165">Register GUIDs and offers</span><span class="sxs-lookup"><span data-stu-id="73039-165">Register GUIDs and offers</span></span>

<span data-ttu-id="73039-166">To include a GUID in our tracking, the GUID must be registered.</span><span class="sxs-lookup"><span data-stu-id="73039-166">To include a GUID in our tracking, the GUID must be registered.</span></span>  

<span data-ttu-id="73039-167">All registrations for template GUIDs are done via the Azure Marketplace Cloud Partner Portal (CPP).</span><span class="sxs-lookup"><span data-stu-id="73039-167">All registrations for template GUIDs are done via the Azure Marketplace Cloud Partner Portal (CPP).</span></span> 

<span data-ttu-id="73039-168">After you add the GUID to your template or in the user agent, and register the GUID in the CPP, all deployments are tracked.</span><span class="sxs-lookup"><span data-stu-id="73039-168">After you add the GUID to your template or in the user agent, and register the GUID in the CPP, all deployments are tracked.</span></span> 

1. <span data-ttu-id="73039-169">Apply to [Azure Marketplace](http://aka.ms/listonazuremarketplace) and get access to the CPP.</span><span class="sxs-lookup"><span data-stu-id="73039-169">Apply to [Azure Marketplace](http://aka.ms/listonazuremarketplace) and get access to the CPP.</span></span>

   * <span data-ttu-id="73039-170">Partners are required to [have a profile in CPP](https://docs.microsoft.com/azure/marketplace/become-publisher).</span><span class="sxs-lookup"><span data-stu-id="73039-170">Partners are required to [have a profile in CPP](https://docs.microsoft.com/azure/marketplace/become-publisher).</span></span> <span data-ttu-id="73039-171">You're encouraged to list the offer in Azure Marketplace or AppSource.</span><span class="sxs-lookup"><span data-stu-id="73039-171">You're encouraged to list the offer in Azure Marketplace or AppSource.</span></span>
   * <span data-ttu-id="73039-172">Partners can register multiple GUIDs.</span><span class="sxs-lookup"><span data-stu-id="73039-172">Partners can register multiple GUIDs.</span></span>
   * <span data-ttu-id="73039-173">Partners can register a GUID for the non-Marketplace solution templates and offers.</span><span class="sxs-lookup"><span data-stu-id="73039-173">Partners can register a GUID for the non-Marketplace solution templates and offers.</span></span>
 
1. <span data-ttu-id="73039-174">Sign in to the [Cloud Partner Portal](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="73039-174">Sign in to the [Cloud Partner Portal](https://cloudpartner.azure.com/).</span></span>

1. <span data-ttu-id="73039-175">In the upper-right corner, select your account icon, and then select **Publisher profile**.</span><span class="sxs-lookup"><span data-stu-id="73039-175">In the upper-right corner, select your account icon, and then select **Publisher profile**.</span></span>

   ![Select Publisher profile](media/marketplace-publishers-guide/guid-image-for-lu.png)

1. <span data-ttu-id="73039-177">On the **Profile page**, select **Add Tracking GUID.**</span><span class="sxs-lookup"><span data-stu-id="73039-177">On the **Profile page**, select **Add Tracking GUID.**</span></span>

   ![Select Add Tracking GUID](media/marketplace-publishers-guide/guid-how-to-add-tracking.png)

1. <span data-ttu-id="73039-179">In the **Tracking GUID** box, enter your tracking GUID.</span><span class="sxs-lookup"><span data-stu-id="73039-179">In the **Tracking GUID** box, enter your tracking GUID.</span></span> <span data-ttu-id="73039-180">Enter just the GUID without the **pid-** prefix.</span><span class="sxs-lookup"><span data-stu-id="73039-180">Enter just the GUID without the **pid-** prefix.</span></span> <span data-ttu-id="73039-181">In the **Custom Description** box, enter your offer name or description.</span><span class="sxs-lookup"><span data-stu-id="73039-181">In the **Custom Description** box, enter your offer name or description.</span></span>

   ![Profile page](media/marketplace-publishers-guide/guid-dev-center-login.png)
   
   ![Enter the GUID and offer description](media/marketplace-publishers-guide/guid-dev-center-example.png)

1. <span data-ttu-id="73039-184">To register more than one GUID, select **Add Tracking GUID** again.</span><span class="sxs-lookup"><span data-stu-id="73039-184">To register more than one GUID, select **Add Tracking GUID** again.</span></span> <span data-ttu-id="73039-185">Additional boxes appear on the page.</span><span class="sxs-lookup"><span data-stu-id="73039-185">Additional boxes appear on the page.</span></span>

   ![Select Add Tracking GUID again](media/marketplace-publishers-guide/guid-dev-center-example-add.png)
   
   ![Enter another GUID and offer description](media/marketplace-publishers-guide/guid-dev-center-example-description.png)

1. <span data-ttu-id="73039-188">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="73039-188">Select **Save**.</span></span>

   ![Select Save](media/marketplace-publishers-guide/guid-dev-center-save.png)

<span data-ttu-id="73039-190">After you add the GUID to your template or in the user agent, and register the GUID in the CPP, all deployments are tracked.</span><span class="sxs-lookup"><span data-stu-id="73039-190">After you add the GUID to your template or in the user agent, and register the GUID in the CPP, all deployments are tracked.</span></span> 

## <a name="verify-the-guid-deployment"></a><span data-ttu-id="73039-191">Verify the GUID deployment</span><span class="sxs-lookup"><span data-stu-id="73039-191">Verify the GUID deployment</span></span> 

<span data-ttu-id="73039-192">After you modify your template and run a test deployment, use the following PowerShell script to retrieve the resources that you deployed and tagged.</span><span class="sxs-lookup"><span data-stu-id="73039-192">After you modify your template and run a test deployment, use the following PowerShell script to retrieve the resources that you deployed and tagged.</span></span> 

<span data-ttu-id="73039-193">You can use the script to verify that the GUID is successfully added to your Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="73039-193">You can use the script to verify that the GUID is successfully added to your Resource Manager template.</span></span> <span data-ttu-id="73039-194">The script doesn't apply to Resource Manager API deployment.</span><span class="sxs-lookup"><span data-stu-id="73039-194">The script doesn't apply to Resource Manager API deployment.</span></span>

<span data-ttu-id="73039-195">Sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="73039-195">Sign in to Azure.</span></span> <span data-ttu-id="73039-196">Select the subscription with the deployment that you want to verify before you run the script.</span><span class="sxs-lookup"><span data-stu-id="73039-196">Select the subscription with the deployment that you want to verify before you run the script.</span></span> <span data-ttu-id="73039-197">Run the script within the subscription context of the deployment.</span><span class="sxs-lookup"><span data-stu-id="73039-197">Run the script within the subscription context of the deployment.</span></span>

<span data-ttu-id="73039-198">The **GUID** and **resourceGroup** name of the deployment are required parameters.</span><span class="sxs-lookup"><span data-stu-id="73039-198">The **GUID** and **resourceGroup** name of the deployment are required parameters.</span></span>

<span data-ttu-id="73039-199">You can get [the original script](https://gist.github.com/bmoore-msft/ae6b8226311014d6e7177c5127c7eba1#file-verify-deploymentguid-ps1) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="73039-199">You can get [the original script](https://gist.github.com/bmoore-msft/ae6b8226311014d6e7177c5127c7eba1#file-verify-deploymentguid-ps1) on GitHub.</span></span>

```
Param(
    [GUID][Parameter(Mandatory=$true)]$guid,
    [string][Parameter(Mandatory=$true)]$resourceGroupName'
)

# Get the correlationId of the pid deployment

$correlationId = (Get-AzureRmResourceGroupDeployment -ResourceGroupName 
$resourceGroupName -Name "pid-$guid").correlationId

# Find all deployments with that correlationId

$deployments = Get-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName | Where-Object{$_.correlationId -eq $correlationId}

# Find all deploymentOperations in a deployment by name
# PowerShell doesn't surface outputResources on the deployment
# or correlationId on the deploymentOperation

foreach ($deployment in $deployments){

# Get deploymentOperations by deploymentName
# then the resourceId for any create operation

($deployment | Get-AzureRmResourceGroupDeploymentOperation | Where-Object{$_.properties.provisioningOperation -eq "Create" -and $_.properties.targetResource.resourceType -ne "Microsoft.Resources/deployments"}).properties.targetResource.id

}
```

## <a name="create-guids"></a><span data-ttu-id="73039-200">Create GUIDs</span><span class="sxs-lookup"><span data-stu-id="73039-200">Create GUIDs</span></span>

<span data-ttu-id="73039-201">A GUID is a unique reference number that has 32 hexadecimal digits.</span><span class="sxs-lookup"><span data-stu-id="73039-201">A GUID is a unique reference number that has 32 hexadecimal digits.</span></span> <span data-ttu-id="73039-202">To create GUIDs for tracking, you should use a GUID generator.</span><span class="sxs-lookup"><span data-stu-id="73039-202">To create GUIDs for tracking, you should use a GUID generator.</span></span> <span data-ttu-id="73039-203">There are multiple [online GUID generators](https://www.bing.com/search?q=guid%20generator&qs=n&form=QBRE&sp=-1&ghc=2&pq=guid%20g&sc=8-6&sk=&cvid=0BAFAFCD70B34E4296BB97FBFA3E1B4E) that you can use.</span><span class="sxs-lookup"><span data-stu-id="73039-203">There are multiple [online GUID generators](https://www.bing.com/search?q=guid%20generator&qs=n&form=QBRE&sp=-1&ghc=2&pq=guid%20g&sc=8-6&sk=&cvid=0BAFAFCD70B34E4296BB97FBFA3E1B4E) that you can use.</span></span>

<span data-ttu-id="73039-204">Create a unique GUID for every offer and distribution channel.</span><span class="sxs-lookup"><span data-stu-id="73039-204">Create a unique GUID for every offer and distribution channel.</span></span> <span data-ttu-id="73039-205">If you deploy two solutions by using a template and each one is available in the Azure Marketplace and on GitHub, you need to create four GUIDS:</span><span class="sxs-lookup"><span data-stu-id="73039-205">If you deploy two solutions by using a template and each one is available in the Azure Marketplace and on GitHub, you need to create four GUIDS:</span></span>

*   <span data-ttu-id="73039-206">Offer A in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="73039-206">Offer A in Azure Marketplace</span></span> 
*   <span data-ttu-id="73039-207">Offer A on GitHub</span><span class="sxs-lookup"><span data-stu-id="73039-207">Offer A on GitHub</span></span>
*   <span data-ttu-id="73039-208">Offer B in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="73039-208">Offer B in Azure Marketplace</span></span> 
*   <span data-ttu-id="73039-209">Offer B on GitHub</span><span class="sxs-lookup"><span data-stu-id="73039-209">Offer B on GitHub</span></span>

<span data-ttu-id="73039-210">Reporting is done by the partner value (Microsoft Partner ID) and the GUID.</span><span class="sxs-lookup"><span data-stu-id="73039-210">Reporting is done by the partner value (Microsoft Partner ID) and the GUID.</span></span> 

<span data-ttu-id="73039-211">You can also track GUIDs at a more granular level like the SKU, where SKUs are variants of an offer.</span><span class="sxs-lookup"><span data-stu-id="73039-211">You can also track GUIDs at a more granular level like the SKU, where SKUs are variants of an offer.</span></span>

## <a name="notify-your-customers"></a><span data-ttu-id="73039-212">Notify your customers</span><span class="sxs-lookup"><span data-stu-id="73039-212">Notify your customers</span></span>

<span data-ttu-id="73039-213">Partners should inform their customers about deployments that use Resource Manager GUID tracking.</span><span class="sxs-lookup"><span data-stu-id="73039-213">Partners should inform their customers about deployments that use Resource Manager GUID tracking.</span></span> <span data-ttu-id="73039-214">Microsoft reports the Azure usage that's associated with these deployments to the partner.</span><span class="sxs-lookup"><span data-stu-id="73039-214">Microsoft reports the Azure usage that's associated with these deployments to the partner.</span></span> <span data-ttu-id="73039-215">The following examples include content that you can use to notify your customers about these deployments.</span><span class="sxs-lookup"><span data-stu-id="73039-215">The following examples include content that you can use to notify your customers about these deployments.</span></span> <span data-ttu-id="73039-216">In the examples, replace \<PARTNER> with your company name.</span><span class="sxs-lookup"><span data-stu-id="73039-216">In the examples, replace \<PARTNER> with your company name.</span></span> <span data-ttu-id="73039-217">Partners should make sure the notification aligns with their data privacy and collection policies, including options for customers to be excluded from tracking.</span><span class="sxs-lookup"><span data-stu-id="73039-217">Partners should make sure the notification aligns with their data privacy and collection policies, including options for customers to be excluded from tracking.</span></span> 

### <a name="notification-for-resource-manager-template-deployments"></a><span data-ttu-id="73039-218">Notification for Resource Manager template deployments</span><span class="sxs-lookup"><span data-stu-id="73039-218">Notification for Resource Manager template deployments</span></span>

<span data-ttu-id="73039-219">When you deploy this template, Microsoft is able to identify the installation of \<PARTNER> software with the Azure resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="73039-219">When you deploy this template, Microsoft is able to identify the installation of \<PARTNER> software with the Azure resources that are deployed.</span></span> <span data-ttu-id="73039-220">Microsoft is able to correlate the Azure resources that are used to support the software.</span><span class="sxs-lookup"><span data-stu-id="73039-220">Microsoft is able to correlate the Azure resources that are used to support the software.</span></span> <span data-ttu-id="73039-221">Microsoft collects this information to provide the best experiences with their products and to operate their business.</span><span class="sxs-lookup"><span data-stu-id="73039-221">Microsoft collects this information to provide the best experiences with their products and to operate their business.</span></span> <span data-ttu-id="73039-222">The data is collected and governed by Microsoft's privacy policies, which can be found at https://www.microsoft.com/trustcenter.</span><span class="sxs-lookup"><span data-stu-id="73039-222">The data is collected and governed by Microsoft's privacy policies, which can be found at https://www.microsoft.com/trustcenter.</span></span> 

### <a name="notification-for-sdk-or-api-deployments"></a><span data-ttu-id="73039-223">Notification for SDK or API deployments</span><span class="sxs-lookup"><span data-stu-id="73039-223">Notification for SDK or API deployments</span></span>

<span data-ttu-id="73039-224">When you deploy \<PARTNER> software, Microsoft is able to identify the installation of \<PARTNER> software with the Azure resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="73039-224">When you deploy \<PARTNER> software, Microsoft is able to identify the installation of \<PARTNER> software with the Azure resources that are deployed.</span></span> <span data-ttu-id="73039-225">Microsoft is able to correlate the Azure resources that are used to support the software.</span><span class="sxs-lookup"><span data-stu-id="73039-225">Microsoft is able to correlate the Azure resources that are used to support the software.</span></span> <span data-ttu-id="73039-226">Microsoft collects this information to provide the best experiences with their products and to operate their business.</span><span class="sxs-lookup"><span data-stu-id="73039-226">Microsoft collects this information to provide the best experiences with their products and to operate their business.</span></span> <span data-ttu-id="73039-227">The data is collected and governed by Microsoft's privacy policies, which can be found at https://www.microsoft.com/trustcenter.</span><span class="sxs-lookup"><span data-stu-id="73039-227">The data is collected and governed by Microsoft's privacy policies, which can be found at https://www.microsoft.com/trustcenter.</span></span>

## <a name="get-support"></a><span data-ttu-id="73039-228">Get support</span><span class="sxs-lookup"><span data-stu-id="73039-228">Get support</span></span>

<span data-ttu-id="73039-229">If you need assistance, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="73039-229">If you need assistance, follow these steps.</span></span>

1. <span data-ttu-id="73039-230">Go to the [support page](https://go.microsoft.com/fwlink/?linkid=844975).</span><span class="sxs-lookup"><span data-stu-id="73039-230">Go to the [support page](https://go.microsoft.com/fwlink/?linkid=844975).</span></span> 

1. <span data-ttu-id="73039-231">Under **Problem type**, select **Marketplace Onboarding**.</span><span class="sxs-lookup"><span data-stu-id="73039-231">Under **Problem type**, select **Marketplace Onboarding**.</span></span>

1. <span data-ttu-id="73039-232">Choose the **Category** for your issue:</span><span class="sxs-lookup"><span data-stu-id="73039-232">Choose the **Category** for your issue:</span></span>

   - <span data-ttu-id="73039-233">For usage association issues, select **Other**.</span><span class="sxs-lookup"><span data-stu-id="73039-233">For usage association issues, select **Other**.</span></span>
   - <span data-ttu-id="73039-234">For access issues with the Azure Marketplace CPP, select **Access Problem**.</span><span class="sxs-lookup"><span data-stu-id="73039-234">For access issues with the Azure Marketplace CPP, select **Access Problem**.</span></span>
   
    ![Choose the issue category](media/marketplace-publishers-guide/lu-article-incident.png)

1. <span data-ttu-id="73039-236">Select **Start Request**.</span><span class="sxs-lookup"><span data-stu-id="73039-236">Select **Start Request**.</span></span>

1. <span data-ttu-id="73039-237">On the next page, enter the required values.</span><span class="sxs-lookup"><span data-stu-id="73039-237">On the next page, enter the required values.</span></span> <span data-ttu-id="73039-238">Select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="73039-238">Select **Continue**.</span></span>

1. <span data-ttu-id="73039-239">On the next page, enter the required values.</span><span class="sxs-lookup"><span data-stu-id="73039-239">On the next page, enter the required values.</span></span>

   > [!Important] 
   > <span data-ttu-id="73039-240">In the **Incident title** box, enter **ISV Usage Tracking**.</span><span class="sxs-lookup"><span data-stu-id="73039-240">In the **Incident title** box, enter **ISV Usage Tracking**.</span></span> <span data-ttu-id="73039-241">Describe your issue in detail.</span><span class="sxs-lookup"><span data-stu-id="73039-241">Describe your issue in detail.</span></span>
   
   ![Enter ISV Usage Tracking for the incident title](media/marketplace-publishers-guide/guid-dev-center-help-hd%201.png)

1. <span data-ttu-id="73039-243">Complete the form, and then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="73039-243">Complete the form, and then select **Submit**.</span></span>

## <a name="faq"></a><span data-ttu-id="73039-244">FAQ</span><span class="sxs-lookup"><span data-stu-id="73039-244">FAQ</span></span>

<span data-ttu-id="73039-245">**What's the benefit of adding the GUID to the template?**</span><span class="sxs-lookup"><span data-stu-id="73039-245">**What's the benefit of adding the GUID to the template?**</span></span>

<span data-ttu-id="73039-246">Microsoft provides partners with a view of customer deployments of their templates and insights on their influenced usage.</span><span class="sxs-lookup"><span data-stu-id="73039-246">Microsoft provides partners with a view of customer deployments of their templates and insights on their influenced usage.</span></span> <span data-ttu-id="73039-247">Both Microsoft and the partner can use this information to drive closer engagement between sales teams.</span><span class="sxs-lookup"><span data-stu-id="73039-247">Both Microsoft and the partner can use this information to drive closer engagement between sales teams.</span></span> <span data-ttu-id="73039-248">Both Microsoft and the partner can use the data to get a more consistent view of an individual partner's impact on Azure growth.</span><span class="sxs-lookup"><span data-stu-id="73039-248">Both Microsoft and the partner can use the data to get a more consistent view of an individual partner's impact on Azure growth.</span></span> 

<span data-ttu-id="73039-249">**Who can add a GUID to a template?**</span><span class="sxs-lookup"><span data-stu-id="73039-249">**Who can add a GUID to a template?**</span></span>

<span data-ttu-id="73039-250">The tracking resource is intended to connect the partner's solution to the customer's Azure usage.</span><span class="sxs-lookup"><span data-stu-id="73039-250">The tracking resource is intended to connect the partner's solution to the customer's Azure usage.</span></span> <span data-ttu-id="73039-251">The usage data is tied to a partner's Microsoft Partner Network identity (MPN ID).</span><span class="sxs-lookup"><span data-stu-id="73039-251">The usage data is tied to a partner's Microsoft Partner Network identity (MPN ID).</span></span> <span data-ttu-id="73039-252">Reporting is available to partners in the CPP.</span><span class="sxs-lookup"><span data-stu-id="73039-252">Reporting is available to partners in the CPP.</span></span>

<span data-ttu-id="73039-253">**After a GUID is added, can it be changed?**</span><span class="sxs-lookup"><span data-stu-id="73039-253">**After a GUID is added, can it be changed?**</span></span>
 
<span data-ttu-id="73039-254">Yes, a customer or implementation partner may customize the template and can change or remove the GUID.</span><span class="sxs-lookup"><span data-stu-id="73039-254">Yes, a customer or implementation partner may customize the template and can change or remove the GUID.</span></span> <span data-ttu-id="73039-255">We suggest that partners proactively describe the role of the resource and GUID to their customers and partners to prevent removal or edits to the tracking GUID.</span><span class="sxs-lookup"><span data-stu-id="73039-255">We suggest that partners proactively describe the role of the resource and GUID to their customers and partners to prevent removal or edits to the tracking GUID.</span></span> <span data-ttu-id="73039-256">Changing the GUID affects only new, not existing, deployments, and resources.</span><span class="sxs-lookup"><span data-stu-id="73039-256">Changing the GUID affects only new, not existing, deployments, and resources.</span></span>

<span data-ttu-id="73039-257">**When will reporting be available?**</span><span class="sxs-lookup"><span data-stu-id="73039-257">**When will reporting be available?**</span></span>

<span data-ttu-id="73039-258">A beta version of reporting should be available soon.</span><span class="sxs-lookup"><span data-stu-id="73039-258">A beta version of reporting should be available soon.</span></span> <span data-ttu-id="73039-259">Reporting will be integrated into the CPP.</span><span class="sxs-lookup"><span data-stu-id="73039-259">Reporting will be integrated into the CPP.</span></span>

<span data-ttu-id="73039-260">**Can I track templates deployed from a non-Microsoft repository like GitHub?**</span><span class="sxs-lookup"><span data-stu-id="73039-260">**Can I track templates deployed from a non-Microsoft repository like GitHub?**</span></span>

<span data-ttu-id="73039-261">Yes, as long as the GUID is present when the template is deployed, usage is tracked.</span><span class="sxs-lookup"><span data-stu-id="73039-261">Yes, as long as the GUID is present when the template is deployed, usage is tracked.</span></span> <span data-ttu-id="73039-262">Partners are required to have a profile in the CPP to register related templates that are published outside of the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="73039-262">Partners are required to have a profile in the CPP to register related templates that are published outside of the Azure Marketplace.</span></span> 

<span data-ttu-id="73039-263">**Is there a difference if the template is deployed from Azure Marketplace versus other repositories like GitHub?**</span><span class="sxs-lookup"><span data-stu-id="73039-263">**Is there a difference if the template is deployed from Azure Marketplace versus other repositories like GitHub?**</span></span>

<span data-ttu-id="73039-264">Yes, partners who publish offers in the Azure Marketplace might receive more detailed data on deployments from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="73039-264">Yes, partners who publish offers in the Azure Marketplace might receive more detailed data on deployments from the Azure Marketplace.</span></span> <span data-ttu-id="73039-265">Partners benefit from exposing their offer to customers on the Azure Marketplace portal and in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="73039-265">Partners benefit from exposing their offer to customers on the Azure Marketplace portal and in the Azure portal.</span></span> <span data-ttu-id="73039-266">Offers in the Azure Marketplace also generate leads for the partner.</span><span class="sxs-lookup"><span data-stu-id="73039-266">Offers in the Azure Marketplace also generate leads for the partner.</span></span>

<span data-ttu-id="73039-267">**What if I create a custom template for an individual customer engagement?**</span><span class="sxs-lookup"><span data-stu-id="73039-267">**What if I create a custom template for an individual customer engagement?**</span></span>

<span data-ttu-id="73039-268">You're still welcome to add the GUID to the template.</span><span class="sxs-lookup"><span data-stu-id="73039-268">You're still welcome to add the GUID to the template.</span></span> <span data-ttu-id="73039-269">If you use an existing registered GUID, it's included in the reporting.</span><span class="sxs-lookup"><span data-stu-id="73039-269">If you use an existing registered GUID, it's included in the reporting.</span></span> <span data-ttu-id="73039-270">If you create a new GUID, you need to register the new GUID to have it included in the tracking.</span><span class="sxs-lookup"><span data-stu-id="73039-270">If you create a new GUID, you need to register the new GUID to have it included in the tracking.</span></span>

<span data-ttu-id="73039-271">**Does the customer receive reporting as well?**</span><span class="sxs-lookup"><span data-stu-id="73039-271">**Does the customer receive reporting as well?**</span></span>

<span data-ttu-id="73039-272">Customers can track their usage of individual resources or customer-defined resource groups within the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="73039-272">Customers can track their usage of individual resources or customer-defined resource groups within the Azure portal.</span></span>   

<span data-ttu-id="73039-273">**Is this tracking methodology similar to the Digital Partner of Record (DPOR)?**</span><span class="sxs-lookup"><span data-stu-id="73039-273">**Is this tracking methodology similar to the Digital Partner of Record (DPOR)?**</span></span>

<span data-ttu-id="73039-274">This new method of connecting the deployment and usage to a partner's solution provides a mechanism to link a partner solution to Azure usage.</span><span class="sxs-lookup"><span data-stu-id="73039-274">This new method of connecting the deployment and usage to a partner's solution provides a mechanism to link a partner solution to Azure usage.</span></span> <span data-ttu-id="73039-275">DPOR is intended to associate a consulting (Systems Integrator) or management (Managed Service Provider) partner with a customer's Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="73039-275">DPOR is intended to associate a consulting (Systems Integrator) or management (Managed Service Provider) partner with a customer's Azure subscription.</span></span>   
