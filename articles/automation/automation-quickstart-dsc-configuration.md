---
title: Azure Quickstart - Configure a VM with DSC | Microsoft Docs
description: Configure a LAMP Stack on a Linux Virtual Machine with Desired State Configuration
services: automation
ms.service: automation
ms.component: dsc
keywords: dsc, configuration, automation
author: KrisBash
ms.author: krbash
ms.date: 12/17/2017
ms.topic: quickstart
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: 959171963bcdc721c81823fcf4f9769174b32636
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969131"
---
# <a name="configure-a-linux-virtual-machine-with-desired-state-configuration"></a><span data-ttu-id="90492-104">Configure a Linux virtual machine with Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="90492-104">Configure a Linux virtual machine with Desired State Configuration</span></span>

<span data-ttu-id="90492-105">By enabling Desired State Configuration (DSC), you can manage and monitor the configurations of your Windows and Linux servers.</span><span class="sxs-lookup"><span data-stu-id="90492-105">By enabling Desired State Configuration (DSC), you can manage and monitor the configurations of your Windows and Linux servers.</span></span> <span data-ttu-id="90492-106">Configurations that drift from the desired configuration can be identified or auto-corrected.</span><span class="sxs-lookup"><span data-stu-id="90492-106">Configurations that drift from the desired configuration can be identified or auto-corrected.</span></span> <span data-ttu-id="90492-107">This quickstart steps through onboarding a Linux VM and deploying a LAMP stack with DSC.</span><span class="sxs-lookup"><span data-stu-id="90492-107">This quickstart steps through onboarding a Linux VM and deploying a LAMP stack with DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90492-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="90492-108">Prerequisites</span></span>

<span data-ttu-id="90492-109">To complete this quickstart, you need:</span><span class="sxs-lookup"><span data-stu-id="90492-109">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="90492-110">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="90492-110">An Azure subscription.</span></span> <span data-ttu-id="90492-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="90492-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="90492-112">An Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="90492-112">An Azure Automation account.</span></span> <span data-ttu-id="90492-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="90492-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="90492-114">An Azure Resource Manager VM (not Classic) running Red Hat Enterprise Linux, CentOS, or Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="90492-114">An Azure Resource Manager VM (not Classic) running Red Hat Enterprise Linux, CentOS, or Oracle Linux.</span></span> <span data-ttu-id="90492-115">For instructions on creating a VM, see [Create your first Linux virtual machine in the Azure portal](../virtual-machines/linux/quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="90492-115">For instructions on creating a VM, see [Create your first Linux virtual machine in the Azure portal](../virtual-machines/linux/quick-create-portal.md)</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="90492-116">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="90492-116">Log in to Azure</span></span>
<span data-ttu-id="90492-117">Log in to Azure at https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="90492-117">Log in to Azure at https://portal.azure.com</span></span>

## <a name="onboard-a-virtual-machine"></a><span data-ttu-id="90492-118">Onboard a virtual machine</span><span class="sxs-lookup"><span data-stu-id="90492-118">Onboard a virtual machine</span></span>
<span data-ttu-id="90492-119">There are many different methods to onboard a machine and enable Desired State Configuration.</span><span class="sxs-lookup"><span data-stu-id="90492-119">There are many different methods to onboard a machine and enable Desired State Configuration.</span></span> <span data-ttu-id="90492-120">This quickstart covers onboarding through an Automation account.</span><span class="sxs-lookup"><span data-stu-id="90492-120">This quickstart covers onboarding through an Automation account.</span></span> <span data-ttu-id="90492-121">You can learn more about different methods to onboard your machines to Desired State Configuration by reading the [onboarding](https://docs.microsoft.com/azure/automation/automation-dsc-onboarding) article.</span><span class="sxs-lookup"><span data-stu-id="90492-121">You can learn more about different methods to onboard your machines to Desired State Configuration by reading the [onboarding](https://docs.microsoft.com/azure/automation/automation-dsc-onboarding) article.</span></span>

1. <span data-ttu-id="90492-122">In the left pane of the Azure portal, select **Automation accounts**.</span><span class="sxs-lookup"><span data-stu-id="90492-122">In the left pane of the Azure portal, select **Automation accounts**.</span></span> <span data-ttu-id="90492-123">If it is not visible in the left pane, click **All services** and search for it in the resulting view.</span><span class="sxs-lookup"><span data-stu-id="90492-123">If it is not visible in the left pane, click **All services** and search for it in the resulting view.</span></span>
1. <span data-ttu-id="90492-124">In the list, select an Automation account.</span><span class="sxs-lookup"><span data-stu-id="90492-124">In the list, select an Automation account.</span></span>
1. <span data-ttu-id="90492-125">In the left pane of the Automation account, select **DSC Nodes**.</span><span class="sxs-lookup"><span data-stu-id="90492-125">In the left pane of the Automation account, select **DSC Nodes**.</span></span>
1. <span data-ttu-id="90492-126">Click the menu option to **Add Azure VM**</span><span class="sxs-lookup"><span data-stu-id="90492-126">Click the menu option to **Add Azure VM**</span></span>
1. <span data-ttu-id="90492-127">Find the virtual machine you would like to enable DSC for.</span><span class="sxs-lookup"><span data-stu-id="90492-127">Find the virtual machine you would like to enable DSC for.</span></span> <span data-ttu-id="90492-128">You can use the search field and filter options to find a specific virtual machine.</span><span class="sxs-lookup"><span data-stu-id="90492-128">You can use the search field and filter options to find a specific virtual machine.</span></span>
1. <span data-ttu-id="90492-129">Click on the virtual machine, and then select **Connect**</span><span class="sxs-lookup"><span data-stu-id="90492-129">Click on the virtual machine, and then select **Connect**</span></span>
1. <span data-ttu-id="90492-130">Select the DSC settings appropriate for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="90492-130">Select the DSC settings appropriate for the virtual machine.</span></span> <span data-ttu-id="90492-131">If you have already prepared a configuration, you can specify it as *Node Configuration Name*.</span><span class="sxs-lookup"><span data-stu-id="90492-131">If you have already prepared a configuration, you can specify it as *Node Configuration Name*.</span></span> <span data-ttu-id="90492-132">You can set the [configuration mode](https://docs.microsoft.com/powershell/dsc/metaconfig) to control the configuration behavior for the machine.</span><span class="sxs-lookup"><span data-stu-id="90492-132">You can set the [configuration mode](https://docs.microsoft.com/powershell/dsc/metaconfig) to control the configuration behavior for the machine.</span></span>
1. <span data-ttu-id="90492-133">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="90492-133">Click **OK**</span></span>

![Onboarding an Azure VM to DSC](./media/automation-quickstart-dsc-configuration/dsc-onboard-azure-vm.png)

<span data-ttu-id="90492-135">While the Desired State Configuration extension is deployed to the virtual machine, it shows *Connecting.*</span><span class="sxs-lookup"><span data-stu-id="90492-135">While the Desired State Configuration extension is deployed to the virtual machine, it shows *Connecting.*</span></span>

## <a name="import-modules"></a><span data-ttu-id="90492-136">Import modules</span><span class="sxs-lookup"><span data-stu-id="90492-136">Import modules</span></span>

<span data-ttu-id="90492-137">Modules contain DSC Resources and many can be found on the [PowerShell Gallery](https://www.powershellgallery.com).</span><span class="sxs-lookup"><span data-stu-id="90492-137">Modules contain DSC Resources and many can be found on the [PowerShell Gallery](https://www.powershellgallery.com).</span></span> <span data-ttu-id="90492-138">Any resources that are used in your configurations must be imported to the Automation Account before compiling.</span><span class="sxs-lookup"><span data-stu-id="90492-138">Any resources that are used in your configurations must be imported to the Automation Account before compiling.</span></span> <span data-ttu-id="90492-139">For this tutorial, the module named **nx** is required.</span><span class="sxs-lookup"><span data-stu-id="90492-139">For this tutorial, the module named **nx** is required.</span></span>

1. <span data-ttu-id="90492-140">In the left pane of the Automation account, select **Modules Gallery** (under Shared Resources).</span><span class="sxs-lookup"><span data-stu-id="90492-140">In the left pane of the Automation account, select **Modules Gallery** (under Shared Resources).</span></span>
1. <span data-ttu-id="90492-141">Search for the module that you would like to import by typing part of its name: *nx*</span><span class="sxs-lookup"><span data-stu-id="90492-141">Search for the module that you would like to import by typing part of its name: *nx*</span></span>
1. <span data-ttu-id="90492-142">Click on the module you would like to import</span><span class="sxs-lookup"><span data-stu-id="90492-142">Click on the module you would like to import</span></span>
1. <span data-ttu-id="90492-143">Click **Import**</span><span class="sxs-lookup"><span data-stu-id="90492-143">Click **Import**</span></span>

![Importing a DSC Module](./media/automation-quickstart-dsc-configuration/dsc-import-module-nx.png)

## <a name="import-the-configuration"></a><span data-ttu-id="90492-145">Import the configuration</span><span class="sxs-lookup"><span data-stu-id="90492-145">Import the configuration</span></span>

<span data-ttu-id="90492-146">This quickstart uses a DSC configuration that configures Apache HTTP Server, MySQL, and PHP on the machine.</span><span class="sxs-lookup"><span data-stu-id="90492-146">This quickstart uses a DSC configuration that configures Apache HTTP Server, MySQL, and PHP on the machine.</span></span>

<span data-ttu-id="90492-147">For information about DSC configurations, see [DSC configurations](https://docs.microsoft.com/powershell/dsc/configurations).</span><span class="sxs-lookup"><span data-stu-id="90492-147">For information about DSC configurations, see [DSC configurations](https://docs.microsoft.com/powershell/dsc/configurations).</span></span>

<span data-ttu-id="90492-148">In a text editor, type the following and save it locally as `LAMPServer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="90492-148">In a text editor, type the following and save it locally as `LAMPServer.ps1`.</span></span>

```powershell-interactive
configuration LAMPServer {
   Import-DSCResource -module "nx"

   Node localhost {

        $requiredPackages = @("httpd","mod_ssl","php","php-mysql","mariadb","mariadb-server")
        $enabledServices = @("httpd","mariadb")

        #Ensure packages are installed
        ForEach ($package in $requiredPackages){
            nxPackage $Package{
                Ensure = "Present"
                Name = $Package
                PackageManager = "yum"
            }
        }

        #Ensure daemons are enabled
        ForEach ($service in $enabledServices){
            nxService $service{
                Enabled = $true
                Name = $service
                Controller = "SystemD"
                State = "running"
            }
        }
   }
}
```

<span data-ttu-id="90492-149">To import the configuration:</span><span class="sxs-lookup"><span data-stu-id="90492-149">To import the configuration:</span></span>

1. <span data-ttu-id="90492-150">In the left pane of the Automation account, select **DSC Configurations**.</span><span class="sxs-lookup"><span data-stu-id="90492-150">In the left pane of the Automation account, select **DSC Configurations**.</span></span>
1. <span data-ttu-id="90492-151">Click the menu option to **Add a Configuration**</span><span class="sxs-lookup"><span data-stu-id="90492-151">Click the menu option to **Add a Configuration**</span></span>
1. <span data-ttu-id="90492-152">Select the *Configuration file* that you saved in the prior step</span><span class="sxs-lookup"><span data-stu-id="90492-152">Select the *Configuration file* that you saved in the prior step</span></span>
1. <span data-ttu-id="90492-153">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="90492-153">Click **OK**</span></span>

## <a name="compile-a-configuration"></a><span data-ttu-id="90492-154">Compile a configuration</span><span class="sxs-lookup"><span data-stu-id="90492-154">Compile a configuration</span></span>

<span data-ttu-id="90492-155">DSC Configurations must be compiled to a Node Configuration (MOF document) before being assigned to a node.</span><span class="sxs-lookup"><span data-stu-id="90492-155">DSC Configurations must be compiled to a Node Configuration (MOF document) before being assigned to a node.</span></span> <span data-ttu-id="90492-156">Compilation validates the configuration and allows for the input of parameter values.</span><span class="sxs-lookup"><span data-stu-id="90492-156">Compilation validates the configuration and allows for the input of parameter values.</span></span> <span data-ttu-id="90492-157">To learn more about compiling a configuration, see: [Compiling Configurations in Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-compile)</span><span class="sxs-lookup"><span data-stu-id="90492-157">To learn more about compiling a configuration, see: [Compiling Configurations in Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-compile)</span></span>

<span data-ttu-id="90492-158">To compile the configuration:</span><span class="sxs-lookup"><span data-stu-id="90492-158">To compile the configuration:</span></span>

1. <span data-ttu-id="90492-159">In the left pane of the Automation account, select **DSC Configurations**.</span><span class="sxs-lookup"><span data-stu-id="90492-159">In the left pane of the Automation account, select **DSC Configurations**.</span></span>
1. <span data-ttu-id="90492-160">Select the configuration you imported in a prior step, "LAMPServer"</span><span class="sxs-lookup"><span data-stu-id="90492-160">Select the configuration you imported in a prior step, "LAMPServer"</span></span>
1. <span data-ttu-id="90492-161">From the menu options, click **Compile** and then **Yes**</span><span class="sxs-lookup"><span data-stu-id="90492-161">From the menu options, click **Compile** and then **Yes**</span></span>
1. <span data-ttu-id="90492-162">In the Configuration view, you see a new *Compilation job* queued.</span><span class="sxs-lookup"><span data-stu-id="90492-162">In the Configuration view, you see a new *Compilation job* queued.</span></span> <span data-ttu-id="90492-163">When the job has completed successfully, you are ready to move on to the next step.</span><span class="sxs-lookup"><span data-stu-id="90492-163">When the job has completed successfully, you are ready to move on to the next step.</span></span> <span data-ttu-id="90492-164">If there are any failures, you can click on the Compilation job for details.</span><span class="sxs-lookup"><span data-stu-id="90492-164">If there are any failures, you can click on the Compilation job for details.</span></span>

![Compilation Job Status](./media/automation-quickstart-dsc-configuration/dsc-compilationjob.png)

## <a name="assign-a-node-configuration"></a><span data-ttu-id="90492-166">Assign a node configuration</span><span class="sxs-lookup"><span data-stu-id="90492-166">Assign a node configuration</span></span>

<span data-ttu-id="90492-167">A compiled *Node Configuration* can be assigned to DSC Nodes.</span><span class="sxs-lookup"><span data-stu-id="90492-167">A compiled *Node Configuration* can be assigned to DSC Nodes.</span></span> <span data-ttu-id="90492-168">Assignment applies the configuration to the machine and monitors (or auto-corrects) for any drift from that configuration.</span><span class="sxs-lookup"><span data-stu-id="90492-168">Assignment applies the configuration to the machine and monitors (or auto-corrects) for any drift from that configuration.</span></span>

1. <span data-ttu-id="90492-169">In the left pane of the Automation account, select **DSC Nodes**</span><span class="sxs-lookup"><span data-stu-id="90492-169">In the left pane of the Automation account, select **DSC Nodes**</span></span>
1. <span data-ttu-id="90492-170">Select the node you would like to assign a configuration to</span><span class="sxs-lookup"><span data-stu-id="90492-170">Select the node you would like to assign a configuration to</span></span>
1. <span data-ttu-id="90492-171">Click **Assign Node Configuration**</span><span class="sxs-lookup"><span data-stu-id="90492-171">Click **Assign Node Configuration**</span></span>
1. <span data-ttu-id="90492-172">Select the *Node Configuration* - **LAMPServer.localhost** -  to assign and click **OK**</span><span class="sxs-lookup"><span data-stu-id="90492-172">Select the *Node Configuration* - **LAMPServer.localhost** -  to assign and click **OK**</span></span>
1. <span data-ttu-id="90492-173">The compiled configuration is now be assigned to the node, and the node status changes to *Pending*.</span><span class="sxs-lookup"><span data-stu-id="90492-173">The compiled configuration is now be assigned to the node, and the node status changes to *Pending*.</span></span> <span data-ttu-id="90492-174">On the next periodic check, the node retrieves the configuration, apply it, and report status back.</span><span class="sxs-lookup"><span data-stu-id="90492-174">On the next periodic check, the node retrieves the configuration, apply it, and report status back.</span></span> <span data-ttu-id="90492-175">It can take up to 30 minutes for the node to retrieve the configuration, depending on the node's settings.</span><span class="sxs-lookup"><span data-stu-id="90492-175">It can take up to 30 minutes for the node to retrieve the configuration, depending on the node's settings.</span></span> <span data-ttu-id="90492-176">To force an immediate check, you can run the following command locally on the Linux virtual machine: `sudo /opt/microsoft/dsc/Scripts/PerformRequiredConfigurationChecks.py`</span><span class="sxs-lookup"><span data-stu-id="90492-176">To force an immediate check, you can run the following command locally on the Linux virtual machine: `sudo /opt/microsoft/dsc/Scripts/PerformRequiredConfigurationChecks.py`</span></span>

![Assigning a Node Configuration](./media/automation-quickstart-dsc-configuration/dsc-assign-node-configuration.png)

## <a name="viewing-node-status"></a><span data-ttu-id="90492-178">Viewing node status</span><span class="sxs-lookup"><span data-stu-id="90492-178">Viewing node status</span></span>

<span data-ttu-id="90492-179">The status of all managed nodes can be found in the **DSC Nodes** view of the Automation Account.</span><span class="sxs-lookup"><span data-stu-id="90492-179">The status of all managed nodes can be found in the **DSC Nodes** view of the Automation Account.</span></span> <span data-ttu-id="90492-180">You can filter the display by status, node configuration, or name search.</span><span class="sxs-lookup"><span data-stu-id="90492-180">You can filter the display by status, node configuration, or name search.</span></span> 

![DSC Node Status](./media/automation-quickstart-dsc-configuration/dsc-node-status.png)

## <a name="next-steps"></a><span data-ttu-id="90492-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="90492-182">Next steps</span></span>

<span data-ttu-id="90492-183">In this quickstart, you onboarded a Linux VM to DSC, created a configuration for a LAMP stack, and deployed it to the VM.</span><span class="sxs-lookup"><span data-stu-id="90492-183">In this quickstart, you onboarded a Linux VM to DSC, created a configuration for a LAMP stack, and deployed it to the VM.</span></span> <span data-ttu-id="90492-184">To learn how you can use Automation DSC to enable continuous deployment, continue to the article:</span><span class="sxs-lookup"><span data-stu-id="90492-184">To learn how you can use Automation DSC to enable continuous deployment, continue to the article:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="90492-185">Continuous deployment to a VM using DSC and Chocolatey</span><span class="sxs-lookup"><span data-stu-id="90492-185">Continuous deployment to a VM using DSC and Chocolatey</span></span>](./automation-dsc-cd-chocolatey.md)

* <span data-ttu-id="90492-186">To learn more about PowerShell Desired State Configuration, see [PowerShell Desired State Configuration Overview](https://docs.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="90492-186">To learn more about PowerShell Desired State Configuration, see [PowerShell Desired State Configuration Overview](https://docs.microsoft.com/powershell/dsc/overview).</span></span>
* <span data-ttu-id="90492-187">To learn more about managing Automation DSC from PowerShell, see [Azure PowerShell](https://docs.microsoft.com/powershell/module/azurerm.automation/?view=azurermps-5.0.0)</span><span class="sxs-lookup"><span data-stu-id="90492-187">To learn more about managing Automation DSC from PowerShell, see [Azure PowerShell](https://docs.microsoft.com/powershell/module/azurerm.automation/?view=azurermps-5.0.0)</span></span>
* <span data-ttu-id="90492-188">To learn how to forward DSC reports to Log Analytics for reporting and alerting, see [Forwarding DSC Reporting to Log Analytics](https://docs.microsoft.com/azure/automation/automation-dsc-diagnostics)</span><span class="sxs-lookup"><span data-stu-id="90492-188">To learn how to forward DSC reports to Log Analytics for reporting and alerting, see [Forwarding DSC Reporting to Log Analytics](https://docs.microsoft.com/azure/automation/automation-dsc-diagnostics)</span></span> 
