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
# <a name="resolve-errors-for-storage-account-names"></a>Resolve errors for storage account names

This article describes naming errors you may encounter when deploying a storage account.

## <a name="symptom"></a>Symptom

If your storage account name includes prohibited characters, you receive an error like:

```
Code=AccountNameInvalid
Message=S!torageckrexph7isnoc is not a valid storage account name. Storage account name must be 
between 3 and 24 characters in length and use numbers and lower-case letters only.
```

For storage accounts, you must provide a name for the resource that is unique across Azure. If you do not provide a unique name, you receive an error like:

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location. Either delete the existing storage account, or provide the same location as the existing storage account.

## <a name="cause"></a>Cause

Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only. The name must be unique.

## <a name="solution"></a>Solution

Make sure the storage account name is unique. You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

Make sure your storage account name does not exceed 24 characters. The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters. If you concatenate a prefix or postfix to the **uniqueString** result, provide a value that is 11 characters or less.

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

Make sure your storage account name does not include any upper-case letters or special characters.