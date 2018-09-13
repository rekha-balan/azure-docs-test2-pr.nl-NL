---
title: How to upgrade Azure Dev Spaces tools | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: ghogen
ms.author: ghogen
ms.date: 07/03/2018
ms.topic: article
ms.technology: azds-kubernetes
description: Rapid Kubernetes development with containers and microservices on Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Container Service, containers
manager: douge
ms.openlocfilehash: 10838528d79caa49abc541b4fcd38fea3c24d68f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968907"
---
# <a name="how-to-upgrade-azure-dev-spaces-tools"></a><span data-ttu-id="817d9-104">How to upgrade Azure Dev Spaces tools</span><span class="sxs-lookup"><span data-stu-id="817d9-104">How to upgrade Azure Dev Spaces tools</span></span>

<span data-ttu-id="817d9-105">If there is a new release and you are already using Azure Dev Spaces, you might need to upgrade your Azure Dev Spaces client tools.</span><span class="sxs-lookup"><span data-stu-id="817d9-105">If there is a new release and you are already using Azure Dev Spaces, you might need to upgrade your Azure Dev Spaces client tools.</span></span>

## <a name="update-the-azure-cli"></a><span data-ttu-id="817d9-106">Update the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="817d9-106">Update the Azure CLI</span></span>

<span data-ttu-id="817d9-107">When you update the latest Azure CLI, you also get the latest version of the Dev Spaces CLI extension.</span><span class="sxs-lookup"><span data-stu-id="817d9-107">When you update the latest Azure CLI, you also get the latest version of the Dev Spaces CLI extension.</span></span>

<span data-ttu-id="817d9-108">You don't need to uninstall the previous version, just find the appropriate download at [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="817d9-108">You don't need to uninstall the previous version, just find the appropriate download at [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>


## <a name="update-the-dev-spaces-cli-extension-and-command-line-tools"></a><span data-ttu-id="817d9-109">Update the Dev Spaces CLI extension and command-line tools</span><span class="sxs-lookup"><span data-stu-id="817d9-109">Update the Dev Spaces CLI extension and command-line tools</span></span>

<span data-ttu-id="817d9-110">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="817d9-110">Run the following command:</span></span>

```cmd
az aks use-dev-spaces -n <your-aks-cluster> -g <your-aks-cluster-resource-group> --update
```

## <a name="update-the-vs-code-extension"></a><span data-ttu-id="817d9-111">Update the VS Code extension</span><span class="sxs-lookup"><span data-stu-id="817d9-111">Update the VS Code extension</span></span>

<span data-ttu-id="817d9-112">Once installed, the extension updates automatically.</span><span class="sxs-lookup"><span data-stu-id="817d9-112">Once installed, the extension updates automatically.</span></span> <span data-ttu-id="817d9-113">You might need to reload the extension to use the new features.</span><span class="sxs-lookup"><span data-stu-id="817d9-113">You might need to reload the extension to use the new features.</span></span> <span data-ttu-id="817d9-114">In VS Code, open the **Extensions** pane, choose the **Azure Dev Spaces** extensions, and choose **Reload**.</span><span class="sxs-lookup"><span data-stu-id="817d9-114">In VS Code, open the **Extensions** pane, choose the **Azure Dev Spaces** extensions, and choose **Reload**.</span></span>

## <a name="update-the-visual-studio-extension"></a><span data-ttu-id="817d9-115">Update the Visual Studio extension</span><span class="sxs-lookup"><span data-stu-id="817d9-115">Update the Visual Studio extension</span></span>

<span data-ttu-id="817d9-116">Like with other extensions and updates, Visual Studio will notify you when there's an update available to the Visual Studio Tools for Kubernetes, which includes Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="817d9-116">Like with other extensions and updates, Visual Studio will notify you when there's an update available to the Visual Studio Tools for Kubernetes, which includes Azure Dev Spaces.</span></span> <span data-ttu-id="817d9-117">Look for a flag icon on the top right of the screen.</span><span class="sxs-lookup"><span data-stu-id="817d9-117">Look for a flag icon on the top right of the screen.</span></span>

<span data-ttu-id="817d9-118">To update the tools in Visual Studio, choose the **Tools > Extensions and Updates** menu item, and on the left side, choose **Updates**.</span><span class="sxs-lookup"><span data-stu-id="817d9-118">To update the tools in Visual Studio, choose the **Tools > Extensions and Updates** menu item, and on the left side, choose **Updates**.</span></span> <span data-ttu-id="817d9-119">Find **Visual Studio Tools for Kubernetes** and choose the **Update** button.</span><span class="sxs-lookup"><span data-stu-id="817d9-119">Find **Visual Studio Tools for Kubernetes** and choose the **Update** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="817d9-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="817d9-120">Next steps</span></span>

<span data-ttu-id="817d9-121">Test out the new tools by creating a new cluster.</span><span class="sxs-lookup"><span data-stu-id="817d9-121">Test out the new tools by creating a new cluster.</span></span> <span data-ttu-id="817d9-122">Try the quickstarts and tutorials at [Azure Dev Spaces](/azure/dev-spaces).</span><span class="sxs-lookup"><span data-stu-id="817d9-122">Try the quickstarts and tutorials at [Azure Dev Spaces](/azure/dev-spaces).</span></span>

> [!WARNING]
> <span data-ttu-id="817d9-123">Azure Dev Spaces on existing clusters will not be immediately patched, so to be sure you are using the most recent version on all your Azure deployments, create a new cluster after upgrading the tools.</span><span class="sxs-lookup"><span data-stu-id="817d9-123">Azure Dev Spaces on existing clusters will not be immediately patched, so to be sure you are using the most recent version on all your Azure deployments, create a new cluster after upgrading the tools.</span></span>
