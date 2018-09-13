---
title: Getting started with Azure Automation DSC | Microsoft Docs
description: Explanation and examples of the most common tasks in Azure Automation Desired State Configuration (DSC)
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 42664b4114e043372cdfacb46b9b3e7e59e50821
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556370"
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="40680-103">Getting started with Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="40680-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="40680-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span><span class="sxs-lookup"><span data-stu-id="40680-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="40680-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40680-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="40680-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="40680-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="40680-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="40680-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="40680-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="40680-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="40680-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="40680-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40680-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="40680-110">Prerequisites</span></span>
<span data-ttu-id="40680-111">To complete the examples in this topic, the following are required:</span><span class="sxs-lookup"><span data-stu-id="40680-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="40680-112">An Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-112">An Azure Automation account.</span></span> <span data-ttu-id="40680-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="40680-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="40680-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="40680-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="40680-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="40680-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="40680-116">Creating a DSC configuration</span><span class="sxs-lookup"><span data-stu-id="40680-116">Creating a DSC configuration</span></span>
<span data-ttu-id="40680-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span><span class="sxs-lookup"><span data-stu-id="40680-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="40680-118">Start the Windows PowerShell ISE (or any text editor).</span><span class="sxs-lookup"><span data-stu-id="40680-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="40680-119">Type the following text:</span><span class="sxs-lookup"><span data-stu-id="40680-119">Type the following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="40680-120">Save the file as `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="40680-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="40680-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span><span class="sxs-lookup"><span data-stu-id="40680-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="40680-122">Importing a configuration into Azure Automation</span><span class="sxs-lookup"><span data-stu-id="40680-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="40680-123">Next, we'll import the configuration into the Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="40680-124">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40680-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40680-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="40680-126">On the **Automation account** blade, click **DSC Configurations**.</span><span class="sxs-lookup"><span data-stu-id="40680-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="40680-127">On the **DSC Configurations** blade, click **Add a configuration**.</span><span class="sxs-lookup"><span data-stu-id="40680-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="40680-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span><span class="sxs-lookup"><span data-stu-id="40680-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![Screenshot of the **Import Configuration** blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="40680-130">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="40680-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="40680-131">Viewing a configuration in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="40680-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="40680-132">After you have imported a configuration, you can view it in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="40680-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="40680-133">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40680-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40680-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="40680-135">On the **Automation account** blade, click **DSC Configurations**</span><span class="sxs-lookup"><span data-stu-id="40680-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="40680-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span><span class="sxs-lookup"><span data-stu-id="40680-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="40680-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span><span class="sxs-lookup"><span data-stu-id="40680-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Screenshot of the TestConfig configuration blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="40680-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span><span class="sxs-lookup"><span data-stu-id="40680-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="40680-140">Compiling a configuration in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="40680-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="40680-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span><span class="sxs-lookup"><span data-stu-id="40680-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="40680-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="40680-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="40680-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="40680-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="40680-144">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40680-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40680-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="40680-146">On the **Automation account** blade, click **DSC Configurations**</span><span class="sxs-lookup"><span data-stu-id="40680-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="40680-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span><span class="sxs-lookup"><span data-stu-id="40680-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="40680-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="40680-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="40680-149">This starts a compilation job.</span><span class="sxs-lookup"><span data-stu-id="40680-149">This starts a compilation job.</span></span>
   
    ![Screenshot of the TestConfig configuration blade highlighting compile button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="40680-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span><span class="sxs-lookup"><span data-stu-id="40680-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="40680-152">Viewing a compilation job</span><span class="sxs-lookup"><span data-stu-id="40680-152">Viewing a compilation job</span></span>
<span data-ttu-id="40680-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span><span class="sxs-lookup"><span data-stu-id="40680-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="40680-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span><span class="sxs-lookup"><span data-stu-id="40680-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="40680-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span><span class="sxs-lookup"><span data-stu-id="40680-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="40680-156">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40680-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40680-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="40680-158">On the **Automation account** blade, click **DSC Configurations**.</span><span class="sxs-lookup"><span data-stu-id="40680-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="40680-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span><span class="sxs-lookup"><span data-stu-id="40680-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="40680-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span><span class="sxs-lookup"><span data-stu-id="40680-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="40680-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span><span class="sxs-lookup"><span data-stu-id="40680-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![Screenshot of the Compilation Job blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="40680-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span><span class="sxs-lookup"><span data-stu-id="40680-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="40680-164">Viewing node configurations</span><span class="sxs-lookup"><span data-stu-id="40680-164">Viewing node configurations</span></span>
<span data-ttu-id="40680-165">Successful completion of a compilation job creates one or more new node configurations.</span><span class="sxs-lookup"><span data-stu-id="40680-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="40680-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span><span class="sxs-lookup"><span data-stu-id="40680-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="40680-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span><span class="sxs-lookup"><span data-stu-id="40680-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="40680-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span><span class="sxs-lookup"><span data-stu-id="40680-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="40680-169">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40680-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40680-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="40680-171">On the **Automation account** blade, click **DSC Node Configurations**.</span><span class="sxs-lookup"><span data-stu-id="40680-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Screenshot of the DSC Node Configurations blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="40680-173">Onboarding an Azure VM for management with Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="40680-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="40680-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span><span class="sxs-lookup"><span data-stu-id="40680-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="40680-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span><span class="sxs-lookup"><span data-stu-id="40680-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="40680-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="40680-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="40680-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="40680-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="40680-178">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40680-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40680-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="40680-180">On the **Automation account** blade, click **DSC Nodes**.</span><span class="sxs-lookup"><span data-stu-id="40680-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="40680-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="40680-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Screenshot of the DSC Nodes blade highlighting the Add Azure VM button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="40680-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span><span class="sxs-lookup"><span data-stu-id="40680-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="40680-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="40680-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="40680-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="40680-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="40680-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span><span class="sxs-lookup"><span data-stu-id="40680-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="40680-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span><span class="sxs-lookup"><span data-stu-id="40680-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="40680-188">This must exactly match the name of a node configuration in the Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="40680-189">Providing a name at this point is optional.</span><span class="sxs-lookup"><span data-stu-id="40680-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="40680-190">You can change the assigned node configuration after onboarding the node.</span><span class="sxs-lookup"><span data-stu-id="40680-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="40680-191">Check **Reboot Node if Needed**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="40680-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Screenshot of the Registration blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="40680-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span><span class="sxs-lookup"><span data-stu-id="40680-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="40680-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="40680-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="40680-195">In the **Add Azure VMs** blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="40680-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="40680-196">Azure will start the process of onboarding the VM.</span><span class="sxs-lookup"><span data-stu-id="40680-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="40680-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="40680-198">Viewing the list of DSC nodes</span><span class="sxs-lookup"><span data-stu-id="40680-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="40680-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span><span class="sxs-lookup"><span data-stu-id="40680-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="40680-200">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40680-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40680-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="40680-202">On the **Automation account** blade, click **DSC Nodes**.</span><span class="sxs-lookup"><span data-stu-id="40680-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="40680-203">Viewing reports for DSC nodes</span><span class="sxs-lookup"><span data-stu-id="40680-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="40680-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span><span class="sxs-lookup"><span data-stu-id="40680-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="40680-205">You can view these reports on the blade for that node.</span><span class="sxs-lookup"><span data-stu-id="40680-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="40680-206">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40680-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40680-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="40680-208">On the **Automation account** blade, click **DSC Nodes**.</span><span class="sxs-lookup"><span data-stu-id="40680-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="40680-209">On the **Reports** tile, click on any of the reports in the list.</span><span class="sxs-lookup"><span data-stu-id="40680-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![Screenshot of the Report blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="40680-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span><span class="sxs-lookup"><span data-stu-id="40680-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="40680-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span><span class="sxs-lookup"><span data-stu-id="40680-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="40680-213">The start time for the consistency check.</span><span class="sxs-lookup"><span data-stu-id="40680-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="40680-214">The total runtime for the consistency check.</span><span class="sxs-lookup"><span data-stu-id="40680-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="40680-215">The type of consistency check.</span><span class="sxs-lookup"><span data-stu-id="40680-215">The type of consistency check.</span></span>
* <span data-ttu-id="40680-216">Any errors, including the error code and error message.</span><span class="sxs-lookup"><span data-stu-id="40680-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="40680-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span><span class="sxs-lookup"><span data-stu-id="40680-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="40680-218">The name, IP address, and configuration mode of the node.</span><span class="sxs-lookup"><span data-stu-id="40680-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="40680-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span><span class="sxs-lookup"><span data-stu-id="40680-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="40680-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="40680-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="40680-221">It can take some time after a node is onboarded before the first report is available.</span><span class="sxs-lookup"><span data-stu-id="40680-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="40680-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span><span class="sxs-lookup"><span data-stu-id="40680-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="40680-223">Reassigning a node to a different node configuration</span><span class="sxs-lookup"><span data-stu-id="40680-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="40680-224">You can assign a node to use a different node configuration than the one you initially assigned.</span><span class="sxs-lookup"><span data-stu-id="40680-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="40680-225">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40680-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40680-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="40680-227">On the **Automation account** blade, click **DSC Nodes**.</span><span class="sxs-lookup"><span data-stu-id="40680-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="40680-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span><span class="sxs-lookup"><span data-stu-id="40680-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="40680-229">On the blade for that node, click **Assign node**.</span><span class="sxs-lookup"><span data-stu-id="40680-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![Screenshot of the Node blade highlighting the Assign Node button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="40680-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="40680-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![Screenshot of the Assign Node Configuration blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="40680-233">Unregistering a node</span><span class="sxs-lookup"><span data-stu-id="40680-233">Unregistering a node</span></span>
<span data-ttu-id="40680-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span><span class="sxs-lookup"><span data-stu-id="40680-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="40680-235">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40680-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40680-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="40680-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="40680-237">On the **Automation account** blade, click **DSC Nodes**.</span><span class="sxs-lookup"><span data-stu-id="40680-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="40680-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span><span class="sxs-lookup"><span data-stu-id="40680-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="40680-239">On the blade for that node, click **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="40680-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![Screenshot of the Node blade highlighting the Unregister button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="40680-241">Related Articles</span><span class="sxs-lookup"><span data-stu-id="40680-241">Related Articles</span></span>
* [<span data-ttu-id="40680-242">Azure Automation DSC overview</span><span class="sxs-lookup"><span data-stu-id="40680-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="40680-243">Onboarding machines for management by Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="40680-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="40680-244">Windows PowerShell Desired State Configuration Overview</span><span class="sxs-lookup"><span data-stu-id="40680-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="40680-245">Azure Automation DSC cmdlets</span><span class="sxs-lookup"><span data-stu-id="40680-245">Azure Automation DSC cmdlets</span></span>](https://msdn.microsoft.com/library/mt244122.aspx)
* [<span data-ttu-id="40680-246">Azure Automation DSC pricing</span><span class="sxs-lookup"><span data-stu-id="40680-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)












