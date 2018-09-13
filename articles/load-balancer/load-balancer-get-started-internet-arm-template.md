---
title: Create an Internet-facing load balancer - Azure template | Microsoft Docs
description: Learn how to create an Internet facing load balancer in Resource Manager using a template
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3539d6f6d3741387174e80ecc132db782d7df9f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671660"
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="adfc6-103">Creating an Internet facing load balancer using a template</span><span class="sxs-lookup"><span data-stu-id="adfc6-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Template](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="adfc6-108">This article covers the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="adfc6-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="adfc6-109">You can also [Learn how to create an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="adfc6-109">You can also [Learn how to create an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="adfc6-110">Deploy the template by using click to deploy</span><span class="sxs-lookup"><span data-stu-id="adfc6-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="adfc6-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span><span class="sxs-lookup"><span data-stu-id="adfc6-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="adfc6-112">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span><span class="sxs-lookup"><span data-stu-id="adfc6-112">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="adfc6-113">Deploy the template by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="adfc6-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="adfc6-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="adfc6-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="adfc6-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="adfc6-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="adfc6-116">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span><span class="sxs-lookup"><span data-stu-id="adfc6-116">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="adfc6-117">Deploy the template by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="adfc6-117">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="adfc6-118">To deploy the template by using the Azure CLI, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="adfc6-118">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="adfc6-119">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="adfc6-119">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="adfc6-120">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span><span class="sxs-lookup"><span data-stu-id="adfc6-120">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="adfc6-121">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="adfc6-121">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="adfc6-122">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span><span class="sxs-lookup"><span data-stu-id="adfc6-122">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span></span> <span data-ttu-id="adfc6-123">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="adfc6-123">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="adfc6-124">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span><span class="sxs-lookup"><span data-stu-id="adfc6-124">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="adfc6-125">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="adfc6-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="adfc6-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="adfc6-126">Next steps</span></span>

[<span data-ttu-id="adfc6-127">Get started configuring an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="adfc6-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="adfc6-128">Configure a load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="adfc6-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="adfc6-129">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="adfc6-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
