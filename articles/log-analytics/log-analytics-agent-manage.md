---
title: Managing the Azure Log Analytics Agent | Microsoft Docs
description: This article describes the different management tasks that you will typically perform during the lifecycle of the Microsoft Monitoring Agent (MMA) deployed on a machine.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/30/2018
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 908418dffaffc25be320bd0008edf03493aa4e55
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871614"
---
# <a name="managing-and-maintaining-the-log-analytics-agent-for-windows-and-linux"></a><span data-ttu-id="8115d-103">Managing and maintaining the Log Analytics agent for Windows and Linux</span><span class="sxs-lookup"><span data-stu-id="8115d-103">Managing and maintaining the Log Analytics agent for Windows and Linux</span></span>

<span data-ttu-id="8115d-104">After initial deployment of the Windows or Linux agent for Log Analytics, you may need to reconfigure the agent, or remove it from the computer if has reached the retirement stage in its lifecycle.</span><span class="sxs-lookup"><span data-stu-id="8115d-104">After initial deployment of the Windows or Linux agent for Log Analytics, you may need to reconfigure the agent, or remove it from the computer if has reached the retirement stage in its lifecycle.</span></span>  <span data-ttu-id="8115d-105">You can easily manage these routine maintenance tasks manually or through automation, which reduces both operational error and expenses.</span><span class="sxs-lookup"><span data-stu-id="8115d-105">You can easily manage these routine maintenance tasks manually or through automation, which reduces both operational error and expenses.</span></span>

## <a name="adding-or-removing-a-workspace"></a><span data-ttu-id="8115d-106">Adding or removing a workspace</span><span class="sxs-lookup"><span data-stu-id="8115d-106">Adding or removing a workspace</span></span> 

### <a name="windows-agent"></a><span data-ttu-id="8115d-107">Windows agent</span><span class="sxs-lookup"><span data-stu-id="8115d-107">Windows agent</span></span>

#### <a name="update-settings-from-control-panel"></a><span data-ttu-id="8115d-108">Update settings from Control Panel</span><span class="sxs-lookup"><span data-stu-id="8115d-108">Update settings from Control Panel</span></span>

1. <span data-ttu-id="8115d-109">Sign on to the computer with an account that has administrative rights.</span><span class="sxs-lookup"><span data-stu-id="8115d-109">Sign on to the computer with an account that has administrative rights.</span></span>
2. <span data-ttu-id="8115d-110">Open **Control Panel**.</span><span class="sxs-lookup"><span data-stu-id="8115d-110">Open **Control Panel**.</span></span>
3. <span data-ttu-id="8115d-111">Select **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span><span class="sxs-lookup"><span data-stu-id="8115d-111">Select **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>
4. <span data-ttu-id="8115d-112">If removing a workspace, select it and then click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="8115d-112">If removing a workspace, select it and then click **Remove**.</span></span> <span data-ttu-id="8115d-113">Repeat this step for any other workspace you want the agent to stop reporting to.</span><span class="sxs-lookup"><span data-stu-id="8115d-113">Repeat this step for any other workspace you want the agent to stop reporting to.</span></span>
5. <span data-ttu-id="8115d-114">If adding a workspace, click **Add** and on the **Add a Log Analytics Workspace** dialog box, paste the Workspace ID and Workspace Key (Primary Key).</span><span class="sxs-lookup"><span data-stu-id="8115d-114">If adding a workspace, click **Add** and on the **Add a Log Analytics Workspace** dialog box, paste the Workspace ID and Workspace Key (Primary Key).</span></span> <span data-ttu-id="8115d-115">If the computer should report to a Log Analytics workspace in Azure Government cloud, select Azure US Government from the Azure Cloud drop-down list.</span><span class="sxs-lookup"><span data-stu-id="8115d-115">If the computer should report to a Log Analytics workspace in Azure Government cloud, select Azure US Government from the Azure Cloud drop-down list.</span></span> 
6. <span data-ttu-id="8115d-116">Click **OK** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="8115d-116">Click **OK** to save your changes.</span></span>

#### <a name="remove-a-workspace-using-powershell"></a><span data-ttu-id="8115d-117">Remove a workspace using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8115d-117">Remove a workspace using PowerShell</span></span> 

```PowerShell
$workspaceId = "<Your workspace Id>"
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.RemoveCloudWorkspace($workspaceId)
$mma.ReloadConfiguration()
```

#### <a name="add-a-workspace-in-azure-commercial-using-powershell"></a><span data-ttu-id="8115d-118">Add a workspace in Azure commercial using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8115d-118">Add a workspace in Azure commercial using PowerShell</span></span> 

```PowerShell
$workspaceId = "<Your workspace Id>"
$workspaceKey = "<Your workspace Key>”
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

#### <a name="add-a-workspace-in-azure-for-us-government-using-powershell"></a><span data-ttu-id="8115d-119">Add a workspace in Azure for US Government using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8115d-119">Add a workspace in Azure for US Government using PowerShell</span></span> 

```PowerShell
$workspaceId = "<Your workspace Id>"
$workspaceKey = "<Your workspace Key>”
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
><span data-ttu-id="8115d-120">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace` and `RemoveCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="8115d-120">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace` and `RemoveCloudWorkspace`.</span></span>
>

### <a name="linux-agent"></a><span data-ttu-id="8115d-121">Linux agent</span><span class="sxs-lookup"><span data-stu-id="8115d-121">Linux agent</span></span>
<span data-ttu-id="8115d-122">The following steps demonstrate how to reconfigure the Linux agent if you decide to register it with a different workspace or want to remove a workspace from its configuration.</span><span class="sxs-lookup"><span data-stu-id="8115d-122">The following steps demonstrate how to reconfigure the Linux agent if you decide to register it with a different workspace or want to remove a workspace from its configuration.</span></span>  

1.  <span data-ttu-id="8115d-123">To verify it is registered to a workspace, run the following command.</span><span class="sxs-lookup"><span data-stu-id="8115d-123">To verify it is registered to a workspace, run the following command.</span></span>

    `/opt/microsoft/omsagent/bin/omsadmin.sh -l` 

    <span data-ttu-id="8115d-124">It should return a status similar to the following example -</span><span class="sxs-lookup"><span data-stu-id="8115d-124">It should return a status similar to the following example -</span></span> 

    `Primary Workspace: <workspaceId>   Status: Onboarded(OMSAgent Running)`

    <span data-ttu-id="8115d-125">It is important that the status also shows the agent is running, otherwise the following steps to reconfigure the agent will not complete successfully.</span><span class="sxs-lookup"><span data-stu-id="8115d-125">It is important that the status also shows the agent is running, otherwise the following steps to reconfigure the agent will not complete successfully.</span></span>  

2. <span data-ttu-id="8115d-126">If it is already registered with a workspace, remove the registered workspace by running the following command.</span><span class="sxs-lookup"><span data-stu-id="8115d-126">If it is already registered with a workspace, remove the registered workspace by running the following command.</span></span>  <span data-ttu-id="8115d-127">Otherwise if it is not registered, proceed to the next step.</span><span class="sxs-lookup"><span data-stu-id="8115d-127">Otherwise if it is not registered, proceed to the next step.</span></span>

    `/opt/microsoft/omsagent/bin/omsadmin.sh -X`  
    
3. <span data-ttu-id="8115d-128">To register with a different workspace, run the command `/opt/microsoft/omsagent/bin/omsadmin.sh -w <workspace id> -s <shared key> [-d <top level domain>]`</span><span class="sxs-lookup"><span data-stu-id="8115d-128">To register with a different workspace, run the command `/opt/microsoft/omsagent/bin/omsadmin.sh -w <workspace id> -s <shared key> [-d <top level domain>]`</span></span> 
4. <span data-ttu-id="8115d-129">To verify your changes took affect, run the command.</span><span class="sxs-lookup"><span data-stu-id="8115d-129">To verify your changes took affect, run the command.</span></span>

    `/opt/microsoft/omsagent/bin/omsadmin.sh -l` 

    <span data-ttu-id="8115d-130">It should return a status similar to the following example -</span><span class="sxs-lookup"><span data-stu-id="8115d-130">It should return a status similar to the following example -</span></span> 

    `Primary Workspace: <workspaceId>   Status: Onboarded(OMSAgent Running)`

<span data-ttu-id="8115d-131">The agent service does not need to be restarted in order for the changes to take effect.</span><span class="sxs-lookup"><span data-stu-id="8115d-131">The agent service does not need to be restarted in order for the changes to take effect.</span></span>

## <a name="update-proxy-settings"></a><span data-ttu-id="8115d-132">Update proxy settings</span><span class="sxs-lookup"><span data-stu-id="8115d-132">Update proxy settings</span></span> 
<span data-ttu-id="8115d-133">To configure the agent to communicate to the service through a proxy server or [OMS Gateway](log-analytics-oms-gateway.md) after deployment, use one of the following methods to complete this task.</span><span class="sxs-lookup"><span data-stu-id="8115d-133">To configure the agent to communicate to the service through a proxy server or [OMS Gateway](log-analytics-oms-gateway.md) after deployment, use one of the following methods to complete this task.</span></span>

### <a name="windows-agent"></a><span data-ttu-id="8115d-134">Windows agent</span><span class="sxs-lookup"><span data-stu-id="8115d-134">Windows agent</span></span>

#### <a name="update-settings-using-control-panel"></a><span data-ttu-id="8115d-135">Update settings using Control Panel</span><span class="sxs-lookup"><span data-stu-id="8115d-135">Update settings using Control Panel</span></span>

1. <span data-ttu-id="8115d-136">Sign on to the computer with an account that has administrative rights.</span><span class="sxs-lookup"><span data-stu-id="8115d-136">Sign on to the computer with an account that has administrative rights.</span></span>
2. <span data-ttu-id="8115d-137">Open **Control Panel**.</span><span class="sxs-lookup"><span data-stu-id="8115d-137">Open **Control Panel**.</span></span>
3. <span data-ttu-id="8115d-138">Select **Microsoft Monitoring Agent** and then click the **Proxy Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="8115d-138">Select **Microsoft Monitoring Agent** and then click the **Proxy Settings** tab.</span></span>
4. <span data-ttu-id="8115d-139">Click **Use a proxy server** and provide the URL and port number of the proxy server or gateway.</span><span class="sxs-lookup"><span data-stu-id="8115d-139">Click **Use a proxy server** and provide the URL and port number of the proxy server or gateway.</span></span> <span data-ttu-id="8115d-140">If your proxy server or OMS Gateway requires authentication, type the username and password to authenticate and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8115d-140">If your proxy server or OMS Gateway requires authentication, type the username and password to authenticate and then click **OK**.</span></span> 

#### <a name="update-settings-using-powershell"></a><span data-ttu-id="8115d-141">Update settings using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8115d-141">Update settings using PowerShell</span></span> 

<span data-ttu-id="8115d-142">Copy the following sample PowerShell code, update it with information specific to your environment, and save it with a PS1 file name extension.</span><span class="sxs-lookup"><span data-stu-id="8115d-142">Copy the following sample PowerShell code, update it with information specific to your environment, and save it with a PS1 file name extension.</span></span>  <span data-ttu-id="8115d-143">Run the script on each computer that connects directly to the Log Analytics service.</span><span class="sxs-lookup"><span data-stu-id="8115d-143">Run the script on each computer that connects directly to the Log Analytics service.</span></span>

```PowerShell
param($ProxyDomainName="https://proxy.contoso.com:30443", $cred=(Get-Credential))

# First we get the Health Service configuration object.  We need to determine if we
#have the right update rollup with the API we need.  If not, no need to run the rest of the script.
$healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

$proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

if (!$proxyMethod)
{
     Write-Output 'Health Service proxy API not present, will not update settings.'
     return
}

Write-Output "Clearing proxy settings."
$healthServiceSettings.SetProxyInfo('', '', '')

$ProxyUserName = $cred.username

Write-Output "Setting proxy to $ProxyDomainName with proxy username $ProxyUserName."
$healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)
```  

### <a name="linux-agent"></a><span data-ttu-id="8115d-144">Linux agent</span><span class="sxs-lookup"><span data-stu-id="8115d-144">Linux agent</span></span>
<span data-ttu-id="8115d-145">Perform the following steps if your Linux computers need to communicate through a proxy server or OMS Gateway to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8115d-145">Perform the following steps if your Linux computers need to communicate through a proxy server or OMS Gateway to Log Analytics.</span></span>  <span data-ttu-id="8115d-146">The proxy configuration value has the following syntax `[protocol://][user:password@]proxyhost[:port]`.</span><span class="sxs-lookup"><span data-stu-id="8115d-146">The proxy configuration value has the following syntax `[protocol://][user:password@]proxyhost[:port]`.</span></span>  <span data-ttu-id="8115d-147">The *proxyhost* property accepts a fully qualified domain name or IP address of the proxy server.</span><span class="sxs-lookup"><span data-stu-id="8115d-147">The *proxyhost* property accepts a fully qualified domain name or IP address of the proxy server.</span></span>

1. <span data-ttu-id="8115d-148">Edit the file `/etc/opt/microsoft/omsagent/proxy.conf` by running the following commands and change the values to your specific settings.</span><span class="sxs-lookup"><span data-stu-id="8115d-148">Edit the file `/etc/opt/microsoft/omsagent/proxy.conf` by running the following commands and change the values to your specific settings.</span></span>

    ```
    proxyconf="https://proxyuser:proxypassword@proxyserver01:30443"
    sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
    sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf 
    ```

2. <span data-ttu-id="8115d-149">Restart the agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="8115d-149">Restart the agent by running the following command:</span></span> 

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
    ``` 

## <a name="uninstall-agent"></a><span data-ttu-id="8115d-150">Uninstall agent</span><span class="sxs-lookup"><span data-stu-id="8115d-150">Uninstall agent</span></span>
<span data-ttu-id="8115d-151">Use one of the following procedures to uninstall the Windows or Linux agent using the command-line or setup wizard.</span><span class="sxs-lookup"><span data-stu-id="8115d-151">Use one of the following procedures to uninstall the Windows or Linux agent using the command-line or setup wizard.</span></span>

### <a name="windows-agent"></a><span data-ttu-id="8115d-152">Windows agent</span><span class="sxs-lookup"><span data-stu-id="8115d-152">Windows agent</span></span>

#### <a name="uninstall-from-control-panel"></a><span data-ttu-id="8115d-153">Uninstall from Control Panel</span><span class="sxs-lookup"><span data-stu-id="8115d-153">Uninstall from Control Panel</span></span>
1. <span data-ttu-id="8115d-154">Sign on to the computer with an account that has administrative rights.</span><span class="sxs-lookup"><span data-stu-id="8115d-154">Sign on to the computer with an account that has administrative rights.</span></span>  
2. <span data-ttu-id="8115d-155">In **Control Panel**, click **Programs and Features**.</span><span class="sxs-lookup"><span data-stu-id="8115d-155">In **Control Panel**, click **Programs and Features**.</span></span>
3. <span data-ttu-id="8115d-156">In **Programs and Features**, click **Microsoft Monitoring Agent**, click **Uninstall**, and then click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="8115d-156">In **Programs and Features**, click **Microsoft Monitoring Agent**, click **Uninstall**, and then click **Yes**.</span></span>

>[!NOTE]
><span data-ttu-id="8115d-157">The Agent Setup Wizard can also be run by double-clicking **MMASetup-<platform>.exe**, which is available for download from a workspace in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8115d-157">The Agent Setup Wizard can also be run by double-clicking **MMASetup-<platform>.exe**, which is available for download from a workspace in the Azure portal.</span></span>

#### <a name="uninstall-from-the-command-line"></a><span data-ttu-id="8115d-158">Uninstall from the command line</span><span class="sxs-lookup"><span data-stu-id="8115d-158">Uninstall from the command line</span></span>
<span data-ttu-id="8115d-159">The downloaded file for the agent is a self-contained installation package created with IExpress.</span><span class="sxs-lookup"><span data-stu-id="8115d-159">The downloaded file for the agent is a self-contained installation package created with IExpress.</span></span>  <span data-ttu-id="8115d-160">The setup program for the agent and supporting files are contained in the package and need to be extracted in order to properly uninstall using the command line shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="8115d-160">The setup program for the agent and supporting files are contained in the package and need to be extracted in order to properly uninstall using the command line shown in the following example.</span></span> 

1. <span data-ttu-id="8115d-161">Sign on to the computer with an account that has administrative rights.</span><span class="sxs-lookup"><span data-stu-id="8115d-161">Sign on to the computer with an account that has administrative rights.</span></span>  
2. <span data-ttu-id="8115d-162">To extract the agent installation files, from an elevated command prompt run `extract MMASetup-<platform>.exe` and it will prompt you for the path to extract files to.</span><span class="sxs-lookup"><span data-stu-id="8115d-162">To extract the agent installation files, from an elevated command prompt run `extract MMASetup-<platform>.exe` and it will prompt you for the path to extract files to.</span></span>  <span data-ttu-id="8115d-163">Alternatively, you can specify the path by passing the arguments `extract MMASetup-<platform>.exe /c:<Path> /t:<Path>`.</span><span class="sxs-lookup"><span data-stu-id="8115d-163">Alternatively, you can specify the path by passing the arguments `extract MMASetup-<platform>.exe /c:<Path> /t:<Path>`.</span></span>  <span data-ttu-id="8115d-164">For more information on the command-line swtiches supported by IExpress, see [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span><span class="sxs-lookup"><span data-stu-id="8115d-164">For more information on the command-line swtiches supported by IExpress, see [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>
3. <span data-ttu-id="8115d-165">At the prompt, type `%WinDir%\System32\msiexec.exe /x <Path>:\MOMAgent.msi /qb`.</span><span class="sxs-lookup"><span data-stu-id="8115d-165">At the prompt, type `%WinDir%\System32\msiexec.exe /x <Path>:\MOMAgent.msi /qb`.</span></span>  

### <a name="linux-agent"></a><span data-ttu-id="8115d-166">Linux agent</span><span class="sxs-lookup"><span data-stu-id="8115d-166">Linux agent</span></span>
<span data-ttu-id="8115d-167">To remove the agent, run the following command on the Linux computer.</span><span class="sxs-lookup"><span data-stu-id="8115d-167">To remove the agent, run the following command on the Linux computer.</span></span>  <span data-ttu-id="8115d-168">The *--purge* argument completely removes the agent and its configuration.</span><span class="sxs-lookup"><span data-stu-id="8115d-168">The *--purge* argument completely removes the agent and its configuration.</span></span>

   `wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh --purge`

## <a name="configure-agent-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="8115d-169">Configure agent to report to an Operations Manager management group</span><span class="sxs-lookup"><span data-stu-id="8115d-169">Configure agent to report to an Operations Manager management group</span></span>

### <a name="windows-agent"></a><span data-ttu-id="8115d-170">Windows agent</span><span class="sxs-lookup"><span data-stu-id="8115d-170">Windows agent</span></span>
<span data-ttu-id="8115d-171">Perform the following steps to configure the OMS Agent for Windows to report to a System Center Operations Manager management group.</span><span class="sxs-lookup"><span data-stu-id="8115d-171">Perform the following steps to configure the OMS Agent for Windows to report to a System Center Operations Manager management group.</span></span> 

1. <span data-ttu-id="8115d-172">Sign on to the computer with an account that has administrative rights.</span><span class="sxs-lookup"><span data-stu-id="8115d-172">Sign on to the computer with an account that has administrative rights.</span></span>
2. <span data-ttu-id="8115d-173">Open **Control Panel**.</span><span class="sxs-lookup"><span data-stu-id="8115d-173">Open **Control Panel**.</span></span> 
3. <span data-ttu-id="8115d-174">Click **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span><span class="sxs-lookup"><span data-stu-id="8115d-174">Click **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>
4. <span data-ttu-id="8115d-175">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span><span class="sxs-lookup"><span data-stu-id="8115d-175">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
5. <span data-ttu-id="8115d-176">Click **Add** to open the **Add a Management Group** dialog box.</span><span class="sxs-lookup"><span data-stu-id="8115d-176">Click **Add** to open the **Add a Management Group** dialog box.</span></span>
6. <span data-ttu-id="8115d-177">In **Management group name** field, type the name of your management group.</span><span class="sxs-lookup"><span data-stu-id="8115d-177">In **Management group name** field, type the name of your management group.</span></span>
7. <span data-ttu-id="8115d-178">In the **Primary management server** field, type the computer name of the primary management server.</span><span class="sxs-lookup"><span data-stu-id="8115d-178">In the **Primary management server** field, type the computer name of the primary management server.</span></span>
8. <span data-ttu-id="8115d-179">In the **Management server port** field, type the TCP port number.</span><span class="sxs-lookup"><span data-stu-id="8115d-179">In the **Management server port** field, type the TCP port number.</span></span>
9. <span data-ttu-id="8115d-180">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span><span class="sxs-lookup"><span data-stu-id="8115d-180">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
10. <span data-ttu-id="8115d-181">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span><span class="sxs-lookup"><span data-stu-id="8115d-181">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>

### <a name="linux-agent"></a><span data-ttu-id="8115d-182">Linux agent</span><span class="sxs-lookup"><span data-stu-id="8115d-182">Linux agent</span></span>
<span data-ttu-id="8115d-183">Perform the following steps to configure the OMS Agent for Linux to report to a System Center Operations Manager management group.</span><span class="sxs-lookup"><span data-stu-id="8115d-183">Perform the following steps to configure the OMS Agent for Linux to report to a System Center Operations Manager management group.</span></span> 

1. <span data-ttu-id="8115d-184">Edit the file `/etc/opt/omi/conf/omiserver.conf`</span><span class="sxs-lookup"><span data-stu-id="8115d-184">Edit the file `/etc/opt/omi/conf/omiserver.conf`</span></span>
2. <span data-ttu-id="8115d-185">Ensure that the line beginning with `httpsport=` defines the port 1270.</span><span class="sxs-lookup"><span data-stu-id="8115d-185">Ensure that the line beginning with `httpsport=` defines the port 1270.</span></span> <span data-ttu-id="8115d-186">Such as: `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="8115d-186">Such as: `httpsport=1270`</span></span>
3. <span data-ttu-id="8115d-187">Restart the OMI server: `sudo /opt/omi/bin/service_control restart`</span><span class="sxs-lookup"><span data-stu-id="8115d-187">Restart the OMI server: `sudo /opt/omi/bin/service_control restart`</span></span>

## <a name="next-steps"></a><span data-ttu-id="8115d-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="8115d-188">Next steps</span></span>

<span data-ttu-id="8115d-189">Review [Troubleshooting the Linux agent](log-analytics-agent-linux-support.md) if you encounter issues while installing or managing the agent.</span><span class="sxs-lookup"><span data-stu-id="8115d-189">Review [Troubleshooting the Linux agent](log-analytics-agent-linux-support.md) if you encounter issues while installing or managing the agent.</span></span>  