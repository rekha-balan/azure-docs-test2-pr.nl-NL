---
title: Create an Azure Application Gateway - templates | Microsoft Docs
description: This page provides instructions to create an Azure application gateway by using the Azure Resource Manager template
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8192ee25-d9f0-4b32-a45e-1d74629c54e5
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: baaf6a579a16162bec4b8ac95ec8e0d90119a101
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662224"
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="91d2e-103">Create an application gateway by using the Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="91d2e-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager template](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

<span data-ttu-id="91d2e-109">Azure Application Gateway is a layer-7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="91d2e-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="91d2e-110">It provides failover, performance-routing HTTP requests between different servers, whether they are in the cloud or on-premises.</span><span class="sxs-lookup"><span data-stu-id="91d2e-110">It provides failover, performance-routing HTTP requests between different servers, whether they are in the cloud or on-premises.</span></span>
<span data-ttu-id="91d2e-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span><span class="sxs-lookup"><span data-stu-id="91d2e-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span>

<span data-ttu-id="91d2e-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="91d2e-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="91d2e-113">You learn how to download and modify an existing Azure Resource Manager template from GitHub and deploy the template from GitHub, PowerShell, and the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="91d2e-113">You learn how to download and modify an existing Azure Resource Manager template from GitHub and deploy the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="91d2e-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span><span class="sxs-lookup"><span data-stu-id="91d2e-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="91d2e-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="91d2e-115">Scenario</span></span>

<span data-ttu-id="91d2e-116">In this scenario you will:</span><span class="sxs-lookup"><span data-stu-id="91d2e-116">In this scenario you will:</span></span>

* <span data-ttu-id="91d2e-117">Create an application gateway with web application firewall.</span><span class="sxs-lookup"><span data-stu-id="91d2e-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="91d2e-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="91d2e-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="91d2e-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span><span class="sxs-lookup"><span data-stu-id="91d2e-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="91d2e-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span><span class="sxs-lookup"><span data-stu-id="91d2e-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="91d2e-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="91d2e-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> Those settings are the parameters for this template. To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.

![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="91d2e-125">Download and understand the Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="91d2e-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="91d2e-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span><span class="sxs-lookup"><span data-stu-id="91d2e-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="91d2e-127">To do so, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="91d2e-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="91d2e-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="91d2e-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="91d2e-129">Click **azuredeploy.json**, and then click **RAW**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="91d2e-130">Save the file to a local folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="91d2e-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="91d2e-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span><span class="sxs-lookup"><span data-stu-id="91d2e-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="91d2e-132">Open the file that you saved and look at the contents under **parameters** in line</span><span class="sxs-lookup"><span data-stu-id="91d2e-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="91d2e-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span><span class="sxs-lookup"><span data-stu-id="91d2e-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="91d2e-134">Parameter</span><span class="sxs-lookup"><span data-stu-id="91d2e-134">Parameter</span></span> | <span data-ttu-id="91d2e-135">Description</span><span class="sxs-lookup"><span data-stu-id="91d2e-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="91d2e-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="91d2e-136">**subnetPrefix**</span></span> |<span data-ttu-id="91d2e-137">CIDR block for the application gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="91d2e-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="91d2e-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="91d2e-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="91d2e-139">Size of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="91d2e-139">Size of the application gateway.</span></span>  <span data-ttu-id="91d2e-140">WAF only allows medium and large.</span><span class="sxs-lookup"><span data-stu-id="91d2e-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="91d2e-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="91d2e-141">**backendIpaddress1**</span></span> |<span data-ttu-id="91d2e-142">IP address of the first web server.</span><span class="sxs-lookup"><span data-stu-id="91d2e-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="91d2e-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="91d2e-143">**backendIpaddress2**</span></span> |<span data-ttu-id="91d2e-144">IP address of the second web server.</span><span class="sxs-lookup"><span data-stu-id="91d2e-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="91d2e-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="91d2e-145">**wafEnabled**</span></span> | <span data-ttu-id="91d2e-146">Setting to determine if WAF is enabled.</span><span class="sxs-lookup"><span data-stu-id="91d2e-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="91d2e-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="91d2e-147">**wafMode**</span></span> | <span data-ttu-id="91d2e-148">Mode of the web application firewall.</span><span class="sxs-lookup"><span data-stu-id="91d2e-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="91d2e-149">Available options are **prevention** or **detection**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="91d2e-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="91d2e-150">**wafRuleSetType**</span></span> | <span data-ttu-id="91d2e-151">Ruleset type for WAF.</span><span class="sxs-lookup"><span data-stu-id="91d2e-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="91d2e-152">Currently OWASP is the only supported option.</span><span class="sxs-lookup"><span data-stu-id="91d2e-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="91d2e-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="91d2e-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="91d2e-154">Ruleset version.</span><span class="sxs-lookup"><span data-stu-id="91d2e-154">Ruleset version.</span></span> <span data-ttu-id="91d2e-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span><span class="sxs-lookup"><span data-stu-id="91d2e-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |


  > [!IMPORTANT]
  > Azure Resource Manager templates maintained in GitHub can change over time. Make sure that you check the template before using it.

1. <span data-ttu-id="91d2e-158">Check the content under **resources** and notice the following properties:</span><span class="sxs-lookup"><span data-stu-id="91d2e-158">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="91d2e-159">**type**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-159">**type**.</span></span> <span data-ttu-id="91d2e-160">Type of resource being created by the template.</span><span class="sxs-lookup"><span data-stu-id="91d2e-160">Type of resource being created by the template.</span></span> <span data-ttu-id="91d2e-161">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span><span class="sxs-lookup"><span data-stu-id="91d2e-161">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="91d2e-162">**name**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-162">**name**.</span></span> <span data-ttu-id="91d2e-163">Name for the resource.</span><span class="sxs-lookup"><span data-stu-id="91d2e-163">Name for the resource.</span></span> <span data-ttu-id="91d2e-164">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span><span class="sxs-lookup"><span data-stu-id="91d2e-164">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="91d2e-165">**properties**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-165">**properties**.</span></span> <span data-ttu-id="91d2e-166">List of properties for the resource.</span><span class="sxs-lookup"><span data-stu-id="91d2e-166">List of properties for the resource.</span></span> <span data-ttu-id="91d2e-167">This template uses the virtual network and public IP address during application gateway creation.</span><span class="sxs-lookup"><span data-stu-id="91d2e-167">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > For more information on templates visit: [Resource Manager templates reference](/templates/)

1. <span data-ttu-id="91d2e-169">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="91d2e-169">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="91d2e-170">Click **azuredeploy-parameters.json**, and then click **RAW**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-170">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="91d2e-171">Save the file to a local folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="91d2e-171">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="91d2e-172">Open the file that you saved and edit the values for the parameters.</span><span class="sxs-lookup"><span data-stu-id="91d2e-172">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="91d2e-173">Use the following values to deploy the application gateway described in our scenario.</span><span class="sxs-lookup"><span data-stu-id="91d2e-173">Use the following values to deploy the application gateway described in our scenario.</span></span>

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. <span data-ttu-id="91d2e-174">Save the file.</span><span class="sxs-lookup"><span data-stu-id="91d2e-174">Save the file.</span></span> <span data-ttu-id="91d2e-175">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="91d2e-175">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="91d2e-176">Deploy the Azure Resource Manager template by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="91d2e-176">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="91d2e-177">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="91d2e-177">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions to sign into Azure and select your subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="91d2e-178">Step 1</span><span class="sxs-lookup"><span data-stu-id="91d2e-178">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="91d2e-179">Step 2</span><span class="sxs-lookup"><span data-stu-id="91d2e-179">Step 2</span></span>

<span data-ttu-id="91d2e-180">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="91d2e-180">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="91d2e-181">You are prompted to authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="91d2e-181">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="91d2e-182">Step 3</span><span class="sxs-lookup"><span data-stu-id="91d2e-182">Step 3</span></span>

<span data-ttu-id="91d2e-183">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="91d2e-183">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="91d2e-184">Step 4</span><span class="sxs-lookup"><span data-stu-id="91d2e-184">Step 4</span></span>

<span data-ttu-id="91d2e-185">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="91d2e-185">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="91d2e-186">In the following example, you create a resource group called AppgatewayRG in East US location.</span><span class="sxs-lookup"><span data-stu-id="91d2e-186">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

```powershell
New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
```

<span data-ttu-id="91d2e-187">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span><span class="sxs-lookup"><span data-stu-id="91d2e-187">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
-TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="91d2e-188">Deploy the Azure Resource Manager template by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="91d2e-188">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="91d2e-189">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span><span class="sxs-lookup"><span data-stu-id="91d2e-189">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="91d2e-190">Step 1</span><span class="sxs-lookup"><span data-stu-id="91d2e-190">Step 1</span></span>

<span data-ttu-id="91d2e-191">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="91d2e-191">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

### <a name="step-2"></a><span data-ttu-id="91d2e-192">Step 2</span><span class="sxs-lookup"><span data-stu-id="91d2e-192">Step 2</span></span>

<span data-ttu-id="91d2e-193">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span><span class="sxs-lookup"><span data-stu-id="91d2e-193">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="91d2e-194">Notice the output of the command.</span><span class="sxs-lookup"><span data-stu-id="91d2e-194">Notice the output of the command.</span></span> <span data-ttu-id="91d2e-195">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="91d2e-195">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="91d2e-196">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91d2e-196">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

```azurecli
az group create --location westus --name appgatewayRG
```

<span data-ttu-id="91d2e-197">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-197">**-n (or --name)**.</span></span> <span data-ttu-id="91d2e-198">Name for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="91d2e-198">Name for the new resource group.</span></span> <span data-ttu-id="91d2e-199">For our scenario, it's *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="91d2e-199">For our scenario, it's *appgatewayRG*.</span></span>

<span data-ttu-id="91d2e-200">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-200">**-l (or --location)**.</span></span> <span data-ttu-id="91d2e-201">Azure region where the new resource group is created.</span><span class="sxs-lookup"><span data-stu-id="91d2e-201">Azure region where the new resource group is created.</span></span> <span data-ttu-id="91d2e-202">For our scenario, it's *westus*.</span><span class="sxs-lookup"><span data-stu-id="91d2e-202">For our scenario, it's *westus*.</span></span>

### <a name="step-4"></a><span data-ttu-id="91d2e-203">Step 4</span><span class="sxs-lookup"><span data-stu-id="91d2e-203">Step 4</span></span>

<span data-ttu-id="91d2e-204">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="91d2e-204">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="91d2e-205">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="91d2e-205">The list shown after the output explains the parameters used.</span></span>

```azurecli
az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="91d2e-206">Deploy the Azure Resource Manager template by using click-to-deploy</span><span class="sxs-lookup"><span data-stu-id="91d2e-206">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="91d2e-207">Click-to-deploy is another way to use Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="91d2e-207">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="91d2e-208">It's an easy way to use templates with the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91d2e-208">It's an easy way to use templates with the Azure portal.</span></span>

### <a name="step-1"></a><span data-ttu-id="91d2e-209">Step 1</span><span class="sxs-lookup"><span data-stu-id="91d2e-209">Step 1</span></span>

<span data-ttu-id="91d2e-210">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="91d2e-210">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

### <a name="step-2"></a><span data-ttu-id="91d2e-211">Step 2</span><span class="sxs-lookup"><span data-stu-id="91d2e-211">Step 2</span></span>

<span data-ttu-id="91d2e-212">Click **Deploy to Azure**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-212">Click **Deploy to Azure**.</span></span>

![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-arm-template/deploytoazure.png)

### <a name="step-3"></a><span data-ttu-id="91d2e-214">Step 3</span><span class="sxs-lookup"><span data-stu-id="91d2e-214">Step 3</span></span>

<span data-ttu-id="91d2e-215">Fill out the parameters for the deployment template on the portal and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-215">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

![Parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-gateway-arm-template/ibiza1.png)

### <a name="step-4"></a><span data-ttu-id="91d2e-217">Step 4</span><span class="sxs-lookup"><span data-stu-id="91d2e-217">Step 4</span></span>

<span data-ttu-id="91d2e-218">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-218">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

### <a name="step-5"></a><span data-ttu-id="91d2e-219">Step 5</span><span class="sxs-lookup"><span data-stu-id="91d2e-219">Step 5</span></span>

<span data-ttu-id="91d2e-220">On the Custom deployment blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="91d2e-220">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="91d2e-221">Providing certificate data to Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="91d2e-221">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="91d2e-222">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span><span class="sxs-lookup"><span data-stu-id="91d2e-222">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="91d2e-223">To convert a .pfx or .cer to a base64 string run the following PowerShell command.</span><span class="sxs-lookup"><span data-stu-id="91d2e-223">To convert a .pfx or .cer to a base64 string run the following PowerShell command.</span></span> <span data-ttu-id="91d2e-224">This snippet converts the certificate to a base64 string, which can be provided to the template.</span><span class="sxs-lookup"><span data-stu-id="91d2e-224">This snippet converts the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="91d2e-225">The expected output is a string that can be stored in a variable and pasted in the template.</span><span class="sxs-lookup"><span data-stu-id="91d2e-225">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="next-steps"></a><span data-ttu-id="91d2e-226">Next steps</span><span class="sxs-lookup"><span data-stu-id="91d2e-226">Next steps</span></span>

<span data-ttu-id="91d2e-227">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="91d2e-227">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="91d2e-228">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="91d2e-228">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="91d2e-229">If you want more information about load balancing options in general, visit:</span><span class="sxs-lookup"><span data-stu-id="91d2e-229">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="91d2e-230">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="91d2e-230">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="91d2e-231">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="91d2e-231">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)




