---
title: Create a public load balancer - Azure template | Microsoft Docs
description: Learn how to create a public load balancer in Resource Manager using a template
services: load-balancer
documentationcenter: na
author: KumudD
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: kumud
ms.openlocfilehash: 8452d3a6e165bbcd6007d9dc2261e458746b475a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44794838"
---
# <a name="creating-a-public-load-balancer-using-a-template"></a><span data-ttu-id="7d298-103">Creating a public load balancer using a template</span><span class="sxs-lookup"><span data-stu-id="7d298-103">Creating a public load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Template](../load-balancer/load-balancer-get-started-internet-arm-template.md)



[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="7d298-108">Deploy the template by using click to deploy</span><span class="sxs-lookup"><span data-stu-id="7d298-108">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="7d298-109">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span><span class="sxs-lookup"><span data-stu-id="7d298-109">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="7d298-110">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span><span class="sxs-lookup"><span data-stu-id="7d298-110">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="7d298-111">Deploy the template by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d298-111">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="7d298-112">To deploy the template you downloaded by using PowerShell, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="7d298-112">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="7d298-113">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="7d298-113">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="7d298-114">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span><span class="sxs-lookup"><span data-stu-id="7d298-114">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="7d298-115">Deploy the template by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7d298-115">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="7d298-116">To deploy the template by using the Azure CLI, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="7d298-116">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="7d298-117">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="7d298-117">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="7d298-118">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span><span class="sxs-lookup"><span data-stu-id="7d298-118">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="7d298-119">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="7d298-119">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="7d298-120">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span><span class="sxs-lookup"><span data-stu-id="7d298-120">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span></span> <span data-ttu-id="7d298-121">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="7d298-121">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="7d298-122">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span><span class="sxs-lookup"><span data-stu-id="7d298-122">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="7d298-123">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="7d298-123">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="7d298-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="7d298-124">Next steps</span></span>

[<span data-ttu-id="7d298-125">Get started configuring an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="7d298-125">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="7d298-126">Configure a load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="7d298-126">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="7d298-127">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="7d298-127">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
