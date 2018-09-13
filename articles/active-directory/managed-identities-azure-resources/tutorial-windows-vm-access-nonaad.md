---
title: Use a Windows VM system-assigned managed identity to access Azure Key Vault
description: A tutorial that walks you through the process of using a Windows VM system-assigned managed identity to access Azure Key Vault.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: daveba
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/20/2017
ms.author: daveba
ms.openlocfilehash: fffa77990b0af3c710a60d2077962257ab50d5e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857663"
---
# <a name="tutorial-use-a-windows-vm-system-assigned-managed-identity-to-access-azure-key-vault"></a><span data-ttu-id="cdab6-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="cdab6-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Key Vault</span></span> 

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="cdab6-104">This tutorial shows you how to use a system-assigned managed identity for a Windows virtual machine (VM) to access Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cdab6-104">This tutorial shows you how to use a system-assigned managed identity for a Windows virtual machine (VM) to access Azure Key Vault.</span></span> <span data-ttu-id="cdab6-105">Serving as a bootstrap, Key Vault makes it possible for your client application to then use the secret to access resources not secured by Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="cdab6-105">Serving as a bootstrap, Key Vault makes it possible for your client application to then use the secret to access resources not secured by Azure Active Directory (AD).</span></span> <span data-ttu-id="cdab6-106">Managed Service Identities are automatically managed by Azure and enable you to authenticate to services that support Azure AD authentication, without needing to insert credentials into your code.</span><span class="sxs-lookup"><span data-stu-id="cdab6-106">Managed Service Identities are automatically managed by Azure and enable you to authenticate to services that support Azure AD authentication, without needing to insert credentials into your code.</span></span> 

<span data-ttu-id="cdab6-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="cdab6-107">You learn how to:</span></span>


> [!div class="checklist"]
> * <span data-ttu-id="cdab6-108">Grant your VM access to a secret stored in a Key Vault</span><span class="sxs-lookup"><span data-stu-id="cdab6-108">Grant your VM access to a secret stored in a Key Vault</span></span> 
> * <span data-ttu-id="cdab6-109">Get an access token using the VM identity and use it to retrieve the secret from Key Vault</span><span class="sxs-lookup"><span data-stu-id="cdab6-109">Get an access token using the VM identity and use it to retrieve the secret from Key Vault</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cdab6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cdab6-110">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="cdab6-111">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="cdab6-111">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="cdab6-112">Create a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="cdab6-112">Create a Windows virtual machine</span></span>](/azure/virtual-machines/windows/quick-create-portal)

- [<span data-ttu-id="cdab6-113">Enable system-assigned managed identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="cdab6-113">Enable system-assigned managed identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

## <a name="grant-your-vm-access-to-a-secret-stored-in-a-key-vault"></a><span data-ttu-id="cdab6-114">Grant your VM access to a Secret stored in a Key Vault</span><span class="sxs-lookup"><span data-stu-id="cdab6-114">Grant your VM access to a Secret stored in a Key Vault</span></span> 
 
<span data-ttu-id="cdab6-115">Using managed identities for Azure resources, your code can get access tokens to authenticate to resources that support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="cdab6-115">Using managed identities for Azure resources, your code can get access tokens to authenticate to resources that support Azure AD authentication.</span></span><span data-ttu-id="cdab6-116">  However, not all Azure services support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="cdab6-116">  However, not all Azure services support Azure AD authentication.</span></span> <span data-ttu-id="cdab6-117">To use managed identities for Azure resources with those services, store the service credentials in Azure Key Vault, and use the VM's managed identity to access Key Vault to retrieve the credentials.</span><span class="sxs-lookup"><span data-stu-id="cdab6-117">To use managed identities for Azure resources with those services, store the service credentials in Azure Key Vault, and use the VM's managed identity to access Key Vault to retrieve the credentials.</span></span> 

<span data-ttu-id="cdab6-118">First, we need to create a Key Vault and grant our VM’s system-assigned managed identity access to the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cdab6-118">First, we need to create a Key Vault and grant our VM’s system-assigned managed identity access to the Key Vault.</span></span>   

1. <span data-ttu-id="cdab6-119">At the top of the left navigation bar, select **Create a resource** > **Security + Identity** > **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="cdab6-119">At the top of the left navigation bar, select **Create a resource** > **Security + Identity** > **Key Vault**.</span></span>  
2. <span data-ttu-id="cdab6-120">Provide a **Name** for the new Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cdab6-120">Provide a **Name** for the new Key Vault.</span></span> 
3. <span data-ttu-id="cdab6-121">Locate the Key Vault in the same subscription and resource group as the VM you created earlier.</span><span class="sxs-lookup"><span data-stu-id="cdab6-121">Locate the Key Vault in the same subscription and resource group as the VM you created earlier.</span></span> 
4. <span data-ttu-id="cdab6-122">Select **Access policies** and click **Add new**.</span><span class="sxs-lookup"><span data-stu-id="cdab6-122">Select **Access policies** and click **Add new**.</span></span> 
5. <span data-ttu-id="cdab6-123">In Configure from template, select **Secret Management**.</span><span class="sxs-lookup"><span data-stu-id="cdab6-123">In Configure from template, select **Secret Management**.</span></span> 
6. <span data-ttu-id="cdab6-124">Choose **Select Principal**, and in the search field enter the name of the VM you created earlier.</span><span class="sxs-lookup"><span data-stu-id="cdab6-124">Choose **Select Principal**, and in the search field enter the name of the VM you created earlier.</span></span>  <span data-ttu-id="cdab6-125">Select the VM in the result list and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="cdab6-125">Select the VM in the result list and click **Select**.</span></span> 
7. <span data-ttu-id="cdab6-126">Click **OK** to finishing adding the new access policy, and **OK** to finish access policy selection.</span><span class="sxs-lookup"><span data-stu-id="cdab6-126">Click **OK** to finishing adding the new access policy, and **OK** to finish access policy selection.</span></span> 
8. <span data-ttu-id="cdab6-127">Click **Create** to finish creating the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cdab6-127">Click **Create** to finish creating the Key Vault.</span></span> 

    ![Alt image text](./media/msi-tutorial-windows-vm-access-nonaad/msi-blade.png)


<span data-ttu-id="cdab6-129">Next, add a secret to the Key Vault, so that later you can retrieve the secret using code running in your VM:</span><span class="sxs-lookup"><span data-stu-id="cdab6-129">Next, add a secret to the Key Vault, so that later you can retrieve the secret using code running in your VM:</span></span> 

1. <span data-ttu-id="cdab6-130">Select **All Resources**, and find and select the Key Vault you created.</span><span class="sxs-lookup"><span data-stu-id="cdab6-130">Select **All Resources**, and find and select the Key Vault you created.</span></span> 
2. <span data-ttu-id="cdab6-131">Select **Secrets**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="cdab6-131">Select **Secrets**, and click **Add**.</span></span> 
3. <span data-ttu-id="cdab6-132">Select **Manual**, from **Upload options**.</span><span class="sxs-lookup"><span data-stu-id="cdab6-132">Select **Manual**, from **Upload options**.</span></span> 
4. <span data-ttu-id="cdab6-133">Enter a name and value for the secret.</span><span class="sxs-lookup"><span data-stu-id="cdab6-133">Enter a name and value for the secret.</span></span>  <span data-ttu-id="cdab6-134">The value can be anything you want.</span><span class="sxs-lookup"><span data-stu-id="cdab6-134">The value can be anything you want.</span></span> 
5. <span data-ttu-id="cdab6-135">Leave the activation date and expiration date clear, and leave **Enabled** as **Yes**.</span><span class="sxs-lookup"><span data-stu-id="cdab6-135">Leave the activation date and expiration date clear, and leave **Enabled** as **Yes**.</span></span> 
6. <span data-ttu-id="cdab6-136">Click **Create** to create the secret.</span><span class="sxs-lookup"><span data-stu-id="cdab6-136">Click **Create** to create the secret.</span></span> 
 
## <a name="get-an-access-token-using-the-vm-identity-and-use-it-to-retrieve-the-secret-from-the-key-vault"></a><span data-ttu-id="cdab6-137">Get an access token using the VM identity and use it to retrieve the secret from the Key Vault</span><span class="sxs-lookup"><span data-stu-id="cdab6-137">Get an access token using the VM identity and use it to retrieve the secret from the Key Vault</span></span>  

<span data-ttu-id="cdab6-138">If you don’t have PowerShell 4.3.1 or greater installed, you'll need to [download and install the latest version](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cdab6-138">If you don’t have PowerShell 4.3.1 or greater installed, you'll need to [download and install the latest version](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="cdab6-139">First, we use the VM’s system-assigned managed identity to get an access token to authenticate to Key Vault:</span><span class="sxs-lookup"><span data-stu-id="cdab6-139">First, we use the VM’s system-assigned managed identity to get an access token to authenticate to Key Vault:</span></span>
 
1. <span data-ttu-id="cdab6-140">In the portal, navigate to **Virtual Machines** and go to your Windows virtual machine and in the **Overview**, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="cdab6-140">In the portal, navigate to **Virtual Machines** and go to your Windows virtual machine and in the **Overview**, click **Connect**.</span></span>
2. <span data-ttu-id="cdab6-141">Enter in your **Username** and **Password** for which you added when you created the **Windows VM**.</span><span class="sxs-lookup"><span data-stu-id="cdab6-141">Enter in your **Username** and **Password** for which you added when you created the **Windows VM**.</span></span>  
3. <span data-ttu-id="cdab6-142">Now that you have created a **Remote Desktop Connection** with the virtual machine, open PowerShell in the remote session.</span><span class="sxs-lookup"><span data-stu-id="cdab6-142">Now that you have created a **Remote Desktop Connection** with the virtual machine, open PowerShell in the remote session.</span></span>  
4. <span data-ttu-id="cdab6-143">In PowerShell, invoke the web request on the tenant to get the token for the local host in the specific port for the VM.</span><span class="sxs-lookup"><span data-stu-id="cdab6-143">In PowerShell, invoke the web request on the tenant to get the token for the local host in the specific port for the VM.</span></span>  

    <span data-ttu-id="cdab6-144">The PowerShell request:</span><span class="sxs-lookup"><span data-stu-id="cdab6-144">The PowerShell request:</span></span>
    
    ```powershell
    $response = Invoke-WebRequest -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fvault.azure.net' -Method GET -Headers @{Metadata="true"} 
    ```
    
    <span data-ttu-id="cdab6-145">Next, extract the full response which is stored as a JavaScript Object Notation (JSON) formatted string in the $response object.</span><span class="sxs-lookup"><span data-stu-id="cdab6-145">Next, extract the full response which is stored as a JavaScript Object Notation (JSON) formatted string in the $response object.</span></span>  
    
    ```powershell
    $content = $response.Content | ConvertFrom-Json 
    ```
    
    <span data-ttu-id="cdab6-146">Next, extract the access token from the response.</span><span class="sxs-lookup"><span data-stu-id="cdab6-146">Next, extract the access token from the response.</span></span>  
    
    ```powershell
    $KeyVaultToken = $content.access_token 
    ```
    
    <span data-ttu-id="cdab6-147">Finally, use PowerShell’s Invoke-WebRequest command to retrieve the secret you created earlier in the Key Vault, passing the access token in the Authorization header.</span><span class="sxs-lookup"><span data-stu-id="cdab6-147">Finally, use PowerShell’s Invoke-WebRequest command to retrieve the secret you created earlier in the Key Vault, passing the access token in the Authorization header.</span></span>  <span data-ttu-id="cdab6-148">You’ll need the URL of your Key Vault, which is in the **Essentials** section of the **Overview** page of the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cdab6-148">You’ll need the URL of your Key Vault, which is in the **Essentials** section of the **Overview** page of the Key Vault.</span></span>  
    
    ```powershell
    (Invoke-WebRequest -Uri https://<your-key-vault-URL>/secrets/<secret-name>?api-version=2016-10-01 -Method GET -Headers @{Authorization="Bearer $KeyVaultToken"}).content 
    ```
    
    <span data-ttu-id="cdab6-149">The response will look like this:</span><span class="sxs-lookup"><span data-stu-id="cdab6-149">The response will look like this:</span></span> 
    
    ```powershell
    {"value":"p@ssw0rd!","id":"https://mytestkeyvault.vault.azure.net/secrets/MyTestSecret/7c2204c6093c4d859bc5b9eff8f29050","attributes":{"enabled":true,"created":1505088747,"updated":1505088747,"recoveryLevel":"Purgeable"}} 
    ```
    
<span data-ttu-id="cdab6-150">Once you’ve retrieved the secret from the Key Vault, you can use it to authenticate to a service that requires a name and password.</span><span class="sxs-lookup"><span data-stu-id="cdab6-150">Once you’ve retrieved the secret from the Key Vault, you can use it to authenticate to a service that requires a name and password.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cdab6-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="cdab6-151">Next steps</span></span>

<span data-ttu-id="cdab6-152">In this tutorial, you learned how use a Windows VM system-assigned managed identity to access Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cdab6-152">In this tutorial, you learned how use a Windows VM system-assigned managed identity to access Azure Key Vault.</span></span>  <span data-ttu-id="cdab6-153">To learn more about Azure Key Vault see:</span><span class="sxs-lookup"><span data-stu-id="cdab6-153">To learn more about Azure Key Vault see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="cdab6-154">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="cdab6-154">Azure Key Vault</span></span>](/azure/key-vault/key-vault-whatis)
