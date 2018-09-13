---
title: Data Science Virtual machines in Azure | Microsoft Docs
description: Set up a Data Science Virtual Machine
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 80bae03ee3b8adfa08977f037dbc2432f2398a7f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540705"
---
# <a name="data-science-virtual-machines-in-azure"></a><span data-ttu-id="1af82-103">Data Science Virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="1af82-103">Data Science Virtual machines in Azure</span></span>
<span data-ttu-id="1af82-104">Instructions are provided here that describe how to set up an Azure VM and an Azure VM with SQL Service as IPython Notebook servers.</span><span class="sxs-lookup"><span data-stu-id="1af82-104">Instructions are provided here that describe how to set up an Azure VM and an Azure VM with SQL Service as IPython Notebook servers.</span></span> <span data-ttu-id="1af82-105">The Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, and AzCopy, as well as other utilities that are useful for data science projects.</span><span class="sxs-lookup"><span data-stu-id="1af82-105">The Windows virtual machine is configured with supporting tools such as IPython Notebook, Azure Storage Explorer, and AzCopy, as well as other utilities that are useful for data science projects.</span></span> <span data-ttu-id="1af82-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways to upload data to Azure storage from your local machine or to download it to your local machine from storage.</span><span class="sxs-lookup"><span data-stu-id="1af82-106">Azure Storage Explorer and AzCopy, for example, provide convenient ways to upload data to Azure storage from your local machine or to download it to your local machine from storage.</span></span> 

<span data-ttu-id="1af82-107">This menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1af82-107">This menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="1af82-108">Several types of Azure virtual machines can be provisioned and configured to be used as part of a cloud-based data science environment.</span><span class="sxs-lookup"><span data-stu-id="1af82-108">Several types of Azure virtual machines can be provisioned and configured to be used as part of a cloud-based data science environment.</span></span> <span data-ttu-id="1af82-109">The decision about which flavor of virtual machine to use depends on the type and quantity of data to be modeled with machine learning, and the target destination for that data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="1af82-109">The decision about which flavor of virtual machine to use depends on the type and quantity of data to be modeled with machine learning, and the target destination for that data in the cloud.</span></span> 

* <span data-ttu-id="1af82-110">For guidance on the questions to consider when making this decision, see [Plan Your Azure Machine Learning Data Science Environment](machine-learning-data-science-plan-your-environment.md).</span><span class="sxs-lookup"><span data-stu-id="1af82-110">For guidance on the questions to consider when making this decision, see [Plan Your Azure Machine Learning Data Science Environment](machine-learning-data-science-plan-your-environment.md).</span></span> 
* <span data-ttu-id="1af82-111">For a catalog of some of the scenarios you might encounter when doing advanced analytics, see [Scenarios for the Advanced Analytics Process and Technology in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="1af82-111">For a catalog of some of the scenarios you might encounter when doing advanced analytics, see [Scenarios for the Advanced Analytics Process and Technology in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md)</span></span>

<span data-ttu-id="1af82-112">Two sets of instructions are provided:</span><span class="sxs-lookup"><span data-stu-id="1af82-112">Two sets of instructions are provided:</span></span>

* <span data-ttu-id="1af82-113">[Set up an Azure virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-virtual-machine.md) shows how to provision an Azure virtual machine with IPython Notebook and other tools used to do data science for cases in which a form of Azure storage other than SQL can be used to store the data.</span><span class="sxs-lookup"><span data-stu-id="1af82-113">[Set up an Azure virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-virtual-machine.md) shows how to provision an Azure virtual machine with IPython Notebook and other tools used to do data science for cases in which a form of Azure storage other than SQL can be used to store the data.</span></span>
* <span data-ttu-id="1af82-114">[Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md) shows how to provision an Azure SQL Server virtual machine with IPython Notebook and other tools used to do data science for cases in which a SQL database can be used to store  the data.</span><span class="sxs-lookup"><span data-stu-id="1af82-114">[Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md) shows how to provision an Azure SQL Server virtual machine with IPython Notebook and other tools used to do data science for cases in which a SQL database can be used to store  the data.</span></span>

<span data-ttu-id="1af82-115">Once provisioned and configured, these virtual machines are ready for use as IPython Notebook servers for the exploration and processing of data, and for other tasks needed in conjunction with Azure Machine Learning and the Team Data Science Process (TDSP).</span><span class="sxs-lookup"><span data-stu-id="1af82-115">Once provisioned and configured, these virtual machines are ready for use as IPython Notebook servers for the exploration and processing of data, and for other tasks needed in conjunction with Azure Machine Learning and the Team Data Science Process (TDSP).</span></span> <span data-ttu-id="1af82-116">The next steps in the data science process are mapped in the [TDSP learning path](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into SQL Server or HDInsight, process and sample it there in preparation for learning from the data with Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1af82-116">The next steps in the data science process are mapped in the [TDSP learning path](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into SQL Server or HDInsight, process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

> [!NOTE]
> <span data-ttu-id="1af82-117">Azure Virtual Machines are priced as **pay only for what you use**.</span><span class="sxs-lookup"><span data-stu-id="1af82-117">Azure Virtual Machines are priced as **pay only for what you use**.</span></span> <span data-ttu-id="1af82-118">To ensure that you are not being billed when not using your virtual machine, it has to be in the **Stopped (Deallocated)** state from the [Azure Classic Portal](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="1af82-118">To ensure that you are not being billed when not using your virtual machine, it has to be in the **Stopped (Deallocated)** state from the [Azure Classic Portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="1af82-119">For step-by-step instructions or how to deallocate you virtual machine, see  [Shutdown and deallocate virtual machine when not in use](machine-learning-data-science-setup-virtual-machine.md#shutdown)</span><span class="sxs-lookup"><span data-stu-id="1af82-119">For step-by-step instructions or how to deallocate you virtual machine, see  [Shutdown and deallocate virtual machine when not in use](machine-learning-data-science-setup-virtual-machine.md#shutdown)</span></span>
> 
> 

