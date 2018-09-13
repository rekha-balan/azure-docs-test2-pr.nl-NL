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
# <a name="track-progress-of-data-science-projects"></a>Track progress of data science projects

Data science group managers, team leads, and project leads need to track the progress of their projects, what work has been done on them and by whom, and remains on the to-do lists. 

## <a name="azure-devops-dashboards"></a>Azure DevOps dashboards
If you are using Azure DevOps, you are able to build dashboards to track the activities and the work items associated with a given Agile project. 

For more information on how to create and customize dashboards and widgets on Azure DevOps, see the following sets of instructions:

- [Add and manage dashboards](https://docs.microsoft.com/azure/devops/report/dashboards/dashboards)
- [Add widgets to a dashboard](https://docs.microsoft.com/azure/devops/report/dashboards/add-widget-to-dashboard).

## <a name="example-dashboard"></a>Example dashboard

Here is a simple example dashboard that is built to track the sprint activities of an Agile data science project, as well as the number of commits to associated repositories. The **top left** panel shows:

- the countdown of the current sprint, 
- the number of commits for each repository in the last 7 days
- the work item for specific users. 

The remaining panels show the cumulative flow diagram (CFD), burndown, and burnup for a project:

- **Bottom left**:  CFD the quantity of work in a given state, showing approved in gray, committed in blue, and done in green.
- **Top right**: burndown chart the work left to complete versus the time remaining).
- **Bottom right**: burnup chart the work that has been completed versus the total amount of work.

![dashboard](./media/track-progress/dashboard.png)

For a description of how to build these charts, see  the quickstarts and tutorials at [Dashboards](https://docs.microsoft.com/azure/devops/report/dashboards/).
 
## <a name="next-steps"></a>Next steps

Walkthroughs that demonstrate all the steps in the process for **specific scenarios** are also provided. They are listed and linked with thumbnail descriptions in the [Example walkthroughs](walkthroughs.md) article. They illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application. 
