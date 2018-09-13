---
title: Create an Azure Application Gateway - templates | Microsoft Docs
description: This page provides instructions to create an Azure application gateway by using the Azure Resource Manager template
documentationcenter: na
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: victorh
ms.openlocfilehash: 24f834c907fee6f2ddae766ae7494f73a31447c5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968663"
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="e2310-103">Create an application gateway by using the Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="e2310-103">Create an application gateway by using the Azure Resource Manager template</span></span>

<span data-ttu-id="e2310-104">Azure Application Gateway is a layer-7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="e2310-104">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="e2310-105">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span><span class="sxs-lookup"><span data-stu-id="e2310-105">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="e2310-106">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span><span class="sxs-lookup"><span data-stu-id="e2310-106">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="e2310-107">To find a complete list of supported features, visit [Application Gateway overview](overview.md)</span><span class="sxs-lookup"><span data-stu-id="e2310-107">To find a complete list of supported features, visit [Application Gateway overview](overview.md)</span></span>

<span data-ttu-id="e2310-108">This article walks you through downloading and modifying an existing [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e2310-108">This article walks you through downloading and modifying an existing [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="e2310-109">If you are simply deploying the template directly from GitHub without any changes, skip to deploy a template from GitHub.</span><span class="sxs-lookup"><span data-stu-id="e2310-109">If you are simply deploying the template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="e2310-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="e2310-110">Scenario</span></span>

<span data-ttu-id="e2310-111">In this scenario you will:</span><span class="sxs-lookup"><span data-stu-id="e2310-111">In this scenario you will:</span></span>

* <span data-ttu-id="e2310-112">Create an application gateway with web application firewall.</span><span class="sxs-lookup"><span data-stu-id="e2310-112">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="e2310-113">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="e2310-113">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="e2310-114">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span><span class="sxs-lookup"><span data-stu-id="e2310-114">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="e2310-115">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span><span class="sxs-lookup"><span data-stu-id="e2310-115">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="e2310-116">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="e2310-116">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="e2310-117">Those settings are the parameters for this template.</span><span class="sxs-lookup"><span data-stu-id="e2310-117">Those settings are the parameters for this template.</span></span> <span data-ttu-id="e2310-118">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span><span class="sxs-lookup"><span data-stu-id="e2310-118">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![Scenario](./media/create-vmss-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="e2310-120">Download and understand the Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="e2310-120">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="e2310-121">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span><span class="sxs-lookup"><span data-stu-id="e2310-121">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="e2310-122">To do so, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2310-122">To do so, use the following steps:</span></span>

1. <span data-ttu-id="e2310-123">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="e2310-123">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="e2310-124">Click **azuredeploy.json**, and then click **RAW**.</span><span class="sxs-lookup"><span data-stu-id="e2310-124">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="e2310-125">Save the file to a local folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="e2310-125">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="e2310-126">If you are familiar with Azure Resource Manager templates, skip to step 7.</span><span class="sxs-lookup"><span data-stu-id="e2310-126">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="e2310-127">Open the file that you saved and look at the contents under **parameters** in line</span><span class="sxs-lookup"><span data-stu-id="e2310-127">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="e2310-128">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span><span class="sxs-lookup"><span data-stu-id="e2310-128">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="e2310-129">Parameter</span><span class="sxs-lookup"><span data-stu-id="e2310-129">Parameter</span></span> | <span data-ttu-id="e2310-130">Description</span><span class="sxs-lookup"><span data-stu-id="e2310-130">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="e2310-131">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="e2310-131">**subnetPrefix**</span></span> |<span data-ttu-id="e2310-132">CIDR block for the application gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="e2310-132">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="e2310-133">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="e2310-133">**applicationGatewaySize**</span></span> | <span data-ttu-id="e2310-134">Size of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="e2310-134">Size of the application gateway.</span></span>  <span data-ttu-id="e2310-135">WAF only allows medium and large.</span><span class="sxs-lookup"><span data-stu-id="e2310-135">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="e2310-136">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="e2310-136">**backendIpaddress1**</span></span> |<span data-ttu-id="e2310-137">IP address of the first web server.</span><span class="sxs-lookup"><span data-stu-id="e2310-137">IP address of the first web server.</span></span> |
  | <span data-ttu-id="e2310-138">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="e2310-138">**backendIpaddress2**</span></span> |<span data-ttu-id="e2310-139">IP address of the second web server.</span><span class="sxs-lookup"><span data-stu-id="e2310-139">IP address of the second web server.</span></span> |
  | <span data-ttu-id="e2310-140">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="e2310-140">**wafEnabled**</span></span> | <span data-ttu-id="e2310-141">Setting to determine if WAF is enabled.</span><span class="sxs-lookup"><span data-stu-id="e2310-141">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="e2310-142">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="e2310-142">**wafMode**</span></span> | <span data-ttu-id="e2310-143">Mode of the web application firewall.</span><span class="sxs-lookup"><span data-stu-id="e2310-143">Mode of the web application firewall.</span></span>  <span data-ttu-id="e2310-144">Available options are **prevention** or **detection**.</span><span class="sxs-lookup"><span data-stu-id="e2310-144">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="e2310-145">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="e2310-145">**wafRuleSetType**</span></span> | <span data-ttu-id="e2310-146">Ruleset type for WAF.</span><span class="sxs-lookup"><span data-stu-id="e2310-146">Ruleset type for WAF.</span></span>  <span data-ttu-id="e2310-147">Currently OWASP is the only supported option.</span><span class="sxs-lookup"><span data-stu-id="e2310-147">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="e2310-148">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="e2310-148">**wafRuleSetVersion**</span></span> |<span data-ttu-id="e2310-149">Ruleset version.</span><span class="sxs-lookup"><span data-stu-id="e2310-149">Ruleset version.</span></span> <span data-ttu-id="e2310-150">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span><span class="sxs-lookup"><span data-stu-id="e2310-150">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="e2310-151">Check the content under **resources** and notice the following properties:</span><span class="sxs-lookup"><span data-stu-id="e2310-151">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="e2310-152">**type**.</span><span class="sxs-lookup"><span data-stu-id="e2310-152">**type**.</span></span> <span data-ttu-id="e2310-153">Type of resource being created by the template.</span><span class="sxs-lookup"><span data-stu-id="e2310-153">Type of resource being created by the template.</span></span> <span data-ttu-id="e2310-154">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span><span class="sxs-lookup"><span data-stu-id="e2310-154">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="e2310-155">**name**.</span><span class="sxs-lookup"><span data-stu-id="e2310-155">**name**.</span></span> <span data-ttu-id="e2310-156">Name for the resource.</span><span class="sxs-lookup"><span data-stu-id="e2310-156">Name for the resource.</span></span> <span data-ttu-id="e2310-157">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span><span class="sxs-lookup"><span data-stu-id="e2310-157">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="e2310-158">**properties**.</span><span class="sxs-lookup"><span data-stu-id="e2310-158">**properties**.</span></span> <span data-ttu-id="e2310-159">List of properties for the resource.</span><span class="sxs-lookup"><span data-stu-id="e2310-159">List of properties for the resource.</span></span> <span data-ttu-id="e2310-160">This template uses the virtual network and public IP address during application gateway creation.</span><span class="sxs-lookup"><span data-stu-id="e2310-160">This template uses the virtual network and public IP address during application gateway creation.</span></span>

1. <span data-ttu-id="e2310-161">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="e2310-161">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="e2310-162">Click **azuredeploy-parameters.json**, and then click **RAW**.</span><span class="sxs-lookup"><span data-stu-id="e2310-162">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="e2310-163">Save the file to a local folder on your computer.</span><span class="sxs-lookup"><span data-stu-id="e2310-163">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="e2310-164">Open the file that you saved and edit the values for the parameters.</span><span class="sxs-lookup"><span data-stu-id="e2310-164">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="e2310-165">Use the following values to deploy the application gateway described in our scenario.</span><span class="sxs-lookup"><span data-stu-id="e2310-165">Use the following values to deploy the application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="e2310-166">Save the file.</span><span class="sxs-lookup"><span data-stu-id="e2310-166">Save the file.</span></span> <span data-ttu-id="e2310-167">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="e2310-167">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="e2310-168">Deploy the Azure Resource Manager template by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2310-168">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="e2310-169">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="e2310-169">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="e2310-170">Login to PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2310-170">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="e2310-171">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="e2310-171">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="e2310-172">You are prompted to authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="e2310-172">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="e2310-173">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="e2310-173">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="e2310-174">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e2310-174">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="e2310-175">In the following example, you create a resource group called AppgatewayRG in East US location.</span><span class="sxs-lookup"><span data-stu-id="e2310-175">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="e2310-176">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span><span class="sxs-lookup"><span data-stu-id="e2310-176">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="e2310-177">Deploy the Azure Resource Manager template by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e2310-177">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="e2310-178">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2310-178">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="e2310-179">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="e2310-179">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="e2310-180">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span><span class="sxs-lookup"><span data-stu-id="e2310-180">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="e2310-181">Notice the output of the command.</span><span class="sxs-lookup"><span data-stu-id="e2310-181">Notice the output of the command.</span></span> <span data-ttu-id="e2310-182">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="e2310-182">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="e2310-183">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2310-183">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="e2310-184">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="e2310-184">**-n (or --name)**.</span></span> <span data-ttu-id="e2310-185">Name for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="e2310-185">Name for the new resource group.</span></span> <span data-ttu-id="e2310-186">For our scenario, it's *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="e2310-186">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="e2310-187">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="e2310-187">**-l (or --location)**.</span></span> <span data-ttu-id="e2310-188">Azure region where the new resource group is created.</span><span class="sxs-lookup"><span data-stu-id="e2310-188">Azure region where the new resource group is created.</span></span> <span data-ttu-id="e2310-189">For our scenario, it's *westus*.</span><span class="sxs-lookup"><span data-stu-id="e2310-189">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="e2310-190">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="e2310-190">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="e2310-191">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="e2310-191">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="e2310-192">Deploy the Azure Resource Manager template by using click-to-deploy</span><span class="sxs-lookup"><span data-stu-id="e2310-192">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="e2310-193">Click-to-deploy is another way to use Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="e2310-193">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="e2310-194">It's an easy way to use templates with the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e2310-194">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="e2310-195">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="e2310-195">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="e2310-196">Click **Deploy to Azure**.</span><span class="sxs-lookup"><span data-stu-id="e2310-196">Click **Deploy to Azure**.</span></span>

    ![Deploy to Azure](./media/create-vmss-template/deploytoazure.png)
    
1. <span data-ttu-id="e2310-198">Fill out the parameters for the deployment template on the portal and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2310-198">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![Parameters](./media/create-vmss-template/ibiza1.png)
    
1. <span data-ttu-id="e2310-200">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="e2310-200">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="e2310-201">On the Custom deployment blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e2310-201">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="e2310-202">Providing certificate data to Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="e2310-202">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="e2310-203">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span><span class="sxs-lookup"><span data-stu-id="e2310-203">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="e2310-204">To convert a .pfx or .cer to a base64 string use one of the following commands.</span><span class="sxs-lookup"><span data-stu-id="e2310-204">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="e2310-205">The following commands convert the certificate to a base64 string, which can be provided to the template.</span><span class="sxs-lookup"><span data-stu-id="e2310-205">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="e2310-206">The expected output is a string that can be stored in a variable and pasted in the template.</span><span class="sxs-lookup"><span data-stu-id="e2310-206">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="e2310-207">macOS</span><span class="sxs-lookup"><span data-stu-id="e2310-207">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="e2310-208">Windows</span><span class="sxs-lookup"><span data-stu-id="e2310-208">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="e2310-209">Delete all resources</span><span class="sxs-lookup"><span data-stu-id="e2310-209">Delete all resources</span></span>

<span data-ttu-id="e2310-210">To delete all resources created in this article, complete one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2310-210">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="e2310-211">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2310-211">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="e2310-212">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e2310-212">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="e2310-213">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2310-213">Next steps</span></span>

<span data-ttu-id="e2310-214">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](tutorial-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e2310-214">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](tutorial-ssl-cli.md).</span></span>

<span data-ttu-id="e2310-215">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](redirect-internal-site-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e2310-215">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](redirect-internal-site-cli.md).</span></span>

<span data-ttu-id="e2310-216">If you want more information about load balancing options in general, visit:</span><span class="sxs-lookup"><span data-stu-id="e2310-216">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="e2310-217">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e2310-217">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="e2310-218">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e2310-218">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

