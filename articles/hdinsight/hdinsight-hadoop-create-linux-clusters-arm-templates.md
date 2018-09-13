---
title: Create HDInsight (Hadoop) clusters by using templates | Microsoft Docs
description: Learn how to create clusters for HDInsight by using Resource Manager templates
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/14/2017
ms.author: jgao
ms.openlocfilehash: 247acb7e7f89360c9a641a68b8e2a22ab716dcfb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556726"
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="02a85-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="02a85-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="02a85-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="02a85-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="02a85-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="02a85-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="02a85-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-creation-methods).</span><span class="sxs-lookup"><span data-stu-id="02a85-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-creation-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02a85-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="02a85-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="02a85-108">To follow the instructions in this article, you'll need:</span><span class="sxs-lookup"><span data-stu-id="02a85-108">To follow the instructions in this article, you'll need:</span></span>

* <span data-ttu-id="02a85-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="02a85-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="02a85-110">Azure PowerShell and/or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="02a85-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="access-control-requirements"></a><span data-ttu-id="02a85-111">Access control requirements</span><span class="sxs-lookup"><span data-stu-id="02a85-111">Access control requirements</span></span>
[!INCLUDE [access-control](../../includes/hdinsight-access-control-requirements.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="02a85-112">Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="02a85-112">Resource Manager templates</span></span>
<span data-ttu-id="02a85-113">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span><span class="sxs-lookup"><span data-stu-id="02a85-113">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="02a85-114">HDInsight clusters and their dependent resources (such as the default storage account)</span><span class="sxs-lookup"><span data-stu-id="02a85-114">HDInsight clusters and their dependent resources (such as the default storage account)</span></span>
* <span data-ttu-id="02a85-115">Other resources (such as Azure SQL Database to use Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="02a85-115">Other resources (such as Azure SQL Database to use Apache Sqoop)</span></span> 

<span data-ttu-id="02a85-116">In the template, you define the resources that are needed for the application.</span><span class="sxs-lookup"><span data-stu-id="02a85-116">In the template, you define the resources that are needed for the application.</span></span> <span data-ttu-id="02a85-117">You also specify deployment parameters to input values for different environments.</span><span class="sxs-lookup"><span data-stu-id="02a85-117">You also specify deployment parameters to input values for different environments.</span></span> <span data-ttu-id="02a85-118">The template consists of JSON and expressions that you use to construct values for your deployment.</span><span class="sxs-lookup"><span data-stu-id="02a85-118">The template consists of JSON and expressions that you use to construct values for your deployment.</span></span>

<span data-ttu-id="02a85-119">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="02a85-119">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="02a85-120">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span><span class="sxs-lookup"><span data-stu-id="02a85-120">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span></span> <span data-ttu-id="02a85-121">You learn how to call the template by using different methods.</span><span class="sxs-lookup"><span data-stu-id="02a85-121">You learn how to call the template by using different methods.</span></span>

<span data-ttu-id="02a85-122">For more information about Resource Manager templates, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="02a85-122">For more information about Resource Manager templates, see the following articles:</span></span>

* [<span data-ttu-id="02a85-123">Author Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="02a85-123">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="02a85-124">Deploy an application with Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="02a85-124">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="02a85-125">Generate templates</span><span class="sxs-lookup"><span data-stu-id="02a85-125">Generate templates</span></span>

<span data-ttu-id="02a85-126">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span><span class="sxs-lookup"><span data-stu-id="02a85-126">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span></span> <span data-ttu-id="02a85-127">You can then reuse the template.</span><span class="sxs-lookup"><span data-stu-id="02a85-127">You can then reuse the template.</span></span>

<span data-ttu-id="02a85-128">**To generate a template by using the Azure portal**</span><span class="sxs-lookup"><span data-stu-id="02a85-128">**To generate a template by using the Azure portal**</span></span>

1. <span data-ttu-id="02a85-129">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02a85-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="02a85-130">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="02a85-130">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="02a85-131">Follow the instructions to enter properties.</span><span class="sxs-lookup"><span data-stu-id="02a85-131">Follow the instructions to enter properties.</span></span> <span data-ttu-id="02a85-132">You can use either the **Quick create** or the **Custom** option.</span><span class="sxs-lookup"><span data-stu-id="02a85-132">You can use either the **Quick create** or the **Custom** option.</span></span>
4. <span data-ttu-id="02a85-133">On the **Summary** tab, click **Download template and parameters**:</span><span class="sxs-lookup"><span data-stu-id="02a85-133">On the **Summary** tab, click **Download template and parameters**:</span></span>

    ![HDInsight Hadoop create cluster Resource Manager template download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="02a85-135">You see a list of the template file, parameters file, and code samples used to deploy the template:</span><span class="sxs-lookup"><span data-stu-id="02a85-135">You see a list of the template file, parameters file, and code samples used to deploy the template:</span></span>

    ![HDInsight Hadoop create cluster Resource Manager template download options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="02a85-137">From here, you can download the template, save it to your template library, or deploy the template.</span><span class="sxs-lookup"><span data-stu-id="02a85-137">From here, you can download the template, save it to your template library, or deploy the template.</span></span>

    <span data-ttu-id="02a85-138">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span><span class="sxs-lookup"><span data-stu-id="02a85-138">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="02a85-139">The template and parameters file must be used together.</span><span class="sxs-lookup"><span data-stu-id="02a85-139">The template and parameters file must be used together.</span></span> <span data-ttu-id="02a85-140">Otherwise, you might get unexpected results.</span><span class="sxs-lookup"><span data-stu-id="02a85-140">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="02a85-141">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span><span class="sxs-lookup"><span data-stu-id="02a85-141">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="02a85-142">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="02a85-142">Deploy with PowerShell</span></span>

<span data-ttu-id="02a85-143">This procedure creates a Hadoop cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02a85-143">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="02a85-144">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span><span class="sxs-lookup"><span data-stu-id="02a85-144">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span></span> <span data-ttu-id="02a85-145">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="02a85-145">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="02a85-146">Set the parameters and variables if needed.</span><span class="sxs-lookup"><span data-stu-id="02a85-146">Set the parameters and variables if needed.</span></span>
3. <span data-ttu-id="02a85-147">Run the template by using the following PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="02a85-147">Run the template by using the following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect to Azure
        ####################################
        #region - Connect to Azure subscription
        Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and the dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="02a85-148">The PowerShell script configures only the cluster name.</span><span class="sxs-lookup"><span data-stu-id="02a85-148">The PowerShell script configures only the cluster name.</span></span> <span data-ttu-id="02a85-149">The storage account name is hard-coded in the template.</span><span class="sxs-lookup"><span data-stu-id="02a85-149">The storage account name is hard-coded in the template.</span></span> <span data-ttu-id="02a85-150">You are prompted to enter the cluster user password.</span><span class="sxs-lookup"><span data-stu-id="02a85-150">You are prompted to enter the cluster user password.</span></span> <span data-ttu-id="02a85-151">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span><span class="sxs-lookup"><span data-stu-id="02a85-151">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span></span> <span data-ttu-id="02a85-152">(The default SSH username is **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="02a85-152">(The default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="02a85-153">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy).</span><span class="sxs-lookup"><span data-stu-id="02a85-153">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="02a85-154">Deploy with CLI</span><span class="sxs-lookup"><span data-stu-id="02a85-154">Deploy with CLI</span></span>
<span data-ttu-id="02a85-155">The following sample uses Azure command-line interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="02a85-155">The following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="02a85-156">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span><span class="sxs-lookup"><span data-stu-id="02a85-156">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="02a85-157">You are prompted to enter:</span><span class="sxs-lookup"><span data-stu-id="02a85-157">You are prompted to enter:</span></span>
* <span data-ttu-id="02a85-158">The cluster name.</span><span class="sxs-lookup"><span data-stu-id="02a85-158">The cluster name.</span></span>
* <span data-ttu-id="02a85-159">The cluster user password.</span><span class="sxs-lookup"><span data-stu-id="02a85-159">The cluster user password.</span></span> <span data-ttu-id="02a85-160">(The default username is **admin**.)</span><span class="sxs-lookup"><span data-stu-id="02a85-160">(The default username is **admin**.)</span></span>
* <span data-ttu-id="02a85-161">The SSH user password.</span><span class="sxs-lookup"><span data-stu-id="02a85-161">The SSH user password.</span></span> <span data-ttu-id="02a85-162">(The default SSH username is **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="02a85-162">(The default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="02a85-163">The following code provides inline parameters:</span><span class="sxs-lookup"><span data-stu-id="02a85-163">The following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="02a85-164">Deploy with the REST API</span><span class="sxs-lookup"><span data-stu-id="02a85-164">Deploy with the REST API</span></span>
<span data-ttu-id="02a85-165">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="02a85-165">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="02a85-166">Deploy with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="02a85-166">Deploy with Visual Studio</span></span>
 <span data-ttu-id="02a85-167">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span><span class="sxs-lookup"><span data-stu-id="02a85-167">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span></span> <span data-ttu-id="02a85-168">You select the type of resources to include in your project.</span><span class="sxs-lookup"><span data-stu-id="02a85-168">You select the type of resources to include in your project.</span></span> <span data-ttu-id="02a85-169">Those resources are automatically added to the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="02a85-169">Those resources are automatically added to the Resource Manager template.</span></span> <span data-ttu-id="02a85-170">The project also provides a PowerShell script to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="02a85-170">The project also provides a PowerShell script to deploy the template.</span></span>

<span data-ttu-id="02a85-171">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="02a85-171">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="02a85-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="02a85-172">Next steps</span></span>
<span data-ttu-id="02a85-173">In this article, you have learned several ways to create an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="02a85-173">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="02a85-174">To learn more, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="02a85-174">To learn more, see the following articles:</span></span>

* <span data-ttu-id="02a85-175">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="02a85-175">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="02a85-176">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="02a85-176">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="02a85-177">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="02a85-177">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="02a85-178">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="02a85-178">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="02a85-179">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="02a85-179">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template"></a><span data-ttu-id="02a85-180">Appendix: Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="02a85-180">Appendix: Resource Manager template</span></span>
<span data-ttu-id="02a85-181">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="02a85-181">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="02a85-182">This sample includes configuration information for Hive metastore and Oozie metastore.</span><span class="sxs-lookup"><span data-stu-id="02a85-182">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="02a85-183">Remove the section or configure the section before using the template.</span><span class="sxs-lookup"><span data-stu-id="02a85-183">Remove the section or configure the section before using the template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "The name of the HDInsight cluster to create."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used to remotely access the cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "The location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "The type of the HDInsight cluster to create."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "The number of nodes in the HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }


