---
title: Azure PowerShell script sample - Deploy a managed application | Microsoft Docs
description: Azure PowerShell script sample - Deploy a managed application definition
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
ms.service: managed-applications
ms.devlang: powershell
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2017
ms.author: tomfitz
ms.openlocfilehash: 2429d561beffed5bc171b9dbc2c2c9c88eba3313
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856403"
---
# <a name="deploy-a-managed-application-for-a-service-catalog-with-powershell"></a><span data-ttu-id="a27d8-103">Deploy a managed application for a service catalog with PowerShell</span><span class="sxs-lookup"><span data-stu-id="a27d8-103">Deploy a managed application for a service catalog with PowerShell</span></span>

<span data-ttu-id="a27d8-104">This script deploys a managed application definition from the service catalog.</span><span class="sxs-lookup"><span data-stu-id="a27d8-104">This script deploys a managed application definition from the service catalog.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a27d8-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="a27d8-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/managed-applications/create-application/create-application.ps1 "Create application")]


## <a name="script-explanation"></a><span data-ttu-id="a27d8-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="a27d8-106">Script explanation</span></span>

<span data-ttu-id="a27d8-107">This script uses the following command to deploy the managed application.</span><span class="sxs-lookup"><span data-stu-id="a27d8-107">This script uses the following command to deploy the managed application.</span></span> <span data-ttu-id="a27d8-108">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="a27d8-108">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="a27d8-109">Command</span><span class="sxs-lookup"><span data-stu-id="a27d8-109">Command</span></span> | <span data-ttu-id="a27d8-110">Notes</span><span class="sxs-lookup"><span data-stu-id="a27d8-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a27d8-111">New-AzureRmManagedApplication</span><span class="sxs-lookup"><span data-stu-id="a27d8-111">New-AzureRmManagedApplication</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermmanagedapplication) | <span data-ttu-id="a27d8-112">Create a managed application.</span><span class="sxs-lookup"><span data-stu-id="a27d8-112">Create a managed application.</span></span> <span data-ttu-id="a27d8-113">Provide the definition ID and parameters for the template.</span><span class="sxs-lookup"><span data-stu-id="a27d8-113">Provide the definition ID and parameters for the template.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="a27d8-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="a27d8-114">Next steps</span></span>

* <span data-ttu-id="a27d8-115">For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="a27d8-115">For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).</span></span>
* <span data-ttu-id="a27d8-116">For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="a27d8-116">For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span></span>
