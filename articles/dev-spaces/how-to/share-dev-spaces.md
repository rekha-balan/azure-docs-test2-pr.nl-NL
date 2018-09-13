---
title: How to share Azure Dev Spaces | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: ghogen
ms.author: ghogen
ms.date: 05/11/2018
ms.topic: article
description: Rapid Kubernetes development with containers and microservices on Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
manager: douge
ms.openlocfilehash: 1d7d665c20baddb3a94bfe53568ab56a5a961630
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967535"
---
# <a name="share-azure-dev-spaces"></a><span data-ttu-id="f7734-104">Share Azure Dev Spaces</span><span class="sxs-lookup"><span data-stu-id="f7734-104">Share Azure Dev Spaces</span></span>

<span data-ttu-id="f7734-105">With Azure Dev Spaces, you can share your dev space with others on your team.</span><span class="sxs-lookup"><span data-stu-id="f7734-105">With Azure Dev Spaces, you can share your dev space with others on your team.</span></span> <span data-ttu-id="f7734-106">Each developer can work in their own space without fear of breaking others.</span><span class="sxs-lookup"><span data-stu-id="f7734-106">Each developer can work in their own space without fear of breaking others.</span></span> <span data-ttu-id="f7734-107">Also, working together in one space can enable you to test code end-to-end without having to create mocks or simulate dependencies.</span><span class="sxs-lookup"><span data-stu-id="f7734-107">Also, working together in one space can enable you to test code end-to-end without having to create mocks or simulate dependencies.</span></span> <span data-ttu-id="f7734-108">See the [Learn about team development](../team-development-nodejs.md) guide for more information.</span><span class="sxs-lookup"><span data-stu-id="f7734-108">See the [Learn about team development](../team-development-nodejs.md) guide for more information.</span></span>

## <a name="set-up-a-dev-space-for-multiple-developers"></a><span data-ttu-id="f7734-109">Set up a dev space for multiple developers</span><span class="sxs-lookup"><span data-stu-id="f7734-109">Set up a dev space for multiple developers</span></span>

1. <span data-ttu-id="f7734-110">Create a Dev Space in Azure.</span><span class="sxs-lookup"><span data-stu-id="f7734-110">Create a Dev Space in Azure.</span></span> <span data-ttu-id="f7734-111">Choose [.NET Core and VS Code](../get-started-netcore.md), [.NET Core and Visual Studio](../get-started-netcore-visualstudio.md), or [Node.js and VS Code](../get-started-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f7734-111">Choose [.NET Core and VS Code](../get-started-netcore.md), [.NET Core and Visual Studio](../get-started-netcore-visualstudio.md), or [Node.js and VS Code](../get-started-nodejs.md).</span></span> <span data-ttu-id="f7734-112">You'll need to have Owner or Contributor access to the selected Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f7734-112">You'll need to have Owner or Contributor access to the selected Azure subscription.</span></span>
1. <span data-ttu-id="f7734-113">Configure the Azure Dev Space's **resource group** to [grant Contributor access](/azure/active-directory/role-based-access-control-configure) for each team member.</span><span class="sxs-lookup"><span data-stu-id="f7734-113">Configure the Azure Dev Space's **resource group** to [grant Contributor access](/azure/active-directory/role-based-access-control-configure) for each team member.</span></span> <span data-ttu-id="f7734-114">You can check a dev space's resource group by running this command: `azds list-up`</span><span class="sxs-lookup"><span data-stu-id="f7734-114">You can check a dev space's resource group by running this command: `azds list-up`</span></span>
1. <span data-ttu-id="f7734-115">Ask team members to **select the dev space** in order to develop in it.</span><span class="sxs-lookup"><span data-stu-id="f7734-115">Ask team members to **select the dev space** in order to develop in it.</span></span>
     * <span data-ttu-id="f7734-116">**Command line or VS Code**: To see existing Azure Dev Spaces you have access to: `azds space list`.</span><span class="sxs-lookup"><span data-stu-id="f7734-116">**Command line or VS Code**: To see existing Azure Dev Spaces you have access to: `azds space list`.</span></span> <span data-ttu-id="f7734-117">To select a dev space: `azds space select`.</span><span class="sxs-lookup"><span data-stu-id="f7734-117">To select a dev space: `azds space select`.</span></span>
     * <span data-ttu-id="f7734-118">**Visual Studio IDE**: Open a project in Visual Studio, select **Azure Dev Spaces** from the launch settings drop-down.</span><span class="sxs-lookup"><span data-stu-id="f7734-118">**Visual Studio IDE**: Open a project in Visual Studio, select **Azure Dev Spaces** from the launch settings drop-down.</span></span> <span data-ttu-id="f7734-119">In the dialog that opens, select an existing cluster.</span><span class="sxs-lookup"><span data-stu-id="f7734-119">In the dialog that opens, select an existing cluster.</span></span>

    ![Visual Studio launch settings drop-down](../media/get-started-netcore-visualstudio/LaunchSettings.png)

## <a name="next-steps"></a><span data-ttu-id="f7734-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7734-121">Next steps</span></span>

<span data-ttu-id="f7734-122">See [Learn about team development](../team-development-nodejs.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="f7734-122">See [Learn about team development](../team-development-nodejs.md) for more information.</span></span>