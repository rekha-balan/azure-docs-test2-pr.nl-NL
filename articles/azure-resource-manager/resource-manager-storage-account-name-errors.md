---
title: Azure storage account name errors | Microsoft Docs
description: Describes the errors you may encounter when specifying a storage account name.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 03/09/2018
ms.author: tomfitz
ms.openlocfilehash: da7147439bba668c6c614c19d91a22ee78275c69
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868311"
---
# <a name="resolve-errors-for-storage-account-names"></a><span data-ttu-id="e5226-103">Resolve errors for storage account names</span><span class="sxs-lookup"><span data-stu-id="e5226-103">Resolve errors for storage account names</span></span>

<span data-ttu-id="e5226-104">This article describes naming errors you may encounter when deploying a storage account.</span><span class="sxs-lookup"><span data-stu-id="e5226-104">This article describes naming errors you may encounter when deploying a storage account.</span></span>

## <a name="symptom"></a><span data-ttu-id="e5226-105">Symptom</span><span class="sxs-lookup"><span data-stu-id="e5226-105">Symptom</span></span>

<span data-ttu-id="e5226-106">If your storage account name includes prohibited characters, you receive an error like:</span><span class="sxs-lookup"><span data-stu-id="e5226-106">If your storage account name includes prohibited characters, you receive an error like:</span></span>

```
Code=AccountNameInvalid
Message=S!torageckrexph7isnoc is not a valid storage account name. Storage account name must be 
between 3 and 24 characters in length and use numbers and lower-case letters only.
```

<span data-ttu-id="e5226-107">For storage accounts, you must provide a name for the resource that is unique across Azure.</span><span class="sxs-lookup"><span data-stu-id="e5226-107">For storage accounts, you must provide a name for the resource that is unique across Azure.</span></span> <span data-ttu-id="e5226-108">If you do not provide a unique name, you receive an error like:</span><span class="sxs-lookup"><span data-stu-id="e5226-108">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

<span data-ttu-id="e5226-109">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span><span class="sxs-lookup"><span data-stu-id="e5226-109">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span></span> <span data-ttu-id="e5226-110">Either delete the existing storage account, or provide the same location as the existing storage account.</span><span class="sxs-lookup"><span data-stu-id="e5226-110">Either delete the existing storage account, or provide the same location as the existing storage account.</span></span>

## <a name="cause"></a><span data-ttu-id="e5226-111">Cause</span><span class="sxs-lookup"><span data-stu-id="e5226-111">Cause</span></span>

<span data-ttu-id="e5226-112">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span><span class="sxs-lookup"><span data-stu-id="e5226-112">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="e5226-113">The name must be unique.</span><span class="sxs-lookup"><span data-stu-id="e5226-113">The name must be unique.</span></span>

## <a name="solution"></a><span data-ttu-id="e5226-114">Solution</span><span class="sxs-lookup"><span data-stu-id="e5226-114">Solution</span></span>

<span data-ttu-id="e5226-115">Make sure the storage account name is unique.</span><span class="sxs-lookup"><span data-stu-id="e5226-115">Make sure the storage account name is unique.</span></span> <span data-ttu-id="e5226-116">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span><span class="sxs-lookup"><span data-stu-id="e5226-116">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="e5226-117">Make sure your storage account name does not exceed 24 characters.</span><span class="sxs-lookup"><span data-stu-id="e5226-117">Make sure your storage account name does not exceed 24 characters.</span></span> <span data-ttu-id="e5226-118">The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span><span class="sxs-lookup"><span data-stu-id="e5226-118">The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="e5226-119">If you concatenate a prefix or postfix to the **uniqueString** result, provide a value that is 11 characters or less.</span><span class="sxs-lookup"><span data-stu-id="e5226-119">If you concatenate a prefix or postfix to the **uniqueString** result, provide a value that is 11 characters or less.</span></span>

```json
"parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name."
      }
    }
}
```

<span data-ttu-id="e5226-120">Make sure your storage account name does not include any upper-case letters or special characters.</span><span class="sxs-lookup"><span data-stu-id="e5226-120">Make sure your storage account name does not include any upper-case letters or special characters.</span></span>