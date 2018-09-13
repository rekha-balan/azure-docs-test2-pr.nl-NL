---
title: Use an Azure SDK to configure a VM with managed identities for Azure resources
description: Step by step instructions for configuring and using managed identities for Azure resources on an Azure VM, using an Azure SDK.
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
ms.date: 09/28/2017
ms.author: daveba
ms.openlocfilehash: 3b485fd0f655588ec5ae7941bcb6a43ca7728134
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855977"
---
# <a name="configure-a-vm-with-managed-identities-for-azure-resources-using-an-azure-sdk"></a><span data-ttu-id="2f545-103">Configure a VM with managed identities for Azure resources using an Azure SDK</span><span class="sxs-lookup"><span data-stu-id="2f545-103">Configure a VM with managed identities for Azure resources using an Azure SDK</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="2f545-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="2f545-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory (AD).</span></span> <span data-ttu-id="2f545-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="2f545-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="2f545-106">In this article, you learn how to enable and remove managed identities for Azure resources for an Azure VM, using an Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="2f545-106">In this article, you learn how to enable and remove managed identities for Azure resources for an Azure VM, using an Azure SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f545-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f545-107">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

## <a name="azure-sdks-with-managed-identities-for-azure-resources-support"></a><span data-ttu-id="2f545-108">Azure SDKs with managed identities for Azure resources support</span><span class="sxs-lookup"><span data-stu-id="2f545-108">Azure SDKs with managed identities for Azure resources support</span></span> 

<span data-ttu-id="2f545-109">Azure supports multiple programming platforms through a series of [Azure SDKs](https://azure.microsoft.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="2f545-109">Azure supports multiple programming platforms through a series of [Azure SDKs](https://azure.microsoft.com/downloads).</span></span> <span data-ttu-id="2f545-110">Several of them have been updated to support managed identities for Azure resources, and provide corresponding samples to demonstrate usage.</span><span class="sxs-lookup"><span data-stu-id="2f545-110">Several of them have been updated to support managed identities for Azure resources, and provide corresponding samples to demonstrate usage.</span></span> <span data-ttu-id="2f545-111">This list is updated as additional support is added:</span><span class="sxs-lookup"><span data-stu-id="2f545-111">This list is updated as additional support is added:</span></span>

| <span data-ttu-id="2f545-112">SDK</span><span class="sxs-lookup"><span data-stu-id="2f545-112">SDK</span></span> | <span data-ttu-id="2f545-113">Sample</span><span class="sxs-lookup"><span data-stu-id="2f545-113">Sample</span></span> |
| --- | ------ | 
| <span data-ttu-id="2f545-114">.NET</span><span class="sxs-lookup"><span data-stu-id="2f545-114">.NET</span></span>   | [<span data-ttu-id="2f545-115">Manage resource from a VM enabled with managed identities for Azure resources enabled</span><span class="sxs-lookup"><span data-stu-id="2f545-115">Manage resource from a VM enabled with managed identities for Azure resources enabled</span></span>](https://azure.microsoft.com/resources/samples/aad-dotnet-manage-resources-from-vm-with-msi/) |
| <span data-ttu-id="2f545-116">Java</span><span class="sxs-lookup"><span data-stu-id="2f545-116">Java</span></span>   | [<span data-ttu-id="2f545-117">Manage storage from a VM enabled with managed identities for Azure resources</span><span class="sxs-lookup"><span data-stu-id="2f545-117">Manage storage from a VM enabled with managed identities for Azure resources</span></span>](https://azure.microsoft.com/resources/samples/compute-java-manage-resources-from-vm-with-msi-in-aad-group/)|
| <span data-ttu-id="2f545-118">Node.js</span><span class="sxs-lookup"><span data-stu-id="2f545-118">Node.js</span></span>| [<span data-ttu-id="2f545-119">Create a VM with system-assigned managed identity enabled</span><span class="sxs-lookup"><span data-stu-id="2f545-119">Create a VM with system-assigned managed identity enabled</span></span>](https://azure.microsoft.com/resources/samples/compute-node-msi-vm/) |
| <span data-ttu-id="2f545-120">Python</span><span class="sxs-lookup"><span data-stu-id="2f545-120">Python</span></span> | [<span data-ttu-id="2f545-121">Create a VM with system-assigned managed identity enabled</span><span class="sxs-lookup"><span data-stu-id="2f545-121">Create a VM with system-assigned managed identity enabled</span></span>](https://azure.microsoft.com/resources/samples/compute-python-msi-vm/) |
| <span data-ttu-id="2f545-122">Ruby</span><span class="sxs-lookup"><span data-stu-id="2f545-122">Ruby</span></span>   | [<span data-ttu-id="2f545-123">Create Azure VM with an system-assigned identity enabled</span><span class="sxs-lookup"><span data-stu-id="2f545-123">Create Azure VM with an system-assigned identity enabled</span></span>](https://azure.microsoft.com/resources/samples/compute-ruby-msi-vm/) |

## <a name="next-steps"></a><span data-ttu-id="2f545-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f545-124">Next steps</span></span>

- <span data-ttu-id="2f545-125">See related articles under **Configure Identity for an Azure VM**, to learn how you can also use the Azure portal, PowerShell, CLI, and resource templates.</span><span class="sxs-lookup"><span data-stu-id="2f545-125">See related articles under **Configure Identity for an Azure VM**, to learn how you can also use the Azure portal, PowerShell, CLI, and resource templates.</span></span>
