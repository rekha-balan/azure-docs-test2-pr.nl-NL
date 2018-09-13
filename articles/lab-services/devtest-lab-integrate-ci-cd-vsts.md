---
title: Integrate Azure DevTest Labs into your VSTS continuous integration and delivery pipeline | Microsoft Docs
description: Learn how to integrate Azure DevTest Labs into your VSTS continuous integration and delivery pipeline
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: a26df85e-2a00-462b-aac1-dd3539532569
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: b7ce07547eccd52a8b10d4cffecaf1456778da4a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866133"
---
# <a name="integrate-azure-devtest-labs-into-your-azure-devops-continuous-integration-and-delivery-pipeline"></a><span data-ttu-id="e36f2-103">Integrate Azure DevTest Labs into your Azure DevOps continuous integration and delivery pipeline</span><span class="sxs-lookup"><span data-stu-id="e36f2-103">Integrate Azure DevTest Labs into your Azure DevOps continuous integration and delivery pipeline</span></span>
<span data-ttu-id="e36f2-104">You can use the *Azure DevTest Labs Tasks* extension that's installed in Azure DevOps to easily integrate your CI/CD build-and-release pipeline with Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="e36f2-104">You can use the *Azure DevTest Labs Tasks* extension that's installed in Azure DevOps to easily integrate your CI/CD build-and-release pipeline with Azure DevTest Labs.</span></span> <span data-ttu-id="e36f2-105">The extension installs three tasks:</span><span class="sxs-lookup"><span data-stu-id="e36f2-105">The extension installs three tasks:</span></span> 
* <span data-ttu-id="e36f2-106">Create a VM</span><span class="sxs-lookup"><span data-stu-id="e36f2-106">Create a VM</span></span>
* <span data-ttu-id="e36f2-107">Create a custom image from a VM</span><span class="sxs-lookup"><span data-stu-id="e36f2-107">Create a custom image from a VM</span></span>
* <span data-ttu-id="e36f2-108">Delete a VM</span><span class="sxs-lookup"><span data-stu-id="e36f2-108">Delete a VM</span></span> 

<span data-ttu-id="e36f2-109">The process makes it easy to, for example, quickly deploy a "golden image" for a specific test task and then delete it when the test is finished.</span><span class="sxs-lookup"><span data-stu-id="e36f2-109">The process makes it easy to, for example, quickly deploy a "golden image" for a specific test task and then delete it when the test is finished.</span></span>

<span data-ttu-id="e36f2-110">This article shows how to create and deploy a VM, create a custom image, and then delete the VM, all as one complete pipeline.</span><span class="sxs-lookup"><span data-stu-id="e36f2-110">This article shows how to create and deploy a VM, create a custom image, and then delete the VM, all as one complete pipeline.</span></span> <span data-ttu-id="e36f2-111">You would ordinarily perform each task individually in your own custom build-test-deploy pipeline.</span><span class="sxs-lookup"><span data-stu-id="e36f2-111">You would ordinarily perform each task individually in your own custom build-test-deploy pipeline.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e36f2-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="e36f2-112">Before you begin</span></span>
<span data-ttu-id="e36f2-113">Before you can integrate your CI/CD pipeline with Azure DevTest Labs, you must install the extension from Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e36f2-113">Before you can integrate your CI/CD pipeline with Azure DevTest Labs, you must install the extension from Visual Studio Marketplace.</span></span>
1. <span data-ttu-id="e36f2-114">Go to [Azure DevTest Labs Tasks](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks).</span><span class="sxs-lookup"><span data-stu-id="e36f2-114">Go to [Azure DevTest Labs Tasks](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks).</span></span>
1. <span data-ttu-id="e36f2-115">Select **Install**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-115">Select **Install**.</span></span>
1. <span data-ttu-id="e36f2-116">Complete the wizard.</span><span class="sxs-lookup"><span data-stu-id="e36f2-116">Complete the wizard.</span></span>

## <a name="create-a-resource-manager-template"></a><span data-ttu-id="e36f2-117">Create a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="e36f2-117">Create a Resource Manager template</span></span>
<span data-ttu-id="e36f2-118">This section describes how to create the Azure Resource Manager template that you use to create an Azure virtual machine on demand.</span><span class="sxs-lookup"><span data-stu-id="e36f2-118">This section describes how to create the Azure Resource Manager template that you use to create an Azure virtual machine on demand.</span></span>

1. <span data-ttu-id="e36f2-119">To create a Resource Manager template in your subscription, complete the procedure in [Use a Resource Manager template](devtest-lab-use-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="e36f2-119">To create a Resource Manager template in your subscription, complete the procedure in [Use a Resource Manager template](devtest-lab-use-resource-manager-template.md).</span></span>
1. <span data-ttu-id="e36f2-120">Before you generate the Resource Manager template, add the [WinRM artifact](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-winrm) as part of creating the VM.</span><span class="sxs-lookup"><span data-stu-id="e36f2-120">Before you generate the Resource Manager template, add the [WinRM artifact](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-winrm) as part of creating the VM.</span></span>

   <span data-ttu-id="e36f2-121">WinRM access is required to use deployment tasks such as *Azure File Copy* and *PowerShell on Target Machines*.</span><span class="sxs-lookup"><span data-stu-id="e36f2-121">WinRM access is required to use deployment tasks such as *Azure File Copy* and *PowerShell on Target Machines*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e36f2-122">When you use WinRM with a shared IP address, you must add a NAT rule to map an external port to the WinRM port.</span><span class="sxs-lookup"><span data-stu-id="e36f2-122">When you use WinRM with a shared IP address, you must add a NAT rule to map an external port to the WinRM port.</span></span> <span data-ttu-id="e36f2-123">This step is not required if you create the VM with a public IP address.</span><span class="sxs-lookup"><span data-stu-id="e36f2-123">This step is not required if you create the VM with a public IP address.</span></span>
   >
   >

1. <span data-ttu-id="e36f2-124">Save the template as a file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e36f2-124">Save the template as a file on your computer.</span></span> <span data-ttu-id="e36f2-125">Name the file **CreateVMTemplate.json**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-125">Name the file **CreateVMTemplate.json**.</span></span>
1. <span data-ttu-id="e36f2-126">Check the template in to your source control system.</span><span class="sxs-lookup"><span data-stu-id="e36f2-126">Check the template in to your source control system.</span></span>
1. <span data-ttu-id="e36f2-127">Open a text editor, and paste the following script into it.</span><span class="sxs-lookup"><span data-stu-id="e36f2-127">Open a text editor, and paste the following script into it.</span></span>

   ```powershell
   Param( [string] $labVmId)

   $labVmComputeId = (Get-AzureRmResource -Id $labVmId).Properties.ComputeId

   # Get lab VM resource group name
   $labVmRgName = (Get-AzureRmResource -Id $labVmComputeId).ResourceGroupName

   # Get the lab VM Name
   $labVmName = (Get-AzureRmResource -Id $labVmId).Name

   # Get lab VM public IP address
   $labVMIpAddress = (Get-AzureRmPublicIpAddress -ResourceGroupName $labVmRgName
                   -Name $labVmName).IpAddress

   # Get lab VM FQDN
   $labVMFqdn = (Get-AzureRmPublicIpAddress -ResourceGroupName $labVmRgName
              -Name $labVmName).DnsSettings.Fqdn

   # Set a variable labVmRgName to store the lab VM resource group name
   Write-Host "##vso[task.setvariable variable=labVmRgName;]$labVmRgName"

   # Set a variable labVMIpAddress to store the lab VM Ip address
   Write-Host "##vso[task.setvariable variable=labVMIpAddress;]$labVMIpAddress"

   # Set a variable labVMFqdn to store the lab VM FQDN name
   Write-Host "##vso[task.setvariable variable=labVMFqdn;]$labVMFqdn"
   ```

1. <span data-ttu-id="e36f2-128">Check the script in to your source control system.</span><span class="sxs-lookup"><span data-stu-id="e36f2-128">Check the script in to your source control system.</span></span> <span data-ttu-id="e36f2-129">Name it something like **GetLabVMParams.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-129">Name it something like **GetLabVMParams.ps1**.</span></span>

   <span data-ttu-id="e36f2-130">When you run this script on the agent as part of the release pipeline, and if you use task steps such as *Azure File Copy* or *PowerShell on Target Machines*, the script collects the values that you need to deploy your app to the VM.</span><span class="sxs-lookup"><span data-stu-id="e36f2-130">When you run this script on the agent as part of the release pipeline, and if you use task steps such as *Azure File Copy* or *PowerShell on Target Machines*, the script collects the values that you need to deploy your app to the VM.</span></span> <span data-ttu-id="e36f2-131">You would ordinarily use these tasks to deploy apps to an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="e36f2-131">You would ordinarily use these tasks to deploy apps to an Azure VM.</span></span> <span data-ttu-id="e36f2-132">The tasks require values such as the VM Resource Group name, IP address, and fully qualified domain name (FDQN).</span><span class="sxs-lookup"><span data-stu-id="e36f2-132">The tasks require values such as the VM Resource Group name, IP address, and fully qualified domain name (FDQN).</span></span>

## <a name="create-a-release-pipeline-in-release-management"></a><span data-ttu-id="e36f2-133">Create a release pipeline in Release Management</span><span class="sxs-lookup"><span data-stu-id="e36f2-133">Create a release pipeline in Release Management</span></span>
<span data-ttu-id="e36f2-134">To create the release pipeline, do the following:</span><span class="sxs-lookup"><span data-stu-id="e36f2-134">To create the release pipeline, do the following:</span></span>

1. <span data-ttu-id="e36f2-135">On the **Releases** tab of the **Build & Release** hub, select the plus sign (+) button.</span><span class="sxs-lookup"><span data-stu-id="e36f2-135">On the **Releases** tab of the **Build & Release** hub, select the plus sign (+) button.</span></span>
1. <span data-ttu-id="e36f2-136">In the **Create release definition** window, select the **Empty** template, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-136">In the **Create release definition** window, select the **Empty** template, and then select **Next**.</span></span>
1. <span data-ttu-id="e36f2-137">Select **Choose Later**, and then select **Create** to create a new release pipeline with one default environment and no linked artifacts.</span><span class="sxs-lookup"><span data-stu-id="e36f2-137">Select **Choose Later**, and then select **Create** to create a new release pipeline with one default environment and no linked artifacts.</span></span>
1. <span data-ttu-id="e36f2-138">To open the shortcut menu, in the new release pipeline, select the ellipsis (...) next to the environment name, and then select **Configure variables**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-138">To open the shortcut menu, in the new release pipeline, select the ellipsis (...) next to the environment name, and then select **Configure variables**.</span></span> 
1. <span data-ttu-id="e36f2-139">In the **Configure - environment** window, for the variables that you use in the release pipeline tasks, enter the following values:</span><span class="sxs-lookup"><span data-stu-id="e36f2-139">In the **Configure - environment** window, for the variables that you use in the release pipeline tasks, enter the following values:</span></span>

   <span data-ttu-id="e36f2-140">a.</span><span class="sxs-lookup"><span data-stu-id="e36f2-140">a.</span></span> <span data-ttu-id="e36f2-141">For **vmName**, enter the name that you assigned to the VM when you created the Resource Manager template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e36f2-141">For **vmName**, enter the name that you assigned to the VM when you created the Resource Manager template in the Azure portal.</span></span>

   <span data-ttu-id="e36f2-142">b.</span><span class="sxs-lookup"><span data-stu-id="e36f2-142">b.</span></span> <span data-ttu-id="e36f2-143">For **userName**, enter the username that you assigned to the VM when you created the Resource Manager template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e36f2-143">For **userName**, enter the username that you assigned to the VM when you created the Resource Manager template in the Azure portal.</span></span>

   <span data-ttu-id="e36f2-144">c.</span><span class="sxs-lookup"><span data-stu-id="e36f2-144">c.</span></span> <span data-ttu-id="e36f2-145">For **password**, enter the password that you assigned to the VM when you created the Resource Manager template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e36f2-145">For **password**, enter the password that you assigned to the VM when you created the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="e36f2-146">Use the "padlock" icon to hide and secure the password.</span><span class="sxs-lookup"><span data-stu-id="e36f2-146">Use the "padlock" icon to hide and secure the password.</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="e36f2-147">Create a VM</span><span class="sxs-lookup"><span data-stu-id="e36f2-147">Create a VM</span></span>

<span data-ttu-id="e36f2-148">The next stage of the deployment is to create the VM to use as the "golden image" for subsequent deployments.</span><span class="sxs-lookup"><span data-stu-id="e36f2-148">The next stage of the deployment is to create the VM to use as the "golden image" for subsequent deployments.</span></span> <span data-ttu-id="e36f2-149">You create the VM within your Azure DevTest Lab instance by using the task that's specially developed for this purpose.</span><span class="sxs-lookup"><span data-stu-id="e36f2-149">You create the VM within your Azure DevTest Lab instance by using the task that's specially developed for this purpose.</span></span> 

1. <span data-ttu-id="e36f2-150">In the release pipeline, select **Add tasks**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-150">In the release pipeline, select **Add tasks**.</span></span>
1. <span data-ttu-id="e36f2-151">On the **Deploy** tab, add an *Azure DevTest Labs Create VM* task.</span><span class="sxs-lookup"><span data-stu-id="e36f2-151">On the **Deploy** tab, add an *Azure DevTest Labs Create VM* task.</span></span> <span data-ttu-id="e36f2-152">Configure the task as follows:</span><span class="sxs-lookup"><span data-stu-id="e36f2-152">Configure the task as follows:</span></span>

   > [!NOTE]
   > <span data-ttu-id="e36f2-153">To create the VM to use for subsequent deployments, see [Azure DevTest Labs tasks](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks).</span><span class="sxs-lookup"><span data-stu-id="e36f2-153">To create the VM to use for subsequent deployments, see [Azure DevTest Labs tasks](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks).</span></span>

   <span data-ttu-id="e36f2-154">a.</span><span class="sxs-lookup"><span data-stu-id="e36f2-154">a.</span></span> <span data-ttu-id="e36f2-155">For **Azure RM Subscription**, select a connection in the **Available Azure Service Connections** list, or create a more restricted permissions connection to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e36f2-155">For **Azure RM Subscription**, select a connection in the **Available Azure Service Connections** list, or create a more restricted permissions connection to your Azure subscription.</span></span> <span data-ttu-id="e36f2-156">For more information, see [Azure Resource Manager service endpoint](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints#sep-azure-rm).</span><span class="sxs-lookup"><span data-stu-id="e36f2-156">For more information, see [Azure Resource Manager service endpoint](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints#sep-azure-rm).</span></span>

   <span data-ttu-id="e36f2-157">b.</span><span class="sxs-lookup"><span data-stu-id="e36f2-157">b.</span></span> <span data-ttu-id="e36f2-158">For **Lab Name**, select the name of the instance that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="e36f2-158">For **Lab Name**, select the name of the instance that you created earlier.</span></span>

   <span data-ttu-id="e36f2-159">c.</span><span class="sxs-lookup"><span data-stu-id="e36f2-159">c.</span></span> <span data-ttu-id="e36f2-160">For **Template Name**, enter the full path and name of the template file that you saved to your source code repository.</span><span class="sxs-lookup"><span data-stu-id="e36f2-160">For **Template Name**, enter the full path and name of the template file that you saved to your source code repository.</span></span> <span data-ttu-id="e36f2-161">You can use the built-in properties of Release Management to simplify the path, for example:</span><span class="sxs-lookup"><span data-stu-id="e36f2-161">You can use the built-in properties of Release Management to simplify the path, for example:</span></span>

   ```
   $(System.DefaultWorkingDirectory)/Contoso/ARMTemplates/CreateVMTemplate.json
   ```

   <span data-ttu-id="e36f2-162">d.</span><span class="sxs-lookup"><span data-stu-id="e36f2-162">d.</span></span> <span data-ttu-id="e36f2-163">For **Template Parameters**, enter the parameters for the variables that are defined in the template.</span><span class="sxs-lookup"><span data-stu-id="e36f2-163">For **Template Parameters**, enter the parameters for the variables that are defined in the template.</span></span> <span data-ttu-id="e36f2-164">Use the names of the variables that you defined in the environment, for example:</span><span class="sxs-lookup"><span data-stu-id="e36f2-164">Use the names of the variables that you defined in the environment, for example:</span></span>

   ```
   -newVMName '$(vmName)' -userName '$(userName)' -password (ConvertTo-SecureString -String '$(password)' -AsPlainText -Force)
   ```

   <span data-ttu-id="e36f2-165">e.</span><span class="sxs-lookup"><span data-stu-id="e36f2-165">e.</span></span> <span data-ttu-id="e36f2-166">For **Output Variables - Lab VM ID**, you need the ID of the newly created VM for subsequent steps.</span><span class="sxs-lookup"><span data-stu-id="e36f2-166">For **Output Variables - Lab VM ID**, you need the ID of the newly created VM for subsequent steps.</span></span> <span data-ttu-id="e36f2-167">You set the default name of the environment variable that is automatically populated with this ID in the **Output Variables** section.</span><span class="sxs-lookup"><span data-stu-id="e36f2-167">You set the default name of the environment variable that is automatically populated with this ID in the **Output Variables** section.</span></span> <span data-ttu-id="e36f2-168">You can edit the variable if necessary, but remember to use the correct name in subsequent tasks.</span><span class="sxs-lookup"><span data-stu-id="e36f2-168">You can edit the variable if necessary, but remember to use the correct name in subsequent tasks.</span></span> <span data-ttu-id="e36f2-169">The Lab VM ID is written in the following form:</span><span class="sxs-lookup"><span data-stu-id="e36f2-169">The Lab VM ID is written in the following form:</span></span>

   ```
   /subscriptions/{subId}/resourceGroups/{rgName}/providers/Microsoft.DevTestLab/labs/{labName}/virtualMachines/{vmName}
   ```

1. <span data-ttu-id="e36f2-170">Execute the script you created earlier to collect the details of the DevTest Labs VM.</span><span class="sxs-lookup"><span data-stu-id="e36f2-170">Execute the script you created earlier to collect the details of the DevTest Labs VM.</span></span> 
1. <span data-ttu-id="e36f2-171">In the release pipeline, select **Add tasks** and then, on the **Deploy** tab, add an *Azure PowerShell* task.</span><span class="sxs-lookup"><span data-stu-id="e36f2-171">In the release pipeline, select **Add tasks** and then, on the **Deploy** tab, add an *Azure PowerShell* task.</span></span> <span data-ttu-id="e36f2-172">Configure the task as follows:</span><span class="sxs-lookup"><span data-stu-id="e36f2-172">Configure the task as follows:</span></span>

   > [!NOTE]
   > <span data-ttu-id="e36f2-173">To collect the details of the DevTest Labs VM, see [Deploy: Azure PowerShell](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/AzurePowerShell) and execute the script.</span><span class="sxs-lookup"><span data-stu-id="e36f2-173">To collect the details of the DevTest Labs VM, see [Deploy: Azure PowerShell](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/AzurePowerShell) and execute the script.</span></span>

   <span data-ttu-id="e36f2-174">a.</span><span class="sxs-lookup"><span data-stu-id="e36f2-174">a.</span></span> <span data-ttu-id="e36f2-175">For **Azure Connection Type**, select **Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-175">For **Azure Connection Type**, select **Azure Resource Manager**.</span></span>

   <span data-ttu-id="e36f2-176">b.</span><span class="sxs-lookup"><span data-stu-id="e36f2-176">b.</span></span> <span data-ttu-id="e36f2-177">For **Azure RM Subscription**, select a connection from the list under **Available Azure Service Connections**, or create a more restricted permissions connection to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e36f2-177">For **Azure RM Subscription**, select a connection from the list under **Available Azure Service Connections**, or create a more restricted permissions connection to your Azure subscription.</span></span> <span data-ttu-id="e36f2-178">For more information, see [Azure Resource Manager service endpoint](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints#sep-azure-rm).</span><span class="sxs-lookup"><span data-stu-id="e36f2-178">For more information, see [Azure Resource Manager service endpoint](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints#sep-azure-rm).</span></span>

   <span data-ttu-id="e36f2-179">c.</span><span class="sxs-lookup"><span data-stu-id="e36f2-179">c.</span></span> <span data-ttu-id="e36f2-180">For **Script Type**, select **Script File**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-180">For **Script Type**, select **Script File**.</span></span>
 
   <span data-ttu-id="e36f2-181">d.</span><span class="sxs-lookup"><span data-stu-id="e36f2-181">d.</span></span> <span data-ttu-id="e36f2-182">For **Script Path**, enter the full path and name of the script that you saved to your source code repository.</span><span class="sxs-lookup"><span data-stu-id="e36f2-182">For **Script Path**, enter the full path and name of the script that you saved to your source code repository.</span></span> <span data-ttu-id="e36f2-183">You can use the built-in properties of Release Management to simplify the path, for example:</span><span class="sxs-lookup"><span data-stu-id="e36f2-183">You can use the built-in properties of Release Management to simplify the path, for example:</span></span>
      ```
      $(System.DefaultWorkingDirectory/Contoso/Scripts/GetLabVMParams.ps1
      ```
   <span data-ttu-id="e36f2-184">e.</span><span class="sxs-lookup"><span data-stu-id="e36f2-184">e.</span></span> <span data-ttu-id="e36f2-185">For **Script Arguments**, enter the name of the environment variable that was automatically populated with the ID of the lab VM by the previous task, for example:</span><span class="sxs-lookup"><span data-stu-id="e36f2-185">For **Script Arguments**, enter the name of the environment variable that was automatically populated with the ID of the lab VM by the previous task, for example:</span></span> 
      ```
      -labVmId '$(labVMId)'
      ```
    <span data-ttu-id="e36f2-186">The script collects the required values and stores them in environment variables within the release pipeline so that you can easily refer to them in subsequent steps.</span><span class="sxs-lookup"><span data-stu-id="e36f2-186">The script collects the required values and stores them in environment variables within the release pipeline so that you can easily refer to them in subsequent steps.</span></span>

1. <span data-ttu-id="e36f2-187">Deploy your app to the new DevTest Labs VM.</span><span class="sxs-lookup"><span data-stu-id="e36f2-187">Deploy your app to the new DevTest Labs VM.</span></span> <span data-ttu-id="e36f2-188">The tasks you ordinarily use to deploy the app are *Azure File Copy* and *PowerShell on Target Machines*.</span><span class="sxs-lookup"><span data-stu-id="e36f2-188">The tasks you ordinarily use to deploy the app are *Azure File Copy* and *PowerShell on Target Machines*.</span></span>
   <span data-ttu-id="e36f2-189">The information about the VM you need for the parameters of these tasks is stored in three configuration variables named **labVmRgName**, **labVMIpAddress**, and **labVMFqdn** within the release pipeline.</span><span class="sxs-lookup"><span data-stu-id="e36f2-189">The information about the VM you need for the parameters of these tasks is stored in three configuration variables named **labVmRgName**, **labVMIpAddress**, and **labVMFqdn** within the release pipeline.</span></span> <span data-ttu-id="e36f2-190">If you only want to experiment with creating a DevTest Labs VM and a custom image, without deploying an app to it, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="e36f2-190">If you only want to experiment with creating a DevTest Labs VM and a custom image, without deploying an app to it, you can skip this step.</span></span>

### <a name="create-an-image"></a><span data-ttu-id="e36f2-191">Create an image</span><span class="sxs-lookup"><span data-stu-id="e36f2-191">Create an image</span></span>

<span data-ttu-id="e36f2-192">The next stage is to create an image of the newly deployed VM in your Azure DevTest Labs instance.</span><span class="sxs-lookup"><span data-stu-id="e36f2-192">The next stage is to create an image of the newly deployed VM in your Azure DevTest Labs instance.</span></span> <span data-ttu-id="e36f2-193">You can then use the image to create copies of the VM on demand whenever you want to execute a dev task or run some tests.</span><span class="sxs-lookup"><span data-stu-id="e36f2-193">You can then use the image to create copies of the VM on demand whenever you want to execute a dev task or run some tests.</span></span> 

1. <span data-ttu-id="e36f2-194">In the release pipeline, select **Add tasks**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-194">In the release pipeline, select **Add tasks**.</span></span>
1. <span data-ttu-id="e36f2-195">On the **Deploy** tab, add an **Azure DevTest Labs Create Custom Image** task.</span><span class="sxs-lookup"><span data-stu-id="e36f2-195">On the **Deploy** tab, add an **Azure DevTest Labs Create Custom Image** task.</span></span> <span data-ttu-id="e36f2-196">Configure it as follows:</span><span class="sxs-lookup"><span data-stu-id="e36f2-196">Configure it as follows:</span></span>

   > [!NOTE]
   > <span data-ttu-id="e36f2-197">To create the image, see [Azure DevTest Labs tasks](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks).</span><span class="sxs-lookup"><span data-stu-id="e36f2-197">To create the image, see [Azure DevTest Labs tasks](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks).</span></span>

   <span data-ttu-id="e36f2-198">a.</span><span class="sxs-lookup"><span data-stu-id="e36f2-198">a.</span></span> <span data-ttu-id="e36f2-199">For **Azure RM Subscription**, in the **Available Azure Service Connections** list, select a connection from the list, or create a more restricted permissions connection to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e36f2-199">For **Azure RM Subscription**, in the **Available Azure Service Connections** list, select a connection from the list, or create a more restricted permissions connection to your Azure subscription.</span></span> <span data-ttu-id="e36f2-200">For more information, see [Azure Resource Manager service endpoint](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints#sep-azure-rm).</span><span class="sxs-lookup"><span data-stu-id="e36f2-200">For more information, see [Azure Resource Manager service endpoint](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints#sep-azure-rm).</span></span>

   <span data-ttu-id="e36f2-201">b.</span><span class="sxs-lookup"><span data-stu-id="e36f2-201">b.</span></span> <span data-ttu-id="e36f2-202">For **Lab Name**, select the name of the instance you created earlier.</span><span class="sxs-lookup"><span data-stu-id="e36f2-202">For **Lab Name**, select the name of the instance you created earlier.</span></span>

   <span data-ttu-id="e36f2-203">c.</span><span class="sxs-lookup"><span data-stu-id="e36f2-203">c.</span></span> <span data-ttu-id="e36f2-204">For **Custom Image Name**, enter a name for the custom image.</span><span class="sxs-lookup"><span data-stu-id="e36f2-204">For **Custom Image Name**, enter a name for the custom image.</span></span>

   <span data-ttu-id="e36f2-205">d.</span><span class="sxs-lookup"><span data-stu-id="e36f2-205">d.</span></span> <span data-ttu-id="e36f2-206">(Optional) For **Description**, enter a description to make it easy to select the correct image later.</span><span class="sxs-lookup"><span data-stu-id="e36f2-206">(Optional) For **Description**, enter a description to make it easy to select the correct image later.</span></span>

   <span data-ttu-id="e36f2-207">e.</span><span class="sxs-lookup"><span data-stu-id="e36f2-207">e.</span></span> <span data-ttu-id="e36f2-208">For **Source Lab VM - Source Lab VM ID**, if you changed the default name of the environment variable that was automatically populated with the ID of the lab VM by an earlier task, edit it here.</span><span class="sxs-lookup"><span data-stu-id="e36f2-208">For **Source Lab VM - Source Lab VM ID**, if you changed the default name of the environment variable that was automatically populated with the ID of the lab VM by an earlier task, edit it here.</span></span> <span data-ttu-id="e36f2-209">The default value is **$(labVMId)**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-209">The default value is **$(labVMId)**.</span></span>

   <span data-ttu-id="e36f2-210">f.</span><span class="sxs-lookup"><span data-stu-id="e36f2-210">f.</span></span> <span data-ttu-id="e36f2-211">For **Output Variables - Custom Image ID**, you need the ID of the newly created image when you want to manage or delete it.</span><span class="sxs-lookup"><span data-stu-id="e36f2-211">For **Output Variables - Custom Image ID**, you need the ID of the newly created image when you want to manage or delete it.</span></span> <span data-ttu-id="e36f2-212">The default name of the environment variable that is automatically populated with this ID is set in the **Output Variables** section.</span><span class="sxs-lookup"><span data-stu-id="e36f2-212">The default name of the environment variable that is automatically populated with this ID is set in the **Output Variables** section.</span></span> <span data-ttu-id="e36f2-213">You can edit the variable if necessary.</span><span class="sxs-lookup"><span data-stu-id="e36f2-213">You can edit the variable if necessary.</span></span>

### <a name="delete-the-vm"></a><span data-ttu-id="e36f2-214">Delete the VM</span><span class="sxs-lookup"><span data-stu-id="e36f2-214">Delete the VM</span></span>

<span data-ttu-id="e36f2-215">The final stage is to delete the VM that you deployed in your Azure DevTest Labs instance.</span><span class="sxs-lookup"><span data-stu-id="e36f2-215">The final stage is to delete the VM that you deployed in your Azure DevTest Labs instance.</span></span> <span data-ttu-id="e36f2-216">You would ordinarily delete the VM after you execute the dev tasks or run the tests that you need on the deployed VM.</span><span class="sxs-lookup"><span data-stu-id="e36f2-216">You would ordinarily delete the VM after you execute the dev tasks or run the tests that you need on the deployed VM.</span></span> 

1. <span data-ttu-id="e36f2-217">In the release pipeline, select **Add tasks** and then, on the **Deploy** tab, add an *Azure DevTest Labs Delete VM* task.</span><span class="sxs-lookup"><span data-stu-id="e36f2-217">In the release pipeline, select **Add tasks** and then, on the **Deploy** tab, add an *Azure DevTest Labs Delete VM* task.</span></span> <span data-ttu-id="e36f2-218">Configure it as follows:</span><span class="sxs-lookup"><span data-stu-id="e36f2-218">Configure it as follows:</span></span>

      > [!NOTE]
      > <span data-ttu-id="e36f2-219">To delete the VM, see [Azure DevTest Labs Tasks](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks).</span><span class="sxs-lookup"><span data-stu-id="e36f2-219">To delete the VM, see [Azure DevTest Labs Tasks](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks).</span></span>

   <span data-ttu-id="e36f2-220">a.</span><span class="sxs-lookup"><span data-stu-id="e36f2-220">a.</span></span> <span data-ttu-id="e36f2-221">For **Azure RM Subscription**, select a connection in the **Available Azure Service Connections** list, or create a more restricted permissions connection to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e36f2-221">For **Azure RM Subscription**, select a connection in the **Available Azure Service Connections** list, or create a more restricted permissions connection to your Azure subscription.</span></span> <span data-ttu-id="e36f2-222">For more information, see [Azure Resource Manager service endpoint](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints#sep-azure-rm).</span><span class="sxs-lookup"><span data-stu-id="e36f2-222">For more information, see [Azure Resource Manager service endpoint](https://docs.microsoft.com/azure/devops/pipelines/library/service-endpoints#sep-azure-rm).</span></span>
 
   <span data-ttu-id="e36f2-223">b.</span><span class="sxs-lookup"><span data-stu-id="e36f2-223">b.</span></span> <span data-ttu-id="e36f2-224">For **Lab VM ID**, if you changed the default name of the environment variable that was automatically populated with the ID of the lab VM by an earlier task, edit it here.</span><span class="sxs-lookup"><span data-stu-id="e36f2-224">For **Lab VM ID**, if you changed the default name of the environment variable that was automatically populated with the ID of the lab VM by an earlier task, edit it here.</span></span> <span data-ttu-id="e36f2-225">The default value is **$(labVMId)**.</span><span class="sxs-lookup"><span data-stu-id="e36f2-225">The default value is **$(labVMId)**.</span></span>

1. <span data-ttu-id="e36f2-226">Enter a name for the release pipeline, and then save it.</span><span class="sxs-lookup"><span data-stu-id="e36f2-226">Enter a name for the release pipeline, and then save it.</span></span>
1. <span data-ttu-id="e36f2-227">Create a new release, select the latest build, and deploy it to the single environment in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e36f2-227">Create a new release, select the latest build, and deploy it to the single environment in the pipeline.</span></span>

<span data-ttu-id="e36f2-228">At each stage, refresh the view of your DevTest Labs instance in the Azure portal to view the VM and image that are being created, and the VM that's being deleted again.</span><span class="sxs-lookup"><span data-stu-id="e36f2-228">At each stage, refresh the view of your DevTest Labs instance in the Azure portal to view the VM and image that are being created, and the VM that's being deleted again.</span></span>

<span data-ttu-id="e36f2-229">You can now use the custom image to create VMs when they're required.</span><span class="sxs-lookup"><span data-stu-id="e36f2-229">You can now use the custom image to create VMs when they're required.</span></span>


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="e36f2-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="e36f2-230">Next steps</span></span>
* <span data-ttu-id="e36f2-231">Learn how to [Create multi-VM environments with Resource Manager templates](devtest-lab-create-environment-from-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e36f2-231">Learn how to [Create multi-VM environments with Resource Manager templates](devtest-lab-create-environment-from-arm.md).</span></span>
* <span data-ttu-id="e36f2-232">Explore more quickstart Resource Manager templates for DevTest Labs automation from the [public DevTest Labs GitHub repo](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="e36f2-232">Explore more quickstart Resource Manager templates for DevTest Labs automation from the [public DevTest Labs GitHub repo](https://github.com/Azure/azure-quickstart-templates).</span></span>
* <span data-ttu-id="e36f2-233">If necessary, see the [Azure DevOps Troubleshooting](https://docs.microsoft.com/azure/devops/pipelines/troubleshooting) page.</span><span class="sxs-lookup"><span data-stu-id="e36f2-233">If necessary, see the [Azure DevOps Troubleshooting](https://docs.microsoft.com/azure/devops/pipelines/troubleshooting) page.</span></span>
 
