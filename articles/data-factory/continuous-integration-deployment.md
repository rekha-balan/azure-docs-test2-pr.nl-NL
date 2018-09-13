---
title: Continuous integration and deployment in Azure Data Factory | Microsoft Docs
description: Learn how to use continuous integration and deployment to move Data Factory pipelines from one environment (development, test, production) to another.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/16/2018
ms.author: douglasl
ms.openlocfilehash: 57c691271c2b2673ade40d600162934341e18a81
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871357"
---
# <a name="continuous-integration-and-deployment-in-azure-data-factory"></a><span data-ttu-id="c8b8a-103">Continuous integration and deployment in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c8b8a-103">Continuous integration and deployment in Azure Data Factory</span></span>

<span data-ttu-id="c8b8a-104">Continuous Integration is the practice of testing each change done to your codebase automatically and as early as possible.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-104">Continuous Integration is the practice of testing each change done to your codebase automatically and as early as possible.</span></span> <span data-ttu-id="c8b8a-105">Continuous Deployment follows the testing that happens during Continuous Integration and pushes changes to a staging or production system.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-105">Continuous Deployment follows the testing that happens during Continuous Integration and pushes changes to a staging or production system.</span></span>

<span data-ttu-id="c8b8a-106">For Azure Data Factory, continuous integration & deployment means moving Data Factory pipelines from one environment (development, test, production) to another.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-106">For Azure Data Factory, continuous integration & deployment means moving Data Factory pipelines from one environment (development, test, production) to another.</span></span> <span data-ttu-id="c8b8a-107">To do continuous integration & deployment, you can use Data Factory UI integration with Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-107">To do continuous integration & deployment, you can use Data Factory UI integration with Azure Resource Manager templates.</span></span> <span data-ttu-id="c8b8a-108">The Data Factory UI can generate a Resource Manager template when you select the **ARM template** options.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-108">The Data Factory UI can generate a Resource Manager template when you select the **ARM template** options.</span></span> <span data-ttu-id="c8b8a-109">When you select **Export ARM template**, the portal generates the Resource Manager template for the data factory and a configuration file that includes all your connections strings and other parameters.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-109">When you select **Export ARM template**, the portal generates the Resource Manager template for the data factory and a configuration file that includes all your connections strings and other parameters.</span></span> <span data-ttu-id="c8b8a-110">Then you have to create one configuration file for each environment (development, test, production).</span><span class="sxs-lookup"><span data-stu-id="c8b8a-110">Then you have to create one configuration file for each environment (development, test, production).</span></span> <span data-ttu-id="c8b8a-111">The main Resource Manager template file remains the same for all the environments.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-111">The main Resource Manager template file remains the same for all the environments.</span></span>

<span data-ttu-id="c8b8a-112">For a nine-minute introduction and demonstration of this feature, watch the following video:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-112">For a nine-minute introduction and demonstration of this feature, watch the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Continuous-integration-and-deployment-using-Azure-Data-Factory/player]

## <a name="create-a-resource-manager-template-for-each-environment"></a><span data-ttu-id="c8b8a-113">Create a Resource Manager template for each environment</span><span class="sxs-lookup"><span data-stu-id="c8b8a-113">Create a Resource Manager template for each environment</span></span>
<span data-ttu-id="c8b8a-114">Select **Export ARM template** to export the Resource Manager template for your data factory in the development environment.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-114">Select **Export ARM template** to export the Resource Manager template for your data factory in the development environment.</span></span>

![](media/continuous-integration-deployment/continuous-integration-image1.png)

<span data-ttu-id="c8b8a-115">Then go to your test data factory and production data factory and select **Import ARM template**.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-115">Then go to your test data factory and production data factory and select **Import ARM template**.</span></span>

![](media/continuous-integration-deployment/continuous-integration-image2.png)

<span data-ttu-id="c8b8a-116">This action takes you to the Azure portal, where you can import the exported template.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-116">This action takes you to the Azure portal, where you can import the exported template.</span></span> <span data-ttu-id="c8b8a-117">Select **Build your own template in the editor** and then **Load file** and select the generated Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-117">Select **Build your own template in the editor** and then **Load file** and select the generated Resource Manager template.</span></span> <span data-ttu-id="c8b8a-118">Provide the settings, and the data factory and the entire pipeline is imported in your production environment.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-118">Provide the settings, and the data factory and the entire pipeline is imported in your production environment.</span></span>

![](media/continuous-integration-deployment/continuous-integration-image3.png)

![](media/continuous-integration-deployment/continuous-integration-image4.png)

<span data-ttu-id="c8b8a-119">Select **Load file** to select the exported Resource Manager template and provide all the configuration values (for example, linked services).</span><span class="sxs-lookup"><span data-stu-id="c8b8a-119">Select **Load file** to select the exported Resource Manager template and provide all the configuration values (for example, linked services).</span></span>

![](media/continuous-integration-deployment/continuous-integration-image5.png)

<span data-ttu-id="c8b8a-120">**Connection strings**.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-120">**Connection strings**.</span></span> <span data-ttu-id="c8b8a-121">You can find the info required to create connection strings in the articles about the individual connectors.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-121">You can find the info required to create connection strings in the articles about the individual connectors.</span></span> <span data-ttu-id="c8b8a-122">For example, for Azure SQL Database, see [Copy data to or from Azure SQL Database by using Azure Data Factory](connector-azure-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c8b8a-122">For example, for Azure SQL Database, see [Copy data to or from Azure SQL Database by using Azure Data Factory](connector-azure-sql-database.md).</span></span> <span data-ttu-id="c8b8a-123">To verify the correct connection string - for a linked service, for example - you can also open code view for the resource in the Data Factory UI.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-123">To verify the correct connection string - for a linked service, for example - you can also open code view for the resource in the Data Factory UI.</span></span> <span data-ttu-id="c8b8a-124">In code view, however, the password or account key portion of the connection string is removed.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-124">In code view, however, the password or account key portion of the connection string is removed.</span></span> <span data-ttu-id="c8b8a-125">To open code view, select the icon highlighted in the following screen shot.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-125">To open code view, select the icon highlighted in the following screen shot.</span></span>

![Open code view to see connection string](media/continuous-integration-deployment/continuous-integration-codeview.png)

## <a name="continuous-integration-lifecycle"></a><span data-ttu-id="c8b8a-127">Continuous integration lifecycle</span><span class="sxs-lookup"><span data-stu-id="c8b8a-127">Continuous integration lifecycle</span></span>
<span data-ttu-id="c8b8a-128">Here is the entire lifecycle for continuous integration & deployment that you can use after you enable Azure DevOps Services GIT integration in the Data Factory UI:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-128">Here is the entire lifecycle for continuous integration & deployment that you can use after you enable Azure DevOps Services GIT integration in the Data Factory UI:</span></span>

1.  <span data-ttu-id="c8b8a-129">Set up a development data factory with Azure DevOps Services in which all developers can author Data Factory resources like pipelines, datasets, and so forth.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-129">Set up a development data factory with Azure DevOps Services in which all developers can author Data Factory resources like pipelines, datasets, and so forth.</span></span>

1.  <span data-ttu-id="c8b8a-130">Then developers can modify resources such as pipelines.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-130">Then developers can modify resources such as pipelines.</span></span> <span data-ttu-id="c8b8a-131">As they make their modifications, they can select **Debug** to see how the pipeline runs with the most recent changes.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-131">As they make their modifications, they can select **Debug** to see how the pipeline runs with the most recent changes.</span></span>

1.  <span data-ttu-id="c8b8a-132">After developers are satisfied with their changes, they can create a pull request from their branch to the master branch (or the collaboration branch) to get their changes reviewed by peers.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-132">After developers are satisfied with their changes, they can create a pull request from their branch to the master branch (or the collaboration branch) to get their changes reviewed by peers.</span></span>

1.  <span data-ttu-id="c8b8a-133">After changes are in the master branch, they can publish to the development factory by selecting **Publish**.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-133">After changes are in the master branch, they can publish to the development factory by selecting **Publish**.</span></span>

1.  <span data-ttu-id="c8b8a-134">When the team is ready to promote changes to the test factory and the production factory, they can export the Resource Manager template from the master branch, or from any other branch in case their master branch backs the live development Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-134">When the team is ready to promote changes to the test factory and the production factory, they can export the Resource Manager template from the master branch, or from any other branch in case their master branch backs the live development Data Factory.</span></span>

1.  <span data-ttu-id="c8b8a-135">The exported Resource Manager template can be deployed with different parameter files to the test factory and the production factory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-135">The exported Resource Manager template can be deployed with different parameter files to the test factory and the production factory.</span></span>

## <a name="automate-continuous-integration-with-azure-devops-services-releases"></a><span data-ttu-id="c8b8a-136">Automate continuous integration with Azure DevOps Services Releases</span><span class="sxs-lookup"><span data-stu-id="c8b8a-136">Automate continuous integration with Azure DevOps Services Releases</span></span>

<span data-ttu-id="c8b8a-137">Here are the steps to set up a Azure DevOps Services Release so you can automate the deployment of a data factory to multiple environments.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-137">Here are the steps to set up a Azure DevOps Services Release so you can automate the deployment of a data factory to multiple environments.</span></span>

![Diagram of continuous integration with Azure DevOps Services](media/continuous-integration-deployment/continuous-integration-image12.png)

### <a name="requirements"></a><span data-ttu-id="c8b8a-139">Requirements</span><span class="sxs-lookup"><span data-stu-id="c8b8a-139">Requirements</span></span>

-   <span data-ttu-id="c8b8a-140">An Azure subscription linked to Team Foundation Server or Azure DevOps Services using the [*Azure Resource Manager service endpoint*](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints#sep-azure-rm).</span><span class="sxs-lookup"><span data-stu-id="c8b8a-140">An Azure subscription linked to Team Foundation Server or Azure DevOps Services using the [*Azure Resource Manager service endpoint*](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints#sep-azure-rm).</span></span>

-   <span data-ttu-id="c8b8a-141">A Data Factory with Azure DevOps Services Git configured.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-141">A Data Factory with Azure DevOps Services Git configured.</span></span>

-   <span data-ttu-id="c8b8a-142">An [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) containing the secrets.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-142">An [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) containing the secrets.</span></span>

### <a name="set-up-a-azure-devops-services-release"></a><span data-ttu-id="c8b8a-143">Set up a Azure DevOps Services Release</span><span class="sxs-lookup"><span data-stu-id="c8b8a-143">Set up a Azure DevOps Services Release</span></span>

1.  <span data-ttu-id="c8b8a-144">Go to your Azure DevOps Services page in the same project as the one configured with the Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-144">Go to your Azure DevOps Services page in the same project as the one configured with the Data Factory.</span></span>

1.  <span data-ttu-id="c8b8a-145">Click on the top menu **Azure Pipelines** &gt; **Releases** &gt; **Create release definition**.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-145">Click on the top menu **Azure Pipelines** &gt; **Releases** &gt; **Create release definition**.</span></span>

    ![](media/continuous-integration-deployment/continuous-integration-image6.png)

1.  <span data-ttu-id="c8b8a-146">Select the **Empty process** template.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-146">Select the **Empty process** template.</span></span>

1.  <span data-ttu-id="c8b8a-147">Enter the name of your environment.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-147">Enter the name of your environment.</span></span>

1.  <span data-ttu-id="c8b8a-148">Add a Git artifact and select the same repo configured with the Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-148">Add a Git artifact and select the same repo configured with the Data Factory.</span></span> <span data-ttu-id="c8b8a-149">Choose `adf_publish` as the default branch with latest default version.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-149">Choose `adf_publish` as the default branch with latest default version.</span></span>

    ![](media/continuous-integration-deployment/continuous-integration-image7.png)

1.  <span data-ttu-id="c8b8a-150">Add an Azure Resource Manager Deployment task:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-150">Add an Azure Resource Manager Deployment task:</span></span>

    <span data-ttu-id="c8b8a-151">a.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-151">a.</span></span>  <span data-ttu-id="c8b8a-152">Create new task, search for **Azure Resource Group Deployment**, and add it.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-152">Create new task, search for **Azure Resource Group Deployment**, and add it.</span></span>

    <span data-ttu-id="c8b8a-153">b.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-153">b.</span></span>  <span data-ttu-id="c8b8a-154">In the Deployment task, choose the subscription, resource group, and location for the target Data Factory, and provide credentials if necessary.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-154">In the Deployment task, choose the subscription, resource group, and location for the target Data Factory, and provide credentials if necessary.</span></span>

    <span data-ttu-id="c8b8a-155">c.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-155">c.</span></span>  <span data-ttu-id="c8b8a-156">Select the **Create or update resource group** action.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-156">Select the **Create or update resource group** action.</span></span>

    <span data-ttu-id="c8b8a-157">d.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-157">d.</span></span>  <span data-ttu-id="c8b8a-158">Select **…**</span><span class="sxs-lookup"><span data-stu-id="c8b8a-158">Select **…**</span></span> <span data-ttu-id="c8b8a-159">in the **Template** field.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-159">in the **Template** field.</span></span> <span data-ttu-id="c8b8a-160">Browse for the Resource Manager template (*ARMTemplateForFactory.json*) that was created by the publish action in the portal.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-160">Browse for the Resource Manager template (*ARMTemplateForFactory.json*) that was created by the publish action in the portal.</span></span> <span data-ttu-id="c8b8a-161">Look for this file in the folder `<FactoryName>` of the `adf_publish` branch.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-161">Look for this file in the folder `<FactoryName>` of the `adf_publish` branch.</span></span>

    <span data-ttu-id="c8b8a-162">e.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-162">e.</span></span>  <span data-ttu-id="c8b8a-163">Do the same thing for the parameters file.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-163">Do the same thing for the parameters file.</span></span> <span data-ttu-id="c8b8a-164">Choose the correct file depending on whether you created a copy or you’re using the default file *ARMTemplateParametersForFactory.json*.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-164">Choose the correct file depending on whether you created a copy or you’re using the default file *ARMTemplateParametersForFactory.json*.</span></span>

    <span data-ttu-id="c8b8a-165">f.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-165">f.</span></span>  <span data-ttu-id="c8b8a-166">Select **…**</span><span class="sxs-lookup"><span data-stu-id="c8b8a-166">Select **…**</span></span> <span data-ttu-id="c8b8a-167">next to the **Override template parameters** field and fill in the information for the target Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-167">next to the **Override template parameters** field and fill in the information for the target Data Factory.</span></span> <span data-ttu-id="c8b8a-168">For the credentials that come from key vault, use the same name for the secret in the following format: assuming the secret’s name is `cred1`, enter `"$(cred1)"` (between quotes).</span><span class="sxs-lookup"><span data-stu-id="c8b8a-168">For the credentials that come from key vault, use the same name for the secret in the following format: assuming the secret’s name is `cred1`, enter `"$(cred1)"` (between quotes).</span></span>

    ![](media/continuous-integration-deployment/continuous-integration-image9.png)

1.  <span data-ttu-id="c8b8a-169">Save the release pipeline.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-169">Save the release pipeline.</span></span>

1.  <span data-ttu-id="c8b8a-170">Create a new release from this release pipeline.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-170">Create a new release from this release pipeline.</span></span>

    ![](media/continuous-integration-deployment/continuous-integration-image10.png)

### <a name="optional---get-the-secrets-from-azure-key-vault"></a><span data-ttu-id="c8b8a-171">Optional - Get the secrets from Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c8b8a-171">Optional - Get the secrets from Azure Key Vault</span></span>

<span data-ttu-id="c8b8a-172">If you have secrets to pass in an Azure Resource Manager template, we recommend using Azure Key Vault with the Azure DevOps Services release.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-172">If you have secrets to pass in an Azure Resource Manager template, we recommend using Azure Key Vault with the Azure DevOps Services release.</span></span>

<span data-ttu-id="c8b8a-173">There are two ways to handle the secrets:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-173">There are two ways to handle the secrets:</span></span>

1.  <span data-ttu-id="c8b8a-174">Add the secrets to parameters file.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-174">Add the secrets to parameters file.</span></span> <span data-ttu-id="c8b8a-175">For more info, see [Use Azure Key Vault to pass secure parameter value during deployment](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="c8b8a-175">For more info, see [Use Azure Key Vault to pass secure parameter value during deployment](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

    -   <span data-ttu-id="c8b8a-176">Create a copy of the parameters file that is uploaded to the publish branch and set the values of the parameters you want to get from key vault with the following format:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-176">Create a copy of the parameters file that is uploaded to the publish branch and set the values of the parameters you want to get from key vault with the following format:</span></span>

    ```json
    {
        "parameters": {
            "azureSqlReportingDbPassword": {
                "reference": {
                    "keyVault": {
                        "id": "/subscriptions/<subId>/resourceGroups/<resourcegroupId> /providers/Microsoft.KeyVault/vaults/<vault-name> "
                    },
                    "secretName": " < secret - name > "
                }
            }
        }
    }
    ```

    -   <span data-ttu-id="c8b8a-177">When you use this method, the secret is pulled from the key vault automatically.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-177">When you use this method, the secret is pulled from the key vault automatically.</span></span>

    -   <span data-ttu-id="c8b8a-178">The parameters file needs to be in the publish branch as well.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-178">The parameters file needs to be in the publish branch as well.</span></span>

1.  <span data-ttu-id="c8b8a-179">Add an [Azure Key Vault task](https://docs.microsoft.com/azure/devops/pipelines/tasks/deploy/azure-key-vault) before the Azure Resource Manager Deployment described in the previous section:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-179">Add an [Azure Key Vault task](https://docs.microsoft.com/azure/devops/pipelines/tasks/deploy/azure-key-vault) before the Azure Resource Manager Deployment described in the previous section:</span></span>

    -   <span data-ttu-id="c8b8a-180">Select the **Tasks** tab, create a new task, search for **Azure Key Vault** and add it.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-180">Select the **Tasks** tab, create a new task, search for **Azure Key Vault** and add it.</span></span>

    -   <span data-ttu-id="c8b8a-181">In the Key Vault task, choose the subscription in which you created the key vault, provide credentials if necessary, and then choose the key vault.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-181">In the Key Vault task, choose the subscription in which you created the key vault, provide credentials if necessary, and then choose the key vault.</span></span>

    ![](media/continuous-integration-deployment/continuous-integration-image8.png)

### <a name="grant-permissions-to-the-azure-devops-services-agent"></a><span data-ttu-id="c8b8a-182">Grant permissions to the Azure DevOps Services agent</span><span class="sxs-lookup"><span data-stu-id="c8b8a-182">Grant permissions to the Azure DevOps Services agent</span></span>
<span data-ttu-id="c8b8a-183">The Azure Key Vault task may fail the first time with an Access Denied error.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-183">The Azure Key Vault task may fail the first time with an Access Denied error.</span></span> <span data-ttu-id="c8b8a-184">Download the logs for the release, and locate the `.ps1` file with the command to give permissions to the Azure DevOps Services agent.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-184">Download the logs for the release, and locate the `.ps1` file with the command to give permissions to the Azure DevOps Services agent.</span></span> <span data-ttu-id="c8b8a-185">You can run the command directly, or you can copy the principal ID from the file and add the access policy manually in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-185">You can run the command directly, or you can copy the principal ID from the file and add the access policy manually in the Azure portal.</span></span> <span data-ttu-id="c8b8a-186">(*Get* and *List* are the minimum permissions required).</span><span class="sxs-lookup"><span data-stu-id="c8b8a-186">(*Get* and *List* are the minimum permissions required).</span></span>

### <a name="update-active-triggers"></a><span data-ttu-id="c8b8a-187">Update active triggers</span><span class="sxs-lookup"><span data-stu-id="c8b8a-187">Update active triggers</span></span>
<span data-ttu-id="c8b8a-188">Deployment can fail if you try to update active triggers.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-188">Deployment can fail if you try to update active triggers.</span></span> <span data-ttu-id="c8b8a-189">To update active triggers, you need to manually stop them and start them after the deployment.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-189">To update active triggers, you need to manually stop them and start them after the deployment.</span></span> <span data-ttu-id="c8b8a-190">You can add an Azure Powershell task for this purpose, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-190">You can add an Azure Powershell task for this purpose, as shown in the following example:</span></span>

1.  <span data-ttu-id="c8b8a-191">In the Tasks tab of the Azure DevOps Services Release, search for **Azure Powershell** and add it.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-191">In the Tasks tab of the Azure DevOps Services Release, search for **Azure Powershell** and add it.</span></span>

1.  <span data-ttu-id="c8b8a-192">Choose **Azure Resource Manager** as the connection type and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-192">Choose **Azure Resource Manager** as the connection type and select your subscription.</span></span>

1.  <span data-ttu-id="c8b8a-193">Choose **Inline Script** as the script type and then provide your code.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-193">Choose **Inline Script** as the script type and then provide your code.</span></span> <span data-ttu-id="c8b8a-194">The following example stops the triggers:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-194">The following example stops the triggers:</span></span>

    ```powershell
    $triggersADF = Get-AzureRmDataFactoryV2Trigger -DataFactoryName $DataFactoryName -ResourceGroupName $ResourceGroupName

    $triggersADF | ForEach-Object { Stop-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name $_.name -Force }
    ```

    ![](media/continuous-integration-deployment/continuous-integration-image11.png)

<span data-ttu-id="c8b8a-195">You can follow similar steps and use similar code (with the `Start-AzureRmDataFactoryV2Trigger` function) to restart the triggers after deployment.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-195">You can follow similar steps and use similar code (with the `Start-AzureRmDataFactoryV2Trigger` function) to restart the triggers after deployment.</span></span>

## <a name="sample-deployment-template"></a><span data-ttu-id="c8b8a-196">Sample deployment template</span><span class="sxs-lookup"><span data-stu-id="c8b8a-196">Sample deployment template</span></span>

<span data-ttu-id="c8b8a-197">Here is a sample deployment template that you can import in Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-197">Here is a sample deployment template that you can import in Azure DevOps Services.</span></span>

```json
{
    "source": 2,
    "id": 1,
    "revision": 51,
    "name": "Data Factory Prod Deployment",
    "description": null,
    "createdBy": {
        "displayName": "Sample User",
        "url": "https://pde14b1dc-d2c9-49e5-88cb-45ccd58d0335.codex.ms/vssps/_apis/Identities/c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
        "id": "c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
        "uniqueName": "sampleuser@microsoft.com",
        "imageUrl": "https://sampleuser.visualstudio.com/_api/_common/identityImage?id=c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
        "descriptor": "aad.M2Y2N2JlZGUtMDViZC03ZWI3LTgxYWMtMDcwM2UyODMxNTBk"
    },
    "createdOn": "2018-03-01T22:57:25.660Z",
    "modifiedBy": {
        "displayName": "Sample User",
        "url": "https://pde14b1dc-d2c9-49e5-88cb-45ccd58d0335.codex.ms/vssps/_apis/Identities/c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
        "id": "c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
        "uniqueName": "sampleuser@microsoft.com",
        "imageUrl": "https://sampleuser.visualstudio.com/_api/_common/identityImage?id=c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
        "descriptor": "aad.M2Y2N2JlZGUtMDViZC03ZWI3LTgxYWMtMDcwM2UyODMxNTBk"
    },
    "modifiedOn": "2018-03-14T17:58:11.643Z",
    "isDeleted": false,
    "path": "\\",
    "variables": {},
    "variableGroups": [],
    "environments": [{
        "id": 1,
        "name": "Prod",
        "rank": 1,
        "owner": {
            "displayName": "Sample User",
            "url": "https://pde14b1dc-d2c9-49e5-88cb-45ccd58d0335.codex.ms/vssps/_apis/Identities/c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
            "id": "c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
            "uniqueName": "sampleuser@microsoft.com",
            "imageUrl": "https://sampleuser.visualstudio.com/_api/_common/identityImage?id=c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
            "descriptor": "aad.M2Y2N2JlZGUtMDViZC03ZWI3LTgxYWMtMDcwM2UyODMxNTBk"
        },
        "variables": {
            "factoryName": {
                "value": "sampleuserprod"
            }
        },
        "variableGroups": [],
        "preDeployApprovals": {
            "approvals": [{
                "rank": 1,
                "isAutomated": true,
                "isNotificationOn": false,
                "id": 1
            }],
            "approvalOptions": {
                "requiredApproverCount": null,
                "releaseCreatorCanBeApprover": false,
                "autoTriggeredAndPreviousEnvironmentApprovedCanBeSkipped": false,
                "enforceIdentityRevalidation": false,
                "timeoutInMinutes": 0,
                "executionOrder": 1
            }
        },
        "deployStep": {
            "id": 2
        },
        "postDeployApprovals": {
            "approvals": [{
                "rank": 1,
                "isAutomated": true,
                "isNotificationOn": false,
                "id": 3
            }],
            "approvalOptions": {
                "requiredApproverCount": null,
                "releaseCreatorCanBeApprover": false,
                "autoTriggeredAndPreviousEnvironmentApprovedCanBeSkipped": false,
                "enforceIdentityRevalidation": false,
                "timeoutInMinutes": 0,
                "executionOrder": 2
            }
        },
        "deployPhases": [{
            "deploymentInput": {
                "parallelExecution": {
                    "parallelExecutionType": "none"
                },
                "skipArtifactsDownload": false,
                "artifactsDownloadInput": {
                    "downloadInputs": []
                },
                "queueId": 19,
                "demands": [],
                "enableAccessToken": false,
                "timeoutInMinutes": 0,
                "jobCancelTimeoutInMinutes": 1,
                "condition": "succeeded()",
                "overrideInputs": {}
            },
            "rank": 1,
            "phaseType": 1,
            "name": "Run on agent",
            "workflowTasks": [{
                "taskId": "72a1931b-effb-4d2e-8fd8-f8472a07cb62",
                "version": "2.*",
                "name": "Azure PowerShell script: FilePath",
                "refName": "",
                "enabled": true,
                "alwaysRun": false,
                "continueOnError": false,
                "timeoutInMinutes": 0,
                "definitionType": "task",
                "overrideInputs": {},
                "condition": "succeeded()",
                "inputs": {
                    "ConnectedServiceNameSelector": "ConnectedServiceNameARM",
                    "ConnectedServiceName": "",
                    "ConnectedServiceNameARM": "e4e2ef4b-8289-41a6-ba7c-92ca469700aa",
                    "ScriptType": "FilePath",
                    "ScriptPath": "$(System.DefaultWorkingDirectory)/Dev/deployment.ps1",
                    "Inline": "param\n(\n    [parameter(Mandatory = $false)] [String] $rootFolder=\"C:\\Users\\sampleuser\\Downloads\\arm_template\",\n    [parameter(Mandatory = $false)] [String] $armTemplate=\"$rootFolder\\arm_template.json\",\n    [parameter(Mandatory = $false)] [String] $armTemplateParameters=\"$rootFolder\\arm_template_parameters.json\",\n    [parameter(Mandatory = $false)] [String] $domain=\"microsoft.onmicrosoft.com\",\n    [parameter(Mandatory = $false)] [String] $TenantId=\"72f988bf-86f1-41af-91ab-2d7cd011db47\",\n    [parame",
                    "ScriptArguments": "-rootFolder \"$(System.DefaultWorkingDirectory)/Dev/\" -DataFactoryName $(factoryname) -predeployment $true",
                    "TargetAzurePs": "LatestVersion",
                    "CustomTargetAzurePs": "5.*"
                }
            }, {
                "taskId": "1e244d32-2dd4-4165-96fb-b7441ca9331e",
                "version": "1.*",
                "name": "Azure Key Vault: sampleuservault",
                "refName": "secret1",
                "enabled": true,
                "alwaysRun": false,
                "continueOnError": false,
                "timeoutInMinutes": 0,
                "definitionType": "task",
                "overrideInputs": {},
                "condition": "succeeded()",
                "inputs": {
                    "ConnectedServiceName": "e4e2ef4b-8289-41a6-ba7c-92ca469700aa",
                    "KeyVaultName": "sampleuservault",
                    "SecretsFilter": "*"
                }
            }, {
                "taskId": "94a74903-f93f-4075-884f-dc11f34058b4",
                "version": "2.*",
                "name": "Azure Deployment:Create Or Update Resource Group action on sampleuser-datafactory",
                "refName": "",
                "enabled": true,
                "alwaysRun": false,
                "continueOnError": false,
                "timeoutInMinutes": 0,
                "definitionType": "task",
                "overrideInputs": {},
                "condition": "succeeded()",
                "inputs": {
                    "ConnectedServiceName": "e4e2ef4b-8289-41a6-ba7c-92ca469700aa",
                    "action": "Create Or Update Resource Group",
                    "resourceGroupName": "sampleuser-datafactory",
                    "location": "East US",
                    "templateLocation": "Linked artifact",
                    "csmFileLink": "",
                    "csmParametersFileLink": "",
                    "csmFile": "$(System.DefaultWorkingDirectory)/Dev/ARMTemplateForFactory.json",
                    "csmParametersFile": "$(System.DefaultWorkingDirectory)/Dev/ARMTemplateParametersForFactory.json",
                    "overrideParameters": "-factoryName \"$(factoryName)\" -linkedService1_connectionString \"$(linkedService1-connectionString)\" -linkedService2_connectionString \"$(linkedService2-connectionString)\"",
                    "deploymentMode": "Incremental",
                    "enableDeploymentPrerequisites": "None",
                    "deploymentGroupEndpoint": "",
                    "project": "",
                    "deploymentGroupName": "",
                    "copyAzureVMTags": "true",
                    "outputVariable": "",
                    "deploymentOutputs": ""
                }
            }, {
                "taskId": "72a1931b-effb-4d2e-8fd8-f8472a07cb62",
                "version": "2.*",
                "name": "Azure PowerShell script: FilePath",
                "refName": "",
                "enabled": true,
                "alwaysRun": false,
                "continueOnError": false,
                "timeoutInMinutes": 0,
                "definitionType": "task",
                "overrideInputs": {},
                "condition": "succeeded()",
                "inputs": {
                    "ConnectedServiceNameSelector": "ConnectedServiceNameARM",
                    "ConnectedServiceName": "",
                    "ConnectedServiceNameARM": "e4e2ef4b-8289-41a6-ba7c-92ca469700aa",
                    "ScriptType": "FilePath",
                    "ScriptPath": "$(System.DefaultWorkingDirectory)/Dev/deployment.ps1",
                    "Inline": "# You can write your azure powershell scripts inline here. \n# You can also pass predefined and custom variables to this script using arguments",
                    "ScriptArguments": "-rootFolder \"$(System.DefaultWorkingDirectory)/Dev/\" -DataFactoryName $(factoryname) -predeployment $false",
                    "TargetAzurePs": "LatestVersion",
                    "CustomTargetAzurePs": ""
                }
            }]
        }],
        "environmentOptions": {
            "emailNotificationType": "OnlyOnFailure",
            "emailRecipients": "release.environment.owner;release.creator",
            "skipArtifactsDownload": false,
            "timeoutInMinutes": 0,
            "enableAccessToken": false,
            "publishDeploymentStatus": true,
            "badgeEnabled": false,
            "autoLinkWorkItems": false
        },
        "demands": [],
        "conditions": [{
            "name": "ReleaseStarted",
            "conditionType": 1,
            "value": ""
        }],
        "executionPolicy": {
            "concurrencyCount": 1,
            "queueDepthCount": 0
        },
        "schedules": [],
        "retentionPolicy": {
            "daysToKeep": 30,
            "releasesToKeep": 3,
            "retainBuild": true
        },
        "processParameters": {
            "dataSourceBindings": [{
                "dataSourceName": "AzureRMWebAppNamesByType",
                "parameters": {
                    "WebAppKind": "$(WebAppKind)"
                },
                "endpointId": "$(ConnectedServiceName)",
                "target": "WebAppName"
            }]
        },
        "properties": {},
        "preDeploymentGates": {
            "id": 0,
            "gatesOptions": null,
            "gates": []
        },
        "postDeploymentGates": {
            "id": 0,
            "gatesOptions": null,
            "gates": []
        },
        "badgeUrl": "https://sampleuser.vsrm.visualstudio.com/_apis/public/Release/badge/19749ef3-2f42-49b5-9696-f28b49faebcb/1/1"
    }, {
        "id": 2,
        "name": "Staging",
        "rank": 2,
        "owner": {
            "displayName": "Sample User",
            "url": "https://pde14b1dc-d2c9-49e5-88cb-45ccd58d0335.codex.ms/vssps/_apis/Identities/c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
            "id": "c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
            "uniqueName": "sampleuser@microsoft.com",
            "imageUrl": "https://sampleuser.visualstudio.com/_api/_common/identityImage?id=c9f828d1-2dbb-4e39-b096-f1c53d82bc2c",
            "descriptor": "aad.M2Y2N2JlZGUtMDViZC03ZWI3LTgxYWMtMDcwM2UyODMxNTBk"
        },
        "variables": {
            "factoryName": {
                "value": "sampleuserstaging"
            }
        },
        "variableGroups": [],
        "preDeployApprovals": {
            "approvals": [{
                "rank": 1,
                "isAutomated": true,
                "isNotificationOn": false,
                "id": 4
            }],
            "approvalOptions": {
                "requiredApproverCount": null,
                "releaseCreatorCanBeApprover": false,
                "autoTriggeredAndPreviousEnvironmentApprovedCanBeSkipped": false,
                "enforceIdentityRevalidation": false,
                "timeoutInMinutes": 0,
                "executionOrder": 1
            }
        },
        "deployStep": {
            "id": 5
        },
        "postDeployApprovals": {
            "approvals": [{
                "rank": 1,
                "isAutomated": true,
                "isNotificationOn": false,
                "id": 6
            }],
            "approvalOptions": {
                "requiredApproverCount": null,
                "releaseCreatorCanBeApprover": false,
                "autoTriggeredAndPreviousEnvironmentApprovedCanBeSkipped": false,
                "enforceIdentityRevalidation": false,
                "timeoutInMinutes": 0,
                "executionOrder": 2
            }
        },
        "deployPhases": [{
            "deploymentInput": {
                "parallelExecution": {
                    "parallelExecutionType": "none"
                },
                "skipArtifactsDownload": false,
                "artifactsDownloadInput": {
                    "downloadInputs": []
                },
                "queueId": 19,
                "demands": [],
                "enableAccessToken": false,
                "timeoutInMinutes": 0,
                "jobCancelTimeoutInMinutes": 1,
                "condition": "succeeded()",
                "overrideInputs": {}
            },
            "rank": 1,
            "phaseType": 1,
            "name": "Run on agent",
            "workflowTasks": [{
                "taskId": "72a1931b-effb-4d2e-8fd8-f8472a07cb62",
                "version": "2.*",
                "name": "Azure PowerShell script: FilePath",
                "refName": "",
                "enabled": true,
                "alwaysRun": false,
                "continueOnError": false,
                "timeoutInMinutes": 0,
                "definitionType": "task",
                "overrideInputs": {},
                "condition": "succeeded()",
                "inputs": {
                    "ConnectedServiceNameSelector": "ConnectedServiceNameARM",
                    "ConnectedServiceName": "",
                    "ConnectedServiceNameARM": "e4e2ef4b-8289-41a6-ba7c-92ca469700aa",
                    "ScriptType": "FilePath",
                    "ScriptPath": "$(System.DefaultWorkingDirectory)/Dev/deployment.ps1",
                    "Inline": "# You can write your azure powershell scripts inline here. \n# You can also pass predefined and custom variables to this script using arguments",
                    "ScriptArguments": "-rootFolder \"$(System.DefaultWorkingDirectory)/Dev/\" -DataFactoryName $(factoryname) -predeployment $true",
                    "TargetAzurePs": "LatestVersion",
                    "CustomTargetAzurePs": ""
                }
            }, {
                "taskId": "1e244d32-2dd4-4165-96fb-b7441ca9331e",
                "version": "1.*",
                "name": "Azure Key Vault: sampleuservault",
                "refName": "",
                "enabled": true,
                "alwaysRun": false,
                "continueOnError": false,
                "timeoutInMinutes": 0,
                "definitionType": "task",
                "overrideInputs": {},
                "condition": "succeeded()",
                "inputs": {
                    "ConnectedServiceName": "e4e2ef4b-8289-41a6-ba7c-92ca469700aa",
                    "KeyVaultName": "sampleuservault",
                    "SecretsFilter": "*"
                }
            }, {
                "taskId": "94a74903-f93f-4075-884f-dc11f34058b4",
                "version": "2.*",
                "name": "Azure Deployment:Create Or Update Resource Group action on sampleuser-datafactory",
                "refName": "",
                "enabled": true,
                "alwaysRun": false,
                "continueOnError": false,
                "timeoutInMinutes": 0,
                "definitionType": "task",
                "overrideInputs": {},
                "condition": "succeeded()",
                "inputs": {
                    "ConnectedServiceName": "e4e2ef4b-8289-41a6-ba7c-92ca469700aa",
                    "action": "Create Or Update Resource Group",
                    "resourceGroupName": "sampleuser-datafactory",
                    "location": "East US",
                    "templateLocation": "Linked artifact",
                    "csmFileLink": "",
                    "csmParametersFileLink": "",
                    "csmFile": "$(System.DefaultWorkingDirectory)/Dev/ARMTemplateForFactory.json",
                    "csmParametersFile": "$(System.DefaultWorkingDirectory)/Dev/ARMTemplateParametersForFactory.json",
                    "overrideParameters": "-factoryName \"$(factoryName)\" -linkedService1_connectionString \"$(linkedService1-connectionString)\" -linkedService2_connectionString \"$(linkedService2-connectionString)\"",
                    "deploymentMode": "Incremental",
                    "enableDeploymentPrerequisites": "None",
                    "deploymentGroupEndpoint": "",
                    "project": "",
                    "deploymentGroupName": "",
                    "copyAzureVMTags": "true",
                    "outputVariable": "",
                    "deploymentOutputs": ""
                }
            }, {
                "taskId": "72a1931b-effb-4d2e-8fd8-f8472a07cb62",
                "version": "2.*",
                "name": "Azure PowerShell script: FilePath",
                "refName": "",
                "enabled": true,
                "alwaysRun": false,
                "continueOnError": false,
                "timeoutInMinutes": 0,
                "definitionType": "task",
                "overrideInputs": {},
                "condition": "succeeded()",
                "inputs": {
                    "ConnectedServiceNameSelector": "ConnectedServiceNameARM",
                    "ConnectedServiceName": "",
                    "ConnectedServiceNameARM": "16a37943-8b58-4c2f-a3d6-052d6f032a07",
                    "ScriptType": "FilePath",
                    "ScriptPath": "$(System.DefaultWorkingDirectory)/Dev/deployment.ps1",
                    "Inline": "param(\n$x,\n$y,\n$z)\nwrite-host \"----------\"\nwrite-host $x\nwrite-host $y\nwrite-host $z | ConvertTo-SecureString\nwrite-host \"----------\"",
                    "ScriptArguments": "-rootFolder \"$(System.DefaultWorkingDirectory)/Dev/\" -DataFactoryName $(factoryname) -predeployment $false",
                    "TargetAzurePs": "LatestVersion",
                    "CustomTargetAzurePs": ""
                }
            }]
        }],
        "environmentOptions": {
            "emailNotificationType": "OnlyOnFailure",
            "emailRecipients": "release.environment.owner;release.creator",
            "skipArtifactsDownload": false,
            "timeoutInMinutes": 0,
            "enableAccessToken": false,
            "publishDeploymentStatus": true,
            "badgeEnabled": false,
            "autoLinkWorkItems": false
        },
        "demands": [],
        "conditions": [{
            "name": "ReleaseStarted",
            "conditionType": 1,
            "value": ""
        }],
        "executionPolicy": {
            "concurrencyCount": 1,
            "queueDepthCount": 0
        },
        "schedules": [],
        "retentionPolicy": {
            "daysToKeep": 30,
            "releasesToKeep": 3,
            "retainBuild": true
        },
        "processParameters": {
            "dataSourceBindings": [{
                "dataSourceName": "AzureRMWebAppNamesByType",
                "parameters": {
                    "WebAppKind": "$(WebAppKind)"
                },
                "endpointId": "$(ConnectedServiceName)",
                "target": "WebAppName"
            }]
        },
        "properties": {},
        "preDeploymentGates": {
            "id": 0,
            "gatesOptions": null,
            "gates": []
        },
        "postDeploymentGates": {
            "id": 0,
            "gatesOptions": null,
            "gates": []
        },
        "badgeUrl": "https://sampleuser.vsrm.visualstudio.com/_apis/public/Release/badge/19749ef3-2f42-49b5-9696-f28b49faebcb/1/2"
    }],
    "artifacts": [{
        "sourceId": "19749ef3-2f42-49b5-9696-f28b49faebcb:a6c88f30-5e1f-4de8-b24d-279bb209d85f",
        "type": "Git",
        "alias": "Dev",
        "definitionReference": {
            "branches": {
                "id": "adf_publish",
                "name": "adf_publish"
            },
            "checkoutSubmodules": {
                "id": "",
                "name": ""
            },
            "defaultVersionSpecific": {
                "id": "",
                "name": ""
            },
            "defaultVersionType": {
                "id": "latestFromBranchType",
                "name": "Latest from default branch"
            },
            "definition": {
                "id": "a6c88f30-5e1f-4de8-b24d-279bb209d85f",
                "name": "Dev"
            },
            "fetchDepth": {
                "id": "",
                "name": ""
            },
            "gitLfsSupport": {
                "id": "",
                "name": ""
            },
            "project": {
                "id": "19749ef3-2f42-49b5-9696-f28b49faebcb",
                "name": "Prod"
            }
        },
        "isPrimary": true
    }],
    "triggers": [{
        "schedule": {
            "jobId": "b5ef09b6-8dfd-4b91-8b48-0709e3e67b2d",
            "timeZoneId": "UTC",
            "startHours": 3,
            "startMinutes": 0,
            "daysToRelease": 31
        },
        "triggerType": 2
    }],
    "releaseNameFormat": "Release-$(rev:r)",
    "url": "https://sampleuser.vsrm.visualstudio.com/19749ef3-2f42-49b5-9696-f28b49faebcb/_apis/Release/definitions/1",
    "_links": {
        "self": {
            "href": "https://sampleuser.vsrm.visualstudio.com/19749ef3-2f42-49b5-9696-f28b49faebcb/_apis/Release/definitions/1"
        },
        "web": {
            "href": "https://sampleuser.visualstudio.com/19749ef3-2f42-49b5-9696-f28b49faebcb/_release?definitionId=1"
        }
    },
    "tags": [],
    "properties": {
        "DefinitionCreationSource": {
            "$type": "System.String",
            "$value": "ReleaseNew"
        }
    }
}
```

## <a name="sample-script-to-stop-and-restart-triggers-and-clean-up"></a><span data-ttu-id="c8b8a-198">Sample script to stop and restart triggers and clean up</span><span class="sxs-lookup"><span data-stu-id="c8b8a-198">Sample script to stop and restart triggers and clean up</span></span>

<span data-ttu-id="c8b8a-199">Here is a sample script to stop triggers before deployment and to restart triggers afterwards.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-199">Here is a sample script to stop triggers before deployment and to restart triggers afterwards.</span></span> <span data-ttu-id="c8b8a-200">The script also includes code to delete resources that have been removed.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-200">The script also includes code to delete resources that have been removed.</span></span>

```powershell
param
(
    [parameter(Mandatory = $false)] [String] $rootFolder="$(env:System.DefaultWorkingDirectory)/Dev/",
    [parameter(Mandatory = $false)] [String] $armTemplate="$rootFolder\arm_template.json",
    [parameter(Mandatory = $false)] [String] $ResourceGroupName="sampleuser-datafactory",
    [parameter(Mandatory = $false)] [String] $DataFactoryName="sampleuserdemo2",
    [parameter(Mandatory = $false)] [Bool] $predeployment=$true

)


$templateJson = Get-Content $armTemplate | ConvertFrom-Json
$resources = $templateJson.resources

#Triggers 
Write-Host "Getting triggers"
$triggersADF = Get-AzureRmDataFactoryV2Trigger -DataFactoryName $DataFactoryName -ResourceGroupName $ResourceGroupName
$triggersTemplate = $resources | Where-Object { $_.type -eq "Microsoft.DataFactory/factories/triggers" }
$triggerNames = $triggersTemplate | ForEach-Object {$_.name.Substring(37, $_.name.Length-40)}
$activeTriggerNames = $triggersTemplate | Where-Object { $_.properties.runtimeState -eq "Started" -and $_.properties.pipelines.Count -gt 0} | ForEach-Object {$_.name.Substring(37, $_.name.Length-40)}
$deletedtriggers = $triggersADF | Where-Object { $triggerNames -notcontains $_.Name }
$triggerstostop = $triggerNames | where { ($triggersADF | Select-Object name).name -contains $_ }

if ($predeployment -eq $true) {
    #Stop all triggers
    Write-Host "Stopping deployed triggers"
    $triggerstostop | ForEach-Object { Stop-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name $_ -Force }
}
else {

    #start Active triggers
    Write-Host "Starting active triggers"
    $activeTriggerNames | ForEach-Object { Start-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name $_ -Force }

    #Deleted resources
    #pipelines
    Write-Host "Getting pipelines"
    $pipelinesADF = Get-AzureRmDataFactoryV2Pipeline -DataFactoryName $DataFactoryName -ResourceGroupName $ResourceGroupName
    $pipelinesTemplate = $resources | Where-Object { $_.type -eq "Microsoft.DataFactory/factories/pipelines" }
    $pipelinesNames = $pipelinesTemplate | ForEach-Object {$_.name.Substring(37, $_.name.Length-40)}
    $deletedpipelines = $pipelinesADF | Where-Object { $pipelinesNames -notcontains $_.Name }
    #datasets
    Write-Host "Getting datasets"
    $datasetsADF = Get-AzureRmDataFactoryV2Dataset -DataFactoryName $DataFactoryName -ResourceGroupName $ResourceGroupName
    $datasetsTemplate = $resources | Where-Object { $_.type -eq "Microsoft.DataFactory/factories/datasets" }
    $datasetsNames = $datasetsTemplate | ForEach-Object {$_.name.Substring(37, $_.name.Length-40) }
    $deleteddataset = $datasetsADF | Where-Object { $datasetsNames -notcontains $_.Name }
    #linkedservices
    Write-Host "Getting linked services"
    $linkedservicesADF = Get-AzureRmDataFactoryV2LinkedService -DataFactoryName $DataFactoryName -ResourceGroupName $ResourceGroupName
    $linkedservicesTemplate = $resources | Where-Object { $_.type -eq "Microsoft.DataFactory/factories/linkedservices" }
    $linkedservicesNames = $linkedservicesTemplate | ForEach-Object {$_.name.Substring(37, $_.name.Length-40)}
    $deletedlinkedservices = $linkedservicesADF | Where-Object { $linkedservicesNames -notcontains $_.Name }
    #Integrationruntimes
    Write-Host "Getting integration runtimes"
    $integrationruntimesADF = Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -ResourceGroupName $ResourceGroupName
    $integrationruntimesTemplate = $resources | Where-Object { $_.type -eq "Microsoft.DataFactory/factories/integrationruntimes" }
    $integrationruntimesNames = $integrationruntimesTemplate | ForEach-Object {$_.name.Substring(37, $_.name.Length-40)}
    $deletedintegrationruntimes = $integrationruntimesADF | Where-Object { $integrationruntimesNames -notcontains $_.Name }

    #delte resources
    Write-Host "Deleting triggers"
    $deletedtriggers | ForEach-Object { Remove-AzureRmDataFactoryV2Trigger -Name $_.Name -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Force }
    Write-Host "Deleting pipelines"
    $deletedpipelines | ForEach-Object { Remove-AzureRmDataFactoryV2Pipeline -Name $_.Name -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Force }
    Write-Host "Deleting datasets"
    $deleteddataset | ForEach-Object { Remove-AzureRmDataFactoryV2Dataset -Name $_.Name -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Force }
    Write-Host "Deleting linked services"
    $deletedlinkedservices | ForEach-Object { Remove-AzureRmDataFactoryV2LinkedService -Name $_.Name -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Force }
    Write-Host "Deleting integration runtimes"
    $deletedintegrationruntimes | ForEach-Object { Remove-AzureRmDataFactoryV2IntegrationRuntime -Name $_.Name -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Force }
}
```

## <a name="use-custom-parameters-with-the-resource-manager-template"></a><span data-ttu-id="c8b8a-201">Use custom parameters with the Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="c8b8a-201">Use custom parameters with the Resource Manager template</span></span>

<span data-ttu-id="c8b8a-202">You can define custom parameters for the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-202">You can define custom parameters for the Resource Manager template.</span></span> <span data-ttu-id="c8b8a-203">You simply need to have a file named `arm-template-parameters-definition.json` in the root folder of the repository.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-203">You simply need to have a file named `arm-template-parameters-definition.json` in the root folder of the repository.</span></span> <span data-ttu-id="c8b8a-204">(The file name must match the name shown here exactly.) Data Factory tries to read the file from whichever branch you are currently working in, not just from the collaboration branch.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-204">(The file name must match the name shown here exactly.) Data Factory tries to read the file from whichever branch you are currently working in, not just from the collaboration branch.</span></span> <span data-ttu-id="c8b8a-205">If no file is found, Data Factory uses the default definitions.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-205">If no file is found, Data Factory uses the default definitions.</span></span>

<span data-ttu-id="c8b8a-206">The following example shows a sample parameters file.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-206">The following example shows a sample parameters file.</span></span> <span data-ttu-id="c8b8a-207">Use this sample as a reference to create your own custom parameters file.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-207">Use this sample as a reference to create your own custom parameters file.</span></span> <span data-ttu-id="c8b8a-208">If the file you provide is not in the proper JSON format, Data Factory outputs an error message in the browser console and reverts to the default definitions shown in the Data Factory UI.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-208">If the file you provide is not in the proper JSON format, Data Factory outputs an error message in the browser console and reverts to the default definitions shown in the Data Factory UI.</span></span>

```json
{
    "Microsoft.DataFactory/factories/pipelines": {},
    "Microsoft.DataFactory/factories/integrationRuntimes": {
        "properties": {
            "typeProperties": {
                "ssisProperties": {
                    "catalogInfo": {
                        "catalogServerEndpoint": "=",
                        "catalogAdminUserName": "=",
                        "catalogAdminPassword": {
                            "value": "-::secureString"
                        }
                    },
                    "customSetupScriptProperties": {
                        "sasToken": {
                            "value": "-::secureString"
                        }
                    }
                },
                "linkedInfo": {
                    "key": {
                        "value": "-::secureString"
                    }
                }
            }
        }
    },
    "Microsoft.DataFactory/factories/triggers": {
        "properties": {
            "pipelines": [{
                    "parameters": {
                        "*": "="
                    }
                },
                "pipelineReference.referenceName"
            ],
            "pipeline": {
                "parameters": {
                    "*": "="
                }
            }
        }
    },
    "Microsoft.DataFactory/factories/linkedServices": {
        "*": {
            "properties": {
                "typeProperties": {
                    "accountName": "=",
                    "username": "=",
                    "userName": "=",
                    "accessKeyId": "=",
                    "servicePrincipalId": "=",
                    "userId": "=",
                    "clientId": "=",
                    "clusterUserName": "=",
                    "clusterSshUserName": "=",
                    "hostSubscriptionId": "=",
                    "clusterResourceGroup": "=",
                    "subscriptionId": "=",
                    "resourceGroupName": "=",
                    "tenant": "=",
                    "dataLakeStoreUri": "=",
                    "baseUrl": "=",
                    "connectionString": "|:-connectionString:secureString"
                }
            }
        }
    },
    "Microsoft.DataFactory/factories/datasets": {
        "*": {
            "properties": {
                "typeProperties": {
                    "folderPath": "=",
                    "fileName": "="
                }
            }
        }
    }
}
```
