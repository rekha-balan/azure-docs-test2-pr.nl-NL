---
title: Set up Azure Key Vault with end-to-end key rotation and auditing | Microsoft Docs
description: Use this how-to to help you get set up with key rotation and monitoring key vault logs.
services: key-vault
documentationcenter: ''
author: swgriffith
manager: mbaldwin
tags: ''
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: 9b200aed72d9c35da4d5e47c3a28c7e0c3487d68
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553057"
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="d6faa-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span><span class="sxs-lookup"><span data-stu-id="d6faa-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="d6faa-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="d6faa-104">Introduction</span></span>
<span data-ttu-id="d6faa-105">After creating your key vault, you will be able to start using that vault to store your keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="d6faa-105">After creating your key vault, you will be able to start using that vault to store your keys and secrets.</span></span> <span data-ttu-id="d6faa-106">Your applications no longer need to persist your keys or secrets, but rather will request them from the key vault as needed.</span><span class="sxs-lookup"><span data-stu-id="d6faa-106">Your applications no longer need to persist your keys or secrets, but rather will request them from the key vault as needed.</span></span> <span data-ttu-id="d6faa-107">This allows you to update keys and secrets without affecting the behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span><span class="sxs-lookup"><span data-stu-id="d6faa-107">This allows you to update keys and secrets without affecting the behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="d6faa-108">This article walks through an example of using Azure Key Vault to store a secret, in this case an Azure Storage Account key that is accessed by an application.</span><span class="sxs-lookup"><span data-stu-id="d6faa-108">This article walks through an example of using Azure Key Vault to store a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="d6faa-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span><span class="sxs-lookup"><span data-stu-id="d6faa-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="d6faa-110">Finally, it walks through a demonstration of how to monitor the key vault audit logs and raise alerts when unexpected requests are made.</span><span class="sxs-lookup"><span data-stu-id="d6faa-110">Finally, it walks through a demonstration of how to monitor the key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="d6faa-111">This tutorial is not intended to explain in detail the initial setup of your key vault.</span><span class="sxs-lookup"><span data-stu-id="d6faa-111">This tutorial is not intended to explain in detail the initial setup of your key vault.</span></span> <span data-ttu-id="d6faa-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6faa-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="d6faa-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d6faa-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="d6faa-114">Set up Key Vault</span><span class="sxs-lookup"><span data-stu-id="d6faa-114">Set up Key Vault</span></span>
<span data-ttu-id="d6faa-115">To enable an application to retrieve a secret from Key Vault, you must first create the secret and upload it to your vault.</span><span class="sxs-lookup"><span data-stu-id="d6faa-115">To enable an application to retrieve a secret from Key Vault, you must first create the secret and upload it to your vault.</span></span> <span data-ttu-id="d6faa-116">This can be accomplished by starting an Azure PowerShell session and signing in to your Azure account with the following command:</span><span class="sxs-lookup"><span data-stu-id="d6faa-116">This can be accomplished by starting an Azure PowerShell session and signing in to your Azure account with the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d6faa-117">In the pop-up browser window, enter your Azure account user name and password.</span><span class="sxs-lookup"><span data-stu-id="d6faa-117">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="d6faa-118">PowerShell will get all the subscriptions that are associated with this account.</span><span class="sxs-lookup"><span data-stu-id="d6faa-118">PowerShell will get all the subscriptions that are associated with this account.</span></span> <span data-ttu-id="d6faa-119">PowerShell uses the first one by default.</span><span class="sxs-lookup"><span data-stu-id="d6faa-119">PowerShell uses the first one by default.</span></span>

<span data-ttu-id="d6faa-120">If you have multiple subscriptions, you might have to specify the one that was used to create your key vault.</span><span class="sxs-lookup"><span data-stu-id="d6faa-120">If you have multiple subscriptions, you might have to specify the one that was used to create your key vault.</span></span> <span data-ttu-id="d6faa-121">Enter the following to see the subscriptions for your account:</span><span class="sxs-lookup"><span data-stu-id="d6faa-121">Enter the following to see the subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="d6faa-122">To specify the subscription that's associated with the key vault you will be logging, enter:</span><span class="sxs-lookup"><span data-stu-id="d6faa-122">To specify the subscription that's associated with the key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="d6faa-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span><span class="sxs-lookup"><span data-stu-id="d6faa-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="d6faa-124">After retrieving your secret (in this case, your storage account key), you must convert that to a secure string and then create a secret with that value in your key vault.</span><span class="sxs-lookup"><span data-stu-id="d6faa-124">After retrieving your secret (in this case, your storage account key), you must convert that to a secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="d6faa-125">Next, get the URI for the secret you created.</span><span class="sxs-lookup"><span data-stu-id="d6faa-125">Next, get the URI for the secret you created.</span></span> <span data-ttu-id="d6faa-126">This is used in a later step when you call the key vault to retrieve your secret.</span><span class="sxs-lookup"><span data-stu-id="d6faa-126">This is used in a later step when you call the key vault to retrieve your secret.</span></span> <span data-ttu-id="d6faa-127">Run the following PowerShell command and make note of the ID value, which is the secret URI:</span><span class="sxs-lookup"><span data-stu-id="d6faa-127">Run the following PowerShell command and make note of the ID value, which is the secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-the-application"></a><span data-ttu-id="d6faa-128">Set up the application</span><span class="sxs-lookup"><span data-stu-id="d6faa-128">Set up the application</span></span>
<span data-ttu-id="d6faa-129">Now that you have a secret stored, you can use code to retrieve and use it.</span><span class="sxs-lookup"><span data-stu-id="d6faa-129">Now that you have a secret stored, you can use code to retrieve and use it.</span></span> <span data-ttu-id="d6faa-130">There are a few steps required to achieve this.</span><span class="sxs-lookup"><span data-stu-id="d6faa-130">There are a few steps required to achieve this.</span></span> <span data-ttu-id="d6faa-131">The first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span><span class="sxs-lookup"><span data-stu-id="d6faa-131">The first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="d6faa-132">Your application must be created on the same Azure Active Directory tenant as your key vault.</span><span class="sxs-lookup"><span data-stu-id="d6faa-132">Your application must be created on the same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="d6faa-133">Open the applications tab of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6faa-133">Open the applications tab of Azure Active Directory.</span></span>

![Open applications in Azure Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="d6faa-135">Choose **ADD** to add an application to your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6faa-135">Choose **ADD** to add an application to your Azure Active Directory.</span></span>

![Choose ADD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="d6faa-137">Leave the application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span><span class="sxs-lookup"><span data-stu-id="d6faa-137">Leave the application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Name the application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="d6faa-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="d6faa-140">These can be anything you want for this demo, and they can be changed later if needed.</span><span class="sxs-lookup"><span data-stu-id="d6faa-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Provide required URIs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="d6faa-142">After the application is added to Azure Active Directory, you will be brought into the application page.</span><span class="sxs-lookup"><span data-stu-id="d6faa-142">After the application is added to Azure Active Directory, you will be brought into the application page.</span></span> <span data-ttu-id="d6faa-143">Click the **Configure** tab and then find and copy the **Client ID** value.</span><span class="sxs-lookup"><span data-stu-id="d6faa-143">Click the **Configure** tab and then find and copy the **Client ID** value.</span></span> <span data-ttu-id="d6faa-144">Make note of the client ID for later steps.</span><span class="sxs-lookup"><span data-stu-id="d6faa-144">Make note of the client ID for later steps.</span></span>

<span data-ttu-id="d6faa-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6faa-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="d6faa-146">You can create this under the **Keys** section in the **Configuration** tab. Make note of the newly generated key from your Azure Active Directory application for use in a later step.</span><span class="sxs-lookup"><span data-stu-id="d6faa-146">You can create this under the **Keys** section in the **Configuration** tab. Make note of the newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Azure Active Directory App Keys](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="d6faa-148">Before establishing any calls from your application into the key vault, you must tell the key vault about your application and its permissions.</span><span class="sxs-lookup"><span data-stu-id="d6faa-148">Before establishing any calls from your application into the key vault, you must tell the key vault about your application and its permissions.</span></span> <span data-ttu-id="d6faa-149">The following command takes the vault name and the client ID from your Azure Active Directory app and grants **Get** access to your key vault for the application.</span><span class="sxs-lookup"><span data-stu-id="d6faa-149">The following command takes the vault name and the client ID from your Azure Active Directory app and grants **Get** access to your key vault for the application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="d6faa-150">At this point, you are ready to start building your application calls.</span><span class="sxs-lookup"><span data-stu-id="d6faa-150">At this point, you are ready to start building your application calls.</span></span> <span data-ttu-id="d6faa-151">In your application, you must install the NuGet packages required to interact with Azure Key Vault and Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6faa-151">In your application, you must install the NuGet packages required to interact with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="d6faa-152">From the Visual Studio Package Manager console, enter the following commands.</span><span class="sxs-lookup"><span data-stu-id="d6faa-152">From the Visual Studio Package Manager console, enter the following commands.</span></span> <span data-ttu-id="d6faa-153">At the writing of this article, the current version of the Azure Active Directory package is 3.10.305231913, so you might want to confirm the latest version and update accordingly.</span><span class="sxs-lookup"><span data-stu-id="d6faa-153">At the writing of this article, the current version of the Azure Active Directory package is 3.10.305231913, so you might want to confirm the latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="d6faa-154">In your application code, create a class to hold the method for your Azure Active Directory authentication.</span><span class="sxs-lookup"><span data-stu-id="d6faa-154">In your application code, create a class to hold the method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="d6faa-155">In this example, that class is called **Utils**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="d6faa-156">Add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="d6faa-156">Add the following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="d6faa-157">Next, add the following method to retrieve the JWT token from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6faa-157">Next, add the following method to retrieve the JWT token from Azure Active Directory.</span></span> <span data-ttu-id="d6faa-158">For maintainability, you may want to move the hard-coded string values into your web or application configuration.</span><span class="sxs-lookup"><span data-stu-id="d6faa-158">For maintainability, you may want to move the hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="d6faa-159">Add the necessary code to call Key Vault and retrieve your secret value.</span><span class="sxs-lookup"><span data-stu-id="d6faa-159">Add the necessary code to call Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="d6faa-160">First you must add the following using statement:</span><span class="sxs-lookup"><span data-stu-id="d6faa-160">First you must add the following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="d6faa-161">Add the method calls to invoke Key Vault and retrieve your secret.</span><span class="sxs-lookup"><span data-stu-id="d6faa-161">Add the method calls to invoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="d6faa-162">In this method, you provide the secret URI that you saved in a previous step.</span><span class="sxs-lookup"><span data-stu-id="d6faa-162">In this method, you provide the secret URI that you saved in a previous step.</span></span> <span data-ttu-id="d6faa-163">Note the use of the **GetToken** method from the **Utils** class created previously.</span><span class="sxs-lookup"><span data-stu-id="d6faa-163">Note the use of the **GetToken** method from the **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="d6faa-164">When you run your application, you should now be authenticating to Azure Active Directory and then retrieving your secret value from Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d6faa-164">When you run your application, you should now be authenticating to Azure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="d6faa-165">Key rotation using Azure Automation</span><span class="sxs-lookup"><span data-stu-id="d6faa-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="d6faa-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span><span class="sxs-lookup"><span data-stu-id="d6faa-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="d6faa-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span><span class="sxs-lookup"><span data-stu-id="d6faa-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="d6faa-168">For the purposes of this article, you will be using Azure PowerShell combined with Azure Automation to change an Azure Storage Account access key.</span><span class="sxs-lookup"><span data-stu-id="d6faa-168">For the purposes of this article, you will be using Azure PowerShell combined with Azure Automation to change an Azure Storage Account access key.</span></span> <span data-ttu-id="d6faa-169">You will then update a key vault secret with that new key.</span><span class="sxs-lookup"><span data-stu-id="d6faa-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="d6faa-170">To allow Azure Automation to set secret values in your key vault, you must get the client ID for the connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span><span class="sxs-lookup"><span data-stu-id="d6faa-170">To allow Azure Automation to set secret values in your key vault, you must get the client ID for the connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="d6faa-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span><span class="sxs-lookup"><span data-stu-id="d6faa-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="d6faa-172">From there, you choose **Connections** and then select the **AzureRunAsConnection** service principle.</span><span class="sxs-lookup"><span data-stu-id="d6faa-172">From there, you choose **Connections** and then select the **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="d6faa-173">Take note of the **Application ID**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-173">Take note of the **Application ID**.</span></span>

![Azure Automation client ID](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="d6faa-175">In **Assets**, choose **Modules**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="d6faa-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of the following modules:</span><span class="sxs-lookup"><span data-stu-id="d6faa-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of the following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="d6faa-177">At the writing of this article, only the previously noted modules needed to be updated for the following script.</span><span class="sxs-lookup"><span data-stu-id="d6faa-177">At the writing of this article, only the previously noted modules needed to be updated for the following script.</span></span> <span data-ttu-id="d6faa-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span><span class="sxs-lookup"><span data-stu-id="d6faa-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="d6faa-179">After you have retrieved the application ID for your Azure Automation connection, you must tell your key vault that this application has access to update secrets in your vault.</span><span class="sxs-lookup"><span data-stu-id="d6faa-179">After you have retrieved the application ID for your Azure Automation connection, you must tell your key vault that this application has access to update secrets in your vault.</span></span> <span data-ttu-id="d6faa-180">This can be accomplished with the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="d6faa-180">This can be accomplished with the following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="d6faa-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="d6faa-182">Select **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-182">Select **Quick Create**.</span></span> <span data-ttu-id="d6faa-183">Name your runbook and select **PowerShell** as the runbook type.</span><span class="sxs-lookup"><span data-stu-id="d6faa-183">Name your runbook and select **PowerShell** as the runbook type.</span></span> <span data-ttu-id="d6faa-184">You have the option to add a description.</span><span class="sxs-lookup"><span data-stu-id="d6faa-184">You have the option to add a description.</span></span> <span data-ttu-id="d6faa-185">Finally, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-185">Finally, click **Create**.</span></span>

![Create runbook](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="d6faa-187">Paste the following PowerShell script in the editor pane for your new runbook:</span><span class="sxs-lookup"><span data-stu-id="d6faa-187">Paste the following PowerShell script in the editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get the connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in to Azure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set the following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for the storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="d6faa-188">From the editor pane, choose **Test pane** to test your script.</span><span class="sxs-lookup"><span data-stu-id="d6faa-188">From the editor pane, choose **Test pane** to test your script.</span></span> <span data-ttu-id="d6faa-189">Once the script is running without error, you can select **Publish**, and then you can apply a schedule for the runbook back in the runbook configuration pane.</span><span class="sxs-lookup"><span data-stu-id="d6faa-189">Once the script is running without error, you can select **Publish**, and then you can apply a schedule for the runbook back in the runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="d6faa-190">Key Vault auditing pipeline</span><span class="sxs-lookup"><span data-stu-id="d6faa-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="d6faa-191">When you set up a key vault, you can turn on auditing to collect logs on access requests made to the key vault.</span><span class="sxs-lookup"><span data-stu-id="d6faa-191">When you set up a key vault, you can turn on auditing to collect logs on access requests made to the key vault.</span></span> <span data-ttu-id="d6faa-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span><span class="sxs-lookup"><span data-stu-id="d6faa-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="d6faa-193">The following scenario uses Azure functions, Azure logic apps, and key vault audit logs to create a pipeline to send an email when an app that does match the app ID of the web app retrieves secrets from the vault.</span><span class="sxs-lookup"><span data-stu-id="d6faa-193">The following scenario uses Azure functions, Azure logic apps, and key vault audit logs to create a pipeline to send an email when an app that does match the app ID of the web app retrieves secrets from the vault.</span></span>

<span data-ttu-id="d6faa-194">First, you must enable logging on your key vault.</span><span class="sxs-lookup"><span data-stu-id="d6faa-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="d6faa-195">This can be done via the following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="d6faa-195">This can be done via the following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="d6faa-196">After this is enabled, audit logs start collecting into the designated storage account.</span><span class="sxs-lookup"><span data-stu-id="d6faa-196">After this is enabled, audit logs start collecting into the designated storage account.</span></span> <span data-ttu-id="d6faa-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span><span class="sxs-lookup"><span data-stu-id="d6faa-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="d6faa-198">You can access your logging information 10 minutes after the key vault operation.</span><span class="sxs-lookup"><span data-stu-id="d6faa-198">You can access your logging information 10 minutes after the key vault operation.</span></span> <span data-ttu-id="d6faa-199">It will usually be quicker than this.</span><span class="sxs-lookup"><span data-stu-id="d6faa-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="d6faa-200">The next step is to [create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="d6faa-200">The next step is to [create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="d6faa-201">This is where key vault audit logs are pushed.</span><span class="sxs-lookup"><span data-stu-id="d6faa-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="d6faa-202">When the audit log messages are in the queue, the logic app picks them up and acts on them.</span><span class="sxs-lookup"><span data-stu-id="d6faa-202">When the audit log messages are in the queue, the logic app picks them up and acts on them.</span></span> <span data-ttu-id="d6faa-203">Create a service bus with the following steps:</span><span class="sxs-lookup"><span data-stu-id="d6faa-203">Create a service bus with the following steps:</span></span>

1. <span data-ttu-id="d6faa-204">Create a Service Bus namespace (if you already have one that you want to use for this, skip to Step 2).</span><span class="sxs-lookup"><span data-stu-id="d6faa-204">Create a Service Bus namespace (if you already have one that you want to use for this, skip to Step 2).</span></span>
2. <span data-ttu-id="d6faa-205">Browse to the service bus in the Azure portal and select the namespace you want to create the queue in.</span><span class="sxs-lookup"><span data-stu-id="d6faa-205">Browse to the service bus in the Azure portal and select the namespace you want to create the queue in.</span></span>
3. <span data-ttu-id="d6faa-206">Select **New** and choose **Service Bus > Queue** and enter the required details.</span><span class="sxs-lookup"><span data-stu-id="d6faa-206">Select **New** and choose **Service Bus > Queue** and enter the required details.</span></span>
4. <span data-ttu-id="d6faa-207">Select the Service Bus connection information by choosing the namespace and clicking **Connection Information**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-207">Select the Service Bus connection information by choosing the namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="d6faa-208">You will need this information for the next section.</span><span class="sxs-lookup"><span data-stu-id="d6faa-208">You will need this information for the next section.</span></span>

<span data-ttu-id="d6faa-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) to poll key vault logs within the storage account and pick up new events.</span><span class="sxs-lookup"><span data-stu-id="d6faa-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) to poll key vault logs within the storage account and pick up new events.</span></span> <span data-ttu-id="d6faa-210">This will be a function that is triggered on a schedule.</span><span class="sxs-lookup"><span data-stu-id="d6faa-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="d6faa-211">To create an Azure function, choose **New > Function App** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d6faa-211">To create an Azure function, choose **New > Function App** in the Azure portal.</span></span> <span data-ttu-id="d6faa-212">During creation, you can use an existing hosting plan or create a new one.</span><span class="sxs-lookup"><span data-stu-id="d6faa-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="d6faa-213">You could also opt for dynamic hosting.</span><span class="sxs-lookup"><span data-stu-id="d6faa-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="d6faa-214">More details on Function hosting options can be found at [How to scale Azure Functions](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="d6faa-214">More details on Function hosting options can be found at [How to scale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="d6faa-215">When the Azure function is created, navigate to it and choose a timer function and C\#.</span><span class="sxs-lookup"><span data-stu-id="d6faa-215">When the Azure function is created, navigate to it and choose a timer function and C\#.</span></span> <span data-ttu-id="d6faa-216">Then click **Create this function**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-216">Then click **Create this function**.</span></span>

![Azure Functions Start blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="d6faa-218">On the **Develop** tab, replace the run.csx code with the following:</span><span class="sxs-lookup"><span data-stu-id="d6faa-218">On the **Develop** tab, replace the run.csx code with the following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting to now.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required to order by time as they may not be in the file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending to ServiceBus, use the payloadStream and set keeporiginal to true
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="d6faa-219">Make sure to replace the variables in the preceding code to point to your storage account where the key vault logs are written, the service bus you created earlier, and the specific path to the key vault storage logs.</span><span class="sxs-lookup"><span data-stu-id="d6faa-219">Make sure to replace the variables in the preceding code to point to your storage account where the key vault logs are written, the service bus you created earlier, and the specific path to the key vault storage logs.</span></span>
>
>

<span data-ttu-id="d6faa-220">The function picks up the latest log file from the storage account where the key vault logs are written, grabs the latest events from that file, and pushes them to a Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="d6faa-220">The function picks up the latest log file from the storage account where the key vault logs are written, grabs the latest events from that file, and pushes them to a Service Bus queue.</span></span> <span data-ttu-id="d6faa-221">Since a single file could have multiple events, you should create a sync.txt file that the function also looks at to determine the time stamp of the last event that was picked up.</span><span class="sxs-lookup"><span data-stu-id="d6faa-221">Since a single file could have multiple events, you should create a sync.txt file that the function also looks at to determine the time stamp of the last event that was picked up.</span></span> <span data-ttu-id="d6faa-222">This ensures that you don't push the same event multiple times.</span><span class="sxs-lookup"><span data-stu-id="d6faa-222">This ensures that you don't push the same event multiple times.</span></span> <span data-ttu-id="d6faa-223">This sync.txt file contains a timestamp for the last encountered event.</span><span class="sxs-lookup"><span data-stu-id="d6faa-223">This sync.txt file contains a timestamp for the last encountered event.</span></span> <span data-ttu-id="d6faa-224">The logs, when loaded, have to be sorted based on the timestamp to ensure they are ordered correctly.</span><span class="sxs-lookup"><span data-stu-id="d6faa-224">The logs, when loaded, have to be sorted based on the timestamp to ensure they are ordered correctly.</span></span>

<span data-ttu-id="d6faa-225">For this function, we reference a couple of additional libraries that are not available out of the box in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="d6faa-225">For this function, we reference a couple of additional libraries that are not available out of the box in Azure Functions.</span></span> <span data-ttu-id="d6faa-226">To include these, we need Azure Functions to pull them using NuGet.</span><span class="sxs-lookup"><span data-stu-id="d6faa-226">To include these, we need Azure Functions to pull them using NuGet.</span></span> <span data-ttu-id="d6faa-227">Choose the **View Files** option.</span><span class="sxs-lookup"><span data-stu-id="d6faa-227">Choose the **View Files** option.</span></span>

![View Files option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="d6faa-229">And add a file called project.json with following content:</span><span class="sxs-lookup"><span data-stu-id="d6faa-229">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="d6faa-230">Upon **Save**, Azure Functions will download the required binaries.</span><span class="sxs-lookup"><span data-stu-id="d6faa-230">Upon **Save**, Azure Functions will download the required binaries.</span></span>

<span data-ttu-id="d6faa-231">Switch to the **Integrate** tab and give the timer parameter a meaningful name to use within the function.</span><span class="sxs-lookup"><span data-stu-id="d6faa-231">Switch to the **Integrate** tab and give the timer parameter a meaningful name to use within the function.</span></span> <span data-ttu-id="d6faa-232">In the preceding code, it expects the timer to be called *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="d6faa-232">In the preceding code, it expects the timer to be called *myTimer*.</span></span> <span data-ttu-id="d6faa-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for the timer that will cause the function to run once a minute.</span><span class="sxs-lookup"><span data-stu-id="d6faa-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for the timer that will cause the function to run once a minute.</span></span>

<span data-ttu-id="d6faa-234">On the same **Integrate** tab, add an input of the type **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-234">On the same **Integrate** tab, add an input of the type **Azure Blob Storage**.</span></span> <span data-ttu-id="d6faa-235">This will point to the sync.txt file that contains the timestamp of the last event looked at by the function.</span><span class="sxs-lookup"><span data-stu-id="d6faa-235">This will point to the sync.txt file that contains the timestamp of the last event looked at by the function.</span></span> <span data-ttu-id="d6faa-236">This will be available within the function by the parameter name.</span><span class="sxs-lookup"><span data-stu-id="d6faa-236">This will be available within the function by the parameter name.</span></span> <span data-ttu-id="d6faa-237">In the preceding code, the Azure Blob Storage input expects the parameter name to be *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="d6faa-237">In the preceding code, the Azure Blob Storage input expects the parameter name to be *inputBlob*.</span></span> <span data-ttu-id="d6faa-238">Choose the storage account where the sync.txt file will reside (it could be the same or a different storage account).</span><span class="sxs-lookup"><span data-stu-id="d6faa-238">Choose the storage account where the sync.txt file will reside (it could be the same or a different storage account).</span></span> <span data-ttu-id="d6faa-239">In the path field, provide the path where the file lives in the format {container-name}/path/to/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="d6faa-239">In the path field, provide the path where the file lives in the format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="d6faa-240">Add an output of the type *Azure Blob Storage* output.</span><span class="sxs-lookup"><span data-stu-id="d6faa-240">Add an output of the type *Azure Blob Storage* output.</span></span> <span data-ttu-id="d6faa-241">This will point to the sync.txt file you defined in the input.</span><span class="sxs-lookup"><span data-stu-id="d6faa-241">This will point to the sync.txt file you defined in the input.</span></span> <span data-ttu-id="d6faa-242">This is used by the function to write the timestamp of the last event looked at.</span><span class="sxs-lookup"><span data-stu-id="d6faa-242">This is used by the function to write the timestamp of the last event looked at.</span></span> <span data-ttu-id="d6faa-243">The preceding code expects this parameter to be called *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="d6faa-243">The preceding code expects this parameter to be called *outputBlob*.</span></span>

<span data-ttu-id="d6faa-244">At this point, the function is ready.</span><span class="sxs-lookup"><span data-stu-id="d6faa-244">At this point, the function is ready.</span></span> <span data-ttu-id="d6faa-245">Make sure to switch back to the **Develop** tab and save the code.</span><span class="sxs-lookup"><span data-stu-id="d6faa-245">Make sure to switch back to the **Develop** tab and save the code.</span></span> <span data-ttu-id="d6faa-246">Check the output window for any compilation errors and correct them accordingly.</span><span class="sxs-lookup"><span data-stu-id="d6faa-246">Check the output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="d6faa-247">If the code compiles, then the code should now be checking the key vault logs every minute and pushing any new events onto the defined Service Bus queue.</span><span class="sxs-lookup"><span data-stu-id="d6faa-247">If the code compiles, then the code should now be checking the key vault logs every minute and pushing any new events onto the defined Service Bus queue.</span></span> <span data-ttu-id="d6faa-248">You should see logging information write out to the log window every time the function is triggered.</span><span class="sxs-lookup"><span data-stu-id="d6faa-248">You should see logging information write out to the log window every time the function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="d6faa-249">Azure logic app</span><span class="sxs-lookup"><span data-stu-id="d6faa-249">Azure logic app</span></span>
<span data-ttu-id="d6faa-250">Next you must create an Azure logic app that picks up the events that the function is pushing to the Service Bus queue, parses the content, and sends an email based on a condition being matched.</span><span class="sxs-lookup"><span data-stu-id="d6faa-250">Next you must create an Azure logic app that picks up the events that the function is pushing to the Service Bus queue, parses the content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="d6faa-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going to **New > Logic App**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going to **New > Logic App**.</span></span>

<span data-ttu-id="d6faa-252">Once the logic app is created, navigate to it and choose **edit**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-252">Once the logic app is created, navigate to it and choose **edit**.</span></span> <span data-ttu-id="d6faa-253">Within the logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials to connect it to the queue.</span><span class="sxs-lookup"><span data-stu-id="d6faa-253">Within the logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials to connect it to the queue.</span></span>

![Azure Logic App Service Bus](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="d6faa-255">Next choose **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="d6faa-256">In the condition, switch to the advanced editor and enter the following code, replacing APP_ID with the actual APP_ID of your web app:</span><span class="sxs-lookup"><span data-stu-id="d6faa-256">In the condition, switch to the advanced editor and enter the following code, replacing APP_ID with the actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="d6faa-257">This expression essentially returns **false** if the *appid* from the incoming event (which is the body of the Service Bus message) is not the *appid* of the app.</span><span class="sxs-lookup"><span data-stu-id="d6faa-257">This expression essentially returns **false** if the *appid* from the incoming event (which is the body of the Service Bus message) is not the *appid* of the app.</span></span>

<span data-ttu-id="d6faa-258">Now, create an action under **If no, do nothing**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-258">Now, create an action under **If no, do nothing**.</span></span>

![Azure Logic App choose action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="d6faa-260">For the action, choose **Office 365 - send email**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-260">For the action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="d6faa-261">Fill out the fields to create an email to send when the defined condition returns **false**.</span><span class="sxs-lookup"><span data-stu-id="d6faa-261">Fill out the fields to create an email to send when the defined condition returns **false**.</span></span> <span data-ttu-id="d6faa-262">If you do not have Office 365, you could look at alternatives to achieve the same results.</span><span class="sxs-lookup"><span data-stu-id="d6faa-262">If you do not have Office 365, you could look at alternatives to achieve the same results.</span></span>

<span data-ttu-id="d6faa-263">At this point, you have an end to end pipeline that looks for new key vault audit logs once a minute.</span><span class="sxs-lookup"><span data-stu-id="d6faa-263">At this point, you have an end to end pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="d6faa-264">It pushes new logs it finds to a service bus queue.</span><span class="sxs-lookup"><span data-stu-id="d6faa-264">It pushes new logs it finds to a service bus queue.</span></span> <span data-ttu-id="d6faa-265">The logic app is triggered when a new message lands in the queue.</span><span class="sxs-lookup"><span data-stu-id="d6faa-265">The logic app is triggered when a new message lands in the queue.</span></span> <span data-ttu-id="d6faa-266">If the *appid* within the event does not match the app ID of the calling application, it sends an email.</span><span class="sxs-lookup"><span data-stu-id="d6faa-266">If the *appid* within the event does not match the app ID of the calling application, it sends an email.</span></span>











