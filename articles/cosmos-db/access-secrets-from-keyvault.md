---
title: Use Key Vault to store and access Azure Cosmos DB keys | Microsoft Docs
description: Use Azure Key Vault to store and access Azure Cosmos DB connection string, keys, URI's.
services: cosmos-db
author: rafats
manager: kfile
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: conceptual
ms.date: 08/21/2018
ms.author: rafats
ms.openlocfilehash: b090c1593b49bec4f51fea8d498860e8af8b2f4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868707"
---
# <a name="use-key-vault-to-store-and-access-azure-cosmos-db-keys"></a><span data-ttu-id="28147-103">Use Key Vault to store and access Azure Cosmos DB keys</span><span class="sxs-lookup"><span data-stu-id="28147-103">Use Key Vault to store and access Azure Cosmos DB keys</span></span>

<span data-ttu-id="28147-104">When using Azure Cosmos DB for your applications, you can access the database, collections, documents by using the endpoint URI and the key within the app’s configuration file.</span><span class="sxs-lookup"><span data-stu-id="28147-104">When using Azure Cosmos DB for your applications, you can access the database, collections, documents by using the endpoint URI and the key within the app’s configuration file.</span></span>  <span data-ttu-id="28147-105">However, it’s not safe to put keys and URL directly in the application code because they are available in clear text format to all the users.</span><span class="sxs-lookup"><span data-stu-id="28147-105">However, it’s not safe to put keys and URL directly in the application code because they are available in clear text format to all the users.</span></span> <span data-ttu-id="28147-106">You want to make sure that the URI and keys are available but through a secured mechanism.</span><span class="sxs-lookup"><span data-stu-id="28147-106">You want to make sure that the URI and keys are available but through a secured mechanism.</span></span> <span data-ttu-id="28147-107">This is where Azure Key Vault can help you to securely store and manage application secrets.</span><span class="sxs-lookup"><span data-stu-id="28147-107">This is where Azure Key Vault can help you to securely store and manage application secrets.</span></span>

<span data-ttu-id="28147-108">The following steps are required to store and read Azure Cosmos DB access keys from Key Vault:</span><span class="sxs-lookup"><span data-stu-id="28147-108">The following steps are required to store and read Azure Cosmos DB access keys from Key Vault:</span></span>

* <span data-ttu-id="28147-109">Create a Key Vault</span><span class="sxs-lookup"><span data-stu-id="28147-109">Create a Key Vault</span></span>  
* <span data-ttu-id="28147-110">Add Azure Cosmos DB access keys to the Key Vault</span><span class="sxs-lookup"><span data-stu-id="28147-110">Add Azure Cosmos DB access keys to the Key Vault</span></span>  
* <span data-ttu-id="28147-111">Create an Azure web application</span><span class="sxs-lookup"><span data-stu-id="28147-111">Create an Azure web application</span></span>  
* <span data-ttu-id="28147-112">Register the application & grant permissions to read the Key Vault</span><span class="sxs-lookup"><span data-stu-id="28147-112">Register the application & grant permissions to read the Key Vault</span></span>  


## <a name="create-a-key-vault"></a><span data-ttu-id="28147-113">Create a Key Vault</span><span class="sxs-lookup"><span data-stu-id="28147-113">Create a Key Vault</span></span>

1. <span data-ttu-id="28147-114">Sign in to [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="28147-114">Sign in to [Azure Portal](https://portal.azure.com/).</span></span>  
2. <span data-ttu-id="28147-115">Select **Create a resource > Security > Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="28147-115">Select **Create a resource > Security > Key Vault**.</span></span>  
3. <span data-ttu-id="28147-116">On the **Create key vault** section provide the following information:</span><span class="sxs-lookup"><span data-stu-id="28147-116">On the **Create key vault** section provide the following information:</span></span>  
   * <span data-ttu-id="28147-117">**Name:** Provide a unique name for your Key Vault.</span><span class="sxs-lookup"><span data-stu-id="28147-117">**Name:** Provide a unique name for your Key Vault.</span></span>  
   * <span data-ttu-id="28147-118">**Subscription:** Choose the subscription that you will use.</span><span class="sxs-lookup"><span data-stu-id="28147-118">**Subscription:** Choose the subscription that you will use.</span></span>  
   * <span data-ttu-id="28147-119">Under **Resource Group** choose **Create new** and enter a resource group name.</span><span class="sxs-lookup"><span data-stu-id="28147-119">Under **Resource Group** choose **Create new** and enter a resource group name.</span></span>  
   * <span data-ttu-id="28147-120">In the Location pull-down menu, choose a location.</span><span class="sxs-lookup"><span data-stu-id="28147-120">In the Location pull-down menu, choose a location.</span></span>  
   * <span data-ttu-id="28147-121">Leave other options to their defaults.</span><span class="sxs-lookup"><span data-stu-id="28147-121">Leave other options to their defaults.</span></span>  
4. <span data-ttu-id="28147-122">After providing the information above, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="28147-122">After providing the information above, select **Create**.</span></span>  

## <a name="add-azure-cosmos-db-access-keys-to-the-key-vault"></a><span data-ttu-id="28147-123">Add Azure Cosmos DB access keys to the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="28147-123">Add Azure Cosmos DB access keys to the Key Vault.</span></span>
1. <span data-ttu-id="28147-124">Navigate to the Key Vault you created in the previous step, open the **Secrets** tab.</span><span class="sxs-lookup"><span data-stu-id="28147-124">Navigate to the Key Vault you created in the previous step, open the **Secrets** tab.</span></span>  
2. <span data-ttu-id="28147-125">Select **+Generate/Import**,</span><span class="sxs-lookup"><span data-stu-id="28147-125">Select **+Generate/Import**,</span></span> 

   * <span data-ttu-id="28147-126">Select **Manual** for **Upload options**.</span><span class="sxs-lookup"><span data-stu-id="28147-126">Select **Manual** for **Upload options**.</span></span>
   * <span data-ttu-id="28147-127">Provide a **Name** for your secret</span><span class="sxs-lookup"><span data-stu-id="28147-127">Provide a **Name** for your secret</span></span>
   * <span data-ttu-id="28147-128">Provide the connection string of your Cosmos DB account into the **Value** field.</span><span class="sxs-lookup"><span data-stu-id="28147-128">Provide the connection string of your Cosmos DB account into the **Value** field.</span></span> <span data-ttu-id="28147-129">And then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="28147-129">And then select **Create**.</span></span>

   ![Create a secret](./media/access-secrets-from-keyvault/create-a-secret.png)

4. <span data-ttu-id="28147-131">After the secret is created, open it and copy the \*\*Secret Identifier that is in the following format.</span><span class="sxs-lookup"><span data-stu-id="28147-131">After the secret is created, open it and copy the \*\*Secret Identifier that is in the following format.</span></span> <span data-ttu-id="28147-132">You will use this identifier in the next section.</span><span class="sxs-lookup"><span data-stu-id="28147-132">You will use this identifier in the next section.</span></span> 

   `https://<Key_Vault_Name>.vault.azure.net/secrets/<Secret _Name>/<ID>`

## <a name="create-an-azure-web-application"></a><span data-ttu-id="28147-133">Create an Azure web application</span><span class="sxs-lookup"><span data-stu-id="28147-133">Create an Azure web application</span></span>

1. <span data-ttu-id="28147-134">Create an Azure web application or you can download the app from the [GitHub repository](https://github.com/Azure/azure-cosmosdb-dotnet/tree/master/Demo/keyvaultdemo).</span><span class="sxs-lookup"><span data-stu-id="28147-134">Create an Azure web application or you can download the app from the [GitHub repository](https://github.com/Azure/azure-cosmosdb-dotnet/tree/master/Demo/keyvaultdemo).</span></span> <span data-ttu-id="28147-135">It is a simple MVC application.</span><span class="sxs-lookup"><span data-stu-id="28147-135">It is a simple MVC application.</span></span>  

2. <span data-ttu-id="28147-136">Unzip the downloaded application and open the **HomeController.cs** file.</span><span class="sxs-lookup"><span data-stu-id="28147-136">Unzip the downloaded application and open the **HomeController.cs** file.</span></span> <span data-ttu-id="28147-137">Update the secret ID in the following line:</span><span class="sxs-lookup"><span data-stu-id="28147-137">Update the secret ID in the following line:</span></span>

   `var secret = await keyVaultClient.GetSecretAsync("<Your Key Vault’s secret identifier>")`

3. <span data-ttu-id="28147-138">**Save** the file, **Build** the solution.</span><span class="sxs-lookup"><span data-stu-id="28147-138">**Save** the file, **Build** the solution.</span></span>  
4. <span data-ttu-id="28147-139">Next deploy the application to Azure.</span><span class="sxs-lookup"><span data-stu-id="28147-139">Next deploy the application to Azure.</span></span> <span data-ttu-id="28147-140">Right click on project and choose **publish**.</span><span class="sxs-lookup"><span data-stu-id="28147-140">Right click on project and choose **publish**.</span></span> <span data-ttu-id="28147-141">Create a new app service profile (you can name the app WebAppKeyVault1) and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="28147-141">Create a new app service profile (you can name the app WebAppKeyVault1) and select **Publish**.</span></span>   

5. <span data-ttu-id="28147-142">Once the application is deployed.</span><span class="sxs-lookup"><span data-stu-id="28147-142">Once the application is deployed.</span></span> <span data-ttu-id="28147-143">From the Azure portal, navigate to web app that you deployed, and turn on the **Managed service identity** of this application.</span><span class="sxs-lookup"><span data-stu-id="28147-143">From the Azure portal, navigate to web app that you deployed, and turn on the **Managed service identity** of this application.</span></span>  

   ![Managed service identity](./media/access-secrets-from-keyvault/turn-on-managed-service-identity.png)

<span data-ttu-id="28147-145">If you will run the application now, you will see the following error, as you have not given any permission to this application in Key Vault.</span><span class="sxs-lookup"><span data-stu-id="28147-145">If you will run the application now, you will see the following error, as you have not given any permission to this application in Key Vault.</span></span>

![App deployed without access](./media/access-secrets-from-keyvault/app-deployed-without-access.png)

## <a name="register-the-application--grant-permissions-to-read-the-key-vault"></a><span data-ttu-id="28147-147">Register the application & grant permissions to read the Key Vault</span><span class="sxs-lookup"><span data-stu-id="28147-147">Register the application & grant permissions to read the Key Vault</span></span>

<span data-ttu-id="28147-148">In this section, you register the application with Azure Active Directory and give permissions for the application to read the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="28147-148">In this section, you register the application with Azure Active Directory and give permissions for the application to read the Key Vault.</span></span> 

1. <span data-ttu-id="28147-149">Navigate to the Azure portal, open the **Key Vault** you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="28147-149">Navigate to the Azure portal, open the **Key Vault** you created in the previous section.</span></span>  

2. <span data-ttu-id="28147-150">Open **Access policies**, select **+Add New** find the web app you deployed, select permissions and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="28147-150">Open **Access policies**, select **+Add New** find the web app you deployed, select permissions and select **OK**.</span></span>  

   ![Add access policy](./media/access-secrets-from-keyvault/add-access-policy.png)

<span data-ttu-id="28147-152">Now, if you run the application, you can read the secret from Key Vault.</span><span class="sxs-lookup"><span data-stu-id="28147-152">Now, if you run the application, you can read the secret from Key Vault.</span></span>

![App deployed with secret](./media/access-secrets-from-keyvault/app-deployed-with-access.png)
 
<span data-ttu-id="28147-154">Similarly, you can add a user to access the key Vault.</span><span class="sxs-lookup"><span data-stu-id="28147-154">Similarly, you can add a user to access the key Vault.</span></span> <span data-ttu-id="28147-155">You need to add yourself to the Key Vault by selecting **Access Policies** and then grant all the permissions you need to run the application from Visual studio.</span><span class="sxs-lookup"><span data-stu-id="28147-155">You need to add yourself to the Key Vault by selecting **Access Policies** and then grant all the permissions you need to run the application from Visual studio.</span></span> <span data-ttu-id="28147-156">When this application is running from your desktop, it takes your identity.</span><span class="sxs-lookup"><span data-stu-id="28147-156">When this application is running from your desktop, it takes your identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28147-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="28147-157">Next steps</span></span>

* <span data-ttu-id="28147-158">To configure a firewall for Azure Cosmos DB see [firewall support](firewall-support.md) article.</span><span class="sxs-lookup"><span data-stu-id="28147-158">To configure a firewall for Azure Cosmos DB see [firewall support](firewall-support.md) article.</span></span>
* <span data-ttu-id="28147-159">To configure virtual network service endpoint, see [secure access by using VNet service endpoint](vnet-service-endpoint.md) article.</span><span class="sxs-lookup"><span data-stu-id="28147-159">To configure virtual network service endpoint, see [secure access by using VNet service endpoint](vnet-service-endpoint.md) article.</span></span>
