---
title: Jenkins continuous deployment with Kubernetes in Azure Kubernetes Service
description: How to automate a continuous deployment process with Jenkins to deploy and upgrade a containerized app on Kubernetes in Azure Kubernetes Service
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 03/26/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a1a6799bc049fea829f8e32d12705e26e3a41dc0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857560"
---
# <a name="continuous-deployment-with-jenkins-and-azure-kubernetes-service"></a><span data-ttu-id="4fb7d-103">Continuous deployment with Jenkins and Azure Kubernetes Service</span><span class="sxs-lookup"><span data-stu-id="4fb7d-103">Continuous deployment with Jenkins and Azure Kubernetes Service</span></span>

<span data-ttu-id="4fb7d-104">This document demonstrates how to set up a basic continuous deployment workflow between Jenkins and an Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-104">This document demonstrates how to set up a basic continuous deployment workflow between Jenkins and an Azure Kubernetes Service (AKS) cluster.</span></span>

<span data-ttu-id="4fb7d-105">The example workflow includes the following steps:</span><span class="sxs-lookup"><span data-stu-id="4fb7d-105">The example workflow includes the following steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4fb7d-106">Deploy the Azure vote application to your Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-106">Deploy the Azure vote application to your Kubernetes cluster.</span></span>
> * <span data-ttu-id="4fb7d-107">Update the Azure vote application code and push to a GitHub repository, which starts the continuous deployment process.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-107">Update the Azure vote application code and push to a GitHub repository, which starts the continuous deployment process.</span></span>
> * <span data-ttu-id="4fb7d-108">Jenkins clones the repository, and builds a new container image with the updated code.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-108">Jenkins clones the repository, and builds a new container image with the updated code.</span></span>
> * <span data-ttu-id="4fb7d-109">This image is pushed to Azure Container Registry (ACR).</span><span class="sxs-lookup"><span data-stu-id="4fb7d-109">This image is pushed to Azure Container Registry (ACR).</span></span>
> * <span data-ttu-id="4fb7d-110">The application running in the AKS cluster is updated with the new container image.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-110">The application running in the AKS cluster is updated with the new container image.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fb7d-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4fb7d-111">Prerequisites</span></span>

<span data-ttu-id="4fb7d-112">You need the following items in order to complete the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-112">You need the following items in order to complete the steps in this article.</span></span>

- <span data-ttu-id="4fb7d-113">Basic understanding of Kubernetes, Git, CI/CD, and Azure Container Registry (ACR).</span><span class="sxs-lookup"><span data-stu-id="4fb7d-113">Basic understanding of Kubernetes, Git, CI/CD, and Azure Container Registry (ACR).</span></span>
- <span data-ttu-id="4fb7d-114">An [Azure Kubernetes Service (AKS) cluster][aks-quickstart] and [AKS credentials configured][aks-credentials] on your development system.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-114">An [Azure Kubernetes Service (AKS) cluster][aks-quickstart] and [AKS credentials configured][aks-credentials] on your development system.</span></span>
- <span data-ttu-id="4fb7d-115">An [Azure Container Registry (ACR) registry][acr-quickstart], the ACR login server name, and [ACR credentials][acr-authentication] with push and pull access.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-115">An [Azure Container Registry (ACR) registry][acr-quickstart], the ACR login server name, and [ACR credentials][acr-authentication] with push and pull access.</span></span>
- <span data-ttu-id="4fb7d-116">Azure CLI installed on your development system.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-116">Azure CLI installed on your development system.</span></span>
- <span data-ttu-id="4fb7d-117">Docker installed on your development system.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-117">Docker installed on your development system.</span></span>
- <span data-ttu-id="4fb7d-118">GitHub account, [GitHub personal access token][git-access-token], and Git client installed on your development system.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-118">GitHub account, [GitHub personal access token][git-access-token], and Git client installed on your development system.</span></span>

## <a name="prepare-application"></a><span data-ttu-id="4fb7d-119">Prepare application</span><span class="sxs-lookup"><span data-stu-id="4fb7d-119">Prepare application</span></span>

<span data-ttu-id="4fb7d-120">The Azure vote application used throughout this document contains a web interface hosted in one or more pods, and a second pod hosting Redis for temporary data storage.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-120">The Azure vote application used throughout this document contains a web interface hosted in one or more pods, and a second pod hosting Redis for temporary data storage.</span></span>

<span data-ttu-id="4fb7d-121">Before building the Jenkins / AKS integration, prepare and deploy the Azure vote application to your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-121">Before building the Jenkins / AKS integration, prepare and deploy the Azure vote application to your AKS cluster.</span></span> <span data-ttu-id="4fb7d-122">Think of this as version one of the application.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-122">Think of this as version one of the application.</span></span>

<span data-ttu-id="4fb7d-123">Fork the following GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-123">Fork the following GitHub repository.</span></span>

```
https://github.com/Azure-Samples/azure-voting-app-redis
```

<span data-ttu-id="4fb7d-124">Once the fork has been created, clone it your development system.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-124">Once the fork has been created, clone it your development system.</span></span> <span data-ttu-id="4fb7d-125">Ensure that you are using the URL of your fork when cloning this repo.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-125">Ensure that you are using the URL of your fork when cloning this repo.</span></span>

```bash
git clone https://github.com/<your-github-account>/azure-voting-app-redis.git
```

<span data-ttu-id="4fb7d-126">Change directories so that you are working from the cloned directory.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-126">Change directories so that you are working from the cloned directory.</span></span>

```bash
cd azure-voting-app-redis
```

<span data-ttu-id="4fb7d-127">Run the `docker-compose.yaml` file to create the `azure-vote-front` container image and start the application.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-127">Run the `docker-compose.yaml` file to create the `azure-vote-front` container image and start the application.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="4fb7d-128">When completed, use the [docker images][docker-images] command to see the created image.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-128">When completed, use the [docker images][docker-images] command to see the created image.</span></span>

<span data-ttu-id="4fb7d-129">Notice that three images have been downloaded or created.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-129">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="4fb7d-130">The `azure-vote-front` image contains the application and uses the `nginx-flask` image as a base.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-130">The `azure-vote-front` image contains the application and uses the `nginx-flask` image as a base.</span></span> <span data-ttu-id="4fb7d-131">The `redis` image is used to start a Redis instance.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-131">The `redis` image is used to start a Redis instance.</span></span>

```console
$ docker images

REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="4fb7d-132">Get the ACR login server with the [az acr list][az-acr-list] command.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-132">Get the ACR login server with the [az acr list][az-acr-list] command.</span></span> <span data-ttu-id="4fb7d-133">Make sure to update the resource group name with the resource group hosting your ACR registry.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-133">Make sure to update the resource group name with the resource group hosting your ACR registry.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="4fb7d-134">Use the [docker tag][docker-tag] command to tag the image with the login server name and a version number of `v1`.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-134">Use the [docker tag][docker-tag] command to tag the image with the login server name and a version number of `v1`.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:v1
```

<span data-ttu-id="4fb7d-135">Update the ACR login server value with your ACR login server name, and push the `azure-vote-front` image to the registry.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-135">Update the ACR login server value with your ACR login server name, and push the `azure-vote-front` image to the registry.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:v1
```

## <a name="deploy-application-to-kubernetes"></a><span data-ttu-id="4fb7d-136">Deploy application to Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4fb7d-136">Deploy application to Kubernetes</span></span>

<span data-ttu-id="4fb7d-137">A Kubernetes manifest file can be found at the root of the Azure vote repository and can be used to deploy the application to your Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-137">A Kubernetes manifest file can be found at the root of the Azure vote repository and can be used to deploy the application to your Kubernetes cluster.</span></span>

<span data-ttu-id="4fb7d-138">First, update the **azure-vote-all-in-one-redis.yaml** manifest file with the location of your ACR registry.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-138">First, update the **azure-vote-all-in-one-redis.yaml** manifest file with the location of your ACR registry.</span></span> <span data-ttu-id="4fb7d-139">Open the file with any text editor and replace `microsoft` with the ACR login server name.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-139">Open the file with any text editor and replace `microsoft` with the ACR login server name.</span></span> <span data-ttu-id="4fb7d-140">This value is found on line **47** of the manifest file.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-140">This value is found on line **47** of the manifest file.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:v1
```

<span data-ttu-id="4fb7d-141">Next, use the [kubectl apply][kubectl-apply] command to run the application.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-141">Next, use the [kubectl apply][kubectl-apply] command to run the application.</span></span> <span data-ttu-id="4fb7d-142">This command parses the manifest file and creates the defined Kubernetes objects.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-142">This command parses the manifest file and creates the defined Kubernetes objects.</span></span>

```bash
kubectl apply -f azure-vote-all-in-one-redis.yaml
```

<span data-ttu-id="4fb7d-143">A [Kubernetes service][kubernetes-service] is created to expose the application to the internet.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-143">A [Kubernetes service][kubernetes-service] is created to expose the application to the internet.</span></span> <span data-ttu-id="4fb7d-144">This process can take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-144">This process can take a few minutes.</span></span>

<span data-ttu-id="4fb7d-145">To monitor progress, use the [kubectl get service][kubectl-get] command with the `--watch` argument.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-145">To monitor progress, use the [kubectl get service][kubectl-get] command with the `--watch` argument.</span></span>

```bash
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="4fb7d-146">Initially the *EXTERNAL-IP* for the *azure-vote-front* service appears as *pending*.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-146">Initially the *EXTERNAL-IP* for the *azure-vote-front* service appears as *pending*.</span></span>

```
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
```

<span data-ttu-id="4fb7d-147">Once the *EXTERNAL-IP* address has changed from *pending* to an *IP address*, use `control+c` to stop the kubectl watch process.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-147">Once the *EXTERNAL-IP* address has changed from *pending* to an *IP address*, use `control+c` to stop the kubectl watch process.</span></span>

```
azure-vote-front   10.0.34.242   13.90.150.118   80:30676/TCP   2m
```

<span data-ttu-id="4fb7d-148">To see the application, browse to the external IP address.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-148">To see the application, browse to the external IP address.</span></span>

![Image of Kubernetes cluster on Azure](media/aks-jenkins/azure-vote-safari.png)

## <a name="deploy-jenkins-to-vm"></a><span data-ttu-id="4fb7d-150">Deploy Jenkins to VM</span><span class="sxs-lookup"><span data-stu-id="4fb7d-150">Deploy Jenkins to VM</span></span>

<span data-ttu-id="4fb7d-151">A script has been pre-created to deploy a virtual machine, configure network access, and complete a basic installation of Jenkins.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-151">A script has been pre-created to deploy a virtual machine, configure network access, and complete a basic installation of Jenkins.</span></span> <span data-ttu-id="4fb7d-152">Additionally, the script copies your Kubernetes configuration file from your development system to the Jenkins system.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-152">Additionally, the script copies your Kubernetes configuration file from your development system to the Jenkins system.</span></span> <span data-ttu-id="4fb7d-153">This file is used for authentication between Jenkins and the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-153">This file is used for authentication between Jenkins and the AKS cluster.</span></span>

<span data-ttu-id="4fb7d-154">Run the following commands to download and run the script.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-154">Run the following commands to download and run the script.</span></span> <span data-ttu-id="4fb7d-155">The below URL can also be used to review the content of the script.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-155">The below URL can also be used to review the content of the script.</span></span>

> [!WARNING]
> <span data-ttu-id="4fb7d-156">This sample script is for demo purposes to quickly provision a Jenkins environment that runs on an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-156">This sample script is for demo purposes to quickly provision a Jenkins environment that runs on an Azure VM.</span></span> <span data-ttu-id="4fb7d-157">It uses the Azure custom script extension to configure a VM and then display the required credentials.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-157">It uses the Azure custom script extension to configure a VM and then display the required credentials.</span></span> <span data-ttu-id="4fb7d-158">Your *~/.kube/config* is copied to the Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-158">Your *~/.kube/config* is copied to the Jenkins VM.</span></span>

```console
curl https://raw.githubusercontent.com/Azure-Samples/azure-voting-app-redis/master/jenkins-tutorial/deploy-jenkins-vm.sh > azure-jenkins.sh
sh azure-jenkins.sh
```

<span data-ttu-id="4fb7d-159">When the script has completed, it outputs an address for the Jenkins server, as well a key to unlock Jenkins.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-159">When the script has completed, it outputs an address for the Jenkins server, as well a key to unlock Jenkins.</span></span> <span data-ttu-id="4fb7d-160">Browse to the URL, enter the key, and following the on-screen prompts to complete the Jenkins configuration.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-160">Browse to the URL, enter the key, and following the on-screen prompts to complete the Jenkins configuration.</span></span>

```console
Open a browser to http://52.166.118.64:8080
Enter the following to Unlock Jenkins:
667e24bba78f4de6b51d330ad89ec6c6
```

## <a name="jenkins-environment-variables"></a><span data-ttu-id="4fb7d-161">Jenkins environment variables</span><span class="sxs-lookup"><span data-stu-id="4fb7d-161">Jenkins environment variables</span></span>

<span data-ttu-id="4fb7d-162">A Jenkins environment variable is used to hold Azure Container Registry (ACR) login server name.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-162">A Jenkins environment variable is used to hold Azure Container Registry (ACR) login server name.</span></span> <span data-ttu-id="4fb7d-163">This variable is referenced during the Jenkins continuous deployment job.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-163">This variable is referenced during the Jenkins continuous deployment job.</span></span>

<span data-ttu-id="4fb7d-164">While on the Jenkins admin portal, click **Manage Jenkins** > **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-164">While on the Jenkins admin portal, click **Manage Jenkins** > **Configure System**.</span></span>

<span data-ttu-id="4fb7d-165">Under **Global Properties**, select **Environment variables**, and add a variable with the name `ACR_LOGINSERVER` and a value of your ACR login server.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-165">Under **Global Properties**, select **Environment variables**, and add a variable with the name `ACR_LOGINSERVER` and a value of your ACR login server.</span></span>

![Jenkins environment variables](media/aks-jenkins/env-variables.png)

<span data-ttu-id="4fb7d-167">When complete, click **Save** on the Jenkins configuration page.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-167">When complete, click **Save** on the Jenkins configuration page.</span></span>

## <a name="jenkins-credentials"></a><span data-ttu-id="4fb7d-168">Jenkins credentials</span><span class="sxs-lookup"><span data-stu-id="4fb7d-168">Jenkins credentials</span></span>

<span data-ttu-id="4fb7d-169">Now store your ACR credentials in a Jenkins credential object.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-169">Now store your ACR credentials in a Jenkins credential object.</span></span> <span data-ttu-id="4fb7d-170">These credentials are referenced during the Jenkins build job.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-170">These credentials are referenced during the Jenkins build job.</span></span>

<span data-ttu-id="4fb7d-171">Back on the Jenkins admin portal, click **Credentials** > **Jenkins** > **Global credentials (unrestricted)** > **Add Credentials**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-171">Back on the Jenkins admin portal, click **Credentials** > **Jenkins** > **Global credentials (unrestricted)** > **Add Credentials**.</span></span>

<span data-ttu-id="4fb7d-172">Ensure that the credential kind is **Username with password** and enter the following items:</span><span class="sxs-lookup"><span data-stu-id="4fb7d-172">Ensure that the credential kind is **Username with password** and enter the following items:</span></span>

- <span data-ttu-id="4fb7d-173">**Username** - ID of the service principal use for authentication with your ACR registry.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-173">**Username** - ID of the service principal use for authentication with your ACR registry.</span></span>
- <span data-ttu-id="4fb7d-174">**Password** - Client secret of the service principal use for authentication with your ACR registry.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-174">**Password** - Client secret of the service principal use for authentication with your ACR registry.</span></span>
- <span data-ttu-id="4fb7d-175">**ID** - Credential identifier such as `acr-credentials`.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-175">**ID** - Credential identifier such as `acr-credentials`.</span></span>

<span data-ttu-id="4fb7d-176">When complete, the credentials form should look similar to this image:</span><span class="sxs-lookup"><span data-stu-id="4fb7d-176">When complete, the credentials form should look similar to this image:</span></span>

![ACR credentials](media/aks-jenkins/acr-credentials.png)

<span data-ttu-id="4fb7d-178">Click **OK** and return to the Jenkins admin portal.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-178">Click **OK** and return to the Jenkins admin portal.</span></span>

## <a name="create-jenkins-project"></a><span data-ttu-id="4fb7d-179">Create Jenkins project</span><span class="sxs-lookup"><span data-stu-id="4fb7d-179">Create Jenkins project</span></span>

<span data-ttu-id="4fb7d-180">From the Jenkins admin portal, click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-180">From the Jenkins admin portal, click **New Item**.</span></span>

<span data-ttu-id="4fb7d-181">Give the project a name, for example `azure-vote`, select **Freestyle Project**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-181">Give the project a name, for example `azure-vote`, select **Freestyle Project**, and click **OK**.</span></span>

![Jenkins project](media/aks-jenkins/jenkins-project.png)

<span data-ttu-id="4fb7d-183">Under **General**, select **GitHub project** and enter the URL to your fork of the Azure vote GitHub project.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-183">Under **General**, select **GitHub project** and enter the URL to your fork of the Azure vote GitHub project.</span></span>

![GitHub project](media/aks-jenkins/github-project.png)

<span data-ttu-id="4fb7d-185">Under **Source Code Management**, select **Git**, enter the URL to your fork of the Azure Vote GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-185">Under **Source Code Management**, select **Git**, enter the URL to your fork of the Azure Vote GitHub repo.</span></span>

<span data-ttu-id="4fb7d-186">For the credentials, click on and **Add** > **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-186">For the credentials, click on and **Add** > **Jenkins**.</span></span> <span data-ttu-id="4fb7d-187">Under **Kind**, select **Secret text** and enter your [GitHub personal access token][git-access-token] as the secret.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-187">Under **Kind**, select **Secret text** and enter your [GitHub personal access token][git-access-token] as the secret.</span></span>

<span data-ttu-id="4fb7d-188">Select **Add** when done.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-188">Select **Add** when done.</span></span>

![GitHub credentials](media/aks-jenkins/github-creds.png)

<span data-ttu-id="4fb7d-190">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-190">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling**.</span></span>

![Jenkins build triggers](media/aks-jenkins/build-triggers.png)

<span data-ttu-id="4fb7d-192">Under **Build Environment**, select **Use secret texts or files**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-192">Under **Build Environment**, select **Use secret texts or files**.</span></span>

![Jenkins build environment](media/aks-jenkins/build-environment.png)

<span data-ttu-id="4fb7d-194">Under **Bindings**, select **Add** > **Username and password (separated)**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-194">Under **Bindings**, select **Add** > **Username and password (separated)**.</span></span>

<span data-ttu-id="4fb7d-195">Enter `ACR_ID` for the **Username Variable**, and `ACR_PASSWORD` for the **Password Variable**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-195">Enter `ACR_ID` for the **Username Variable**, and `ACR_PASSWORD` for the **Password Variable**.</span></span>

![Jenkins bindings](media/aks-jenkins/bindings.png)

<span data-ttu-id="4fb7d-197">Add a **Build Step** of type **Execute shell** and use the following text.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-197">Add a **Build Step** of type **Execute shell** and use the following text.</span></span> <span data-ttu-id="4fb7d-198">This script builds a new container image and pushes it to your ACR registry.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-198">This script builds a new container image and pushes it to your ACR registry.</span></span>

```bash
# Build new image and push to ACR.
WEB_IMAGE_NAME="${ACR_LOGINSERVER}/azure-vote-front:kube${BUILD_NUMBER}"
docker build -t $WEB_IMAGE_NAME ./azure-vote
docker login ${ACR_LOGINSERVER} -u ${ACR_ID} -p ${ACR_PASSWORD}
docker push $WEB_IMAGE_NAME
```

<span data-ttu-id="4fb7d-199">Add another **Build Step** of type **Execute shell** and use the following text.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-199">Add another **Build Step** of type **Execute shell** and use the following text.</span></span> <span data-ttu-id="4fb7d-200">This script updates the Kubernetes deployment.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-200">This script updates the Kubernetes deployment.</span></span>

```bash
# Update kubernetes deployment with new image.
WEB_IMAGE_NAME="${ACR_LOGINSERVER}/azure-vote-front:kube${BUILD_NUMBER}"
kubectl set image deployment/azure-vote-front azure-vote-front=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
```

<span data-ttu-id="4fb7d-201">Once completed, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-201">Once completed, click **Save**.</span></span>

## <a name="test-the-jenkins-build"></a><span data-ttu-id="4fb7d-202">Test the Jenkins build</span><span class="sxs-lookup"><span data-stu-id="4fb7d-202">Test the Jenkins build</span></span>

<span data-ttu-id="4fb7d-203">Before proceeding, test the Jenkins build.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-203">Before proceeding, test the Jenkins build.</span></span> <span data-ttu-id="4fb7d-204">This validates that the build job has been correctly configured, the proper Kubernetes authentication file is in place, and that the proper ACR credentials have been provided.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-204">This validates that the build job has been correctly configured, the proper Kubernetes authentication file is in place, and that the proper ACR credentials have been provided.</span></span>

<span data-ttu-id="4fb7d-205">Click **Build Now** in the left-hand menu of the project.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-205">Click **Build Now** in the left-hand menu of the project.</span></span>

![Jenkins test build](media/aks-jenkins/test-build.png)

<span data-ttu-id="4fb7d-207">During this process, the GitHub repository is cloned to the Jenkins build server.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-207">During this process, the GitHub repository is cloned to the Jenkins build server.</span></span> <span data-ttu-id="4fb7d-208">A new container image is built and pushed to the ACR registry.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-208">A new container image is built and pushed to the ACR registry.</span></span> <span data-ttu-id="4fb7d-209">Finally, the Azure vote application running on the AKS cluster is updated to use the new image.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-209">Finally, the Azure vote application running on the AKS cluster is updated to use the new image.</span></span> <span data-ttu-id="4fb7d-210">Because no changes have been made to the application code, the application is not changed.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-210">Because no changes have been made to the application code, the application is not changed.</span></span>

<span data-ttu-id="4fb7d-211">Once the process is complete, click on **build #1** under build history and select **Console Output** to see all output from the build process.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-211">Once the process is complete, click on **build #1** under build history and select **Console Output** to see all output from the build process.</span></span> <span data-ttu-id="4fb7d-212">The final line should indicate a successful build.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-212">The final line should indicate a successful build.</span></span>

## <a name="create-github-webhook"></a><span data-ttu-id="4fb7d-213">Create GitHub webhook</span><span class="sxs-lookup"><span data-stu-id="4fb7d-213">Create GitHub webhook</span></span>

<span data-ttu-id="4fb7d-214">Next, hook the application repository to the Jenkins build server so that on any commit, a new build is triggered.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-214">Next, hook the application repository to the Jenkins build server so that on any commit, a new build is triggered.</span></span>

1. <span data-ttu-id="4fb7d-215">Browse to the forked GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-215">Browse to the forked GitHub repository.</span></span>
2. <span data-ttu-id="4fb7d-216">Select **Settings**, then select **Webhooks** on the left-hand side.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-216">Select **Settings**, then select **Webhooks** on the left-hand side.</span></span>
3. <span data-ttu-id="4fb7d-217">Choose to **Add webhook**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-217">Choose to **Add webhook**.</span></span> <span data-ttu-id="4fb7d-218">For the *Payload URL*, enter `http://<publicIp:8080>/github-webhook/` where `publicIp` is the IP address of the Jenkins server.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-218">For the *Payload URL*, enter `http://<publicIp:8080>/github-webhook/` where `publicIp` is the IP address of the Jenkins server.</span></span> <span data-ttu-id="4fb7d-219">Make sure to include the trailing /.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-219">Make sure to include the trailing /.</span></span> <span data-ttu-id="4fb7d-220">Leave the other defaults for content type and to trigger on *push* events.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-220">Leave the other defaults for content type and to trigger on *push* events.</span></span>
4. <span data-ttu-id="4fb7d-221">Select **Add webhook**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-221">Select **Add webhook**.</span></span>

    ![GitHub webhook](media/aks-jenkins/webhook.png)

## <a name="test-cicd-process-end-to-end"></a><span data-ttu-id="4fb7d-223">Test CI/CD process end to end</span><span class="sxs-lookup"><span data-stu-id="4fb7d-223">Test CI/CD process end to end</span></span>

<span data-ttu-id="4fb7d-224">On your development machine, open up the cloned application with a code editor.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-224">On your development machine, open up the cloned application with a code editor.</span></span>

<span data-ttu-id="4fb7d-225">Under the **/azure-vote/azure-vote** directory, find a file named **config_file.cfg**.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-225">Under the **/azure-vote/azure-vote** directory, find a file named **config_file.cfg**.</span></span> <span data-ttu-id="4fb7d-226">Update the vote values in this file to something other than cats and dogs.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-226">Update the vote values in this file to something other than cats and dogs.</span></span>

<span data-ttu-id="4fb7d-227">The following example shows and updated **config_file.cfg** file.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-227">The following example shows and updated **config_file.cfg** file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="4fb7d-228">When complete, save the file, commit the changes, and push these to your fork of the GitHub repository..</span><span class="sxs-lookup"><span data-stu-id="4fb7d-228">When complete, save the file, commit the changes, and push these to your fork of the GitHub repository..</span></span> <span data-ttu-id="4fb7d-229">Once the commit has completed, the GitHub webhook triggers a new Jenkins build, which updates the container image, and the AKS deployment.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-229">Once the commit has completed, the GitHub webhook triggers a new Jenkins build, which updates the container image, and the AKS deployment.</span></span> <span data-ttu-id="4fb7d-230">Monitor the build process on the Jenkins admin console.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-230">Monitor the build process on the Jenkins admin console.</span></span>

<span data-ttu-id="4fb7d-231">Once the build has completed, browse again to the application endpoint to observe the changes.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-231">Once the build has completed, browse again to the application endpoint to observe the changes.</span></span>

![Azure vote updated](media/aks-jenkins/azure-vote-updated-safari.png)

<span data-ttu-id="4fb7d-233">At this point, a simple continuous deployment process has been completed.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-233">At this point, a simple continuous deployment process has been completed.</span></span> <span data-ttu-id="4fb7d-234">The steps and configurations shown in this example can be used to build out a more robust and production-ready continuous build automation.</span><span class="sxs-lookup"><span data-stu-id="4fb7d-234">The steps and configurations shown in this example can be used to build out a more robust and production-ready continuous build automation.</span></span>

<!-- LINKS - external -->
[docker-images]: https://docs.docker.com/engine/reference/commandline/images/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[git-access-token]: https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubernetes-service]: https://kubernetes.io/docs/concepts/services-networking/service/

<!-- LINKS - internal -->
[az-acr-list]: /cli/azure/acr#az-acr-list
[acr-authentication]: ../container-registry/container-registry-auth-aks.md
[acr-quickstart]: ../container-registry/container-registry-get-started-azure-cli.md
[aks-credentials]: /cli/azure/aks#az-aks-get-credentials
[aks-quickstart]: kubernetes-walkthrough.md
[azure-cli-install]: /cli/azure/install-azure-cli