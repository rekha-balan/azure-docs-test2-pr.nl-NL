---
title: Create Azure integration runtime in Azure Data Factory | Microsoft Docs
description: Learn how to create Azure integration runtime in Azure Data Factory, which is used to copy data and dispatch transform activities.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/15/2018
ms.author: douglasl
ms.openlocfilehash: cb1a263c0a33a291a44e7c60b3c032d7f9dc16a3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869825"
---
# <a name="how-to-create-and-configure-azure-integration-runtime"></a><span data-ttu-id="6ae40-103">How to create and configure Azure Integration Runtime</span><span class="sxs-lookup"><span data-stu-id="6ae40-103">How to create and configure Azure Integration Runtime</span></span>
<span data-ttu-id="6ae40-104">The Integration Runtime (IR) is the compute infrastructure used by Azure Data Factory to provide data integration capabilities across different network environments.</span><span class="sxs-lookup"><span data-stu-id="6ae40-104">The Integration Runtime (IR) is the compute infrastructure used by Azure Data Factory to provide data integration capabilities across different network environments.</span></span> <span data-ttu-id="6ae40-105">For more information about IR, see [Integration runtime](concepts-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="6ae40-105">For more information about IR, see [Integration runtime](concepts-integration-runtime.md).</span></span>

<span data-ttu-id="6ae40-106">Azure IR provides a fully managed compute to natively perform data movement and dispatch data transformation activities to compute services like HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ae40-106">Azure IR provides a fully managed compute to natively perform data movement and dispatch data transformation activities to compute services like HDInsight.</span></span> <span data-ttu-id="6ae40-107">It is hosted in Azure environment and supports connecting to resources in public network environment with public accessible endpoints.</span><span class="sxs-lookup"><span data-stu-id="6ae40-107">It is hosted in Azure environment and supports connecting to resources in public network environment with public accessible endpoints.</span></span>

<span data-ttu-id="6ae40-108">This document introduces how you can create and configure Azure Integration Runtime.</span><span class="sxs-lookup"><span data-stu-id="6ae40-108">This document introduces how you can create and configure Azure Integration Runtime.</span></span> 

## <a name="default-azure-ir"></a><span data-ttu-id="6ae40-109">Default Azure IR</span><span class="sxs-lookup"><span data-stu-id="6ae40-109">Default Azure IR</span></span>
<span data-ttu-id="6ae40-110">By default, each data factory has an Azure IR in the backend that supports  operations on cloud data stores and compute services in public network.</span><span class="sxs-lookup"><span data-stu-id="6ae40-110">By default, each data factory has an Azure IR in the backend that supports  operations on cloud data stores and compute services in public network.</span></span> <span data-ttu-id="6ae40-111">The location of that Azure IR is auto-resolve.</span><span class="sxs-lookup"><span data-stu-id="6ae40-111">The location of that Azure IR is auto-resolve.</span></span> <span data-ttu-id="6ae40-112">If **connectVia** property is not specified in the linked service definition, the default Azure IR is used.</span><span class="sxs-lookup"><span data-stu-id="6ae40-112">If **connectVia** property is not specified in the linked service definition, the default Azure IR is used.</span></span> <span data-ttu-id="6ae40-113">You only need to explicitly create an Azure IR when you would like to explicitly define the location of the IR, or if you would like to virtually group the activity executions on different IRs for management purpose.</span><span class="sxs-lookup"><span data-stu-id="6ae40-113">You only need to explicitly create an Azure IR when you would like to explicitly define the location of the IR, or if you would like to virtually group the activity executions on different IRs for management purpose.</span></span> 

## <a name="create-azure-ir"></a><span data-ttu-id="6ae40-114">Create Azure IR</span><span class="sxs-lookup"><span data-stu-id="6ae40-114">Create Azure IR</span></span>
<span data-ttu-id="6ae40-115">Integration Runtime can be created using the **Set-AzureRmDataFactoryV2IntegrationRuntime** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6ae40-115">Integration Runtime can be created using the **Set-AzureRmDataFactoryV2IntegrationRuntime** PowerShell cmdlet.</span></span> <span data-ttu-id="6ae40-116">To create an Azure IR, you specify the name, location and type to the command.</span><span class="sxs-lookup"><span data-stu-id="6ae40-116">To create an Azure IR, you specify the name, location and type to the command.</span></span> <span data-ttu-id="6ae40-117">Here is a sample command to create an Azure IR with location set to "West Europe":</span><span class="sxs-lookup"><span data-stu-id="6ae40-117">Here is a sample command to create an Azure IR with location set to "West Europe":</span></span>

```powershell
Set-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName "SampleV2DataFactory1" -Name "MySampleAzureIR" -ResourceGroupName "ADFV2SampleRG" -Type Managed -Location "West Europe"
```  
<span data-ttu-id="6ae40-118">For Azure IR, the type must be set to **Managed**.</span><span class="sxs-lookup"><span data-stu-id="6ae40-118">For Azure IR, the type must be set to **Managed**.</span></span> <span data-ttu-id="6ae40-119">You do not need to specify compute details because it is fully managed elastically in cloud.</span><span class="sxs-lookup"><span data-stu-id="6ae40-119">You do not need to specify compute details because it is fully managed elastically in cloud.</span></span> <span data-ttu-id="6ae40-120">Specify compute details like node size and node count when you would like to create Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="6ae40-120">Specify compute details like node size and node count when you would like to create Azure-SSIS IR.</span></span> <span data-ttu-id="6ae40-121">For more information, see [Create and Configure Azure-SSIS IR](create-azure-ssis-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="6ae40-121">For more information, see [Create and Configure Azure-SSIS IR](create-azure-ssis-integration-runtime.md).</span></span>

<span data-ttu-id="6ae40-122">You can configure an existing Azure IR to change its location using the Set-AzureRmDataFactoryV2IntegrationRuntime PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6ae40-122">You can configure an existing Azure IR to change its location using the Set-AzureRmDataFactoryV2IntegrationRuntime PowerShell cmdlet.</span></span> <span data-ttu-id="6ae40-123">For more information about the location of an Azure IR, see [Introduction to integration runtime](concepts-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="6ae40-123">For more information about the location of an Azure IR, see [Introduction to integration runtime](concepts-integration-runtime.md).</span></span>

## <a name="use-azure-ir"></a><span data-ttu-id="6ae40-124">Use Azure IR</span><span class="sxs-lookup"><span data-stu-id="6ae40-124">Use Azure IR</span></span>

<span data-ttu-id="6ae40-125">Once an Azure IR is created, you can reference it in your Linked Service definition.</span><span class="sxs-lookup"><span data-stu-id="6ae40-125">Once an Azure IR is created, you can reference it in your Linked Service definition.</span></span> <span data-ttu-id="6ae40-126">Below is a sample of how you can reference the Azure Integration Runtime created above from an Azure Storage Linked Service:</span><span class="sxs-lookup"><span data-stu-id="6ae40-126">Below is a sample of how you can reference the Azure Integration Runtime created above from an Azure Storage Linked Service:</span></span>  

```json
{
    "name": "MyStorageLinkedService",
    "properties": {
      "type": "AzureStorage",
      "typeProperties": {
        "connectionString": {
          "value": "DefaultEndpointsProtocol=https;AccountName=myaccountname;AccountKey=...",
          "type": "SecureString"
        }
      },
      "connectVia": {
        "referenceName": "MySampleAzureIR",
        "type": "IntegrationRuntimeReference"
      }   
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="6ae40-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ae40-127">Next steps</span></span>
<span data-ttu-id="6ae40-128">See the following articles on how to create other types of integration runtimes:</span><span class="sxs-lookup"><span data-stu-id="6ae40-128">See the following articles on how to create other types of integration runtimes:</span></span>

- [<span data-ttu-id="6ae40-129">Create self-hosted integration runtime</span><span class="sxs-lookup"><span data-stu-id="6ae40-129">Create self-hosted integration runtime</span></span>](create-self-hosted-integration-runtime.md)
- [<span data-ttu-id="6ae40-130">Create Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="6ae40-130">Create Azure-SSIS integration runtime</span></span>](create-azure-ssis-integration-runtime.md)
 
