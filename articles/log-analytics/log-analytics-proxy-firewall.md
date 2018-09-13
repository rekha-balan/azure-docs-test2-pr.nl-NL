---
title: Configure proxy and firewall settings in Azure Log Analytics | Microsoft Docs
description: Configure proxy and firewall settings when your agents or OMS services need to use specific ports.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: b55ebd80-efd4-4220-971b-c18aea1b1ab2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/12/2017
ms.author: banders;magoedte
ms.openlocfilehash: 9a236ca98c2f407f4772bf62d196a0bf73ddbdd1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556639"
---
# <a name="configure-proxy-and-firewall-settings-in-log-analytics"></a>Configure proxy and firewall settings in Log Analytics
Actions needed to configure proxy and firewall settings for Log Analytics differ for the type of agents that you are using. Review the following sections for the type of agent that you use.

## <a name="settings-for-the-oms-gateway"></a>Settings for the OMS Gateway

If your agents do not have Internet access, they can instead send their data using your own network resources to the OMS Gateway. The Gateway collects their data and sends it to the OMS service on their behalf.

Configure agents that communicate with the OMS Gateway using its fully qualified domain name and custom port number.

The OMS Gateway needs Internet access. Use the same proxy server or firewall settings for the OMS Gateway that you would for the type of agents you have. For more information about the OMS Gateway, see [Connect computers and devices to OMS using the OMS Gateway](log-analytics-oms-gateway.md).

## <a name="configure-settings-with-the-microsoft-monitoring-agent"></a>Configure settings with the Microsoft Monitoring Agent
For the Microsoft Monitoring Agent to connect to and register with the OMS service, it must have access to the port number of your domains and the URLs. If you use a proxy server for communication between the agent and the OMS service, you’ll need to ensure that the appropriate resources are accessible. If you use a firewall to restrict access to the Internet, you need to configure your firewall to permit access to OMS. The following tables list the ports that OMS needs.

| **Agent Resource** | **Ports** | **Bypass HTTPS inspection** |
| --- | --- | --- |
| \*.ods.opinsights.azure.com |443 |Yes |
| \*.oms.opinsights.azure.com |443 |Yes |
| \*.blob.core.windows.net |443 |Yes |
| \*.azure-automation.net |443 |Yes |

You can use the following procedure to configure proxy settings for the Microsoft Monitoring Agent using Control Panel. You'll need to use the procedure for each server. If you have many servers that you need to configure, you might find it easier to use a script to automate this process. If so, see the next procedure [To configure proxy settings for the Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-control-panel"></a>To configure proxy settings for the Microsoft Monitoring Agent using Control Panel
1. Open **Control Panel**.
2. Open **Microsoft Monitoring Agent**.
3. Click the **Proxy Settings** tab.<br>  
   ![proxy settings tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-direct-agent-proxy.png)
4. Select **Use a proxy server** and type the URL and port number, if one is needed, similar to the example shown. If your proxy server requires authentication, type the username and password to access the proxy server.

Use the following procedure to create a PowerShell script that you can run to set the proxy settings for each agent that connects directly to servers.

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script"></a>To configure proxy settings for the Microsoft Monitoring Agent using a script
Copy the following sample, update it with information specific to your environment, save it with a PS1 file name extension, and then run the script on each computer that connects directly to the OMS service.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

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


## <a name="configure-settings-with-operations-manager"></a>Configure settings with Operations Manager
For an Operations Manager management group to connect to and register with the OMS service, it must have access to the port numbers of your domains and URLs. If you use a proxy server for communication between the Operations Manager management server and the OMS service, you’ll need to ensure that the appropriate resources are accessible. If you use a firewall to restrict access to the Internet, you need to configure your firewall to permit access to OMS. Even if an Operations Manager management server is not behind a proxy server, its agents might be. In this case, the proxy server should be configured in the same manner as agents are in order to enable and allow Security and Log Management solution data to get sent to the OMS web service.

In order for Operations Manager agents to communicate with the OMS service, your Operations Manager infrastructure (including agents) should have the correct proxy settings and version. The proxy setting for agents is specified in the Operations Manager console. Your version should be one of the following:

* Operations Manager 2012 SP1 Update Rollup 7 or later
* Operations Manager 2012 R2 Update Rollup 3 or later

The following tables list the ports related to these tasks.

> [!NOTE]
> Some of the following resources mention Advisor and Operational Insights, both were previous versions of OMS. However, the listed resources will change in the future.
>
>

Here's a list of agent resources and ports:<br>

| **Agent resource** | **Ports** |
| --- | --- |
| \*.ods.opinsights.azure.com |443 |
| \*.oms.opinsights.azure.com |443 |
| \*.blob.core.windows.net/\* |443 |

<br>
Here's a list of management server resources and ports:<br>

| **Management server resource** | **Ports** | **Bypass HTTPS inspection** |
| --- | --- | --- |
| service.systemcenteradvisor.com |443 | |
| \*.service.opinsights.azure.com |443 | |
| \*.blob.core.windows.net |443 |Yes |
| \*.ods.opinsights.azure.com |443 |Yes |
| \*.azure-automation.net |443 |Yes |

<br>
Here's a list of OMS and Operations Manager console resources and ports.<br>

| **OMS and Operations Manager console resource** | **Ports** |
| --- | --- |
| service.systemcenteradvisor.com |443 |
| \*.service.opinsights.azure.com |443 |
| \*.live.com |Port 80 and 443 |
| \*.microsoft.com |Port 80 and 443 |
| \*.microsoftonline.com |Port 80 and 443 |
| \*.mms.microsoft.com |Port 80 and 443 |
| login.windows.net |Port 80 and 443 |

<br>

Use the following procedures to register your Operations Manager management group with the OMS service. If you are having communication problems between the management group and the OMS service, use the validation procedures to troubleshoot data transmission to the OMS service.

### <a name="to-request-exceptions-for-the-oms-service-endpoints"></a>To request exceptions for the OMS service endpoints
1. Use the information from the first table presented previously to ensure that the resources needed for the Operations Manager management server are accessible through any firewalls you might have.
2. Use the information from the second table presented previously to ensure that the resources needed for the Operations console in Operations Manager and OMS are accessible through any firewalls you might have.
3. If you use a proxy server with Internet Explorer, ensure that it is configured and works correctly. To verify, you can open a secure web connection (HTTPS), for example [https://bing.com](https://bing.com). If the secure web connection doesn’t work in a browser, it probably won’t work in the Operations Manager management console with web services in the cloud.

### <a name="to-configure-the-proxy-server-in-the-operations-manager-console"></a>To configure the proxy server in the Operations Manager console
1. Open the Operations Manager console and select the **Administration** workspace.
2. Expand **Operational Insights**, and then select **Operational Insights Connection**.<br>  
   ![Operations Manager OMS Connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-om01.png)
3. In the OMS Connection view, click **Configure Proxy Server**.<br>  
   ![Operations Manager OMS Connection Configure Proxy Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-om02.png)
4. In Operational Insights Settings Wizard: Proxy Server, select **Use a proxy server to access the Operational Insights Web Service**, and then type the URL with the port number, for example, **http://myproxy:80**.<br>  
   ![Operations Manager OMS proxy address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-om03.png)

### <a name="to-specify-credentials-if-the-proxy-server-requires-authentication"></a>To specify credentials if the proxy server requires authentication
 Proxy server credentials and settings need to propagate to managed computers that will report to OMS. Those servers should be in the *Microsoft System Center Advisor Monitoring Server Group*. Credentials are encrypted in the registry of each server in the group.

1. Open the Operations Manager console and select the **Administration** workspace.
2. Under **RunAs Configuration**, select **Profiles**.
3. Open the **System Center Advisor Run As Profile Proxy** profile.<br>  
   ![image of the System Center Advisor Run As Proxy profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-proxyacct1.png)
4. In the Run As Profile Wizard, click **Add** to use a Run As account. You can create a new Run As account or use an existing account. This account needs to have sufficient permissions to pass through the proxy server.<br>   
   ![image of the Run As Profile Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-proxyacct2.png)
5. To set the account to manage, choose **A selected class, group, or object** to open the Object Search box.<br>  
   ![image of the Run As Profile Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-proxyacct2-1.png)
6. Search for then select **Microsoft System Center Advisor Monitoring Server Group**.<br>  
   ![image of the Object Search box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-proxyacct3.png)
7. Click **OK** to close the Add a Run As account box.<br>  
   ![image of the Run As Profile Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-proxyacct4.png)
8. Complete the wizard and save the changes.<br>  
   ![image of the Run As Profile Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-proxyacct5.png)

### <a name="to-validate-that-oms-management-packs-are-downloaded"></a>To validate that OMS management packs are downloaded
If you've added solutions to OMS, you can view them in the Operations Manager console as management packs under **Administration**. Search for *System Center Advisor* to quickly find them.<br>  
   ![management packs downloaded](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-mpdownloaded.png)  <br>  
Or, you can also check for OMS management packs by using the following Windows PowerShell command in the Operations Manager management server:

   ```  
    Get-ScomManagementPack | where {$_.DisplayName -match 'Advisor'} | select Name,DisplayName,Version,KeyToken
   ```  

### <a name="to-validate-that-operations-manager-is-sending-data-to-the-oms-service"></a>To validate that Operations Manager is sending data to the OMS service
1. In the Operations Manager management server, open Performance Monitor (perfmon.exe), and select **Performance Monitor**.
2. Click **Add**, and then select **Health Service Management Groups**.
3. Add all the counters that start with **HTTP**.<br>  
   ![add counters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-sendingdata1.png)
4. If your Operations Manager configuration is good, you will see activity for Health Service Management counters for events and other data items, based on the management packs that you added in OMS and the configured log collection policy.<br>  
   ![Performance Monitor showing activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-proxy-firewall/proxy-sendingdata2.png)

## <a name="next-steps"></a>Next steps
* [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.
* Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.













