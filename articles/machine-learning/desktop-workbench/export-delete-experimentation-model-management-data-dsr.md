---
title: Export or delete experimentation or model management data - Azure Machine Learning  | Microsoft Docs
description: In Azure Machine Learning, you can export or delete your account data related to experimentation or model management with the Azure portal, CLI, SDK, and authenticated REST APIs. This article shows you how.
services: machine-learning
author: cjgronlund
ms.author: cgronlun
manager: haining
ms.reviewer: jmartens, mldocs
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.date: 05/22/2018
ms.openlocfilehash: 5475ce3be24321b15ab78a078b758c25843f0ed3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864976"
---
# <a name="export-or-delete-your-experimentation-or-model-management-data-in-machine-learning"></a><span data-ttu-id="cf15e-104">Export or delete your experimentation or model management data in Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cf15e-104">Export or delete your experimentation or model management data in Machine Learning</span></span>

<span data-ttu-id="cf15e-105">In Azure Machine Learning, you can export or delete your account data related to experimentation or model management with the authenticated REST API.</span><span class="sxs-lookup"><span data-stu-id="cf15e-105">In Azure Machine Learning, you can export or delete your account data related to experimentation or model management with the authenticated REST API.</span></span> <span data-ttu-id="cf15e-106">This article tells you how.</span><span class="sxs-lookup"><span data-stu-id="cf15e-106">This article tells you how.</span></span>

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-dsr-and-stp-note.md)]

[!INCLUDE [GDPR-related guidance](../../../includes/gdpr-intro-sentence.md)]

## <a name="control-your-account-data"></a><span data-ttu-id="cf15e-107">Control your account data</span><span class="sxs-lookup"><span data-stu-id="cf15e-107">Control your account data</span></span>
<span data-ttu-id="cf15e-108">In-product data stored by Azure Machine Learning experimentation and model management is available for export and deletion through the Azure portal, CLI, SDK, and authenticated REST APIs.</span><span class="sxs-lookup"><span data-stu-id="cf15e-108">In-product data stored by Azure Machine Learning experimentation and model management is available for export and deletion through the Azure portal, CLI, SDK, and authenticated REST APIs.</span></span> <span data-ttu-id="cf15e-109">Telemetry data can be accessed through the Azure Privacy portal.</span><span class="sxs-lookup"><span data-stu-id="cf15e-109">Telemetry data can be accessed through the Azure Privacy portal.</span></span> 

<span data-ttu-id="cf15e-110">In Azure Machine Learning, personal data consists of user information in run history documents and telemetry records of some user interactions with the service.</span><span class="sxs-lookup"><span data-stu-id="cf15e-110">In Azure Machine Learning, personal data consists of user information in run history documents and telemetry records of some user interactions with the service.</span></span>

## <a name="delete-account-data-with-the-rest-api"></a><span data-ttu-id="cf15e-111">Delete account data with the REST API</span><span class="sxs-lookup"><span data-stu-id="cf15e-111">Delete account data with the REST API</span></span> 

<span data-ttu-id="cf15e-112">In order to delete data, the following API calls can be made with the HTTP DELETE verb.</span><span class="sxs-lookup"><span data-stu-id="cf15e-112">In order to delete data, the following API calls can be made with the HTTP DELETE verb.</span></span> <span data-ttu-id="cf15e-113">These are authorized by having an `Authorization: Bearer <arm-token>` header in the request, where `<arm-token>` is the AAD access token for the endpoint `https://management.core.windows.net/` endpoint.</span><span class="sxs-lookup"><span data-stu-id="cf15e-113">These are authorized by having an `Authorization: Bearer <arm-token>` header in the request, where `<arm-token>` is the AAD access token for the endpoint `https://management.core.windows.net/` endpoint.</span></span>  

<span data-ttu-id="cf15e-114">To learn how to get this token and call Azure endpoints, see [Azure REST API documentation](https://docs.microsoft.com/rest/api/azure/).</span><span class="sxs-lookup"><span data-stu-id="cf15e-114">To learn how to get this token and call Azure endpoints, see [Azure REST API documentation](https://docs.microsoft.com/rest/api/azure/).</span></span>  

<span data-ttu-id="cf15e-115">In the examples following, replace the text in {} with the instance names that determine the associated resource.</span><span class="sxs-lookup"><span data-stu-id="cf15e-115">In the examples following, replace the text in {} with the instance names that determine the associated resource.</span></span>

## <a name="delete-from-a-hosting-account"></a><span data-ttu-id="cf15e-116">Delete from a hosting account</span><span class="sxs-lookup"><span data-stu-id="cf15e-116">Delete from a hosting account</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.MachineLearningModelManagement/accounts/{account-name}?api-version=2017-09-01-preview      

## <a name="delete-from-the-model-management-service"></a><span data-ttu-id="cf15e-117">Delete from the model management service</span><span class="sxs-lookup"><span data-stu-id="cf15e-117">Delete from the model management service</span></span>

### <a name="model-document"></a><span data-ttu-id="cf15e-118">Model document</span><span class="sxs-lookup"><span data-stu-id="cf15e-118">Model document</span></span>
<span data-ttu-id="cf15e-119">Use this call to get a list of models and their IDs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-119">Use this call to get a list of models and their IDs:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/models?api-version=2017-09-01-preview"

<span data-ttu-id="cf15e-120">Individual models can be deleted with:</span><span class="sxs-lookup"><span data-stu-id="cf15e-120">Individual models can be deleted with:</span></span>  

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/models/{modelId}?api-version=2017-09-01-preview

### <a name="manifest-document"></a><span data-ttu-id="cf15e-121">Manifest document</span><span class="sxs-lookup"><span data-stu-id="cf15e-121">Manifest document</span></span>
<span data-ttu-id="cf15e-122">Use this call to get a list of all manifests and their IDs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-122">Use this call to get a list of all manifests and their IDs:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/manifests?api-version=2017-09-01-preview

<span data-ttu-id="cf15e-123">Individual manifests can be deleted with:</span><span class="sxs-lookup"><span data-stu-id="cf15e-123">Individual manifests can be deleted with:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/manifests/{manifestId}?api-version=2017-09-01-preview

### <a name="service-documents"></a><span data-ttu-id="cf15e-124">Service documents</span><span class="sxs-lookup"><span data-stu-id="cf15e-124">Service documents</span></span>
<span data-ttu-id="cf15e-125">Use this call to get a list of all services and their IDs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-125">Use this call to get a list of all services and their IDs:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/services?api-version=2017-09-01-preview

<span data-ttu-id="cf15e-126">Individual services can be deleted with:</span><span class="sxs-lookup"><span data-stu-id="cf15e-126">Individual services can be deleted with:</span></span>    

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/services/{serviceName}?api-version=2017-09-01-preview

### <a name="image-document"></a><span data-ttu-id="cf15e-127">Image document</span><span class="sxs-lookup"><span data-stu-id="cf15e-127">Image document</span></span>
<span data-ttu-id="cf15e-128">Use this call to get a list of all images and their IDs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-128">Use this call to get a list of all images and their IDs:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/images?api-version=2017-09-01-preview

<span data-ttu-id="cf15e-129">Individual images can be deleted with:</span><span class="sxs-lookup"><span data-stu-id="cf15e-129">Individual images can be deleted with:</span></span>  

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/images/{imageId}?api-version=2017-09-01-preview

## <a name="delete-run-history-artifact-and-notification-data"></a><span data-ttu-id="cf15e-130">Delete run history, artifact, and notification data</span><span class="sxs-lookup"><span data-stu-id="cf15e-130">Delete run history, artifact, and notification data</span></span>
<span data-ttu-id="cf15e-131">Run history, artifact, and notification stores for a project are all deleted after deleting the corresponding project document:</span><span class="sxs-lookup"><span data-stu-id="cf15e-131">Run history, artifact, and notification stores for a project are all deleted after deleting the corresponding project document:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.MachineLearningExperimentation/accounts/{account-name}/workspaces/{workspace-name}/projects/{project-name}?api-version=2017-05-01-preview
    
## <a name="delete-from-experimentation-account-resource-provider"></a><span data-ttu-id="cf15e-132">Delete from experimentation account resource provider</span><span class="sxs-lookup"><span data-stu-id="cf15e-132">Delete from experimentation account resource provider</span></span>
<span data-ttu-id="cf15e-133">Project documents are deleted with:</span><span class="sxs-lookup"><span data-stu-id="cf15e-133">Project documents are deleted with:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.MachineLearningExperimentation/accounts/{account-name}/workspaces/{workspace-name}/projects/{project-name}?api-version=2017-05-01-preview

<span data-ttu-id="cf15e-134">Workspace documents are deleted with:</span><span class="sxs-lookup"><span data-stu-id="cf15e-134">Workspace documents are deleted with:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.MachineLearningExperimentation/accounts/{account-name}/workspaces/{workspace-name}?api-version=2017-05-01-preview

<span data-ttu-id="cf15e-135">The entire experimentation account is deleted with:</span><span class="sxs-lookup"><span data-stu-id="cf15e-135">The entire experimentation account is deleted with:</span></span>
    
    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.MachineLearningExperimentation/accounts/{account-name}?api-version=2017-05-01-preview


## <a name="export-service-data-with-the-rest-api"></a><span data-ttu-id="cf15e-136">Export service data with the REST API</span><span class="sxs-lookup"><span data-stu-id="cf15e-136">Export service data with the REST API</span></span>
<span data-ttu-id="cf15e-137">In order to export data, the following API calls can be made with the HTTP GET verb.</span><span class="sxs-lookup"><span data-stu-id="cf15e-137">In order to export data, the following API calls can be made with the HTTP GET verb.</span></span> <span data-ttu-id="cf15e-138">These are authorized by having an `Authorization: Bearer <arm-token>` header in the request, where `<arm-token>` is the AAD access token for the endpoint `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="cf15e-138">These are authorized by having an `Authorization: Bearer <arm-token>` header in the request, where `<arm-token>` is the AAD access token for the endpoint `https://management.core.windows.net/`</span></span>  

<span data-ttu-id="cf15e-139">To learn how to get this token and call Azure endpoints, see [Azure REST API documentation](https://docs.microsoft.com/rest/api/azure/).</span><span class="sxs-lookup"><span data-stu-id="cf15e-139">To learn how to get this token and call Azure endpoints, see [Azure REST API documentation](https://docs.microsoft.com/rest/api/azure/).</span></span>   

<span data-ttu-id="cf15e-140">In the examples following, replace the text in {} with the instance names that determine the associated resource.</span><span class="sxs-lookup"><span data-stu-id="cf15e-140">In the examples following, replace the text in {} with the instance names that determine the associated resource.</span></span>

## <a name="export-hosting-account-data"></a><span data-ttu-id="cf15e-141">Export hosting account data</span><span class="sxs-lookup"><span data-stu-id="cf15e-141">Export hosting account data</span></span>

    https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningModelManagement/accounts/{accountName}?api-version=2017-09-01-preview     

## <a name="export-model-management-service-data"></a><span data-ttu-id="cf15e-142">Export model management service data</span><span class="sxs-lookup"><span data-stu-id="cf15e-142">Export model management service data</span></span>
### <a name="model-document"></a><span data-ttu-id="cf15e-143">Model document</span><span class="sxs-lookup"><span data-stu-id="cf15e-143">Model document</span></span>

<span data-ttu-id="cf15e-144">Use this call to get a list of models and their IDs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-144">Use this call to get a list of models and their IDs:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/models?api-version=2017-09-01-preview"

<span data-ttu-id="cf15e-145">Individual models can be obtained by:</span><span class="sxs-lookup"><span data-stu-id="cf15e-145">Individual models can be obtained by:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/models/{modelId}?api-version=2017-09-01-preview 

### <a name="manifests"></a><span data-ttu-id="cf15e-146">Manifests</span><span class="sxs-lookup"><span data-stu-id="cf15e-146">Manifests</span></span>
<span data-ttu-id="cf15e-147">Use this call to get a list of all manifests and their IDs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-147">Use this call to get a list of all manifests and their IDs:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/manifests?api-version=2017-09-01-preview

<span data-ttu-id="cf15e-148">Individual manifests can be obtained by:</span><span class="sxs-lookup"><span data-stu-id="cf15e-148">Individual manifests can be obtained by:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/manifests/{manifestId}?api-version=2017-09-01-preview

### <a name="services"></a><span data-ttu-id="cf15e-149">Services</span><span class="sxs-lookup"><span data-stu-id="cf15e-149">Services</span></span>
<span data-ttu-id="cf15e-150">Use this call to get a list of all services and their IDs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-150">Use this call to get a list of all services and their IDs:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/services?api-version=2017-09-01-preview

<span data-ttu-id="cf15e-151">Individual services can be obtained by:</span><span class="sxs-lookup"><span data-stu-id="cf15e-151">Individual services can be obtained by:</span></span> 

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/services/{serviceName}?api-version=2017-09-01-preview

### <a name="images"></a><span data-ttu-id="cf15e-152">Images</span><span class="sxs-lookup"><span data-stu-id="cf15e-152">Images</span></span>
<span data-ttu-id="cf15e-153">Use this call to get a list of all images and their IDs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-153">Use this call to get a list of all images and their IDs:</span></span>

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/images?api-version=2017-09-01-preview

<span data-ttu-id="cf15e-154">Individual services can be obtained by:</span><span class="sxs-lookup"><span data-stu-id="cf15e-154">Individual services can be obtained by:</span></span> 

    https://{location}.modelmanagement.azureml.net/api/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/accounts/{accountName}/images/{imageId}?api-version=2017-09-01-preview     

## <a name="export-compute-data"></a><span data-ttu-id="cf15e-155">Export compute data</span><span class="sxs-lookup"><span data-stu-id="cf15e-155">Export compute data</span></span>
### <a name="compute-clusters"></a><span data-ttu-id="cf15e-156">Compute clusters</span><span class="sxs-lookup"><span data-stu-id="cf15e-156">Compute clusters</span></span>
<span data-ttu-id="cf15e-157">Use this call to get a list of all compute clusters and their names:</span><span class="sxs-lookup"><span data-stu-id="cf15e-157">Use this call to get a list of all compute clusters and their names:</span></span>

    https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningServices/workspaces/{workspaceName}/computes?api-version=2018-03-01-preview

<span data-ttu-id="cf15e-158">Individual clusters can be obtained by:</span><span class="sxs-lookup"><span data-stu-id="cf15e-158">Individual clusters can be obtained by:</span></span>

    https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningServices/workspaces/{workspaceName}/computes/{compute-name}?api-version=2018-03-01-preview

### <a name="operationalization-clusters"></a><span data-ttu-id="cf15e-159">Operationalization clusters</span><span class="sxs-lookup"><span data-stu-id="cf15e-159">Operationalization clusters</span></span>
<span data-ttu-id="cf15e-160">Use this call to get a list of all clusters and their names:</span><span class="sxs-lookup"><span data-stu-id="cf15e-160">Use this call to get a list of all clusters and their names:</span></span>

    https://management.azure.com/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.MachineLearningCompute/operationalizationClusters?api-version=2017-06-01-preview

<span data-ttu-id="cf15e-161">Individual clusters can be obtained by:</span><span class="sxs-lookup"><span data-stu-id="cf15e-161">Individual clusters can be obtained by:</span></span>

    https://management.azure.com/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.MachineLearningCompute/operationalizationClusters/{clusterName}?api-version=2017-06-01-preview

## <a name="export-run-history-data"></a><span data-ttu-id="cf15e-162">Export run history data</span><span class="sxs-lookup"><span data-stu-id="cf15e-162">Export run history data</span></span>
<span data-ttu-id="cf15e-163">Use this call to get a list of all runs and their IDs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-163">Use this call to get a list of all runs and their IDs:</span></span>

    https://{location}.experiments.azureml.net/history/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/runs

<span data-ttu-id="cf15e-164">Use this call to get a list of all experiments and their IDs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-164">Use this call to get a list of all experiments and their IDs:</span></span>

    https://{location}.experiments.azureml.net/history/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/experiments

<span data-ttu-id="cf15e-165">Run history items can be obtained by:</span><span class="sxs-lookup"><span data-stu-id="cf15e-165">Run history items can be obtained by:</span></span>

    https://{location}.experiments.azureml.net/history/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/runs/{runId}

<span data-ttu-id="cf15e-166">Run metrics items can be obtained by:</span><span class="sxs-lookup"><span data-stu-id="cf15e-166">Run metrics items can be obtained by:</span></span>

    https://{location}.experiments.azureml.net/history/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/runmetrics

<span data-ttu-id="cf15e-167">Run experiments can be obtained by:</span><span class="sxs-lookup"><span data-stu-id="cf15e-167">Run experiments can be obtained by:</span></span>

    https://{location}.experiments.azureml.net/history/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/experiments/{experimentId}    

<span data-ttu-id="cf15e-168">Run history artifacts:</span><span class="sxs-lookup"><span data-stu-id="cf15e-168">Run history artifacts:</span></span>

    https://{location}.experiments.azureml.net/history/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/runs/{runId}/artifacts

<span data-ttu-id="cf15e-169">Run history artifacts URIs:</span><span class="sxs-lookup"><span data-stu-id="cf15e-169">Run history artifacts URIs:</span></span>

    https://{location}.experiments.azureml.net/history/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/runs/{runId}/artifacturi?name={artifactName}

## <a name="export-artifacts"></a><span data-ttu-id="cf15e-170">Export artifacts</span><span class="sxs-lookup"><span data-stu-id="cf15e-170">Export artifacts</span></span>
<span data-ttu-id="cf15e-171">Use this call to get a list of assets and their names:</span><span class="sxs-lookup"><span data-stu-id="cf15e-171">Use this call to get a list of assets and their names:</span></span>

    https://{location}.experiments.azureml.net/artifact/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/assets

<span data-ttu-id="cf15e-172">Use this call to get a list of artifacts and their paths:</span><span class="sxs-lookup"><span data-stu-id="cf15e-172">Use this call to get a list of artifacts and their paths:</span></span>

    https://{location}.experiments.azureml.net/artifact/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/artifacts/origins/{origin}/containers/{runId}
        
        
### <a name="artifact-contents"></a><span data-ttu-id="cf15e-173">Artifact contents</span><span class="sxs-lookup"><span data-stu-id="cf15e-173">Artifact contents</span></span>

    https://{location}.experiments.azureml.net/artifact/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/artifacts/contentinfo/ExperimentRun/{runId}/{artifactPath}

### <a name="artifact-documents"></a><span data-ttu-id="cf15e-174">Artifact documents</span><span class="sxs-lookup"><span data-stu-id="cf15e-174">Artifact documents</span></span>

    https://{location}.experiments.azureml.net/history/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/runs/{runId}/artifacts
        
### <a name="assets"></a><span data-ttu-id="cf15e-175">Assets</span><span class="sxs-lookup"><span data-stu-id="cf15e-175">Assets</span></span>

    https://{location}.experiments.azureml.net/artifact/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/assets/name/{name}

## <a name="export-notifications"></a><span data-ttu-id="cf15e-176">Export notifications</span><span class="sxs-lookup"><span data-stu-id="cf15e-176">Export notifications</span></span>

1. <span data-ttu-id="cf15e-177">Go to the [Users section of the Azure portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UsersManagementMenuBlade/), and then select a user from the **Name** column.</span><span class="sxs-lookup"><span data-stu-id="cf15e-177">Go to the [Users section of the Azure portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UsersManagementMenuBlade/), and then select a user from the **Name** column.</span></span> 
2. <span data-ttu-id="cf15e-178">Note the **Object ID**, and use it in the following call:</span><span class="sxs-lookup"><span data-stu-id="cf15e-178">Note the **Object ID**, and use it in the following call:</span></span>     

        https://{location}.experiments.azureml.net/notification/v1.0/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}/users/{objectId}/jobs

## <a name="export-experimentation-account-information"></a><span data-ttu-id="cf15e-179">Export experimentation account information</span><span class="sxs-lookup"><span data-stu-id="cf15e-179">Export experimentation account information</span></span>
### <a name="experimentation-account-information"></a><span data-ttu-id="cf15e-180">Experimentation account information</span><span class="sxs-lookup"><span data-stu-id="cf15e-180">Experimentation account information</span></span>

    https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}?api-version=2017-05-01-preview
        
### <a name="workspace-information"></a><span data-ttu-id="cf15e-181">Workspace information</span><span class="sxs-lookup"><span data-stu-id="cf15e-181">Workspace information</span></span>

    https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}?api-version=2017-05-01-preview  

### <a name="project-information"></a><span data-ttu-id="cf15e-182">Project information</span><span class="sxs-lookup"><span data-stu-id="cf15e-182">Project information</span></span>

    https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.MachineLearningExperimentation/accounts/{accountName}/workspaces/{workspaceName}/projects/{projectName}?api-version=2017-05-01-preview
