---
title: Azure Government Security + Identity | Microsoft Docs
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: ryansoc
manager: zakramer
ms.assetid: e2fe7983-5870-43e9-ae01-2d45d3102c8a
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 11/14/2016
ms.author: ryansoc
ms.openlocfilehash: 2c3a3eec41dfb6860eb680694023b82099290b7f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550049"
---
# <a name="azure-government-security--identity"></a><span data-ttu-id="227a8-103">Azure Government Security + Identity</span><span class="sxs-lookup"><span data-stu-id="227a8-103">Azure Government Security + Identity</span></span>
## <a name="key-vault"></a><span data-ttu-id="227a8-104">Key Vault</span><span class="sxs-lookup"><span data-stu-id="227a8-104">Key Vault</span></span>
<span data-ttu-id="227a8-105">For details on this service and how to use it, see the [Azure Key Vault public documentation](../key-vault/index.md).</span><span class="sxs-lookup"><span data-stu-id="227a8-105">For details on this service and how to use it, see the [Azure Key Vault public documentation](../key-vault/index.md).</span></span>

### <a name="data-considerations"></a><span data-ttu-id="227a8-106">Data Considerations</span><span class="sxs-lookup"><span data-stu-id="227a8-106">Data Considerations</span></span>
<span data-ttu-id="227a8-107">The following information identifies the Azure Government boundary for Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="227a8-107">The following information identifies the Azure Government boundary for Azure Key Vault:</span></span>

| <span data-ttu-id="227a8-108">Regulated/controlled data permitted</span><span class="sxs-lookup"><span data-stu-id="227a8-108">Regulated/controlled data permitted</span></span> | <span data-ttu-id="227a8-109">Regulated/controlled data not permitted</span><span class="sxs-lookup"><span data-stu-id="227a8-109">Regulated/controlled data not permitted</span></span> |
| --- | --- |
| <span data-ttu-id="227a8-110">All data encrypted with an Azure Key Vault key may contain Regulated/controlled data.</span><span class="sxs-lookup"><span data-stu-id="227a8-110">All data encrypted with an Azure Key Vault key may contain Regulated/controlled data.</span></span> |<span data-ttu-id="227a8-111">Azure Key Vault metadata is not permitted to contain export controlled data.</span><span class="sxs-lookup"><span data-stu-id="227a8-111">Azure Key Vault metadata is not permitted to contain export controlled data.</span></span> <span data-ttu-id="227a8-112">This metadata includes all configuration data entered when creating and maintaining your Key Vault.</span><span class="sxs-lookup"><span data-stu-id="227a8-112">This metadata includes all configuration data entered when creating and maintaining your Key Vault.</span></span>  <span data-ttu-id="227a8-113">Do not enter Regulated/controlled data into the following fields: Resource group names, Key Vault names, Subscription name</span><span class="sxs-lookup"><span data-stu-id="227a8-113">Do not enter Regulated/controlled data into the following fields: Resource group names, Key Vault names, Subscription name</span></span> |

<span data-ttu-id="227a8-114">Key Vault is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="227a8-114">Key Vault is generally available in Azure Government.</span></span> <span data-ttu-id="227a8-115">As in public, there is no extension, so Key Vault is available through PowerShell and CLI only.</span><span class="sxs-lookup"><span data-stu-id="227a8-115">As in public, there is no extension, so Key Vault is available through PowerShell and CLI only.</span></span>

## <a name="next-steps"></a><span data-ttu-id="227a8-116">Next Steps</span><span class="sxs-lookup"><span data-stu-id="227a8-116">Next Steps</span></span>
<span data-ttu-id="227a8-117">For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span><span class="sxs-lookup"><span data-stu-id="227a8-117">For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span></span>

