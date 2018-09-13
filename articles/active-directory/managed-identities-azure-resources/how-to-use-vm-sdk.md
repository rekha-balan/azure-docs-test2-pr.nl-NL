---
title: How to use managed identities for Azure resources on an Azure VM with Azure SDKs
description: Code samples for using Azure SDKs with an Azure VM that has managed identities for Azure resources.
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
ms.date: 12/01/2017
ms.author: daveba
ms.openlocfilehash: 6827b01e72cd72d3f017df36205ccb985b4f242e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968675"
---
# <a name="how-to-use-managed-identities-for-azure-resources-on-an-azure-vm-with-azure-sdks"></a>How to use managed identities for Azure resources on an Azure VM with Azure SDKs 

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]  
This article provides a list of SDK samples, which demonstrate use of their respective Azure SDK's support for managed identities for Azure resources.

## <a name="prerequisites"></a>Prerequisites

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

> [!IMPORTANT]
> - All sample code/script in this article assumes the client is running on a VM with managed identities for Azure resources enabled. Use the VM "Connect" feature in the Azure portal, to remotely connect to your VM. For details on enabling managed identities for Azure resources on a VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md), or one of the variant articles (using PowerShell, CLI, a template, or an Azure SDK). 

## <a name="sdk-code-samples"></a>SDK code samples

| SDK             | Code sample |
| --------------- | ----------- |
| .NET            | [Deploy an Azure Resource Manager template from a Windows VM using managed identities for Azure resources](https://github.com/Azure-Samples/windowsvm-msi-arm-dotnet) |
| .NET Core       | [Call Azure services from a Linux VM using managed identities for Azure resources](https://github.com/Azure-Samples/linuxvm-msi-keyvault-arm-dotnet/) |
| Node.js         | [Manage resources using managed identities for Azure resources](https://azure.microsoft.com/resources/samples/resources-node-manage-resources-with-msi/) |
| Python          | [Use managed identities for Azure resources to authenticate simply from inside a VM](https://azure.microsoft.com/resources/samples/resource-manager-python-manage-resources-with-msi/) |
| Ruby            | [Manage resources from a VM with managed identities for Azure resources enabled](https://azure.microsoft.com/resources/samples/resources-ruby-manage-resources-with-msi/) |

## <a name="next-steps"></a>Next steps

- See [Azure SDKs](https://azure.microsoft.com/downloads/) for the full list of Azure SDK resources, including library downloads, documentation, and more.
- To enable managed identities for Azure resources on an Azure VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md).







