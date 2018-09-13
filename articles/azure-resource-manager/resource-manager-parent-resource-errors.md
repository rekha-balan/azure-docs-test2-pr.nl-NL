---
title: Azure parent resource errors | Microsoft Docs
description: Describes how to resolve errors when working with a parent resource.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 08/01/2018
ms.author: tomfitz
ms.openlocfilehash: 3042ea1a523f12ae0311545a1b9bc67306f266dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871136"
---
# <a name="resolve-errors-for-parent-resources"></a><span data-ttu-id="28934-103">Resolve errors for parent resources</span><span class="sxs-lookup"><span data-stu-id="28934-103">Resolve errors for parent resources</span></span>

<span data-ttu-id="28934-104">This article describes the errors you may get when deploying a resource that is dependent on a parent resource.</span><span class="sxs-lookup"><span data-stu-id="28934-104">This article describes the errors you may get when deploying a resource that is dependent on a parent resource.</span></span>

## <a name="symptom"></a><span data-ttu-id="28934-105">Symptom</span><span class="sxs-lookup"><span data-stu-id="28934-105">Symptom</span></span>

<span data-ttu-id="28934-106">When deploying a resource that is a child to another resource, you may receive the following error:</span><span class="sxs-lookup"><span data-stu-id="28934-106">When deploying a resource that is a child to another resource, you may receive the following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

## <a name="cause"></a><span data-ttu-id="28934-107">Cause</span><span class="sxs-lookup"><span data-stu-id="28934-107">Cause</span></span>

<span data-ttu-id="28934-108">When one resource is a child to another resource, the parent resource must exist before creating the child resource.</span><span class="sxs-lookup"><span data-stu-id="28934-108">When one resource is a child to another resource, the parent resource must exist before creating the child resource.</span></span> <span data-ttu-id="28934-109">The name of the child resource defines the connection with the parent resource.</span><span class="sxs-lookup"><span data-stu-id="28934-109">The name of the child resource defines the connection with the parent resource.</span></span> <span data-ttu-id="28934-110">The name of the child resource is in the format `<parent-resource-name>/<child-resource-name>`.</span><span class="sxs-lookup"><span data-stu-id="28934-110">The name of the child resource is in the format `<parent-resource-name>/<child-resource-name>`.</span></span> <span data-ttu-id="28934-111">For example, a SQL Database might be defined as:</span><span class="sxs-lookup"><span data-stu-id="28934-111">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="28934-112">If you deploy both the server and the database in the same template, but don't specify a dependency on the server, the database deployment might start before the server has deployed.</span><span class="sxs-lookup"><span data-stu-id="28934-112">If you deploy both the server and the database in the same template, but don't specify a dependency on the server, the database deployment might start before the server has deployed.</span></span> 

<span data-ttu-id="28934-113">If the parent resource already exists and isn't deployed in the same template, you get this error when Resource Manager can't associate the child resource with parent.</span><span class="sxs-lookup"><span data-stu-id="28934-113">If the parent resource already exists and isn't deployed in the same template, you get this error when Resource Manager can't associate the child resource with parent.</span></span> <span data-ttu-id="28934-114">This error might happen when the child resource isn't in the correct format, or the child resource is deployed to a resource group that is different than the resource group for parent resource.</span><span class="sxs-lookup"><span data-stu-id="28934-114">This error might happen when the child resource isn't in the correct format, or the child resource is deployed to a resource group that is different than the resource group for parent resource.</span></span>

## <a name="solution"></a><span data-ttu-id="28934-115">Solution</span><span class="sxs-lookup"><span data-stu-id="28934-115">Solution</span></span>

<span data-ttu-id="28934-116">To resolve this error when parent and child resources are deployed in the same template, include a dependency.</span><span class="sxs-lookup"><span data-stu-id="28934-116">To resolve this error when parent and child resources are deployed in the same template, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<span data-ttu-id="28934-117">To resolve this error when the parent resource was previously deployed in a different template, you don't set a dependency.</span><span class="sxs-lookup"><span data-stu-id="28934-117">To resolve this error when the parent resource was previously deployed in a different template, you don't set a dependency.</span></span> <span data-ttu-id="28934-118">Instead, deploy the child to the same resource group and provide the name of the parent resource.</span><span class="sxs-lookup"><span data-stu-id="28934-118">Instead, deploy the child to the same resource group and provide the name of the parent resource.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "sqlServerName": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        }
    },
    "resources": [
        {
            "apiVersion": "2014-04-01",
            "type": "Microsoft.Sql/servers/databases",
            "location": "[resourceGroup().location]",
            "name": "[concat(parameters('sqlServerName'), '/', parameters('databaseName'))]",
            "properties": {
                "collation": "SQL_Latin1_General_CP1_CI_AS",
                "edition": "Basic"
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="28934-119">For more information, see [Define the order for deploying resources in Azure Resource Manager templates](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="28934-119">For more information, see [Define the order for deploying resources in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span>