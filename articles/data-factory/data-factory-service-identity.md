---
title: Azure Data Factory service identity | Microsoft Docs
description: Learn about data factory service identity in Azure Data Factory.
services: data-factory
author: linda33wj
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/17/2018
ms.author: jingwang
ms.openlocfilehash: ffe7337282d06dd9a7e22d6750ac98b3a56964bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856148"
---
# <a name="azure-data-factory-service-identity"></a><span data-ttu-id="edf60-103">Azure Data Factory service identity</span><span class="sxs-lookup"><span data-stu-id="edf60-103">Azure Data Factory service identity</span></span>

<span data-ttu-id="edf60-104">This article helps you understand what is data factory service identity and how it works.</span><span class="sxs-lookup"><span data-stu-id="edf60-104">This article helps you understand what is data factory service identity and how it works.</span></span>

## <a name="overview"></a><span data-ttu-id="edf60-105">Overview</span><span class="sxs-lookup"><span data-stu-id="edf60-105">Overview</span></span>

<span data-ttu-id="edf60-106">When creating a data factory, a service identity can be created along with factory creation.</span><span class="sxs-lookup"><span data-stu-id="edf60-106">When creating a data factory, a service identity can be created along with factory creation.</span></span> <span data-ttu-id="edf60-107">The service identity is a managed application registered to Azure Activity Directory, and represents this specific data factory.</span><span class="sxs-lookup"><span data-stu-id="edf60-107">The service identity is a managed application registered to Azure Activity Directory, and represents this specific data factory.</span></span>

<span data-ttu-id="edf60-108">Data factory service identity benefits the following features:</span><span class="sxs-lookup"><span data-stu-id="edf60-108">Data factory service identity benefits the following features:</span></span>

- <span data-ttu-id="edf60-109">[Store credential in Azure Key Vault](store-credentials-in-key-vault.md), in which case data factory service identity is used for Azure Key Vault authentication.</span><span class="sxs-lookup"><span data-stu-id="edf60-109">[Store credential in Azure Key Vault](store-credentials-in-key-vault.md), in which case data factory service identity is used for Azure Key Vault authentication.</span></span>
- <span data-ttu-id="edf60-110">Connectors including [Azure Blob storage](connector-azure-blob-storage.md), [Azure Data Lake Storage Gen1](connector-azure-data-lake-store.md), [Azure SQL Database](connector-azure-sql-database.md), and [Azure SQL Data Warehouse](connector-azure-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="edf60-110">Connectors including [Azure Blob storage](connector-azure-blob-storage.md), [Azure Data Lake Storage Gen1](connector-azure-data-lake-store.md), [Azure SQL Database](connector-azure-sql-database.md), and [Azure SQL Data Warehouse](connector-azure-sql-data-warehouse.md).</span></span>

## <a name="generate-service-identity"></a><span data-ttu-id="edf60-111">Generate service identity</span><span class="sxs-lookup"><span data-stu-id="edf60-111">Generate service identity</span></span>

<span data-ttu-id="edf60-112">Data factory service identity is generated as follows:</span><span class="sxs-lookup"><span data-stu-id="edf60-112">Data factory service identity is generated as follows:</span></span>

- <span data-ttu-id="edf60-113">When creating data factory through **Azure portal or PowerShell**, service identity will always be created automatically.</span><span class="sxs-lookup"><span data-stu-id="edf60-113">When creating data factory through **Azure portal or PowerShell**, service identity will always be created automatically.</span></span>
- <span data-ttu-id="edf60-114">When creating data factory through **SDK**, service identity will be created only if you specify "Identity = new FactoryIdentity()" in the factory object for creation.</span><span class="sxs-lookup"><span data-stu-id="edf60-114">When creating data factory through **SDK**, service identity will be created only if you specify "Identity = new FactoryIdentity()" in the factory object for creation.</span></span> <span data-ttu-id="edf60-115">See example in [.NET quickstart - create data factory](quickstart-create-data-factory-dot-net.md#create-a-data-factory).</span><span class="sxs-lookup"><span data-stu-id="edf60-115">See example in [.NET quickstart - create data factory](quickstart-create-data-factory-dot-net.md#create-a-data-factory).</span></span>
- <span data-ttu-id="edf60-116">When creating data factory through **REST API**, service identity will be created only if you specify "identity" section in request body.</span><span class="sxs-lookup"><span data-stu-id="edf60-116">When creating data factory through **REST API**, service identity will be created only if you specify "identity" section in request body.</span></span> <span data-ttu-id="edf60-117">See example in [REST quickstart - create data factory](quickstart-create-data-factory-rest-api.md#create-a-data-factory).</span><span class="sxs-lookup"><span data-stu-id="edf60-117">See example in [REST quickstart - create data factory](quickstart-create-data-factory-rest-api.md#create-a-data-factory).</span></span>

<span data-ttu-id="edf60-118">If you find your data factory doesn't have a service identity associated following [retrieve service identity](#retrieve-service-identity) instruction, you can explicitly generate one by updating the data factory with identity initiator programmatically:</span><span class="sxs-lookup"><span data-stu-id="edf60-118">If you find your data factory doesn't have a service identity associated following [retrieve service identity](#retrieve-service-identity) instruction, you can explicitly generate one by updating the data factory with identity initiator programmatically:</span></span>

- [<span data-ttu-id="edf60-119">Generate service identity using PowerShell</span><span class="sxs-lookup"><span data-stu-id="edf60-119">Generate service identity using PowerShell</span></span>](#generate-service-identity-using-powershell)
- [<span data-ttu-id="edf60-120">Generate service identity using REST API</span><span class="sxs-lookup"><span data-stu-id="edf60-120">Generate service identity using REST API</span></span>](#generate-service-identity-using-rest-api)
- [<span data-ttu-id="edf60-121">Generate service identity using SDK</span><span class="sxs-lookup"><span data-stu-id="edf60-121">Generate service identity using SDK</span></span>](#generate-service-identity-using-sdk)

>[!NOTE]
>- <span data-ttu-id="edf60-122">Service identity cannot be modified.</span><span class="sxs-lookup"><span data-stu-id="edf60-122">Service identity cannot be modified.</span></span> <span data-ttu-id="edf60-123">Updating a data factory which already have a service identity won't have any impact, the service identity is kept unchanged.</span><span class="sxs-lookup"><span data-stu-id="edf60-123">Updating a data factory which already have a service identity won't have any impact, the service identity is kept unchanged.</span></span>
>- <span data-ttu-id="edf60-124">If you update a data factory which already have a service identity without specifying "identity" parameter in the factory object or without specifying "identity" section in REST request body, you will get an error.</span><span class="sxs-lookup"><span data-stu-id="edf60-124">If you update a data factory which already have a service identity without specifying "identity" parameter in the factory object or without specifying "identity" section in REST request body, you will get an error.</span></span>
>- <span data-ttu-id="edf60-125">When you delete a data factory, the associated service identity will be deleted along.</span><span class="sxs-lookup"><span data-stu-id="edf60-125">When you delete a data factory, the associated service identity will be deleted along.</span></span>

### <a name="generate-service-identity-using-powershell"></a><span data-ttu-id="edf60-126">Generate service identity using PowerShell</span><span class="sxs-lookup"><span data-stu-id="edf60-126">Generate service identity using PowerShell</span></span>

<span data-ttu-id="edf60-127">Call **Set-AzureRmDataFactoryV2** command again, then you see "Identity" fields being newly generated:</span><span class="sxs-lookup"><span data-stu-id="edf60-127">Call **Set-AzureRmDataFactoryV2** command again, then you see "Identity" fields being newly generated:</span></span>

```powershell
PS C:\WINDOWS\system32> Set-AzureRmDataFactoryV2 -ResourceGroupName <resourceGroupName> -Name <dataFactoryName> -Location <region>

DataFactoryName   : ADFV2DemoFactory
DataFactoryId     : /subscriptions/<subsID>/resourceGroups/<resourceGroupName>/providers/Microsoft.DataFactory/factories/ADFV2DemoFactory
ResourceGroupName : <resourceGroupName>
Location          : East US
Tags              : {}
Identity          : Microsoft.Azure.Management.DataFactory.Models.FactoryIdentity
ProvisioningState : Succeeded
```

### <a name="generate-service-identity-using-rest-api"></a><span data-ttu-id="edf60-128">Generate service identity using REST API</span><span class="sxs-lookup"><span data-stu-id="edf60-128">Generate service identity using REST API</span></span>

<span data-ttu-id="edf60-129">Call below API with "identity" section in the request body:</span><span class="sxs-lookup"><span data-stu-id="edf60-129">Call below API with "identity" section in the request body:</span></span>

```
PATCH https://management.azure.com/subscriptions/<subsID>/resourceGroups/<resourceGroupName>/providers/Microsoft.DataFactory/factories/<data factory name>?api-version=2017-09-01-preview
```

<span data-ttu-id="edf60-130">**Request body**: add "identity": { "type": "SystemAssigned" }.</span><span class="sxs-lookup"><span data-stu-id="edf60-130">**Request body**: add "identity": { "type": "SystemAssigned" }.</span></span>

```json
{
    "name": "<dataFactoryName>",
    "location": "<region>",
    "properties": {},
    "identity": {
        "type": "SystemAssigned"
    }
}
```

<span data-ttu-id="edf60-131">**Response**: service identity is created automatically, and "identity" section is populated accordingly.</span><span class="sxs-lookup"><span data-stu-id="edf60-131">**Response**: service identity is created automatically, and "identity" section is populated accordingly.</span></span>

```json
{
    "name": "ADFV2DemoFactory",
    "tags": {},
    "properties": {
        "provisioningState": "Succeeded",
        "loggingStorageAccountKey": "**********",
        "createTime": "2017-09-26T04:10:01.1135678Z",
        "version": "2017-09-01-preview"
    },
    "identity": {
        "type": "SystemAssigned",
        "principalId": "765ad4ab-XXXX-XXXX-XXXX-51ed985819dc",
        "tenantId": "72f988bf-XXXX-XXXX-XXXX-2d7cd011db47"
    },
    "id": "/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.DataFactory/factories/ADFV2DemoFactory",
    "type": "Microsoft.DataFactory/factories",
    "location": "EastUS"
}
```

### <a name="generate-service-identity-using-sdk"></a><span data-ttu-id="edf60-132">Generate service identity using SDK</span><span class="sxs-lookup"><span data-stu-id="edf60-132">Generate service identity using SDK</span></span>

<span data-ttu-id="edf60-133">Call the data factory create_or_update function with Identity=new FactoryIdentity().</span><span class="sxs-lookup"><span data-stu-id="edf60-133">Call the data factory create_or_update function with Identity=new FactoryIdentity().</span></span> <span data-ttu-id="edf60-134">Sample code using .NET:</span><span class="sxs-lookup"><span data-stu-id="edf60-134">Sample code using .NET:</span></span>

```csharp
Factory dataFactory = new Factory
{
    Location = <region>,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
```

## <a name="retrieve-service-identity"></a><span data-ttu-id="edf60-135">Retrieve service identity</span><span class="sxs-lookup"><span data-stu-id="edf60-135">Retrieve service identity</span></span>

<span data-ttu-id="edf60-136">You can retrieve the service identity from Azure portal or programmatically.</span><span class="sxs-lookup"><span data-stu-id="edf60-136">You can retrieve the service identity from Azure portal or programmatically.</span></span> <span data-ttu-id="edf60-137">The following sections show some samples.</span><span class="sxs-lookup"><span data-stu-id="edf60-137">The following sections show some samples.</span></span>

>[!TIP]
> <span data-ttu-id="edf60-138">If you don't see the service identity, [generate service identity](#generate-service-identity) by updating your factory.</span><span class="sxs-lookup"><span data-stu-id="edf60-138">If you don't see the service identity, [generate service identity](#generate-service-identity) by updating your factory.</span></span>

### <a name="retrieve-service-identity-using-azure-portal"></a><span data-ttu-id="edf60-139">Retrieve service identity using Azure portal</span><span class="sxs-lookup"><span data-stu-id="edf60-139">Retrieve service identity using Azure portal</span></span>

<span data-ttu-id="edf60-140">You can find the service identity information from Azure portal -> your data factory -> Settings -> Properties:</span><span class="sxs-lookup"><span data-stu-id="edf60-140">You can find the service identity information from Azure portal -> your data factory -> Settings -> Properties:</span></span>

- <span data-ttu-id="edf60-141">SERVICE IDENTITY ID</span><span class="sxs-lookup"><span data-stu-id="edf60-141">SERVICE IDENTITY ID</span></span>
- <span data-ttu-id="edf60-142">SERVICE IDENTITY TENANT</span><span class="sxs-lookup"><span data-stu-id="edf60-142">SERVICE IDENTITY TENANT</span></span>
- <span data-ttu-id="edf60-143">**SERVICE IDENTITY APPLICATION ID** > copy this value</span><span class="sxs-lookup"><span data-stu-id="edf60-143">**SERVICE IDENTITY APPLICATION ID** > copy this value</span></span>

![Retrieve service identity](media/data-factory-service-identity/retrieve-service-identity-portal.png)

### <a name="retrieve-service-identity-using-powershell"></a><span data-ttu-id="edf60-145">Retrieve service identity using PowerShell</span><span class="sxs-lookup"><span data-stu-id="edf60-145">Retrieve service identity using PowerShell</span></span>

<span data-ttu-id="edf60-146">The service identity principal ID and tenant ID will be returned when you get a specific data factory as follows:</span><span class="sxs-lookup"><span data-stu-id="edf60-146">The service identity principal ID and tenant ID will be returned when you get a specific data factory as follows:</span></span>

```powershell
PS C:\WINDOWS\system32> (Get-AzureRmDataFactoryV2 -ResourceGroupName <resourceGroupName> -Name <dataFactoryName>).Identity

PrincipalId                          TenantId
-----------                          --------
765ad4ab-XXXX-XXXX-XXXX-51ed985819dc 72f988bf-XXXX-XXXX-XXXX-2d7cd011db47
```

<span data-ttu-id="edf60-147">Copy the principal ID, then run below Azure Active Directory command with principal ID as parameter to get the **ApplicationId**, which you use to grant access:</span><span class="sxs-lookup"><span data-stu-id="edf60-147">Copy the principal ID, then run below Azure Active Directory command with principal ID as parameter to get the **ApplicationId**, which you use to grant access:</span></span>

```powershell
PS C:\WINDOWS\system32> Get-AzureRmADServicePrincipal -ObjectId 765ad4ab-XXXX-XXXX-XXXX-51ed985819dc

ServicePrincipalNames : {76f668b3-XXXX-XXXX-XXXX-1b3348c75e02, https://identity.azure.net/P86P8g6nt1QxfPJx22om8MOooMf/Ag0Qf/nnREppHkU=}
ApplicationId         : 76f668b3-XXXX-XXXX-XXXX-1b3348c75e02
DisplayName           : ADFV2DemoFactory
Id                    : 765ad4ab-XXXX-XXXX-XXXX-51ed985819dc
Type                  : ServicePrincipal
```

## <a name="next-steps"></a><span data-ttu-id="edf60-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="edf60-148">Next steps</span></span>
<span data-ttu-id="edf60-149">See the following topics which introduce when and how to use data factory service identity:</span><span class="sxs-lookup"><span data-stu-id="edf60-149">See the following topics which introduce when and how to use data factory service identity:</span></span>

- [<span data-ttu-id="edf60-150">Store credential in Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="edf60-150">Store credential in Azure Key Vault</span></span>](store-credentials-in-key-vault.md)
- [<span data-ttu-id="edf60-151">Copy data from/to Azure Data Lake Store using managed service identity authentication</span><span class="sxs-lookup"><span data-stu-id="edf60-151">Copy data from/to Azure Data Lake Store using managed service identity authentication</span></span>](connector-azure-data-lake-store.md)

<span data-ttu-id="edf60-152">See [MSI Overview](~/articles/active-directory/msi-overview.md) for more background on Managed Service Identity, which data factory service identity is based upon.</span><span class="sxs-lookup"><span data-stu-id="edf60-152">See [MSI Overview](~/articles/active-directory/msi-overview.md) for more background on Managed Service Identity, which data factory service identity is based upon.</span></span> 