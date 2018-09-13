---
title: Azure Quickstart - Set and retrieve a secret from Key Vault using Azure portal | Microsoft Docs
description: Quickstart showing how to set and retrieve a secret from Azure Key Vault using the Azure portal
services: key-vault
author: barclayn
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 98cf8387-34de-468e-ac8f-5c02c9e83e68
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.custom: mvc
ms.date: 05/10/2018
ms.author: barclayn
ms.openlocfilehash: 864c80fe0ab8b061439b5a80a111edbd1b2004b6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870699"
---
# <a name="quickstart-set-and-retrieve-a-secret-from-azure-key-vault-using-the-azure-portal"></a><span data-ttu-id="9610c-103">Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9610c-103">Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal</span></span>

<span data-ttu-id="9610c-104">Azure Key Vault is a cloud service that provides a secure store for secrets.</span><span class="sxs-lookup"><span data-stu-id="9610c-104">Azure Key Vault is a cloud service that provides a secure store for secrets.</span></span> <span data-ttu-id="9610c-105">You can securely store keys, passwords, certificates, and other secrets.</span><span class="sxs-lookup"><span data-stu-id="9610c-105">You can securely store keys, passwords, certificates, and other secrets.</span></span> <span data-ttu-id="9610c-106">Azure key vaults may be created and managed through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9610c-106">Azure key vaults may be created and managed through the Azure portal.</span></span> <span data-ttu-id="9610c-107">In this quickstart, you create a key vault, then use it to store a secret.</span><span class="sxs-lookup"><span data-stu-id="9610c-107">In this quickstart, you create a key vault, then use it to store a secret.</span></span> <span data-ttu-id="9610c-108">For more information on Key Vault, review the [Overview](key-vault-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9610c-108">For more information on Key Vault, review the [Overview](key-vault-overview.md).</span></span>

<span data-ttu-id="9610c-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="9610c-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="9610c-110">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="9610c-110">Sign in to Azure</span></span>

<span data-ttu-id="9610c-111">Sign in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="9610c-111">Sign in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-vault"></a><span data-ttu-id="9610c-112">Create a vault</span><span class="sxs-lookup"><span data-stu-id="9610c-112">Create a vault</span></span>

1. <span data-ttu-id="9610c-113">Select the **Create a resource** option on the upper left-hand corner of the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9610c-113">Select the **Create a resource** option on the upper left-hand corner of the Azure portal</span></span>

    ![Output after Key Vault creation completes](./media/quick-create-portal/search-services.png)
2. <span data-ttu-id="9610c-115">In the Search box, enter **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="9610c-115">In the Search box, enter **Key Vault**.</span></span>
3. <span data-ttu-id="9610c-116">From the results list, choose **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="9610c-116">From the results list, choose **Key Vault**.</span></span>
4. <span data-ttu-id="9610c-117">On the Key Vault section, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="9610c-117">On the Key Vault section, choose **Create**.</span></span>
5. <span data-ttu-id="9610c-118">On the **Create key vault** section provide the following information:</span><span class="sxs-lookup"><span data-stu-id="9610c-118">On the **Create key vault** section provide the following information:</span></span>
    - <span data-ttu-id="9610c-119">**Name**: A unique name is required.</span><span class="sxs-lookup"><span data-stu-id="9610c-119">**Name**: A unique name is required.</span></span> <span data-ttu-id="9610c-120">For this quickstart we use **Contoso-vault2**.</span><span class="sxs-lookup"><span data-stu-id="9610c-120">For this quickstart we use **Contoso-vault2**.</span></span> 
    - <span data-ttu-id="9610c-121">**Subscription**: Choose a subscription.</span><span class="sxs-lookup"><span data-stu-id="9610c-121">**Subscription**: Choose a subscription.</span></span>
    - <span data-ttu-id="9610c-122">Under **Resource Group** choose **Create new** and enter a resource group name.</span><span class="sxs-lookup"><span data-stu-id="9610c-122">Under **Resource Group** choose **Create new** and enter a resource group name.</span></span>
    - <span data-ttu-id="9610c-123">In the **Location** pull-down menu, choose a location.</span><span class="sxs-lookup"><span data-stu-id="9610c-123">In the **Location** pull-down menu, choose a location.</span></span>
    - <span data-ttu-id="9610c-124">Check the **Pin to dashboard** checkbox.</span><span class="sxs-lookup"><span data-stu-id="9610c-124">Check the **Pin to dashboard** checkbox.</span></span>
    - <span data-ttu-id="9610c-125">Leave the other options to their defaults.</span><span class="sxs-lookup"><span data-stu-id="9610c-125">Leave the other options to their defaults.</span></span>
6. <span data-ttu-id="9610c-126">After providing the information above, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="9610c-126">After providing the information above, select **Create**.</span></span>

<span data-ttu-id="9610c-127">Take note of the two properties listed below:</span><span class="sxs-lookup"><span data-stu-id="9610c-127">Take note of the two properties listed below:</span></span>

* <span data-ttu-id="9610c-128">**Vault Name**: In the example, this is **Contoso-Vault2**.</span><span class="sxs-lookup"><span data-stu-id="9610c-128">**Vault Name**: In the example, this is **Contoso-Vault2**.</span></span> <span data-ttu-id="9610c-129">You will use this name for other steps.</span><span class="sxs-lookup"><span data-stu-id="9610c-129">You will use this name for other steps.</span></span>
* <span data-ttu-id="9610c-130">**Vault URI**: In the example, this is https://contoso-vault2.vault.azure.net/.</span><span class="sxs-lookup"><span data-stu-id="9610c-130">**Vault URI**: In the example, this is https://contoso-vault2.vault.azure.net/.</span></span> <span data-ttu-id="9610c-131">Applications that use your vault through its REST API must use this URI.</span><span class="sxs-lookup"><span data-stu-id="9610c-131">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="9610c-132">At this point, your Azure account is the only one authorized to perform operations on this new vault.</span><span class="sxs-lookup"><span data-stu-id="9610c-132">At this point, your Azure account is the only one authorized to perform operations on this new vault.</span></span>

![Output after Key Vault creation completes](./media/quick-create-portal/vault-properties.png)

## <a name="add-a-secret-to-key-vault"></a><span data-ttu-id="9610c-134">Add a secret to Key Vault</span><span class="sxs-lookup"><span data-stu-id="9610c-134">Add a secret to Key Vault</span></span>

<span data-ttu-id="9610c-135">To add a secret to the vault, you just need to take a couple of additional steps.</span><span class="sxs-lookup"><span data-stu-id="9610c-135">To add a secret to the vault, you just need to take a couple of additional steps.</span></span> <span data-ttu-id="9610c-136">In this case, we add a password that could be used by an application.</span><span class="sxs-lookup"><span data-stu-id="9610c-136">In this case, we add a password that could be used by an application.</span></span> <span data-ttu-id="9610c-137">The password is called **ExamplePassword** and we store the value of **Pa$$w0rd** in it.</span><span class="sxs-lookup"><span data-stu-id="9610c-137">The password is called **ExamplePassword** and we store the value of **Pa$$w0rd** in it.</span></span>

1. <span data-ttu-id="9610c-138">On the Key Vault properties pages select **Secrets**.</span><span class="sxs-lookup"><span data-stu-id="9610c-138">On the Key Vault properties pages select **Secrets**.</span></span>
2. <span data-ttu-id="9610c-139">Click on **Generate/Import**.</span><span class="sxs-lookup"><span data-stu-id="9610c-139">Click on **Generate/Import**.</span></span>
3. <span data-ttu-id="9610c-140">On the **Create a secret** screen choose the following values:</span><span class="sxs-lookup"><span data-stu-id="9610c-140">On the **Create a secret** screen choose the following values:</span></span>
    - <span data-ttu-id="9610c-141">**Upload options**: Manual.</span><span class="sxs-lookup"><span data-stu-id="9610c-141">**Upload options**: Manual.</span></span>
    - <span data-ttu-id="9610c-142">**Name**: ExamplePassword.</span><span class="sxs-lookup"><span data-stu-id="9610c-142">**Name**: ExamplePassword.</span></span>
    - <span data-ttu-id="9610c-143">**Value**: Pa$$w0rd.</span><span class="sxs-lookup"><span data-stu-id="9610c-143">**Value**: Pa$$w0rd.</span></span>
    - <span data-ttu-id="9610c-144">Leave the other values to their defaults.</span><span class="sxs-lookup"><span data-stu-id="9610c-144">Leave the other values to their defaults.</span></span> <span data-ttu-id="9610c-145">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9610c-145">Click **Create**.</span></span>

<span data-ttu-id="9610c-146">Once that you receive the message that the secret has been successfully created, you may click on it on the list.</span><span class="sxs-lookup"><span data-stu-id="9610c-146">Once that you receive the message that the secret has been successfully created, you may click on it on the list.</span></span> <span data-ttu-id="9610c-147">You can then see some of the properties.</span><span class="sxs-lookup"><span data-stu-id="9610c-147">You can then see some of the properties.</span></span> <span data-ttu-id="9610c-148">If you click on the current version, you can see the value you specified in the previous step.</span><span class="sxs-lookup"><span data-stu-id="9610c-148">If you click on the current version, you can see the value you specified in the previous step.</span></span>

![Secret properties](./media/quick-create-portal/version.png)

## <a name="clean-up-resources"></a><span data-ttu-id="9610c-150">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="9610c-150">Clean up resources</span></span>

<span data-ttu-id="9610c-151">Other Key Vault quickstarts and tutorials build upon this quickstart.</span><span class="sxs-lookup"><span data-stu-id="9610c-151">Other Key Vault quickstarts and tutorials build upon this quickstart.</span></span> <span data-ttu-id="9610c-152">If you plan to continue on to work with subsequent quickstarts and tutorials, you may wish to leave these resources in place.</span><span class="sxs-lookup"><span data-stu-id="9610c-152">If you plan to continue on to work with subsequent quickstarts and tutorials, you may wish to leave these resources in place.</span></span>
<span data-ttu-id="9610c-153">When no longer needed, delete the resource group, which deletes the Key Vault and related resources.</span><span class="sxs-lookup"><span data-stu-id="9610c-153">When no longer needed, delete the resource group, which deletes the Key Vault and related resources.</span></span> <span data-ttu-id="9610c-154">To delete the resource group through the portal:</span><span class="sxs-lookup"><span data-stu-id="9610c-154">To delete the resource group through the portal:</span></span>

1. <span data-ttu-id="9610c-155">Enter the name of your resource group in the Search box at the top of the portal.</span><span class="sxs-lookup"><span data-stu-id="9610c-155">Enter the name of your resource group in the Search box at the top of the portal.</span></span> <span data-ttu-id="9610c-156">When you see the resource group used in this quickstart in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="9610c-156">When you see the resource group used in this quickstart in the search results, select it.</span></span>
2. <span data-ttu-id="9610c-157">Select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="9610c-157">Select **Delete resource group**.</span></span>
3. <span data-ttu-id="9610c-158">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="9610c-158">In the **TYPE THE RESOURCE GROUP NAME:** box type in the name of the resource group and select **Delete**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9610c-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="9610c-159">Next steps</span></span>

<span data-ttu-id="9610c-160">In this quickstart, you have created a Key Vault and stored a secret.</span><span class="sxs-lookup"><span data-stu-id="9610c-160">In this quickstart, you have created a Key Vault and stored a secret.</span></span> <span data-ttu-id="9610c-161">To learn more about Key Vault and how you can use it with your applications, continue to the tutorial for web applications working with Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9610c-161">To learn more about Key Vault and how you can use it with your applications, continue to the tutorial for web applications working with Key Vault.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="9610c-162">To learn how to read a secret from Key Vault from a web application using managed identities for Azure resources, continue with the following tutorial [Configure an Azure web application to read a secret from Key vault](quick-create-net.md).</span><span class="sxs-lookup"><span data-stu-id="9610c-162">To learn how to read a secret from Key Vault from a web application using managed identities for Azure resources, continue with the following tutorial [Configure an Azure web application to read a secret from Key vault](quick-create-net.md).</span></span>
