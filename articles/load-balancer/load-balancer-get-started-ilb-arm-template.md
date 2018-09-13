---
title: Create an Internal load balancer - Azure template | Microsoft Docs
description: Learn how to create an internal load balancer using a template in Resource Manager
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 0cee0950055012cef7324f97e1b8a8f3fbd0112c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660790"
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="e390b-103">Create an internal load balancer using a template</span><span class="sxs-lookup"><span data-stu-id="e390b-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Template](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).  This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="e390b-110">Deploy the template by using click to deploy</span><span class="sxs-lookup"><span data-stu-id="e390b-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="e390b-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span><span class="sxs-lookup"><span data-stu-id="e390b-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="e390b-112">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span><span class="sxs-lookup"><span data-stu-id="e390b-112">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="e390b-113">Deploy the template by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e390b-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="e390b-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="e390b-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="e390b-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="e390b-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="e390b-116">Download the parameters file to your local disk.</span><span class="sxs-lookup"><span data-stu-id="e390b-116">Download the parameters file to your local disk.</span></span>
3. <span data-ttu-id="e390b-117">Edit the file and save it.</span><span class="sxs-lookup"><span data-stu-id="e390b-117">Edit the file and save it.</span></span>
4. <span data-ttu-id="e390b-118">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span><span class="sxs-lookup"><span data-stu-id="e390b-118">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="e390b-119">Deploy the template by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e390b-119">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="e390b-120">To deploy the template by using the Azure CLI, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="e390b-120">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="e390b-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="e390b-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="e390b-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span><span class="sxs-lookup"><span data-stu-id="e390b-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="e390b-123">Here is the expected output for the command above:</span><span class="sxs-lookup"><span data-stu-id="e390b-123">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="e390b-124">Open the parameter file, select its contents, and save it to a file in your computer.</span><span class="sxs-lookup"><span data-stu-id="e390b-124">Open the parameter file, select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="e390b-125">For this example, we saved the parameters file to *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="e390b-125">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="e390b-126">Run the **azure group deployment create** command to deploy the new internal load balancer by using the template and parameter files you downloaded and modified above.</span><span class="sxs-lookup"><span data-stu-id="e390b-126">Run the **azure group deployment create** command to deploy the new internal load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="e390b-127">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="e390b-127">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="e390b-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="e390b-128">Next steps</span></span>

[<span data-ttu-id="e390b-129">Configure a load balancer distribution mode using source IP affinity</span><span class="sxs-lookup"><span data-stu-id="e390b-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="e390b-130">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="e390b-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

