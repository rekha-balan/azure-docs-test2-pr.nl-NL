---
title: Continuous integration in VS Team Services using Azure Resource Group projects | Microsoft Docs
description: Describes how to set up continuous integration in Visual Studio Team Services by using Azure Resource Group deployment projects in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: ''
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 94cb10ad2fd1edc517ccdab5a07b8e7d1917f701
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555997"
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a><span data-ttu-id="ab86e-103">Continuous integration in Visual Studio Team Services using Azure Resource Group deployment projects</span><span class="sxs-lookup"><span data-stu-id="ab86e-103">Continuous integration in Visual Studio Team Services using Azure Resource Group deployment projects</span></span>
<span data-ttu-id="ab86e-104">To deploy an Azure template, you need to perform tasks to go through the various stages: Build, Test, Copy to Azure (also called "Staging"), and Deploy Template.</span><span class="sxs-lookup"><span data-stu-id="ab86e-104">To deploy an Azure template, you need to perform tasks to go through the various stages: Build, Test, Copy to Azure (also called "Staging"), and Deploy Template.</span></span>  <span data-ttu-id="ab86e-105">There are two different ways to deploy templates Visual Studio Team Services (VS Team Services).</span><span class="sxs-lookup"><span data-stu-id="ab86e-105">There are two different ways to deploy templates Visual Studio Team Services (VS Team Services).</span></span> <span data-ttu-id="ab86e-106">Both methods provide the same results, so choose the one that best fits your workflow.</span><span class="sxs-lookup"><span data-stu-id="ab86e-106">Both methods provide the same results, so choose the one that best fits your workflow.</span></span>

1. <span data-ttu-id="ab86e-107">Add a single step to your build definition that runs the PowerShell script that’s included in the Azure Resource Group deployment project (Deploy-AzureResourceGroup.ps1).</span><span class="sxs-lookup"><span data-stu-id="ab86e-107">Add a single step to your build definition that runs the PowerShell script that’s included in the Azure Resource Group deployment project (Deploy-AzureResourceGroup.ps1).</span></span> <span data-ttu-id="ab86e-108">The script copies artifacts and then deploys the template.</span><span class="sxs-lookup"><span data-stu-id="ab86e-108">The script copies artifacts and then deploys the template.</span></span>
2. <span data-ttu-id="ab86e-109">Add multiple VS Team Services build steps, each one performing a stage task.</span><span class="sxs-lookup"><span data-stu-id="ab86e-109">Add multiple VS Team Services build steps, each one performing a stage task.</span></span>

<span data-ttu-id="ab86e-110">This article demonstrates both options.</span><span class="sxs-lookup"><span data-stu-id="ab86e-110">This article demonstrates both options.</span></span>  <span data-ttu-id="ab86e-111">The first option has the advantage of using the same script used by developers in Visual Studio providing consistency throughout the lifecycle.</span><span class="sxs-lookup"><span data-stu-id="ab86e-111">The first option has the advantage of using the same script used by developers in Visual Studio providing consistency throughout the lifecycle.</span></span>  <span data-ttu-id="ab86e-112">The second option offers a convenient alternative to the built in script.</span><span class="sxs-lookup"><span data-stu-id="ab86e-112">The second option offers a convenient alternative to the built in script.</span></span>  <span data-ttu-id="ab86e-113">Both procedures assume you already have a Visual Studio deployment project checked into VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="ab86e-113">Both procedures assume you already have a Visual Studio deployment project checked into VS Team Services.</span></span>

## <a name="copy-artifacts-to-azure"></a><span data-ttu-id="ab86e-114">Copy artifacts to Azure</span><span class="sxs-lookup"><span data-stu-id="ab86e-114">Copy artifacts to Azure</span></span>
<span data-ttu-id="ab86e-115">Regardless of the scenario, if you have any artifacts that are needed for template deployment, you need to give Azure Resource Manager access to them.</span><span class="sxs-lookup"><span data-stu-id="ab86e-115">Regardless of the scenario, if you have any artifacts that are needed for template deployment, you need to give Azure Resource Manager access to them.</span></span> <span data-ttu-id="ab86e-116">These artifacts can include files such as:</span><span class="sxs-lookup"><span data-stu-id="ab86e-116">These artifacts can include files such as:</span></span>

* <span data-ttu-id="ab86e-117">Nested templates</span><span class="sxs-lookup"><span data-stu-id="ab86e-117">Nested templates</span></span>
* <span data-ttu-id="ab86e-118">Configuration scripts and DSC scripts</span><span class="sxs-lookup"><span data-stu-id="ab86e-118">Configuration scripts and DSC scripts</span></span>
* <span data-ttu-id="ab86e-119">Application binaries</span><span class="sxs-lookup"><span data-stu-id="ab86e-119">Application binaries</span></span>

### <a name="nested-templates-and-configuration-scripts"></a><span data-ttu-id="ab86e-120">Nested Templates and Configuration Scripts</span><span class="sxs-lookup"><span data-stu-id="ab86e-120">Nested Templates and Configuration Scripts</span></span>
<span data-ttu-id="ab86e-121">When you use the templates provided by Visual Studio (or built with Visual Studio snippets), the PowerShell script not only stages the artifacts, it also parameterizes the URI for the resources for different deployments.</span><span class="sxs-lookup"><span data-stu-id="ab86e-121">When you use the templates provided by Visual Studio (or built with Visual Studio snippets), the PowerShell script not only stages the artifacts, it also parameterizes the URI for the resources for different deployments.</span></span> <span data-ttu-id="ab86e-122">The script then copies the artifacts to a secure container in Azure, creates a SaS token for that container, and then passes that information on to the template deployment.</span><span class="sxs-lookup"><span data-stu-id="ab86e-122">The script then copies the artifacts to a secure container in Azure, creates a SaS token for that container, and then passes that information on to the template deployment.</span></span> <span data-ttu-id="ab86e-123">See [Create a template deployment](https://msdn.microsoft.com/library/azure/dn790564.aspx) to learn more about nested templates.</span><span class="sxs-lookup"><span data-stu-id="ab86e-123">See [Create a template deployment](https://msdn.microsoft.com/library/azure/dn790564.aspx) to learn more about nested templates.</span></span>  <span data-ttu-id="ab86e-124">When using tasks in VS Team Services, you need to select the appropriate tasks for your template deployment and if necessary pass parameter values from the staging step to the template deployment.</span><span class="sxs-lookup"><span data-stu-id="ab86e-124">When using tasks in VS Team Services, you need to select the appropriate tasks for your template deployment and if necessary pass parameter values from the staging step to the template deployment.</span></span>

## <a name="set-up-continuous-deployment-in-vs-team-services"></a><span data-ttu-id="ab86e-125">Set up continuous deployment in VS Team Services</span><span class="sxs-lookup"><span data-stu-id="ab86e-125">Set up continuous deployment in VS Team Services</span></span>
<span data-ttu-id="ab86e-126">To call the PowerShell script in VS Team Services, you need to update your build definition.</span><span class="sxs-lookup"><span data-stu-id="ab86e-126">To call the PowerShell script in VS Team Services, you need to update your build definition.</span></span> <span data-ttu-id="ab86e-127">In brief, the steps are:</span><span class="sxs-lookup"><span data-stu-id="ab86e-127">In brief, the steps are:</span></span> 

1. <span data-ttu-id="ab86e-128">Edit the build definition.</span><span class="sxs-lookup"><span data-stu-id="ab86e-128">Edit the build definition.</span></span>
2. <span data-ttu-id="ab86e-129">Set up Azure authorization in VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="ab86e-129">Set up Azure authorization in VS Team Services.</span></span>
3. <span data-ttu-id="ab86e-130">Add an Azure PowerShell build step that references the PowerShell script in the Azure Resource Group deployment project.</span><span class="sxs-lookup"><span data-stu-id="ab86e-130">Add an Azure PowerShell build step that references the PowerShell script in the Azure Resource Group deployment project.</span></span>
4. <span data-ttu-id="ab86e-131">Set the value of the *-ArtifactsStagingDirectory* parameter to work with a project built in VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="ab86e-131">Set the value of the *-ArtifactsStagingDirectory* parameter to work with a project built in VS Team Services.</span></span>

### <a name="detailed-walkthrough-for-option-1"></a><span data-ttu-id="ab86e-132">Detailed walkthrough for Option 1</span><span class="sxs-lookup"><span data-stu-id="ab86e-132">Detailed walkthrough for Option 1</span></span>
<span data-ttu-id="ab86e-133">The following steps walk you through the steps necessary to configure continuous deployment in VS Team Services using a single task that runs the PowerShell script in your project.</span><span class="sxs-lookup"><span data-stu-id="ab86e-133">The following steps walk you through the steps necessary to configure continuous deployment in VS Team Services using a single task that runs the PowerShell script in your project.</span></span> 

1. <span data-ttu-id="ab86e-134">Edit your VS Team Services build definition and add an Azure PowerShell build step.</span><span class="sxs-lookup"><span data-stu-id="ab86e-134">Edit your VS Team Services build definition and add an Azure PowerShell build step.</span></span> <span data-ttu-id="ab86e-135">Choose the build definition under the **Build definitions** category and then choose the **Edit** link.</span><span class="sxs-lookup"><span data-stu-id="ab86e-135">Choose the build definition under the **Build definitions** category and then choose the **Edit** link.</span></span>
   
   ![Edit build definition][0]
2. <span data-ttu-id="ab86e-137">Add a new **Azure PowerShell** build step to the build definition and then choose the **Add build step…**</span><span class="sxs-lookup"><span data-stu-id="ab86e-137">Add a new **Azure PowerShell** build step to the build definition and then choose the **Add build step…**</span></span> <span data-ttu-id="ab86e-138">button.</span><span class="sxs-lookup"><span data-stu-id="ab86e-138">button.</span></span>
   
   ![Add build step][1]
3. <span data-ttu-id="ab86e-140">Choose the **Deploy task** category, select the **Azure PowerShell** task, and then choose its **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ab86e-140">Choose the **Deploy task** category, select the **Azure PowerShell** task, and then choose its **Add** button.</span></span>
   
   ![Add tasks][2]
4. <span data-ttu-id="ab86e-142">Choose the **Azure PowerShell** build step and then fill in its values.</span><span class="sxs-lookup"><span data-stu-id="ab86e-142">Choose the **Azure PowerShell** build step and then fill in its values.</span></span>
   
   1. <span data-ttu-id="ab86e-143">If you already have an Azure service endpoint added to VS Team Services, choose the subscription in the **Azure Subscription** drop down list box and then skip to the next section.</span><span class="sxs-lookup"><span data-stu-id="ab86e-143">If you already have an Azure service endpoint added to VS Team Services, choose the subscription in the **Azure Subscription** drop down list box and then skip to the next section.</span></span> 
      
      <span data-ttu-id="ab86e-144">If you don’t have an Azure service endpoint in VS Team Services, you need to add one.</span><span class="sxs-lookup"><span data-stu-id="ab86e-144">If you don’t have an Azure service endpoint in VS Team Services, you need to add one.</span></span> <span data-ttu-id="ab86e-145">This subsection takes you through the process.</span><span class="sxs-lookup"><span data-stu-id="ab86e-145">This subsection takes you through the process.</span></span> <span data-ttu-id="ab86e-146">If your Azure account uses a Microsoft account (such as Hotmail), you need to take the following steps to get a Service Principal authentication.</span><span class="sxs-lookup"><span data-stu-id="ab86e-146">If your Azure account uses a Microsoft account (such as Hotmail), you need to take the following steps to get a Service Principal authentication.</span></span>
   2. <span data-ttu-id="ab86e-147">Choose the **Manage** link next to the **Azure Subscription** drop down list box.</span><span class="sxs-lookup"><span data-stu-id="ab86e-147">Choose the **Manage** link next to the **Azure Subscription** drop down list box.</span></span>
      
      ![Manage Azure subscriptions][3]
   3. <span data-ttu-id="ab86e-149">Choose **Azure** in the **New Service Endpoint** drop down list box.</span><span class="sxs-lookup"><span data-stu-id="ab86e-149">Choose **Azure** in the **New Service Endpoint** drop down list box.</span></span>
      
      ![New service endpoint][4]
   4. <span data-ttu-id="ab86e-151">In the **Add Azure Subscription** dialog box, select the **Service Principal** option.</span><span class="sxs-lookup"><span data-stu-id="ab86e-151">In the **Add Azure Subscription** dialog box, select the **Service Principal** option.</span></span>
      
      ![Service principal option][5]
   5. <span data-ttu-id="ab86e-153">Add your Azure subscription information to the **Add Azure Subscription** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ab86e-153">Add your Azure subscription information to the **Add Azure Subscription** dialog box.</span></span> <span data-ttu-id="ab86e-154">You need to provide the following items:</span><span class="sxs-lookup"><span data-stu-id="ab86e-154">You need to provide the following items:</span></span>
      
      * <span data-ttu-id="ab86e-155">Subscription Id</span><span class="sxs-lookup"><span data-stu-id="ab86e-155">Subscription Id</span></span>
      * <span data-ttu-id="ab86e-156">Subscription Name</span><span class="sxs-lookup"><span data-stu-id="ab86e-156">Subscription Name</span></span>
      * <span data-ttu-id="ab86e-157">Service Principal Id</span><span class="sxs-lookup"><span data-stu-id="ab86e-157">Service Principal Id</span></span>
      * <span data-ttu-id="ab86e-158">Service Principal Key</span><span class="sxs-lookup"><span data-stu-id="ab86e-158">Service Principal Key</span></span>
      * <span data-ttu-id="ab86e-159">Tenant Id</span><span class="sxs-lookup"><span data-stu-id="ab86e-159">Tenant Id</span></span>
   6. <span data-ttu-id="ab86e-160">Add a name of your choice to the **Subscription** name box.</span><span class="sxs-lookup"><span data-stu-id="ab86e-160">Add a name of your choice to the **Subscription** name box.</span></span> <span data-ttu-id="ab86e-161">This value appears later in the **Azure Subscription** drop down list in VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="ab86e-161">This value appears later in the **Azure Subscription** drop down list in VS Team Services.</span></span> 
   7. <span data-ttu-id="ab86e-162">If you don’t know your Azure subscription ID, you can use one of the following commands to retrieve it.</span><span class="sxs-lookup"><span data-stu-id="ab86e-162">If you don’t know your Azure subscription ID, you can use one of the following commands to retrieve it.</span></span>
      
      <span data-ttu-id="ab86e-163">For PowerShell scripts, use:</span><span class="sxs-lookup"><span data-stu-id="ab86e-163">For PowerShell scripts, use:</span></span>
      
      `Get-AzureRmSubscription`
      
      <span data-ttu-id="ab86e-164">For Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="ab86e-164">For Azure CLI, use:</span></span>
      
      `azure account show`
   8. <span data-ttu-id="ab86e-165">To get a Service Principal ID, Service Principal Key, and Tenant ID, follow the procedure in [Create Active Directory application and service principal using portal](resource-group-create-service-principal-portal.md) or [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="ab86e-165">To get a Service Principal ID, Service Principal Key, and Tenant ID, follow the procedure in [Create Active Directory application and service principal using portal](resource-group-create-service-principal-portal.md) or [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal.md).</span></span>
   9. <span data-ttu-id="ab86e-166">Add the Service Principal ID, Service Principal Key, and Tenant ID values to the **Add Azure Subscription** dialog box and then choose the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="ab86e-166">Add the Service Principal ID, Service Principal Key, and Tenant ID values to the **Add Azure Subscription** dialog box and then choose the **OK** button.</span></span>
      
      <span data-ttu-id="ab86e-167">You now have a valid Service Principal to use to run the Azure PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="ab86e-167">You now have a valid Service Principal to use to run the Azure PowerShell script.</span></span>
5. <span data-ttu-id="ab86e-168">Edit the build definition and choose the **Azure PowerShell** build step.</span><span class="sxs-lookup"><span data-stu-id="ab86e-168">Edit the build definition and choose the **Azure PowerShell** build step.</span></span> <span data-ttu-id="ab86e-169">Select the subscription in the **Azure Subscription** drop down list box.</span><span class="sxs-lookup"><span data-stu-id="ab86e-169">Select the subscription in the **Azure Subscription** drop down list box.</span></span> <span data-ttu-id="ab86e-170">(If the subscription doesn't appear, choose the **Refresh** button next the **Manage** link.)</span><span class="sxs-lookup"><span data-stu-id="ab86e-170">(If the subscription doesn't appear, choose the **Refresh** button next the **Manage** link.)</span></span> 
   
   ![Configure Azure PowerShell build task][8]
6. <span data-ttu-id="ab86e-172">Provide a path to the Deploy-AzureResourceGroup.ps1 PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="ab86e-172">Provide a path to the Deploy-AzureResourceGroup.ps1 PowerShell script.</span></span> <span data-ttu-id="ab86e-173">To do this, choose the ellipsis (…) button next to the **Script Path** box, navigate to the Deploy-AzureResourceGroup.ps1 PowerShell script in the **Scripts** folder of your project, select it, and then choose the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="ab86e-173">To do this, choose the ellipsis (…) button next to the **Script Path** box, navigate to the Deploy-AzureResourceGroup.ps1 PowerShell script in the **Scripts** folder of your project, select it, and then choose the **OK** button.</span></span>    
   
   ![Select path to script][9]
7. <span data-ttu-id="ab86e-175">After you select the script, update the path to the script so that it’s run from the Build.StagingDirectory (the same directory that *ArtifactsLocation* is set to).</span><span class="sxs-lookup"><span data-stu-id="ab86e-175">After you select the script, update the path to the script so that it’s run from the Build.StagingDirectory (the same directory that *ArtifactsLocation* is set to).</span></span> <span data-ttu-id="ab86e-176">You can do this by adding “$(Build.StagingDirectory)/” to the beginning of the script path.</span><span class="sxs-lookup"><span data-stu-id="ab86e-176">You can do this by adding “$(Build.StagingDirectory)/” to the beginning of the script path.</span></span>
   
    ![Edit path to script][10]
8. <span data-ttu-id="ab86e-178">In the **Script Arguments** box, enter the following parameters (in a single line).</span><span class="sxs-lookup"><span data-stu-id="ab86e-178">In the **Script Arguments** box, enter the following parameters (in a single line).</span></span> <span data-ttu-id="ab86e-179">When you run the script in Visual Studio, you can see how VS uses the parameters in the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="ab86e-179">When you run the script in Visual Studio, you can see how VS uses the parameters in the **Output** window.</span></span> <span data-ttu-id="ab86e-180">You can use this as a starting point for setting the parameter values in your build step.</span><span class="sxs-lookup"><span data-stu-id="ab86e-180">You can use this as a starting point for setting the parameter values in your build step.</span></span>
   
   | <span data-ttu-id="ab86e-181">Parameter</span><span class="sxs-lookup"><span data-stu-id="ab86e-181">Parameter</span></span> | <span data-ttu-id="ab86e-182">Description</span><span class="sxs-lookup"><span data-stu-id="ab86e-182">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="ab86e-183">-ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="ab86e-183">-ResourceGroupLocation</span></span> |<span data-ttu-id="ab86e-184">The geo-location value where the resource group is located, such as **eastus** or **'East US'**.</span><span class="sxs-lookup"><span data-stu-id="ab86e-184">The geo-location value where the resource group is located, such as **eastus** or **'East US'**.</span></span> <span data-ttu-id="ab86e-185">(Add single quotes if there's a space in the name.) See [Azure Regions](https://azure.microsoft.com/en-us/regions/) for more information.</span><span class="sxs-lookup"><span data-stu-id="ab86e-185">(Add single quotes if there's a space in the name.) See [Azure Regions](https://azure.microsoft.com/en-us/regions/) for more information.</span></span> |
   | <span data-ttu-id="ab86e-186">-ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ab86e-186">-ResourceGroupName</span></span> |<span data-ttu-id="ab86e-187">The name of the resource group used for this deployment.</span><span class="sxs-lookup"><span data-stu-id="ab86e-187">The name of the resource group used for this deployment.</span></span> |
   | <span data-ttu-id="ab86e-188">-UploadArtifacts</span><span class="sxs-lookup"><span data-stu-id="ab86e-188">-UploadArtifacts</span></span> |<span data-ttu-id="ab86e-189">This parameter, when present, specifies that artifacts need to be uploaded to Azure from the local system.</span><span class="sxs-lookup"><span data-stu-id="ab86e-189">This parameter, when present, specifies that artifacts need to be uploaded to Azure from the local system.</span></span> <span data-ttu-id="ab86e-190">You only need to set this switch if your template deployment requires extra artifacts that you want to stage using the PowerShell script (such as configuration scripts or nested templates).</span><span class="sxs-lookup"><span data-stu-id="ab86e-190">You only need to set this switch if your template deployment requires extra artifacts that you want to stage using the PowerShell script (such as configuration scripts or nested templates).</span></span> |
   | <span data-ttu-id="ab86e-191">-StorageAccountName</span><span class="sxs-lookup"><span data-stu-id="ab86e-191">-StorageAccountName</span></span> |<span data-ttu-id="ab86e-192">The name of the storage account used to stage artifacts for this deployment.</span><span class="sxs-lookup"><span data-stu-id="ab86e-192">The name of the storage account used to stage artifacts for this deployment.</span></span>  <span data-ttu-id="ab86e-193">This parameter is only used if you are staging artifacts for deployment.</span><span class="sxs-lookup"><span data-stu-id="ab86e-193">This parameter is only used if you are staging artifacts for deployment.</span></span> <span data-ttu-id="ab86e-194">If this parameter is supplied, a new storage account is created if the script has not created one during a previous deployment.</span><span class="sxs-lookup"><span data-stu-id="ab86e-194">If this parameter is supplied, a new storage account is created if the script has not created one during a previous deployment.</span></span>  <span data-ttu-id="ab86e-195">If the parameter is specified, the storage account must already exist.</span><span class="sxs-lookup"><span data-stu-id="ab86e-195">If the parameter is specified, the storage account must already exist.</span></span> |
   | <span data-ttu-id="ab86e-196">-StorageAccountResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ab86e-196">-StorageAccountResourceGroupName</span></span> |<span data-ttu-id="ab86e-197">The name of the resource group associated with the storage account.</span><span class="sxs-lookup"><span data-stu-id="ab86e-197">The name of the resource group associated with the storage account.</span></span> <span data-ttu-id="ab86e-198">This parameter is required only if you provide a value for the StorageAccountName parameter.</span><span class="sxs-lookup"><span data-stu-id="ab86e-198">This parameter is required only if you provide a value for the StorageAccountName parameter.</span></span> |
   | <span data-ttu-id="ab86e-199">-TemplateFile</span><span class="sxs-lookup"><span data-stu-id="ab86e-199">-TemplateFile</span></span> |<span data-ttu-id="ab86e-200">The path to the template file in the Azure Resource Group deployment project.</span><span class="sxs-lookup"><span data-stu-id="ab86e-200">The path to the template file in the Azure Resource Group deployment project.</span></span> <span data-ttu-id="ab86e-201">To enhance flexibility, use a path for this parameter that is relative to the location of the PowerShell script instead of an absolute path.</span><span class="sxs-lookup"><span data-stu-id="ab86e-201">To enhance flexibility, use a path for this parameter that is relative to the location of the PowerShell script instead of an absolute path.</span></span> |
   | <span data-ttu-id="ab86e-202">-TemplateParametersFile</span><span class="sxs-lookup"><span data-stu-id="ab86e-202">-TemplateParametersFile</span></span> |<span data-ttu-id="ab86e-203">The path to the parameters file in the Azure Resource Group deployment project.</span><span class="sxs-lookup"><span data-stu-id="ab86e-203">The path to the parameters file in the Azure Resource Group deployment project.</span></span> <span data-ttu-id="ab86e-204">To enhance flexibility, use a path for this parameter that is relative to the location of the PowerShell script instead of an absolute path.</span><span class="sxs-lookup"><span data-stu-id="ab86e-204">To enhance flexibility, use a path for this parameter that is relative to the location of the PowerShell script instead of an absolute path.</span></span> |
   | <span data-ttu-id="ab86e-205">-ArtifactStagingDirectory</span><span class="sxs-lookup"><span data-stu-id="ab86e-205">-ArtifactStagingDirectory</span></span> |<span data-ttu-id="ab86e-206">This parameter lets the PowerShell script know the folder from where the project’s binary files should be copied.</span><span class="sxs-lookup"><span data-stu-id="ab86e-206">This parameter lets the PowerShell script know the folder from where the project’s binary files should be copied.</span></span> <span data-ttu-id="ab86e-207">This value overrides the default value used by the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="ab86e-207">This value overrides the default value used by the PowerShell script.</span></span> <span data-ttu-id="ab86e-208">For VS Team Services use, set the value to: -ArtifactStagingDirectory $(Build.StagingDirectory)</span><span class="sxs-lookup"><span data-stu-id="ab86e-208">For VS Team Services use, set the value to: -ArtifactStagingDirectory $(Build.StagingDirectory)</span></span> |
   
   <span data-ttu-id="ab86e-209">Here’s a script arguments example (line broken for readability):</span><span class="sxs-lookup"><span data-stu-id="ab86e-209">Here’s a script arguments example (line broken for readability):</span></span>
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   <span data-ttu-id="ab86e-210">When you’re finished, the **Script Arguments** box should resemble the following list:</span><span class="sxs-lookup"><span data-stu-id="ab86e-210">When you’re finished, the **Script Arguments** box should resemble the following list:</span></span>
   
   ![Script arguments][11]
9. <span data-ttu-id="ab86e-212">After you’ve added all the required items to the Azure PowerShell build step, choose the **Queue** build button to build the project.</span><span class="sxs-lookup"><span data-stu-id="ab86e-212">After you’ve added all the required items to the Azure PowerShell build step, choose the **Queue** build button to build the project.</span></span> <span data-ttu-id="ab86e-213">The **Build** screen shows the output from the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="ab86e-213">The **Build** screen shows the output from the PowerShell script.</span></span>

### <a name="detailed-walkthrough-for-option-2"></a><span data-ttu-id="ab86e-214">Detailed walkthrough for Option 2</span><span class="sxs-lookup"><span data-stu-id="ab86e-214">Detailed walkthrough for Option 2</span></span>
<span data-ttu-id="ab86e-215">The following steps walk you through the steps necessary to configure continuous deployment in VS Team Services using the built-in tasks.</span><span class="sxs-lookup"><span data-stu-id="ab86e-215">The following steps walk you through the steps necessary to configure continuous deployment in VS Team Services using the built-in tasks.</span></span>

1. <span data-ttu-id="ab86e-216">Edit your VS Team Services build definition to add two new build steps.</span><span class="sxs-lookup"><span data-stu-id="ab86e-216">Edit your VS Team Services build definition to add two new build steps.</span></span> <span data-ttu-id="ab86e-217">Choose the build definition under the **Build definitions** category and then choose the **Edit** link.</span><span class="sxs-lookup"><span data-stu-id="ab86e-217">Choose the build definition under the **Build definitions** category and then choose the **Edit** link.</span></span>
   
   ![Edit build defintion][12]
2. <span data-ttu-id="ab86e-219">Add the new build steps to the build definition using the **Add build step…**</span><span class="sxs-lookup"><span data-stu-id="ab86e-219">Add the new build steps to the build definition using the **Add build step…**</span></span> <span data-ttu-id="ab86e-220">button.</span><span class="sxs-lookup"><span data-stu-id="ab86e-220">button.</span></span>
   
   ![Add build step][13]
3. <span data-ttu-id="ab86e-222">Choose the **Deploy** task category, select the **Azure File Copy** task, and then choose its **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ab86e-222">Choose the **Deploy** task category, select the **Azure File Copy** task, and then choose its **Add** button.</span></span>
   
   ![Add Azure File Copy task][14]
4. <span data-ttu-id="ab86e-224">Choose the **Azure Resource Group Deployment** task, then choose its **Add** button and then **Close** the **Task Catalog**.</span><span class="sxs-lookup"><span data-stu-id="ab86e-224">Choose the **Azure Resource Group Deployment** task, then choose its **Add** button and then **Close** the **Task Catalog**.</span></span>
   
   ![Add Azure Resource Group Deployment task][15]
5. <span data-ttu-id="ab86e-226">Choose the **Azure File Copy** task and fill in its values.</span><span class="sxs-lookup"><span data-stu-id="ab86e-226">Choose the **Azure File Copy** task and fill in its values.</span></span>
   
   <span data-ttu-id="ab86e-227">If you already have an Azure service endpoint added to VS Team Services, choose the subscription in the **Azure Subscription** drop down list box.</span><span class="sxs-lookup"><span data-stu-id="ab86e-227">If you already have an Azure service endpoint added to VS Team Services, choose the subscription in the **Azure Subscription** drop down list box.</span></span>  <span data-ttu-id="ab86e-228">If you do not have a subscription see [Option 1](#detailed-walkthrough-for-option-1) for instructions on setting one up in VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="ab86e-228">If you do not have a subscription see [Option 1](#detailed-walkthrough-for-option-1) for instructions on setting one up in VS Team Services.</span></span>
   
   * <span data-ttu-id="ab86e-229">Source - enter **$(Build.StagingDirectory)**</span><span class="sxs-lookup"><span data-stu-id="ab86e-229">Source - enter **$(Build.StagingDirectory)**</span></span>
   * <span data-ttu-id="ab86e-230">Azure Connection Type - select **Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="ab86e-230">Azure Connection Type - select **Azure Resource Manager**</span></span>
   * <span data-ttu-id="ab86e-231">Azure RM Subscription - select the subscription for the storage account you want to use in the **Azure Subscription** drop down list box.</span><span class="sxs-lookup"><span data-stu-id="ab86e-231">Azure RM Subscription - select the subscription for the storage account you want to use in the **Azure Subscription** drop down list box.</span></span> <span data-ttu-id="ab86e-232">If the subscription doesn't appear, choose the **Refresh** button next the **Manage** link.</span><span class="sxs-lookup"><span data-stu-id="ab86e-232">If the subscription doesn't appear, choose the **Refresh** button next the **Manage** link.</span></span>
   * <span data-ttu-id="ab86e-233">Destination Type - select **Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="ab86e-233">Destination Type - select **Azure Blob**</span></span>
   * <span data-ttu-id="ab86e-234">RM Storage Account - select the storage account you would like to use for staging artifacts</span><span class="sxs-lookup"><span data-stu-id="ab86e-234">RM Storage Account - select the storage account you would like to use for staging artifacts</span></span>
   * <span data-ttu-id="ab86e-235">Container Name - enter the name of the container you would like to use for staging, it can be any valid container name but use one dedicated to this build definition</span><span class="sxs-lookup"><span data-stu-id="ab86e-235">Container Name - enter the name of the container you would like to use for staging, it can be any valid container name but use one dedicated to this build definition</span></span>
   
   <span data-ttu-id="ab86e-236">For the output values:</span><span class="sxs-lookup"><span data-stu-id="ab86e-236">For the output values:</span></span>
   
   * <span data-ttu-id="ab86e-237">Storage Container URI - enter **artifactsLocation**</span><span class="sxs-lookup"><span data-stu-id="ab86e-237">Storage Container URI - enter **artifactsLocation**</span></span>
   * <span data-ttu-id="ab86e-238">Storage Container SAS Token - enter **artifactsLocationSasToken**</span><span class="sxs-lookup"><span data-stu-id="ab86e-238">Storage Container SAS Token - enter **artifactsLocationSasToken**</span></span>
   
   ![Configure Azure File Copy task][16]
6. <span data-ttu-id="ab86e-240">Choose the **Azure Resource Group Deployment** build step and then fill in its values.</span><span class="sxs-lookup"><span data-stu-id="ab86e-240">Choose the **Azure Resource Group Deployment** build step and then fill in its values.</span></span>
   
   * <span data-ttu-id="ab86e-241">Azure Connection Type - select **Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="ab86e-241">Azure Connection Type - select **Azure Resource Manager**</span></span>
   * <span data-ttu-id="ab86e-242">Azure RM Subscription - select the subscription for deployment in the **Azure Subscription** drop down list box.</span><span class="sxs-lookup"><span data-stu-id="ab86e-242">Azure RM Subscription - select the subscription for deployment in the **Azure Subscription** drop down list box.</span></span> <span data-ttu-id="ab86e-243">This will usually be the same subscription used in the previous step.</span><span class="sxs-lookup"><span data-stu-id="ab86e-243">This will usually be the same subscription used in the previous step.</span></span>
   * <span data-ttu-id="ab86e-244">Action - select **Create or Update Resource Group**</span><span class="sxs-lookup"><span data-stu-id="ab86e-244">Action - select **Create or Update Resource Group**</span></span>
   * <span data-ttu-id="ab86e-245">Resource Group - select a resource group or enter the name of a new resource group for the deployment</span><span class="sxs-lookup"><span data-stu-id="ab86e-245">Resource Group - select a resource group or enter the name of a new resource group for the deployment</span></span>
   * <span data-ttu-id="ab86e-246">Location - select the location for the resource group</span><span class="sxs-lookup"><span data-stu-id="ab86e-246">Location - select the location for the resource group</span></span>
   * <span data-ttu-id="ab86e-247">Template - enter the path and name of the template to be deployed prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**</span><span class="sxs-lookup"><span data-stu-id="ab86e-247">Template - enter the path and name of the template to be deployed prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**</span></span>
   * <span data-ttu-id="ab86e-248">Template Parameters - enter the path and name of the parameters to be used, prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**</span><span class="sxs-lookup"><span data-stu-id="ab86e-248">Template Parameters - enter the path and name of the parameters to be used, prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**</span></span>
   * <span data-ttu-id="ab86e-249">Override Template Parameters - enter or copy and paste the following code:</span><span class="sxs-lookup"><span data-stu-id="ab86e-249">Override Template Parameters - enter or copy and paste the following code:</span></span>
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Configure Azure Resource Group Deployment Task][17]
7. <span data-ttu-id="ab86e-251">After you’ve added all the required items, save the build definition and choose **Queue new build** at the top.</span><span class="sxs-lookup"><span data-stu-id="ab86e-251">After you’ve added all the required items, save the build definition and choose **Queue new build** at the top.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab86e-252">Next steps</span><span class="sxs-lookup"><span data-stu-id="ab86e-252">Next steps</span></span>
<span data-ttu-id="ab86e-253">Read [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md) to learn more about Azure Resource Manager and Azure resource groups.</span><span class="sxs-lookup"><span data-stu-id="ab86e-253">Read [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md) to learn more about Azure Resource Manager and Azure resource groups.</span></span>

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
















