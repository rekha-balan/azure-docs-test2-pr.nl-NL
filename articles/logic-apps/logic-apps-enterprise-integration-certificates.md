---
title: Using certificates with Enterprise Integration Pack | Microsoft Docs
description: Learn how to use certificates with the Enterprise Integration Pack | Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: padmavc
ms.openlocfilehash: 9a53d5472cd4e75f4a1eeceb88062331e28ed1b5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550327"
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="0af0a-103">Learn about certificates and Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="0af0a-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="0af0a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="0af0a-104">Overview</span></span>
<span data-ttu-id="0af0a-105">Enterprise integration uses certificates to secure B2B communications.</span><span class="sxs-lookup"><span data-stu-id="0af0a-105">Enterprise integration uses certificates to secure B2B communications.</span></span> <span data-ttu-id="0af0a-106">You can use two types of certificates in your enterprise integration apps:</span><span class="sxs-lookup"><span data-stu-id="0af0a-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="0af0a-107">Public certificates, which must be purchased from a certification authority (CA).</span><span class="sxs-lookup"><span data-stu-id="0af0a-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="0af0a-108">Private certificates, which you can issue yourself.</span><span class="sxs-lookup"><span data-stu-id="0af0a-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="0af0a-109">These certificates are sometimes referred to as self-signed certificates.</span><span class="sxs-lookup"><span data-stu-id="0af0a-109">These certificates are sometimes referred to as self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="0af0a-110">What are certificates?</span><span class="sxs-lookup"><span data-stu-id="0af0a-110">What are certificates?</span></span>
<span data-ttu-id="0af0a-111">Certificates are digital documents that verify the identity of the participants in electronic communications and that also secure electronic communications.</span><span class="sxs-lookup"><span data-stu-id="0af0a-111">Certificates are digital documents that verify the identity of the participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="0af0a-112">Why use certificates?</span><span class="sxs-lookup"><span data-stu-id="0af0a-112">Why use certificates?</span></span>
<span data-ttu-id="0af0a-113">Sometimes B2B communications must be kept confidential.</span><span class="sxs-lookup"><span data-stu-id="0af0a-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="0af0a-114">Enterprise integration uses certificates to secure these communications in two ways:</span><span class="sxs-lookup"><span data-stu-id="0af0a-114">Enterprise integration uses certificates to secure these communications in two ways:</span></span>

* <span data-ttu-id="0af0a-115">By encrypting the contents of messages</span><span class="sxs-lookup"><span data-stu-id="0af0a-115">By encrypting the contents of messages</span></span>
* <span data-ttu-id="0af0a-116">By digitally signing messages</span><span class="sxs-lookup"><span data-stu-id="0af0a-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="0af0a-117">Upload a public certificate</span><span class="sxs-lookup"><span data-stu-id="0af0a-117">Upload a public certificate</span></span>

<span data-ttu-id="0af0a-118">To use a *public certificate* in your logic apps with B2B capabilities, you first need to upload the certificate into your integration account.</span><span class="sxs-lookup"><span data-stu-id="0af0a-118">To use a *public certificate* in your logic apps with B2B capabilities, you first need to upload the certificate into your integration account.</span></span>  

<span data-ttu-id="0af0a-119">After you upload a certificate, it's available to help you secure your B2B messages when you define their properties in the [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span><span class="sxs-lookup"><span data-stu-id="0af0a-119">After you upload a certificate, it's available to help you secure your B2B messages when you define their properties in the [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="0af0a-120">Here are the detailed steps for uploading your public certificates into your integration account after you sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="0af0a-120">Here are the detailed steps for uploading your public certificates into your integration account after you sign in to the Azure portal:</span></span>

1. <span data-ttu-id="0af0a-121">Select **More services** and enter **integration** in the filter search box.</span><span class="sxs-lookup"><span data-stu-id="0af0a-121">Select **More services** and enter **integration** in the filter search box.</span></span> <span data-ttu-id="0af0a-122">Select **Integration Accounts** from the results list</span><span class="sxs-lookup"><span data-stu-id="0af0a-122">Select **Integration Accounts** from the results list</span></span>     
<span data-ttu-id="0af0a-123">![Select Browse](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="0af0a-123">![Select Browse](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="0af0a-124">Select the integration account to which you want to add the certificate.</span><span class="sxs-lookup"><span data-stu-id="0af0a-124">Select the integration account to which you want to add the certificate.</span></span>  
![Select the integration account to which you want to add the certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="0af0a-126">Select the **Certificates** tile.</span><span class="sxs-lookup"><span data-stu-id="0af0a-126">Select the **Certificates** tile.</span></span>  
<span data-ttu-id="0af0a-127">![Select the Certificates tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="0af0a-127">![Select the Certificates tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="0af0a-128">In the **Certificates** blade that opens, select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0af0a-128">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="0af0a-129">![Select the Add button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="0af0a-129">![Select the Add button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="0af0a-130">Enter a **Name** for your certificate, and then select the certificate type as **public** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="0af0a-130">Enter a **Name** for your certificate, and then select the certificate type as **public** from the dropdown.</span></span>  
6. <span data-ttu-id="0af0a-131">Select the folder icon on the right side of the **Certificate** text box.</span><span class="sxs-lookup"><span data-stu-id="0af0a-131">Select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="0af0a-132">When the file picker opens, find and select the certificate file that you want to upload to your integration account.</span><span class="sxs-lookup"><span data-stu-id="0af0a-132">When the file picker opens, find and select the certificate file that you want to upload to your integration account.</span></span>
7. <span data-ttu-id="0af0a-133">Select the certificate, and then select **OK** in the file picker.</span><span class="sxs-lookup"><span data-stu-id="0af0a-133">Select the certificate, and then select **OK** in the file picker.</span></span> <span data-ttu-id="0af0a-134">This validates and uploads the certificate to your integration account.</span><span class="sxs-lookup"><span data-stu-id="0af0a-134">This validates and uploads the certificate to your integration account.</span></span>
8. <span data-ttu-id="0af0a-135">Finally, back on the **Add certificate** blade, select the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="0af0a-135">Finally, back on the **Add certificate** blade, select the **OK** button.</span></span>  
<span data-ttu-id="0af0a-136">![Select the OK button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="0af0a-136">![Select the OK button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="0af0a-137">Select the **Certificates** tile.</span><span class="sxs-lookup"><span data-stu-id="0af0a-137">Select the **Certificates** tile.</span></span> <span data-ttu-id="0af0a-138">You should see the newly added certificate.</span><span class="sxs-lookup"><span data-stu-id="0af0a-138">You should see the newly added certificate.</span></span>  
<span data-ttu-id="0af0a-139">![See the new certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="0af0a-139">![See the new certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="0af0a-140">Upload a private certificate</span><span class="sxs-lookup"><span data-stu-id="0af0a-140">Upload a private certificate</span></span>

<span data-ttu-id="0af0a-141">To use a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate to your integration account by taking the following steps</span><span class="sxs-lookup"><span data-stu-id="0af0a-141">To use a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate to your integration account by taking the following steps</span></span>

1. <span data-ttu-id="0af0a-142">[Upload your private key to Key Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span><span class="sxs-lookup"><span data-stu-id="0af0a-142">[Upload your private key to Key Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="0af0a-143">You must authorize Logic Apps to perform operations on Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0af0a-143">You must authorize Logic Apps to perform operations on Key Vault.</span></span> <span data-ttu-id="0af0a-144">You can grant access to the Logic Apps service principal by using the following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="0af0a-144">You can grant access to the Logic Apps service principal by using the following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="0af0a-145">After you've taken the previous step, add a private certificate to integration account.</span><span class="sxs-lookup"><span data-stu-id="0af0a-145">After you've taken the previous step, add a private certificate to integration account.</span></span>

<span data-ttu-id="0af0a-146">Following are the detailed steps for uploading your private certificates into your integration account after you sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="0af0a-146">Following are the detailed steps for uploading your private certificates into your integration account after you sign in to the Azure portal:</span></span>  
 
1. <span data-ttu-id="0af0a-147">Select the integration account to which you want to add the certificate and select the **Certificates** tile.</span><span class="sxs-lookup"><span data-stu-id="0af0a-147">Select the integration account to which you want to add the certificate and select the **Certificates** tile.</span></span>  
<span data-ttu-id="0af0a-148">![Select the Certificates tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="0af0a-148">![Select the Certificates tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="0af0a-149">In the **Certificates** blade that opens, select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0af0a-149">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="0af0a-150">![Select the Add button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="0af0a-150">![Select the Add button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="0af0a-151">Enter a **Name** for your certificate, and select the certificate type as **private** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="0af0a-151">Enter a **Name** for your certificate, and select the certificate type as **private** from the dropdown.</span></span>   
4. <span data-ttu-id="0af0a-152">select the folder icon on the right side of the **Certificate** text box.</span><span class="sxs-lookup"><span data-stu-id="0af0a-152">select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="0af0a-153">When the file picker opens, find the corresponding public certificate that you want to upload to your integration account.</span><span class="sxs-lookup"><span data-stu-id="0af0a-153">When the file picker opens, find the corresponding public certificate that you want to upload to your integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="0af0a-154">While adding a private certificate it is important to add corresponding public certificate to show in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting the messages.</span><span class="sxs-lookup"><span data-stu-id="0af0a-154">While adding a private certificate it is important to add corresponding public certificate to show in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting the messages.</span></span>
   > 
   >   

5. <span data-ttu-id="0af0a-155">Select the **Resource Group**, **Key Vault**, **Key Name** and select the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="0af0a-155">Select the **Resource Group**, **Key Vault**, **Key Name** and select the **OK** button.</span></span>  
<span data-ttu-id="0af0a-156">![Add certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="0af0a-156">![Add certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="0af0a-157">Select the **Certificates** tile.</span><span class="sxs-lookup"><span data-stu-id="0af0a-157">Select the **Certificates** tile.</span></span> <span data-ttu-id="0af0a-158">You should see the newly added certificate.</span><span class="sxs-lookup"><span data-stu-id="0af0a-158">You should see the newly added certificate.</span></span>
<span data-ttu-id="0af0a-159">![See the new certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="0af0a-159">![See the new certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="0af0a-160">Create a B2B agreement</span><span class="sxs-lookup"><span data-stu-id="0af0a-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="0af0a-161">Learn more about Key Vault</span><span class="sxs-lookup"><span data-stu-id="0af0a-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "Learn about Key Vault")  











