---
title: Create multi-VM environments and PaaS resources with Azure Resource Manager templates | Microsoft Docs
description: Learn how to create multi-VM environments and PaaS resources in Azure DevTest Labs from an Azure Resource Manager template
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: ''
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: 6823ca3fd45af4c290d7bc4093206808d4ac321e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552329"
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a><span data-ttu-id="11fba-103">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="11fba-103">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>

<span data-ttu-id="11fba-104">The [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) enables you to easily [create and add a VM to a lab](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="11fba-104">The [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) enables you to easily [create and add a VM to a lab](./devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="11fba-105">This works well for creating one VM at a time.</span><span class="sxs-lookup"><span data-stu-id="11fba-105">This works well for creating one VM at a time.</span></span> <span data-ttu-id="11fba-106">However, if the environment contains multiple VMs, each VM has to be individually created.</span><span class="sxs-lookup"><span data-stu-id="11fba-106">However, if the environment contains multiple VMs, each VM has to be individually created.</span></span> <span data-ttu-id="11fba-107">For scenarios such as a multi-tier Web app or a SharePoint farm, a mechanism is needed to allow for the creation of multiple VMs in a single step.</span><span class="sxs-lookup"><span data-stu-id="11fba-107">For scenarios such as a multi-tier Web app or a SharePoint farm, a mechanism is needed to allow for the creation of multiple VMs in a single step.</span></span> <span data-ttu-id="11fba-108">By using Azure Resource Manager templates, you can now define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple VMs in a consistent state.</span><span class="sxs-lookup"><span data-stu-id="11fba-108">By using Azure Resource Manager templates, you can now define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple VMs in a consistent state.</span></span> <span data-ttu-id="11fba-109">This feature provides the following benefits:</span><span class="sxs-lookup"><span data-stu-id="11fba-109">This feature provides the following benefits:</span></span>

- <span data-ttu-id="11fba-110">Azure Resource Manager templates are loaded directly from your source control repository (GitHub or Team Services Git).</span><span class="sxs-lookup"><span data-stu-id="11fba-110">Azure Resource Manager templates are loaded directly from your source control repository (GitHub or Team Services Git).</span></span>
- <span data-ttu-id="11fba-111">Once configured, your users can create an environment by picking an Azure Resource Manager template from the Azure portal as what they can do with other types of [VM bases](./devtest-lab-comparing-vm-base-image-types.md).</span><span class="sxs-lookup"><span data-stu-id="11fba-111">Once configured, your users can create an environment by picking an Azure Resource Manager template from the Azure portal as what they can do with other types of [VM bases](./devtest-lab-comparing-vm-base-image-types.md).</span></span>
- <span data-ttu-id="11fba-112">Azure PaaS resources can be provisioned in an environment from an Azure Resource Manager template in addition to IaasS VMs.</span><span class="sxs-lookup"><span data-stu-id="11fba-112">Azure PaaS resources can be provisioned in an environment from an Azure Resource Manager template in addition to IaasS VMs.</span></span>
- <span data-ttu-id="11fba-113">The cost of environments can be tracked in the lab in addition to individual VMs created by other types of bases.</span><span class="sxs-lookup"><span data-stu-id="11fba-113">The cost of environments can be tracked in the lab in addition to individual VMs created by other types of bases.</span></span>
- <span data-ttu-id="11fba-114">Users have the same VM policy control for environments as what they have for single-lab VMs.</span><span class="sxs-lookup"><span data-stu-id="11fba-114">Users have the same VM policy control for environments as what they have for single-lab VMs.</span></span>

## <a name="configure-azure-resource-manager-template-repositories"></a><span data-ttu-id="11fba-115">Configure Azure Resource Manager template repositories</span><span class="sxs-lookup"><span data-stu-id="11fba-115">Configure Azure Resource Manager template repositories</span></span>

<span data-ttu-id="11fba-116">As one of the best practices with infrastructure-as-code and configuration-as-code, environment templates should be managed in source control.</span><span class="sxs-lookup"><span data-stu-id="11fba-116">As one of the best practices with infrastructure-as-code and configuration-as-code, environment templates should be managed in source control.</span></span> <span data-ttu-id="11fba-117">Azure DevTest Labs follows this practice and loads all Azure Resource Manager templates directly from your GitHub or VSTS Git repositories.</span><span class="sxs-lookup"><span data-stu-id="11fba-117">Azure DevTest Labs follows this practice and loads all Azure Resource Manager templates directly from your GitHub or VSTS Git repositories.</span></span> <span data-ttu-id="11fba-118">There are a couple of rules to organize your Azure Resource Manager templates in a repository:</span><span class="sxs-lookup"><span data-stu-id="11fba-118">There are a couple of rules to organize your Azure Resource Manager templates in a repository:</span></span>

- <span data-ttu-id="11fba-119">The master template file must be named `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="11fba-119">The master template file must be named `azuredeploy.json`.</span></span> 

    ![Key Azure Resource Manager template files](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-environment-from-arm/master-template.png)

- <span data-ttu-id="11fba-121">If you want to use parameter values defined in a parameter file, the parameter file must be named `azuredeploy.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="11fba-121">If you want to use parameter values defined in a parameter file, the parameter file must be named `azuredeploy.parameters.json`.</span></span>
- <span data-ttu-id="11fba-122">Metadata can be defined to specify the template display name and description.</span><span class="sxs-lookup"><span data-stu-id="11fba-122">Metadata can be defined to specify the template display name and description.</span></span> <span data-ttu-id="11fba-123">This metadata must be in a file named `metadata.json`.</span><span class="sxs-lookup"><span data-stu-id="11fba-123">This metadata must be in a file named `metadata.json`.</span></span> <span data-ttu-id="11fba-124">The following example metadata file illustrates how to specify the display name and description:</span><span class="sxs-lookup"><span data-stu-id="11fba-124">The following example metadata file illustrates how to specify the display name and description:</span></span> 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of the template>"
 
}
```

<span data-ttu-id="11fba-125">The following steps guide you through adding a repository to your lab using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="11fba-125">The following steps guide you through adding a repository to your lab using the Azure portal.</span></span> 

1. <span data-ttu-id="11fba-126">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="11fba-126">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="11fba-127">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="11fba-127">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="11fba-128">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="11fba-128">From the list of labs, select the desired lab.</span></span>   
1. <span data-ttu-id="11fba-129">On the lab's blade, select **Configuration and Policies**.</span><span class="sxs-lookup"><span data-stu-id="11fba-129">On the lab's blade, select **Configuration and Policies**.</span></span>

    ![Configuration and policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. <span data-ttu-id="11fba-131">From the **Configuration and Policies** settings list, select **Repositories**.</span><span class="sxs-lookup"><span data-stu-id="11fba-131">From the **Configuration and Policies** settings list, select **Repositories**.</span></span> <span data-ttu-id="11fba-132">The **Repositories** blade lists the repositories that have been added to the lab.</span><span class="sxs-lookup"><span data-stu-id="11fba-132">The **Repositories** blade lists the repositories that have been added to the lab.</span></span> <span data-ttu-id="11fba-133">A repository named `Public Repo` is automatically generated for all labs, and connects to the [DevTest Labs GitHub repo](https://github.com/Azure/azure-devtestlab) that contains several VM artifacts for your use.</span><span class="sxs-lookup"><span data-stu-id="11fba-133">A repository named `Public Repo` is automatically generated for all labs, and connects to the [DevTest Labs GitHub repo](https://github.com/Azure/azure-devtestlab) that contains several VM artifacts for your use.</span></span>

    ![Public repo](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-environment-from-arm/public-repo.png)

1. <span data-ttu-id="11fba-135">Select **Add+** to add your Azure Resource Manager template repository.</span><span class="sxs-lookup"><span data-stu-id="11fba-135">Select **Add+** to add your Azure Resource Manager template repository.</span></span>
1. <span data-ttu-id="11fba-136">When the second **Repositories** blade opens, enter the necessary information as follows:</span><span class="sxs-lookup"><span data-stu-id="11fba-136">When the second **Repositories** blade opens, enter the necessary information as follows:</span></span>
    - <span data-ttu-id="11fba-137">**Name** - Enter the repository name that is used in the lab.</span><span class="sxs-lookup"><span data-stu-id="11fba-137">**Name** - Enter the repository name that is used in the lab.</span></span>
    - <span data-ttu-id="11fba-138">**Git clone URL** - Enter the GIT HTTPS clone URL from GitHub or Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="11fba-138">**Git clone URL** - Enter the GIT HTTPS clone URL from GitHub or Visual Studio Team Services.</span></span>  
    - <span data-ttu-id="11fba-139">**Branch** - Enter the branch name to access your Azure Resource Manager template definitions.</span><span class="sxs-lookup"><span data-stu-id="11fba-139">**Branch** - Enter the branch name to access your Azure Resource Manager template definitions.</span></span> 
    - <span data-ttu-id="11fba-140">**Personal access token** - The personal access token is used to securely access your repository.</span><span class="sxs-lookup"><span data-stu-id="11fba-140">**Personal access token** - The personal access token is used to securely access your repository.</span></span> <span data-ttu-id="11fba-141">To get your token from Visual Studio Team Services, select **&lt;YourName> > My profile > Security > Public access token**.</span><span class="sxs-lookup"><span data-stu-id="11fba-141">To get your token from Visual Studio Team Services, select **&lt;YourName> > My profile > Security > Public access token**.</span></span> <span data-ttu-id="11fba-142">To get your token from GitHub, select your avatar followed by selecting **Settings > Public access token**.</span><span class="sxs-lookup"><span data-stu-id="11fba-142">To get your token from GitHub, select your avatar followed by selecting **Settings > Public access token**.</span></span> 
    - <span data-ttu-id="11fba-143">**Folder paths** - Using one of the two input fields, enter the folder path that starts with a forward slash - / - and is relative to your Git clone URI to either your artifact definitions (first input field) or your Azure Resource Manager template definitions.</span><span class="sxs-lookup"><span data-stu-id="11fba-143">**Folder paths** - Using one of the two input fields, enter the folder path that starts with a forward slash - / - and is relative to your Git clone URI to either your artifact definitions (first input field) or your Azure Resource Manager template definitions.</span></span>   
    
        ![Public repo](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-environment-from-arm/repo-values.png)

1. <span data-ttu-id="11fba-145">Once all the required fields are entered and pass the validation, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="11fba-145">Once all the required fields are entered and pass the validation, select **Save**.</span></span>

<span data-ttu-id="11fba-146">The next section will walk you through creating environments from an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="11fba-146">The next section will walk you through creating environments from an Azure Resource Manager template.</span></span>

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a><span data-ttu-id="11fba-147">Create an environment from an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="11fba-147">Create an environment from an Azure Resource Manager template</span></span>

<span data-ttu-id="11fba-148">Once an Azure Resource Manager template repository has been configured in the lab, your lab users can create an environment using Azure portal with the following steps:</span><span class="sxs-lookup"><span data-stu-id="11fba-148">Once an Azure Resource Manager template repository has been configured in the lab, your lab users can create an environment using Azure portal with the following steps:</span></span>

1. <span data-ttu-id="11fba-149">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="11fba-149">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="11fba-150">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="11fba-150">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="11fba-151">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="11fba-151">From the list of labs, select the desired lab.</span></span>   
1. <span data-ttu-id="11fba-152">On the lab's blade, select **Add+**.</span><span class="sxs-lookup"><span data-stu-id="11fba-152">On the lab's blade, select **Add+**.</span></span>
1. <span data-ttu-id="11fba-153">The **Choose a base** blade displays the base images you can use with the Azure Resource Manager templates listed first.</span><span class="sxs-lookup"><span data-stu-id="11fba-153">The **Choose a base** blade displays the base images you can use with the Azure Resource Manager templates listed first.</span></span> <span data-ttu-id="11fba-154">Select the desired Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="11fba-154">Select the desired Azure Resource Manager template.</span></span>

    ![Choose a base](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. <span data-ttu-id="11fba-156">On the **Add** blade, enter the **Environment name** value.</span><span class="sxs-lookup"><span data-stu-id="11fba-156">On the **Add** blade, enter the **Environment name** value.</span></span> <span data-ttu-id="11fba-157">The environment name is what is displayed to your users in the lab.</span><span class="sxs-lookup"><span data-stu-id="11fba-157">The environment name is what is displayed to your users in the lab.</span></span> <span data-ttu-id="11fba-158">The remaining input fields are defined in the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="11fba-158">The remaining input fields are defined in the Azure Resource Manager template.</span></span> <span data-ttu-id="11fba-159">If default values are defined in the template or the `azuredeploy.parameter.json` file is present, default values are displayed in those input fields.</span><span class="sxs-lookup"><span data-stu-id="11fba-159">If default values are defined in the template or the `azuredeploy.parameter.json` file is present, default values are displayed in those input fields.</span></span> <span data-ttu-id="11fba-160">For parameters of type *secure string*, you can use the secrets stored in the lab’s [personal secret store](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).</span><span class="sxs-lookup"><span data-stu-id="11fba-160">For parameters of type *secure string*, you can use the secrets stored in the lab’s [personal secret store](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).</span></span>

    ![Add blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > <span data-ttu-id="11fba-162">There are several parameter values that - even if specified - are displayed as empty values.</span><span class="sxs-lookup"><span data-stu-id="11fba-162">There are several parameter values that - even if specified - are displayed as empty values.</span></span> <span data-ttu-id="11fba-163">Therefore, if users assign those values to parameters in an Azure Resource Manager template, DevTest Labs does not display the values; instead showing blank input fields where the lab users need to enter a value when creating the environment.</span><span class="sxs-lookup"><span data-stu-id="11fba-163">Therefore, if users assign those values to parameters in an Azure Resource Manager template, DevTest Labs does not display the values; instead showing blank input fields where the lab users need to enter a value when creating the environment.</span></span>
    > 
    > - <span data-ttu-id="11fba-164">GEN-UNIQUE</span><span class="sxs-lookup"><span data-stu-id="11fba-164">GEN-UNIQUE</span></span>
    > - <span data-ttu-id="11fba-165">GEN-UNIQUE-[N]</span><span class="sxs-lookup"><span data-stu-id="11fba-165">GEN-UNIQUE-[N]</span></span>
    > - <span data-ttu-id="11fba-166">GEN-SSH-PUB-KEY</span><span class="sxs-lookup"><span data-stu-id="11fba-166">GEN-SSH-PUB-KEY</span></span>
    > - <span data-ttu-id="11fba-167">GEN-PASSWORD</span><span class="sxs-lookup"><span data-stu-id="11fba-167">GEN-PASSWORD</span></span> 
 
1. <span data-ttu-id="11fba-168">Select **Add** to create the environment.</span><span class="sxs-lookup"><span data-stu-id="11fba-168">Select **Add** to create the environment.</span></span> <span data-ttu-id="11fba-169">The environment starts provisioning immediately with the status displaying in the **My virtual machines** list.</span><span class="sxs-lookup"><span data-stu-id="11fba-169">The environment starts provisioning immediately with the status displaying in the **My virtual machines** list.</span></span> <span data-ttu-id="11fba-170">A new resource group is automatically created by the lab to provision all the resources defined in the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="11fba-170">A new resource group is automatically created by the lab to provision all the resources defined in the Azure Resource Manager template.</span></span>
1. <span data-ttu-id="11fba-171">Once the environment is created, select the environment in **My virtual machines** list to open the resource group blade and browse the resources provisioned in the environment.</span><span class="sxs-lookup"><span data-stu-id="11fba-171">Once the environment is created, select the environment in **My virtual machines** list to open the resource group blade and browse the resources provisioned in the environment.</span></span>
    
    ![My virtual machines list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. <span data-ttu-id="11fba-173">Click any of the environments to view the available actions - such as applying artifacts, attaching data disks, changing auto-shutdown time, and more.</span><span class="sxs-lookup"><span data-stu-id="11fba-173">Click any of the environments to view the available actions - such as applying artifacts, attaching data disks, changing auto-shutdown time, and more.</span></span>

    ![Environment actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a><span data-ttu-id="11fba-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="11fba-175">Next steps</span></span>
* <span data-ttu-id="11fba-176">Once a VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span><span class="sxs-lookup"><span data-stu-id="11fba-176">Once a VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="11fba-177">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates)</span><span class="sxs-lookup"><span data-stu-id="11fba-177">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates)</span></span>








