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
# <a name="use-packet-capture-to-do-proactive-network-monitoring-with-azure-functions"></a><span data-ttu-id="1670b-103">Use packet capture to do proactive network monitoring with Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1670b-103">Use packet capture to do proactive network monitoring with Azure Functions</span></span>

<span data-ttu-id="1670b-104">Network Watcher packet capture creates capture sessions to track traffic in and out of a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1670b-104">Network Watcher packet capture creates capture sessions to track traffic in and out of a virtual machine.</span></span> <span data-ttu-id="1670b-105">The capture file can have a filter that is defined to track only the traffic you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="1670b-105">The capture file can have a filter that is defined to track only the traffic you want to monitor.</span></span> <span data-ttu-id="1670b-106">This data is then stored in a storage blob or locally on the guest machine.</span><span class="sxs-lookup"><span data-stu-id="1670b-106">This data is then stored in a storage blob or locally on the guest machine.</span></span> <span data-ttu-id="1670b-107">This capability can be started remotely from other automation scenarios like Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1670b-107">This capability can be started remotely from other automation scenarios like Azure Functions.</span></span> <span data-ttu-id="1670b-108">Packet capture provides the capability of running proactive captures based on defined network anomalies.</span><span class="sxs-lookup"><span data-stu-id="1670b-108">Packet capture provides the capability of running proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="1670b-109">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span><span class="sxs-lookup"><span data-stu-id="1670b-109">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="1670b-110">Resources deployed in Azure are running 24/7.</span><span class="sxs-lookup"><span data-stu-id="1670b-110">Resources deployed in Azure are running 24/7.</span></span> <span data-ttu-id="1670b-111">You or your staff cannot actively monitor the status of all resources 24/7.</span><span class="sxs-lookup"><span data-stu-id="1670b-111">You or your staff cannot actively monitor the status of all resources 24/7.</span></span> <span data-ttu-id="1670b-112">What happens if an issue occurs at 2am?</span><span class="sxs-lookup"><span data-stu-id="1670b-112">What happens if an issue occurs at 2am?</span></span>

<span data-ttu-id="1670b-113">By using Network Watcher, Alerting, and Functions from within the Azure ecosystem, you can proactively respond to issues in your network with the data and tools to solve the problem.</span><span class="sxs-lookup"><span data-stu-id="1670b-113">By using Network Watcher, Alerting, and Functions from within the Azure ecosystem, you can proactively respond to issues in your network with the data and tools to solve the problem.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1670b-114">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1670b-114">Before you begin</span></span>

<span data-ttu-id="1670b-115">In this example, your VM is sending more TCP segments than usual, and you would like to be alerted.</span><span class="sxs-lookup"><span data-stu-id="1670b-115">In this example, your VM is sending more TCP segments than usual, and you would like to be alerted.</span></span> <span data-ttu-id="1670b-116">TCP Segments are used as an example, you could use any alert condition.</span><span class="sxs-lookup"><span data-stu-id="1670b-116">TCP Segments are used as an example, you could use any alert condition.</span></span> <span data-ttu-id="1670b-117">When you are alerted, you want to have packet level data to understand why communication has increased so you can take steps to return the machine to regular communication.</span><span class="sxs-lookup"><span data-stu-id="1670b-117">When you are alerted, you want to have packet level data to understand why communication has increased so you can take steps to return the machine to regular communication.</span></span>
<span data-ttu-id="1670b-118">This scenario assumes you have an existing instance of Network Watcher, and a resource group with a valid virtual machine to be used.</span><span class="sxs-lookup"><span data-stu-id="1670b-118">This scenario assumes you have an existing instance of Network Watcher, and a resource group with a valid virtual machine to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="1670b-119">Scenario</span><span class="sxs-lookup"><span data-stu-id="1670b-119">Scenario</span></span>

<span data-ttu-id="1670b-120">To automate this process, we create and connect an Alert on our VM to trigger when the incident occurs, and an Azure Function to call into Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="1670b-120">To automate this process, we create and connect an Alert on our VM to trigger when the incident occurs, and an Azure Function to call into Network Watcher.</span></span>

<span data-ttu-id="1670b-121">This scenario:</span><span class="sxs-lookup"><span data-stu-id="1670b-121">This scenario:</span></span>

* <span data-ttu-id="1670b-122">Creates an Azure function that starts a packet capture.</span><span class="sxs-lookup"><span data-stu-id="1670b-122">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="1670b-123">Creates an alert rule on a virtual machine</span><span class="sxs-lookup"><span data-stu-id="1670b-123">Creates an alert rule on a virtual machine</span></span>
* <span data-ttu-id="1670b-124">Configures the alert rule to call the Azure function</span><span class="sxs-lookup"><span data-stu-id="1670b-124">Configures the alert rule to call the Azure function</span></span>

## <a name="creating-an-azure-function-and-overview"></a><span data-ttu-id="1670b-125">Creating an Azure Function and overview</span><span class="sxs-lookup"><span data-stu-id="1670b-125">Creating an Azure Function and overview</span></span>

<span data-ttu-id="1670b-126">The first step is to create an Azure function to process the alert and create a packet capture.</span><span class="sxs-lookup"><span data-stu-id="1670b-126">The first step is to create an Azure function to process the alert and create a packet capture.</span></span>

<span data-ttu-id="1670b-127">The following list is an overview of the workflow that takes place.</span><span class="sxs-lookup"><span data-stu-id="1670b-127">The following list is an overview of the workflow that takes place.</span></span>

1. <span data-ttu-id="1670b-128">An alert is triggered on your VM.</span><span class="sxs-lookup"><span data-stu-id="1670b-128">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="1670b-129">The alert calls your Azure Function via a webhook.</span><span class="sxs-lookup"><span data-stu-id="1670b-129">The alert calls your Azure Function via a webhook.</span></span>
1. <span data-ttu-id="1670b-130">Your Azure Function processes the alert and starts a Network Watcher packet capture session.</span><span class="sxs-lookup"><span data-stu-id="1670b-130">Your Azure Function processes the alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="1670b-131">Packet capture runs on the VM and collects traffic.</span><span class="sxs-lookup"><span data-stu-id="1670b-131">Packet capture runs on the VM and collects traffic.</span></span> 
1. <span data-ttu-id="1670b-132">The capture file is uploaded to a storage account for review and diagnosis</span><span class="sxs-lookup"><span data-stu-id="1670b-132">The capture file is uploaded to a storage account for review and diagnosis</span></span> 

<span data-ttu-id="1670b-133">Creating an Azure Function can be accomplished in the portal by following [Create your first Azure Function](../azure-functions/functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="1670b-133">Creating an Azure Function can be accomplished in the portal by following [Create your first Azure Function](../azure-functions/functions-create-first-azure-function.md).</span></span> <span data-ttu-id="1670b-134">For this example, we chose an HttpTrigger-PowerShell type function.</span><span class="sxs-lookup"><span data-stu-id="1670b-134">For this example, we chose an HttpTrigger-PowerShell type function.</span></span> <span data-ttu-id="1670b-135">Customizations are required for this example and are explained in the following steps:</span><span class="sxs-lookup"><span data-stu-id="1670b-135">Customizations are required for this example and are explained in the following steps:</span></span>

![functions example][functions1]

> [!NOTE]
> <span data-ttu-id="1670b-137">The PowerShell template is experimental and does not have full support.</span><span class="sxs-lookup"><span data-stu-id="1670b-137">The PowerShell template is experimental and does not have full support.</span></span>

## <a name="adding-modules"></a><span data-ttu-id="1670b-138">Adding modules</span><span class="sxs-lookup"><span data-stu-id="1670b-138">Adding modules</span></span>

<span data-ttu-id="1670b-139">To use Network Watcher PowerShell cmdlets, the latest PowerShell module needs to be uploaded to the Function app.</span><span class="sxs-lookup"><span data-stu-id="1670b-139">To use Network Watcher PowerShell cmdlets, the latest PowerShell module needs to be uploaded to the Function app.</span></span>

1. <span data-ttu-id="1670b-140">On your local machine with the latest Azure PowerShell modules installed, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="1670b-140">On your local machine with the latest Azure PowerShell modules installed, run the following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="1670b-141">This example gives you the local path of your Azure PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="1670b-141">This example gives you the local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="1670b-142">These folders are used in a later step.</span><span class="sxs-lookup"><span data-stu-id="1670b-142">These folders are used in a later step.</span></span> <span data-ttu-id="1670b-143">The modules used in this scenario are:</span><span class="sxs-lookup"><span data-stu-id="1670b-143">The modules used in this scenario are:</span></span>

    * <span data-ttu-id="1670b-144">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="1670b-144">AzureRM.Network</span></span>

    * <span data-ttu-id="1670b-145">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="1670b-145">AzureRM.Profile</span></span>

    * <span data-ttu-id="1670b-146">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="1670b-146">AzureRM.Resources</span></span>

    ![powershell folders][functions5]

1. <span data-ttu-id="1670b-148">Navigate to **Function app settings** > **Go to App Service Editor**.</span><span class="sxs-lookup"><span data-stu-id="1670b-148">Navigate to **Function app settings** > **Go to App Service Editor**.</span></span>

    ![functions kudu][functions2]

1. <span data-ttu-id="1670b-150">Right-click the AlertPacketCapturePowershell folder and create a folder called **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="1670b-150">Right-click the AlertPacketCapturePowershell folder and create a folder called **azuremodules**.</span></span> <span data-ttu-id="1670b-151">Continue creating sub folders for each module needed.</span><span class="sxs-lookup"><span data-stu-id="1670b-151">Continue creating sub folders for each module needed.</span></span>

    ![functions kudu][functions3]

    * <span data-ttu-id="1670b-153">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="1670b-153">AzureRM.Network</span></span>

    * <span data-ttu-id="1670b-154">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="1670b-154">AzureRM.Profile</span></span>

    * <span data-ttu-id="1670b-155">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="1670b-155">AzureRM.Resources</span></span>

1. <span data-ttu-id="1670b-156">Right-click the **AzureRM.Network** sub folder and click **Upload Files**.</span><span class="sxs-lookup"><span data-stu-id="1670b-156">Right-click the **AzureRM.Network** sub folder and click **Upload Files**.</span></span> <span data-ttu-id="1670b-157">Navigate to where your Azure modules are installed, and in the local AzureRM.Network folder select all the files in the folder and click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="1670b-157">Navigate to where your Azure modules are installed, and in the local AzureRM.Network folder select all the files in the folder and click **Ok**.</span></span>  <span data-ttu-id="1670b-158">Repeat these steps for AzureRM.Profile and AzureRM.Resources.</span><span class="sxs-lookup"><span data-stu-id="1670b-158">Repeat these steps for AzureRM.Profile and AzureRM.Resources.</span></span>

    ![upload files][functions6]

1. <span data-ttu-id="1670b-160">When complete, each folder should have the PowerShell module files from your local machine.</span><span class="sxs-lookup"><span data-stu-id="1670b-160">When complete, each folder should have the PowerShell module files from your local machine.</span></span>

    ![powershell files][functions7]

## <a name="authentication"></a><span data-ttu-id="1670b-162">Authentication</span><span class="sxs-lookup"><span data-stu-id="1670b-162">Authentication</span></span>

<span data-ttu-id="1670b-163">To use the PowerShell cmdlets, you must authenticate.</span><span class="sxs-lookup"><span data-stu-id="1670b-163">To use the PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="1670b-164">Authentication needs to be configured in the Function app.</span><span class="sxs-lookup"><span data-stu-id="1670b-164">Authentication needs to be configured in the Function app.</span></span> <span data-ttu-id="1670b-165">To configure authencation, environment variables are configured and an encrypted key file needs to be uploaded to the Function app.</span><span class="sxs-lookup"><span data-stu-id="1670b-165">To configure authencation, environment variables are configured and an encrypted key file needs to be uploaded to the Function app.</span></span>

> [!NOTE]
> <span data-ttu-id="1670b-166">This scenario provides just one example of how to implement authentication with Azure Functions, there are other ways to do this.</span><span class="sxs-lookup"><span data-stu-id="1670b-166">This scenario provides just one example of how to implement authentication with Azure Functions, there are other ways to do this.</span></span>

### <a name="encrypted-credentials"></a><span data-ttu-id="1670b-167">Encrypted Credentials</span><span class="sxs-lookup"><span data-stu-id="1670b-167">Encrypted Credentials</span></span>

<span data-ttu-id="1670b-168">The following PowerShell script creates a key file called **PassEncryptKey.key** and provides an encrypted version of the password supplied.</span><span class="sxs-lookup"><span data-stu-id="1670b-168">The following PowerShell script creates a key file called **PassEncryptKey.key** and provides an encrypted version of the password supplied.</span></span>  <span data-ttu-id="1670b-169">This password is the same password that is defined for the Azure AD Application that is used for authentication.</span><span class="sxs-lookup"><span data-stu-id="1670b-169">This password is the same password that is defined for the Azure AD Application that is used for authentication.</span></span>

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

<span data-ttu-id="1670b-170">In the App Service Editor of the Function app, create a folder called **keys** under **AlertPacketCapturePowerShell** and upload the **PassEncryptKey.key** file created by the preceding PowerShell sample.</span><span class="sxs-lookup"><span data-stu-id="1670b-170">In the App Service Editor of the Function app, create a folder called **keys** under **AlertPacketCapturePowerShell** and upload the **PassEncryptKey.key** file created by the preceding PowerShell sample.</span></span>

![functions key][functions8]

### <a name="retrieving-values-for-environment-variables"></a><span data-ttu-id="1670b-172">Retrieving values for Environment variables</span><span class="sxs-lookup"><span data-stu-id="1670b-172">Retrieving values for Environment variables</span></span>

<span data-ttu-id="1670b-173">The final configuration required is to set up the environment variables needed to access the values for authentication.</span><span class="sxs-lookup"><span data-stu-id="1670b-173">The final configuration required is to set up the environment variables needed to access the values for authentication.</span></span> <span data-ttu-id="1670b-174">The following list lists the environment variables that are created:</span><span class="sxs-lookup"><span data-stu-id="1670b-174">The following list lists the environment variables that are created:</span></span>

* <span data-ttu-id="1670b-175">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="1670b-175">AzureClientID</span></span>

* <span data-ttu-id="1670b-176">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="1670b-176">AzureTenant</span></span>

* <span data-ttu-id="1670b-177">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="1670b-177">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="1670b-178">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="1670b-178">AzureClientID</span></span>

<span data-ttu-id="1670b-179">The client ID is the Application ID of an application in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1670b-179">The client ID is the Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="1670b-180">If you do not already have an application to use, run the following example to create an application.</span><span class="sxs-lookup"><span data-stu-id="1670b-180">If you do not already have an application to use, run the following example to create an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="1670b-181">The password used when creating the application should be the same password that was created earlier when saving the key file.</span><span class="sxs-lookup"><span data-stu-id="1670b-181">The password used when creating the application should be the same password that was created earlier when saving the key file.</span></span>

1. <span data-ttu-id="1670b-182">In the Azure portal, navigate to **Subscriptions** > Choose the subscription to use > **Access control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="1670b-182">In the Azure portal, navigate to **Subscriptions** > Choose the subscription to use > **Access control (IAM)**.</span></span>

    ![functions iam][functions9]

1. <span data-ttu-id="1670b-184">Choose the account to use and click Properties.</span><span class="sxs-lookup"><span data-stu-id="1670b-184">Choose the account to use and click Properties.</span></span> <span data-ttu-id="1670b-185">Copy the Application ID.</span><span class="sxs-lookup"><span data-stu-id="1670b-185">Copy the Application ID.</span></span>

    ![functions application id][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="1670b-187">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="1670b-187">AzureTenant</span></span>

<span data-ttu-id="1670b-188">The tenant ID is obtained by running the following PowerShell sample:</span><span class="sxs-lookup"><span data-stu-id="1670b-188">The tenant ID is obtained by running the following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="1670b-189">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="1670b-189">AzureCredPassword</span></span>

<span data-ttu-id="1670b-190">The value of the AzureCredPassword environment variable is the value from running the following PowerShell sample.</span><span class="sxs-lookup"><span data-stu-id="1670b-190">The value of the AzureCredPassword environment variable is the value from running the following PowerShell sample.</span></span> <span data-ttu-id="1670b-191">This is the same example as shown in the preceding **Encrypted Credentials** section.</span><span class="sxs-lookup"><span data-stu-id="1670b-191">This is the same example as shown in the preceding **Encrypted Credentials** section.</span></span> <span data-ttu-id="1670b-192">The value needed is the output of the `$Encryptedpassword` variable.</span><span class="sxs-lookup"><span data-stu-id="1670b-192">The value needed is the output of the `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="1670b-193">This is the service principal password that we encrypted using the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="1670b-193">This is the service principal password that we encrypted using the PowerShell script.</span></span>

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

### <a name="storing-the-environment-variables"></a><span data-ttu-id="1670b-194">Storing the Environment variables</span><span class="sxs-lookup"><span data-stu-id="1670b-194">Storing the Environment variables</span></span>

1. <span data-ttu-id="1670b-195">Navigate to the function app, click **Function app settings** > **Configure app settings**</span><span class="sxs-lookup"><span data-stu-id="1670b-195">Navigate to the function app, click **Function app settings** > **Configure app settings**</span></span>

    ![configure app settings][functions11]

1. <span data-ttu-id="1670b-197">Add the environment variables and their values to the App settings and click **Save**</span><span class="sxs-lookup"><span data-stu-id="1670b-197">Add the environment variables and their values to the App settings and click **Save**</span></span>

    ![app settings][functions12]

## <a name="processing-the-alert-and-starting-a-packet-capture-session"></a><span data-ttu-id="1670b-199">Processing the alert and starting a packet capture session</span><span class="sxs-lookup"><span data-stu-id="1670b-199">Processing the alert and starting a packet capture session</span></span>

<span data-ttu-id="1670b-200">It is now time to make calls into Network Watcher from within the Azure Function.</span><span class="sxs-lookup"><span data-stu-id="1670b-200">It is now time to make calls into Network Watcher from within the Azure Function.</span></span> <span data-ttu-id="1670b-201">Depending on the requirements, the implementation of this function is different.</span><span class="sxs-lookup"><span data-stu-id="1670b-201">Depending on the requirements, the implementation of this function is different.</span></span> <span data-ttu-id="1670b-202">However, the general flow of the code is as such:</span><span class="sxs-lookup"><span data-stu-id="1670b-202">However, the general flow of the code is as such:</span></span>

1. <span data-ttu-id="1670b-203">Process input parameters</span><span class="sxs-lookup"><span data-stu-id="1670b-203">Process input parameters</span></span>
2. <span data-ttu-id="1670b-204">Query existing packet captures verify limits and resolve name conflicts</span><span class="sxs-lookup"><span data-stu-id="1670b-204">Query existing packet captures verify limits and resolve name conflicts</span></span>
3. <span data-ttu-id="1670b-205">Create a packet capture with appropriate parameters</span><span class="sxs-lookup"><span data-stu-id="1670b-205">Create a packet capture with appropriate parameters</span></span>
4. <span data-ttu-id="1670b-206">Poll packet capture periodically until complete</span><span class="sxs-lookup"><span data-stu-id="1670b-206">Poll packet capture periodically until complete</span></span>
5. <span data-ttu-id="1670b-207">Notify user that packet capture session is complete</span><span class="sxs-lookup"><span data-stu-id="1670b-207">Notify user that packet capture session is complete</span></span>

<span data-ttu-id="1670b-208">The following example is PowerShell that can be used in the Azure Function.</span><span class="sxs-lookup"><span data-stu-id="1670b-208">The following example is PowerShell that can be used in the Azure Function.</span></span> <span data-ttu-id="1670b-209">There are values that need to be replaced for subscriptionId, resourceGroupName, and storageAccountName.</span><span class="sxs-lookup"><span data-stu-id="1670b-209">There are values that need to be replaced for subscriptionId, resourceGroupName, and storageAccountName.</span></span>

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

<span data-ttu-id="1670b-210">Once you have created your function, you need to configure your alert to call the URL associated with the function.</span><span class="sxs-lookup"><span data-stu-id="1670b-210">Once you have created your function, you need to configure your alert to call the URL associated with the function.</span></span> <span data-ttu-id="1670b-211">To get this value, click **</> Get function URL**</span><span class="sxs-lookup"><span data-stu-id="1670b-211">To get this value, click **</> Get function URL**</span></span> 

![finding the function url 1][functions13]

<span data-ttu-id="1670b-213">Copy the Function URL for your function app.</span><span class="sxs-lookup"><span data-stu-id="1670b-213">Copy the Function URL for your function app.</span></span>

![finding the function url 2][2]

<span data-ttu-id="1670b-215">If you require custom properties in the payload of the webhook POST request, refer to [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="1670b-215">If you require custom properties in the payload of the webhook POST request, refer to [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md)</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="1670b-216">Configure an alert on a VM</span><span class="sxs-lookup"><span data-stu-id="1670b-216">Configure an alert on a VM</span></span>

<span data-ttu-id="1670b-217">Alerts can be configured to notify individuals when a specific metric crosses a threshold assigned to it.</span><span class="sxs-lookup"><span data-stu-id="1670b-217">Alerts can be configured to notify individuals when a specific metric crosses a threshold assigned to it.</span></span> <span data-ttu-id="1670b-218">In this example, the alert is on the TCP segments sent, but the alert can be triggered for many other metrics.</span><span class="sxs-lookup"><span data-stu-id="1670b-218">In this example, the alert is on the TCP segments sent, but the alert can be triggered for many other metrics.</span></span> <span data-ttu-id="1670b-219">In this example, an alert is configured to call a webhook to call the function.</span><span class="sxs-lookup"><span data-stu-id="1670b-219">In this example, an alert is configured to call a webhook to call the function.</span></span>

### <a name="create-the-alert-rule"></a><span data-ttu-id="1670b-220">Create the alert rule</span><span class="sxs-lookup"><span data-stu-id="1670b-220">Create the alert rule</span></span>

<span data-ttu-id="1670b-221">Navigate to an existing virtual machine and add an alert rule.</span><span class="sxs-lookup"><span data-stu-id="1670b-221">Navigate to an existing virtual machine and add an alert rule.</span></span> <span data-ttu-id="1670b-222">More detailed documentation about configuring alerts can be found at [User Azure portal to create alerts for Azure services](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1670b-222">More detailed documentation about configuring alerts can be found at [User Azure portal to create alerts for Azure services](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> 

![add vm alert rule to a virtual machine][1]

> [!NOTE]
> <span data-ttu-id="1670b-224">The TCP segments metric is not enabled by default.</span><span class="sxs-lookup"><span data-stu-id="1670b-224">The TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="1670b-225">Learn more about how to enable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="1670b-225">Learn more about how to enable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md)</span></span>

<span data-ttu-id="1670b-226">Finally paste the URL from the preceding step into the webhook textbox on your alert.</span><span class="sxs-lookup"><span data-stu-id="1670b-226">Finally paste the URL from the preceding step into the webhook textbox on your alert.</span></span> <span data-ttu-id="1670b-227">Click **OK** to save the alert rule.</span><span class="sxs-lookup"><span data-stu-id="1670b-227">Click **OK** to save the alert rule.</span></span>

![pasting the url to the alert rule][3]

## <a name="downloading-and-viewing-the-capture-file"></a><span data-ttu-id="1670b-229">Downloading and viewing the capture file</span><span class="sxs-lookup"><span data-stu-id="1670b-229">Downloading and viewing the capture file</span></span>

<span data-ttu-id="1670b-230">If you save your capture to a storage account, then the capture file can be downloaded via the portal or programmatically.</span><span class="sxs-lookup"><span data-stu-id="1670b-230">If you save your capture to a storage account, then the capture file can be downloaded via the portal or programmatically.</span></span> <span data-ttu-id="1670b-231">If the capture file is stored locally, the capture file is retrieved by logging in to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1670b-231">If the capture file is stored locally, the capture file is retrieved by logging in to the virtual machine.</span></span> 

<span data-ttu-id="1670b-232">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="1670b-232">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="1670b-233">Another tool that can be used is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="1670b-233">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="1670b-234">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="1670b-234">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="1670b-235">Once your capture is downloaded, you can view it using any tool that can read a **.cap** file.</span><span class="sxs-lookup"><span data-stu-id="1670b-235">Once your capture is downloaded, you can view it using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="1670b-236">The following are links to two of these tools:</span><span class="sxs-lookup"><span data-stu-id="1670b-236">The following are links to two of these tools:</span></span>

[<span data-ttu-id="1670b-237">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="1670b-237">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/en-us/library/jj649776.aspx)  
[<span data-ttu-id="1670b-238">WireShark</span><span class="sxs-lookup"><span data-stu-id="1670b-238">WireShark</span></span>](https://www.wireshark.org/)  

## <a name="next-steps"></a><span data-ttu-id="1670b-239">Next steps</span><span class="sxs-lookup"><span data-stu-id="1670b-239">Next steps</span></span>

<span data-ttu-id="1670b-240">Learn how to view your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="1670b-240">Learn how to view your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-alert-triggered-packet-capture.md)</span></span>

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














