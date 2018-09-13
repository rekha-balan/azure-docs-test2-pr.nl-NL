---
title: Execution of data science projects - Azure Machine Learning | Microsoft Docs
description: How a data scientist can track the progress of a data science project.
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: ''
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: deguhath
ms.openlocfilehash: 32390b05d2ec258a68ed4f53135399675105a7e9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870356"
---
# <a name="track-progress-of-data-science-projects"></a><span data-ttu-id="10e81-103">Track progress of data science projects</span><span class="sxs-lookup"><span data-stu-id="10e81-103">Track progress of data science projects</span></span>

<span data-ttu-id="10e81-104">Data science group managers, team leads, and project leads need to track the progress of their projects, what work has been done on them and by whom, and remains on the to-do lists.</span><span class="sxs-lookup"><span data-stu-id="10e81-104">Data science group managers, team leads, and project leads need to track the progress of their projects, what work has been done on them and by whom, and remains on the to-do lists.</span></span> 

## <a name="azure-devops-dashboards"></a><span data-ttu-id="10e81-105">Azure DevOps dashboards</span><span class="sxs-lookup"><span data-stu-id="10e81-105">Azure DevOps dashboards</span></span>
<span data-ttu-id="10e81-106">If you are using Azure DevOps, you are able to build dashboards to track the activities and the work items associated with a given Agile project.</span><span class="sxs-lookup"><span data-stu-id="10e81-106">If you are using Azure DevOps, you are able to build dashboards to track the activities and the work items associated with a given Agile project.</span></span> 

<span data-ttu-id="10e81-107">For more information on how to create and customize dashboards and widgets on Azure DevOps, see the following sets of instructions:</span><span class="sxs-lookup"><span data-stu-id="10e81-107">For more information on how to create and customize dashboards and widgets on Azure DevOps, see the following sets of instructions:</span></span>

- [<span data-ttu-id="10e81-108">Add and manage dashboards</span><span class="sxs-lookup"><span data-stu-id="10e81-108">Add and manage dashboards</span></span>](https://docs.microsoft.com/azure/devops/report/dashboards/dashboards)
- <span data-ttu-id="10e81-109">[Add widgets to a dashboard](https://docs.microsoft.com/azure/devops/report/dashboards/add-widget-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="10e81-109">[Add widgets to a dashboard](https://docs.microsoft.com/azure/devops/report/dashboards/add-widget-to-dashboard).</span></span>

## <a name="example-dashboard"></a><span data-ttu-id="10e81-110">Example dashboard</span><span class="sxs-lookup"><span data-stu-id="10e81-110">Example dashboard</span></span>

<span data-ttu-id="10e81-111">Here is a simple example dashboard that is built to track the sprint activities of an Agile data science project, as well as the number of commits to associated repositories.</span><span class="sxs-lookup"><span data-stu-id="10e81-111">Here is a simple example dashboard that is built to track the sprint activities of an Agile data science project, as well as the number of commits to associated repositories.</span></span> <span data-ttu-id="10e81-112">The **top left** panel shows:</span><span class="sxs-lookup"><span data-stu-id="10e81-112">The **top left** panel shows:</span></span>

- <span data-ttu-id="10e81-113">the countdown of the current sprint,</span><span class="sxs-lookup"><span data-stu-id="10e81-113">the countdown of the current sprint,</span></span> 
- <span data-ttu-id="10e81-114">the number of commits for each repository in the last 7 days</span><span class="sxs-lookup"><span data-stu-id="10e81-114">the number of commits for each repository in the last 7 days</span></span>
- <span data-ttu-id="10e81-115">the work item for specific users.</span><span class="sxs-lookup"><span data-stu-id="10e81-115">the work item for specific users.</span></span> 

<span data-ttu-id="10e81-116">The remaining panels show the cumulative flow diagram (CFD), burndown, and burnup for a project:</span><span class="sxs-lookup"><span data-stu-id="10e81-116">The remaining panels show the cumulative flow diagram (CFD), burndown, and burnup for a project:</span></span>

- <span data-ttu-id="10e81-117">**Bottom left**:  CFD the quantity of work in a given state, showing approved in gray, committed in blue, and done in green.</span><span class="sxs-lookup"><span data-stu-id="10e81-117">**Bottom left**:  CFD the quantity of work in a given state, showing approved in gray, committed in blue, and done in green.</span></span>
- <span data-ttu-id="10e81-118">**Top right**: burndown chart the work left to complete versus the time remaining).</span><span class="sxs-lookup"><span data-stu-id="10e81-118">**Top right**: burndown chart the work left to complete versus the time remaining).</span></span>
- <span data-ttu-id="10e81-119">**Bottom right**: burnup chart the work that has been completed versus the total amount of work.</span><span class="sxs-lookup"><span data-stu-id="10e81-119">**Bottom right**: burnup chart the work that has been completed versus the total amount of work.</span></span>

![dashboard](./media/track-progress/dashboard.png)

<span data-ttu-id="10e81-121">For a description of how to build these charts, see  the quickstarts and tutorials at [Dashboards](https://docs.microsoft.com/azure/devops/report/dashboards/).</span><span class="sxs-lookup"><span data-stu-id="10e81-121">For a description of how to build these charts, see  the quickstarts and tutorials at [Dashboards](https://docs.microsoft.com/azure/devops/report/dashboards/).</span></span>
 
## <a name="next-steps"></a><span data-ttu-id="10e81-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="10e81-122">Next steps</span></span>

<span data-ttu-id="10e81-123">Walkthroughs that demonstrate all the steps in the process for **specific scenarios** are also provided.</span><span class="sxs-lookup"><span data-stu-id="10e81-123">Walkthroughs that demonstrate all the steps in the process for **specific scenarios** are also provided.</span></span> <span data-ttu-id="10e81-124">They are listed and linked with thumbnail descriptions in the [Example walkthroughs](walkthroughs.md) article.</span><span class="sxs-lookup"><span data-stu-id="10e81-124">They are listed and linked with thumbnail descriptions in the [Example walkthroughs](walkthroughs.md) article.</span></span> <span data-ttu-id="10e81-125">They illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span><span class="sxs-lookup"><span data-stu-id="10e81-125">They illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span></span> 
