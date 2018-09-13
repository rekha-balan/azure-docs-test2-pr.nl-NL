---
title: Create a Machine Learning workspace | Microsoft Docs
description: How to create a workspace for Azure Machine Learning Studio
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 5062cafa232c216e006efbf318f8aadc250fb32e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661639"
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="935d9-103">Create and share an Azure Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="935d9-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="935d9-104">This menu links to topics that describe how to set up the various data science environments used by the Cortana Analytics Process (CAPS).</span><span class="sxs-lookup"><span data-stu-id="935d9-104">This menu links to topics that describe how to set up the various data science environments used by the Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="935d9-105">To use Azure Machine Learning Studio, you need to have a Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="935d9-105">To use Azure Machine Learning Studio, you need to have a Machine Learning workspace.</span></span> <span data-ttu-id="935d9-106">This workspace contains the tools you need to create, manage, and publish experiments.</span><span class="sxs-lookup"><span data-stu-id="935d9-106">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="to-create-a-workspace"></a><span data-ttu-id="935d9-107">To create a workspace</span><span class="sxs-lookup"><span data-stu-id="935d9-107">To create a workspace</span></span>
1. <span data-ttu-id="935d9-108">Sign in to the [Azure portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="935d9-108">Sign in to the [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="935d9-109">To sign in and create a workspace, you need to be an Azure subscription administrator.</span><span class="sxs-lookup"><span data-stu-id="935d9-109">To sign in and create a workspace, you need to be an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="935d9-110">Click **+New**</span><span class="sxs-lookup"><span data-stu-id="935d9-110">Click **+New**</span></span>

3. <span data-ttu-id="935d9-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span><span class="sxs-lookup"><span data-stu-id="935d9-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="935d9-112">Enter your workspace information</span><span class="sxs-lookup"><span data-stu-id="935d9-112">Enter your workspace information</span></span>

    - <span data-ttu-id="935d9-113">The *workspace name* may be up to 260 characters, not ending in a space.</span><span class="sxs-lookup"><span data-stu-id="935d9-113">The *workspace name* may be up to 260 characters, not ending in a space.</span></span> <span data-ttu-id="935d9-114">The name can't include these characters: `< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="935d9-114">The name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="935d9-115">The *web service plan* you choose (or create), along with the associated *pricing tier* you select, is used if you deploy web services from this workspace.</span><span class="sxs-lookup"><span data-stu-id="935d9-115">The *web service plan* you choose (or create), along with the associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Create a new workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="935d9-117">Click **Create**</span><span class="sxs-lookup"><span data-stu-id="935d9-117">Click **Create**</span></span>

<span data-ttu-id="935d9-118">Once the workspace is deployed, you can open it in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="935d9-118">Once the workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="935d9-119">Browse to Machine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="935d9-119">Browse to Machine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="935d9-120">Select your workspace in the upper-right-hand corner.</span><span class="sxs-lookup"><span data-stu-id="935d9-120">Select your workspace in the upper-right-hand corner.</span></span>

    ![Select workspace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="935d9-122">Click **my experiments**.</span><span class="sxs-lookup"><span data-stu-id="935d9-122">Click **my experiments**.</span></span>

    ![Open experiments](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="935d9-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="935d9-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="935d9-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect to a Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="935d9-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect to a Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="935d9-126">Sharing an Azure Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="935d9-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="935d9-127">Once a Machine Learning workspace is created, you can invite users to your workspace to share access to your workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span><span class="sxs-lookup"><span data-stu-id="935d9-127">Once a Machine Learning workspace is created, you can invite users to your workspace to share access to your workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="935d9-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in the workspace.</span><span class="sxs-lookup"><span data-stu-id="935d9-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in the workspace.</span></span>
* <span data-ttu-id="935d9-129">**Owner** - An owner can invite and remove users in the workspace, in addition to what a user can do.</span><span class="sxs-lookup"><span data-stu-id="935d9-129">**Owner** - An owner can invite and remove users in the workspace, in addition to what a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="935d9-130">The administrator account that creates the workspace is automatically added to the workspace as workspace Owner.</span><span class="sxs-lookup"><span data-stu-id="935d9-130">The administrator account that creates the workspace is automatically added to the workspace as workspace Owner.</span></span> <span data-ttu-id="935d9-131">However, other administrators or users in that subscription are not automatically granted access to the workspace - you need to invite them explicitly.</span><span class="sxs-lookup"><span data-stu-id="935d9-131">However, other administrators or users in that subscription are not automatically granted access to the workspace - you need to invite them explicitly.</span></span>
> 
> 

### <a name="to-share-a-workspace"></a><span data-ttu-id="935d9-132">To share a workspace</span><span class="sxs-lookup"><span data-stu-id="935d9-132">To share a workspace</span></span>

1. <span data-ttu-id="935d9-133">Sign in to Machine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="935d9-133">Sign in to Machine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="935d9-134">In the left panel, click **SETTINGS**</span><span class="sxs-lookup"><span data-stu-id="935d9-134">In the left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="935d9-135">Click the **USERS** tab</span><span class="sxs-lookup"><span data-stu-id="935d9-135">Click the **USERS** tab</span></span>

4. <span data-ttu-id="935d9-136">Click **INVITE MORE USERS** at the bottom of the page</span><span class="sxs-lookup"><span data-stu-id="935d9-136">Click **INVITE MORE USERS** at the bottom of the page</span></span>

    ![Studio settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="935d9-138">Enter one or more email addresses.</span><span class="sxs-lookup"><span data-stu-id="935d9-138">Enter one or more email addresses.</span></span> <span data-ttu-id="935d9-139">The users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="935d9-139">The users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="935d9-140">Select whether you want to add the users as Owner or User.</span><span class="sxs-lookup"><span data-stu-id="935d9-140">Select whether you want to add the users as Owner or User.</span></span>

7. <span data-ttu-id="935d9-141">Click the **OK** checkmark button.</span><span class="sxs-lookup"><span data-stu-id="935d9-141">Click the **OK** checkmark button.</span></span>

<span data-ttu-id="935d9-142">Each user you add will receive an email with instructions on how to sign in to the shared workspace.</span><span class="sxs-lookup"><span data-stu-id="935d9-142">Each user you add will receive an email with instructions on how to sign in to the shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="935d9-143">For users to be able to deploy or manage web services in this workspace, they must be a contributor or administrator in the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="935d9-143">For users to be able to deploy or manage web services in this workspace, they must be a contributor or administrator in the Azure subscription.</span></span> 







