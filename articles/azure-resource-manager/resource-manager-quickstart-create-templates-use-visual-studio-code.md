---
title: Use Visual Studio Code to create Azure Resource Manager template | Microsoft Docs
description: Use Visual Studio Code and the Azure Resource Manager tools extension to work on Resource Manager templates.
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
ms.topic: quickstart
ms.author: jgao
ms.openlocfilehash: 73053d83ed42df9af117fc74cf33495a6f4231d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864849"
---
# <a name="quickstart-create-azure-resource-manager-templates-by-using-visual-studio-code"></a><span data-ttu-id="8a355-103">Quickstart: create Azure Resource Manager templates by using Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8a355-103">Quickstart: create Azure Resource Manager templates by using Visual Studio Code</span></span>

<span data-ttu-id="8a355-104">Learn how to create Azure Resource Manager templates by using Visual Studio Code and the Azure Resource Manager Tools extension.</span><span class="sxs-lookup"><span data-stu-id="8a355-104">Learn how to create Azure Resource Manager templates by using Visual Studio Code and the Azure Resource Manager Tools extension.</span></span> <span data-ttu-id="8a355-105">You can create Resource Manager templates in Visual Studio Code without the extension, but the extension provides autocomplete options that simplify template development.</span><span class="sxs-lookup"><span data-stu-id="8a355-105">You can create Resource Manager templates in Visual Studio Code without the extension, but the extension provides autocomplete options that simplify template development.</span></span> <span data-ttu-id="8a355-106">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a355-106">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="8a355-107">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="8a355-107">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a355-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8a355-108">Prerequisites</span></span>

<span data-ttu-id="8a355-109">To complete this article, you need:</span><span class="sxs-lookup"><span data-stu-id="8a355-109">To complete this article, you need:</span></span>

- <span data-ttu-id="8a355-110">[Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="8a355-110">[Visual Studio Code](https://code.visualstudio.com/).</span></span>
- <span data-ttu-id="8a355-111">Resource Manager Tools extension.</span><span class="sxs-lookup"><span data-stu-id="8a355-111">Resource Manager Tools extension.</span></span> <span data-ttu-id="8a355-112">To install, use these steps:</span><span class="sxs-lookup"><span data-stu-id="8a355-112">To install, use these steps:</span></span>

    1. <span data-ttu-id="8a355-113">Open Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8a355-113">Open Visual Studio Code.</span></span>
    2. <span data-ttu-id="8a355-114">Press **CTRL+SHIFT+X** to open the Extensions pane</span><span class="sxs-lookup"><span data-stu-id="8a355-114">Press **CTRL+SHIFT+X** to open the Extensions pane</span></span>
    3. <span data-ttu-id="8a355-115">Search for **Azure Resource Manager Tools**, and then select **Install**.</span><span class="sxs-lookup"><span data-stu-id="8a355-115">Search for **Azure Resource Manager Tools**, and then select **Install**.</span></span>
    4. <span data-ttu-id="8a355-116">Select **Reload** to finish the extension installation.</span><span class="sxs-lookup"><span data-stu-id="8a355-116">Select **Reload** to finish the extension installation.</span></span>

## <a name="open-a-quickstart-template"></a><span data-ttu-id="8a355-117">Open a Quickstart template</span><span class="sxs-lookup"><span data-stu-id="8a355-117">Open a Quickstart template</span></span>

<span data-ttu-id="8a355-118">Instead of creating a template from scratch, you open a template from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/).</span><span class="sxs-lookup"><span data-stu-id="8a355-118">Instead of creating a template from scratch, you open a template from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/).</span></span> <span data-ttu-id="8a355-119">Azure QuickStart Templates is a repository for Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="8a355-119">Azure QuickStart Templates is a repository for Resource Manager templates.</span></span>

<span data-ttu-id="8a355-120">The template used in this quickstart is called [Create a standard storage account](https://azure.microsoft.com/resources/templates/101-storage-account-create/).</span><span class="sxs-lookup"><span data-stu-id="8a355-120">The template used in this quickstart is called [Create a standard storage account](https://azure.microsoft.com/resources/templates/101-storage-account-create/).</span></span> <span data-ttu-id="8a355-121">The template defines an Azure Storage account resource.</span><span class="sxs-lookup"><span data-stu-id="8a355-121">The template defines an Azure Storage account resource.</span></span>

1. <span data-ttu-id="8a355-122">From Visual Studio Code, select **File**>**Open File**.</span><span class="sxs-lookup"><span data-stu-id="8a355-122">From Visual Studio Code, select **File**>**Open File**.</span></span>
2. <span data-ttu-id="8a355-123">In **File name**, paste the following URL:</span><span class="sxs-lookup"><span data-stu-id="8a355-123">In **File name**, paste the following URL:</span></span>

    ```url
    https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
    ```
3. <span data-ttu-id="8a355-124">Select **Open** to open the file.</span><span class="sxs-lookup"><span data-stu-id="8a355-124">Select **Open** to open the file.</span></span>
4. <span data-ttu-id="8a355-125">Select **File**>**Save As** to save the file as **azuredeploy.json** to your local computer.</span><span class="sxs-lookup"><span data-stu-id="8a355-125">Select **File**>**Save As** to save the file as **azuredeploy.json** to your local computer.</span></span>

## <a name="edit-the-template"></a><span data-ttu-id="8a355-126">Edit the template</span><span class="sxs-lookup"><span data-stu-id="8a355-126">Edit the template</span></span>

<span data-ttu-id="8a355-127">To learn how to edit a template using Visual Studio Code, you add one more element into the outputs section.</span><span class="sxs-lookup"><span data-stu-id="8a355-127">To learn how to edit a template using Visual Studio Code, you add one more element into the outputs section.</span></span>

1. <span data-ttu-id="8a355-128">From Visual Studio Code, add one more output to the exported template:</span><span class="sxs-lookup"><span data-stu-id="8a355-128">From Visual Studio Code, add one more output to the exported template:</span></span>

    ```json
    "storageUri": {
      "type": "string",
      "value": "[reference(variables('storageAccountName')).primaryEndpoints.blob]"
    }
    ```

    <span data-ttu-id="8a355-129">When you are done, the outputs section looks like:</span><span class="sxs-lookup"><span data-stu-id="8a355-129">When you are done, the outputs section looks like:</span></span>

    ```json
    "outputs": {
      "storageAccountName": {
        "type": "string",
        "value": "[variables('storageAccountName')]"
      },
      "storageUri": {
        "type": "string",
        "value": "[reference(variables('storageAccountName')).primaryEndpoints.blob]"
      }
    }
    ```

    <span data-ttu-id="8a355-130">If you copied and pasted the code inside Visual Studio Code, try to retype the **value** element to experience the intellisense capability of the Resource Manager Tools extension.</span><span class="sxs-lookup"><span data-stu-id="8a355-130">If you copied and pasted the code inside Visual Studio Code, try to retype the **value** element to experience the intellisense capability of the Resource Manager Tools extension.</span></span>

    ![Resource Manager template visual studio code intellisense](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/resource-manager-templates-visual-studio-code-intellisense.png)

2. <span data-ttu-id="8a355-132">Select **File**>**Save** to save the file.</span><span class="sxs-lookup"><span data-stu-id="8a355-132">Select **File**>**Save** to save the file.</span></span>

## <a name="deploy-the-template"></a><span data-ttu-id="8a355-133">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="8a355-133">Deploy the template</span></span>

<span data-ttu-id="8a355-134">There are many methods for deploying templates.</span><span class="sxs-lookup"><span data-stu-id="8a355-134">There are many methods for deploying templates.</span></span>  <span data-ttu-id="8a355-135">In this quickstart, you use Azure Cloud Shell from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8a355-135">In this quickstart, you use Azure Cloud Shell from the Azure portal.</span></span> <span data-ttu-id="8a355-136">Cloud Shell supports both Azure CLI and Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a355-136">Cloud Shell supports both Azure CLI and Azure PowerShell.</span></span> 

1. <span data-ttu-id="8a355-137">Sign in to the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="8a355-137">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="8a355-138">Select **Cloud Shell** from the upper right corner as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="8a355-138">Select **Cloud Shell** from the upper right corner as shown in the following image:</span></span>

    ![Azure portal Cloud shell](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell.png)

    <span data-ttu-id="8a355-140">Cloud Shell is opened on the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="8a355-140">Cloud Shell is opened on the bottom of the window.</span></span>

3. <span data-ttu-id="8a355-141">On the upper left corner of the Cloud shell, it shows either **PowerShell** or **Bash**.</span><span class="sxs-lookup"><span data-stu-id="8a355-141">On the upper left corner of the Cloud shell, it shows either **PowerShell** or **Bash**.</span></span> <span data-ttu-id="8a355-142">To use CLI, you need to open a Bash session.</span><span class="sxs-lookup"><span data-stu-id="8a355-142">To use CLI, you need to open a Bash session.</span></span> <span data-ttu-id="8a355-143">To run PowerShell, you need to open a PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="8a355-143">To run PowerShell, you need to open a PowerShell session.</span></span> <span data-ttu-id="8a355-144">Select the down arrow to toggle between the Bash and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a355-144">Select the down arrow to toggle between the Bash and PowerShell.</span></span> <span data-ttu-id="8a355-145">The following image shows switching from PowerShell to Bash.</span><span class="sxs-lookup"><span data-stu-id="8a355-145">The following image shows switching from PowerShell to Bash.</span></span>

    ![Azure portal Cloud shell CLI](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-choose-cli.png)

    <span data-ttu-id="8a355-147">Restarting the shell is required when you switch.</span><span class="sxs-lookup"><span data-stu-id="8a355-147">Restarting the shell is required when you switch.</span></span>
4. <span data-ttu-id="8a355-148">Select **Upload/download files**, and then select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="8a355-148">Select **Upload/download files**, and then select **Upload**.</span></span>

    # <a name="clitabcli"></a>[<span data-ttu-id="8a355-149">CLI</span><span class="sxs-lookup"><span data-stu-id="8a355-149">CLI</span></span>](#tab/CLI)

    ![Azure portal Cloud shell upload file](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-upload-file.png)
   
    # <a name="powershelltabpowershell"></a>[<span data-ttu-id="8a355-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a355-151">PowerShell</span></span>](#tab/PowerShell)
    
    ![Azure portal Cloud shell upload file](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-upload-file-powershell.png)
    
    ---

    <span data-ttu-id="8a355-153">You must upload the template file before you can deploy it from the shell.</span><span class="sxs-lookup"><span data-stu-id="8a355-153">You must upload the template file before you can deploy it from the shell.</span></span>
5. <span data-ttu-id="8a355-154">Select the file you saved earlier in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="8a355-154">Select the file you saved earlier in the quickstart.</span></span> <span data-ttu-id="8a355-155">The default name is **azuredeploy.json**.</span><span class="sxs-lookup"><span data-stu-id="8a355-155">The default name is **azuredeploy.json**.</span></span>
6. <span data-ttu-id="8a355-156">From the Cloud shell, run the **ls** command to verify the file is uploaded successfully.</span><span class="sxs-lookup"><span data-stu-id="8a355-156">From the Cloud shell, run the **ls** command to verify the file is uploaded successfully.</span></span> <span data-ttu-id="8a355-157">You can also use the **cat** command to verify the template content.</span><span class="sxs-lookup"><span data-stu-id="8a355-157">You can also use the **cat** command to verify the template content.</span></span> <span data-ttu-id="8a355-158">The following image shows running the command from Bash.</span><span class="sxs-lookup"><span data-stu-id="8a355-158">The following image shows running the command from Bash.</span></span>  <span data-ttu-id="8a355-159">You use the same commands from a PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="8a355-159">You use the same commands from a PowerShell session.</span></span>

    # <a name="clitabcli"></a>[<span data-ttu-id="8a355-160">CLI</span><span class="sxs-lookup"><span data-stu-id="8a355-160">CLI</span></span>](#tab/CLI)

    ![Azure portal Cloud shell list file](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-list-file.png)
   
    # <a name="powershelltabpowershell"></a>[<span data-ttu-id="8a355-162">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a355-162">PowerShell</span></span>](#tab/PowerShell)
    
    ![Azure portal Cloud shell list file](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-list-file-powershell.png)
    
    ---
7. <span data-ttu-id="8a355-164">From the Cloud shell, run the following commands.</span><span class="sxs-lookup"><span data-stu-id="8a355-164">From the Cloud shell, run the following commands.</span></span> <span data-ttu-id="8a355-165">Select the tab to show the PowerShell code or the CLI code.</span><span class="sxs-lookup"><span data-stu-id="8a355-165">Select the tab to show the PowerShell code or the CLI code.</span></span>

    # <a name="clitabcli"></a>[<span data-ttu-id="8a355-166">CLI</span><span class="sxs-lookup"><span data-stu-id="8a355-166">CLI</span></span>](#tab/CLI)
    ```cli
    az group create --name <ResourceGroupName> --location <AzureLocation>

    az group deployment create --name <DeploymentName> --resource-group <ResourceGroupName> --template-file <TemplateFileName>
    ```
   
    # <a name="powershelltabpowershell"></a>[<span data-ttu-id="8a355-167">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a355-167">PowerShell</span></span>](#tab/PowerShell)
    
    ```powershell
    New-AzureRmResourceGroup -Name <ResourceGroupName> -Location <AzureLocation>

    New-AzureRmResourceGroupDeployment -ResourceGroupName <ResourceGroupName> -TemplateFile <TemplateFileName>
    ```
    
    ---

    <span data-ttu-id="8a355-168">The following screenshot shows a sample deployment:</span><span class="sxs-lookup"><span data-stu-id="8a355-168">The following screenshot shows a sample deployment:</span></span>

    # <a name="clitabcli"></a>[<span data-ttu-id="8a355-169">CLI</span><span class="sxs-lookup"><span data-stu-id="8a355-169">CLI</span></span>](#tab/CLI)

    ![Azure portal Cloud shell deploy template](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-deploy-template.png)
   
    # <a name="powershelltabpowershell"></a>[<span data-ttu-id="8a355-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a355-171">PowerShell</span></span>](#tab/PowerShell)
    
    ![Azure portal Cloud shell deploy template](./media/resource-manager-quickstart-create-templates-use-visual-studio-code/azure-portal-cloud-shell-deploy-template-powershell.png)
    
    ---

    <span data-ttu-id="8a355-173">On the screenshot, these values are used:</span><span class="sxs-lookup"><span data-stu-id="8a355-173">On the screenshot, these values are used:</span></span>

    - <span data-ttu-id="8a355-174">**&lt;ResourceGroupName>**: myresourcegroup0709.</span><span class="sxs-lookup"><span data-stu-id="8a355-174">**&lt;ResourceGroupName>**: myresourcegroup0709.</span></span> <span data-ttu-id="8a355-175">There are two appearances of the parameter.</span><span class="sxs-lookup"><span data-stu-id="8a355-175">There are two appearances of the parameter.</span></span>  <span data-ttu-id="8a355-176">Make sure to use the same value.</span><span class="sxs-lookup"><span data-stu-id="8a355-176">Make sure to use the same value.</span></span>
    - <span data-ttu-id="8a355-177">**&lt;AzureLocation>**: eastus2</span><span class="sxs-lookup"><span data-stu-id="8a355-177">**&lt;AzureLocation>**: eastus2</span></span>
    - <span data-ttu-id="8a355-178">**&lt;DeployName>**: mydeployment0709</span><span class="sxs-lookup"><span data-stu-id="8a355-178">**&lt;DeployName>**: mydeployment0709</span></span>
    - <span data-ttu-id="8a355-179">**&lt;TemplateFile>**: azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="8a355-179">**&lt;TemplateFile>**: azuredeploy.json</span></span>

    <span data-ttu-id="8a355-180">From the screenshot output, the storage account name is *3tqebj3slyfyestandardsa*.</span><span class="sxs-lookup"><span data-stu-id="8a355-180">From the screenshot output, the storage account name is *3tqebj3slyfyestandardsa*.</span></span> 

7. <span data-ttu-id="8a355-181">Run the following CLI or PowerShell command to list the newly created storage account:</span><span class="sxs-lookup"><span data-stu-id="8a355-181">Run the following CLI or PowerShell command to list the newly created storage account:</span></span>

    # <a name="clitabcli"></a>[<span data-ttu-id="8a355-182">CLI</span><span class="sxs-lookup"><span data-stu-id="8a355-182">CLI</span></span>](#tab/CLI)
    ```cli
    az storage account show --resource-group <ResourceGroupName> --name <StorageAccountName>
    ```
   
    # <a name="powershelltabpowershell"></a>[<span data-ttu-id="8a355-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a355-183">PowerShell</span></span>](#tab/PowerShell)
    
    ```powershell
    Get-AzureRmStorageAccount -ResourceGroupName <ResourceGroupName> -Name <StorageAccountName>
    ```
    
    ---

## <a name="clean-up-resources"></a><span data-ttu-id="8a355-184">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="8a355-184">Clean up resources</span></span>

<span data-ttu-id="8a355-185">When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="8a355-185">When the Azure resources are no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

1. <span data-ttu-id="8a355-186">From the Azure portal, select **Resource group** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="8a355-186">From the Azure portal, select **Resource group** from the left menu.</span></span>
2. <span data-ttu-id="8a355-187">Enter the resource group name in the **Filter by name** field.</span><span class="sxs-lookup"><span data-stu-id="8a355-187">Enter the resource group name in the **Filter by name** field.</span></span>
3. <span data-ttu-id="8a355-188">Select the resource group name.</span><span class="sxs-lookup"><span data-stu-id="8a355-188">Select the resource group name.</span></span>  <span data-ttu-id="8a355-189">You shall see a total of six resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="8a355-189">You shall see a total of six resources in the resource group.</span></span>
4. <span data-ttu-id="8a355-190">Select **Delete resource group** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="8a355-190">Select **Delete resource group** from the top menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a355-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a355-191">Next steps</span></span>

<span data-ttu-id="8a355-192">The main focus of this quickstart is to use Visual Studio Code to edit an existing template from Azure Quickstart templates.</span><span class="sxs-lookup"><span data-stu-id="8a355-192">The main focus of this quickstart is to use Visual Studio Code to edit an existing template from Azure Quickstart templates.</span></span> <span data-ttu-id="8a355-193">You also learned how to deploy the template using either CLI or PowerShell from Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="8a355-193">You also learned how to deploy the template using either CLI or PowerShell from Azure Cloud Shell.</span></span> <span data-ttu-id="8a355-194">The templates from Azure Quickstart templates might not give you everything you need.</span><span class="sxs-lookup"><span data-stu-id="8a355-194">The templates from Azure Quickstart templates might not give you everything you need.</span></span> <span data-ttu-id="8a355-195">The next tutorial shows you how to find the information from template reference so you can create an encrypted Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="8a355-195">The next tutorial shows you how to find the information from template reference so you can create an encrypted Azure Storage account.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8a355-196">Create an encrypted storage account</span><span class="sxs-lookup"><span data-stu-id="8a355-196">Create an encrypted storage account</span></span>](./resource-manager-tutorial-create-encrypted-storage-accounts.md)
