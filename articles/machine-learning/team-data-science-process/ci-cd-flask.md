---
title: 'DevOps for Artificial Intelligence (AI) applications: Creating continous integration pipeline on Azure using Docker, Kubernetes & Python Flask application'
description: 'DevOps for Artificial Intelligence (AI) applications: Creating continous integration pipeline on Azure using Docker and Kubernetes'
services: machine-learning, team-data-science-process
documentationcenter: ''
author: jainr
manager: deguhath
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2018
ms.author: jainr
ms.openlocfilehash: b0368e742c990feed626a1c4982bfedc35785b49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856666"
---
# <a name="devops-for-artificial-intelligence-ai-applications-creating-continuous-integration-pipeline-on-azure-using-docker-and-kubernetes"></a><span data-ttu-id="60728-103">DevOps for Artificial Intelligence (AI) applications: Creating continuous integration pipeline on Azure using Docker and Kubernetes</span><span class="sxs-lookup"><span data-stu-id="60728-103">DevOps for Artificial Intelligence (AI) applications: Creating continuous integration pipeline on Azure using Docker and Kubernetes</span></span>
<span data-ttu-id="60728-104">For an AI application, there are frequently two streams of work, Data Scientists building machine learning models and App developers building the application and exposing it to end users to consume.</span><span class="sxs-lookup"><span data-stu-id="60728-104">For an AI application, there are frequently two streams of work, Data Scientists building machine learning models and App developers building the application and exposing it to end users to consume.</span></span> <span data-ttu-id="60728-105">In this article, we demonstrate how to implement a Continuous Integration (CI)/Continous Delivery (CD) pipeline for an AI application.</span><span class="sxs-lookup"><span data-stu-id="60728-105">In this article, we demonstrate how to implement a Continuous Integration (CI)/Continous Delivery (CD) pipeline for an AI application.</span></span> <span data-ttu-id="60728-106">AI application is a combination of application code embedded with a pretrained machine learning (ML) model.</span><span class="sxs-lookup"><span data-stu-id="60728-106">AI application is a combination of application code embedded with a pretrained machine learning (ML) model.</span></span> <span data-ttu-id="60728-107">For this article, we are fetching a pretrained model from a private Azure blob storage account, it could be an AWS S3 account as well.</span><span class="sxs-lookup"><span data-stu-id="60728-107">For this article, we are fetching a pretrained model from a private Azure blob storage account, it could be an AWS S3 account as well.</span></span> <span data-ttu-id="60728-108">We will use a simple python flask web application for the article.</span><span class="sxs-lookup"><span data-stu-id="60728-108">We will use a simple python flask web application for the article.</span></span>

> [!NOTE]
> <span data-ttu-id="60728-109">This is one of several ways CI/CD can be performed.</span><span class="sxs-lookup"><span data-stu-id="60728-109">This is one of several ways CI/CD can be performed.</span></span> <span data-ttu-id="60728-110">There are alternatives to the tooling and other pre-requisites mentioned below.</span><span class="sxs-lookup"><span data-stu-id="60728-110">There are alternatives to the tooling and other pre-requisites mentioned below.</span></span> <span data-ttu-id="60728-111">As we develop additional content, we will publish those.</span><span class="sxs-lookup"><span data-stu-id="60728-111">As we develop additional content, we will publish those.</span></span>
>
>

## <a name="github-repository-with-document-and-code"></a><span data-ttu-id="60728-112">GitHub repository with document and code</span><span class="sxs-lookup"><span data-stu-id="60728-112">GitHub repository with document and code</span></span>
<span data-ttu-id="60728-113">You can download the source code from [GitHub](https://github.com/Azure/DevOps-For-AI-Apps).</span><span class="sxs-lookup"><span data-stu-id="60728-113">You can download the source code from [GitHub](https://github.com/Azure/DevOps-For-AI-Apps).</span></span> <span data-ttu-id="60728-114">A [detailed tutorial](https://github.com/Azure/DevOps-For-AI-Apps/blob/master/Tutorial.md) is also available.</span><span class="sxs-lookup"><span data-stu-id="60728-114">A [detailed tutorial](https://github.com/Azure/DevOps-For-AI-Apps/blob/master/Tutorial.md) is also available.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="60728-115">Pre-requisites</span><span class="sxs-lookup"><span data-stu-id="60728-115">Pre-requisites</span></span>
<span data-ttu-id="60728-116">The following are the pre-requisites for following the CI/CD pipeline described below:</span><span class="sxs-lookup"><span data-stu-id="60728-116">The following are the pre-requisites for following the CI/CD pipeline described below:</span></span>
* [<span data-ttu-id="60728-117">Azure DevOps Organization</span><span class="sxs-lookup"><span data-stu-id="60728-117">Azure DevOps Organization</span></span>](https://docs.microsoft.com/azure/devops/organizations/accounts/create-organization-msa-or-work-student)
* [<span data-ttu-id="60728-118">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="60728-118">Azure CLI</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)
* [<span data-ttu-id="60728-119">Azure Container Service (AKS) cluster running Kubernetes</span><span class="sxs-lookup"><span data-stu-id="60728-119">Azure Container Service (AKS) cluster running Kubernetes</span></span>](https://docs.microsoft.com/azure/container-service/kubernetes/container-service-tutorial-kubernetes-deploy-cluster)
* [<span data-ttu-id="60728-120">Azure Container Registy (ACR) account</span><span class="sxs-lookup"><span data-stu-id="60728-120">Azure Container Registy (ACR) account</span></span>](https://docs.microsoft.com/azure/container-registry/container-registry-get-started-portal)
* [<span data-ttu-id="60728-121">Install Kubectl to run commands against Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="60728-121">Install Kubectl to run commands against Kubernetes cluster.</span></span>](https://kubernetes.io/docs/tasks/tools/install-kubectl/) <span data-ttu-id="60728-122">We will need this to fetch configuration from ACS cluster.</span><span class="sxs-lookup"><span data-stu-id="60728-122">We will need this to fetch configuration from ACS cluster.</span></span> 
* <span data-ttu-id="60728-123">Fork the repository to your GitHub account.</span><span class="sxs-lookup"><span data-stu-id="60728-123">Fork the repository to your GitHub account.</span></span>

## <a name="description-of-the-cicd-pipeline"></a><span data-ttu-id="60728-124">Description of the CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="60728-124">Description of the CI/CD pipeline</span></span>
<span data-ttu-id="60728-125">The pipeline kicks off for each new commit, run the test suite, if the test passes takes the latest build, packages it in a Docker container.</span><span class="sxs-lookup"><span data-stu-id="60728-125">The pipeline kicks off for each new commit, run the test suite, if the test passes takes the latest build, packages it in a Docker container.</span></span> <span data-ttu-id="60728-126">The container is then deployed using Azure container service (ACS) and images are securely stored in Azure container registry (ACR).</span><span class="sxs-lookup"><span data-stu-id="60728-126">The container is then deployed using Azure container service (ACS) and images are securely stored in Azure container registry (ACR).</span></span> <span data-ttu-id="60728-127">ACS is running Kubernetes for managing container cluster but you can choose Docker Swarm or Mesos.</span><span class="sxs-lookup"><span data-stu-id="60728-127">ACS is running Kubernetes for managing container cluster but you can choose Docker Swarm or Mesos.</span></span>

<span data-ttu-id="60728-128">The application securely pulls the latest model from an Azure Storage account and packages that as part of the application.</span><span class="sxs-lookup"><span data-stu-id="60728-128">The application securely pulls the latest model from an Azure Storage account and packages that as part of the application.</span></span> <span data-ttu-id="60728-129">The deployed application has the app code and ML model packaged as single container.</span><span class="sxs-lookup"><span data-stu-id="60728-129">The deployed application has the app code and ML model packaged as single container.</span></span> <span data-ttu-id="60728-130">This decouples the app developers and data scientists, to make sure that their production app is always running the latest code with latest ML model.</span><span class="sxs-lookup"><span data-stu-id="60728-130">This decouples the app developers and data scientists, to make sure that their production app is always running the latest code with latest ML model.</span></span>

<span data-ttu-id="60728-131">The pipeline architecture is given below.</span><span class="sxs-lookup"><span data-stu-id="60728-131">The pipeline architecture is given below.</span></span> 

![Architecture](./media/ci-cd-flask/Architecture.PNG?raw=true)

## <a name="steps-of-the-cicd-pipeline"></a><span data-ttu-id="60728-133">Steps of the CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="60728-133">Steps of the CI/CD pipeline</span></span>
1. <span data-ttu-id="60728-134">Developer work on the IDE of their choice on the application code.</span><span class="sxs-lookup"><span data-stu-id="60728-134">Developer work on the IDE of their choice on the application code.</span></span>
2. <span data-ttu-id="60728-135">They commit the code to source control of their choice (Azure DevOps has good support for various source controls)</span><span class="sxs-lookup"><span data-stu-id="60728-135">They commit the code to source control of their choice (Azure DevOps has good support for various source controls)</span></span>
3. <span data-ttu-id="60728-136">Separately, the data scientist work on developing their model.</span><span class="sxs-lookup"><span data-stu-id="60728-136">Separately, the data scientist work on developing their model.</span></span>
4. <span data-ttu-id="60728-137">Once happy, they publish the model to a model repository, in this case we are using a blob storage account.</span><span class="sxs-lookup"><span data-stu-id="60728-137">Once happy, they publish the model to a model repository, in this case we are using a blob storage account.</span></span> <span data-ttu-id="60728-138">This could be easily replaced with Azure ML Workbench's Model management service through their REST APIs.</span><span class="sxs-lookup"><span data-stu-id="60728-138">This could be easily replaced with Azure ML Workbench's Model management service through their REST APIs.</span></span>
5. <span data-ttu-id="60728-139">A build is kicked off in Azure DevOps based on the commit in GitHub.</span><span class="sxs-lookup"><span data-stu-id="60728-139">A build is kicked off in Azure DevOps based on the commit in GitHub.</span></span>
6. <span data-ttu-id="60728-140">Azure DevOps Build pipeline pulls the latest model from Blob container and creates a container.</span><span class="sxs-lookup"><span data-stu-id="60728-140">Azure DevOps Build pipeline pulls the latest model from Blob container and creates a container.</span></span>
7. <span data-ttu-id="60728-141">Azure DevOps pushes the image to private image repository in Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="60728-141">Azure DevOps pushes the image to private image repository in Azure Container Registry</span></span>
8. <span data-ttu-id="60728-142">On a set schedule (nightly), release pipeline is kicked off.</span><span class="sxs-lookup"><span data-stu-id="60728-142">On a set schedule (nightly), release pipeline is kicked off.</span></span>
9. <span data-ttu-id="60728-143">Latest image from ACR is pulled and deployed across Kubernetes cluster on ACS.</span><span class="sxs-lookup"><span data-stu-id="60728-143">Latest image from ACR is pulled and deployed across Kubernetes cluster on ACS.</span></span>
10. <span data-ttu-id="60728-144">Users request for the app goes through DNS server.</span><span class="sxs-lookup"><span data-stu-id="60728-144">Users request for the app goes through DNS server.</span></span>
11. <span data-ttu-id="60728-145">DNS server passes the request to load balancer and sends the response back to user.</span><span class="sxs-lookup"><span data-stu-id="60728-145">DNS server passes the request to load balancer and sends the response back to user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60728-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="60728-146">Next steps</span></span>
* <span data-ttu-id="60728-147">Refer to the [tutorial](https://github.com/Azure/DevOps-For-AI-Apps/blob/master/Tutorial.md) to follow the details and implement your own CI/CD pipeline for your application.</span><span class="sxs-lookup"><span data-stu-id="60728-147">Refer to the [tutorial](https://github.com/Azure/DevOps-For-AI-Apps/blob/master/Tutorial.md) to follow the details and implement your own CI/CD pipeline for your application.</span></span>

## <a name="references"></a><span data-ttu-id="60728-148">References</span><span class="sxs-lookup"><span data-stu-id="60728-148">References</span></span>
* [<span data-ttu-id="60728-149">Team Data Science Process (TDSP)</span><span class="sxs-lookup"><span data-stu-id="60728-149">Team Data Science Process (TDSP)</span></span>](https://aka.ms/tdsp)
* [<span data-ttu-id="60728-150">Azure Machine Learning (AML)</span><span class="sxs-lookup"><span data-stu-id="60728-150">Azure Machine Learning (AML)</span></span>](https://docs.microsoft.com/azure/machine-learning/service/)
* [<span data-ttu-id="60728-151">Visual Studio Team Services (VSTS)</span><span class="sxs-lookup"><span data-stu-id="60728-151">Visual Studio Team Services (VSTS)</span></span>](https://www.visualstudio.com/vso/)
* [<span data-ttu-id="60728-152">Azure Kubernetes Services (AKS)</span><span class="sxs-lookup"><span data-stu-id="60728-152">Azure Kubernetes Services (AKS)</span></span>](https://docs.microsoft.com/azure/aks/intro-kubernetes)
