---
title: How to create and delete a user-assigned managed identity using Azure Resource Manager
description: Step by step instructions on how to create and delete user-assigned managed identities using Azure Resource Manager.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/16/2018
ms.author: daveba
ms.openlocfilehash: 9e1ea4e35c1d8b90aa3d0fdf5e619f7b7f7db400
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858041"
---
# <a name="create-list-and-delete-a-user-assigned-managed-identity-using-azure-resource-manager"></a><span data-ttu-id="d5180-103">Create, list and delete a user-assigned managed identity using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d5180-103">Create, list and delete a user-assigned managed identity using Azure Resource Manager</span></span>

[!INCLUDE [preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

<span data-ttu-id="d5180-104">Managed identities for Azure resources provides Azure services with a managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5180-104">Managed identities for Azure resources provides Azure services with a managed identity in Azure Active Directory.</span></span> <span data-ttu-id="d5180-105">You can use this identity to authenticate to services that support Azure AD authentication, without needing credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="d5180-105">You can use this identity to authenticate to services that support Azure AD authentication, without needing credentials in your code.</span></span> 

<span data-ttu-id="d5180-106">In this article, you create a user-assigned managed identity using an Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d5180-106">In this article, you create a user-assigned managed identity using an Azure Resource Manager.</span></span>

<span data-ttu-id="d5180-107">It is not possible to list and delete a user-assigned managed identity using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="d5180-107">It is not possible to list and delete a user-assigned managed identity using an Azure Resource Manager template.</span></span>  <span data-ttu-id="d5180-108">See the following articles to create and list a user-assigned managed identity:</span><span class="sxs-lookup"><span data-stu-id="d5180-108">See the following articles to create and list a user-assigned managed identity:</span></span>

- [<span data-ttu-id="d5180-109">List user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="d5180-109">List user-assigned managed identity</span></span>](how-to-manage-ua-identity-cli.md#list-user-assigned-managed-identities)
- [<span data-ttu-id="d5180-110">Delete user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="d5180-110">Delete user-assigned managed identity</span></span>](how-to-manage-ua-identity-cli.md#delete-a-user-assigned-managed-identity)
## <a name="prerequisites"></a><span data-ttu-id="d5180-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d5180-111">Prerequisites</span></span>

- <span data-ttu-id="d5180-112">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5180-112">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span> <span data-ttu-id="d5180-113">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="d5180-113">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="d5180-114">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="d5180-114">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="d5180-115">To perform the operations in this article, your account needs the following role assignment:</span><span class="sxs-lookup"><span data-stu-id="d5180-115">To perform the operations in this article, your account needs the following role assignment:</span></span>
    - <span data-ttu-id="d5180-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create, read (list), update, and delete a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="d5180-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create, read (list), update, and delete a user-assigned managed identity.</span></span>

## <a name="template-creation-and-editing"></a><span data-ttu-id="d5180-117">Template creation and editing</span><span class="sxs-lookup"><span data-stu-id="d5180-117">Template creation and editing</span></span>

<span data-ttu-id="d5180-118">As with the Azure portal and scripting, Azure Resource Manager templates provide the ability to deploy new or modified resources defined by an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="d5180-118">As with the Azure portal and scripting, Azure Resource Manager templates provide the ability to deploy new or modified resources defined by an Azure resource group.</span></span> <span data-ttu-id="d5180-119">Several options are available for template editing and deployment, both local and portal-based, including:</span><span class="sxs-lookup"><span data-stu-id="d5180-119">Several options are available for template editing and deployment, both local and portal-based, including:</span></span>

- <span data-ttu-id="d5180-120">Using a [custom template from the Azure Marketplace](../../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template), which allows you to create a template from scratch, or base it on an existing common or [QuickStart template](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="d5180-120">Using a [custom template from the Azure Marketplace](../../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template), which allows you to create a template from scratch, or base it on an existing common or [QuickStart template](https://azure.microsoft.com/documentation/templates/).</span></span>
- <span data-ttu-id="d5180-121">Deriving from an existing resource group, by exporting a template from either [the original deployment](../../azure-resource-manager/resource-manager-export-template.md#view-template-from-deployment-history), or from the [current state of the deployment](../../azure-resource-manager/resource-manager-export-template.md#export-the-template-from-resource-group).</span><span class="sxs-lookup"><span data-stu-id="d5180-121">Deriving from an existing resource group, by exporting a template from either [the original deployment](../../azure-resource-manager/resource-manager-export-template.md#view-template-from-deployment-history), or from the [current state of the deployment](../../azure-resource-manager/resource-manager-export-template.md#export-the-template-from-resource-group).</span></span>
- <span data-ttu-id="d5180-122">Using a local [JSON editor (such as VS Code)](../../azure-resource-manager/resource-manager-create-first-template.md), and then uploading and deploying by using PowerShell or CLI.</span><span class="sxs-lookup"><span data-stu-id="d5180-122">Using a local [JSON editor (such as VS Code)](../../azure-resource-manager/resource-manager-create-first-template.md), and then uploading and deploying by using PowerShell or CLI.</span></span>
- <span data-ttu-id="d5180-123">Using the Visual Studio [Azure Resource Group project](../../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) to both create and deploy a template.</span><span class="sxs-lookup"><span data-stu-id="d5180-123">Using the Visual Studio [Azure Resource Group project](../../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) to both create and deploy a template.</span></span> 

## <a name="create-a-user-assigned-managed-identity"></a><span data-ttu-id="d5180-124">Create a user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="d5180-124">Create a user-assigned managed identity</span></span> 

<span data-ttu-id="d5180-125">To create a user-assigned managed identity, use the following template.</span><span class="sxs-lookup"><span data-stu-id="d5180-125">To create a user-assigned managed identity, use the following template.</span></span> <span data-ttu-id="d5180-126">Replace the `<USER ASSIGNED IDENTITY NAME>` value with your own values:</span><span class="sxs-lookup"><span data-stu-id="d5180-126">Replace the `<USER ASSIGNED IDENTITY NAME>` value with your own values:</span></span>

[!INCLUDE [ua-character-limit](~/includes/managed-identity-ua-character-limits.md)]

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "resourceName": {
          "type": "string",
          "metadata": {
            "description": "<USER ASSIGNED IDENTITY NAME>"
          }
        }
  },
  "resources": [
    {
      "type": "Microsoft.ManagedIdentity/userAssignedIdentities",
      "name": "[parameters('resourceName')]",
      "apiVersion": "2015-08-31-PREVIEW",
      "location": "[resourceGroup().location]"
    }
  ],
  "outputs": {
      "identityName": {
          "type": "string",
          "value": "[parameters('resourceName')]"
      }
  }
}
```
## <a name="next-steps"></a><span data-ttu-id="d5180-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5180-127">Next steps</span></span>

<span data-ttu-id="d5180-128">For information on how to assign a user-assigned managed identity to an Azure VM using an Azure Resource Manager template see, [Configure managed identities for Azure resources on an Azure VM using a templates](qs-configure-template-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="d5180-128">For information on how to assign a user-assigned managed identity to an Azure VM using an Azure Resource Manager template see, [Configure managed identities for Azure resources on an Azure VM using a templates](qs-configure-template-windows-vm.md).</span></span>


 
