---
title: Connect Windows computers to Azure Log Analytics | Microsoft Docs
description: This article shows the steps to connect the Windows computers in your on-premises infrastructure to the Log Analytics service by using a customized version of the Microsoft Monitoring Agent (MMA).
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 86720f497fca9ba2c2e585ca888829644651c092
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552018"
---
# <a name="connect-windows-computers-to-the-log-analytics-service-in-azure"></a><span data-ttu-id="31a85-103">Connect Windows computers to the Log Analytics service in Azure</span><span class="sxs-lookup"><span data-stu-id="31a85-103">Connect Windows computers to the Log Analytics service in Azure</span></span>

<span data-ttu-id="31a85-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="31a85-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="31a85-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span><span class="sxs-lookup"><span data-stu-id="31a85-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span></span> <span data-ttu-id="31a85-106">Each agent can report to multiple workspaces.</span><span class="sxs-lookup"><span data-stu-id="31a85-106">Each agent can report to multiple workspaces.</span></span>

<span data-ttu-id="31a85-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="31a85-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="31a85-108">For virtual machines running in Azure you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="31a85-108">For virtual machines running in Azure you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="31a85-109">On computers with Internet connectivity, the agent will use the connection to the Internet to send data to OMS.</span><span class="sxs-lookup"><span data-stu-id="31a85-109">On computers with Internet connectivity, the agent will use the connection to the Internet to send data to OMS.</span></span> <span data-ttu-id="31a85-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="31a85-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="31a85-111">Connecting your Windows computers to OMS is straightforward using 3 simple steps:</span><span class="sxs-lookup"><span data-stu-id="31a85-111">Connecting your Windows computers to OMS is straightforward using 3 simple steps:</span></span>

1. <span data-ttu-id="31a85-112">Download the agent setup file from the OMS portal</span><span class="sxs-lookup"><span data-stu-id="31a85-112">Download the agent setup file from the OMS portal</span></span>
2. <span data-ttu-id="31a85-113">Install the agent using the method you choose</span><span class="sxs-lookup"><span data-stu-id="31a85-113">Install the agent using the method you choose</span></span>
3. <span data-ttu-id="31a85-114">Configure the agent or add additional workspaces, if necessary</span><span class="sxs-lookup"><span data-stu-id="31a85-114">Configure the agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="31a85-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span><span class="sxs-lookup"><span data-stu-id="31a85-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/oms-direct-agent-diagram.png)


## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="31a85-117">System requirements and required configuration</span><span class="sxs-lookup"><span data-stu-id="31a85-117">System requirements and required configuration</span></span>
<span data-ttu-id="31a85-118">Before you install or deploy agents, review the following details to ensure you meet necessary requirements.</span><span class="sxs-lookup"><span data-stu-id="31a85-118">Before you install or deploy agents, review the following details to ensure you meet necessary requirements.</span></span>

- <span data-ttu-id="31a85-119">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span><span class="sxs-lookup"><span data-stu-id="31a85-119">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="31a85-120">You'll need an OMS subscription.</span><span class="sxs-lookup"><span data-stu-id="31a85-120">You'll need an OMS subscription.</span></span>  <span data-ttu-id="31a85-121">For additional information, see [Get started with Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="31a85-121">For additional information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="31a85-122">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="31a85-122">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span></span> <span data-ttu-id="31a85-123">This connection can be direct, via a proxy, or through the OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="31a85-123">This connection can be direct, via a proxy, or through the OMS Gateway.</span></span>
- <span data-ttu-id="31a85-124">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span><span class="sxs-lookup"><span data-stu-id="31a85-124">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="31a85-125">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="31a85-125">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="31a85-126">The agent needs to use TCP port 443 for various resources.</span><span class="sxs-lookup"><span data-stu-id="31a85-126">The agent needs to use TCP port 443 for various resources.</span></span> <span data-ttu-id="31a85-127">For more information, see [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md).</span><span class="sxs-lookup"><span data-stu-id="31a85-127">For more information, see [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md).</span></span>

## <a name="download-the-agent-setup-file-from-oms"></a><span data-ttu-id="31a85-128">Download the agent setup file from OMS</span><span class="sxs-lookup"><span data-stu-id="31a85-128">Download the agent setup file from OMS</span></span>
1. <span data-ttu-id="31a85-129">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span><span class="sxs-lookup"><span data-stu-id="31a85-129">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span></span>  <span data-ttu-id="31a85-130">Click the **Connected Sources** tab at the top.</span><span class="sxs-lookup"><span data-stu-id="31a85-130">Click the **Connected Sources** tab at the top.</span></span>  
    <span data-ttu-id="31a85-131">![Connected Sources tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="31a85-131">![Connected Sources tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="31a85-132">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span><span class="sxs-lookup"><span data-stu-id="31a85-132">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span></span>
3. <span data-ttu-id="31a85-133">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span><span class="sxs-lookup"><span data-stu-id="31a85-133">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span></span>
4. <span data-ttu-id="31a85-134">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span><span class="sxs-lookup"><span data-stu-id="31a85-134">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span></span>     

## <a name="install-the-agent-using-setup"></a><span data-ttu-id="31a85-135">Install the agent using setup</span><span class="sxs-lookup"><span data-stu-id="31a85-135">Install the agent using setup</span></span>
1. <span data-ttu-id="31a85-136">Run Setup to install the agent on a computer that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="31a85-136">Run Setup to install the agent on a computer that you want to manage.</span></span>
2. <span data-ttu-id="31a85-137">On the Welcome page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="31a85-137">On the Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="31a85-138">On the License Terms page, read the license and then click **I Agree**.</span><span class="sxs-lookup"><span data-stu-id="31a85-138">On the License Terms page, read the license and then click **I Agree**.</span></span>
4. <span data-ttu-id="31a85-139">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="31a85-139">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="31a85-140">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span><span class="sxs-lookup"><span data-stu-id="31a85-140">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span></span> <span data-ttu-id="31a85-141">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="31a85-141">Click **Next**.</span></span>   
    - <span data-ttu-id="31a85-142">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="31a85-142">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="31a85-143">![paste Workspace ID and Primary Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="31a85-143">![paste Workspace ID and Primary Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="31a85-144">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="31a85-144">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="31a85-145">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="31a85-145">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="31a85-146">![management group configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="31a85-146">![management group configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="31a85-147">On the Ready to Install page, review your choices and then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="31a85-147">On the Ready to Install page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="31a85-148">On the Configuration completed successfully page, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="31a85-148">On the Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="31a85-149">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span><span class="sxs-lookup"><span data-stu-id="31a85-149">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="31a85-150">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="31a85-150">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span></span> <span data-ttu-id="31a85-151">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span><span class="sxs-lookup"><span data-stu-id="31a85-151">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span></span>

## <a name="install-the-agent-using-the-command-line"></a><span data-ttu-id="31a85-152">Install the agent using the command line</span><span class="sxs-lookup"><span data-stu-id="31a85-152">Install the agent using the command line</span></span>
- <span data-ttu-id="31a85-153">Modify and then use the following example to install the agent using the command line.</span><span class="sxs-lookup"><span data-stu-id="31a85-153">Modify and then use the following example to install the agent using the command line.</span></span> <span data-ttu-id="31a85-154">The example performs a fully silent installation.</span><span class="sxs-lookup"><span data-stu-id="31a85-154">The example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="31a85-155">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span><span class="sxs-lookup"><span data-stu-id="31a85-155">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span></span> <span data-ttu-id="31a85-156">See the next section to upgrade an agent.</span><span class="sxs-lookup"><span data-stu-id="31a85-156">See the next section to upgrade an agent.</span></span>

    ```
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="31a85-157">The agent uses IExpress as its self-extractor using the `/c` command.</span><span class="sxs-lookup"><span data-stu-id="31a85-157">The agent uses IExpress as its self-extractor using the `/c` command.</span></span> <span data-ttu-id="31a85-158">You can the command line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span><span class="sxs-lookup"><span data-stu-id="31a85-158">You can the command line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>

## <a name="upgrade-the-agent-and-add-a-workspace-using-a-script"></a><span data-ttu-id="31a85-159">Upgrade the agent and add a workspace using a script</span><span class="sxs-lookup"><span data-stu-id="31a85-159">Upgrade the agent and add a workspace using a script</span></span>
<span data-ttu-id="31a85-160">You can upgrade an agent and add a workspace using the Log Analytics scripting API with the following PowerShell example.</span><span class="sxs-lookup"><span data-stu-id="31a85-160">You can upgrade an agent and add a workspace using the Log Analytics scripting API with the following PowerShell example.</span></span>

```
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="31a85-161">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="31a85-161">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-the-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="31a85-162">Install the agent using DSC in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="31a85-162">Install the agent using DSC in Azure Automation</span></span>

<span data-ttu-id="31a85-163">You can use the following script example to install the agent using DSC in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="31a85-163">You can use the following script example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="31a85-164">The example installs the 64-bit agent, identified by the `URI` value.</span><span class="sxs-lookup"><span data-stu-id="31a85-164">The example installs the 64-bit agent, identified by the `URI` value.</span></span> <span data-ttu-id="31a85-165">You can also use the 32-bit version by replacing the URI value.</span><span class="sxs-lookup"><span data-stu-id="31a85-165">You can also use the 32-bit version by replacing the URI value.</span></span> <span data-ttu-id="31a85-166">The URIs for both versions are:</span><span class="sxs-lookup"><span data-stu-id="31a85-166">The URIs for both versions are:</span></span>

- <span data-ttu-id="31a85-167">Windows 64 bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="31a85-167">Windows 64 bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="31a85-168">Windows 32 bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="31a85-168">Windows 32 bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="31a85-169">This procedure and script example will not upgrade an existing agent.</span><span class="sxs-lookup"><span data-stu-id="31a85-169">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="31a85-170">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="31a85-170">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="31a85-171">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="31a85-171">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="31a85-172">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span><span class="sxs-lookup"><span data-stu-id="31a85-172">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span></span>
3.  <span data-ttu-id="31a85-173">Use the script below and save it as MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="31a85-173">Use the script below and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="31a85-174">Modify and then use the following example to install the agent using DSC in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="31a85-174">Modify and then use the following example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="31a85-175">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31a85-175">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="31a85-176">Assign a node to the configuration.</span><span class="sxs-lookup"><span data-stu-id="31a85-176">Assign a node to the configuration.</span></span> <span data-ttu-id="31a85-177">Within 15 minutes the node will check its configuration and the MMA will be pushed to the node.</span><span class="sxs-lookup"><span data-stu-id="31a85-177">Within 15 minutes the node will check its configuration and the MMA will be pushed to the node.</span></span>

```
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-the-latest-productid-value"></a><span data-ttu-id="31a85-178">Get the latest ProductId value</span><span class="sxs-lookup"><span data-stu-id="31a85-178">Get the latest ProductId value</span></span>

<span data-ttu-id="31a85-179">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span><span class="sxs-lookup"><span data-stu-id="31a85-179">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span></span> <span data-ttu-id="31a85-180">When an updated version of each agent is published, the ProductId value changes.</span><span class="sxs-lookup"><span data-stu-id="31a85-180">When an updated version of each agent is published, the ProductId value changes.</span></span> <span data-ttu-id="31a85-181">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span><span class="sxs-lookup"><span data-stu-id="31a85-181">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span></span> <span data-ttu-id="31a85-182">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span><span class="sxs-lookup"><span data-stu-id="31a85-182">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span></span> <span data-ttu-id="31a85-183">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="31a85-183">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span></span>

```
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="31a85-184">Configure an agent manually or add additional workspaces</span><span class="sxs-lookup"><span data-stu-id="31a85-184">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="31a85-185">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span><span class="sxs-lookup"><span data-stu-id="31a85-185">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span></span> <span data-ttu-id="31a85-186">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span><span class="sxs-lookup"><span data-stu-id="31a85-186">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="31a85-187">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span><span class="sxs-lookup"><span data-stu-id="31a85-187">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="31a85-188">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span><span class="sxs-lookup"><span data-stu-id="31a85-188">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="31a85-189">Click **Add** to open the **Add a Log Analytics Workspace** box.</span><span class="sxs-lookup"><span data-stu-id="31a85-189">Click **Add** to open the **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="31a85-190">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="31a85-190">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span></span>  
    <span data-ttu-id="31a85-191">![configure Operational Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="31a85-191">![configure Operational Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="31a85-192">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span><span class="sxs-lookup"><span data-stu-id="31a85-192">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="to-disable-an-agent"></a><span data-ttu-id="31a85-193">To disable an agent</span><span class="sxs-lookup"><span data-stu-id="31a85-193">To disable an agent</span></span>
1. <span data-ttu-id="31a85-194">After installing the agent, open **Control Panel**.</span><span class="sxs-lookup"><span data-stu-id="31a85-194">After installing the agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="31a85-195">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span><span class="sxs-lookup"><span data-stu-id="31a85-195">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="31a85-196">Select a workspace and then click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="31a85-196">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="31a85-197">Repeat this step for all other workspaces.</span><span class="sxs-lookup"><span data-stu-id="31a85-197">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="31a85-198">Optionally, configure agents to report to an Operations Manager management group</span><span class="sxs-lookup"><span data-stu-id="31a85-198">Optionally, configure agents to report to an Operations Manager management group</span></span>

<span data-ttu-id="31a85-199">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span><span class="sxs-lookup"><span data-stu-id="31a85-199">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span></span>

### <a name="to-configure-mma-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="31a85-200">To configure MMA agents to report to an Operations Manager management group</span><span class="sxs-lookup"><span data-stu-id="31a85-200">To configure MMA agents to report to an Operations Manager management group</span></span>
1.  <span data-ttu-id="31a85-201">On the computer where the agent is installed, open **Control Panel**.</span><span class="sxs-lookup"><span data-stu-id="31a85-201">On the computer where the agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="31a85-202">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span><span class="sxs-lookup"><span data-stu-id="31a85-202">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>  
    <span data-ttu-id="31a85-203">![Microsoft Monitoring Agent Operations Manager tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="31a85-203">![Microsoft Monitoring Agent Operations Manager tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="31a85-204">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span><span class="sxs-lookup"><span data-stu-id="31a85-204">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="31a85-205">Click **Add** to open the **Add a Management Group** dialog box.</span><span class="sxs-lookup"><span data-stu-id="31a85-205">Click **Add** to open the **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="31a85-206">![Microsoft Monitoring Agent Add a Management Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="31a85-206">![Microsoft Monitoring Agent Add a Management Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="31a85-207">In **Management group name** box, type the name of your management group.</span><span class="sxs-lookup"><span data-stu-id="31a85-207">In **Management group name** box, type the name of your management group.</span></span>
6.  <span data-ttu-id="31a85-208">In the **Primary management server** box, type the computer name of the primary management server.</span><span class="sxs-lookup"><span data-stu-id="31a85-208">In the **Primary management server** box, type the computer name of the primary management server.</span></span>
7.  <span data-ttu-id="31a85-209">In the **Management server port** box, type the TCP port number.</span><span class="sxs-lookup"><span data-stu-id="31a85-209">In the **Management server port** box, type the TCP port number.</span></span>
8.  <span data-ttu-id="31a85-210">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span><span class="sxs-lookup"><span data-stu-id="31a85-210">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="31a85-211">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span><span class="sxs-lookup"><span data-stu-id="31a85-211">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>

## <a name="optionally-configure-agents-to-use-the-oms-gateway"></a><span data-ttu-id="31a85-212">Optionally, configure agents to use the OMS Gateway</span><span class="sxs-lookup"><span data-stu-id="31a85-212">Optionally, configure agents to use the OMS Gateway</span></span>

<span data-ttu-id="31a85-213">If you have servers or clients that do not have a connection to the Internet, you can still have them send data to OMS by using the OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="31a85-213">If you have servers or clients that do not have a connection to the Internet, you can still have them send data to OMS by using the OMS Gateway.</span></span>  <span data-ttu-id="31a85-214">When you use the Gateway, all data from agents is sent through a single server that has access to the Internet.</span><span class="sxs-lookup"><span data-stu-id="31a85-214">When you use the Gateway, all data from agents is sent through a single server that has access to the Internet.</span></span> <span data-ttu-id="31a85-215">The Gateway transfers data from the agents to OMS directly without analyzing any of the data that is transferred.</span><span class="sxs-lookup"><span data-stu-id="31a85-215">The Gateway transfers data from the agents to OMS directly without analyzing any of the data that is transferred.</span></span>

<span data-ttu-id="31a85-216">See [OMS Gateway](log-analytics-oms-gateway.md) to learn more about the Gateway, including setup, and configuration.</span><span class="sxs-lookup"><span data-stu-id="31a85-216">See [OMS Gateway](log-analytics-oms-gateway.md) to learn more about the Gateway, including setup, and configuration.</span></span>

<span data-ttu-id="31a85-217">For information about how to configure your agents to use a proxy server, which in this case is the OMS Gateway, see [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md).</span><span class="sxs-lookup"><span data-stu-id="31a85-217">For information about how to configure your agents to use a proxy server, which in this case is the OMS Gateway, see [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md).</span></span>

## <a name="optionally-configure-proxy-and-firewall-settings"></a><span data-ttu-id="31a85-218">Optionally, configure proxy and firewall settings</span><span class="sxs-lookup"><span data-stu-id="31a85-218">Optionally, configure proxy and firewall settings</span></span>
<span data-ttu-id="31a85-219">If you have proxy servers or firewalls in your environment that restrict access to the Internet, see [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md) to enable your agents to communicate to the OMS service.</span><span class="sxs-lookup"><span data-stu-id="31a85-219">If you have proxy servers or firewalls in your environment that restrict access to the Internet, see [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md) to enable your agents to communicate to the OMS service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31a85-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="31a85-220">Next steps</span></span>

- <span data-ttu-id="31a85-221">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span><span class="sxs-lookup"><span data-stu-id="31a85-221">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
- <span data-ttu-id="31a85-222">[Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md) if your organization uses a proxy server or firewall so that agents can communicate with the Log Analytics service.</span><span class="sxs-lookup"><span data-stu-id="31a85-222">[Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md) if your organization uses a proxy server or firewall so that agents can communicate with the Log Analytics service.</span></span>








