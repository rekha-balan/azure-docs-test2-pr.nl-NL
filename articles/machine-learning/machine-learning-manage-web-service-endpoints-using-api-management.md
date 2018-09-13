---
title: Learn how to manage AzureML web services using API Management | Microsoft Docs
description: A guide showing how to manage AzureML web services using API Management.
keywords: machine learning,api management
services: machine-learning
documentationcenter: ''
author: roalexan
manager: jhubbard
editor: ''
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: db2670caf369f916868d45688510609418ff1679
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563258"
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="012df-104">Learn how to manage AzureML web services using API Management</span><span class="sxs-lookup"><span data-stu-id="012df-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="012df-105">Overview</span><span class="sxs-lookup"><span data-stu-id="012df-105">Overview</span></span>
<span data-ttu-id="012df-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span><span class="sxs-lookup"><span data-stu-id="012df-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="012df-107">What is Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="012df-107">What is Azure API Management?</span></span>
<span data-ttu-id="012df-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span><span class="sxs-lookup"><span data-stu-id="012df-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="012df-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="012df-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="012df-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="012df-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="012df-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span><span class="sxs-lookup"><span data-stu-id="012df-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="012df-112">What is AzureML?</span><span class="sxs-lookup"><span data-stu-id="012df-112">What is AzureML?</span></span>
<span data-ttu-id="012df-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="012df-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="012df-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span><span class="sxs-lookup"><span data-stu-id="012df-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="012df-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="012df-115">Prerequisites</span></span>
<span data-ttu-id="012df-116">To complete this guide, you need:</span><span class="sxs-lookup"><span data-stu-id="012df-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="012df-117">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="012df-117">An Azure account.</span></span> <span data-ttu-id="012df-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span><span class="sxs-lookup"><span data-stu-id="012df-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="012df-119">An AzureML account.</span><span class="sxs-lookup"><span data-stu-id="012df-119">An AzureML account.</span></span> <span data-ttu-id="012df-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span><span class="sxs-lookup"><span data-stu-id="012df-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="012df-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span><span class="sxs-lookup"><span data-stu-id="012df-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="012df-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="012df-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span><span class="sxs-lookup"><span data-stu-id="012df-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="012df-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span><span class="sxs-lookup"><span data-stu-id="012df-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="012df-125">Create an API Management instance</span><span class="sxs-lookup"><span data-stu-id="012df-125">Create an API Management instance</span></span>
<span data-ttu-id="012df-126">Below are the steps for using API Management to manage your AzureML web service.</span><span class="sxs-lookup"><span data-stu-id="012df-126">Below are the steps for using API Management to manage your AzureML web service.</span></span> <span data-ttu-id="012df-127">First create a service instance.</span><span class="sxs-lookup"><span data-stu-id="012df-127">First create a service instance.</span></span> <span data-ttu-id="012df-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="012df-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="012df-130">Specify a unique **URL**.</span><span class="sxs-lookup"><span data-stu-id="012df-130">Specify a unique **URL**.</span></span> <span data-ttu-id="012df-131">This guide uses **demoazureml** – you will need to choose something different.</span><span class="sxs-lookup"><span data-stu-id="012df-131">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="012df-132">Choose the desired **Subscription** and **Region** for your service instance.</span><span class="sxs-lookup"><span data-stu-id="012df-132">Choose the desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="012df-133">After making your selections, click the next button.</span><span class="sxs-lookup"><span data-stu-id="012df-133">After making your selections, click the next button.</span></span>

![create-service-1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="012df-135">Specify a value for the **Organization Name**.</span><span class="sxs-lookup"><span data-stu-id="012df-135">Specify a value for the **Organization Name**.</span></span> <span data-ttu-id="012df-136">This guide uses **demoazureml** – you will need to choose something different.</span><span class="sxs-lookup"><span data-stu-id="012df-136">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="012df-137">Enter your email address in the **administrator e-mail** field.</span><span class="sxs-lookup"><span data-stu-id="012df-137">Enter your email address in the **administrator e-mail** field.</span></span> <span data-ttu-id="012df-138">This email address is used for notifications from the API Management system.</span><span class="sxs-lookup"><span data-stu-id="012df-138">This email address is used for notifications from the API Management system.</span></span>

![create-service-2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="012df-140">Click the check box to create your service instance.</span><span class="sxs-lookup"><span data-stu-id="012df-140">Click the check box to create your service instance.</span></span> <span data-ttu-id="012df-141">*It takes up to thirty minutes for a new service to be created*.</span><span class="sxs-lookup"><span data-stu-id="012df-141">*It takes up to thirty minutes for a new service to be created*.</span></span>

## <a name="create-the-api"></a><span data-ttu-id="012df-142">Create the API</span><span class="sxs-lookup"><span data-stu-id="012df-142">Create the API</span></span>
<span data-ttu-id="012df-143">Once the service instance is created, the next step is to create the API.</span><span class="sxs-lookup"><span data-stu-id="012df-143">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="012df-144">An API consists of a set of operations that can be invoked from a client application.</span><span class="sxs-lookup"><span data-stu-id="012df-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="012df-145">API operations are proxied to existing web services.</span><span class="sxs-lookup"><span data-stu-id="012df-145">API operations are proxied to existing web services.</span></span> <span data-ttu-id="012df-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span><span class="sxs-lookup"><span data-stu-id="012df-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="012df-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="012df-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span></span> <span data-ttu-id="012df-148">To reach the publisher portal, select your service instance.</span><span class="sxs-lookup"><span data-stu-id="012df-148">To reach the publisher portal, select your service instance.</span></span>

![select-service-instance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="012df-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="012df-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span></span>

![manage-service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="012df-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span><span class="sxs-lookup"><span data-stu-id="012df-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span></span>

![api-management-menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="012df-154">Type **AzureML Demo API** as the **Web API name**.</span><span class="sxs-lookup"><span data-stu-id="012df-154">Type **AzureML Demo API** as the **Web API name**.</span></span> <span data-ttu-id="012df-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span><span class="sxs-lookup"><span data-stu-id="012df-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span></span> <span data-ttu-id="012df-156">Type **azureml-demo** as the **Web API URL suffix**.</span><span class="sxs-lookup"><span data-stu-id="012df-156">Type **azureml-demo** as the **Web API URL suffix**.</span></span> <span data-ttu-id="012df-157">Check **HTTPS** as the **Web API URL** scheme.</span><span class="sxs-lookup"><span data-stu-id="012df-157">Check **HTTPS** as the **Web API URL** scheme.</span></span> <span data-ttu-id="012df-158">Select **Starter** as **Products**.</span><span class="sxs-lookup"><span data-stu-id="012df-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="012df-159">When finished, click **Save** to create the API.</span><span class="sxs-lookup"><span data-stu-id="012df-159">When finished, click **Save** to create the API.</span></span>

![add-new-api](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-the-operations"></a><span data-ttu-id="012df-161">Add the operations</span><span class="sxs-lookup"><span data-stu-id="012df-161">Add the operations</span></span>
<span data-ttu-id="012df-162">Click **Add operation** to add operations to this API.</span><span class="sxs-lookup"><span data-stu-id="012df-162">Click **Add operation** to add operations to this API.</span></span>

![add-operation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="012df-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span><span class="sxs-lookup"><span data-stu-id="012df-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="012df-165">Add RRS Operation</span><span class="sxs-lookup"><span data-stu-id="012df-165">Add RRS Operation</span></span>
<span data-ttu-id="012df-166">First create an operation for the AzureML RRS service.</span><span class="sxs-lookup"><span data-stu-id="012df-166">First create an operation for the AzureML RRS service.</span></span> <span data-ttu-id="012df-167">Select **POST** as the **HTTP verb**.</span><span class="sxs-lookup"><span data-stu-id="012df-167">Select **POST** as the **HTTP verb**.</span></span> <span data-ttu-id="012df-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span><span class="sxs-lookup"><span data-stu-id="012df-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span></span> <span data-ttu-id="012df-169">Type **RRS Execute** as the **Display name**.</span><span class="sxs-lookup"><span data-stu-id="012df-169">Type **RRS Execute** as the **Display name**.</span></span>

![add-rrs-operation-signature](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="012df-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="012df-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="012df-172">Click **Save** to save this operation.</span><span class="sxs-lookup"><span data-stu-id="012df-172">Click **Save** to save this operation.</span></span>

![add-rrs-operation-response](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="012df-174">Add BES Operations</span><span class="sxs-lookup"><span data-stu-id="012df-174">Add BES Operations</span></span>
<span data-ttu-id="012df-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span><span class="sxs-lookup"><span data-stu-id="012df-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="012df-176">Submit (but not start) a Batch Execution job</span><span class="sxs-lookup"><span data-stu-id="012df-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="012df-177">Click **add operation** to add the AzureML BES operation to the API.</span><span class="sxs-lookup"><span data-stu-id="012df-177">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="012df-178">Select **POST** for the **HTTP verb**.</span><span class="sxs-lookup"><span data-stu-id="012df-178">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="012df-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span><span class="sxs-lookup"><span data-stu-id="012df-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="012df-180">Type **BES Submit** for the **Display name**.</span><span class="sxs-lookup"><span data-stu-id="012df-180">Type **BES Submit** for the **Display name**.</span></span> <span data-ttu-id="012df-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="012df-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="012df-182">Click **Save** to save this operation.</span><span class="sxs-lookup"><span data-stu-id="012df-182">Click **Save** to save this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="012df-183">Start a Batch Execution job</span><span class="sxs-lookup"><span data-stu-id="012df-183">Start a Batch Execution job</span></span>
<span data-ttu-id="012df-184">Click **add operation** to add the AzureML BES operation to the API.</span><span class="sxs-lookup"><span data-stu-id="012df-184">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="012df-185">Select **POST** for the **HTTP verb**.</span><span class="sxs-lookup"><span data-stu-id="012df-185">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="012df-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span><span class="sxs-lookup"><span data-stu-id="012df-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="012df-187">Type **BES Start** for the **Display name**.</span><span class="sxs-lookup"><span data-stu-id="012df-187">Type **BES Start** for the **Display name**.</span></span> <span data-ttu-id="012df-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="012df-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="012df-189">Click **Save** to save this operation.</span><span class="sxs-lookup"><span data-stu-id="012df-189">Click **Save** to save this operation.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="012df-190">Get the status or result of a Batch Execution job</span><span class="sxs-lookup"><span data-stu-id="012df-190">Get the status or result of a Batch Execution job</span></span>
<span data-ttu-id="012df-191">Click **add operation** to add the AzureML BES operation to the API.</span><span class="sxs-lookup"><span data-stu-id="012df-191">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="012df-192">Select **GET** for the **HTTP verb**.</span><span class="sxs-lookup"><span data-stu-id="012df-192">Select **GET** for the **HTTP verb**.</span></span> <span data-ttu-id="012df-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span><span class="sxs-lookup"><span data-stu-id="012df-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="012df-194">Type **BES Status** for the **Display name**.</span><span class="sxs-lookup"><span data-stu-id="012df-194">Type **BES Status** for the **Display name**.</span></span> <span data-ttu-id="012df-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="012df-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="012df-196">Click **Save** to save this operation.</span><span class="sxs-lookup"><span data-stu-id="012df-196">Click **Save** to save this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="012df-197">Delete a Batch Execution job</span><span class="sxs-lookup"><span data-stu-id="012df-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="012df-198">Click **add operation** to add the AzureML BES operation to the API.</span><span class="sxs-lookup"><span data-stu-id="012df-198">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="012df-199">Select **DELETE** for the **HTTP verb**.</span><span class="sxs-lookup"><span data-stu-id="012df-199">Select **DELETE** for the **HTTP verb**.</span></span> <span data-ttu-id="012df-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span><span class="sxs-lookup"><span data-stu-id="012df-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="012df-201">Type **BES Delete** for the **Display name**.</span><span class="sxs-lookup"><span data-stu-id="012df-201">Type **BES Delete** for the **Display name**.</span></span> <span data-ttu-id="012df-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="012df-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="012df-203">Click **Save** to save this operation.</span><span class="sxs-lookup"><span data-stu-id="012df-203">Click **Save** to save this operation.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="012df-204">Call an operation from the Developer Portal</span><span class="sxs-lookup"><span data-stu-id="012df-204">Call an operation from the Developer Portal</span></span>
<span data-ttu-id="012df-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span><span class="sxs-lookup"><span data-stu-id="012df-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="012df-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span><span class="sxs-lookup"><span data-stu-id="012df-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> <span data-ttu-id="012df-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="012df-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span></span>

![developer-portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="012df-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span><span class="sxs-lookup"><span data-stu-id="012df-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

![demoazureml-api](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="012df-211">Select **RRS Execute** for the operation.</span><span class="sxs-lookup"><span data-stu-id="012df-211">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="012df-212">Click **Try It**.</span><span class="sxs-lookup"><span data-stu-id="012df-212">Click **Try It**.</span></span>

![try-it](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="012df-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span><span class="sxs-lookup"><span data-stu-id="012df-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span></span> <span data-ttu-id="012df-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span><span class="sxs-lookup"><span data-stu-id="012df-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="012df-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="012df-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="012df-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span><span class="sxs-lookup"><span data-stu-id="012df-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="012df-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span><span class="sxs-lookup"><span data-stu-id="012df-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span></span>

![azureml-demo-api](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="012df-220">Click **Send**.</span><span class="sxs-lookup"><span data-stu-id="012df-220">Click **Send**.</span></span>

![send](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="012df-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span><span class="sxs-lookup"><span data-stu-id="012df-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![response-status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="012df-224">Appendix A - Creating and testing a simple AzureML web service</span><span class="sxs-lookup"><span data-stu-id="012df-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="012df-225">Creating the experiment</span><span class="sxs-lookup"><span data-stu-id="012df-225">Creating the experiment</span></span>
<span data-ttu-id="012df-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span><span class="sxs-lookup"><span data-stu-id="012df-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="012df-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span><span class="sxs-lookup"><span data-stu-id="012df-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="012df-228">For example:</span><span class="sxs-lookup"><span data-stu-id="012df-228">For example:</span></span>

| <span data-ttu-id="012df-229">Text</span><span class="sxs-lookup"><span data-stu-id="012df-229">Text</span></span> | <span data-ttu-id="012df-230">Hashed Text</span><span class="sxs-lookup"><span data-stu-id="012df-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="012df-231">This is a good day</span><span class="sxs-lookup"><span data-stu-id="012df-231">This is a good day</span></span> |<span data-ttu-id="012df-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="012df-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="012df-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span><span class="sxs-lookup"><span data-stu-id="012df-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="012df-234">Next, create a new blank experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="012df-236">Rename it to **SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="012df-236">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="012df-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="012df-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="012df-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span><span class="sxs-lookup"><span data-stu-id="012df-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![select-columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="012df-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span><span class="sxs-lookup"><span data-stu-id="012df-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="012df-243">Click the checkmark to apply these changes.</span><span class="sxs-lookup"><span data-stu-id="012df-243">Click the checkmark to apply these changes.</span></span>

![select-columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="012df-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="012df-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="012df-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![connect-project-columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="012df-248">Type **3** for the **Hashing bitsize**.</span><span class="sxs-lookup"><span data-stu-id="012df-248">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="012df-249">This will create 8 (23) columns.</span><span class="sxs-lookup"><span data-stu-id="012df-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="012df-251">At this point, you may want to click **Run** to test the experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-251">At this point, you may want to click **Run** to test the experiment.</span></span>

![run](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="012df-253">Create a web service</span><span class="sxs-lookup"><span data-stu-id="012df-253">Create a web service</span></span>
<span data-ttu-id="012df-254">Now create a web service.</span><span class="sxs-lookup"><span data-stu-id="012df-254">Now create a web service.</span></span> <span data-ttu-id="012df-255">Expand **Web Service** and drag **Input** onto your experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="012df-256">Connect **Input** to **Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="012df-256">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="012df-257">Also drag **output** onto your experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="012df-258">Connect **Output** to **Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="012df-258">Connect **Output** to **Feature Hashing**.</span></span>

![output-to-feature-hashing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="012df-260">Click **Publish web service**.</span><span class="sxs-lookup"><span data-stu-id="012df-260">Click **Publish web service**.</span></span>

![publish-web-service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="012df-262">Click **Yes** to publish the experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-262">Click **Yes** to publish the experiment.</span></span>

![yes-to-publish](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="012df-264">Test the web service</span><span class="sxs-lookup"><span data-stu-id="012df-264">Test the web service</span></span>
<span data-ttu-id="012df-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span><span class="sxs-lookup"><span data-stu-id="012df-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="012df-266">RSS is for synchronous execution.</span><span class="sxs-lookup"><span data-stu-id="012df-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="012df-267">BES is for asynchronous job execution.</span><span class="sxs-lookup"><span data-stu-id="012df-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="012df-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="012df-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="012df-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span><span class="sxs-lookup"><span data-stu-id="012df-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="012df-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span><span class="sxs-lookup"><span data-stu-id="012df-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![find-workspace-and-service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="012df-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span><span class="sxs-lookup"><span data-stu-id="012df-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![find-api-key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="012df-274">Test RRS endpoint</span><span class="sxs-lookup"><span data-stu-id="012df-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="012df-275">Test button</span><span class="sxs-lookup"><span data-stu-id="012df-275">Test button</span></span>
<span data-ttu-id="012df-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span><span class="sxs-lookup"><span data-stu-id="012df-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="012df-278">Type **This is a good day** for **col2**.</span><span class="sxs-lookup"><span data-stu-id="012df-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="012df-279">Click the checkmark.</span><span class="sxs-lookup"><span data-stu-id="012df-279">Click the checkmark.</span></span>

![enter-data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="012df-281">You will see something like</span><span class="sxs-lookup"><span data-stu-id="012df-281">You will see something like</span></span>

![sample-output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="012df-283">Sample Code</span><span class="sxs-lookup"><span data-stu-id="012df-283">Sample Code</span></span>
<span data-ttu-id="012df-284">Another way to test your RRS is from your client code.</span><span class="sxs-lookup"><span data-stu-id="012df-284">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="012df-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span><span class="sxs-lookup"><span data-stu-id="012df-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="012df-286">This guide shows a working Python example.</span><span class="sxs-lookup"><span data-stu-id="012df-286">This guide shows a working Python example.</span></span> <span data-ttu-id="012df-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

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

#### <a name="test-bes-endpoint"></a><span data-ttu-id="012df-288">Test BES endpoint</span><span class="sxs-lookup"><span data-stu-id="012df-288">Test BES endpoint</span></span>
<span data-ttu-id="012df-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span><span class="sxs-lookup"><span data-stu-id="012df-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="012df-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span><span class="sxs-lookup"><span data-stu-id="012df-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="012df-291">This guide shows a working Python example.</span><span class="sxs-lookup"><span data-stu-id="012df-291">This guide shows a working Python example.</span></span> <span data-ttu-id="012df-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span><span class="sxs-lookup"><span data-stu-id="012df-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="012df-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span><span class="sxs-lookup"><span data-stu-id="012df-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="012df-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span><span class="sxs-lookup"><span data-stu-id="012df-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

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































