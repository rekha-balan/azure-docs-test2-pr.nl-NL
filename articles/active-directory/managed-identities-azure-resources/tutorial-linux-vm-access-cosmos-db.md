---
title: Use a Linux VM system-assigned managed identity to access Azure Cosmos DB
description: A tutorial that walks you through the process of using a Linux VM system-assigned managed identity to access Azure Cosmos DB.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/09/2018
ms.author: daveba
ms.openlocfilehash: 60d7e7fb2e2ced97b82dc01ef14d3c529434c5db
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866570"
---
# <a name="tutorial-use-a-linux-vm-system-assigned-managed-identity-to-access-azure-cosmos-db"></a><span data-ttu-id="2e6ed-103">Tutorial: Use a Linux VM system-assigned managed identity to access Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2e6ed-103">Tutorial: Use a Linux VM system-assigned managed identity to access Azure Cosmos DB</span></span> 

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]


<span data-ttu-id="2e6ed-104">This tutorial shows you how to to use a system-assigned managed identity for a Linux virtual machine (VM) to access Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-104">This tutorial shows you how to to use a system-assigned managed identity for a Linux virtual machine (VM) to access Azure Cosmos DB.</span></span> <span data-ttu-id="2e6ed-105">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="2e6ed-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2e6ed-106">Create a Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="2e6ed-106">Create a Cosmos DB account</span></span>
> * <span data-ttu-id="2e6ed-107">Create a collection in the Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="2e6ed-107">Create a collection in the Cosmos DB account</span></span>
> * <span data-ttu-id="2e6ed-108">Grant the system-assigned managed identity access to an Azure Cosmos DB instance</span><span class="sxs-lookup"><span data-stu-id="2e6ed-108">Grant the system-assigned managed identity access to an Azure Cosmos DB instance</span></span>
> * <span data-ttu-id="2e6ed-109">Retrieve the `principalID` of the of the Linux VM's system-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="2e6ed-109">Retrieve the `principalID` of the of the Linux VM's system-assigned managed identity</span></span>
> * <span data-ttu-id="2e6ed-110">Get an access token and use it to call Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e6ed-110">Get an access token and use it to call Azure Resource Manager</span></span>
> * <span data-ttu-id="2e6ed-111">Get access keys from Azure Resource Manager to make Cosmos DB calls</span><span class="sxs-lookup"><span data-stu-id="2e6ed-111">Get access keys from Azure Resource Manager to make Cosmos DB calls</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e6ed-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2e6ed-112">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="2e6ed-113">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="2e6ed-113">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="2e6ed-114">Create a Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="2e6ed-114">Create a Linux virtual machine</span></span>](/azure/virtual-machines/linux/quick-create-portal)

- [<span data-ttu-id="2e6ed-115">Enable system-assigned managed identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="2e6ed-115">Enable system-assigned managed identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

<span data-ttu-id="2e6ed-116">To run the CLI script examples in this tutorial, you have two options:</span><span class="sxs-lookup"><span data-stu-id="2e6ed-116">To run the CLI script examples in this tutorial, you have two options:</span></span>

- <span data-ttu-id="2e6ed-117">Use [Azure Cloud Shell](~/articles/cloud-shell/overview.md) either from the Azure portal, or via the **Try It** button, located in the top right corner of each code block.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-117">Use [Azure Cloud Shell](~/articles/cloud-shell/overview.md) either from the Azure portal, or via the **Try It** button, located in the top right corner of each code block.</span></span>
- <span data-ttu-id="2e6ed-118">[Install the latest version of CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0.23 or later) if you prefer to use a local CLI console.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-118">[Install the latest version of CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0.23 or later) if you prefer to use a local CLI console.</span></span>

## <a name="create-a-cosmos-db-account"></a><span data-ttu-id="2e6ed-119">Create a Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="2e6ed-119">Create a Cosmos DB account</span></span> 

<span data-ttu-id="2e6ed-120">If you don't already have one, create a Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-120">If you don't already have one, create a Cosmos DB account.</span></span> <span data-ttu-id="2e6ed-121">You can skip this step and use an existing Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-121">You can skip this step and use an existing Cosmos DB account.</span></span> 

1. <span data-ttu-id="2e6ed-122">Click the **+/Create new service** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-122">Click the **+/Create new service** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="2e6ed-123">Click **Databases**, then **Azure Cosmos DB**, and a new "New account" panel  displays.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-123">Click **Databases**, then **Azure Cosmos DB**, and a new "New account" panel  displays.</span></span>
3. <span data-ttu-id="2e6ed-124">Enter an **ID** for the Cosmos DB account, which you use later.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-124">Enter an **ID** for the Cosmos DB account, which you use later.</span></span>  
4. <span data-ttu-id="2e6ed-125">**API** should be set to "SQL."</span><span class="sxs-lookup"><span data-stu-id="2e6ed-125">**API** should be set to "SQL."</span></span> <span data-ttu-id="2e6ed-126">The approach described in this tutorial can be used with the other available API types, but the steps in this tutorial are for the SQL API.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-126">The approach described in this tutorial can be used with the other available API types, but the steps in this tutorial are for the SQL API.</span></span>
5. <span data-ttu-id="2e6ed-127">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-127">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span></span>  <span data-ttu-id="2e6ed-128">Select a **Location** where Cosmos DB is available.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-128">Select a **Location** where Cosmos DB is available.</span></span>
6. <span data-ttu-id="2e6ed-129">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-129">Click **Create**.</span></span>

## <a name="create-a-collection-in-the-cosmos-db-account"></a><span data-ttu-id="2e6ed-130">Create a collection in the Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="2e6ed-130">Create a collection in the Cosmos DB account</span></span>

<span data-ttu-id="2e6ed-131">Next, add a data collection in the Cosmos DB account that you can query in later steps.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-131">Next, add a data collection in the Cosmos DB account that you can query in later steps.</span></span>

1. <span data-ttu-id="2e6ed-132">Navigate to your newly created Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-132">Navigate to your newly created Cosmos DB account.</span></span>
2. <span data-ttu-id="2e6ed-133">On the **Overview** tab click the **+/Add Collection** button, and an "Add Collection" panel slides out.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-133">On the **Overview** tab click the **+/Add Collection** button, and an "Add Collection" panel slides out.</span></span>
3. <span data-ttu-id="2e6ed-134">Give the collection a database ID, collection ID, select a storage capacity, enter a partition key, enter a throughput value, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-134">Give the collection a database ID, collection ID, select a storage capacity, enter a partition key, enter a throughput value, then click **OK**.</span></span>  <span data-ttu-id="2e6ed-135">For this tutorial, it is sufficient to use "Test" as the database ID and collection ID, select a fixed storage capacity and lowest throughput (400 RU/s).</span><span class="sxs-lookup"><span data-stu-id="2e6ed-135">For this tutorial, it is sufficient to use "Test" as the database ID and collection ID, select a fixed storage capacity and lowest throughput (400 RU/s).</span></span>  

## <a name="retrieve-the-principalid-of-the-linux-vms-system-assigned-managed-identity"></a><span data-ttu-id="2e6ed-136">Retrieve the `principalID` of the Linux VM's system-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="2e6ed-136">Retrieve the `principalID` of the Linux VM's system-assigned managed identity</span></span>

<span data-ttu-id="2e6ed-137">To gain access to the Cosmos DB account access keys from the Resource Manager in the following section, you need to retrieve the `principalID` of the Linux VM's system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-137">To gain access to the Cosmos DB account access keys from the Resource Manager in the following section, you need to retrieve the `principalID` of the Linux VM's system-assigned managed identity.</span></span>  <span data-ttu-id="2e6ed-138">Be sure to replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>` (resource group in which you VM resides), and `<VM NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-138">Be sure to replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>` (resource group in which you VM resides), and `<VM NAME>` parameter values with your own values.</span></span>

```azurecli-interactive
az resource show --id /subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachines/<VM NAMe> --api-version 2017-12-01
```
<span data-ttu-id="2e6ed-139">The response includes the details of the system-assigned managed identity (note the principalID as it is used in the next section):</span><span class="sxs-lookup"><span data-stu-id="2e6ed-139">The response includes the details of the system-assigned managed identity (note the principalID as it is used in the next section):</span></span>

```bash  
{
    "id": "/subscriptions/<SUBSCRIPTION ID>/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachines/<VM NAMe>",
  "identity": {
    "principalId": "6891c322-314a-4e85-b129-52cf2daf47bd",
    "tenantId": "733a8f0e-ec41-4e69-8ad8-971fc4b533f8",
    "type": "SystemAssigned"
 }

```
## <a name="grant-your-linux-vms-system-assigned-identity-access-to-the-cosmos-db-account-access-keys"></a><span data-ttu-id="2e6ed-140">Grant your Linux VM's system-assigned identity access to the Cosmos DB account access keys</span><span class="sxs-lookup"><span data-stu-id="2e6ed-140">Grant your Linux VM's system-assigned identity access to the Cosmos DB account access keys</span></span>

<span data-ttu-id="2e6ed-141">Cosmos DB does not natively support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-141">Cosmos DB does not natively support Azure AD authentication.</span></span> <span data-ttu-id="2e6ed-142">However, you can use a managed identity to retrieve a Cosmos DB access key from the Resource Manager, then use the key to access Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-142">However, you can use a managed identity to retrieve a Cosmos DB access key from the Resource Manager, then use the key to access Cosmos DB.</span></span> <span data-ttu-id="2e6ed-143">In this step, you grant your system-assigned managed identity access to the keys to the Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-143">In this step, you grant your system-assigned managed identity access to the keys to the Cosmos DB account.</span></span>

<span data-ttu-id="2e6ed-144">To grant the system-assigned managed identity access to the Cosmos DB account in Azure Resource Manager using the Azure CLI, update the values for `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<COSMOS DB ACCOUNT NAME>` for your environment.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-144">To grant the system-assigned managed identity access to the Cosmos DB account in Azure Resource Manager using the Azure CLI, update the values for `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<COSMOS DB ACCOUNT NAME>` for your environment.</span></span> <span data-ttu-id="2e6ed-145">Replace `<MI PRINCIPALID>` with the `principalId` property returned by the `az resource show` command in [Retrieve the principalID of the Linux VM's MI](#retrieve-the-principalID-of-the-linux-VM's-system-assigned-identity).</span><span class="sxs-lookup"><span data-stu-id="2e6ed-145">Replace `<MI PRINCIPALID>` with the `principalId` property returned by the `az resource show` command in [Retrieve the principalID of the Linux VM's MI](#retrieve-the-principalID-of-the-linux-VM's-system-assigned-identity).</span></span>  <span data-ttu-id="2e6ed-146">Cosmos DB supports two levels of granularity when using access keys:  read/write access to the account, and read-only access to the account.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-146">Cosmos DB supports two levels of granularity when using access keys:  read/write access to the account, and read-only access to the account.</span></span>  <span data-ttu-id="2e6ed-147">Assign the `DocumentDB Account Contributor` role if you want to get read/write keys for the account, or assign the `Cosmos DB Account Reader Role` role if you want to get read-only keys for the account:</span><span class="sxs-lookup"><span data-stu-id="2e6ed-147">Assign the `DocumentDB Account Contributor` role if you want to get read/write keys for the account, or assign the `Cosmos DB Account Reader Role` role if you want to get read-only keys for the account:</span></span>

```azurecli-interactive
az role assignment create --assignee <MI PRINCIPALID> --role '<ROLE NAME>' --scope "/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.DocumentDB/databaseAccounts/<COSMODS DB ACCOUNT NAME>"
```

<span data-ttu-id="2e6ed-148">The response includes the details for the role assignment created:</span><span class="sxs-lookup"><span data-stu-id="2e6ed-148">The response includes the details for the role assignment created:</span></span>

```
{
  "id": "/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.DocumentDB/databaseAccounts/<COSMOS DB ACCOUNT>/providers/Microsoft.Authorization/roleAssignments/5b44e628-394e-4e7b-bbc3-d6cd4f28f15b",
  "name": "5b44e628-394e-4e7b-bbc3-d6cd4f28f15b",
  "properties": {
    "principalId": "c0833082-6cc3-4a26-a1b1-c4b5f90a981f",
    "roleDefinitionId": "/subscriptions/<SUBSCRIPTION ID>/providers/Microsoft.Authorization/roleDefinitions/fbdf93bf-df7d-467e-a4d2-9458aa1360c8",
    "scope": "/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.DocumentDB/databaseAccounts/<COSMOS DB ACCOUNT>"
  },
  "resourceGroup": "<RESOURCE GROUP>",
  "type": "Microsoft.Authorization/roleAssignments"
}
```

## <a name="get-an-access-token-using-the-linux-vms-system-assigned-managed-identity-and-use-it-to-call-azure-resource-manager"></a><span data-ttu-id="2e6ed-149">Get an access token using the Linux VM's system-assigned managed identity and use it to call Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e6ed-149">Get an access token using the Linux VM's system-assigned managed identity and use it to call Azure Resource Manager</span></span>

<span data-ttu-id="2e6ed-150">For the remainder of the tutorial, work from the VM created earlier.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-150">For the remainder of the tutorial, work from the VM created earlier.</span></span>

<span data-ttu-id="2e6ed-151">To complete these steps, you need an SSH client.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-151">To complete these steps, you need an SSH client.</span></span> <span data-ttu-id="2e6ed-152">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="2e6ed-152">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/install_guide).</span></span> <span data-ttu-id="2e6ed-153">If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](../../virtual-machines/linux/ssh-from-windows.md), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](../../virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="2e6ed-153">If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](../../virtual-machines/linux/ssh-from-windows.md), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](../../virtual-machines/linux/mac-create-ssh-keys.md).</span></span>

1. <span data-ttu-id="2e6ed-154">In the Azure portal, navigate to **Virtual Machines**, go to your Linux virtual machine, then from the **Overview** page click **Connect** at the top.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-154">In the Azure portal, navigate to **Virtual Machines**, go to your Linux virtual machine, then from the **Overview** page click **Connect** at the top.</span></span> <span data-ttu-id="2e6ed-155">Copy the string to connect to your VM.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-155">Copy the string to connect to your VM.</span></span> 
2. <span data-ttu-id="2e6ed-156">Connect to your VM using your SSH client.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-156">Connect to your VM using your SSH client.</span></span>  
3. <span data-ttu-id="2e6ed-157">Next, you are prompted to enter in your **Password** you added when creating the **Linux VM**.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-157">Next, you are prompted to enter in your **Password** you added when creating the **Linux VM**.</span></span> <span data-ttu-id="2e6ed-158">You should then be successfully signed in.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-158">You should then be successfully signed in.</span></span>  
4. <span data-ttu-id="2e6ed-159">Use CURL to get an access token for Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="2e6ed-159">Use CURL to get an access token for Azure Resource Manager:</span></span> 
     
    ```bash
    curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -H Metadata:true   
    ```
 
    > [!NOTE]
    > <span data-ttu-id="2e6ed-160">In the previous request, the value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-160">In the previous request, the value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span></span> <span data-ttu-id="2e6ed-161">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-161">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span></span>
    > <span data-ttu-id="2e6ed-162">In the following response, the access_token element as been shortened for brevity.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-162">In the following response, the access_token element as been shortened for brevity.</span></span>
    
    ```bash
    {"access_token":"eyJ0eXAiOi...",
     "expires_in":"3599",
     "expires_on":"1518503375",
     "not_before":"1518499475",
     "resource":"https://management.azure.com/",
     "token_type":"Bearer",
     "client_id":"1ef89848-e14b-465f-8780-bf541d325cd5"}
     ```
    
## <a name="get-access-keys-from-azure-resource-manager-to-make-cosmos-db-calls"></a><span data-ttu-id="2e6ed-163">Get access keys from Azure Resource Manager to make Cosmos DB calls</span><span class="sxs-lookup"><span data-stu-id="2e6ed-163">Get access keys from Azure Resource Manager to make Cosmos DB calls</span></span>  

<span data-ttu-id="2e6ed-164">Now use CURL to call Resource Manager using the access token retrieved in the previous section to retrieve the Cosmos DB account access key.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-164">Now use CURL to call Resource Manager using the access token retrieved in the previous section to retrieve the Cosmos DB account access key.</span></span> <span data-ttu-id="2e6ed-165">Once we have the access key, we can query Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-165">Once we have the access key, we can query Cosmos DB.</span></span> <span data-ttu-id="2e6ed-166">Be sure to replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<COSMOS DB ACCOUNT NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-166">Be sure to replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<COSMOS DB ACCOUNT NAME>` parameter values with your own values.</span></span> <span data-ttu-id="2e6ed-167">Replace the `<ACCESS TOKEN>` value with the access token you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-167">Replace the `<ACCESS TOKEN>` value with the access token you retrieved earlier.</span></span>  <span data-ttu-id="2e6ed-168">If you want to retrieve read/write keys, use key operation type `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-168">If you want to retrieve read/write keys, use key operation type `listKeys`.</span></span>  <span data-ttu-id="2e6ed-169">If you want to retrieve read-only keys, use the key operation type `readonlykeys`:</span><span class="sxs-lookup"><span data-stu-id="2e6ed-169">If you want to retrieve read-only keys, use the key operation type `readonlykeys`:</span></span>

```bash 
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.DocumentDB/databaseAccounts/<COSMOS DB ACCOUNT NAME>/<KEY OPERATION TYPE>?api-version=2016-03-31' -X POST -d "" -H "Authorization: Bearer <ACCESS TOKEN>" 
```

> [!NOTE]
> <span data-ttu-id="2e6ed-170">The text in the prior URL is case-sensitive, so ensure if you are using upper-lowercase for your Resource Groups to reflect it accordingly.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-170">The text in the prior URL is case-sensitive, so ensure if you are using upper-lowercase for your Resource Groups to reflect it accordingly.</span></span> <span data-ttu-id="2e6ed-171">Additionally, it’s important to know that this is a POST request not a GET request and ensure you pass a value to capture a length limit with -d that can be NULL.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-171">Additionally, it’s important to know that this is a POST request not a GET request and ensure you pass a value to capture a length limit with -d that can be NULL.</span></span>  

<span data-ttu-id="2e6ed-172">The CURL response gives you the list of Keys.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-172">The CURL response gives you the list of Keys.</span></span>  <span data-ttu-id="2e6ed-173">For example, if you get the read-only keys:</span><span class="sxs-lookup"><span data-stu-id="2e6ed-173">For example, if you get the read-only keys:</span></span>  

```bash 
{"primaryReadonlyMasterKey":"bWpDxS...dzQ==",
"secondaryReadonlyMasterKey":"38v5ns...7bA=="}
```

Now that you have the access key for the Cosmos DB account you can pass it to a Cosmos DB SDK and make calls to access the account.  For a quick example, you can pass the access key to the Azure CLI.  You can get the <COSMOS DB CONNECTION URL> from the **Overview** tab on the Cosmos DB account blade in the Azure portal.  <span data-ttu-id="2e6ed-177">Replace the <ACCESS KEY> with the value you obtained above:</span><span class="sxs-lookup"><span data-stu-id="2e6ed-177">Replace the <ACCESS KEY> with the value you obtained above:</span></span>

```bash
az cosmosdb collection show -c <COLLECTION ID> -d <DATABASE ID> --url-connection "<COSMOS DB CONNECTION URL>" --key <ACCESS KEY>
```

<span data-ttu-id="2e6ed-178">This CLI command returns details about the collection:</span><span class="sxs-lookup"><span data-stu-id="2e6ed-178">This CLI command returns details about the collection:</span></span>

```bash
{
  "collection": {
    "_conflicts": "conflicts/",
    "_docs": "docs/",
    "_etag": "\"00006700-0000-0000-0000-5a8271e90000\"",
    "_rid": "Es5SAM2FDwA=",
    "_self": "dbs/Es5SAA==/colls/Es5SAM2FDwA=/",
    "_sprocs": "sprocs/",
    "_triggers": "triggers/",
    "_ts": 1518498281,
    "_udfs": "udfs/",
    "id": "Test",
    "indexingPolicy": {
      "automatic": true,
      "excludedPaths": [],
      "includedPaths": [
        {
          "indexes": [
            {
              "dataType": "Number",
              "kind": "Range",
              "precision": -1
            },
            {
              "dataType": "String",
              "kind": "Range",
              "precision": -1
            },
            {
              "dataType": "Point",
              "kind": "Spatial"
            }
          ],
          "path": "/*"
        }
      ],
      "indexingMode": "consistent"
    }
  },
  "offer": {
    "_etag": "\"00006800-0000-0000-0000-5a8271ea0000\"",
    "_rid": "f4V+",
    "_self": "offers/f4V+/",
    "_ts": 1518498282,
    "content": {
      "offerIsRUPerMinuteThroughputEnabled": false,
      "offerThroughput": 400
    },
    "id": "f4V+",
    "offerResourceId": "Es5SAM2FDwA=",
    "offerType": "Invalid",
    "offerVersion": "V2",
    "resource": "dbs/Es5SAA==/colls/Es5SAM2FDwA=/"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="2e6ed-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="2e6ed-179">Next steps</span></span>

<span data-ttu-id="2e6ed-180">In this tutorial, you learned how to use a system-assigned managed identity on a Linux virtual machine to access Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2e6ed-180">In this tutorial, you learned how to use a system-assigned managed identity on a Linux virtual machine to access Cosmos DB.</span></span>  <span data-ttu-id="2e6ed-181">To learn more about Cosmos DB see:</span><span class="sxs-lookup"><span data-stu-id="2e6ed-181">To learn more about Cosmos DB see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="2e6ed-182">Azure Cosmos DB overview</span><span class="sxs-lookup"><span data-stu-id="2e6ed-182">Azure Cosmos DB overview</span></span>](/azure/cosmos-db/introduction)

