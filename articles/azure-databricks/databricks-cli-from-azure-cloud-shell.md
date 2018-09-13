---
title: Use Databricks CLI from Azure Cloud Shell | Microsoft Docs
description: Learn how to use the Databricks CLI from Azure Cloud Shell.
services: azure-databricks
documentationcenter: ''
author: nitinme
manager: cgronlun
editor: cgronlun
ms.service: azure-databricks
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: 3ea4ebbd95237b50054fb0e344f260120d597ab5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867357"
---
# <a name="use-databricks-cli-from-azure-cloud-shell"></a><span data-ttu-id="ac085-103">Use Databricks CLI from Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="ac085-103">Use Databricks CLI from Azure Cloud Shell</span></span>

<span data-ttu-id="ac085-104">Learn how to use the Databricks CLI from Azure Cloud Shell to perform operations on Databricks.</span><span class="sxs-lookup"><span data-stu-id="ac085-104">Learn how to use the Databricks CLI from Azure Cloud Shell to perform operations on Databricks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac085-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ac085-105">Prerequisites</span></span>

* <span data-ttu-id="ac085-106">An Azure Databricks workspace and cluster.</span><span class="sxs-lookup"><span data-stu-id="ac085-106">An Azure Databricks workspace and cluster.</span></span> <span data-ttu-id="ac085-107">For instructions, see [Get started with Azure Databricks](quickstart-create-databricks-workspace-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ac085-107">For instructions, see [Get started with Azure Databricks](quickstart-create-databricks-workspace-portal.md).</span></span> 

* <span data-ttu-id="ac085-108">Set up a personal access token in Databricks.</span><span class="sxs-lookup"><span data-stu-id="ac085-108">Set up a personal access token in Databricks.</span></span> <span data-ttu-id="ac085-109">For instructions, see [Token management](https://docs.azuredatabricks.net/api/latest/authentication.html#token-management).</span><span class="sxs-lookup"><span data-stu-id="ac085-109">For instructions, see [Token management](https://docs.azuredatabricks.net/api/latest/authentication.html#token-management).</span></span>

## <a name="use-the-azure-cloud-shell"></a><span data-ttu-id="ac085-110">Use the Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="ac085-110">Use the Azure Cloud Shell</span></span>

1. <span data-ttu-id="ac085-111">Log in to the [Azure  portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac085-111">Log in to the [Azure  portal](https://portal.azure.com).</span></span>
 
2. <span data-ttu-id="ac085-112">From the top-right corner, click the **Cloud Shell** icon.</span><span class="sxs-lookup"><span data-stu-id="ac085-112">From the top-right corner, click the **Cloud Shell** icon.</span></span>

   <span data-ttu-id="ac085-113">![Launch Cloud Shell](./media/databricks-cli-from-azure-cloud-shell/launch-azure-cloud-shell.png "Launch Azure Cloud Shell")</span><span class="sxs-lookup"><span data-stu-id="ac085-113">![Launch Cloud Shell](./media/databricks-cli-from-azure-cloud-shell/launch-azure-cloud-shell.png "Launch Azure Cloud Shell")</span></span>

3. <span data-ttu-id="ac085-114">Make sure you select **Bash** for the Cloud Shell environment.</span><span class="sxs-lookup"><span data-stu-id="ac085-114">Make sure you select **Bash** for the Cloud Shell environment.</span></span> <span data-ttu-id="ac085-115">You can select from the drop-down option, as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="ac085-115">You can select from the drop-down option, as shown in the following screenshot.</span></span>

   <span data-ttu-id="ac085-116">![Select Bash for the Cloud Shell environment](./media/databricks-cli-from-azure-cloud-shell/select-bash-for-shell.png "Select Bash")</span><span class="sxs-lookup"><span data-stu-id="ac085-116">![Select Bash for the Cloud Shell environment](./media/databricks-cli-from-azure-cloud-shell/select-bash-for-shell.png "Select Bash")</span></span> 

4. <span data-ttu-id="ac085-117">Create a virtual environment in which you can install the Databricks CLI.</span><span class="sxs-lookup"><span data-stu-id="ac085-117">Create a virtual environment in which you can install the Databricks CLI.</span></span> <span data-ttu-id="ac085-118">In the snippet below, you create a virtual environment called `databrickscli`.</span><span class="sxs-lookup"><span data-stu-id="ac085-118">In the snippet below, you create a virtual environment called `databrickscli`.</span></span>

       virtualenv -p /usr/bin/python2.7 databrickscli

5. <span data-ttu-id="ac085-119">Switch to the virtual environment you created.</span><span class="sxs-lookup"><span data-stu-id="ac085-119">Switch to the virtual environment you created.</span></span>

       source databrickscli/bin/activate

6. <span data-ttu-id="ac085-120">Install the Databricks CLI.</span><span class="sxs-lookup"><span data-stu-id="ac085-120">Install the Databricks CLI.</span></span>

       pip install databricks-cli

7. <span data-ttu-id="ac085-121">Set up authentication with Databricks by using the access token that you must have created, listed as part of prerequisites.</span><span class="sxs-lookup"><span data-stu-id="ac085-121">Set up authentication with Databricks by using the access token that you must have created, listed as part of prerequisites.</span></span> <span data-ttu-id="ac085-122">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="ac085-122">Use the following command:</span></span>

       databricks configure --token

    <span data-ttu-id="ac085-123">You will receive the following prompts:</span><span class="sxs-lookup"><span data-stu-id="ac085-123">You will receive the following prompts:</span></span>

    * <span data-ttu-id="ac085-124">First, you are prompted to enter the Databricks host.</span><span class="sxs-lookup"><span data-stu-id="ac085-124">First, you are prompted to enter the Databricks host.</span></span> <span data-ttu-id="ac085-125">Enter the value in the format `https://eastus2.azuredatabricks.net`.</span><span class="sxs-lookup"><span data-stu-id="ac085-125">Enter the value in the format `https://eastus2.azuredatabricks.net`.</span></span> <span data-ttu-id="ac085-126">Here, **East US 2** is the Azure region where you created your Azure Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="ac085-126">Here, **East US 2** is the Azure region where you created your Azure Databricks workspace.</span></span>

    * <span data-ttu-id="ac085-127">Next, you are prompted to enter a token.</span><span class="sxs-lookup"><span data-stu-id="ac085-127">Next, you are prompted to enter a token.</span></span> <span data-ttu-id="ac085-128">Enter the token that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ac085-128">Enter the token that you created earlier.</span></span>

<span data-ttu-id="ac085-129">Once you complete these steps, you can start using Databricks CLI from Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="ac085-129">Once you complete these steps, you can start using Databricks CLI from Azure Cloud Shell.</span></span>

## <a name="use-databricks-cli"></a><span data-ttu-id="ac085-130">Use Databricks CLI</span><span class="sxs-lookup"><span data-stu-id="ac085-130">Use Databricks CLI</span></span>

<span data-ttu-id="ac085-131">You can now start using the Databricks CLI.</span><span class="sxs-lookup"><span data-stu-id="ac085-131">You can now start using the Databricks CLI.</span></span> <span data-ttu-id="ac085-132">For example, run the following command to list all the Databricks clusters that you have in your workspace.</span><span class="sxs-lookup"><span data-stu-id="ac085-132">For example, run the following command to list all the Databricks clusters that you have in your workspace.</span></span>

    databricks clusters list

<span data-ttu-id="ac085-133">You can also use the following command to access the Databricks filesystem (DBFS).</span><span class="sxs-lookup"><span data-stu-id="ac085-133">You can also use the following command to access the Databricks filesystem (DBFS).</span></span>

    databricks fs ls


<span data-ttu-id="ac085-134">For a complete reference on commands, see [Databricks CLI](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html).</span><span class="sxs-lookup"><span data-stu-id="ac085-134">For a complete reference on commands, see [Databricks CLI](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html).</span></span>


## <a name="next-steps"></a><span data-ttu-id="ac085-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="ac085-135">Next steps</span></span>

* <span data-ttu-id="ac085-136">To learn more about Azure CLI, see [Azure CLI overview](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="ac085-136">To learn more about Azure CLI, see [Azure CLI overview](../cloud-shell/overview.md)</span></span>
* <span data-ttu-id="ac085-137">To see a list of commands for Azure CLI, see [Azure CLI reference](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)</span><span class="sxs-lookup"><span data-stu-id="ac085-137">To see a list of commands for Azure CLI, see [Azure CLI reference](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)</span></span>
* <span data-ttu-id="ac085-138">To see a list of commands for Databricks CLI, see [Databricks CLI](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html)</span><span class="sxs-lookup"><span data-stu-id="ac085-138">To see a list of commands for Databricks CLI, see [Databricks CLI](https://docs.azuredatabricks.net/user-guide/dev-tools/databricks-cli.html)</span></span>


