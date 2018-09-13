---
title: Getting started with Azure Automation State Configuration
description: Explanation and examples of the most common tasks in Azure Automation State Configuration (DSC)
services: automation
ms.service: automation
ms.component: dsc
author: DCtheGeek
ms.author: dacoulte
ms.date: 08/08/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 9a18855d11c0b367b7d58ffb0f4c62e752c05b89
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805199"
---
# <a name="getting-started-with-azure-automation-state-configuration"></a><span data-ttu-id="680f1-103">Getting started with Azure Automation State Configuration</span><span class="sxs-lookup"><span data-stu-id="680f1-103">Getting started with Azure Automation State Configuration</span></span>

<span data-ttu-id="680f1-104">This article explains how to do the most common tasks with Azure Automation State Configuration, such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span><span class="sxs-lookup"><span data-stu-id="680f1-104">This article explains how to do the most common tasks with Azure Automation State Configuration, such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="680f1-105">For an overview of what Azure Automation State Configuration is, see [Azure Automation State Configuration Overview](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="680f1-105">For an overview of what Azure Automation State Configuration is, see [Azure Automation State Configuration Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="680f1-106">For Desired State Configuration (DSC) documentation, see [Windows PowerShell Desired State Configuration Overview](/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="680f1-106">For Desired State Configuration (DSC) documentation, see [Windows PowerShell Desired State Configuration Overview](/powershell/dsc/overview).</span></span>

<span data-ttu-id="680f1-107">This article provides a step-by-step guide to using Azure Automation State Configuration.</span><span class="sxs-lookup"><span data-stu-id="680f1-107">This article provides a step-by-step guide to using Azure Automation State Configuration.</span></span> <span data-ttu-id="680f1-108">If you want a sample environment that is already set up without following the steps described in this article, you can use the following Resource Manager template: [Azure Automation Managed Node template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-automation-configuration).</span><span class="sxs-lookup"><span data-stu-id="680f1-108">If you want a sample environment that is already set up without following the steps described in this article, you can use the following Resource Manager template: [Azure Automation Managed Node template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-automation-configuration).</span></span> <span data-ttu-id="680f1-109">This template sets up a completed Azure Automation State Configuration environment, including an Azure VM that is managed by Azure Automation State Configuration.</span><span class="sxs-lookup"><span data-stu-id="680f1-109">This template sets up a completed Azure Automation State Configuration environment, including an Azure VM that is managed by Azure Automation State Configuration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="680f1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="680f1-110">Prerequisites</span></span>

<span data-ttu-id="680f1-111">To complete the examples in this article, the following are required:</span><span class="sxs-lookup"><span data-stu-id="680f1-111">To complete the examples in this article, the following are required:</span></span>

- <span data-ttu-id="680f1-112">An Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-112">An Azure Automation account.</span></span> <span data-ttu-id="680f1-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="680f1-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
- <span data-ttu-id="680f1-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="680f1-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="680f1-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="680f1-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="680f1-116">Creating a DSC configuration</span><span class="sxs-lookup"><span data-stu-id="680f1-116">Creating a DSC configuration</span></span>

<span data-ttu-id="680f1-117">You create a simple [DSC configuration](/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span><span class="sxs-lookup"><span data-stu-id="680f1-117">You create a simple [DSC configuration](/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="680f1-118">Start [VSCode](https://code.visualstudio.com/docs) (or any text editor).</span><span class="sxs-lookup"><span data-stu-id="680f1-118">Start [VSCode](https://code.visualstudio.com/docs) (or any text editor).</span></span>
1. <span data-ttu-id="680f1-119">Type the following text:</span><span class="sxs-lookup"><span data-stu-id="680f1-119">Type the following text:</span></span>

    ```powershell
    configuration TestConfig
    {
        Node IsWebServer
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
1. <span data-ttu-id="680f1-120">Save the file as `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="680f1-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="680f1-121">This configuration calls one resource in each node block, the [WindowsFeature resource](/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span><span class="sxs-lookup"><span data-stu-id="680f1-121">This configuration calls one resource in each node block, the [WindowsFeature resource](/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="680f1-122">Importing a configuration into Azure Automation</span><span class="sxs-lookup"><span data-stu-id="680f1-122">Importing a configuration into Azure Automation</span></span>

<span data-ttu-id="680f1-123">Next, you import the configuration into the Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-123">Next, you import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="680f1-124">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680f1-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="680f1-125">On the left, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-125">On the left, click **All resources** and then the name of your Automation account.</span></span>
1. <span data-ttu-id="680f1-126">On the **Automation account** page, select **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="680f1-126">On the **Automation account** page, select **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="680f1-127">On the **State configuration (DSC)** page, click the **Configurations** tab, then click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="680f1-127">On the **State configuration (DSC)** page, click the **Configurations** tab, then click **+ Add**.</span></span>
1. <span data-ttu-id="680f1-128">On the **Import Configuration** page, browse to the `TestConfig.ps1` file on your computer.</span><span class="sxs-lookup"><span data-stu-id="680f1-128">On the **Import Configuration** page, browse to the `TestConfig.ps1` file on your computer.</span></span>

   ![Screenshot of the **Import Configuration** blade](./media/automation-dsc-getting-started/AddConfig.png)

1. <span data-ttu-id="680f1-130">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="680f1-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="680f1-131">Viewing a configuration in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="680f1-131">Viewing a configuration in Azure Automation</span></span>

<span data-ttu-id="680f1-132">After you have imported a configuration, you can view it in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="680f1-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="680f1-133">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680f1-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="680f1-134">On the left, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-134">On the left, click **All resources** and then the name of your Automation account.</span></span>
1. <span data-ttu-id="680f1-135">On the **Automation account** page, select  **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="680f1-135">On the **Automation account** page, select  **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="680f1-136">On the **State configuration (DSC)** page, click the **Configurations** tab, then click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span><span class="sxs-lookup"><span data-stu-id="680f1-136">On the **State configuration (DSC)** page, click the **Configurations** tab, then click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
1. <span data-ttu-id="680f1-137">On the **TestConfig Configuration** page, click **View configuration source**.</span><span class="sxs-lookup"><span data-stu-id="680f1-137">On the **TestConfig Configuration** page, click **View configuration source**.</span></span>

   ![Screenshot of the TestConfig configuration blade](./media/automation-dsc-getting-started/ViewConfigSource.png)

   <span data-ttu-id="680f1-139">A **TestConfig Configuration source** page opens, displaying the PowerShell code for the configuration.</span><span class="sxs-lookup"><span data-stu-id="680f1-139">A **TestConfig Configuration source** page opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="680f1-140">Compiling a configuration in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="680f1-140">Compiling a configuration in Azure Automation</span></span>

<span data-ttu-id="680f1-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span><span class="sxs-lookup"><span data-stu-id="680f1-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="680f1-142">For a more detailed description of compiling configurations in Azure Automation State Configuration, see [Compiling configurations in Azure Automation State Configuration](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="680f1-142">For a more detailed description of compiling configurations in Azure Automation State Configuration, see [Compiling configurations in Azure Automation State Configuration](automation-dsc-compile.md).</span></span>
<span data-ttu-id="680f1-143">For more information about compiling configurations, see [DSC Configurations](/powershell/dsc/configurations).</span><span class="sxs-lookup"><span data-stu-id="680f1-143">For more information about compiling configurations, see [DSC Configurations](/powershell/dsc/configurations).</span></span>

1. <span data-ttu-id="680f1-144">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680f1-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="680f1-145">On the left, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-145">On the left, click **All resources** and then the name of your Automation account.</span></span>
1. <span data-ttu-id="680f1-146">On the **Automation account** page, click **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="680f1-146">On the **Automation account** page, click **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="680f1-147">On the **State configuration (DSC)** page, click the **Configurations** tab, then click **TestConfig** (the name of the previously imported configuration).</span><span class="sxs-lookup"><span data-stu-id="680f1-147">On the **State configuration (DSC)** page, click the **Configurations** tab, then click **TestConfig** (the name of the previously imported configuration).</span></span>
1. <span data-ttu-id="680f1-148">On the **TestConfig Configuration** page, click **Compile**, and then click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="680f1-148">On the **TestConfig Configuration** page, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="680f1-149">This starts a compilation job.</span><span class="sxs-lookup"><span data-stu-id="680f1-149">This starts a compilation job.</span></span>

   ![Screenshot of the TestConfig configuration page highlighting compile button](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="680f1-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span><span class="sxs-lookup"><span data-stu-id="680f1-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="680f1-152">Viewing a compilation job</span><span class="sxs-lookup"><span data-stu-id="680f1-152">Viewing a compilation job</span></span>

<span data-ttu-id="680f1-153">After you start a compilation, you can view it in the **Compilation Jobs** tile in the **Configuration** page.</span><span class="sxs-lookup"><span data-stu-id="680f1-153">After you start a compilation, you can view it in the **Compilation Jobs** tile in the **Configuration** page.</span></span> <span data-ttu-id="680f1-154">The **Compilation Jobs** tile shows currently running, completed, and failed jobs.</span><span class="sxs-lookup"><span data-stu-id="680f1-154">The **Compilation Jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="680f1-155">When you open a compilation job page, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span><span class="sxs-lookup"><span data-stu-id="680f1-155">When you open a compilation job page, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="680f1-156">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680f1-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="680f1-157">On the left, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-157">On the left, click **All resources** and then the name of your Automation account.</span></span>
1. <span data-ttu-id="680f1-158">On the **Automation account** page, click **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="680f1-158">On the **Automation account** page, click **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="680f1-159">On the **State configuration (DSC)** page, click the **Configurations** tab, then click **TestConfig** (the name of the previously imported configuration).</span><span class="sxs-lookup"><span data-stu-id="680f1-159">On the **State configuration (DSC)** page, click the **Configurations** tab, then click **TestConfig** (the name of the previously imported configuration).</span></span>
1. <span data-ttu-id="680f1-160">Under **Compilation jobs**, select the compilation job you want to view.</span><span class="sxs-lookup"><span data-stu-id="680f1-160">Under **Compilation jobs**, select the compilation job you want to view.</span></span> <span data-ttu-id="680f1-161">A **Compilation Job** page opens labeled with the date that the compilation job was started.</span><span class="sxs-lookup"><span data-stu-id="680f1-161">A **Compilation Job** page opens labeled with the date that the compilation job was started.</span></span>

   ![Screenshot of the Compilation Job page](./media/automation-dsc-getting-started/CompilationJob.png)

1. <span data-ttu-id="680f1-163">Click on any tile in the **Compilation Job** page to see further details about the job.</span><span class="sxs-lookup"><span data-stu-id="680f1-163">Click on any tile in the **Compilation Job** page to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="680f1-164">Viewing node configurations</span><span class="sxs-lookup"><span data-stu-id="680f1-164">Viewing node configurations</span></span>

<span data-ttu-id="680f1-165">Successful completion of a compilation job creates one or more new node configurations.</span><span class="sxs-lookup"><span data-stu-id="680f1-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="680f1-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span><span class="sxs-lookup"><span data-stu-id="680f1-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="680f1-167">You can view the node configurations in your Automation account in the **State configuration (DSC)** page.</span><span class="sxs-lookup"><span data-stu-id="680f1-167">You can view the node configurations in your Automation account in the **State configuration (DSC)** page.</span></span> <span data-ttu-id="680f1-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span><span class="sxs-lookup"><span data-stu-id="680f1-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="680f1-169">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680f1-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="680f1-170">On the left, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-170">On the left, click **All resources** and then the name of your Automation account.</span></span>
1. <span data-ttu-id="680f1-171">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="680f1-171">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="680f1-172">On the **State configuration (DSC)** page, click the **Compiled configurations** tab.</span><span class="sxs-lookup"><span data-stu-id="680f1-172">On the **State configuration (DSC)** page, click the **Compiled configurations** tab.</span></span>

   ![Screenshot of the Compiled Configurations tab](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-state-configuration"></a><span data-ttu-id="680f1-174">Onboarding an Azure VM for management with Azure Automation State Configuration</span><span class="sxs-lookup"><span data-stu-id="680f1-174">Onboarding an Azure VM for management with Azure Automation State Configuration</span></span>

<span data-ttu-id="680f1-175">You can use Azure Automation State Configuration to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span><span class="sxs-lookup"><span data-stu-id="680f1-175">You can use Azure Automation State Configuration to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="680f1-176">In this article, you learn how to onboard only Azure Resource Manager VMs.</span><span class="sxs-lookup"><span data-stu-id="680f1-176">In this article, you learn how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="680f1-177">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation State Configuration](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="680f1-177">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation State Configuration](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-state-configuration"></a><span data-ttu-id="680f1-178">To onboard an Azure Resource Manager VM for management by Azure Automation State Configuration</span><span class="sxs-lookup"><span data-stu-id="680f1-178">To onboard an Azure Resource Manager VM for management by Azure Automation State Configuration</span></span>

1. <span data-ttu-id="680f1-179">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680f1-179">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="680f1-180">On the left, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-180">On the left, click **All resources** and then the name of your Automation account.</span></span>
1. <span data-ttu-id="680f1-181">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="680f1-181">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="680f1-182">On the **State configuration (DSC)** page, while on the **Nodes** tab, click **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="680f1-182">On the **State configuration (DSC)** page, while on the **Nodes** tab, click **+ Add**.</span></span>

   ![Screenshot of the DSC Nodes page highlighting the Add Azure VM button](./media/automation-dsc-getting-started/OnboardVM.png)

1. <span data-ttu-id="680f1-184">On the **Virtual Machines** page, select your VM.</span><span class="sxs-lookup"><span data-stu-id="680f1-184">On the **Virtual Machines** page, select your VM.</span></span>
1. <span data-ttu-id="680f1-185">On the **Virtual machine** detail page, click **+ Connect**.</span><span class="sxs-lookup"><span data-stu-id="680f1-185">On the **Virtual machine** detail page, click **+ Connect**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="680f1-186">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="680f1-186">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>

1. <span data-ttu-id="680f1-187">In the **Registration** page, select the name of the node configuration you want to apply to the VM in the **Node configuration name** box.</span><span class="sxs-lookup"><span data-stu-id="680f1-187">In the **Registration** page, select the name of the node configuration you want to apply to the VM in the **Node configuration name** box.</span></span> <span data-ttu-id="680f1-188">Providing a name at this point is optional.</span><span class="sxs-lookup"><span data-stu-id="680f1-188">Providing a name at this point is optional.</span></span> <span data-ttu-id="680f1-189">You can change the assigned node configuration after onboarding the node.</span><span class="sxs-lookup"><span data-stu-id="680f1-189">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="680f1-190">Check **Reboot Node if Needed**, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="680f1-190">Check **Reboot Node if Needed**, then click **OK**.</span></span>

   ![Screenshot of the Registration blade](./media/automation-dsc-getting-started/RegisterVM.png)

   <span data-ttu-id="680f1-192">The node configuration you specified are applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM checks for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span><span class="sxs-lookup"><span data-stu-id="680f1-192">The node configuration you specified are applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM checks for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="680f1-193">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="680f1-193">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
1. <span data-ttu-id="680f1-194">In the **Add Azure VMs** blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="680f1-194">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="680f1-195">Azure starts the process of onboarding the VM.</span><span class="sxs-lookup"><span data-stu-id="680f1-195">Azure starts the process of onboarding the VM.</span></span> <span data-ttu-id="680f1-196">When it is complete, the VM shows up in the **Nodes** tab of the **State configuration (DSC)** page in the Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-196">When it is complete, the VM shows up in the **Nodes** tab of the **State configuration (DSC)** page in the Automation account.</span></span>

## <a name="viewing-the-list-of-managed-nodes"></a><span data-ttu-id="680f1-197">Viewing the list of managed nodes</span><span class="sxs-lookup"><span data-stu-id="680f1-197">Viewing the list of managed nodes</span></span>

<span data-ttu-id="680f1-198">You can view the list of all machines that have been onboarded for management in your Automation account in the **Nodes** tab of the **State configuration (DSC)** page.</span><span class="sxs-lookup"><span data-stu-id="680f1-198">You can view the list of all machines that have been onboarded for management in your Automation account in the **Nodes** tab of the **State configuration (DSC)** page.</span></span>

1. <span data-ttu-id="680f1-199">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680f1-199">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="680f1-200">On the left, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-200">On the left, click **All resources** and then the name of your Automation account.</span></span>
1. <span data-ttu-id="680f1-201">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="680f1-201">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="680f1-202">On the **State configuration (DSC)** page, click the **Nodes** tab.</span><span class="sxs-lookup"><span data-stu-id="680f1-202">On the **State configuration (DSC)** page, click the **Nodes** tab.</span></span>

## <a name="viewing-reports-for-managed-nodes"></a><span data-ttu-id="680f1-203">Viewing reports for managed nodes</span><span class="sxs-lookup"><span data-stu-id="680f1-203">Viewing reports for managed nodes</span></span>

<span data-ttu-id="680f1-204">Each time Azure Automation State Configuration performs a consistency check on a managed node, the node sends a status report back to the pull server.</span><span class="sxs-lookup"><span data-stu-id="680f1-204">Each time Azure Automation State Configuration performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="680f1-205">You can view these reports on the page for that node.</span><span class="sxs-lookup"><span data-stu-id="680f1-205">You can view these reports on the page for that node.</span></span>

1. <span data-ttu-id="680f1-206">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680f1-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="680f1-207">On the left, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-207">On the left, click **All resources** and then the name of your Automation account.</span></span>
1. <span data-ttu-id="680f1-208">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="680f1-208">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="680f1-209">On the **State configuration (DSC)** page, click the **Nodes** tab. Here, you can see the overview of Configuration state and the details for each node.</span><span class="sxs-lookup"><span data-stu-id="680f1-209">On the **State configuration (DSC)** page, click the **Nodes** tab. Here, you can see the overview of Configuration state and the details for each node.</span></span>

   ![Screenshot of Node page](./media/automation-dsc-getting-started/NodesTab.png)

1. <span data-ttu-id="680f1-211">While on the **Nodes** tab, click the node record to open the reporting.</span><span class="sxs-lookup"><span data-stu-id="680f1-211">While on the **Nodes** tab, click the node record to open the reporting.</span></span> <span data-ttu-id="680f1-212">Click the report you want to view additional reporting details.</span><span class="sxs-lookup"><span data-stu-id="680f1-212">Click the report you want to view additional reporting details.</span></span>

   ![Screenshot of the Report blade](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="680f1-214">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span><span class="sxs-lookup"><span data-stu-id="680f1-214">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

- <span data-ttu-id="680f1-215">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **ApplyandMonitor** mode and the machine is not in the desired state).</span><span class="sxs-lookup"><span data-stu-id="680f1-215">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **ApplyandMonitor** mode and the machine is not in the desired state).</span></span>
- <span data-ttu-id="680f1-216">The start time for the consistency check.</span><span class="sxs-lookup"><span data-stu-id="680f1-216">The start time for the consistency check.</span></span>
- <span data-ttu-id="680f1-217">The total runtime for the consistency check.</span><span class="sxs-lookup"><span data-stu-id="680f1-217">The total runtime for the consistency check.</span></span>
- <span data-ttu-id="680f1-218">The type of consistency check.</span><span class="sxs-lookup"><span data-stu-id="680f1-218">The type of consistency check.</span></span>
- <span data-ttu-id="680f1-219">Any errors, including the error code and error message.</span><span class="sxs-lookup"><span data-stu-id="680f1-219">Any errors, including the error code and error message.</span></span>
- <span data-ttu-id="680f1-220">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span><span class="sxs-lookup"><span data-stu-id="680f1-220">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
- <span data-ttu-id="680f1-221">The name, IP address, and configuration mode of the node.</span><span class="sxs-lookup"><span data-stu-id="680f1-221">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="680f1-222">You can also click **View raw report** to see the actual data that the node sends to the server.</span><span class="sxs-lookup"><span data-stu-id="680f1-222">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span>
<span data-ttu-id="680f1-223">For more information about using that data, see [Using a DSC report server](/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="680f1-223">For more information about using that data, see [Using a DSC report server](/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="680f1-224">It can take some time after a node is onboarded before the first report is available.</span><span class="sxs-lookup"><span data-stu-id="680f1-224">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="680f1-225">You might need to wait up to 30 minutes for the first report after you onboard a node.</span><span class="sxs-lookup"><span data-stu-id="680f1-225">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="680f1-226">Reassigning a node to a different node configuration</span><span class="sxs-lookup"><span data-stu-id="680f1-226">Reassigning a node to a different node configuration</span></span>

<span data-ttu-id="680f1-227">You can assign a node to use a different node configuration than the one you initially assigned.</span><span class="sxs-lookup"><span data-stu-id="680f1-227">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="680f1-228">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680f1-228">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="680f1-229">On the left, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-229">On the left, click **All resources** and then the name of your Automation account.</span></span>
1. <span data-ttu-id="680f1-230">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="680f1-230">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="680f1-231">On the **State configuration (DSC)** page, click the **Nodes** tab.</span><span class="sxs-lookup"><span data-stu-id="680f1-231">On the **State configuration (DSC)** page, click the **Nodes** tab.</span></span>
1. <span data-ttu-id="680f1-232">On the **Nodes** tab, click on the name of the node you want to reassign.</span><span class="sxs-lookup"><span data-stu-id="680f1-232">On the **Nodes** tab, click on the name of the node you want to reassign.</span></span>
1. <span data-ttu-id="680f1-233">On the page for that node, click **Assign node configuration**.</span><span class="sxs-lookup"><span data-stu-id="680f1-233">On the page for that node, click **Assign node configuration**.</span></span>

    ![Screenshot of the Node details page highlighting the Assign node configuration button](./media/automation-dsc-getting-started/AssignNode.png)

1. <span data-ttu-id="680f1-235">On the **Assign Node Configuration** page, select the node configuration to which you want to assign the node, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="680f1-235">On the **Assign Node Configuration** page, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>

    ![Screenshot of the Assign Node Configuration page](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="680f1-237">Unregistering a node</span><span class="sxs-lookup"><span data-stu-id="680f1-237">Unregistering a node</span></span>

<span data-ttu-id="680f1-238">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span><span class="sxs-lookup"><span data-stu-id="680f1-238">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="680f1-239">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680f1-239">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="680f1-240">On the left, click **All resources** and then the name of your Automation account.</span><span class="sxs-lookup"><span data-stu-id="680f1-240">On the left, click **All resources** and then the name of your Automation account.</span></span>
1. <span data-ttu-id="680f1-241">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span><span class="sxs-lookup"><span data-stu-id="680f1-241">On the **Automation account** blade, click **State configuration (DSC)** under **Configuration Management**.</span></span>
1. <span data-ttu-id="680f1-242">On the **State configuration (DSC)** page, click the **Nodes** tab.</span><span class="sxs-lookup"><span data-stu-id="680f1-242">On the **State configuration (DSC)** page, click the **Nodes** tab.</span></span>
1. <span data-ttu-id="680f1-243">On the **Nodes** tab, click on the name of the node you want to unregister.</span><span class="sxs-lookup"><span data-stu-id="680f1-243">On the **Nodes** tab, click on the name of the node you want to unregister.</span></span>
1. <span data-ttu-id="680f1-244">On the page for that node, click **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="680f1-244">On the page for that node, click **Unregister**.</span></span>

    ![Screenshot of the Node details page highlighting the Unregister button](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="680f1-246">Related Articles</span><span class="sxs-lookup"><span data-stu-id="680f1-246">Related Articles</span></span>

- [<span data-ttu-id="680f1-247">Azure Automation State Configuration overview</span><span class="sxs-lookup"><span data-stu-id="680f1-247">Azure Automation State Configuration overview</span></span>](automation-dsc-overview.md)
- [<span data-ttu-id="680f1-248">Onboarding machines for management by Azure Automation State Configuration</span><span class="sxs-lookup"><span data-stu-id="680f1-248">Onboarding machines for management by Azure Automation State Configuration</span></span>](automation-dsc-onboarding.md)
- [<span data-ttu-id="680f1-249">Windows PowerShell Desired State Configuration Overview</span><span class="sxs-lookup"><span data-stu-id="680f1-249">Windows PowerShell Desired State Configuration Overview</span></span>](/powershell/dsc/overview)
- [<span data-ttu-id="680f1-250">Azure Automation State Configuration cmdlets</span><span class="sxs-lookup"><span data-stu-id="680f1-250">Azure Automation State Configuration cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
- [<span data-ttu-id="680f1-251">Azure Automation State Configuration pricing</span><span class="sxs-lookup"><span data-stu-id="680f1-251">Azure Automation State Configuration pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)