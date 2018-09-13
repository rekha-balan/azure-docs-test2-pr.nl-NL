---
title: Deploy to Azure Kubernetes Service (AKS) by using Jenkins and the blue/green deployment pattern
description: Learn how to deploy to Azure Kubernetes Service (AKS) by using Jenkins and the blue/green deployment pattern.
ms.service: jenkins
keywords: jenkins, azure, devops, kubernetes, k8s, aks, blue green deployment, continuous delivery, cd
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.topic: tutorial
ms.date: 07/23/2018
ms.openlocfilehash: d3d3ed8aaac16bc0a8cf817f4972ed3b771ed8d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865041"
---
# <a name="deploy-to-azure-kubernetes-service-aks-by-using-jenkins-and-the-bluegreen-deployment-pattern"></a><span data-ttu-id="9b213-104">Deploy to Azure Kubernetes Service (AKS) by using Jenkins and the blue/green deployment pattern</span><span class="sxs-lookup"><span data-stu-id="9b213-104">Deploy to Azure Kubernetes Service (AKS) by using Jenkins and the blue/green deployment pattern</span></span>

<span data-ttu-id="9b213-105">Azure Kubernetes Service (AKS) manages your hosted Kubernetes environment, making it quick and easy to deploy and manage containerized applications.</span><span class="sxs-lookup"><span data-stu-id="9b213-105">Azure Kubernetes Service (AKS) manages your hosted Kubernetes environment, making it quick and easy to deploy and manage containerized applications.</span></span> <span data-ttu-id="9b213-106">You don't need expertise in container orchestration.</span><span class="sxs-lookup"><span data-stu-id="9b213-106">You don't need expertise in container orchestration.</span></span> <span data-ttu-id="9b213-107">AKS also eliminates the burden of ongoing operations and maintenance, by provisioning, upgrading, and scaling resources on demand.</span><span class="sxs-lookup"><span data-stu-id="9b213-107">AKS also eliminates the burden of ongoing operations and maintenance, by provisioning, upgrading, and scaling resources on demand.</span></span> <span data-ttu-id="9b213-108">You don't need to take your applications offline.</span><span class="sxs-lookup"><span data-stu-id="9b213-108">You don't need to take your applications offline.</span></span> <span data-ttu-id="9b213-109">For more information about AKS, see the [AKS documentation](/azure/aks/).</span><span class="sxs-lookup"><span data-stu-id="9b213-109">For more information about AKS, see the [AKS documentation](/azure/aks/).</span></span>

<span data-ttu-id="9b213-110">Blue/green deployment is an Azure DevOps Continuous Delivery pattern that relies on keeping an existing (blue) version live, while a new (green) one is deployed.</span><span class="sxs-lookup"><span data-stu-id="9b213-110">Blue/green deployment is an Azure DevOps Continuous Delivery pattern that relies on keeping an existing (blue) version live, while a new (green) one is deployed.</span></span> <span data-ttu-id="9b213-111">Typically, this pattern employs load balancing to direct increasing amounts of traffic to the green deployment.</span><span class="sxs-lookup"><span data-stu-id="9b213-111">Typically, this pattern employs load balancing to direct increasing amounts of traffic to the green deployment.</span></span> <span data-ttu-id="9b213-112">If monitoring discovers an incident, traffic can be rerouted to the blue deployment, which is still running.</span><span class="sxs-lookup"><span data-stu-id="9b213-112">If monitoring discovers an incident, traffic can be rerouted to the blue deployment, which is still running.</span></span> <span data-ttu-id="9b213-113">For more information about Continuous Delivery, see [What is Continuous Delivery](/azure/devops/what-is-continuous-delivery).</span><span class="sxs-lookup"><span data-stu-id="9b213-113">For more information about Continuous Delivery, see [What is Continuous Delivery](/azure/devops/what-is-continuous-delivery).</span></span>

<span data-ttu-id="9b213-114">In this tutorial, you learn how to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="9b213-114">In this tutorial, you learn how to perform the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9b213-115">Learn about the blue/green deployment pattern</span><span class="sxs-lookup"><span data-stu-id="9b213-115">Learn about the blue/green deployment pattern</span></span>
> * <span data-ttu-id="9b213-116">Create a managed Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="9b213-116">Create a managed Kubernetes cluster</span></span>
> * <span data-ttu-id="9b213-117">Run a sample script to configure a Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="9b213-117">Run a sample script to configure a Kubernetes cluster</span></span>
> * <span data-ttu-id="9b213-118">Manually configure a Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="9b213-118">Manually configure a Kubernetes cluster</span></span>
> * <span data-ttu-id="9b213-119">Create and run a Jenkins job</span><span class="sxs-lookup"><span data-stu-id="9b213-119">Create and run a Jenkins job</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b213-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9b213-120">Prerequisites</span></span>
- <span data-ttu-id="9b213-121">[GitHub account](https://github.com) : You need a GitHub account to clone the sample repo.</span><span class="sxs-lookup"><span data-stu-id="9b213-121">[GitHub account](https://github.com) : You need a GitHub account to clone the sample repo.</span></span>
- <span data-ttu-id="9b213-122">[Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) : You use the Azure CLI 2.0 to create the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="9b213-122">[Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) : You use the Azure CLI 2.0 to create the Kubernetes cluster.</span></span>
- <span data-ttu-id="9b213-123">[Chocolatey](https://chocolatey.org): A package manager you use to install kubectl.</span><span class="sxs-lookup"><span data-stu-id="9b213-123">[Chocolatey](https://chocolatey.org): A package manager you use to install kubectl.</span></span>
- <span data-ttu-id="9b213-124">[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/): A command-line interface you use for running commands against Kubernetes clusters.</span><span class="sxs-lookup"><span data-stu-id="9b213-124">[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/): A command-line interface you use for running commands against Kubernetes clusters.</span></span>
- <span data-ttu-id="9b213-125">[jq](https://stedolan.github.io/jq/download/): A lightweight, command-line JSON processor.</span><span class="sxs-lookup"><span data-stu-id="9b213-125">[jq](https://stedolan.github.io/jq/download/): A lightweight, command-line JSON processor.</span></span>

## <a name="clone-the-sample-app-from-github"></a><span data-ttu-id="9b213-126">Clone the sample app from GitHub</span><span class="sxs-lookup"><span data-stu-id="9b213-126">Clone the sample app from GitHub</span></span>

<span data-ttu-id="9b213-127">On the Microsoft repo in GitHub, you can find a sample app that illustrates how to deploy to AKS by using Jenkins and the blue/green pattern.</span><span class="sxs-lookup"><span data-stu-id="9b213-127">On the Microsoft repo in GitHub, you can find a sample app that illustrates how to deploy to AKS by using Jenkins and the blue/green pattern.</span></span> <span data-ttu-id="9b213-128">In this section, you create a fork of that repo in your GitHub, and clone the app to your local system.</span><span class="sxs-lookup"><span data-stu-id="9b213-128">In this section, you create a fork of that repo in your GitHub, and clone the app to your local system.</span></span>

1. <span data-ttu-id="9b213-129">Browse to the GitHub repo for the [todo-app-java-on-azure](https://github.com/microsoft/todo-app-java-on-azure.git) sample app.</span><span class="sxs-lookup"><span data-stu-id="9b213-129">Browse to the GitHub repo for the [todo-app-java-on-azure](https://github.com/microsoft/todo-app-java-on-azure.git) sample app.</span></span>

    ![Screenshot of sample app on Microsoft GitHub repo](./media/jenkins-aks-blue-green-deployment/github-sample-msft.png)

1. <span data-ttu-id="9b213-131">Fork the repo by selecting **Fork** in the upper right of the page, and follow the instructions to fork the repo in your GitHub account.</span><span class="sxs-lookup"><span data-stu-id="9b213-131">Fork the repo by selecting **Fork** in the upper right of the page, and follow the instructions to fork the repo in your GitHub account.</span></span>

    ![Screenshot of GitHub option to fork](./media/jenkins-aks-blue-green-deployment/github-sample-msft-fork.png)

1. <span data-ttu-id="9b213-133">After you fork the repo, you see that the account name changes to your account name, and a note indicates from where the repo was forked (Microsoft).</span><span class="sxs-lookup"><span data-stu-id="9b213-133">After you fork the repo, you see that the account name changes to your account name, and a note indicates from where the repo was forked (Microsoft).</span></span>

    ![Screenshot of GitHub account name and note](./media/jenkins-aks-blue-green-deployment/github-sample-msft-forked.png)

1. <span data-ttu-id="9b213-135">Select **Clone or download**.</span><span class="sxs-lookup"><span data-stu-id="9b213-135">Select **Clone or download**.</span></span>

    ![Screenshot of GitHub option to clone or download a repo](./media/jenkins-aks-blue-green-deployment/github-sample-clone.png)

1. <span data-ttu-id="9b213-137">In the **Clone with HTTPS** window, select the **copy** icon.</span><span class="sxs-lookup"><span data-stu-id="9b213-137">In the **Clone with HTTPS** window, select the **copy** icon.</span></span>

    ![Screenshot of GitHub option to copy the clone URL to the clipboard](./media/jenkins-aks-blue-green-deployment/github-sample-copy.png)

1. <span data-ttu-id="9b213-139">Open a terminal or Git Bash window.</span><span class="sxs-lookup"><span data-stu-id="9b213-139">Open a terminal or Git Bash window.</span></span>

1. <span data-ttu-id="9b213-140">Change directories to the desired location where you want to store the local copy (clone) of the repo.</span><span class="sxs-lookup"><span data-stu-id="9b213-140">Change directories to the desired location where you want to store the local copy (clone) of the repo.</span></span>

1. <span data-ttu-id="9b213-141">Using the `git clone` command, clone the URL you copied previously.</span><span class="sxs-lookup"><span data-stu-id="9b213-141">Using the `git clone` command, clone the URL you copied previously.</span></span>

    ![Screenshot of Git Bash git clone command](./media/jenkins-aks-blue-green-deployment/git-clone-command.png)

1. <span data-ttu-id="9b213-143">Press the Enter key to start the clone process.</span><span class="sxs-lookup"><span data-stu-id="9b213-143">Press the Enter key to start the clone process.</span></span>

    ![Screenshot of Git Bash git clone command results](./media/jenkins-aks-blue-green-deployment/git-clone-results.png)

1. <span data-ttu-id="9b213-145">Change directories to the newly created directory that contains the clone of the app source.</span><span class="sxs-lookup"><span data-stu-id="9b213-145">Change directories to the newly created directory that contains the clone of the app source.</span></span>

## <a name="create-and-configure-a-managed-kubernetes-cluster"></a><span data-ttu-id="9b213-146">Create and configure a managed Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="9b213-146">Create and configure a managed Kubernetes cluster</span></span>

<span data-ttu-id="9b213-147">In this section, you perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9b213-147">In this section, you perform the following steps:</span></span>

- <span data-ttu-id="9b213-148">Use the Azure CLI 2.0 to create a managed Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="9b213-148">Use the Azure CLI 2.0 to create a managed Kubernetes cluster.</span></span>
- <span data-ttu-id="9b213-149">Learn how to set up a cluster, either by using the setup script or manually.</span><span class="sxs-lookup"><span data-stu-id="9b213-149">Learn how to set up a cluster, either by using the setup script or manually.</span></span>
- <span data-ttu-id="9b213-150">Create an instance of the Azure Container Registry service.</span><span class="sxs-lookup"><span data-stu-id="9b213-150">Create an instance of the Azure Container Registry service.</span></span>

> [!NOTE]   
> <span data-ttu-id="9b213-151">AKS is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="9b213-151">AKS is currently in preview.</span></span> <span data-ttu-id="9b213-152">For information on enabling the preview for your Azure subscription, see [Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster](/azure/aks/kubernetes-walkthrough#enabling-aks-preview-for-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="9b213-152">For information on enabling the preview for your Azure subscription, see [Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster](/azure/aks/kubernetes-walkthrough#enabling-aks-preview-for-your-azure-subscription).</span></span>

### <a name="use-the-azure-cli-20-to-create-a-managed-kubernetes-cluster"></a><span data-ttu-id="9b213-153">Use the Azure CLI 2.0 to create a managed Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="9b213-153">Use the Azure CLI 2.0 to create a managed Kubernetes cluster</span></span>
<span data-ttu-id="9b213-154">In order to create a managed Kubernetes cluster with the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), ensure that you are using the Azure CLI version 2.0.25 or later.</span><span class="sxs-lookup"><span data-stu-id="9b213-154">In order to create a managed Kubernetes cluster with the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), ensure that you are using the Azure CLI version 2.0.25 or later.</span></span>

1. <span data-ttu-id="9b213-155">Sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="9b213-155">Sign in to your Azure account.</span></span> <span data-ttu-id="9b213-156">After you enter the following command, you  receive instructions that explain how to complete the sign-in.</span><span class="sxs-lookup"><span data-stu-id="9b213-156">After you enter the following command, you  receive instructions that explain how to complete the sign-in.</span></span> 
    
    ```bash
    az login
    ```

1. <span data-ttu-id="9b213-157">When you run the `az login` command in the previous step, a list of all your Azure subscriptions appears (along with their subscription IDs).</span><span class="sxs-lookup"><span data-stu-id="9b213-157">When you run the `az login` command in the previous step, a list of all your Azure subscriptions appears (along with their subscription IDs).</span></span> <span data-ttu-id="9b213-158">In this step, you set the default Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9b213-158">In this step, you set the default Azure subscription.</span></span> <span data-ttu-id="9b213-159">Replace the &lt;your-subscription-id> placeholder with the desired Azure subscription ID.</span><span class="sxs-lookup"><span data-stu-id="9b213-159">Replace the &lt;your-subscription-id> placeholder with the desired Azure subscription ID.</span></span> 

    ```bash
    az account set -s <your-subscription-id>
    ```

1. <span data-ttu-id="9b213-160">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="9b213-160">Create a resource group.</span></span> <span data-ttu-id="9b213-161">Replace the &lt;your-resource-group-name> placeholder with the name of your new resource group, and replace the &lt;your-location> placeholder with the location.</span><span class="sxs-lookup"><span data-stu-id="9b213-161">Replace the &lt;your-resource-group-name> placeholder with the name of your new resource group, and replace the &lt;your-location> placeholder with the location.</span></span> <span data-ttu-id="9b213-162">The command `az account list-locations` displays all Azure locations.</span><span class="sxs-lookup"><span data-stu-id="9b213-162">The command `az account list-locations` displays all Azure locations.</span></span> <span data-ttu-id="9b213-163">During the AKS preview, not all locations are available.</span><span class="sxs-lookup"><span data-stu-id="9b213-163">During the AKS preview, not all locations are available.</span></span> <span data-ttu-id="9b213-164">If you enter a location that is not valid at this time, the error message lists the available locations.</span><span class="sxs-lookup"><span data-stu-id="9b213-164">If you enter a location that is not valid at this time, the error message lists the available locations.</span></span>

    ```bash
    az group create -n <your-resource-group-name> -l <your-location>
    ```

1. <span data-ttu-id="9b213-165">Create the Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="9b213-165">Create the Kubernetes cluster.</span></span> <span data-ttu-id="9b213-166">Replace the &lt;your-resource-group-name> with the name of the resource group created in the previous step, and replace the &lt;your-kubernetes-cluster-name> with the name of your new cluster.</span><span class="sxs-lookup"><span data-stu-id="9b213-166">Replace the &lt;your-resource-group-name> with the name of the resource group created in the previous step, and replace the &lt;your-kubernetes-cluster-name> with the name of your new cluster.</span></span> <span data-ttu-id="9b213-167">(This process can take several minutes to complete.)</span><span class="sxs-lookup"><span data-stu-id="9b213-167">(This process can take several minutes to complete.)</span></span>

    ```bash
    az aks create -g <your-resource-group-name> -n <your-kubernetes-cluster-name> --generate-ssh-keys --node-count 2
    ```

### <a name="set-up-the-kubernetes-cluster"></a><span data-ttu-id="9b213-168">Set up the Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="9b213-168">Set up the Kubernetes cluster</span></span>

<span data-ttu-id="9b213-169">You can set up a blue/green deployment in AKS manually, or with a setup script provided in the sample cloned earlier.</span><span class="sxs-lookup"><span data-stu-id="9b213-169">You can set up a blue/green deployment in AKS manually, or with a setup script provided in the sample cloned earlier.</span></span> <span data-ttu-id="9b213-170">In this section, you see how to do both.</span><span class="sxs-lookup"><span data-stu-id="9b213-170">In this section, you see how to do both.</span></span>

#### <a name="set-up-the-kubernetes-cluster-via-the-sample-setup-script"></a><span data-ttu-id="9b213-171">Set up the Kubernetes cluster via the sample setup script</span><span class="sxs-lookup"><span data-stu-id="9b213-171">Set up the Kubernetes cluster via the sample setup script</span></span>
1. <span data-ttu-id="9b213-172">Edit the **deploy/aks/setup/setup.sh** file, replacing the following placeholders with the appropriate values for your environment:</span><span class="sxs-lookup"><span data-stu-id="9b213-172">Edit the **deploy/aks/setup/setup.sh** file, replacing the following placeholders with the appropriate values for your environment:</span></span> 

    - <span data-ttu-id="9b213-173">**&lt;your-resource-group-name>**</span><span class="sxs-lookup"><span data-stu-id="9b213-173">**&lt;your-resource-group-name>**</span></span>
    - <span data-ttu-id="9b213-174">**&lt;your-kubernetes-cluster-name>**</span><span class="sxs-lookup"><span data-stu-id="9b213-174">**&lt;your-kubernetes-cluster-name>**</span></span>
    - <span data-ttu-id="9b213-175">**&lt;your-location>**</span><span class="sxs-lookup"><span data-stu-id="9b213-175">**&lt;your-location>**</span></span>
    - <span data-ttu-id="9b213-176">**&lt;your-dns-name-suffix>**</span><span class="sxs-lookup"><span data-stu-id="9b213-176">**&lt;your-dns-name-suffix>**</span></span>

    ![Screenshot setup.sh script in bash, with several placeholders highlighted](./media/jenkins-aks-blue-green-deployment/edit-setup-script.png)

1. <span data-ttu-id="9b213-178">Run the setup script.</span><span class="sxs-lookup"><span data-stu-id="9b213-178">Run the setup script.</span></span>

    ```bash
    sh setup.sh
    ```

#### <a name="set-up-a-kubernetes-cluster-manually"></a><span data-ttu-id="9b213-179">Set up a Kubernetes cluster manually</span><span class="sxs-lookup"><span data-stu-id="9b213-179">Set up a Kubernetes cluster manually</span></span> 
1. <span data-ttu-id="9b213-180">Download the Kubernetes configuration to your profile folder.</span><span class="sxs-lookup"><span data-stu-id="9b213-180">Download the Kubernetes configuration to your profile folder.</span></span>

    ```bash
    az aks get-credentials -g <your-resource-group-name> -n <your-kubernetes-cluster-name> --admin
    ```

1. <span data-ttu-id="9b213-181">Change the directory to the **deploy/aks/setup** directory.</span><span class="sxs-lookup"><span data-stu-id="9b213-181">Change the directory to the **deploy/aks/setup** directory.</span></span> 

1. <span data-ttu-id="9b213-182">Run the following **kubectl** commands to set up the services for the public endpoint, and the two test endpoints.</span><span class="sxs-lookup"><span data-stu-id="9b213-182">Run the following **kubectl** commands to set up the services for the public endpoint, and the two test endpoints.</span></span>

    ```bash
    kubectl apply -f  service-green.yml
    kubectl apply -f  test-endpoint-blue.yml
    kubectl apply -f  test-endpoint-green.yml
    ```

1. <span data-ttu-id="9b213-183">Update the DNS name for the public and test endpoints.</span><span class="sxs-lookup"><span data-stu-id="9b213-183">Update the DNS name for the public and test endpoints.</span></span> <span data-ttu-id="9b213-184">When you create a Kubernetes cluster, you also create an [additional resource group](https://github.com/Azure/AKS/issues/3), with the naming pattern of **MC_&lt;your-resource-group-name>_&lt;your-kubernetes-cluster-name>_&lt;your-location>**.</span><span class="sxs-lookup"><span data-stu-id="9b213-184">When you create a Kubernetes cluster, you also create an [additional resource group](https://github.com/Azure/AKS/issues/3), with the naming pattern of **MC_&lt;your-resource-group-name>_&lt;your-kubernetes-cluster-name>_&lt;your-location>**.</span></span>

    <span data-ttu-id="9b213-185">Locate the public IPs in the resource group.</span><span class="sxs-lookup"><span data-stu-id="9b213-185">Locate the public IPs in the resource group.</span></span>

    ![Screenshot of the public IPs in the resource group](./media/jenkins-aks-blue-green-deployment/publicip.png)

    <span data-ttu-id="9b213-187">For each of the services, find the external IP address by running the following command:</span><span class="sxs-lookup"><span data-stu-id="9b213-187">For each of the services, find the external IP address by running the following command:</span></span>
    
    ```bash
    kubectl get service todoapp-service
    ```
    
    <span data-ttu-id="9b213-188">Update the DNS name for the corresponding IP address with the following command:</span><span class="sxs-lookup"><span data-stu-id="9b213-188">Update the DNS name for the corresponding IP address with the following command:</span></span>

    ```bash
    az network public-ip update --dns-name aks-todoapp --ids /subscriptions/<your-subscription-id>/resourceGroups/MC_<resourcegroup>_<aks>_<location>/providers/Microsoft.Network/publicIPAddresses/kubernetes-<ip-address>
    ```

    <span data-ttu-id="9b213-189">Repeat the call for `todoapp-test-blue` and `todoapp-test-green`:</span><span class="sxs-lookup"><span data-stu-id="9b213-189">Repeat the call for `todoapp-test-blue` and `todoapp-test-green`:</span></span>

    ```bash
    az network public-ip update --dns-name todoapp-blue --ids /subscriptions/<your-subscription-id>/resourceGroups/MC_<resourcegroup>_<aks>_<location>/providers/Microsoft.Network/publicIPAddresses/kubernetes-<ip-address>

    az network public-ip update --dns-name todoapp-green --ids /subscriptions/<your-subscription-id>/resourceGroups/MC_<resourcegroup>_<aks>_<location>/providers/Microsoft.Network/publicIPAddresses/kubernetes-<ip-address>
    ```

    <span data-ttu-id="9b213-190">The DNS name needs to be unique in your subscription.</span><span class="sxs-lookup"><span data-stu-id="9b213-190">The DNS name needs to be unique in your subscription.</span></span> <span data-ttu-id="9b213-191">To ensure the uniqueness, you can use `<your-dns-name-suffix>`.</span><span class="sxs-lookup"><span data-stu-id="9b213-191">To ensure the uniqueness, you can use `<your-dns-name-suffix>`.</span></span>

### <a name="create-an-instance-of-container-registry"></a><span data-ttu-id="9b213-192">Create an instance of Container Registry</span><span class="sxs-lookup"><span data-stu-id="9b213-192">Create an instance of Container Registry</span></span>

1. <span data-ttu-id="9b213-193">Run the `az acr create` command to create an instance of Container Registry.</span><span class="sxs-lookup"><span data-stu-id="9b213-193">Run the `az acr create` command to create an instance of Container Registry.</span></span> <span data-ttu-id="9b213-194">In the next section, you can then use `login server` as the Docker registry URL.</span><span class="sxs-lookup"><span data-stu-id="9b213-194">In the next section, you can then use `login server` as the Docker registry URL.</span></span>

    ```bash
    az acr create -n <your-registry-name> -g <your-resource-group-name>
    ```

1. <span data-ttu-id="9b213-195">Run the `az acr credential` command to show your Container Registry credentials.</span><span class="sxs-lookup"><span data-stu-id="9b213-195">Run the `az acr credential` command to show your Container Registry credentials.</span></span> <span data-ttu-id="9b213-196">Note the Docker registry username and password, as you need them in the next section.</span><span class="sxs-lookup"><span data-stu-id="9b213-196">Note the Docker registry username and password, as you need them in the next section.</span></span>

    ```bash
    az acr credential show -n <your-registry-name>
    ```

## <a name="prepare-the-jenkins-server"></a><span data-ttu-id="9b213-197">Prepare the Jenkins server</span><span class="sxs-lookup"><span data-stu-id="9b213-197">Prepare the Jenkins server</span></span>

<span data-ttu-id="9b213-198">In this section, you see how to prepare the Jenkins server to run a build, which is fine for testing.</span><span class="sxs-lookup"><span data-stu-id="9b213-198">In this section, you see how to prepare the Jenkins server to run a build, which is fine for testing.</span></span> <span data-ttu-id="9b213-199">However, you should use an [Azure VM agent](https://plugins.jenkins.io/azure-vm-agents) or [Azure Container agent](https://plugins.jenkins.io/azure-container-agents) to spin up an agent in Azure to run your builds.</span><span class="sxs-lookup"><span data-stu-id="9b213-199">However, you should use an [Azure VM agent](https://plugins.jenkins.io/azure-vm-agents) or [Azure Container agent](https://plugins.jenkins.io/azure-container-agents) to spin up an agent in Azure to run your builds.</span></span> <span data-ttu-id="9b213-200">For more information, see the Jenkins article on the [security implications of building on master](https://wiki.jenkins.io/display/JENKINS/Security+implication+of+building+on+master).</span><span class="sxs-lookup"><span data-stu-id="9b213-200">For more information, see the Jenkins article on the [security implications of building on master](https://wiki.jenkins.io/display/JENKINS/Security+implication+of+building+on+master).</span></span>

1. <span data-ttu-id="9b213-201">Deploy a [Jenkins Master on Azure](https://aka.ms/jenkins-on-azure).</span><span class="sxs-lookup"><span data-stu-id="9b213-201">Deploy a [Jenkins Master on Azure](https://aka.ms/jenkins-on-azure).</span></span>

1. <span data-ttu-id="9b213-202">Connect to the server via SSH, and install the build tools on the server where you run your build.</span><span class="sxs-lookup"><span data-stu-id="9b213-202">Connect to the server via SSH, and install the build tools on the server where you run your build.</span></span>
   
   ```bash
   sudo apt-get install git maven 
   ```
   
1. <span data-ttu-id="9b213-203">[Install Docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce).</span><span class="sxs-lookup"><span data-stu-id="9b213-203">[Install Docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce).</span></span> <span data-ttu-id="9b213-204">Ensure that the user `jenkins` has permission to run the `docker` commands.</span><span class="sxs-lookup"><span data-stu-id="9b213-204">Ensure that the user `jenkins` has permission to run the `docker` commands.</span></span>

1. <span data-ttu-id="9b213-205">[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).</span><span class="sxs-lookup"><span data-stu-id="9b213-205">[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).</span></span>

1. <span data-ttu-id="9b213-206">[Download jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="9b213-206">[Download jq](https://stedolan.github.io/jq/download/).</span></span>

1. <span data-ttu-id="9b213-207">Install jq with the following command:</span><span class="sxs-lookup"><span data-stu-id="9b213-207">Install jq with the following command:</span></span>

   ```bash
   sudo apt-get install jq
   ```
   
1. <span data-ttu-id="9b213-208">Install the plugins in Jenkins by performing the following steps within the Jenkins dashboard:</span><span class="sxs-lookup"><span data-stu-id="9b213-208">Install the plugins in Jenkins by performing the following steps within the Jenkins dashboard:</span></span>

    1. <span data-ttu-id="9b213-209">Select **Manage Jenkins > Manage Plugins > Available**.</span><span class="sxs-lookup"><span data-stu-id="9b213-209">Select **Manage Jenkins > Manage Plugins > Available**.</span></span>
    1. <span data-ttu-id="9b213-210">Search for and install the Azure Container Service plug-in.</span><span class="sxs-lookup"><span data-stu-id="9b213-210">Search for and install the Azure Container Service plug-in.</span></span>

1. <span data-ttu-id="9b213-211">Add credentials to manage resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="9b213-211">Add credentials to manage resources in Azure.</span></span> <span data-ttu-id="9b213-212">If you don’t already have the plug-in, install the **Azure Credential** plugin.</span><span class="sxs-lookup"><span data-stu-id="9b213-212">If you don’t already have the plug-in, install the **Azure Credential** plugin.</span></span>

1. <span data-ttu-id="9b213-213">Add your Azure Service Principal credential as the type **Microsoft Azure Service Principal**.</span><span class="sxs-lookup"><span data-stu-id="9b213-213">Add your Azure Service Principal credential as the type **Microsoft Azure Service Principal**.</span></span>

1. <span data-ttu-id="9b213-214">Add your Azure Docker registry username and password (as obtained in the section, "Create an instance of Container Registry") as the type **Username with password**.</span><span class="sxs-lookup"><span data-stu-id="9b213-214">Add your Azure Docker registry username and password (as obtained in the section, "Create an instance of Container Registry") as the type **Username with password**.</span></span>

## <a name="edit-the-jenkinsfile"></a><span data-ttu-id="9b213-215">Edit the Jenkinsfile</span><span class="sxs-lookup"><span data-stu-id="9b213-215">Edit the Jenkinsfile</span></span>

1. <span data-ttu-id="9b213-216">In your own repo, go to `/deploy/aks/`, and open `Jenkinsfile`.</span><span class="sxs-lookup"><span data-stu-id="9b213-216">In your own repo, go to `/deploy/aks/`, and open `Jenkinsfile`.</span></span>

2. <span data-ttu-id="9b213-217">Update the file as follows:</span><span class="sxs-lookup"><span data-stu-id="9b213-217">Update the file as follows:</span></span>

    ```groovy
    def servicePrincipalId = '<your-service-principal>'
    def resourceGroup = '<your-resource-group-name>'
    def aks = '<your-kubernetes-cluster-name>'

    def cosmosResourceGroup = '<your-cosmodb-resource-group>'
    def cosmosDbName = '<your-cosmodb-name>'
    def dbName = '<your-dbname>'

    def dockerRegistry = '<your-acr-name>.azurecr.io'
    ```
    
    <span data-ttu-id="9b213-218">Update the Container Registry credential ID:</span><span class="sxs-lookup"><span data-stu-id="9b213-218">Update the Container Registry credential ID:</span></span>
    
    ```groovy
    def dockerCredentialId = '<your-acr-credential-id>'
    ```

## <a name="create-the-job"></a><span data-ttu-id="9b213-219">Create the job</span><span class="sxs-lookup"><span data-stu-id="9b213-219">Create the job</span></span>
1. <span data-ttu-id="9b213-220">Add a new job in type **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="9b213-220">Add a new job in type **Pipeline**.</span></span>

1. <span data-ttu-id="9b213-221">Select **Pipeline** > **Definition** > **Pipeline script from SCM**.</span><span class="sxs-lookup"><span data-stu-id="9b213-221">Select **Pipeline** > **Definition** > **Pipeline script from SCM**.</span></span>

1. <span data-ttu-id="9b213-222">Enter the SCM repo URL with your &lt;your-forked-repo>.</span><span class="sxs-lookup"><span data-stu-id="9b213-222">Enter the SCM repo URL with your &lt;your-forked-repo>.</span></span>

1. <span data-ttu-id="9b213-223">Enter the script path as `deploy/aks/Jenkinsfile`.</span><span class="sxs-lookup"><span data-stu-id="9b213-223">Enter the script path as `deploy/aks/Jenkinsfile`.</span></span>

## <a name="run-the-job"></a><span data-ttu-id="9b213-224">Run the job</span><span class="sxs-lookup"><span data-stu-id="9b213-224">Run the job</span></span>

1. <span data-ttu-id="9b213-225">Verify that you can run your project successfully in your local environment.</span><span class="sxs-lookup"><span data-stu-id="9b213-225">Verify that you can run your project successfully in your local environment.</span></span> <span data-ttu-id="9b213-226">Here's how: [Run project on local machine](https://github.com/Microsoft/todo-app-java-on-azure/blob/master/README.md#run-it).</span><span class="sxs-lookup"><span data-stu-id="9b213-226">Here's how: [Run project on local machine](https://github.com/Microsoft/todo-app-java-on-azure/blob/master/README.md#run-it).</span></span>

1. <span data-ttu-id="9b213-227">Run the Jenkins job.</span><span class="sxs-lookup"><span data-stu-id="9b213-227">Run the Jenkins job.</span></span> <span data-ttu-id="9b213-228">The first time you run the job, Jenkins deploys the todo app to the blue environment, which is the default inactive environment.</span><span class="sxs-lookup"><span data-stu-id="9b213-228">The first time you run the job, Jenkins deploys the todo app to the blue environment, which is the default inactive environment.</span></span> 

1. <span data-ttu-id="9b213-229">To verify that the job ran, go to these URLs:</span><span class="sxs-lookup"><span data-stu-id="9b213-229">To verify that the job ran, go to these URLs:</span></span>
    - <span data-ttu-id="9b213-230">Public end point: `http://aks-todoapp<your-dns-name-suffix>.<your-location>.cloudapp.azure.com`</span><span class="sxs-lookup"><span data-stu-id="9b213-230">Public end point: `http://aks-todoapp<your-dns-name-suffix>.<your-location>.cloudapp.azure.com`</span></span>
    - <span data-ttu-id="9b213-231">Blue end point - `http://aks-todoapp-blue<your-dns-name-suffix>.<your-location>.cloudapp.azure.com`</span><span class="sxs-lookup"><span data-stu-id="9b213-231">Blue end point - `http://aks-todoapp-blue<your-dns-name-suffix>.<your-location>.cloudapp.azure.com`</span></span>
    - <span data-ttu-id="9b213-232">Green end point - `http://aks-todoapp-green<your-dns-name-suffix>.<your-location>.cloudapp.azure.com`</span><span class="sxs-lookup"><span data-stu-id="9b213-232">Green end point - `http://aks-todoapp-green<your-dns-name-suffix>.<your-location>.cloudapp.azure.com`</span></span>

<span data-ttu-id="9b213-233">The public and the blue test end points have the same update, while the green end point shows the default tomcat image.</span><span class="sxs-lookup"><span data-stu-id="9b213-233">The public and the blue test end points have the same update, while the green end point shows the default tomcat image.</span></span> 

<span data-ttu-id="9b213-234">If you run the build more than once, it cycles through blue and green deployments.</span><span class="sxs-lookup"><span data-stu-id="9b213-234">If you run the build more than once, it cycles through blue and green deployments.</span></span> <span data-ttu-id="9b213-235">In other words, if the current environment is blue, the job deploys and tests to the green environment.</span><span class="sxs-lookup"><span data-stu-id="9b213-235">In other words, if the current environment is blue, the job deploys and tests to the green environment.</span></span> <span data-ttu-id="9b213-236">Then, if tests are good, the job updates the application public endpoint to route traffic to the green environment.</span><span class="sxs-lookup"><span data-stu-id="9b213-236">Then, if tests are good, the job updates the application public endpoint to route traffic to the green environment.</span></span>

## <a name="additional-information"></a><span data-ttu-id="9b213-237">Additional information</span><span class="sxs-lookup"><span data-stu-id="9b213-237">Additional information</span></span>

<span data-ttu-id="9b213-238">For more on zero-downtime deployment, see this [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/301-jenkins-aks-zero-downtime-deployment).</span><span class="sxs-lookup"><span data-stu-id="9b213-238">For more on zero-downtime deployment, see this [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/301-jenkins-aks-zero-downtime-deployment).</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="9b213-239">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="9b213-239">Clean up resources</span></span>

<span data-ttu-id="9b213-240">When you no longer need the resources you created in this tutorial, you can delete them.</span><span class="sxs-lookup"><span data-stu-id="9b213-240">When you no longer need the resources you created in this tutorial, you can delete them.</span></span>

```bash
az group delete -y --no-wait -n <your-resource-group-name>
```

## <a name="troubleshooting"></a><span data-ttu-id="9b213-241">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="9b213-241">Troubleshooting</span></span>

<span data-ttu-id="9b213-242">If you encounter any bugs with the Jenkins plugins, file an issue in the [Jenkins JIRA](https://issues.jenkins-ci.org/) for the specific component.</span><span class="sxs-lookup"><span data-stu-id="9b213-242">If you encounter any bugs with the Jenkins plugins, file an issue in the [Jenkins JIRA](https://issues.jenkins-ci.org/) for the specific component.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b213-243">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b213-243">Next steps</span></span>

<span data-ttu-id="9b213-244">In this tutorial, you learned how to deploy to AKS by using Jenkins and the blue/green deployment pattern.</span><span class="sxs-lookup"><span data-stu-id="9b213-244">In this tutorial, you learned how to deploy to AKS by using Jenkins and the blue/green deployment pattern.</span></span> <span data-ttu-id="9b213-245">To learn more about the Azure Jenkins provider, see the Jenkins on Azure site.</span><span class="sxs-lookup"><span data-stu-id="9b213-245">To learn more about the Azure Jenkins provider, see the Jenkins on Azure site.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9b213-246">Jenkins on Azure</span><span class="sxs-lookup"><span data-stu-id="9b213-246">Jenkins on Azure</span></span>](/azure/jenkins/)