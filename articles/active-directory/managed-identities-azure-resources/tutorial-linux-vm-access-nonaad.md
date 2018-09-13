---
title: Use a Linux VM system-assigned managed identity to access Azure Key Vault
description: A tutorial that walks you through the process of using a Linux VM system-assigned managed identity to access Azure Resource Manager.
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
ms.openlocfilehash: 300565509b2f0903b6c730be7e0693ba0e298e07
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865676"
---
# <a name="tutorial-use-a-linux-vm-system-assigned-managed-identity-to-access-azure-key-vault"></a><span data-ttu-id="30915-103">Tutorial: Use a Linux VM system-assigned managed identity to access Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="30915-103">Tutorial: Use a Linux VM system-assigned managed identity to access Azure Key Vault</span></span> 

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="30915-104">This tutorial shows you how to to use a system-assigned managed identity for a Linux virtual machine (VM) to access Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="30915-104">This tutorial shows you how to to use a system-assigned managed identity for a Linux virtual machine (VM) to access Azure Key Vault.</span></span> <span data-ttu-id="30915-105">Serving as a bootstrap, Key Vault makes it possible for your client application to then use the secret to access resources not secured by Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="30915-105">Serving as a bootstrap, Key Vault makes it possible for your client application to then use the secret to access resources not secured by Azure Active Directory (AD).</span></span> <span data-ttu-id="30915-106">Managed identities for Azure resources are automatically managed by Azure and enable you to authenticate to services that support Azure AD authentication, without needing to insert credentials into your code.</span><span class="sxs-lookup"><span data-stu-id="30915-106">Managed identities for Azure resources are automatically managed by Azure and enable you to authenticate to services that support Azure AD authentication, without needing to insert credentials into your code.</span></span> 

<span data-ttu-id="30915-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="30915-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="30915-108">Grant your VM access to a secret stored in a Key Vault</span><span class="sxs-lookup"><span data-stu-id="30915-108">Grant your VM access to a secret stored in a Key Vault</span></span> 
> * <span data-ttu-id="30915-109">Get an access token using the VM's identity and use it to retrieve the secret from the Key Vault</span><span class="sxs-lookup"><span data-stu-id="30915-109">Get an access token using the VM's identity and use it to retrieve the secret from the Key Vault</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="30915-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="30915-110">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="30915-111">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="30915-111">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="30915-112">Create a Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="30915-112">Create a Linux virtual machine</span></span>](/azure/virtual-machines/linux/quick-create-portal)

- [<span data-ttu-id="30915-113">Enable system-assigned managed identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="30915-113">Enable system-assigned managed identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

## <a name="grant-your-vm-access-to-a-secret-stored-in-a-key-vault"></a><span data-ttu-id="30915-114">Grant your VM access to a Secret stored in a Key Vault</span><span class="sxs-lookup"><span data-stu-id="30915-114">Grant your VM access to a Secret stored in a Key Vault</span></span>  

<span data-ttu-id="30915-115">Using managed service identities for Azure resources your code can get access tokens to authenticate to resources that support Azure Active Directory authentication.</span><span class="sxs-lookup"><span data-stu-id="30915-115">Using managed service identities for Azure resources your code can get access tokens to authenticate to resources that support Azure Active Directory authentication.</span></span><span data-ttu-id="30915-116"> However, not all Azure services support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="30915-116"> However, not all Azure services support Azure AD authentication.</span></span> <span data-ttu-id="30915-117">To use managed identities for Azure resources with those services, store the service credentials in Azure Key Vault, and use managed identities for Azure resources to access Key Vault to retrieve the credentials.</span><span class="sxs-lookup"><span data-stu-id="30915-117">To use managed identities for Azure resources with those services, store the service credentials in Azure Key Vault, and use managed identities for Azure resources to access Key Vault to retrieve the credentials.</span></span> 

<span data-ttu-id="30915-118">First, we need to create a Key Vault and grant our VM’s system-assigned managed identity access to the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="30915-118">First, we need to create a Key Vault and grant our VM’s system-assigned managed identity access to the Key Vault.</span></span>   

1. <span data-ttu-id="30915-119">At the top of the left navigation bar, select **Create a resource** > **Security + Identity** > **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="30915-119">At the top of the left navigation bar, select **Create a resource** > **Security + Identity** > **Key Vault**.</span></span>  
2. <span data-ttu-id="30915-120">Provide a **Name** for the new Key Vault.</span><span class="sxs-lookup"><span data-stu-id="30915-120">Provide a **Name** for the new Key Vault.</span></span> 
3. <span data-ttu-id="30915-121">Locate the Key Vault in the same subscription and resource group as the VM you created earlier.</span><span class="sxs-lookup"><span data-stu-id="30915-121">Locate the Key Vault in the same subscription and resource group as the VM you created earlier.</span></span> 
4. <span data-ttu-id="30915-122">Select **Access policies** and click **Add new**.</span><span class="sxs-lookup"><span data-stu-id="30915-122">Select **Access policies** and click **Add new**.</span></span> 
5. <span data-ttu-id="30915-123">In Configure from template, select **Secret Management**.</span><span class="sxs-lookup"><span data-stu-id="30915-123">In Configure from template, select **Secret Management**.</span></span> 
6. <span data-ttu-id="30915-124">Choose **Select Principal**, and in the search field enter the name of the VM you created earlier.</span><span class="sxs-lookup"><span data-stu-id="30915-124">Choose **Select Principal**, and in the search field enter the name of the VM you created earlier.</span></span>  <span data-ttu-id="30915-125">Select the VM in the result list and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="30915-125">Select the VM in the result list and click **Select**.</span></span> 
7. <span data-ttu-id="30915-126">Click **OK** to finishing adding the new access policy, and **OK** to finish access policy selection.</span><span class="sxs-lookup"><span data-stu-id="30915-126">Click **OK** to finishing adding the new access policy, and **OK** to finish access policy selection.</span></span> 
8. <span data-ttu-id="30915-127">Click **Create** to finish creating the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="30915-127">Click **Create** to finish creating the Key Vault.</span></span> 

    ![Alt image text](./media/msi-tutorial-windows-vm-access-nonaad/msi-blade.png)

<span data-ttu-id="30915-129">Next, add a secret to the Key Vault, so that later you can retrieve the secret using code running in your VM:</span><span class="sxs-lookup"><span data-stu-id="30915-129">Next, add a secret to the Key Vault, so that later you can retrieve the secret using code running in your VM:</span></span> 

1. <span data-ttu-id="30915-130">Select **All Resources**, and find and select the Key Vault you created.</span><span class="sxs-lookup"><span data-stu-id="30915-130">Select **All Resources**, and find and select the Key Vault you created.</span></span> 
2. <span data-ttu-id="30915-131">Select **Secrets**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="30915-131">Select **Secrets**, and click **Add**.</span></span> 
3. <span data-ttu-id="30915-132">Select **Manual**, from **Upload options**.</span><span class="sxs-lookup"><span data-stu-id="30915-132">Select **Manual**, from **Upload options**.</span></span> 
4. <span data-ttu-id="30915-133">Enter a name and value for the secret.</span><span class="sxs-lookup"><span data-stu-id="30915-133">Enter a name and value for the secret.</span></span>  <span data-ttu-id="30915-134">The value can be anything you want.</span><span class="sxs-lookup"><span data-stu-id="30915-134">The value can be anything you want.</span></span> 
5. <span data-ttu-id="30915-135">Leave the activation date and expiration date clear, and leave **Enabled** as **Yes**.</span><span class="sxs-lookup"><span data-stu-id="30915-135">Leave the activation date and expiration date clear, and leave **Enabled** as **Yes**.</span></span> 
6. <span data-ttu-id="30915-136">Click **Create** to create the secret.</span><span class="sxs-lookup"><span data-stu-id="30915-136">Click **Create** to create the secret.</span></span> 
 
## <a name="get-an-access-token-using-the-vms-identity-and-use-it-to-retrieve-the-secret-from-the-key-vault"></a><span data-ttu-id="30915-137">Get an access token using the VM's identity and use it to retrieve the secret from the Key Vault</span><span class="sxs-lookup"><span data-stu-id="30915-137">Get an access token using the VM's identity and use it to retrieve the secret from the Key Vault</span></span>  

<span data-ttu-id="30915-138">To complete these steps, you need an SSH client.</span><span class="sxs-lookup"><span data-stu-id="30915-138">To complete these steps, you need an SSH client.</span></span>  <span data-ttu-id="30915-139">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="30915-139">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="30915-140">If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](../../virtual-machines/linux/ssh-from-windows.md), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](../../virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="30915-140">If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](../../virtual-machines/linux/ssh-from-windows.md), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](../../virtual-machines/linux/mac-create-ssh-keys.md).</span></span>
 
1. <span data-ttu-id="30915-141">In the portal, navigate to your Linux VM and in the **Overview**, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="30915-141">In the portal, navigate to your Linux VM and in the **Overview**, click **Connect**.</span></span> 
2. <span data-ttu-id="30915-142">**Connect** to the VM with the SSH client of your choice.</span><span class="sxs-lookup"><span data-stu-id="30915-142">**Connect** to the VM with the SSH client of your choice.</span></span> 
3. <span data-ttu-id="30915-143">In the terminal window, using CURL, make a request to the local managed identities for Azure resources endpoint to get an access token for Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="30915-143">In the terminal window, using CURL, make a request to the local managed identities for Azure resources endpoint to get an access token for Azure Key Vault.</span></span>  
 
    <span data-ttu-id="30915-144">The CURL request for the access token is below.</span><span class="sxs-lookup"><span data-stu-id="30915-144">The CURL request for the access token is below.</span></span>  
    
    ```bash
    curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fvault.azure.net' -H Metadata:true  
    ```
    <span data-ttu-id="30915-145">The response includes the access token you need to access Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="30915-145">The response includes the access token you need to access Resource Manager.</span></span> 
    
    <span data-ttu-id="30915-146">Response:</span><span class="sxs-lookup"><span data-stu-id="30915-146">Response:</span></span>  
    
    ```bash
    {"access_token":"eyJ0eXAi...",
    "refresh_token":"",
    "expires_in":"3599",
    "expires_on":"1504130527",
    "not_before":"1504126627",
    "resource":"https://vault.azure.net",
    "token_type":"Bearer"} 
    ```
    
    <span data-ttu-id="30915-147">You can use this access token to authenticate to Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="30915-147">You can use this access token to authenticate to Azure Key Vault.</span></span>  <span data-ttu-id="30915-148">The next CURL request shows how to read a secret from Key Vault using CURL and the Key Vault REST API.</span><span class="sxs-lookup"><span data-stu-id="30915-148">The next CURL request shows how to read a secret from Key Vault using CURL and the Key Vault REST API.</span></span>  <span data-ttu-id="30915-149">You’ll need the URL of your Key Vault, which is in the **Essentials** section of the **Overview** page of the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="30915-149">You’ll need the URL of your Key Vault, which is in the **Essentials** section of the **Overview** page of the Key Vault.</span></span>  <span data-ttu-id="30915-150">You will also need the access token you obtained on the previous call.</span><span class="sxs-lookup"><span data-stu-id="30915-150">You will also need the access token you obtained on the previous call.</span></span> 
        
    ```bash
    curl https://<YOUR-KEY-VAULT-URL>/secrets/<secret-name>?api-version=2016-10-01 -H "Authorization: Bearer <ACCESS TOKEN>" 
    ```
    
    <span data-ttu-id="30915-151">The response will look like this:</span><span class="sxs-lookup"><span data-stu-id="30915-151">The response will look like this:</span></span> 
    
    ```bash
    {"value":"p@ssw0rd!","id":"https://mytestkeyvault.vault.azure.net/secrets/MyTestSecret/7c2204c6093c4d859bc5b9eff8f29050","attributes":{"enabled":true,"created":1505088747,"updated":1505088747,"recoveryLevel":"Purgeable"}} 
    ```
    
<span data-ttu-id="30915-152">Once you’ve retrieved the secret from the Key Vault, you can use it to authenticate to a service that requires a name and password.</span><span class="sxs-lookup"><span data-stu-id="30915-152">Once you’ve retrieved the secret from the Key Vault, you can use it to authenticate to a service that requires a name and password.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30915-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="30915-153">Next steps</span></span>

<span data-ttu-id="30915-154">In this tutorial, you learned how to use a Linux VM system-assigned managed identity to access Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="30915-154">In this tutorial, you learned how to use a Linux VM system-assigned managed identity to access Azure Key Vault.</span></span>  <span data-ttu-id="30915-155">To learn more about Azure Key Vault see:</span><span class="sxs-lookup"><span data-stu-id="30915-155">To learn more about Azure Key Vault see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="30915-156">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="30915-156">Azure Key Vault</span></span>](/azure/key-vault/key-vault-whatis)




