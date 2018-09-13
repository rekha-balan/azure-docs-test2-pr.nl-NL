---
title: Manage a Machine Learning workspace | Microsoft Docs
description: Manage access to Azure Machine Learning workspaces, and deploy and manage ML API web services
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.openlocfilehash: e1bdff6398f3229f8cde6e47376fa1dc03dd74b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856803"
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="6fa4a-103">Manage an Azure Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="6fa4a-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="6fa4a-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="6fa4a-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="6fa4a-105">You can manage Machine Learning workspaces in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-105">You can manage Machine Learning workspaces in the Azure portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="use-the-azure-portal"></a><span data-ttu-id="6fa4a-106">Use the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6fa4a-106">Use the Azure portal</span></span>

<span data-ttu-id="6fa4a-107">To manage a workspace in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="6fa4a-107">To manage a workspace in the Azure portal:</span></span>

1. <span data-ttu-id="6fa4a-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="6fa4a-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="6fa4a-110">Click the workspace you want to manage.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-110">Click the workspace you want to manage.</span></span>

<span data-ttu-id="6fa4a-111">In addition to the standard resource management information and options available, you can:</span><span class="sxs-lookup"><span data-stu-id="6fa4a-111">In addition to the standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="6fa4a-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="6fa4a-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span></span> <span data-ttu-id="6fa4a-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span></span>

<span data-ttu-id="6fa4a-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span></span> <span data-ttu-id="6fa4a-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md) for complete information.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="6fa4a-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="6fa4a-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span><span class="sxs-lookup"><span data-stu-id="6fa4a-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="6fa4a-119">For more information on setting access permissions, see [Manage access using RBAC and the Azure portal](../../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6fa4a-119">For more information on setting access permissions, see [Manage access using RBAC and the Azure portal](../../role-based-access-control/role-assignments-portal.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fa4a-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="6fa4a-120">Next steps</span></span>
* <span data-ttu-id="6fa4a-121">Learn more about [deploy Machine Learning with Azure Resource Manager Templates](deploy-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="6fa4a-121">Learn more about [deploy Machine Learning with Azure Resource Manager Templates](deploy-with-resource-manager-template.md).</span></span> 