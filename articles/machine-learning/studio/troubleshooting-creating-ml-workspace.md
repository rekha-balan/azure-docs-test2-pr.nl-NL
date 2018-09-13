---
title: 'Troubleshoot: Create and connect to a Machine Learning workspace | Microsoft Docs'
description: Solutions for common issues in creating and connecting to an Azure Machine Learning workspace
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.openlocfilehash: 262c9af4e0f3ee34dc89986affacb6c0d8a0d801
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871079"
---
# <a name="troubleshooting-guide-create-and-connect-to-an-machine-learning-workspace"></a><span data-ttu-id="ded1e-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="ded1e-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span></span>
<span data-ttu-id="ded1e-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span><span class="sxs-lookup"><span data-stu-id="ded1e-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="ded1e-105">Workspace owner</span><span class="sxs-lookup"><span data-stu-id="ded1e-105">Workspace owner</span></span>
<span data-ttu-id="ded1e-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span><span class="sxs-lookup"><span data-stu-id="ded1e-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span> <span data-ttu-id="ded1e-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span><span class="sxs-lookup"><span data-stu-id="ded1e-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span></span>

<span data-ttu-id="ded1e-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span><span class="sxs-lookup"><span data-stu-id="ded1e-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

[Manage an Azure Machine Learning workspace]: manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="ded1e-110">Allowed regions</span><span class="sxs-lookup"><span data-stu-id="ded1e-110">Allowed regions</span></span>
<span data-ttu-id="ded1e-111">Machine Learning is currently available in a limited number of regions.</span><span class="sxs-lookup"><span data-stu-id="ded1e-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="ded1e-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span><span class="sxs-lookup"><span data-stu-id="ded1e-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span></span>

<span data-ttu-id="ded1e-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span><span class="sxs-lookup"><span data-stu-id="ded1e-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="ded1e-114">Storage account</span><span class="sxs-lookup"><span data-stu-id="ded1e-114">Storage account</span></span>
<span data-ttu-id="ded1e-115">The Machine Learning service needs a storage account to store data.</span><span class="sxs-lookup"><span data-stu-id="ded1e-115">The Machine Learning service needs a storage account to store data.</span></span> <span data-ttu-id="ded1e-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span><span class="sxs-lookup"><span data-stu-id="ded1e-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span></span>

<span data-ttu-id="ded1e-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span><span class="sxs-lookup"><span data-stu-id="ded1e-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span></span> <span data-ttu-id="ded1e-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span><span class="sxs-lookup"><span data-stu-id="ded1e-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span></span>

![Workspace not found][screen3]

<span data-ttu-id="ded1e-120">**To delete browser cookies**</span><span class="sxs-lookup"><span data-stu-id="ded1e-120">**To delete browser cookies**</span></span>

1. <span data-ttu-id="ded1e-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span><span class="sxs-lookup"><span data-stu-id="ded1e-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span></span>  

![Internet options][screen4]

2. <span data-ttu-id="ded1e-123">Under the **General** tab, click **Delete…**</span><span class="sxs-lookup"><span data-stu-id="ded1e-123">Under the **General** tab, click **Delete…**</span></span>

![General tab][screen5]

3. <span data-ttu-id="ded1e-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ded1e-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Delete cookies][screen6]

<span data-ttu-id="ded1e-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span><span class="sxs-lookup"><span data-stu-id="ded1e-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="ded1e-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span><span class="sxs-lookup"><span data-stu-id="ded1e-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="ded1e-129">Comments</span><span class="sxs-lookup"><span data-stu-id="ded1e-129">Comments</span></span>

<span data-ttu-id="ded1e-130">Our goal is to make the Machine Learning experience as seamless as possible.</span><span class="sxs-lookup"><span data-stu-id="ded1e-130">Our goal is to make the Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="ded1e-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span><span class="sxs-lookup"><span data-stu-id="ded1e-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span></span>

[screen1]:media/troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/troubleshooting-creating-ml-workspace/screen6.png
