---
title: Jenkins CI/CD with Kubernetes in Azure Container Service | Microsoft Docs
description: How to automate a CI/CD process with Jenkins to deploy and upgrade a containerized app on Kubernetes in Azure Container Service
services: container-service
documentationcenter: ''
author: chzbrgr71
manager: johny
editor: ''
tags: acs, azure-container-service, jenkins
keywords: Docker, Containers, Kubernetes, Azure, Jenkins
ms.assetid: ''
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.openlocfilehash: 011d56c88d97c89194087a2805de8246198813a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563789"
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="e76b8-104">Jenkins integration with Azure Container Service and Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e76b8-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="e76b8-105">In this tutorial, we walk through the process to set up continuous integration of a multi-container application into Azure Container Service Kubernetes using the Jenkins platform.</span><span class="sxs-lookup"><span data-stu-id="e76b8-105">In this tutorial, we walk through the process to set up continuous integration of a multi-container application into Azure Container Service Kubernetes using the Jenkins platform.</span></span> <span data-ttu-id="e76b8-106">The workflow updates the container image in Docker Hub and upgrades the Kubernetes pods using a deployment rollout.</span><span class="sxs-lookup"><span data-stu-id="e76b8-106">The workflow updates the container image in Docker Hub and upgrades the Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="e76b8-107">High level process</span><span class="sxs-lookup"><span data-stu-id="e76b8-107">High level process</span></span>
<span data-ttu-id="e76b8-108">The basic steps detailed in this article are:</span><span class="sxs-lookup"><span data-stu-id="e76b8-108">The basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="e76b8-109">Install a Kubernetes cluster in Container Service</span><span class="sxs-lookup"><span data-stu-id="e76b8-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="e76b8-110">Set up Jenkins and configure access to Container Service</span><span class="sxs-lookup"><span data-stu-id="e76b8-110">Set up Jenkins and configure access to Container Service</span></span>
- <span data-ttu-id="e76b8-111">Create a Jenkins workflow</span><span class="sxs-lookup"><span data-stu-id="e76b8-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="e76b8-112">Test the CI/CD process end to end</span><span class="sxs-lookup"><span data-stu-id="e76b8-112">Test the CI/CD process end to end</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="e76b8-113">Install a Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="e76b8-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="e76b8-114">Deploy the Kubernetes cluster in Azure Container Service using the following steps.</span><span class="sxs-lookup"><span data-stu-id="e76b8-114">Deploy the Kubernetes cluster in Azure Container Service using the following steps.</span></span> <span data-ttu-id="e76b8-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e76b8-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="e76b8-116">Step 1: Create a resource group</span><span class="sxs-lookup"><span data-stu-id="e76b8-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-the-cluster"></a><span data-ttu-id="e76b8-117">Step 2: Deploy the cluster</span><span class="sxs-lookup"><span data-stu-id="e76b8-117">Step 2: Deploy the cluster</span></span>
> [!NOTE]
> <span data-ttu-id="e76b8-118">The following steps require a local SSH public key stored in the ~/.ssh folder.</span><span class="sxs-lookup"><span data-stu-id="e76b8-118">The following steps require a local SSH public key stored in the ~/.ssh folder.</span></span>
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \ 
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \ 
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-to-container-service"></a><span data-ttu-id="e76b8-119">Set up Jenkins and configure access to Container Service</span><span class="sxs-lookup"><span data-stu-id="e76b8-119">Set up Jenkins and configure access to Container Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="e76b8-120">Step 1: Install Jenkins</span><span class="sxs-lookup"><span data-stu-id="e76b8-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="e76b8-121">Create an Azure VM with Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="e76b8-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span> 
2. <span data-ttu-id="e76b8-122">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="e76b8-122">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span>
3. <span data-ttu-id="e76b8-123">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="e76b8-123">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
4. <span data-ttu-id="e76b8-124">Update the Azure network security group to allow port 8080 and then browse the public IP at port 8080 to manage Jenkins in your browser.</span><span class="sxs-lookup"><span data-stu-id="e76b8-124">Update the Azure network security group to allow port 8080 and then browse the public IP at port 8080 to manage Jenkins in your browser.</span></span>
5. <span data-ttu-id="e76b8-125">Initial Jenkins admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword.</span><span class="sxs-lookup"><span data-stu-id="e76b8-125">Initial Jenkins admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword.</span></span>
6. <span data-ttu-id="e76b8-126">Install Docker on the Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="e76b8-126">Install Docker on the Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="e76b8-127">This allows for Docker commands to be run in Jenkins jobs.</span><span class="sxs-lookup"><span data-stu-id="e76b8-127">This allows for Docker commands to be run in Jenkins jobs.</span></span>
7. <span data-ttu-id="e76b8-128">Configure Docker permissions to allow Jenkins to access endpoint.</span><span class="sxs-lookup"><span data-stu-id="e76b8-128">Configure Docker permissions to allow Jenkins to access endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="e76b8-129">Install `kubectl` CLI on Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e76b8-129">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="e76b8-130">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="e76b8-130">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-to-the-kubernetes-cluster"></a><span data-ttu-id="e76b8-131">Step 2: Set up access to the Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="e76b8-131">Step 2: Set up access to the Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="e76b8-132">There are multiple approaches to accomplishing the following steps.</span><span class="sxs-lookup"><span data-stu-id="e76b8-132">There are multiple approaches to accomplishing the following steps.</span></span> <span data-ttu-id="e76b8-133">Use the approach that is easiest for you.</span><span class="sxs-lookup"><span data-stu-id="e76b8-133">Use the approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="e76b8-134">Copy the `kubectl` config file to the Jenkins machine.</span><span class="sxs-lookup"><span data-stu-id="e76b8-134">Copy the `kubectl` config file to the Jenkins machine.</span></span>

    ```bash
    export KUBE_MASTER=<your_cluster_master_fqdn>
        
    sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config user@<your_jenkins_server>:~/.kube/config
        
    sudo ssh user@<your_jenkins_server> sudo chmod 777 /home/user/.kube/config

    sudo ssh -i ~/.ssh/id_rsa user@<your_jenkins_server> sudo chmod 777 /home/user/.kube/config
        
    sudo ssh -i ~/.ssh/id_rsa user@<your_jenkins_server> sudo cp /home/user/.kube/config /var/lib/jenkins/config
    ```
        
2. <span data-ttu-id="e76b8-135">Validate from Jenkins that the Kubernetes cluster is accessible.</span><span class="sxs-lookup"><span data-stu-id="e76b8-135">Validate from Jenkins that the Kubernetes cluster is accessible.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="e76b8-136">Create a Jenkins workflow</span><span class="sxs-lookup"><span data-stu-id="e76b8-136">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e76b8-137">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e76b8-137">Prerequisites</span></span>

- <span data-ttu-id="e76b8-138">GitHub account for code repo.</span><span class="sxs-lookup"><span data-stu-id="e76b8-138">GitHub account for code repo.</span></span>
- <span data-ttu-id="e76b8-139">Docker Hub account to store and update images.</span><span class="sxs-lookup"><span data-stu-id="e76b8-139">Docker Hub account to store and update images.</span></span>
- <span data-ttu-id="e76b8-140">Containerized application that can be rebuilt and updated.</span><span class="sxs-lookup"><span data-stu-id="e76b8-140">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="e76b8-141">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="e76b8-141">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="e76b8-142">The following steps must be performed in your own GitHub account.</span><span class="sxs-lookup"><span data-stu-id="e76b8-142">The following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="e76b8-143">Feel free to clone the above repo, but you must use your own account to configure the webhooks and Jenkins access.</span><span class="sxs-lookup"><span data-stu-id="e76b8-143">Feel free to clone the above repo, but you must use your own account to configure the webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="e76b8-144">Step 1: Deploy initial v1 of application</span><span class="sxs-lookup"><span data-stu-id="e76b8-144">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="e76b8-145">Build the app from the developer machine with the following commands.</span><span class="sxs-lookup"><span data-stu-id="e76b8-145">Build the app from the developer machine with the following commands.</span></span> <span data-ttu-id="e76b8-146">Replace `myrepo` with your own.</span><span class="sxs-lookup"><span data-stu-id="e76b8-146">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="e76b8-147">Push image to Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="e76b8-147">Push image to Docker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="e76b8-148">Deploy to the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="e76b8-148">Deploy to the Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="e76b8-149">Edit the `go-web.yaml` file to update your container image and repo.</span><span class="sxs-lookup"><span data-stu-id="e76b8-149">Edit the `go-web.yaml` file to update your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="e76b8-150">Step 2: Configure Jenkins system</span><span class="sxs-lookup"><span data-stu-id="e76b8-150">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="e76b8-151">Click **Manage Jenkins** > **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="e76b8-151">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="e76b8-152">Under **GitHub**, select **Add GitHub Server**.</span><span class="sxs-lookup"><span data-stu-id="e76b8-152">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="e76b8-153">Leave **API URL** as default.</span><span class="sxs-lookup"><span data-stu-id="e76b8-153">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="e76b8-154">Under **Credentials**, add a Jenkins credential using **Secret text**.</span><span class="sxs-lookup"><span data-stu-id="e76b8-154">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="e76b8-155">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span><span class="sxs-lookup"><span data-stu-id="e76b8-155">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="e76b8-156">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="e76b8-156">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="e76b8-157">Click **Test connection** to ensure this is configured correctly.</span><span class="sxs-lookup"><span data-stu-id="e76b8-157">Click **Test connection** to ensure this is configured correctly.</span></span>
6. <span data-ttu-id="e76b8-158">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span><span class="sxs-lookup"><span data-stu-id="e76b8-158">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="e76b8-159">(This is useful in this demo, but a production scenario would require a more secure approach.)</span><span class="sxs-lookup"><span data-stu-id="e76b8-159">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="e76b8-160">Save.</span><span class="sxs-lookup"><span data-stu-id="e76b8-160">Save.</span></span>

![Jenkins GitHub access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-the-jenkins-workflow"></a><span data-ttu-id="e76b8-162">Step 3: Create the Jenkins workflow</span><span class="sxs-lookup"><span data-stu-id="e76b8-162">Step 3: Create the Jenkins workflow</span></span>
1. <span data-ttu-id="e76b8-163">Create a Jenkins item.</span><span class="sxs-lookup"><span data-stu-id="e76b8-163">Create a Jenkins item.</span></span>
2. <span data-ttu-id="e76b8-164">Provide a name (for example, "go-web") and select **Freestyle Project**.</span><span class="sxs-lookup"><span data-stu-id="e76b8-164">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="e76b8-165">Check **GitHub project** and provide the URL to your GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="e76b8-165">Check **GitHub project** and provide the URL to your GitHub repo.</span></span>
4. <span data-ttu-id="e76b8-166">In **Source Code Management**, provide the GitHub repo URL and credentials.</span><span class="sxs-lookup"><span data-stu-id="e76b8-166">In **Source Code Management**, provide the GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="e76b8-167">Add a **Build Step** of type **Execute shell** and use the following text:</span><span class="sxs-lookup"><span data-stu-id="e76b8-167">Add a **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="e76b8-168">Add another **Build Step** of type **Execute shell** and use the following text:</span><span class="sxs-lookup"><span data-stu-id="e76b8-168">Add another **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins build steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="e76b8-170">Save the Jenkins item and test with **Build Now**.</span><span class="sxs-lookup"><span data-stu-id="e76b8-170">Save the Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="e76b8-171">Step 4: Connect GitHub webhook</span><span class="sxs-lookup"><span data-stu-id="e76b8-171">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="e76b8-172">In the Jenkins item you created, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="e76b8-172">In the Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="e76b8-173">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span><span class="sxs-lookup"><span data-stu-id="e76b8-173">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="e76b8-174">This automatically configures the GitHub webhook.</span><span class="sxs-lookup"><span data-stu-id="e76b8-174">This automatically configures the GitHub webhook.</span></span>
3. <span data-ttu-id="e76b8-175">In your GitHub repo for go-web, click **Settings > Webhooks**.</span><span class="sxs-lookup"><span data-stu-id="e76b8-175">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="e76b8-176">Verify that the Jenkins webhook URL was added successfully.</span><span class="sxs-lookup"><span data-stu-id="e76b8-176">Verify that the Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="e76b8-177">The URL should end in "github-webhook".</span><span class="sxs-lookup"><span data-stu-id="e76b8-177">The URL should end in "github-webhook".</span></span>

![Jenkins webhook configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-the-cicd-process-end-to-end"></a><span data-ttu-id="e76b8-179">Test the CI/CD process end to end</span><span class="sxs-lookup"><span data-stu-id="e76b8-179">Test the CI/CD process end to end</span></span>

1. <span data-ttu-id="e76b8-180">Update code for the repo and push/synch with the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="e76b8-180">Update code for the repo and push/synch with the GitHub repository.</span></span>
2. <span data-ttu-id="e76b8-181">From the Jenkins console, check the **Build History** and validate that the job has run.</span><span class="sxs-lookup"><span data-stu-id="e76b8-181">From the Jenkins console, check the **Build History** and validate that the job has run.</span></span> <span data-ttu-id="e76b8-182">View console output to see details.</span><span class="sxs-lookup"><span data-stu-id="e76b8-182">View console output to see details.</span></span>
3. <span data-ttu-id="e76b8-183">From Kubernetes, view details of the upgraded deployment:</span><span class="sxs-lookup"><span data-stu-id="e76b8-183">From Kubernetes, view details of the upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="e76b8-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="e76b8-184">Next steps</span></span>

- <span data-ttu-id="e76b8-185">Deploy Azure Container Registry and store images in a secure repository.</span><span class="sxs-lookup"><span data-stu-id="e76b8-185">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="e76b8-186">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="e76b8-186">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="e76b8-187">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="e76b8-187">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="e76b8-188">For more information about CI/CD with Jenkins and Kubernetes, see the [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="e76b8-188">For more information about CI/CD with Jenkins and Kubernetes, see the [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>



