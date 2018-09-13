---
title: Azure CLI Script Sample - Add an Application in Batch | Microsoft Docs
description: Azure CLI Script Sample - Add an Application in Batch
services: batch
documentationcenter: ''
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: ''
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/20/2017
ms.author: antisch
ms.openlocfilehash: c38766b8414be45a4776c6035f2e5f865f565c47
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549418"
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="2b051-103">Adding applications to Azure Batch with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2b051-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="2b051-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span><span class="sxs-lookup"><span data-stu-id="2b051-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="2b051-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span><span class="sxs-lookup"><span data-stu-id="2b051-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="2b051-106">In this example the executable zip file is called 'my-application-exe.zip'.</span><span class="sxs-lookup"><span data-stu-id="2b051-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>
<span data-ttu-id="2b051-107">Running this script assumes that a Batch account has already been set up.</span><span class="sxs-lookup"><span data-stu-id="2b051-107">Running this script assumes that a Batch account has already been set up.</span></span> <span data-ttu-id="2b051-108">For more information, please see the [sample script for creating a Batch account](./batch-cli-sample-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="2b051-108">For more information, please see the [sample script for creating a Batch account](./batch-cli-sample-create-account.md).</span></span>

<span data-ttu-id="2b051-109">If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to log into Azure.</span><span class="sxs-lookup"><span data-stu-id="2b051-109">If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to log into Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="2b051-110">Sample script</span><span class="sxs-lookup"><span data-stu-id="2b051-110">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="2b051-111">Clean up application</span><span class="sxs-lookup"><span data-stu-id="2b051-111">Clean up application</span></span>

<span data-ttu-id="2b051-112">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span><span class="sxs-lookup"><span data-stu-id="2b051-112">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="2b051-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="2b051-113">Script explanation</span></span>

<span data-ttu-id="2b051-114">This script uses the following commands to create an application and upload an application package.</span><span class="sxs-lookup"><span data-stu-id="2b051-114">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="2b051-115">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="2b051-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="2b051-116">Command</span><span class="sxs-lookup"><span data-stu-id="2b051-116">Command</span></span> | <span data-ttu-id="2b051-117">Notes</span><span class="sxs-lookup"><span data-stu-id="2b051-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2b051-118">az batch application create</span><span class="sxs-lookup"><span data-stu-id="2b051-118">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="2b051-119">Creates an application.</span><span class="sxs-lookup"><span data-stu-id="2b051-119">Creates an application.</span></span>  |
| [<span data-ttu-id="2b051-120">az batch application set</span><span class="sxs-lookup"><span data-stu-id="2b051-120">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="2b051-121">Updates properties of an application.</span><span class="sxs-lookup"><span data-stu-id="2b051-121">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="2b051-122">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="2b051-122">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="2b051-123">Adds an application package to the specified application.</span><span class="sxs-lookup"><span data-stu-id="2b051-123">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="2b051-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b051-124">Next steps</span></span>

<span data-ttu-id="2b051-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2b051-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2b051-126">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2b051-126">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
