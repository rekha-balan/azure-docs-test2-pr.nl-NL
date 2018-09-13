---
title: Set up data science environments in Azure | Microsoft Docs
description: Set up data science environments on Azure for use in the Team Data Science Process.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: 481cfa6a-7ea3-46ac-b0f9-2e3982c37153
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: deguhath
ms.openlocfilehash: 6c28a64830afeb19c6a9264888b296c3b99990d1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856405"
---
# <a name="set-up-data-science-environments-for-use-in-the-team-data-science-process"></a><span data-ttu-id="57dea-103">Set up data science environments for use in the Team Data Science Process</span><span class="sxs-lookup"><span data-stu-id="57dea-103">Set up data science environments for use in the Team Data Science Process</span></span>
<span data-ttu-id="57dea-104">The Team Data Science Process uses various data science environments for the storage, processing, and analysis of data.</span><span class="sxs-lookup"><span data-stu-id="57dea-104">The Team Data Science Process uses various data science environments for the storage, processing, and analysis of data.</span></span> <span data-ttu-id="57dea-105">They include Azure Blob Storage, several types of Azure virtual machines, HDInsight (Hadoop) clusters, and Azure Machine Learning workspaces.</span><span class="sxs-lookup"><span data-stu-id="57dea-105">They include Azure Blob Storage, several types of Azure virtual machines, HDInsight (Hadoop) clusters, and Azure Machine Learning workspaces.</span></span> <span data-ttu-id="57dea-106">The decision about which environment to use depends on the type and quantity of data to be modeled and the target destination for that data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="57dea-106">The decision about which environment to use depends on the type and quantity of data to be modeled and the target destination for that data in the cloud.</span></span> 

* <span data-ttu-id="57dea-107">For guidance on questions to consider when making this decision, see [Plan Your Azure Machine Learning Data Science Environment](plan-your-environment.md).</span><span class="sxs-lookup"><span data-stu-id="57dea-107">For guidance on questions to consider when making this decision, see [Plan Your Azure Machine Learning Data Science Environment](plan-your-environment.md).</span></span> 
* <span data-ttu-id="57dea-108">For a catalog of some of the scenarios you might encounter when doing advanced analytics, see [Scenarios for the Team Data Science Process](plan-sample-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="57dea-108">For a catalog of some of the scenarios you might encounter when doing advanced analytics, see [Scenarios for the Team Data Science Process](plan-sample-scenarios.md)</span></span>

<span data-ttu-id="57dea-109">This menu links to topics that describe how to set up the various data science environments used by the Team Data Science Process.</span><span class="sxs-lookup"><span data-stu-id="57dea-109">This menu links to topics that describe how to set up the various data science environments used by the Team Data Science Process.</span></span>

[!INCLUDE [data-science-environment-setup](../../../includes/cap-setup-environments.md)]

<span data-ttu-id="57dea-110">The **Microsoft Data Science Virtual Machine (DSVM)** is also available as an Azure virtual machine (VM) image.</span><span class="sxs-lookup"><span data-stu-id="57dea-110">The **Microsoft Data Science Virtual Machine (DSVM)** is also available as an Azure virtual machine (VM) image.</span></span> <span data-ttu-id="57dea-111">This VM is pre-installed and configured with several popular tools that are commonly used for data analytics and machine learning.</span><span class="sxs-lookup"><span data-stu-id="57dea-111">This VM is pre-installed and configured with several popular tools that are commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="57dea-112">The DSVM is available on both Windows and Linux.</span><span class="sxs-lookup"><span data-stu-id="57dea-112">The DSVM is available on both Windows and Linux.</span></span> <span data-ttu-id="57dea-113">For more information, see [Introduction to the cloud-based Data Science Virtual Machine for Linux and Windows](../data-science-virtual-machine/overview.md).</span><span class="sxs-lookup"><span data-stu-id="57dea-113">For more information, see [Introduction to the cloud-based Data Science Virtual Machine for Linux and Windows](../data-science-virtual-machine/overview.md).</span></span>

<span data-ttu-id="57dea-114">Learn how to create:</span><span class="sxs-lookup"><span data-stu-id="57dea-114">Learn how to create:</span></span>

- [<span data-ttu-id="57dea-115">Windows DSVM</span><span class="sxs-lookup"><span data-stu-id="57dea-115">Windows DSVM</span></span>](../data-science-virtual-machine/provision-vm.md)
- [<span data-ttu-id="57dea-116">Ubuntu DSVM</span><span class="sxs-lookup"><span data-stu-id="57dea-116">Ubuntu DSVM</span></span>](../data-science-virtual-machine/dsvm-ubuntu-intro.md)
- [<span data-ttu-id="57dea-117">CentOS DSVM</span><span class="sxs-lookup"><span data-stu-id="57dea-117">CentOS DSVM</span></span>](../data-science-virtual-machine/linux-dsvm-intro.md)
- [<span data-ttu-id="57dea-118">Deep Learning VM</span><span class="sxs-lookup"><span data-stu-id="57dea-118">Deep Learning VM</span></span>](../data-science-virtual-machine/provision-deep-learning-dsvm.md)
