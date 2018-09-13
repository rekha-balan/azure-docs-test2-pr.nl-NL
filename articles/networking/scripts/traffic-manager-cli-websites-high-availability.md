---
title: Azure CLI Script Sample - Route traffic for high availability of applications | Microsoft Docs
description: Azure CLI Script Sample - Route traffic for high availability of applications
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: ''
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 06/26/2018
ms.author: kumud
ms.openlocfilehash: 48d265cd42954018d3482b74daf64ccf4d1b40cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965448"
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="d8d4e-103">Route traffic for high availability of applications</span><span class="sxs-lookup"><span data-stu-id="d8d4e-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="d8d4e-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="d8d4e-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="d8d4e-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="d8d4e-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d8d4e-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="d8d4e-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="d8d4e-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="d8d4e-109">Clean up deployment</span></span> 

<span data-ttu-id="d8d4e-110">After the script sample has been run, the follow command can be used to remove the resource group, App Service app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-110">After the script sample has been run, the follow command can be used to remove the resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d8d4e-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="d8d4e-111">Script explanation</span></span>

<span data-ttu-id="d8d4e-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="d8d4e-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d8d4e-114">Command</span><span class="sxs-lookup"><span data-stu-id="d8d4e-114">Command</span></span> | <span data-ttu-id="d8d4e-115">Notes</span><span class="sxs-lookup"><span data-stu-id="d8d4e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d8d4e-116">az group create</span><span class="sxs-lookup"><span data-stu-id="d8d4e-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az_group_create) | <span data-ttu-id="d8d4e-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d8d4e-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="d8d4e-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#az_appservice_plan_create) | <span data-ttu-id="d8d4e-119">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-119">Creates an App Service plan.</span></span> <span data-ttu-id="d8d4e-120">This is like a server farm for your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="d8d4e-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="d8d4e-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="d8d4e-122">Creates an Azure web app within the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-122">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="d8d4e-123">az network traffic-manager profile create</span><span class="sxs-lookup"><span data-stu-id="d8d4e-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#az_network_traffic_manager_profile_create) | <span data-ttu-id="d8d4e-124">Creates an Azure Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="d8d4e-125">az network traffic-manager endpoint create</span><span class="sxs-lookup"><span data-stu-id="d8d4e-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#az_network_traffic_manager_endpoint_create) | <span data-ttu-id="d8d4e-126">Adds a endpoint to an Azure Traffic Manager Profile.</span><span class="sxs-lookup"><span data-stu-id="d8d4e-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d8d4e-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8d4e-127">Next steps</span></span>

<span data-ttu-id="d8d4e-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="d8d4e-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="d8d4e-129">Additional App Service CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d8d4e-129">Additional App Service CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>
