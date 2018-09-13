---
title: PowerShell module for Machine Learning | Microsoft Docs
description: The PowerShell module for Azure Machine Learning is available in public preview mode. Use PowerShell to create and manage workspaces, experiments, web services, and more.
keywords: experiment,linear regression,machine learning algorithms,machine learning tutorial,predictive modeling techniques,data science experiment
services: machine-learning
documentationcenter: ''
author: hning86
ms.author: haining
manager: mwinkle
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.openlocfilehash: 6ecd2d9a1519cd89058385ad1e40aee9b3fc9082
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856830"
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a><span data-ttu-id="15165-105">PowerShell module for Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="15165-105">PowerShell module for Microsoft Azure Machine Learning</span></span>
<span data-ttu-id="15165-106">The PowerShell module for Azure Machine Learning is a powerful tool that allows you to use Windows PowerShell to manage workspaces, experiments, datasets, Classic web services, and more.</span><span class="sxs-lookup"><span data-stu-id="15165-106">The PowerShell module for Azure Machine Learning is a powerful tool that allows you to use Windows PowerShell to manage workspaces, experiments, datasets, Classic web services, and more.</span></span>

<span data-ttu-id="15165-107">You can view the documentation and download the module, along with the full source code, at [https://aka.ms/amlps](https://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="15165-107">You can view the documentation and download the module, along with the full source code, at [https://aka.ms/amlps](https://aka.ms/amlps).</span></span> 

> [!NOTE]
> <span data-ttu-id="15165-108">The Azure Machine Learning PowerShell module is currently in preview mode.</span><span class="sxs-lookup"><span data-stu-id="15165-108">The Azure Machine Learning PowerShell module is currently in preview mode.</span></span> <span data-ttu-id="15165-109">The module will continue to be improved and expanded during this preview period.</span><span class="sxs-lookup"><span data-stu-id="15165-109">The module will continue to be improved and expanded during this preview period.</span></span> <span data-ttu-id="15165-110">Keep an eye on the [Cortana Intelligence and Machine Learning Blog](https://blogs.technet.microsoft.com/machinelearning/) for news and information.</span><span class="sxs-lookup"><span data-stu-id="15165-110">Keep an eye on the [Cortana Intelligence and Machine Learning Blog](https://blogs.technet.microsoft.com/machinelearning/) for news and information.</span></span>

## <a name="what-is-the-machine-learning-powershell-module"></a><span data-ttu-id="15165-111">What is the Machine Learning PowerShell module?</span><span class="sxs-lookup"><span data-stu-id="15165-111">What is the Machine Learning PowerShell module?</span></span>
<span data-ttu-id="15165-112">The Machine Learning PowerShell module is a .NET-based DLL module that allows you to fully manage Azure Machine Learning workspaces, experiments, datasets, Classic web services, and Classic web service endpoints from Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15165-112">The Machine Learning PowerShell module is a .NET-based DLL module that allows you to fully manage Azure Machine Learning workspaces, experiments, datasets, Classic web services, and Classic web service endpoints from Windows PowerShell.</span></span> 

<span data-ttu-id="15165-113">Along with the module, you can download the full source code which includes a cleanly separated [C# API layer](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs).</span><span class="sxs-lookup"><span data-stu-id="15165-113">Along with the module, you can download the full source code which includes a cleanly separated [C# API layer](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs).</span></span> <span data-ttu-id="15165-114">You can reference this DLL from your own .NET project and manage Azure Machine Learning through .NET code.</span><span class="sxs-lookup"><span data-stu-id="15165-114">You can reference this DLL from your own .NET project and manage Azure Machine Learning through .NET code.</span></span> <span data-ttu-id="15165-115">In addition, the DLL depends on underlying REST APIs that you can use directly from your favorite client.</span><span class="sxs-lookup"><span data-stu-id="15165-115">In addition, the DLL depends on underlying REST APIs that you can use directly from your favorite client.</span></span>

## <a name="what-can-i-do-with-the-powershell-module"></a><span data-ttu-id="15165-116">What can I do with the PowerShell module?</span><span class="sxs-lookup"><span data-stu-id="15165-116">What can I do with the PowerShell module?</span></span>
<span data-ttu-id="15165-117">Here are some of the tasks you can perform with this PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="15165-117">Here are some of the tasks you can perform with this PowerShell module.</span></span> <span data-ttu-id="15165-118">Check out the [full documentation](https://aka.ms/amlps) for these and many more functions.</span><span class="sxs-lookup"><span data-stu-id="15165-118">Check out the [full documentation](https://aka.ms/amlps) for these and many more functions.</span></span>

* <span data-ttu-id="15165-119">Provision a new workspace using a management certificate ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))</span><span class="sxs-lookup"><span data-stu-id="15165-119">Provision a new workspace using a management certificate ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))</span></span>
* <span data-ttu-id="15165-120">Export and import a JSON file representing an experiment graph ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) and [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))</span><span class="sxs-lookup"><span data-stu-id="15165-120">Export and import a JSON file representing an experiment graph ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) and [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))</span></span>
* <span data-ttu-id="15165-121">Run an experiment ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))</span><span class="sxs-lookup"><span data-stu-id="15165-121">Run an experiment ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))</span></span>
* <span data-ttu-id="15165-122">Create a web service out of a predictive experiment ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))</span><span class="sxs-lookup"><span data-stu-id="15165-122">Create a web service out of a predictive experiment ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))</span></span>
* <span data-ttu-id="15165-123">Create an endpoint on a published web service ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))</span><span class="sxs-lookup"><span data-stu-id="15165-123">Create an endpoint on a published web service ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))</span></span>
* <span data-ttu-id="15165-124">Invoke an RRS and/or BES web service endpoint ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) and [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))</span><span class="sxs-lookup"><span data-stu-id="15165-124">Invoke an RRS and/or BES web service endpoint ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) and [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))</span></span>

<span data-ttu-id="15165-125">Here's a quick example of using PowerShell to run an existing experiment:</span><span class="sxs-lookup"><span data-stu-id="15165-125">Here's a quick example of using PowerShell to run an existing experiment:</span></span>

        #Find the first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run the Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

<span data-ttu-id="15165-126">For a more in-depth use case, see this article on using the PowerShell module to automate a commonly-requested task: [Create many Machine Learning models and web service endpoints from one experiment using PowerShell](create-models-and-endpoints-with-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="15165-126">For a more in-depth use case, see this article on using the PowerShell module to automate a commonly-requested task: [Create many Machine Learning models and web service endpoints from one experiment using PowerShell](create-models-and-endpoints-with-powershell.md).</span></span>

## <a name="how-do-i-get-started"></a><span data-ttu-id="15165-127">How do I get started?</span><span class="sxs-lookup"><span data-stu-id="15165-127">How do I get started?</span></span>
<span data-ttu-id="15165-128">To get started with Machine Learning PowerShell, download the [release package](https://github.com/hning86/azuremlps/releases) from GitHub and follow the [instructions for installation](https://github.com/hning86/azuremlps/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="15165-128">To get started with Machine Learning PowerShell, download the [release package](https://github.com/hning86/azuremlps/releases) from GitHub and follow the [instructions for installation](https://github.com/hning86/azuremlps/blob/master/README.md).</span></span> <span data-ttu-id="15165-129">The instructions explain how to unblock the downloaded/unzipped DLL and then import it into your PowerShell environment.</span><span class="sxs-lookup"><span data-stu-id="15165-129">The instructions explain how to unblock the downloaded/unzipped DLL and then import it into your PowerShell environment.</span></span> <span data-ttu-id="15165-130">Most of the cmdlets require that you supply the workspace ID, the workspace authorization token, and the Azure region that the workspace is in.</span><span class="sxs-lookup"><span data-stu-id="15165-130">Most of the cmdlets require that you supply the workspace ID, the workspace authorization token, and the Azure region that the workspace is in.</span></span> <span data-ttu-id="15165-131">The simplest way to provide the values is through a default config.json file.</span><span class="sxs-lookup"><span data-stu-id="15165-131">The simplest way to provide the values is through a default config.json file.</span></span> <span data-ttu-id="15165-132">The instructions also explain how to configure this file.</span><span class="sxs-lookup"><span data-stu-id="15165-132">The instructions also explain how to configure this file.</span></span> 

<span data-ttu-id="15165-133">And if you want, you can clone the git tree, modify the code, and compile it locally using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15165-133">And if you want, you can clone the git tree, modify the code, and compile it locally using Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15165-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="15165-134">Next steps</span></span>
<span data-ttu-id="15165-135">You can find the full documentation for the PowerShell module at [https://aka.ms/amlps](https://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="15165-135">You can find the full documentation for the PowerShell module at [https://aka.ms/amlps](https://aka.ms/amlps).</span></span> 

<span data-ttu-id="15165-136">For an extended example of how to use the module in a real-world scenario, check out the in-depth use case, [Create many Machine Learning models and web service endpoints from one experiment using PowerShell](create-models-and-endpoints-with-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="15165-136">For an extended example of how to use the module in a real-world scenario, check out the in-depth use case, [Create many Machine Learning models and web service endpoints from one experiment using PowerShell](create-models-and-endpoints-with-powershell.md).</span></span>
