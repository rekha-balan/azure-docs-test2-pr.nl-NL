---
title: Use packet capture to do proactive network monitoring with Azure Functions | Microsoft Docs
description: This article describes how to create an alert triggered packet capture with Azure Network Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b13a826a9e19da2d7e9c5dba556371ecf8770106
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540808"
---
# <a name="use-packet-capture-to-do-proactive-network-monitoring-with-azure-functions"></a>Use packet capture to do proactive network monitoring with Azure Functions

Network Watcher packet capture creates capture sessions to track traffic in and out of a virtual machine. The capture file can have a filter that is defined to track only the traffic you want to monitor. This data is then stored in a storage blob or locally on the guest machine. This capability can be started remotely from other automation scenarios like Azure Functions. Packet capture provides the capability of running proactive captures based on defined network anomalies. Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.

Resources deployed in Azure are running 24/7. You or your staff cannot actively monitor the status of all resources 24/7. What happens if an issue occurs at 2am?

By using Network Watcher, Alerting, and Functions from within the Azure ecosystem, you can proactively respond to issues in your network with the data and tools to solve the problem.

## <a name="before-you-begin"></a>Before you begin

In this example, your VM is sending more TCP segments than usual, and you would like to be alerted. TCP Segments are used as an example, you could use any alert condition. When you are alerted, you want to have packet level data to understand why communication has increased so you can take steps to return the machine to regular communication.
This scenario assumes you have an existing instance of Network Watcher, and a resource group with a valid virtual machine to be used.

## <a name="scenario"></a>Scenario

To automate this process, we create and connect an Alert on our VM to trigger when the incident occurs, and an Azure Function to call into Network Watcher.

This scenario:

* Creates an Azure function that starts a packet capture.
* Creates an alert rule on a virtual machine
* Configures the alert rule to call the Azure function

## <a name="creating-an-azure-function-and-overview"></a>Creating an Azure Function and overview

The first step is to create an Azure function to process the alert and create a packet capture.

The following list is an overview of the workflow that takes place.

1. An alert is triggered on your VM.
1. The alert calls your Azure Function via a webhook.
1. Your Azure Function processes the alert and starts a Network Watcher packet capture session.
1. Packet capture runs on the VM and collects traffic. 
1. The capture file is uploaded to a storage account for review and diagnosis 

Creating an Azure Function can be accomplished in the portal by following [Create your first Azure Function](../azure-functions/functions-create-first-azure-function.md). For this example, we chose an HttpTrigger-PowerShell type function. Customizations are required for this example and are explained in the following steps:

![functions example][functions1]

> [!NOTE]
> The PowerShell template is experimental and does not have full support.

## <a name="adding-modules"></a>Adding modules

To use Network Watcher PowerShell cmdlets, the latest PowerShell module needs to be uploaded to the Function app.

1. On your local machine with the latest Azure PowerShell modules installed, run the following PowerShell command:

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    This example gives you the local path of your Azure PowerShell modules. These folders are used in a later step. The modules used in this scenario are:

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

    ![powershell folders][functions5]

1. Navigate to **Function app settings** > **Go to App Service Editor**.

    ![functions kudu][functions2]

1. Right-click the AlertPacketCapturePowershell folder and create a folder called **azuremodules**. Continue creating sub folders for each module needed.

    ![functions kudu][functions3]

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

1. Right-click the **AzureRM.Network** sub folder and click **Upload Files**. Navigate to where your Azure modules are installed, and in the local AzureRM.Network folder select all the files in the folder and click **Ok**.  Repeat these steps for AzureRM.Profile and AzureRM.Resources.

    ![upload files][functions6]

1. When complete, each folder should have the PowerShell module files from your local machine.

    ![powershell files][functions7]

## <a name="authentication"></a>Authentication

To use the PowerShell cmdlets, you must authenticate. Authentication needs to be configured in the Function app. To configure authencation, environment variables are configured and an encrypted key file needs to be uploaded to the Function app.

> [!NOTE]
> This scenario provides just one example of how to implement authentication with Azure Functions, there are other ways to do this.

### <a name="encrypted-credentials"></a>Encrypted Credentials

The following PowerShell script creates a key file called **PassEncryptKey.key** and provides an encrypted version of the password supplied.  This password is the same password that is defined for the Azure AD Application that is used for authentication.

```powershell
#variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

In the App Service Editor of the Function app, create a folder called **keys** under **AlertPacketCapturePowerShell** and upload the **PassEncryptKey.key** file created by the preceding PowerShell sample.

![functions key][functions8]

### <a name="retrieving-values-for-environment-variables"></a>Retrieving values for Environment variables

The final configuration required is to set up the environment variables needed to access the values for authentication. The following list lists the environment variables that are created:

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

The client ID is the Application ID of an application in Azure Active Directory.

1. If you do not already have an application to use, run the following example to create an application.

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > The password used when creating the application should be the same password that was created earlier when saving the key file.

1. In the Azure portal, navigate to **Subscriptions** > Choose the subscription to use > **Access control (IAM)**.

    ![functions iam][functions9]

1. Choose the account to use and click Properties. Copy the Application ID.

    ![functions application id][functions10]

#### <a name="azuretenant"></a>AzureTenant

The tenant ID is obtained by running the following PowerShell sample:

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

The value of the AzureCredPassword environment variable is the value from running the following PowerShell sample. This is the same example as shown in the preceding **Encrypted Credentials** section. The value needed is the output of the `$Encryptedpassword` variable.  This is the service principal password that we encrypted using the PowerShell script.

```powershell
#variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="storing-the-environment-variables"></a>Storing the Environment variables

1. Navigate to the function app, click **Function app settings** > **Configure app settings**

    ![configure app settings][functions11]

1. Add the environment variables and their values to the App settings and click **Save**

    ![app settings][functions12]

## <a name="processing-the-alert-and-starting-a-packet-capture-session"></a>Processing the alert and starting a packet capture session

It is now time to make calls into Network Watcher from within the Azure Function. Depending on the requirements, the implementation of this function is different. However, the general flow of the code is as such:

1. Process input parameters
2. Query existing packet captures verify limits and resolve name conflicts
3. Create a packet capture with appropriate parameters
4. Poll packet capture periodically until complete
5. Notify user that packet capture session is complete

The following example is PowerShell that can be used in the Azure Function. There are values that need to be replaced for subscriptionId, resourceGroupName, and storageAccountName.

```powershell
#Import Azure PowerShell modules required to make calls to Network Watcher
Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

#Process Alert Request Body
$requestBody = Get-Content $req -Raw | ConvertFrom-Json

#Storage Account Id to save captures in
$storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

#Packet Capture Vars
$packetcapturename = "PSAzureFunction"
$packetCaptureLimit = 10
$packetCaptureDuration = 10

#Credentials
$tenant = $env:AzureTenant
$pw = $env:AzureCredPassword
$clientid = $env:AzureClientId
$keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

#Authentication
$secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
$credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


#Get the VM that fired the Alert
if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
{
    Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
    Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
    Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
    Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

    #Get the Network Watcher in the VM's Region
    $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
    $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

    #Get existing packetCaptures
    $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

    #Remove existing packet capture created by the function if it exists
    $packetCaptures | %{if($_.Name -eq $packetCaptureName)
    { 
        Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
    }}

    #Initiate Packet Capture on the VM that fired the alert
    if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
        echo "Initiating Packet Capture"
        New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
        Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
    }
} 
``` 

Once you have created your function, you need to configure your alert to call the URL associated with the function. To get this value, click **</> Get function URL** 

![finding the function url 1][functions13]

Copy the Function URL for your function app.

![finding the function url 2][2]

If you require custom properties in the payload of the webhook POST request, refer to [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="configure-an-alert-on-a-vm"></a>Configure an alert on a VM

Alerts can be configured to notify individuals when a specific metric crosses a threshold assigned to it. In this example, the alert is on the TCP segments sent, but the alert can be triggered for many other metrics. In this example, an alert is configured to call a webhook to call the function.

### <a name="create-the-alert-rule"></a>Create the alert rule

Navigate to an existing virtual machine and add an alert rule. More detailed documentation about configuring alerts can be found at [User Azure portal to create alerts for Azure services](../monitoring-and-diagnostics/insights-alerts-portal.md). 

![add vm alert rule to a virtual machine][1]

> [!NOTE]
> The TCP segments metric is not enabled by default. Learn more about how to enable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md)

Finally paste the URL from the preceding step into the webhook textbox on your alert. Click **OK** to save the alert rule.

![pasting the url to the alert rule][3]

## <a name="downloading-and-viewing-the-capture-file"></a>Downloading and viewing the capture file

If you save your capture to a storage account, then the capture file can be downloaded via the portal or programmatically. If the capture file is stored locally, the capture file is retrieved by logging in to the virtual machine. 

For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md). Another tool that can be used is Storage Explorer. More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)

Once your capture is downloaded, you can view it using any tool that can read a **.cap** file. The following are links to two of these tools:

[Microsoft Message Analyzer](https://technet.microsoft.com/en-us/library/jj649776.aspx)  
[WireShark](https://www.wireshark.org/)  

## <a name="next-steps"></a>Next steps

Learn how to view your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-alert-triggered-packet-capture.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-alert-triggered-packet-capture/functions13.png














