---
title: Manage a Machine Learning workspace | Microsoft Docs
description: Manage access to Azure Machine Learning workspaces, and deploy and manage ML API web services
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7692360ddf2fb7638eebf326b6354c81f6f5ae99
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562743"
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="2dc73-103">Manage an Azure Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="2dc73-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="2dc73-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="2dc73-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="2dc73-105">You can manage Machine Learning workspaces in either the Azure portal or the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="2dc73-105">You can manage Machine Learning workspaces in either the Azure portal or the Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-the-azure-portal"></a><span data-ttu-id="2dc73-106">Use the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2dc73-106">Use the Azure portal</span></span>

<span data-ttu-id="2dc73-107">To manage a workspace in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="2dc73-107">To manage a workspace in the Azure portal:</span></span>

1. <span data-ttu-id="2dc73-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span><span class="sxs-lookup"><span data-stu-id="2dc73-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="2dc73-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span><span class="sxs-lookup"><span data-stu-id="2dc73-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="2dc73-110">Click the workspace you want to manage.</span><span class="sxs-lookup"><span data-stu-id="2dc73-110">Click the workspace you want to manage.</span></span>

<span data-ttu-id="2dc73-111">In addition to the standard resource management information and options available, you can:</span><span class="sxs-lookup"><span data-stu-id="2dc73-111">In addition to the standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="2dc73-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span><span class="sxs-lookup"><span data-stu-id="2dc73-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="2dc73-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span><span class="sxs-lookup"><span data-stu-id="2dc73-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span></span> <span data-ttu-id="2dc73-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span><span class="sxs-lookup"><span data-stu-id="2dc73-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span></span>

<span data-ttu-id="2dc73-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="2dc73-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span></span> <span data-ttu-id="2dc73-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span><span class="sxs-lookup"><span data-stu-id="2dc73-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="2dc73-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span><span class="sxs-lookup"><span data-stu-id="2dc73-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="2dc73-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span><span class="sxs-lookup"><span data-stu-id="2dc73-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="2dc73-119">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="2dc73-119">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="2dc73-120">Use the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="2dc73-120">Use the Azure classic portal</span></span>

<span data-ttu-id="2dc73-121">Using the Azure classic portal, you can manage your Machine Learning workspaces to:</span><span class="sxs-lookup"><span data-stu-id="2dc73-121">Using the Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="2dc73-122">Monitor how the workspace is being used</span><span class="sxs-lookup"><span data-stu-id="2dc73-122">Monitor how the workspace is being used</span></span>
* <span data-ttu-id="2dc73-123">Configure the workspace to allow or deny access</span><span class="sxs-lookup"><span data-stu-id="2dc73-123">Configure the workspace to allow or deny access</span></span>
* <span data-ttu-id="2dc73-124">Manage Web services created in the workspace</span><span class="sxs-lookup"><span data-stu-id="2dc73-124">Manage Web services created in the workspace</span></span>
* <span data-ttu-id="2dc73-125">Delete the workspace</span><span class="sxs-lookup"><span data-stu-id="2dc73-125">Delete the workspace</span></span>

<span data-ttu-id="2dc73-126">In addition, the dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span><span class="sxs-lookup"><span data-stu-id="2dc73-126">In addition, the dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="2dc73-127">In Azure Machine Learning Studio, on the **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span><span class="sxs-lookup"><span data-stu-id="2dc73-127">In Azure Machine Learning Studio, on the **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="2dc73-128">To manage a workspace in the Azure classic portal:</span><span class="sxs-lookup"><span data-stu-id="2dc73-128">To manage a workspace in the Azure classic portal:</span></span>

1. <span data-ttu-id="2dc73-129">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2dc73-129">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="2dc73-130">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span><span class="sxs-lookup"><span data-stu-id="2dc73-130">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="2dc73-131">Click the workspace you want to manage.</span><span class="sxs-lookup"><span data-stu-id="2dc73-131">Click the workspace you want to manage.</span></span>

<span data-ttu-id="2dc73-132">The workspace page has three tabs:</span><span class="sxs-lookup"><span data-stu-id="2dc73-132">The workspace page has three tabs:</span></span>

* <span data-ttu-id="2dc73-133">**DASHBOARD** - Allows you to view workspace usage and information</span><span class="sxs-lookup"><span data-stu-id="2dc73-133">**DASHBOARD** - Allows you to view workspace usage and information</span></span>
* <span data-ttu-id="2dc73-134">**CONFIGURE** - Allows you to manage access to the workspace</span><span class="sxs-lookup"><span data-stu-id="2dc73-134">**CONFIGURE** - Allows you to manage access to the workspace</span></span>
* <span data-ttu-id="2dc73-135">**WEB SERVICES** - Allows you to manage Web services that have been published from this workspace</span><span class="sxs-lookup"><span data-stu-id="2dc73-135">**WEB SERVICES** - Allows you to manage Web services that have been published from this workspace</span></span>

### <a name="to-monitor-how-the-workspace-is-being-used"></a><span data-ttu-id="2dc73-136">To monitor how the workspace is being used</span><span class="sxs-lookup"><span data-stu-id="2dc73-136">To monitor how the workspace is being used</span></span>
<span data-ttu-id="2dc73-137">Click the **DASHBOARD** tab.</span><span class="sxs-lookup"><span data-stu-id="2dc73-137">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="2dc73-138">From the dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span><span class="sxs-lookup"><span data-stu-id="2dc73-138">From the dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="2dc73-139">The **COMPUTE** chart shows the compute resources being used by the workspace.</span><span class="sxs-lookup"><span data-stu-id="2dc73-139">The **COMPUTE** chart shows the compute resources being used by the workspace.</span></span> <span data-ttu-id="2dc73-140">You can change the view to display relative or absolute values, and you can change the timeframe displayed in the chart.</span><span class="sxs-lookup"><span data-stu-id="2dc73-140">You can change the view to display relative or absolute values, and you can change the timeframe displayed in the chart.</span></span>
* <span data-ttu-id="2dc73-141">**Usage overview** displays Azure storage being used by the workspace.</span><span class="sxs-lookup"><span data-stu-id="2dc73-141">**Usage overview** displays Azure storage being used by the workspace.</span></span>
* <span data-ttu-id="2dc73-142">**Quick glance** provides a summary of workspace information and useful links.</span><span class="sxs-lookup"><span data-stu-id="2dc73-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="2dc73-143">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span><span class="sxs-lookup"><span data-stu-id="2dc73-143">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="2dc73-144">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span><span class="sxs-lookup"><span data-stu-id="2dc73-144">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span></span> <span data-ttu-id="2dc73-145">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span><span class="sxs-lookup"><span data-stu-id="2dc73-145">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span>
> 
> 

### <a name="to-grant-or-suspend-access-for-users"></a><span data-ttu-id="2dc73-146">To grant or suspend access for users</span><span class="sxs-lookup"><span data-stu-id="2dc73-146">To grant or suspend access for users</span></span>
<span data-ttu-id="2dc73-147">Click the **CONFIGURE** tab.</span><span class="sxs-lookup"><span data-stu-id="2dc73-147">Click the **CONFIGURE** tab.</span></span>

<span data-ttu-id="2dc73-148">From the configuration tab you can:</span><span class="sxs-lookup"><span data-stu-id="2dc73-148">From the configuration tab you can:</span></span>

* <span data-ttu-id="2dc73-149">Suspend access to the Machine Learning workspace by clicking DENY.</span><span class="sxs-lookup"><span data-stu-id="2dc73-149">Suspend access to the Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="2dc73-150">Users will no longer be able to open the workspace in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="2dc73-150">Users will no longer be able to open the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="2dc73-151">To restore access, click ALLOW.</span><span class="sxs-lookup"><span data-stu-id="2dc73-151">To restore access, click ALLOW.</span></span>

<span data-ttu-id="2dc73-152">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab (see the preceeding note regarding **Sign-in to ML Studio**).</span><span class="sxs-lookup"><span data-stu-id="2dc73-152">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab (see the preceeding note regarding **Sign-in to ML Studio**).</span></span> <span data-ttu-id="2dc73-153">This opens the workspace in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="2dc73-153">This opens the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="2dc73-154">From here, click the **SETTINGS** tab and then **USERS**.</span><span class="sxs-lookup"><span data-stu-id="2dc73-154">From here, click the **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="2dc73-155">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span><span class="sxs-lookup"><span data-stu-id="2dc73-155">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span></span>

### <a name="to-manage-web-services-in-this-workspace"></a><span data-ttu-id="2dc73-156">To manage web services in this workspace</span><span class="sxs-lookup"><span data-stu-id="2dc73-156">To manage web services in this workspace</span></span>
<span data-ttu-id="2dc73-157">Click the **WEB SERVICES** tab.</span><span class="sxs-lookup"><span data-stu-id="2dc73-157">Click the **WEB SERVICES** tab.</span></span>

<span data-ttu-id="2dc73-158">This displays a list of web services published from this workspace.</span><span class="sxs-lookup"><span data-stu-id="2dc73-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="2dc73-159">To manage a web service, click the name in the list to open the Web service page.</span><span class="sxs-lookup"><span data-stu-id="2dc73-159">To manage a web service, click the name in the list to open the Web service page.</span></span>

<span data-ttu-id="2dc73-160">A Web service may have one or more endpoints defined.</span><span class="sxs-lookup"><span data-stu-id="2dc73-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="2dc73-161">You can define more endpoints in addition to the "Default" endpoint.</span><span class="sxs-lookup"><span data-stu-id="2dc73-161">You can define more endpoints in addition to the "Default" endpoint.</span></span> <span data-ttu-id="2dc73-162">To add the endpoint, click **Manage Endpoints** at the bottom of the dashboard to open the Azure Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="2dc73-162">To add the endpoint, click **Manage Endpoints** at the bottom of the dashboard to open the Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="2dc73-163">To delete an endpoint (you cannot delete the "Default" endpoint), click the check box at the beginning of the endpoint row, and click **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="2dc73-163">To delete an endpoint (you cannot delete the "Default" endpoint), click the check box at the beginning of the endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="2dc73-164">This removes the endpoint from the Web service.</span><span class="sxs-lookup"><span data-stu-id="2dc73-164">This removes the endpoint from the Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2dc73-165">If an application is using the web service endpoint when the endpoint is deleted, the application will receive an error the next time it tries to access the service.</span><span class="sxs-lookup"><span data-stu-id="2dc73-165">If an application is using the web service endpoint when the endpoint is deleted, the application will receive an error the next time it tries to access the service.</span></span>
  > 
  > 

<span data-ttu-id="2dc73-166">Click the name of a Web service endpoint to open it.</span><span class="sxs-lookup"><span data-stu-id="2dc73-166">Click the name of a Web service endpoint to open it.</span></span> 

<span data-ttu-id="2dc73-167">From the dashboard, you can view overall usage of your Web service over a period of time.</span><span class="sxs-lookup"><span data-stu-id="2dc73-167">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="2dc73-168">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span><span class="sxs-lookup"><span data-stu-id="2dc73-168">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="2dc73-169">The dashboard shows the following information:</span><span class="sxs-lookup"><span data-stu-id="2dc73-169">The dashboard shows the following information:</span></span>

* <span data-ttu-id="2dc73-170">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span><span class="sxs-lookup"><span data-stu-id="2dc73-170">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="2dc73-171">It can help identify if you are experiencing spikes in usage.</span><span class="sxs-lookup"><span data-stu-id="2dc73-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="2dc73-172">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span><span class="sxs-lookup"><span data-stu-id="2dc73-172">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="2dc73-173">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span><span class="sxs-lookup"><span data-stu-id="2dc73-173">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="2dc73-174">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span><span class="sxs-lookup"><span data-stu-id="2dc73-174">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="2dc73-175">**Average Job Latency** displays an average of the time needed to execute the received requests.</span><span class="sxs-lookup"><span data-stu-id="2dc73-175">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="2dc73-176">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span><span class="sxs-lookup"><span data-stu-id="2dc73-176">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="2dc73-177">**Services Costs** displays the charges for the billing plan associated with the service.</span><span class="sxs-lookup"><span data-stu-id="2dc73-177">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

<span data-ttu-id="2dc73-178">From the Configure page, you can update the following properties:</span><span class="sxs-lookup"><span data-stu-id="2dc73-178">From the Configure page, you can update the following properties:</span></span>

* <span data-ttu-id="2dc73-179">**Description** allows you to enter a description for the Web service.</span><span class="sxs-lookup"><span data-stu-id="2dc73-179">**Description** allows you to enter a description for the Web service.</span></span> <span data-ttu-id="2dc73-180">Description is a required field.</span><span class="sxs-lookup"><span data-stu-id="2dc73-180">Description is a required field.</span></span>
* <span data-ttu-id="2dc73-181">**Logging** allows you to enable or disable error logging on the endpoint.</span><span class="sxs-lookup"><span data-stu-id="2dc73-181">**Logging** allows you to enable or disable error logging on the endpoint.</span></span> <span data-ttu-id="2dc73-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="2dc73-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="2dc73-183">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span><span class="sxs-lookup"><span data-stu-id="2dc73-183">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="2dc73-184">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span><span class="sxs-lookup"><span data-stu-id="2dc73-184">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="2dc73-185">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span><span class="sxs-lookup"><span data-stu-id="2dc73-185">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

