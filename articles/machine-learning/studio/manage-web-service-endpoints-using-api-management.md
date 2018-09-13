---
title: Learn how to manage AzureML web services using API Management | Microsoft Docs
description: A guide showing how to manage AzureML web services using API Management.
keywords: machine learning,api management
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/03/2017
ms.openlocfilehash: 4ca551ed07447e41ec94b0334eac0d235e0a5b6f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871681"
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="e1d62-104">Learn how to manage AzureML web services using API Management</span><span class="sxs-lookup"><span data-stu-id="e1d62-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="e1d62-105">Overview</span><span class="sxs-lookup"><span data-stu-id="e1d62-105">Overview</span></span>
<span data-ttu-id="e1d62-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span><span class="sxs-lookup"><span data-stu-id="e1d62-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="e1d62-107">What is Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="e1d62-107">What is Azure API Management?</span></span>
<span data-ttu-id="e1d62-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span><span class="sxs-lookup"><span data-stu-id="e1d62-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="e1d62-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="e1d62-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="e1d62-110">Click [here](../../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="e1d62-110">Click [here](../../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="e1d62-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span><span class="sxs-lookup"><span data-stu-id="e1d62-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="e1d62-112">What is AzureML?</span><span class="sxs-lookup"><span data-stu-id="e1d62-112">What is AzureML?</span></span>
<span data-ttu-id="e1d62-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="e1d62-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="e1d62-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span><span class="sxs-lookup"><span data-stu-id="e1d62-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1d62-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e1d62-115">Prerequisites</span></span>
<span data-ttu-id="e1d62-116">To complete this guide, you need:</span><span class="sxs-lookup"><span data-stu-id="e1d62-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="e1d62-117">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="e1d62-117">An Azure account.</span></span> <span data-ttu-id="e1d62-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span><span class="sxs-lookup"><span data-stu-id="e1d62-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="e1d62-119">An AzureML account.</span><span class="sxs-lookup"><span data-stu-id="e1d62-119">An AzureML account.</span></span> <span data-ttu-id="e1d62-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span><span class="sxs-lookup"><span data-stu-id="e1d62-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="e1d62-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span><span class="sxs-lookup"><span data-stu-id="e1d62-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="e1d62-122">Click [here](create-experiment.md) for details on how to create an AzureML experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-122">Click [here](create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="e1d62-123">Click [here](publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span><span class="sxs-lookup"><span data-stu-id="e1d62-123">Click [here](publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="e1d62-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span><span class="sxs-lookup"><span data-stu-id="e1d62-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="e1d62-125">Create an API Management instance</span><span class="sxs-lookup"><span data-stu-id="e1d62-125">Create an API Management instance</span></span>

<span data-ttu-id="e1d62-126">You can manage your Azure Machine Learning web service with an API Management instance.</span><span class="sxs-lookup"><span data-stu-id="e1d62-126">You can manage your Azure Machine Learning web service with an API Management instance.</span></span>

1. <span data-ttu-id="e1d62-127">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1d62-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e1d62-128">Select **+ Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-128">Select **+ Create a resource**.</span></span>
3. <span data-ttu-id="e1d62-129">In the search box, type "API management", then select the "API management" resource.</span><span class="sxs-lookup"><span data-stu-id="e1d62-129">In the search box, type "API management", then select the "API management" resource.</span></span>
4. <span data-ttu-id="e1d62-130">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-130">Click **Create**.</span></span>
5. <span data-ttu-id="e1d62-131">The **Name** value will be used to create a unique URL (this example uses "demoazureml").</span><span class="sxs-lookup"><span data-stu-id="e1d62-131">The **Name** value will be used to create a unique URL (this example uses "demoazureml").</span></span>
6. <span data-ttu-id="e1d62-132">Select a **Subscription**, **Resource group**, and **Location** for your service instance.</span><span class="sxs-lookup"><span data-stu-id="e1d62-132">Select a **Subscription**, **Resource group**, and **Location** for your service instance.</span></span>
7. <span data-ttu-id="e1d62-133">Specify a value for **Organization name** (this example uses "demoazureml").</span><span class="sxs-lookup"><span data-stu-id="e1d62-133">Specify a value for **Organization name** (this example uses "demoazureml").</span></span>
8. <span data-ttu-id="e1d62-134">Enter your **Administrator email** - this email will be used for notifications from the API Management system.</span><span class="sxs-lookup"><span data-stu-id="e1d62-134">Enter your **Administrator email** - this email will be used for notifications from the API Management system.</span></span>
9. <span data-ttu-id="e1d62-135">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-135">Click **Create**.</span></span>

<span data-ttu-id="e1d62-136">It may take up to 30 minutes for a new service to be created.</span><span class="sxs-lookup"><span data-stu-id="e1d62-136">It may take up to 30 minutes for a new service to be created.</span></span>

![create-service](./media/manage-web-service-endpoints-using-api-management/create-service.png)


## <a name="create-the-api"></a><span data-ttu-id="e1d62-138">Create the API</span><span class="sxs-lookup"><span data-stu-id="e1d62-138">Create the API</span></span>
<span data-ttu-id="e1d62-139">Once the service instance is created, the next step is to create the API.</span><span class="sxs-lookup"><span data-stu-id="e1d62-139">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="e1d62-140">An API consists of a set of operations that can be invoked from a client application.</span><span class="sxs-lookup"><span data-stu-id="e1d62-140">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="e1d62-141">API operations are proxied to existing web services.</span><span class="sxs-lookup"><span data-stu-id="e1d62-141">API operations are proxied to existing web services.</span></span> <span data-ttu-id="e1d62-142">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span><span class="sxs-lookup"><span data-stu-id="e1d62-142">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="e1d62-143">To create the API:</span><span class="sxs-lookup"><span data-stu-id="e1d62-143">To create the API:</span></span>

1. <span data-ttu-id="e1d62-144">In the Azure portal, open the service instance you just created.</span><span class="sxs-lookup"><span data-stu-id="e1d62-144">In the Azure portal, open the service instance you just created.</span></span>
2. <span data-ttu-id="e1d62-145">In the left navigation pane, select **APIs**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-145">In the left navigation pane, select **APIs**.</span></span>

   ![api-management-menu](./media/manage-web-service-endpoints-using-api-management/api-management.png)

1. <span data-ttu-id="e1d62-147">Click **Add API**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-147">Click **Add API**.</span></span>
2. <span data-ttu-id="e1d62-148">Enter a **Web API name** (this example uses "AzureML Demo API").</span><span class="sxs-lookup"><span data-stu-id="e1d62-148">Enter a **Web API name** (this example uses "AzureML Demo API").</span></span>
3. <span data-ttu-id="e1d62-149">For **Web service URL**, enter "`https://ussouthcentral.services.azureml.net`".</span><span class="sxs-lookup"><span data-stu-id="e1d62-149">For **Web service URL**, enter "`https://ussouthcentral.services.azureml.net`".</span></span>
4. <span data-ttu-id="e1d62-150">Enter a \*\*Web API URL suffix".</span><span class="sxs-lookup"><span data-stu-id="e1d62-150">Enter a \*\*Web API URL suffix".</span></span> <span data-ttu-id="e1d62-151">This will become the last part of the URL that customers will use for sending requests to the service instance (this example uses "azureml-demo").</span><span class="sxs-lookup"><span data-stu-id="e1d62-151">This will become the last part of the URL that customers will use for sending requests to the service instance (this example uses "azureml-demo").</span></span>
5. <span data-ttu-id="e1d62-152">For **Web API URL scheme**, select **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-152">For **Web API URL scheme**, select **HTTPS**.</span></span>
6. <span data-ttu-id="e1d62-153">For **Products**, select **Starter**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-153">For **Products**, select **Starter**.</span></span>
7. <span data-ttu-id="e1d62-154">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-154">Click **Save**.</span></span>


## <a name="add-the-operations"></a><span data-ttu-id="e1d62-155">Add the operations</span><span class="sxs-lookup"><span data-stu-id="e1d62-155">Add the operations</span></span>

<span data-ttu-id="e1d62-156">Operations are added and configured to an API in the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="e1d62-156">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="e1d62-157">To access the publisher portal, click **Publisher portal** in the Azure portal for your API Management service, select **APIs**, **Operations**, then click **Add operation**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-157">To access the publisher portal, click **Publisher portal** in the Azure portal for your API Management service, select **APIs**, **Operations**, then click **Add operation**.</span></span>

![add-operation](./media/manage-web-service-endpoints-using-api-management/add-an-operation.png)

<span data-ttu-id="e1d62-159">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span><span class="sxs-lookup"><span data-stu-id="e1d62-159">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="e1d62-160">Add RRS Operation</span><span class="sxs-lookup"><span data-stu-id="e1d62-160">Add RRS Operation</span></span>
<span data-ttu-id="e1d62-161">First create an operation for the AzureML RRS service:</span><span class="sxs-lookup"><span data-stu-id="e1d62-161">First create an operation for the AzureML RRS service:</span></span>

1. <span data-ttu-id="e1d62-162">For the **HTTP verb**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-162">For the **HTTP verb**, select **POST**.</span></span>
2. <span data-ttu-id="e1d62-163">For the **URL template**, type "`/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}`".</span><span class="sxs-lookup"><span data-stu-id="e1d62-163">For the **URL template**, type "`/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}`".</span></span>
3. <span data-ttu-id="e1d62-164">Enter a **Display name** (this example uses "RRS Execute").</span><span class="sxs-lookup"><span data-stu-id="e1d62-164">Enter a **Display name** (this example uses "RRS Execute").</span></span>

   ![add-rrs-operation-signature](./media/manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

4. <span data-ttu-id="e1d62-166">Click **Responses** > **ADD** on the left and select **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-166">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span>
5. <span data-ttu-id="e1d62-167">Click **Save** to save this operation.</span><span class="sxs-lookup"><span data-stu-id="e1d62-167">Click **Save** to save this operation.</span></span>

   ![add-rrs-operation-response](./media/manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="e1d62-169">Add BES Operations</span><span class="sxs-lookup"><span data-stu-id="e1d62-169">Add BES Operations</span></span>

> [!NOTE]
> <span data-ttu-id="e1d62-170">Screenshots are not included here for the BES operations as they are very similar to those for adding the RRS operation.</span><span class="sxs-lookup"><span data-stu-id="e1d62-170">Screenshots are not included here for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="e1d62-171">Submit (but not start) a Batch Execution job</span><span class="sxs-lookup"><span data-stu-id="e1d62-171">Submit (but not start) a Batch Execution job</span></span>

1. <span data-ttu-id="e1d62-172">Click **add operation** to add a BES operation to the API.</span><span class="sxs-lookup"><span data-stu-id="e1d62-172">Click **add operation** to add a BES operation to the API.</span></span>
2. <span data-ttu-id="e1d62-173">For the **HTTP verb**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-173">For the **HTTP verb**, select **POST**.</span></span>
3. <span data-ttu-id="e1d62-174">For the **URL template**, type "`/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}`".</span><span class="sxs-lookup"><span data-stu-id="e1d62-174">For the **URL template**, type "`/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}`".</span></span>
4. <span data-ttu-id="e1d62-175">Enter a **Display name** (this example uses "BES Submit").</span><span class="sxs-lookup"><span data-stu-id="e1d62-175">Enter a **Display name** (this example uses "BES Submit").</span></span>
5. <span data-ttu-id="e1d62-176">Click **Responses** > **ADD** on the left and select **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-176">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span>
6. <span data-ttu-id="e1d62-177">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-177">Click **Save**.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="e1d62-178">Start a Batch Execution job</span><span class="sxs-lookup"><span data-stu-id="e1d62-178">Start a Batch Execution job</span></span>

1. <span data-ttu-id="e1d62-179">Click **add operation** to add a BES operation to the API.</span><span class="sxs-lookup"><span data-stu-id="e1d62-179">Click **add operation** to add a BES operation to the API.</span></span>
2. <span data-ttu-id="e1d62-180">For the **HTTP verb**, select **POST**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-180">For the **HTTP verb**, select **POST**.</span></span>
3. <span data-ttu-id="e1d62-181">For the **HTTP verb**, type "`/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}`".</span><span class="sxs-lookup"><span data-stu-id="e1d62-181">For the **HTTP verb**, type "`/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}`".</span></span>
4. <span data-ttu-id="e1d62-182">Enter a **Display name** (this example uses "BES Start").</span><span class="sxs-lookup"><span data-stu-id="e1d62-182">Enter a **Display name** (this example uses "BES Start").</span></span>
6. <span data-ttu-id="e1d62-183">Click **Responses** > **ADD** on the left and select **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-183">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span>
7. <span data-ttu-id="e1d62-184">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-184">Click **Save**.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="e1d62-185">Get the status or result of a Batch Execution job</span><span class="sxs-lookup"><span data-stu-id="e1d62-185">Get the status or result of a Batch Execution job</span></span>

1. <span data-ttu-id="e1d62-186">Click **add operation** to add a BES operation to the API.</span><span class="sxs-lookup"><span data-stu-id="e1d62-186">Click **add operation** to add a BES operation to the API.</span></span>
2. <span data-ttu-id="e1d62-187">For the **HTTP verb**, select **GET**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-187">For the **HTTP verb**, select **GET**.</span></span>
3. <span data-ttu-id="e1d62-188">For the **URL template**, type "`/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}`".</span><span class="sxs-lookup"><span data-stu-id="e1d62-188">For the **URL template**, type "`/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}`".</span></span>
4. <span data-ttu-id="e1d62-189">Enter a **Display name** (this example uses "BES Status").</span><span class="sxs-lookup"><span data-stu-id="e1d62-189">Enter a **Display name** (this example uses "BES Status").</span></span>
6. <span data-ttu-id="e1d62-190">Click **Responses** > **ADD** on the left and select **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-190">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span>
7. <span data-ttu-id="e1d62-191">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-191">Click **Save**.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="e1d62-192">Delete a Batch Execution job</span><span class="sxs-lookup"><span data-stu-id="e1d62-192">Delete a Batch Execution job</span></span>

1. <span data-ttu-id="e1d62-193">Click **add operation** to add a BES operation to the API.</span><span class="sxs-lookup"><span data-stu-id="e1d62-193">Click **add operation** to add a BES operation to the API.</span></span>
2. <span data-ttu-id="e1d62-194">For the **HTTP verb**, select **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-194">For the **HTTP verb**, select **DELETE**.</span></span>
3. <span data-ttu-id="e1d62-195">For the **URL template**, type "`/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}`".</span><span class="sxs-lookup"><span data-stu-id="e1d62-195">For the **URL template**, type "`/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}`".</span></span>
4. <span data-ttu-id="e1d62-196">Enter a **Display name** (this example uses "BES Delete").</span><span class="sxs-lookup"><span data-stu-id="e1d62-196">Enter a **Display name** (this example uses "BES Delete").</span></span>
5. <span data-ttu-id="e1d62-197">Click **Responses** > **ADD** on the left and select **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-197">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span>
6. <span data-ttu-id="e1d62-198">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-198">Click **Save**.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="e1d62-199">Call an operation from the Developer portal</span><span class="sxs-lookup"><span data-stu-id="e1d62-199">Call an operation from the Developer portal</span></span>

<span data-ttu-id="e1d62-200">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="e1d62-200">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="e1d62-201">In this step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-201">In this step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> 

1. <span data-ttu-id="e1d62-202">Click **Developer portal**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-202">Click **Developer portal**.</span></span>

   ![developer-portal](./media/manage-web-service-endpoints-using-api-management/developer-portal.png)

2. <span data-ttu-id="e1d62-204">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span><span class="sxs-lookup"><span data-stu-id="e1d62-204">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

   ![demoazureml-api](./media/manage-web-service-endpoints-using-api-management/demoazureml-api.png)

3. <span data-ttu-id="e1d62-206">Select **RRS Execute** for the operation.</span><span class="sxs-lookup"><span data-stu-id="e1d62-206">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="e1d62-207">Click **Try It**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-207">Click **Try It**.</span></span>

   ![try-it](./media/manage-web-service-endpoints-using-api-management/try-it.png)

4. <span data-ttu-id="e1d62-209">For **Request parameters**, type your **workspace** and  **service**, type "2.0 for the **apiversion**, and  "true" for the **details**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-209">For **Request parameters**, type your **workspace** and  **service**, type "2.0 for the **apiversion**, and  "true" for the **details**.</span></span> <span data-ttu-id="e1d62-210">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span><span class="sxs-lookup"><span data-stu-id="e1d62-210">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

   <span data-ttu-id="e1d62-211">For **Request headers**, click **Add header** and type "Content-Type" and "application/json".</span><span class="sxs-lookup"><span data-stu-id="e1d62-211">For **Request headers**, click **Add header** and type "Content-Type" and "application/json".</span></span> <span data-ttu-id="e1d62-212">Click **Add header** again and type "Authorization" and "Bearer *\<your service API-KEY\>*".</span><span class="sxs-lookup"><span data-stu-id="e1d62-212">Click **Add header** again and type "Authorization" and "Bearer *\<your service API-KEY\>*".</span></span> <span data-ttu-id="e1d62-213">You can find your API-KEY in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span><span class="sxs-lookup"><span data-stu-id="e1d62-213">You can find your API-KEY in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

   <span data-ttu-id="e1d62-214">For **Request body**, type `{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}`.</span><span class="sxs-lookup"><span data-stu-id="e1d62-214">For **Request body**, type `{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}`.</span></span>

   ![azureml-demo-api](./media/manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

5. <span data-ttu-id="e1d62-216">Click **Send**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-216">Click **Send**.</span></span>

   ![send](./media/manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="e1d62-218">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-218">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![response-status](./media/manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="e1d62-220">Appendix A - Creating and testing a simple AzureML web service</span><span class="sxs-lookup"><span data-stu-id="e1d62-220">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="e1d62-221">Creating the experiment</span><span class="sxs-lookup"><span data-stu-id="e1d62-221">Creating the experiment</span></span>
<span data-ttu-id="e1d62-222">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span><span class="sxs-lookup"><span data-stu-id="e1d62-222">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="e1d62-223">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span><span class="sxs-lookup"><span data-stu-id="e1d62-223">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="e1d62-224">For example:</span><span class="sxs-lookup"><span data-stu-id="e1d62-224">For example:</span></span>

| <span data-ttu-id="e1d62-225">Text</span><span class="sxs-lookup"><span data-stu-id="e1d62-225">Text</span></span> | <span data-ttu-id="e1d62-226">Hashed Text</span><span class="sxs-lookup"><span data-stu-id="e1d62-226">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="e1d62-227">This is a good day</span><span class="sxs-lookup"><span data-stu-id="e1d62-227">This is a good day</span></span> |<span data-ttu-id="e1d62-228">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="e1d62-228">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="e1d62-229">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span><span class="sxs-lookup"><span data-stu-id="e1d62-229">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="e1d62-230">Next, create a new blank experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-230">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="e1d62-232">Rename it to **SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-232">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="e1d62-233">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-233">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="e1d62-235">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-235">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="e1d62-236">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-236">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![select-columns](./media/manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="e1d62-238">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-238">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="e1d62-239">Click the checkmark to apply these changes.</span><span class="sxs-lookup"><span data-stu-id="e1d62-239">Click the checkmark to apply these changes.</span></span>

![select-columns](./media/manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="e1d62-241">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-241">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="e1d62-242">Connect **Select Columns in Dataset** to **Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-242">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![connect-project-columns](./media/manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="e1d62-244">Type **3** for the **Hashing bitsize**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-244">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="e1d62-245">This will create 8 (23) columns.</span><span class="sxs-lookup"><span data-stu-id="e1d62-245">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="e1d62-247">At this point, you may want to click **Run** to test the experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-247">At this point, you may want to click **Run** to test the experiment.</span></span>

![run](./media/manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="e1d62-249">Create a web service</span><span class="sxs-lookup"><span data-stu-id="e1d62-249">Create a web service</span></span>
<span data-ttu-id="e1d62-250">Now create a web service.</span><span class="sxs-lookup"><span data-stu-id="e1d62-250">Now create a web service.</span></span> <span data-ttu-id="e1d62-251">Expand **Web Service** and drag **Input** onto your experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-251">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="e1d62-252">Connect **Input** to **Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-252">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="e1d62-253">Also drag **output** onto your experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-253">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="e1d62-254">Connect **Output** to **Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-254">Connect **Output** to **Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="e1d62-256">Click **Publish web service**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-256">Click **Publish web service**.</span></span>

![publish-web-service](./media/manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="e1d62-258">Click **Yes** to publish the experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-258">Click **Yes** to publish the experiment.</span></span>

![yes-to-publish](./media/manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="e1d62-260">Test the web service</span><span class="sxs-lookup"><span data-stu-id="e1d62-260">Test the web service</span></span>
<span data-ttu-id="e1d62-261">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span><span class="sxs-lookup"><span data-stu-id="e1d62-261">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="e1d62-262">RSS is for synchronous execution.</span><span class="sxs-lookup"><span data-stu-id="e1d62-262">RSS is for synchronous execution.</span></span> <span data-ttu-id="e1d62-263">BES is for asynchronous job execution.</span><span class="sxs-lookup"><span data-stu-id="e1d62-263">BES is for asynchronous job execution.</span></span> <span data-ttu-id="e1d62-264">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="e1d62-264">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../../python-how-to-install.md)).</span></span>

<span data-ttu-id="e1d62-265">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span><span class="sxs-lookup"><span data-stu-id="e1d62-265">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="e1d62-266">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span><span class="sxs-lookup"><span data-stu-id="e1d62-266">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![find-workspace-and-service](./media/manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="e1d62-268">You can find the **api_key** by clicking your experiment in the web service dashboard.</span><span class="sxs-lookup"><span data-stu-id="e1d62-268">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![find-api-key](./media/manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="e1d62-270">Test RRS endpoint</span><span class="sxs-lookup"><span data-stu-id="e1d62-270">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="e1d62-271">Test button</span><span class="sxs-lookup"><span data-stu-id="e1d62-271">Test button</span></span>
<span data-ttu-id="e1d62-272">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span><span class="sxs-lookup"><span data-stu-id="e1d62-272">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![test](./media/manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="e1d62-274">Type **This is a good day** for **col2**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-274">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="e1d62-275">Click the checkmark.</span><span class="sxs-lookup"><span data-stu-id="e1d62-275">Click the checkmark.</span></span>

![enter-data](./media/manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="e1d62-277">You will see something like</span><span class="sxs-lookup"><span data-stu-id="e1d62-277">You will see something like</span></span>

![sample-output](./media/manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="e1d62-279">Sample Code</span><span class="sxs-lookup"><span data-stu-id="e1d62-279">Sample Code</span></span>
<span data-ttu-id="e1d62-280">Another way to test your RRS is from your client code.</span><span class="sxs-lookup"><span data-stu-id="e1d62-280">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="e1d62-281">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span><span class="sxs-lookup"><span data-stu-id="e1d62-281">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="e1d62-282">This guide shows a working Python example.</span><span class="sxs-lookup"><span data-stu-id="e1d62-282">This guide shows a working Python example.</span></span> <span data-ttu-id="e1d62-283">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-283">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="e1d62-284">Test BES endpoint</span><span class="sxs-lookup"><span data-stu-id="e1d62-284">Test BES endpoint</span></span>
<span data-ttu-id="e1d62-285">Click **Batch execution** on the dashboard and scroll to the bottom.</span><span class="sxs-lookup"><span data-stu-id="e1d62-285">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="e1d62-286">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span><span class="sxs-lookup"><span data-stu-id="e1d62-286">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="e1d62-287">This guide shows a working Python example.</span><span class="sxs-lookup"><span data-stu-id="e1d62-287">This guide shows a working Python example.</span></span> <span data-ttu-id="e1d62-288">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span><span class="sxs-lookup"><span data-stu-id="e1d62-288">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="e1d62-289">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-289">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="e1d62-290">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span><span class="sxs-lookup"><span data-stu-id="e1d62-290">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
