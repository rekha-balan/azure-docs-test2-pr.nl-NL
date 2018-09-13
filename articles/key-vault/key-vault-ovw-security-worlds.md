---
ms.assetid: ''
title: Azure Key Vault security worlds | Microsoft Docs
ms.service: key-vault
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 7fd7357a317d5059d6169de2c1536568a254e016
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866775"
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="e1dcc-102">Azure Key Vault security worlds and geographic boundaries</span><span class="sxs-lookup"><span data-stu-id="e1dcc-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="e1dcc-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span><span class="sxs-lookup"><span data-stu-id="e1dcc-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="e1dcc-104">All HSMs at Azure locations in the same geographic region share the same cryptographic boundary (Thales Security World).</span><span class="sxs-lookup"><span data-stu-id="e1dcc-104">All HSMs at Azure locations in the same geographic region share the same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="e1dcc-105">For example, East US and West US share the same security world because they belong to the US geo location.</span><span class="sxs-lookup"><span data-stu-id="e1dcc-105">For example, East US and West US share the same security world because they belong to the US geo location.</span></span> <span data-ttu-id="e1dcc-106">Similarly, all Azure locations in Japan share the same security world and all Azure locations in Australia, India, and so on.</span><span class="sxs-lookup"><span data-stu-id="e1dcc-106">Similarly, all Azure locations in Japan share the same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="e1dcc-107">Backup and restore behavior</span><span class="sxs-lookup"><span data-stu-id="e1dcc-107">Backup and restore behavior</span></span>

<span data-ttu-id="e1dcc-108">A backup taken of a key from a key vault in one Azure location can be restored to a key vault in another Azure location, as long as both of these conditions are true:</span><span class="sxs-lookup"><span data-stu-id="e1dcc-108">A backup taken of a key from a key vault in one Azure location can be restored to a key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="e1dcc-109">Both of the Azure locations belong to the same geographical location</span><span class="sxs-lookup"><span data-stu-id="e1dcc-109">Both of the Azure locations belong to the same geographical location</span></span>
- <span data-ttu-id="e1dcc-110">Both of the key vaults belong to the same Azure subscription</span><span class="sxs-lookup"><span data-stu-id="e1dcc-110">Both of the key vaults belong to the same Azure subscription</span></span>

<span data-ttu-id="e1dcc-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored to another key vault in the same subscription and geo location; West India, Central India or South India.</span><span class="sxs-lookup"><span data-stu-id="e1dcc-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored to another key vault in the same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="e1dcc-112">Regions and products</span><span class="sxs-lookup"><span data-stu-id="e1dcc-112">Regions and products</span></span>

- [<span data-ttu-id="e1dcc-113">Azure regions</span><span class="sxs-lookup"><span data-stu-id="e1dcc-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="e1dcc-114">Microsoft products by region</span><span class="sxs-lookup"><span data-stu-id="e1dcc-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="e1dcc-115">Regions are mapped to security worlds, shown as major headings in the tables:</span><span class="sxs-lookup"><span data-stu-id="e1dcc-115">Regions are mapped to security worlds, shown as major headings in the tables:</span></span>

<span data-ttu-id="e1dcc-116">In the products by region article, for example, the **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping to the Americas region.</span><span class="sxs-lookup"><span data-stu-id="e1dcc-116">In the products by region article, for example, the **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping to the Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="e1dcc-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span><span class="sxs-lookup"><span data-stu-id="e1dcc-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="e1dcc-118">Similarly, on the **Europe** tab, NORTH EUROPE and WEST EUROPE both map to the Europe region.</span><span class="sxs-lookup"><span data-stu-id="e1dcc-118">Similarly, on the **Europe** tab, NORTH EUROPE and WEST EUROPE both map to the Europe region.</span></span> <span data-ttu-id="e1dcc-119">The same is also true on the **Asia Pacific** tab.</span><span class="sxs-lookup"><span data-stu-id="e1dcc-119">The same is also true on the **Asia Pacific** tab.</span></span>



