---
title: How to assign an MSI access to an Azure resource, using Azure CLI
description: Step by step instructions for assigning an MSI on one resource, access to another resource, using Azure CLI.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/25/2017
ms.author: daveba
ms.openlocfilehash: f46475dfc74212a01b70d487c04d6cd54ca4ca2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866252"
---
# <a name="assign-a-managed-service-identity-msi-access-to-a-resource-using-azure-cli"></a>Assign a Managed Service Identity (MSI) access to a resource using Azure CLI

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

Once you've configured an Azure resource with an MSI, you can give the MSI access to another resource, just like any security principal. This example shows you how to give an Azure virtual machine or virtual machine scale set's MSI access to an Azure storage account, using Azure CLI.

## <a name="prerequisites"></a>Prerequisites

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

To run the CLI script examples, you have three options:

- Use [Azure Cloud Shell](../../cloud-shell/overview.md) from the Azure portal (see next section).
- Use the embedded Azure Cloud Shell via the "Try It" button, located in the top right corner of each code block.
- [Install the latest version of CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0.13 or later) if you prefer to use a local CLI console. 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="use-rbac-to-assign-the-msi-access-to-another-resource"></a>Use RBAC to assign the MSI access to another resource

After you've enabled MSI on an Azure resource, such as an [Azure virtual machine](qs-configure-cli-windows-vm.md) or [Azure virtual machine scale set](qs-configure-cli-windows-vmss.md): 

1. If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login). Use an account that is associated with the Azure subscription under which you would like to deploy the VM or virtual machine scale set:

   ```azurecli-interactive
   az login
   ```

2. In this example, we are giving an Azure virtual machine access to a storage account. First we use [az resource list](/cli/azure/resource/#az-resource-list) to get the service principal for the virtual machine named "myVM":

   ```azurecli-interactive
   spID=$(az resource list -n myVM --query [*].identity.principalId --out tsv)
   ```
   For an Azure virtual machine scale set, the command is the same except here, you get the service principal for the virtual machine scale set named "DevTestVMSS":
   
   ```azurecli-interactive
   spID=$(az resource list -n DevTestVMSS --query [*].identity.principalId --out tsv)
   ```

3. Once you have the service principal ID, use [az role assignment create](/cli/azure/role/assignment#az-role-assignment-create) to give the virtual machine or virtual machine scale set "Reader" access to a storage account called "myStorageAcct":

   ```azurecli-interactive
   az role assignment create --assignee $spID --role 'Reader' --scope /subscriptions/<mySubscriptionID>/resourceGroups/<myResourceGroup>/providers/Microsoft.Storage/storageAccounts/myStorageAcct
   ```

## <a name="troubleshooting"></a>Troubleshooting

If the MSI for the resource does not show up in the list of available identities, verify that the MSI has been enabled correctly. In our case, we can go back to the Azure virtual machine or virtual machine scale set in the [Azure portal](https://portal.azure.com) and:

- Look at the "Configuration" page and ensure MSI enabled = "Yes."
- Look at the "Extensions" page and ensure the MSI extension deployed successfully (**Extensions** page is not available for an Azure virtual machine scale set).

If either is incorrect, you may need to redeploy the MSI on your resource again, or troubleshoot the deployment failure.

## <a name="related-content"></a>Related content

- For an overview of MSI, see [Managed Service Identity overview](overview.md).
- To enable MSI on an Azure virtual machine, see [Configure an Azure VM Managed Service Identity (MSI) using Azure CLI](qs-configure-cli-windows-vm.md).
- To enable MSI on an Azure virtual machine scale set, see [Configure an Azure Virtual Machine Scale Set Managed Service Identity (MSI) using the Azure portal](qs-configure-portal-windows-vmss.md)

Use the following comments section to provide feedback and help us refine and shape our content.

