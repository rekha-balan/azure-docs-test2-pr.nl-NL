---
title: Create Azure Resource Manager templates with dependent resources | Microsoft Docs
description: Learn how to create an Azure Resource Manager template with multiple resources, and how to deploy it using the Azure portal
services: azure-resource-manager
documentationcenter: ''
author: mumian
manager: dougeby
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/07/2018
ms.topic: tutorial
ms.author: jgao
ms.openlocfilehash: e5ced038d5f1ab57939221a0392ab436560c348d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870438"
---
# <a name="tutorial-create-azure-resource-manager-templates-with-dependent-resources"></a><span data-ttu-id="a05dc-103">Tutorial: create Azure Resource Manager templates with dependent resources</span><span class="sxs-lookup"><span data-stu-id="a05dc-103">Tutorial: create Azure Resource Manager templates with dependent resources</span></span>

<span data-ttu-id="a05dc-104">Learn how to create an Azure Resource Manager template to deploy multiple resources.</span><span class="sxs-lookup"><span data-stu-id="a05dc-104">Learn how to create an Azure Resource Manager template to deploy multiple resources.</span></span>  <span data-ttu-id="a05dc-105">After you create the template, you deploy the template using the Cloud shell from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a05dc-105">After you create the template, you deploy the template using the Cloud shell from the Azure portal.</span></span>

<span data-ttu-id="a05dc-106">Some of the resources cannot be deployed until another resource exists.</span><span class="sxs-lookup"><span data-stu-id="a05dc-106">Some of the resources cannot be deployed until another resource exists.</span></span> <span data-ttu-id="a05dc-107">For example, you can't create the virtual machine until its storage account and network interface exist.</span><span class="sxs-lookup"><span data-stu-id="a05dc-107">For example, you can't create the virtual machine until its storage account and network interface exist.</span></span> <span data-ttu-id="a05dc-108">You define this relationship by making one resource as dependent on the other resources.</span><span class="sxs-lookup"><span data-stu-id="a05dc-108">You define this relationship by making one resource as dependent on the other resources.</span></span> <span data-ttu-id="a05dc-109">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span><span class="sxs-lookup"><span data-stu-id="a05dc-109">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="a05dc-110">When resources aren't dependent on each other, Resource Manager deploys them in parallel.</span><span class="sxs-lookup"><span data-stu-id="a05dc-110">When resources aren't dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="a05dc-111">For more information, see [Define the order for deploying resources in Azure Resource Manager Templates](./resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="a05dc-111">For more information, see [Define the order for deploying resources in Azure Resource Manager Templates](./resource-group-define-dependencies.md).</span></span>

<span data-ttu-id="a05dc-112">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="a05dc-112">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a05dc-113">Open a quickstart template</span><span class="sxs-lookup"><span data-stu-id="a05dc-113">Open a quickstart template</span></span>
> * <span data-ttu-id="a05dc-114">Explore the template</span><span class="sxs-lookup"><span data-stu-id="a05dc-114">Explore the template</span></span>
> * <span data-ttu-id="a05dc-115">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="a05dc-115">Deploy the template</span></span>

<span data-ttu-id="a05dc-116">The instructions in this tutorial create a virtual machine, a virtual network, and some other dependent resources.</span><span class="sxs-lookup"><span data-stu-id="a05dc-116">The instructions in this tutorial create a virtual machine, a virtual network, and some other dependent resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a05dc-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a05dc-117">Prerequisites</span></span>

<span data-ttu-id="a05dc-118">To complete this article, you need:</span><span class="sxs-lookup"><span data-stu-id="a05dc-118">To complete this article, you need:</span></span>

* <span data-ttu-id="a05dc-119">[Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a05dc-119">[Visual Studio Code](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="a05dc-120">Resource Manager Tools extension.</span><span class="sxs-lookup"><span data-stu-id="a05dc-120">Resource Manager Tools extension.</span></span>  <span data-ttu-id="a05dc-121">See [Install the extension ](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#prerequisites)</span><span class="sxs-lookup"><span data-stu-id="a05dc-121">See [Install the extension ](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#prerequisites)</span></span>

## <a name="open-a-quickstart-template"></a><span data-ttu-id="a05dc-122">Open a Quickstart template</span><span class="sxs-lookup"><span data-stu-id="a05dc-122">Open a Quickstart template</span></span>

<span data-ttu-id="a05dc-123">Azure QuickStart Templates is a repository for Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="a05dc-123">Azure QuickStart Templates is a repository for Resource Manager templates.</span></span> <span data-ttu-id="a05dc-124">Instead of creating a template from scratch, you can find a sample template and customize it.</span><span class="sxs-lookup"><span data-stu-id="a05dc-124">Instead of creating a template from scratch, you can find a sample template and customize it.</span></span> <span data-ttu-id="a05dc-125">The template used in this tutorial is called [Deploy a simple Windows VM](https://azure.microsoft.com/resources/templates/101-vm-simple-windows/).</span><span class="sxs-lookup"><span data-stu-id="a05dc-125">The template used in this tutorial is called [Deploy a simple Windows VM](https://azure.microsoft.com/resources/templates/101-vm-simple-windows/).</span></span>

1. <span data-ttu-id="a05dc-126">From Visual Studio Code, select **File**>**Open File**.</span><span class="sxs-lookup"><span data-stu-id="a05dc-126">From Visual Studio Code, select **File**>**Open File**.</span></span>
2. <span data-ttu-id="a05dc-127">In **File name**, paste the following URL:</span><span class="sxs-lookup"><span data-stu-id="a05dc-127">In **File name**, paste the following URL:</span></span>

    ```url
    https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-windows/azuredeploy.json
    ```
3. <span data-ttu-id="a05dc-128">Select **Open** to open the file.</span><span class="sxs-lookup"><span data-stu-id="a05dc-128">Select **Open** to open the file.</span></span>
4. <span data-ttu-id="a05dc-129">Select **File**>**Save As** to save a copy of the file to your local computer with the name **azuredeploy.json**.</span><span class="sxs-lookup"><span data-stu-id="a05dc-129">Select **File**>**Save As** to save a copy of the file to your local computer with the name **azuredeploy.json**.</span></span>

## <a name="explore-the-template"></a><span data-ttu-id="a05dc-130">Explore the template</span><span class="sxs-lookup"><span data-stu-id="a05dc-130">Explore the template</span></span>

<span data-ttu-id="a05dc-131">When you explore the template in this section, try to answer these questions:</span><span class="sxs-lookup"><span data-stu-id="a05dc-131">When you explore the template in this section, try to answer these questions:</span></span>

- <span data-ttu-id="a05dc-132">How many Azure resources defined in this template?</span><span class="sxs-lookup"><span data-stu-id="a05dc-132">How many Azure resources defined in this template?</span></span>
- <span data-ttu-id="a05dc-133">One of the resources is an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a05dc-133">One of the resources is an Azure storage account.</span></span>  <span data-ttu-id="a05dc-134">Does the definition look like the one used in the last tutorial?</span><span class="sxs-lookup"><span data-stu-id="a05dc-134">Does the definition look like the one used in the last tutorial?</span></span>
- <span data-ttu-id="a05dc-135">Can you find the template references for the resources defined in this template?</span><span class="sxs-lookup"><span data-stu-id="a05dc-135">Can you find the template references for the resources defined in this template?</span></span>
- <span data-ttu-id="a05dc-136">Can you find the dependencies of the resources?</span><span class="sxs-lookup"><span data-stu-id="a05dc-136">Can you find the dependencies of the resources?</span></span>

1. <span data-ttu-id="a05dc-137">From Visual Studio Code, collapse the elements until you only see the first-level elements and the second-level elements inside **resources**:</span><span class="sxs-lookup"><span data-stu-id="a05dc-137">From Visual Studio Code, collapse the elements until you only see the first-level elements and the second-level elements inside **resources**:</span></span>

    ![Visual Studio Code Azure Resource Manager templates](./media/resource-manager-tutorial-create-templates-with-dependent-resources/resource-manager-template-visual-studio-code.png)

    <span data-ttu-id="a05dc-139">There are five resources defined by the template.</span><span class="sxs-lookup"><span data-stu-id="a05dc-139">There are five resources defined by the template.</span></span>
2. <span data-ttu-id="a05dc-140">Expand the first resource.</span><span class="sxs-lookup"><span data-stu-id="a05dc-140">Expand the first resource.</span></span> <span data-ttu-id="a05dc-141">It is a storage account.</span><span class="sxs-lookup"><span data-stu-id="a05dc-141">It is a storage account.</span></span> <span data-ttu-id="a05dc-142">The definition shall be identical to the one used at the begining of the last tutorial.</span><span class="sxs-lookup"><span data-stu-id="a05dc-142">The definition shall be identical to the one used at the begining of the last tutorial.</span></span>

    ![Visual Studio Code Azure Resource Manager templates storage account definition](./media/resource-manager-tutorial-create-templates-with-dependent-resources/resource-manager-template-storage-account-definition.png)

3. <span data-ttu-id="a05dc-144">Expand the second resource.</span><span class="sxs-lookup"><span data-stu-id="a05dc-144">Expand the second resource.</span></span> <span data-ttu-id="a05dc-145">The resource type is **Microsoft.Network/publicIPAddresses**.</span><span class="sxs-lookup"><span data-stu-id="a05dc-145">The resource type is **Microsoft.Network/publicIPAddresses**.</span></span> <span data-ttu-id="a05dc-146">To find the template reference, browse to [template reference](https://docs.microsoft.com/azure/templates/), enter **public ip address** or **public ip addresses** in the **Filter by title** field.</span><span class="sxs-lookup"><span data-stu-id="a05dc-146">To find the template reference, browse to [template reference](https://docs.microsoft.com/azure/templates/), enter **public ip address** or **public ip addresses** in the **Filter by title** field.</span></span> <span data-ttu-id="a05dc-147">Compare the resource definition to the template reference.</span><span class="sxs-lookup"><span data-stu-id="a05dc-147">Compare the resource definition to the template reference.</span></span>

    ![Visual Studio Code Azure Resource Manager templates public IP address definition](./media/resource-manager-tutorial-create-templates-with-dependent-resources/resource-manager-template-public-ip-address-definition.png)
4. <span data-ttu-id="a05dc-149">Repeat the last step to find the template references for the other resources defined in this template.</span><span class="sxs-lookup"><span data-stu-id="a05dc-149">Repeat the last step to find the template references for the other resources defined in this template.</span></span>  <span data-ttu-id="a05dc-150">Compare the resource definitions to the references.</span><span class="sxs-lookup"><span data-stu-id="a05dc-150">Compare the resource definitions to the references.</span></span>
5. <span data-ttu-id="a05dc-151">Expand the fourth resource:</span><span class="sxs-lookup"><span data-stu-id="a05dc-151">Expand the fourth resource:</span></span>

    ![Visual Studio Code Azure Resource Manager templates dependson](./media/resource-manager-tutorial-create-templates-with-dependent-resources/resource-manager-template-visual-studio-code-dependson.png)

    <span data-ttu-id="a05dc-153">The dependsOn element enables you to define one resource as a dependent on one or more resources.</span><span class="sxs-lookup"><span data-stu-id="a05dc-153">The dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="a05dc-154">In this example, this resource is a networkInterface.</span><span class="sxs-lookup"><span data-stu-id="a05dc-154">In this example, this resource is a networkInterface.</span></span>  <span data-ttu-id="a05dc-155">It depends on two other resources:</span><span class="sxs-lookup"><span data-stu-id="a05dc-155">It depends on two other resources:</span></span>

    * <span data-ttu-id="a05dc-156">publicIPAddress</span><span class="sxs-lookup"><span data-stu-id="a05dc-156">publicIPAddress</span></span>
    * <span data-ttu-id="a05dc-157">virtualNetwork</span><span class="sxs-lookup"><span data-stu-id="a05dc-157">virtualNetwork</span></span>

6. <span data-ttu-id="a05dc-158">Expand the fifth resource.</span><span class="sxs-lookup"><span data-stu-id="a05dc-158">Expand the fifth resource.</span></span> <span data-ttu-id="a05dc-159">This resource is a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a05dc-159">This resource is a virtual machine.</span></span> <span data-ttu-id="a05dc-160">It depends on two other resources:</span><span class="sxs-lookup"><span data-stu-id="a05dc-160">It depends on two other resources:</span></span>

    * <span data-ttu-id="a05dc-161">storageAccount</span><span class="sxs-lookup"><span data-stu-id="a05dc-161">storageAccount</span></span>
    * <span data-ttu-id="a05dc-162">networkInterface</span><span class="sxs-lookup"><span data-stu-id="a05dc-162">networkInterface</span></span>

<span data-ttu-id="a05dc-163">The following diagram illustrates the resources and the dependency information for this template:</span><span class="sxs-lookup"><span data-stu-id="a05dc-163">The following diagram illustrates the resources and the dependency information for this template:</span></span>

![Visual Studio Code Azure Resource Manager templates dependency diagram](./media/resource-manager-tutorial-create-templates-with-dependent-resources/resource-manager-template-visual-studio-code-dependency-diagram.png)

<span data-ttu-id="a05dc-165">By specifying the dependencies, Resource Manager efficiently deploys the solution.</span><span class="sxs-lookup"><span data-stu-id="a05dc-165">By specifying the dependencies, Resource Manager efficiently deploys the solution.</span></span> <span data-ttu-id="a05dc-166">It deploys the storage account, public IP address, and virtual network in parallel because they have no dependencies.</span><span class="sxs-lookup"><span data-stu-id="a05dc-166">It deploys the storage account, public IP address, and virtual network in parallel because they have no dependencies.</span></span> <span data-ttu-id="a05dc-167">After the public IP address and virtual network are deployed, the network interface is created.</span><span class="sxs-lookup"><span data-stu-id="a05dc-167">After the public IP address and virtual network are deployed, the network interface is created.</span></span> <span data-ttu-id="a05dc-168">When all other resources are deployed, Resource Manager deploys the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a05dc-168">When all other resources are deployed, Resource Manager deploys the virtual machine.</span></span>

## <a name="deploy-the-template"></a><span data-ttu-id="a05dc-169">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="a05dc-169">Deploy the template</span></span>

<span data-ttu-id="a05dc-170">There are many methods for deploying templates.</span><span class="sxs-lookup"><span data-stu-id="a05dc-170">There are many methods for deploying templates.</span></span>  <span data-ttu-id="a05dc-171">In this tutorial, you use Cloud Shell from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a05dc-171">In this tutorial, you use Cloud Shell from the Azure portal.</span></span>

1. <span data-ttu-id="a05dc-172">Sign in to the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="a05dc-172">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="a05dc-173">Select **Cloud Shell** from the upper right corner as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="a05dc-173">Select **Cloud Shell** from the upper right corner as shown in the following image:</span></span>

    ![Azure portal Cloud shell](./media/resource-manager-tutorial-create-templates-with-dependent-resources/azure-portal-cloud-shell.png)
3. <span data-ttu-id="a05dc-175">Select **PowerShell** from the upper left corner of the Cloud shell.</span><span class="sxs-lookup"><span data-stu-id="a05dc-175">Select **PowerShell** from the upper left corner of the Cloud shell.</span></span>  <span data-ttu-id="a05dc-176">You use PowerShell in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a05dc-176">You use PowerShell in this tutorial.</span></span>
4. <span data-ttu-id="a05dc-177">Select **Restart**</span><span class="sxs-lookup"><span data-stu-id="a05dc-177">Select **Restart**</span></span>
5. <span data-ttu-id="a05dc-178">Select **Upload file** from the Cloud shell:</span><span class="sxs-lookup"><span data-stu-id="a05dc-178">Select **Upload file** from the Cloud shell:</span></span>

    ![Azure portal Cloud shell upload file](./media/resource-manager-tutorial-create-templates-with-dependent-resources/azure-portal-cloud-shell-upload-file.png)
6. <span data-ttu-id="a05dc-180">Select the file you saved earlier in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="a05dc-180">Select the file you saved earlier in the tutorial.</span></span> <span data-ttu-id="a05dc-181">The default name is **azuredeploy.json**.</span><span class="sxs-lookup"><span data-stu-id="a05dc-181">The default name is **azuredeploy.json**.</span></span>  <span data-ttu-id="a05dc-182">If you have a file with the same file name, the old file will be overwritten without any notification.</span><span class="sxs-lookup"><span data-stu-id="a05dc-182">If you have a file with the same file name, the old file will be overwritten without any notification.</span></span>
7. <span data-ttu-id="a05dc-183">From the Cloud shell, run the following command to verify the file is uploaded successfully.</span><span class="sxs-lookup"><span data-stu-id="a05dc-183">From the Cloud shell, run the following command to verify the file is uploaded successfully.</span></span> 

    ```shell
    ls
    ```

    ![Azure portal Cloud shell list file](./media/resource-manager-tutorial-create-templates-with-dependent-resources/azure-portal-cloud-shell-list-file.png)

    <span data-ttu-id="a05dc-185">The file name shown on the screenshot is azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="a05dc-185">The file name shown on the screenshot is azuredeploy.json.</span></span>

8. <span data-ttu-id="a05dc-186">From the Cloud shell run the following command to verify the content of the JSON file:</span><span class="sxs-lookup"><span data-stu-id="a05dc-186">From the Cloud shell run the following command to verify the content of the JSON file:</span></span>

    ```shell
    cat azuredeploy.json
    ```
9. <span data-ttu-id="a05dc-187">From the Cloud shell, run the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="a05dc-187">From the Cloud shell, run the following PowerShell commands:</span></span>

    ```powershell
    $resourceGroupName = "<Enter the resource group name>"
    $location = "<Enter the Azure location>"
    $vmAdmin = "<Enter the admin username>"
    $vmPassword = "<Enter the password>"
    $dnsLabelPrefix = "<Enter the prefix>"

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    $vmPW = ConvertTo-SecureString -String $vmPassword -AsPlainText -Force
    New-AzureRmResourceGroupDeployment -Name mydeployment0710 -ResourceGroupName $resourceGroupName `
        -TemplateFile azuredeploy.json -adminUsername $vmAdmin -adminPassword $vmPW `
        -dnsLabelPrefix $dnsLabelPrefix
    ```
    <span data-ttu-id="a05dc-188">Here is the screenshot for a sample deployment:</span><span class="sxs-lookup"><span data-stu-id="a05dc-188">Here is the screenshot for a sample deployment:</span></span>

    ![Azure portal Cloud shell deploy template](./media/resource-manager-tutorial-create-templates-with-dependent-resources/azure-portal-cloud-shell-deploy-template.png)

    <span data-ttu-id="a05dc-190">On the screenshot, these values are used:</span><span class="sxs-lookup"><span data-stu-id="a05dc-190">On the screenshot, these values are used:</span></span>

    * <span data-ttu-id="a05dc-191">**$resourceGroupName**: myresourcegroup0710.</span><span class="sxs-lookup"><span data-stu-id="a05dc-191">**$resourceGroupName**: myresourcegroup0710.</span></span> 
    * <span data-ttu-id="a05dc-192">**$location**: eastus2</span><span class="sxs-lookup"><span data-stu-id="a05dc-192">**$location**: eastus2</span></span>
    * <span data-ttu-id="a05dc-193">**&lt;DeployName>**: mydeployment0710</span><span class="sxs-lookup"><span data-stu-id="a05dc-193">**&lt;DeployName>**: mydeployment0710</span></span>
    * <span data-ttu-id="a05dc-194">**&lt;TemplateFile>**: azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="a05dc-194">**&lt;TemplateFile>**: azuredeploy.json</span></span>
    * <span data-ttu-id="a05dc-195">**Template parameter**s:</span><span class="sxs-lookup"><span data-stu-id="a05dc-195">**Template parameter**s:</span></span>

        * <span data-ttu-id="a05dc-196">**adminUsername**: JohnDole</span><span class="sxs-lookup"><span data-stu-id="a05dc-196">**adminUsername**: JohnDole</span></span>
        * <span data-ttu-id="a05dc-197">**adminPassword**: Pass@word123</span><span class="sxs-lookup"><span data-stu-id="a05dc-197">**adminPassword**: Pass@word123</span></span>
        * <span data-ttu-id="a05dc-198">**dnsLabelPrefix**: myvm0710</span><span class="sxs-lookup"><span data-stu-id="a05dc-198">**dnsLabelPrefix**: myvm0710</span></span>

10. <span data-ttu-id="a05dc-199">Run the following PowerShell command to list the newly created virtual machine:</span><span class="sxs-lookup"><span data-stu-id="a05dc-199">Run the following PowerShell command to list the newly created virtual machine:</span></span>

    ```powershell
    Get-AzureRmVM -Name SimpleWinVM -ResourceGroupName <ResourceGroupName>
    ```

    <span data-ttu-id="a05dc-200">The virtual machine name is hard-coded as **SimpleWinVM** inside the template.</span><span class="sxs-lookup"><span data-stu-id="a05dc-200">The virtual machine name is hard-coded as **SimpleWinVM** inside the template.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="a05dc-201">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a05dc-201">Clean up resources</span></span>

<span data-ttu-id="a05dc-202">When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="a05dc-202">When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

1. <span data-ttu-id="a05dc-203">From the Azure portal, select **Resource group** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="a05dc-203">From the Azure portal, select **Resource group** from the left menu.</span></span>
2. <span data-ttu-id="a05dc-204">Enter the resource group name in the **Filter by name** field.</span><span class="sxs-lookup"><span data-stu-id="a05dc-204">Enter the resource group name in the **Filter by name** field.</span></span>
3. <span data-ttu-id="a05dc-205">Select the resource group name.</span><span class="sxs-lookup"><span data-stu-id="a05dc-205">Select the resource group name.</span></span>  <span data-ttu-id="a05dc-206">You shall see a total of six resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="a05dc-206">You shall see a total of six resources in the resource group.</span></span>
4. <span data-ttu-id="a05dc-207">Select **Delete resource group** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="a05dc-207">Select **Delete resource group** from the top menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a05dc-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="a05dc-208">Next steps</span></span>

<span data-ttu-id="a05dc-209">In this tutorial, you develop and deploy a template to create a virtual machine, a virtual network, and the dependent resources.</span><span class="sxs-lookup"><span data-stu-id="a05dc-209">In this tutorial, you develop and deploy a template to create a virtual machine, a virtual network, and the dependent resources.</span></span> <span data-ttu-id="a05dc-210">To learn more about templates, see [Understand the structure and syntax of Azure Resource Manager Templates](./resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a05dc-210">To learn more about templates, see [Understand the structure and syntax of Azure Resource Manager Templates](./resource-group-authoring-templates.md).</span></span>