---
title: Install licensed components for the Azure-SSIS integration runtime | Microsoft Docs
description: Learn how an ISV can develop and install paid or licensed custom components for the Azure-SSIS integration runtime
services: data-factory
documentationcenter: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/13/2018
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 146dc8c4475a041f28d7fe7ca464dfbc104258c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856406"
---
# <a name="install-paid-or-licensed-custom-components-for-the-azure-ssis-integration-runtime"></a><span data-ttu-id="7ea5d-103">Install paid or licensed custom components for the Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="7ea5d-103">Install paid or licensed custom components for the Azure-SSIS integration runtime</span></span>

<span data-ttu-id="7ea5d-104">This article describes how an ISV can develop and install paid or licensed custom components for SQL Server Integration Services (SSIS) packages that run in Azure in the Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-104">This article describes how an ISV can develop and install paid or licensed custom components for SQL Server Integration Services (SSIS) packages that run in Azure in the Azure-SSIS integration runtime.</span></span>

## <a name="the-problem"></a><span data-ttu-id="7ea5d-105">The problem</span><span class="sxs-lookup"><span data-stu-id="7ea5d-105">The problem</span></span>

<span data-ttu-id="7ea5d-106">The nature of the Azure-SSIS integration runtime presents several challenges, which make the typical licensing methods used for the on-premises installation of custom components inadequate.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-106">The nature of the Azure-SSIS integration runtime presents several challenges, which make the typical licensing methods used for the on-premises installation of custom components inadequate.</span></span> <span data-ttu-id="7ea5d-107">As a result, the Azure-SSIS IR requires a different approach.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-107">As a result, the Azure-SSIS IR requires a different approach.</span></span>

-   <span data-ttu-id="7ea5d-108">The nodes of the Azure-SSIS IR are volatile and can be allocated or released at any time.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-108">The nodes of the Azure-SSIS IR are volatile and can be allocated or released at any time.</span></span> <span data-ttu-id="7ea5d-109">For example, you can start or stop nodes to manage the cost, or scale up and down through various node sizes.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-109">For example, you can start or stop nodes to manage the cost, or scale up and down through various node sizes.</span></span> <span data-ttu-id="7ea5d-110">As a result, binding a third-party component license to a particular node by using machine-specific info such as MAC address or CPU ID is no longer viable.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-110">As a result, binding a third-party component license to a particular node by using machine-specific info such as MAC address or CPU ID is no longer viable.</span></span>

-   <span data-ttu-id="7ea5d-111">You can also scale the Azure-SSIS IR in or out, so that the number of nodes can shrink or expand at any time.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-111">You can also scale the Azure-SSIS IR in or out, so that the number of nodes can shrink or expand at any time.</span></span>

## <a name="the-solution"></a><span data-ttu-id="7ea5d-112">The solution</span><span class="sxs-lookup"><span data-stu-id="7ea5d-112">The solution</span></span>

<span data-ttu-id="7ea5d-113">As a result of the limitations of traditional licensing methods described in the previous section, the Azure-SSIS IR provides a new solution.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-113">As a result of the limitations of traditional licensing methods described in the previous section, the Azure-SSIS IR provides a new solution.</span></span> <span data-ttu-id="7ea5d-114">This solution uses Windows environment variables and SSIS system variables for the license binding and validation of third-party components.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-114">This solution uses Windows environment variables and SSIS system variables for the license binding and validation of third-party components.</span></span> <span data-ttu-id="7ea5d-115">ISVs can use these variables to obtain unique and persistent info for an Azure-SSIS IR, such as Cluster ID and Cluster Node Count.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-115">ISVs can use these variables to obtain unique and persistent info for an Azure-SSIS IR, such as Cluster ID and Cluster Node Count.</span></span> <span data-ttu-id="7ea5d-116">With this info, ISVs can then bind the license for their component to an Azure-SSIS IR *as a cluster*.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-116">With this info, ISVs can then bind the license for their component to an Azure-SSIS IR *as a cluster*.</span></span> <span data-ttu-id="7ea5d-117">This binding uses an ID that doesn't change when customers start or stop, scale up or down, scale in or out, or reconfigure the Azure-SSIS IR in any way.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-117">This binding uses an ID that doesn't change when customers start or stop, scale up or down, scale in or out, or reconfigure the Azure-SSIS IR in any way.</span></span>

<span data-ttu-id="7ea5d-118">The following diagram shows the typical installation, activation and license binding, and validation flows for third-party components that use these new variables:</span><span class="sxs-lookup"><span data-stu-id="7ea5d-118">The following diagram shows the typical installation, activation and license binding, and validation flows for third-party components that use these new variables:</span></span>

![Installation of licensed components](media/how-to-configure-azure-ssis-ir-licensed-components/licensed-component-installation.png)

## <a name="instructions"></a><span data-ttu-id="7ea5d-120">Instructions</span><span class="sxs-lookup"><span data-stu-id="7ea5d-120">Instructions</span></span>
1. <span data-ttu-id="7ea5d-121">ISVs can offer their licensed components in various SKUs or tiers (for example, single node, up to 5 nodes, up to 10 nodes, and so forth).</span><span class="sxs-lookup"><span data-stu-id="7ea5d-121">ISVs can offer their licensed components in various SKUs or tiers (for example, single node, up to 5 nodes, up to 10 nodes, and so forth).</span></span> <span data-ttu-id="7ea5d-122">The ISV provides the corresponding Product Key when customers purchase a product.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-122">The ISV provides the corresponding Product Key when customers purchase a product.</span></span> <span data-ttu-id="7ea5d-123">The ISV can also provide an Azure Storage blob container that contains an ISV Setup script and associated files.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-123">The ISV can also provide an Azure Storage blob container that contains an ISV Setup script and associated files.</span></span> <span data-ttu-id="7ea5d-124">Customers can copy these files into their own storage container and modify them with their own Product Key (for example, by running `IsvSetup.exe -pid xxxx-xxxx-xxxx`).</span><span class="sxs-lookup"><span data-stu-id="7ea5d-124">Customers can copy these files into their own storage container and modify them with their own Product Key (for example, by running `IsvSetup.exe -pid xxxx-xxxx-xxxx`).</span></span> <span data-ttu-id="7ea5d-125">Customers can then provision or reconfigure the Azure-SSIS IR with the SAS URI of their container as parameter.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-125">Customers can then provision or reconfigure the Azure-SSIS IR with the SAS URI of their container as parameter.</span></span> <span data-ttu-id="7ea5d-126">For more info, see [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md).</span><span class="sxs-lookup"><span data-stu-id="7ea5d-126">For more info, see [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md).</span></span>

2. <span data-ttu-id="7ea5d-127">When the Azure-SSIS IR is provisioned or reconfigured, ISV Setup runs on each node to query the Windows environment variables, `SSIS_CLUSTERID` and `SSIS_CLUSTERNODECOUNT`.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-127">When the Azure-SSIS IR is provisioned or reconfigured, ISV Setup runs on each node to query the Windows environment variables, `SSIS_CLUSTERID` and `SSIS_CLUSTERNODECOUNT`.</span></span> <span data-ttu-id="7ea5d-128">Then the Azure-SSIS IR submits its Cluster ID and the Product Key for the licensed product to the ISV Activation Server to generate an Activation Key.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-128">Then the Azure-SSIS IR submits its Cluster ID and the Product Key for the licensed product to the ISV Activation Server to generate an Activation Key.</span></span>

3. <span data-ttu-id="7ea5d-129">After receiving the Activation Key, ISV Setup can store the key locally on each node (for example, in the Registry).</span><span class="sxs-lookup"><span data-stu-id="7ea5d-129">After receiving the Activation Key, ISV Setup can store the key locally on each node (for example, in the Registry).</span></span>

4. <span data-ttu-id="7ea5d-130">When customers run a package that uses the ISV's licensed component on a node of the Azure-SSIS IR, the package reads the locally stored Activation Key and validates it against the node's Cluster ID.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-130">When customers run a package that uses the ISV's licensed component on a node of the Azure-SSIS IR, the package reads the locally stored Activation Key and validates it against the node's Cluster ID.</span></span> <span data-ttu-id="7ea5d-131">The package can also optionally report the Cluster Node Count to the ISV activation server.</span><span class="sxs-lookup"><span data-stu-id="7ea5d-131">The package can also optionally report the Cluster Node Count to the ISV activation server.</span></span>

    <span data-ttu-id="7ea5d-132">Here is an example of code that validates the activation key and reports the cluster node count:</span><span class="sxs-lookup"><span data-stu-id="7ea5d-132">Here is an example of code that validates the activation key and reports the cluster node count:</span></span>

    ```csharp
    public override DTSExecResult Validate(Connections, VariableDispenser, IDTSComponentEvents componentEvents, IDTSLogging log) 
                                                                                                                               
    {                                                                                                                             
                                                                                                                               
    Variables vars = null;                                                                                                        
                                                                                                                               
    variableDispenser.LockForRead("System::ClusterID");                                                                           
                                                                                                                               
    variableDispenser.LockForRead("System::ClusterNodeCount");                                                                    
                                                                                                                               
    variableDispenser.GetVariables(ref vars);                                                                                     
                                                                                                                               
    // Validate Activation Key with ClusterID                                                                                     
                                                                                                                               
    // Report on ClusterNodeCount                                                                                                 
                                                                                                                               
    vars.Unlock();                                                                                                                
                                                                                                                               
    return base.Validate(connections, variableDispenser, componentEvents, log);                                                   
                                                                                                                               
    }
    ```

## <a name="isv-partners"></a><span data-ttu-id="7ea5d-133">ISV partners</span><span class="sxs-lookup"><span data-stu-id="7ea5d-133">ISV partners</span></span>

<span data-ttu-id="7ea5d-134">You can find a list of ISV partners who have adapted their components and extensions for the Azure-SSIS IR at the end of this blog post - [Enterprise Edition, Custom Setup, and 3rd Party Extensibility for SSIS in ADF](https://blogs.msdn.microsoft.com/ssis/2018/04/27/enterprise-edition-custom-setup-and-3rd-party-extensibility-for-ssis-in-adf/).</span><span class="sxs-lookup"><span data-stu-id="7ea5d-134">You can find a list of ISV partners who have adapted their components and extensions for the Azure-SSIS IR at the end of this blog post - [Enterprise Edition, Custom Setup, and 3rd Party Extensibility for SSIS in ADF](https://blogs.msdn.microsoft.com/ssis/2018/04/27/enterprise-edition-custom-setup-and-3rd-party-extensibility-for-ssis-in-adf/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ea5d-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ea5d-135">Next steps</span></span>

-   [<span data-ttu-id="7ea5d-136">Custom setup for the Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="7ea5d-136">Custom setup for the Azure-SSIS integration runtime</span></span>](how-to-configure-azure-ssis-ir-custom-setup.md)

-   [<span data-ttu-id="7ea5d-137">Enterprise Edition of the Azure-SSIS Integration Runtime</span><span class="sxs-lookup"><span data-stu-id="7ea5d-137">Enterprise Edition of the Azure-SSIS Integration Runtime</span></span>](how-to-configure-azure-ssis-ir-enterprise-edition.md)
