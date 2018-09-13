---
title: Use a Windows VM system-assigned managed identity to access Azure Cosmos DB
description: A tutorial that walks you through the process of using a system-assigned managed identity on a Windows VM, to access Azure Cosmos DB.
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
ms.date: 04/10/2018
ms.author: daveba
ms.openlocfilehash: 00dd4fd809c7078f5c4c037fabd16ab9e6f41684
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858117"
---
# <a name="tutorial-use-a-windows-vm-system-assigned-managed-identity-to-access-azure-cosmos-db"></a><span data-ttu-id="05c30-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="05c30-103">Tutorial: Use a Windows VM system-assigned managed identity to access Azure Cosmos DB</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="05c30-104">This tutorial shows you how to use a system-assigned managed identity for a Windows virtual machine (VM) to access Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05c30-104">This tutorial shows you how to use a system-assigned managed identity for a Windows virtual machine (VM) to access Cosmos DB.</span></span> <span data-ttu-id="05c30-105">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="05c30-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="05c30-106">Create a Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="05c30-106">Create a Cosmos DB account</span></span>
> * <span data-ttu-id="05c30-107">Grant a Windows VM system-assigned managed identity access to the Cosmos DB account access keys</span><span class="sxs-lookup"><span data-stu-id="05c30-107">Grant a Windows VM system-assigned managed identity access to the Cosmos DB account access keys</span></span>
> * <span data-ttu-id="05c30-108">Get an access token using the Windows VM system-assigned managed identity to call Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05c30-108">Get an access token using the Windows VM system-assigned managed identity to call Azure Resource Manager</span></span>
> * <span data-ttu-id="05c30-109">Get access keys from Azure Resource Manager to make Cosmos DB calls</span><span class="sxs-lookup"><span data-stu-id="05c30-109">Get access keys from Azure Resource Manager to make Cosmos DB calls</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05c30-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="05c30-110">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

- [<span data-ttu-id="05c30-111">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="05c30-111">Sign in to Azure portal</span></span>](https://portal.azure.com)

- [<span data-ttu-id="05c30-112">Create a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="05c30-112">Create a Windows virtual machine</span></span>](/azure/virtual-machines/windows/quick-create-portal)

- [<span data-ttu-id="05c30-113">Enable system-assigned managed identity on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="05c30-113">Enable system-assigned managed identity on your virtual machine</span></span>](/azure/active-directory/managed-service-identity/qs-configure-portal-windows-vm#enable-system-assigned-identity-on-an-existing-vm)

## <a name="create-a-cosmos-db-account"></a><span data-ttu-id="05c30-114">Create a Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="05c30-114">Create a Cosmos DB account</span></span> 

<span data-ttu-id="05c30-115">If you don't already have one, create a Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="05c30-115">If you don't already have one, create a Cosmos DB account.</span></span> <span data-ttu-id="05c30-116">You can skip this step and use an existing Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="05c30-116">You can skip this step and use an existing Cosmos DB account.</span></span> 

1. <span data-ttu-id="05c30-117">Click the **+/Create new service** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="05c30-117">Click the **+/Create new service** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="05c30-118">Click **Databases**, then **Azure Cosmos DB**, and a new "New account" panel  displays.</span><span class="sxs-lookup"><span data-stu-id="05c30-118">Click **Databases**, then **Azure Cosmos DB**, and a new "New account" panel  displays.</span></span>
3. <span data-ttu-id="05c30-119">Enter an **ID** for the Cosmos DB account, which you use later.</span><span class="sxs-lookup"><span data-stu-id="05c30-119">Enter an **ID** for the Cosmos DB account, which you use later.</span></span>  
4. <span data-ttu-id="05c30-120">**API** should be set to "SQL."</span><span class="sxs-lookup"><span data-stu-id="05c30-120">**API** should be set to "SQL."</span></span> <span data-ttu-id="05c30-121">The approach described in this tutorial can be used with the other available API types, but the steps in this tutorial are for the SQL API.</span><span class="sxs-lookup"><span data-stu-id="05c30-121">The approach described in this tutorial can be used with the other available API types, but the steps in this tutorial are for the SQL API.</span></span>
5. <span data-ttu-id="05c30-122">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span><span class="sxs-lookup"><span data-stu-id="05c30-122">Ensure the **Subscription** and **Resource Group** match the ones you specified when you created your VM in the previous step.</span></span>  <span data-ttu-id="05c30-123">Select a **Location** where Cosmos DB is available.</span><span class="sxs-lookup"><span data-stu-id="05c30-123">Select a **Location** where Cosmos DB is available.</span></span>
6. <span data-ttu-id="05c30-124">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="05c30-124">Click **Create**.</span></span>

## <a name="create-a-collection-in-the-cosmos-db-account"></a><span data-ttu-id="05c30-125">Create a collection in the Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="05c30-125">Create a collection in the Cosmos DB account</span></span>

<span data-ttu-id="05c30-126">Next, add a data collection in the Cosmos DB account that you can query in later steps.</span><span class="sxs-lookup"><span data-stu-id="05c30-126">Next, add a data collection in the Cosmos DB account that you can query in later steps.</span></span>

1. <span data-ttu-id="05c30-127">Navigate to your newly created Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="05c30-127">Navigate to your newly created Cosmos DB account.</span></span>
2. <span data-ttu-id="05c30-128">On the **Overview** tab click the **+/Add Collection** button, and an "Add Collection" panel slides out.</span><span class="sxs-lookup"><span data-stu-id="05c30-128">On the **Overview** tab click the **+/Add Collection** button, and an "Add Collection" panel slides out.</span></span>
3. <span data-ttu-id="05c30-129">Give the collection a database ID, collection ID, select a storage capacity, enter a partition key, enter a throughput value, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="05c30-129">Give the collection a database ID, collection ID, select a storage capacity, enter a partition key, enter a throughput value, then click **OK**.</span></span>  <span data-ttu-id="05c30-130">For this tutorial, it is sufficient to use "Test" as the database ID and collection ID, select a fixed storage capacity and lowest throughput (400 RU/s).</span><span class="sxs-lookup"><span data-stu-id="05c30-130">For this tutorial, it is sufficient to use "Test" as the database ID and collection ID, select a fixed storage capacity and lowest throughput (400 RU/s).</span></span>  

## <a name="grant-windows-vm-system-assigned-managed-identity-access-to-the-cosmos-db-account-access-keys"></a><span data-ttu-id="05c30-131">Grant Windows VM system-assigned managed identity access to the Cosmos DB account access keys</span><span class="sxs-lookup"><span data-stu-id="05c30-131">Grant Windows VM system-assigned managed identity access to the Cosmos DB account access keys</span></span>

<span data-ttu-id="05c30-132">Cosmos DB does not natively support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="05c30-132">Cosmos DB does not natively support Azure AD authentication.</span></span> <span data-ttu-id="05c30-133">However, you can use a system-assigned managed identity to retrieve a Cosmos DB access key from the Resource Manager, and use the key to access Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05c30-133">However, you can use a system-assigned managed identity to retrieve a Cosmos DB access key from the Resource Manager, and use the key to access Cosmos DB.</span></span> <span data-ttu-id="05c30-134">In this step, you grant your Windows VM system-assigned managed identity access to the keys to the Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="05c30-134">In this step, you grant your Windows VM system-assigned managed identity access to the keys to the Cosmos DB account.</span></span>

<span data-ttu-id="05c30-135">To grant the Windows VM system-assigned managed identity access to the Cosmos DB account in Azure Resource Manager using PowerShell, update the values for `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<COSMOS DB ACCOUNT NAME>` for your environment.</span><span class="sxs-lookup"><span data-stu-id="05c30-135">To grant the Windows VM system-assigned managed identity access to the Cosmos DB account in Azure Resource Manager using PowerShell, update the values for `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<COSMOS DB ACCOUNT NAME>` for your environment.</span></span> <span data-ttu-id="05c30-136">Replace `<PRINCIPALID>` with the `principalId` property returned by the `az resource show` command in [Retrieve the principalID of the Linux VM's system-assigned managed identity](#retrieve-the-principalID-of-the-linux-VM's-MSI).</span><span class="sxs-lookup"><span data-stu-id="05c30-136">Replace `<PRINCIPALID>` with the `principalId` property returned by the `az resource show` command in [Retrieve the principalID of the Linux VM's system-assigned managed identity](#retrieve-the-principalID-of-the-linux-VM's-MSI).</span></span>  <span data-ttu-id="05c30-137">Cosmos DB supports two levels of granularity when using access keys:  read/write access to the account, and read-only access to the account.</span><span class="sxs-lookup"><span data-stu-id="05c30-137">Cosmos DB supports two levels of granularity when using access keys:  read/write access to the account, and read-only access to the account.</span></span>  <span data-ttu-id="05c30-138">Assign the `DocumentDB Account Contributor` role if you want to get read/write keys for the account, or assign the `Cosmos DB Account Reader Role` role if you want to get read-only keys for the account:</span><span class="sxs-lookup"><span data-stu-id="05c30-138">Assign the `DocumentDB Account Contributor` role if you want to get read/write keys for the account, or assign the `Cosmos DB Account Reader Role` role if you want to get read-only keys for the account:</span></span>

```azurepowershell
$spID = (Get-AzureRMVM -ResourceGroupName myRG -Name myVM).identity.principalid
New-AzureRmRoleAssignment -ObjectId $spID -RoleDefinitionName "Reader" -Scope "/subscriptions/<mySubscriptionID>/resourceGroups/<myResourceGroup>/providers/Microsoft.Storage/storageAccounts/<myStorageAcct>"
```

## <a name="get-an-access-token-using-the-windows-vm-system-assigned-managed-identity-to-call-azure-resource-manager"></a><span data-ttu-id="05c30-139">Get an access token using the Windows VM system-assigned managed identity to call Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05c30-139">Get an access token using the Windows VM system-assigned managed identity to call Azure Resource Manager</span></span>

<span data-ttu-id="05c30-140">For the remainder of the tutorial, we will work from the VM we created earlier.</span><span class="sxs-lookup"><span data-stu-id="05c30-140">For the remainder of the tutorial, we will work from the VM we created earlier.</span></span> 

<span data-ttu-id="05c30-141">You will need to use the Azure Resource Manager PowerShell cmdlets in this portion.</span><span class="sxs-lookup"><span data-stu-id="05c30-141">You will need to use the Azure Resource Manager PowerShell cmdlets in this portion.</span></span>  <span data-ttu-id="05c30-142">If you don’t have it installed, [download the latest version](https://docs.microsoft.com/powershell/azure/overview) before continuing.</span><span class="sxs-lookup"><span data-stu-id="05c30-142">If you don’t have it installed, [download the latest version](https://docs.microsoft.com/powershell/azure/overview) before continuing.</span></span>

<span data-ttu-id="05c30-143">You will also need to install the latest version of [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) on your Windows VM.</span><span class="sxs-lookup"><span data-stu-id="05c30-143">You will also need to install the latest version of [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) on your Windows VM.</span></span>

1. <span data-ttu-id="05c30-144">In the Azure portal, navigate to **Virtual Machines**, go to your Windows virtual machine, then from the **Overview** page click **Connect** at the top.</span><span class="sxs-lookup"><span data-stu-id="05c30-144">In the Azure portal, navigate to **Virtual Machines**, go to your Windows virtual machine, then from the **Overview** page click **Connect** at the top.</span></span> 
2. <span data-ttu-id="05c30-145">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span><span class="sxs-lookup"><span data-stu-id="05c30-145">Enter in your **Username** and **Password** for which you added when you created the Windows VM.</span></span> 
3. <span data-ttu-id="05c30-146">Now that you have created a **Remote Desktop Connection** with the virtual machine, open PowerShell in the remote session.</span><span class="sxs-lookup"><span data-stu-id="05c30-146">Now that you have created a **Remote Desktop Connection** with the virtual machine, open PowerShell in the remote session.</span></span>
4. <span data-ttu-id="05c30-147">Using Powershell’s Invoke-WebRequest, make a request to the local managed identities for Azure resources endpoint to get an access token for Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="05c30-147">Using Powershell’s Invoke-WebRequest, make a request to the local managed identities for Azure resources endpoint to get an access token for Azure Resource Manager.</span></span>

    ```powershell
        $response = Invoke-WebRequest -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -Method GET -Headers @{Metadata="true"}
    ```

    > [!NOTE]
    > <span data-ttu-id="05c30-148">The value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05c30-148">The value of the "resource" parameter must be an exact match for what is expected by Azure AD.</span></span> <span data-ttu-id="05c30-149">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span><span class="sxs-lookup"><span data-stu-id="05c30-149">When using the Azure Resource Manager resource ID, you must include the trailing slash on the URI.</span></span>
    
    <span data-ttu-id="05c30-150">Next, extract the "Content" element, which is stored as a JavaScript Object Notation (JSON) formatted string in the $response object.</span><span class="sxs-lookup"><span data-stu-id="05c30-150">Next, extract the "Content" element, which is stored as a JavaScript Object Notation (JSON) formatted string in the $response object.</span></span> 
    
    ```powershell
    $content = $response.Content | ConvertFrom-Json
    ```
    <span data-ttu-id="05c30-151">Next, extract the access token from the response.</span><span class="sxs-lookup"><span data-stu-id="05c30-151">Next, extract the access token from the response.</span></span>
    
    ```powershell
    $ArmToken = $content.access_token
    ```

## <a name="get-access-keys-from-azure-resource-manager-to-make-cosmos-db-calls"></a><span data-ttu-id="05c30-152">Get access keys from Azure Resource Manager to make Cosmos DB calls</span><span class="sxs-lookup"><span data-stu-id="05c30-152">Get access keys from Azure Resource Manager to make Cosmos DB calls</span></span>

<span data-ttu-id="05c30-153">Now use PowerShell to call Resource Manager using the access token retrieved in the previous section to retrieve the Cosmos DB account access key.</span><span class="sxs-lookup"><span data-stu-id="05c30-153">Now use PowerShell to call Resource Manager using the access token retrieved in the previous section to retrieve the Cosmos DB account access key.</span></span> <span data-ttu-id="05c30-154">Once we have the access key, we can query Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05c30-154">Once we have the access key, we can query Cosmos DB.</span></span> <span data-ttu-id="05c30-155">Be sure to replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<COSMOS DB ACCOUNT NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="05c30-155">Be sure to replace the `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, and `<COSMOS DB ACCOUNT NAME>` parameter values with your own values.</span></span> <span data-ttu-id="05c30-156">Replace the `<ACCESS TOKEN>` value with the access token you retrieved earlier.</span><span class="sxs-lookup"><span data-stu-id="05c30-156">Replace the `<ACCESS TOKEN>` value with the access token you retrieved earlier.</span></span>  <span data-ttu-id="05c30-157">If you want to retrieve read/write keys, use key operation type `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="05c30-157">If you want to retrieve read/write keys, use key operation type `listKeys`.</span></span>  <span data-ttu-id="05c30-158">If you want to retrieve read-only keys, use the key operation type `readonlykeys`:</span><span class="sxs-lookup"><span data-stu-id="05c30-158">If you want to retrieve read-only keys, use the key operation type `readonlykeys`:</span></span>

```powershell
Invoke-WebRequest -Uri https://management.azure.com/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>/providers/Microsoft.DocumentDb/databaseAccounts/<COSMOS DB ACCOUNT NAME>/listKeys/?api-version=2016-12-01 -Method POST -Headers @{Authorization="Bearer $ARMToken"}
```
<span data-ttu-id="05c30-159">The response give you the list of Keys.</span><span class="sxs-lookup"><span data-stu-id="05c30-159">The response give you the list of Keys.</span></span>  <span data-ttu-id="05c30-160">For example, if you get read-only keys:</span><span class="sxs-lookup"><span data-stu-id="05c30-160">For example, if you get read-only keys:</span></span>

```powershell
{"primaryReadonlyMasterKey":"bWpDxS...dzQ==",
"secondaryReadonlyMasterKey":"38v5ns...7bA=="}
```
Now that you have the access key for the Cosmos DB account you can pass it to a Cosmos DB SDK and make calls to access the account.  For a quick example, you can pass the access key to the Azure CLI.  You can get the <COSMOS DB CONNECTION URL> from the **Overview** tab on the Cosmos DB account blade in the Azure portal.  <span data-ttu-id="05c30-164">Replace the <ACCESS KEY> with the value you obtained above:</span><span class="sxs-lookup"><span data-stu-id="05c30-164">Replace the <ACCESS KEY> with the value you obtained above:</span></span>

```bash
az cosmosdb collection show -c <COLLECTION ID> -d <DATABASE ID> --url-connection "<COSMOS DB CONNECTION URL>" --key <ACCESS KEY>
```

<span data-ttu-id="05c30-165">This CLI command returns details about the collection:</span><span class="sxs-lookup"><span data-stu-id="05c30-165">This CLI command returns details about the collection:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="05c30-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="05c30-166">Next steps</span></span>

<span data-ttu-id="05c30-167">In this tutorial, you learned how to use a Windows VM system-assigned identity to access Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="05c30-167">In this tutorial, you learned how to use a Windows VM system-assigned identity to access Cosmos DB.</span></span>  <span data-ttu-id="05c30-168">To learn more about Cosmos DB see:</span><span class="sxs-lookup"><span data-stu-id="05c30-168">To learn more about Cosmos DB see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="05c30-169">Azure Cosmos DB overview</span><span class="sxs-lookup"><span data-stu-id="05c30-169">Azure Cosmos DB overview</span></span>](/azure/cosmos-db/introduction)


