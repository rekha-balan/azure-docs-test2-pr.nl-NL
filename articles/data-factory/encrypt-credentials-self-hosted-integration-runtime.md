---
title: Encrypt credentials in Azure Data Factory | Microsoft Docs
description: Learn how to encrypt and store credentials for your on-premises data stores on a machine with self-hosted integration runtime.
services: data-factory
documentationcenter: ''
author: nabhishek
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/15/2018
ms.author: abnarain
ms.openlocfilehash: b577c276627c3a187215cd0da551428fbb32791f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867370"
---
# <a name="encrypt-credentials-for-on-premises-data-stores-in-azure-data-factory"></a><span data-ttu-id="e064f-103">Encrypt credentials for on-premises data stores in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e064f-103">Encrypt credentials for on-premises data stores in Azure Data Factory</span></span>
<span data-ttu-id="e064f-104">You can encrypt and store credentials for your on-premises data stores (linked services with sensitive information) on a machine with self-hosted integration runtime.</span><span class="sxs-lookup"><span data-stu-id="e064f-104">You can encrypt and store credentials for your on-premises data stores (linked services with sensitive information) on a machine with self-hosted integration runtime.</span></span> 

<span data-ttu-id="e064f-105">You pass a JSON definition file with credentials to the</span><span class="sxs-lookup"><span data-stu-id="e064f-105">You pass a JSON definition file with credentials to the</span></span> <br/><span data-ttu-id="e064f-106">[**New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential**](https://docs.microsoft.com/powershell/module/azurerm.datafactoryv2/New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential?view=azurermps-4.4.0) cmdlet to produce an output JSON definition file with the encrypted credentials.</span><span class="sxs-lookup"><span data-stu-id="e064f-106">[**New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential**](https://docs.microsoft.com/powershell/module/azurerm.datafactoryv2/New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential?view=azurermps-4.4.0) cmdlet to produce an output JSON definition file with the encrypted credentials.</span></span> <span data-ttu-id="e064f-107">Then, use the updated JSON definition to create the linked services.</span><span class="sxs-lookup"><span data-stu-id="e064f-107">Then, use the updated JSON definition to create the linked services.</span></span>

## <a name="author-sql-server-linked-service"></a><span data-ttu-id="e064f-108">Author SQL Server linked service</span><span class="sxs-lookup"><span data-stu-id="e064f-108">Author SQL Server linked service</span></span>
<span data-ttu-id="e064f-109">Create a JSON file named **SqlServerLinkedService.json** in any folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="e064f-109">Create a JSON file named **SqlServerLinkedService.json** in any folder with the following content:</span></span>  

<span data-ttu-id="e064f-110">Replace `<servername>`, `<databasename>`, `<username>`, and `<password>` with values for your SQL Server before saving the file.</span><span class="sxs-lookup"><span data-stu-id="e064f-110">Replace `<servername>`, `<databasename>`, `<username>`, and `<password>` with values for your SQL Server before saving the file.</span></span> <span data-ttu-id="e064f-111">And, replace `<integration runtime name>` with the name of your integration runtime.</span><span class="sxs-lookup"><span data-stu-id="e064f-111">And, replace `<integration runtime name>` with the name of your integration runtime.</span></span> 

```json
{
    "properties": {
        "type": "SqlServer",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Server=<servername>;Database=<databasename>;User ID=<username>;Password=<password>;Timeout=60"
            }
        },
        "connectVia": {
            "type": "integrationRuntimeReference",
            "referenceName": "<integration runtime name>"
        },
        "name": "SqlServerLinkedService"
    }
}
```

## <a name="encrypt-credentials"></a><span data-ttu-id="e064f-112">Encrypt credentials</span><span class="sxs-lookup"><span data-stu-id="e064f-112">Encrypt credentials</span></span>
<span data-ttu-id="e064f-113">To encrypt the sensitive data from the JSON payload on an on-premises self-hosted integration runtime, run **New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential**, and pass on the JSON payload.</span><span class="sxs-lookup"><span data-stu-id="e064f-113">To encrypt the sensitive data from the JSON payload on an on-premises self-hosted integration runtime, run **New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential**, and pass on the JSON payload.</span></span> <span data-ttu-id="e064f-114">This cmdlet ensures the credentials are encrypted using DPAPI and stored on the self-hosted integration runtime node locally.</span><span class="sxs-lookup"><span data-stu-id="e064f-114">This cmdlet ensures the credentials are encrypted using DPAPI and stored on the self-hosted integration runtime node locally.</span></span> <span data-ttu-id="e064f-115">The output payload can be redirected to another JSON file (in this case 'encryptedLinkedService.json'), which contains encrypted credentials.</span><span class="sxs-lookup"><span data-stu-id="e064f-115">The output payload can be redirected to another JSON file (in this case 'encryptedLinkedService.json'), which contains encrypted credentials.</span></span>

```powershell
New-AzureRmDataFactoryV2LinkedServiceEncryptedCredential -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "SqlServerLinkedService" -DefinitionFile ".\SQLServerLinkedService.json" > encryptedSQLServerLinkedService.json
```

## <a name="use-the-json-with-encrypted-credentials"></a><span data-ttu-id="e064f-116">Use the JSON with encrypted credentials</span><span class="sxs-lookup"><span data-stu-id="e064f-116">Use the JSON with encrypted credentials</span></span>
<span data-ttu-id="e064f-117">Now, use the output JSON file from the previous command containing the encrypted credential to set up the **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="e064f-117">Now, use the output JSON file from the previous command containing the encrypted credential to set up the **SqlServerLinkedService**.</span></span>

```powershell
Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $ResourceGroupName -Name "EncryptedSqlServerLinkedService" -DefinitionFile ".\encryptedSqlServerLinkedService.json" 
```

## <a name="next-steps"></a><span data-ttu-id="e064f-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="e064f-118">Next steps</span></span>
<span data-ttu-id="e064f-119">For information about security considerations for data movement, see [Data movement security considerations](data-movement-security-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="e064f-119">For information about security considerations for data movement, see [Data movement security considerations](data-movement-security-considerations.md).</span></span>

