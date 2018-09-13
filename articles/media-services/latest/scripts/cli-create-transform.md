---
title: Azure CLI Script Example - Create a transform | Microsoft Docs
description: Use the Azure CLI script to create a Transform.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: media-services
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/11/2018
ms.author: juliako
ms.openlocfilehash: cbe20c4b75fff27fad60446fb933a9c8ba2e3312
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865916"
---
# <a name="cli-example-create-a-transform"></a><span data-ttu-id="38ad7-103">CLI example: Create a Transform</span><span class="sxs-lookup"><span data-stu-id="38ad7-103">CLI example: Create a Transform</span></span>

<span data-ttu-id="38ad7-104">The Azure CLI script in this article shows how to create a transform.</span><span class="sxs-lookup"><span data-stu-id="38ad7-104">The Azure CLI script in this article shows how to create a transform.</span></span> <span data-ttu-id="38ad7-105">Transforms describe a simple workflow of tasks for processing your video or audio files (often referred to as a "recipe").</span><span class="sxs-lookup"><span data-stu-id="38ad7-105">Transforms describe a simple workflow of tasks for processing your video or audio files (often referred to as a "recipe").</span></span> <span data-ttu-id="38ad7-106">You should always check if a Transform with desired name and "recipe" already exist.</span><span class="sxs-lookup"><span data-stu-id="38ad7-106">You should always check if a Transform with desired name and "recipe" already exist.</span></span> <span data-ttu-id="38ad7-107">If it does, you should reuse it.</span><span class="sxs-lookup"><span data-stu-id="38ad7-107">If it does, you should reuse it.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="38ad7-108">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later.</span><span class="sxs-lookup"><span data-stu-id="38ad7-108">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later.</span></span> <span data-ttu-id="38ad7-109">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="38ad7-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="38ad7-110">If you need to install or upgrade, see [Install the Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="38ad7-110">If you need to install or upgrade, see [Install the Azure CLI](/cli/azure/install-azure-cli).</span></span> 

## <a name="example-script"></a><span data-ttu-id="38ad7-111">Example script</span><span class="sxs-lookup"><span data-stu-id="38ad7-111">Example script</span></span>

[!code-azurecli-interactive[main](../../../../cli_scripts/media-services/create-transform/Create-Transform.sh "Create a transform")]

## <a name="next-steps"></a><span data-ttu-id="38ad7-112">Next steps</span><span class="sxs-lookup"><span data-stu-id="38ad7-112">Next steps</span></span>

<span data-ttu-id="38ad7-113">For more examples, see [Azure CLI samples](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="38ad7-113">For more examples, see [Azure CLI samples](../cli-samples.md).</span></span>
