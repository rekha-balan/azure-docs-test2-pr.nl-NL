---
title: Continuous build and integration for your Azure Service Fabric Linux Java application by using Jenkins | Microsoft Docs
description: Continuous build and integration for your Linux Java application by using Jenkins
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: ''
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: saysa
ms.openlocfilehash: 3ed5cb77e4cccf254f6832f83f3b8ea94c924a0a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663034"
---
# <a name="use-jenkins-to-build-and-deploy-your-linux-java-application"></a><span data-ttu-id="42d1d-103">Use Jenkins to build and deploy your Linux Java application</span><span class="sxs-lookup"><span data-stu-id="42d1d-103">Use Jenkins to build and deploy your Linux Java application</span></span>
<span data-ttu-id="42d1d-104">Jenkins is a popular tool for continuous integration and deployment of your apps.</span><span class="sxs-lookup"><span data-stu-id="42d1d-104">Jenkins is a popular tool for continuous integration and deployment of your apps.</span></span> <span data-ttu-id="42d1d-105">Here's how to build and deploy your Azure Service Fabric application by using Jenkins.</span><span class="sxs-lookup"><span data-stu-id="42d1d-105">Here's how to build and deploy your Azure Service Fabric application by using Jenkins.</span></span>

## <a name="general-prerequisites"></a><span data-ttu-id="42d1d-106">General prerequisites</span><span class="sxs-lookup"><span data-stu-id="42d1d-106">General prerequisites</span></span>
- <span data-ttu-id="42d1d-107">Have Git installed locally.</span><span class="sxs-lookup"><span data-stu-id="42d1d-107">Have Git installed locally.</span></span> <span data-ttu-id="42d1d-108">You can install the appropriate Git version from [the Git downloads page](https://git-scm.com/downloads), based on your operating system.</span><span class="sxs-lookup"><span data-stu-id="42d1d-108">You can install the appropriate Git version from [the Git downloads page](https://git-scm.com/downloads), based on your operating system.</span></span> <span data-ttu-id="42d1d-109">If you are new to Git, learn more about it from the [Git documentation](https://git-scm.com/docs).</span><span class="sxs-lookup"><span data-stu-id="42d1d-109">If you are new to Git, learn more about it from the [Git documentation](https://git-scm.com/docs).</span></span>
- <span data-ttu-id="42d1d-110">Have the Service Fabric Jenkins plug-in handy.</span><span class="sxs-lookup"><span data-stu-id="42d1d-110">Have the Service Fabric Jenkins plug-in handy.</span></span> <span data-ttu-id="42d1d-111">You can download it from [Service Fabric downloads](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).</span><span class="sxs-lookup"><span data-stu-id="42d1d-111">You can download it from [Service Fabric downloads](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).</span></span>

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a><span data-ttu-id="42d1d-112">Set up Jenkins inside a Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="42d1d-112">Set up Jenkins inside a Service Fabric cluster</span></span>

<span data-ttu-id="42d1d-113">You can set up Jenkins either inside or outside a Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="42d1d-113">You can set up Jenkins either inside or outside a Service Fabric cluster.</span></span> <span data-ttu-id="42d1d-114">The following sections show how to set it up inside a cluster.</span><span class="sxs-lookup"><span data-stu-id="42d1d-114">The following sections show how to set it up inside a cluster.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="42d1d-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42d1d-115">Prerequisites</span></span>
1. <span data-ttu-id="42d1d-116">Have a Service Fabric Linux cluster ready.</span><span class="sxs-lookup"><span data-stu-id="42d1d-116">Have a Service Fabric Linux cluster ready.</span></span> <span data-ttu-id="42d1d-117">A Service Fabric cluster created from the Azure portal already has Docker installed.</span><span class="sxs-lookup"><span data-stu-id="42d1d-117">A Service Fabric cluster created from the Azure portal already has Docker installed.</span></span> <span data-ttu-id="42d1d-118">If you are running the cluster locally, check if Docker is installed by using the command ``docker info``.</span><span class="sxs-lookup"><span data-stu-id="42d1d-118">If you are running the cluster locally, check if Docker is installed by using the command ``docker info``.</span></span> <span data-ttu-id="42d1d-119">If it is not installed, install it accordingly by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="42d1d-119">If it is not installed, install it accordingly by using the following commands:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. <span data-ttu-id="42d1d-120">Have the Service Fabric container application deployed on the cluster, by using the following steps:</span><span class="sxs-lookup"><span data-stu-id="42d1d-120">Have the Service Fabric container application deployed on the cluster, by using the following steps:</span></span>

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git -b JenkinsDocker
cd service-fabric-java-getting-started/Services/JenkinsDocker/
azure servicefabric cluster connect http://PublicIPorFQDN:19080   # Azure CLI cluster connect command
bash Scripts/install.sh
```
<span data-ttu-id="42d1d-121">This installs a Jenkins container on the cluster, and can be monitored by using the Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="42d1d-121">This installs a Jenkins container on the cluster, and can be monitored by using the Service Fabric Explorer.</span></span>

### <a name="steps"></a><span data-ttu-id="42d1d-122">Steps</span><span class="sxs-lookup"><span data-stu-id="42d1d-122">Steps</span></span>
1. <span data-ttu-id="42d1d-123">From your browser, go to ``http://PublicIPorFQDN:8081``.</span><span class="sxs-lookup"><span data-stu-id="42d1d-123">From your browser, go to ``http://PublicIPorFQDN:8081``.</span></span> <span data-ttu-id="42d1d-124">It provides the path of the initial admin password required to sign in.</span><span class="sxs-lookup"><span data-stu-id="42d1d-124">It provides the path of the initial admin password required to sign in.</span></span> <span data-ttu-id="42d1d-125">You can continue to use Jenkins as an admin user.</span><span class="sxs-lookup"><span data-stu-id="42d1d-125">You can continue to use Jenkins as an admin user.</span></span> <span data-ttu-id="42d1d-126">Or you can create and change the user, after you sign in with the initial admin account.</span><span class="sxs-lookup"><span data-stu-id="42d1d-126">Or you can create and change the user, after you sign in with the initial admin account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="42d1d-127">Ensure that the 8081 port is specified as the application endpoint port while you are creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="42d1d-127">Ensure that the 8081 port is specified as the application endpoint port while you are creating the cluster.</span></span>
   >

2. <span data-ttu-id="42d1d-128">Get the container instance ID by using ``docker ps -a``.</span><span class="sxs-lookup"><span data-stu-id="42d1d-128">Get the container instance ID by using ``docker ps -a``.</span></span>
3. <span data-ttu-id="42d1d-129">Secure Shell (SSH) sign in to the container, and paste the path you were shown on the Jenkins portal.</span><span class="sxs-lookup"><span data-stu-id="42d1d-129">Secure Shell (SSH) sign in to the container, and paste the path you were shown on the Jenkins portal.</span></span> <span data-ttu-id="42d1d-130">For example, if in the portal it shows the path `PATH_TO_INITIAL_ADMIN_PASSWORD`, run the following:</span><span class="sxs-lookup"><span data-stu-id="42d1d-130">For example, if in the portal it shows the path `PATH_TO_INITIAL_ADMIN_PASSWORD`, run the following:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. <span data-ttu-id="42d1d-131">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span><span class="sxs-lookup"><span data-stu-id="42d1d-131">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
    * <span data-ttu-id="42d1d-132">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting your repository.</span><span class="sxs-lookup"><span data-stu-id="42d1d-132">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting your repository.</span></span>
    * <span data-ttu-id="42d1d-133">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span><span class="sxs-lookup"><span data-stu-id="42d1d-133">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span></span>
    * <span data-ttu-id="42d1d-134">To sign in to the Jenkins shell from your host, use the following command:</span><span class="sxs-lookup"><span data-stu-id="42d1d-134">To sign in to the Jenkins shell from your host, use the following command:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a><span data-ttu-id="42d1d-135">Set up Jenkins outside a Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="42d1d-135">Set up Jenkins outside a Service Fabric cluster</span></span>

<span data-ttu-id="42d1d-136">You can set up Jenkins either inside or outside of a Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="42d1d-136">You can set up Jenkins either inside or outside of a Service Fabric cluster.</span></span> <span data-ttu-id="42d1d-137">The following sections show how to set it up outside a cluster.</span><span class="sxs-lookup"><span data-stu-id="42d1d-137">The following sections show how to set it up outside a cluster.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="42d1d-138">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42d1d-138">Prerequisites</span></span>
<span data-ttu-id="42d1d-139">You need to have Docker installed.</span><span class="sxs-lookup"><span data-stu-id="42d1d-139">You need to have Docker installed.</span></span> <span data-ttu-id="42d1d-140">The following commands can be used to install Docker from the terminal:</span><span class="sxs-lookup"><span data-stu-id="42d1d-140">The following commands can be used to install Docker from the terminal:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

<span data-ttu-id="42d1d-141">Now when you run ``docker info`` in the terminal, you should see in the output that the Docker service is running.</span><span class="sxs-lookup"><span data-stu-id="42d1d-141">Now when you run ``docker info`` in the terminal, you should see in the output that the Docker service is running.</span></span>

### <a name="steps"></a><span data-ttu-id="42d1d-142">Steps</span><span class="sxs-lookup"><span data-stu-id="42d1d-142">Steps</span></span>
  1. <span data-ttu-id="42d1d-143">Pull the Service Fabric Jenkins container image: ``docker pull raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="42d1d-143">Pull the Service Fabric Jenkins container image: ``docker pull raunakpandya/jenkins:v1``</span></span>
  2. <span data-ttu-id="42d1d-144">Run the container image: ``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="42d1d-144">Run the container image: ``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span></span>
  3. <span data-ttu-id="42d1d-145">Get the ID of the container image instance.</span><span class="sxs-lookup"><span data-stu-id="42d1d-145">Get the ID of the container image instance.</span></span> <span data-ttu-id="42d1d-146">You can list all the Docker containers with the command ``docker ps –a``</span><span class="sxs-lookup"><span data-stu-id="42d1d-146">You can list all the Docker containers with the command ``docker ps –a``</span></span>
  4. <span data-ttu-id="42d1d-147">Sign in to the Jenkins portal by using the following steps:</span><span class="sxs-lookup"><span data-stu-id="42d1d-147">Sign in to the Jenkins portal by using the following steps:</span></span>

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    <span data-ttu-id="42d1d-148">If container ID is 2d24a73b5964, use 2d24.</span><span class="sxs-lookup"><span data-stu-id="42d1d-148">If container ID is 2d24a73b5964, use 2d24.</span></span>
    * <span data-ttu-id="42d1d-149">This password is required for signing in to the Jenkins dashboard from portal, which is ``http://<HOST-IP>:8080``</span><span class="sxs-lookup"><span data-stu-id="42d1d-149">This password is required for signing in to the Jenkins dashboard from portal, which is ``http://<HOST-IP>:8080``</span></span>
    * <span data-ttu-id="42d1d-150">After you sign in for the first time, you can create your own user account and use that for future purposes, or you can continue to use the administrator account.</span><span class="sxs-lookup"><span data-stu-id="42d1d-150">After you sign in for the first time, you can create your own user account and use that for future purposes, or you can continue to use the administrator account.</span></span> <span data-ttu-id="42d1d-151">After you create a user, you need to continue with that.</span><span class="sxs-lookup"><span data-stu-id="42d1d-151">After you create a user, you need to continue with that.</span></span>
  5. <span data-ttu-id="42d1d-152">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span><span class="sxs-lookup"><span data-stu-id="42d1d-152">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
        * <span data-ttu-id="42d1d-153">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting the repository.</span><span class="sxs-lookup"><span data-stu-id="42d1d-153">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting the repository.</span></span>
        * <span data-ttu-id="42d1d-154">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span><span class="sxs-lookup"><span data-stu-id="42d1d-154">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span></span>
      * <span data-ttu-id="42d1d-155">To sign in to the Jenkins shell from your host, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="42d1d-155">To sign in to the Jenkins shell from your host, use the following commands:</span></span>

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

<span data-ttu-id="42d1d-156">Ensure that the cluster or machine where the Jenkins container image is hosted has a public-facing IP.</span><span class="sxs-lookup"><span data-stu-id="42d1d-156">Ensure that the cluster or machine where the Jenkins container image is hosted has a public-facing IP.</span></span> <span data-ttu-id="42d1d-157">This enables the Jenkins instance to receive notifications from GitHub.</span><span class="sxs-lookup"><span data-stu-id="42d1d-157">This enables the Jenkins instance to receive notifications from GitHub.</span></span>

## <a name="install-the-service-fabric-jenkins-plug-in-from-the-portal"></a><span data-ttu-id="42d1d-158">Install the Service Fabric Jenkins plug-in from the portal</span><span class="sxs-lookup"><span data-stu-id="42d1d-158">Install the Service Fabric Jenkins plug-in from the portal</span></span>

1. <span data-ttu-id="42d1d-159">Go to ``http://PublicIPorFQDN:8081``</span><span class="sxs-lookup"><span data-stu-id="42d1d-159">Go to ``http://PublicIPorFQDN:8081``</span></span>
2. <span data-ttu-id="42d1d-160">From the Jenkins dashboard, select **Manage Jenkins** > **Manage Plugins** > **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="42d1d-160">From the Jenkins dashboard, select **Manage Jenkins** > **Manage Plugins** > **Advanced**.</span></span>
<span data-ttu-id="42d1d-161">Here, you can upload a plug-in.</span><span class="sxs-lookup"><span data-stu-id="42d1d-161">Here, you can upload a plug-in.</span></span> <span data-ttu-id="42d1d-162">Select **Choose file**, and then select the **serviceFabric.hpi** file, which you downloaded under prerequisites.</span><span class="sxs-lookup"><span data-stu-id="42d1d-162">Select **Choose file**, and then select the **serviceFabric.hpi** file, which you downloaded under prerequisites.</span></span> <span data-ttu-id="42d1d-163">When you select **Upload**, Jenkins automatically installs the plug-in.</span><span class="sxs-lookup"><span data-stu-id="42d1d-163">When you select **Upload**, Jenkins automatically installs the plug-in.</span></span> <span data-ttu-id="42d1d-164">Allow a restart if requested.</span><span class="sxs-lookup"><span data-stu-id="42d1d-164">Allow a restart if requested.</span></span>

## <a name="create-and-configure-a-jenkins-job"></a><span data-ttu-id="42d1d-165">Create and configure a Jenkins job</span><span class="sxs-lookup"><span data-stu-id="42d1d-165">Create and configure a Jenkins job</span></span>

1. <span data-ttu-id="42d1d-166">Create a **new item** from dashboard.</span><span class="sxs-lookup"><span data-stu-id="42d1d-166">Create a **new item** from dashboard.</span></span>
2. <span data-ttu-id="42d1d-167">Enter an item name (for example, **MyJob**).</span><span class="sxs-lookup"><span data-stu-id="42d1d-167">Enter an item name (for example, **MyJob**).</span></span> <span data-ttu-id="42d1d-168">Select **free-style project**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="42d1d-168">Select **free-style project**, and click **OK**.</span></span>
3. <span data-ttu-id="42d1d-169">Go the job page, and click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="42d1d-169">Go the job page, and click **Configure**.</span></span>

   <span data-ttu-id="42d1d-170">a.</span><span class="sxs-lookup"><span data-stu-id="42d1d-170">a.</span></span> <span data-ttu-id="42d1d-171">In the general section, under **GitHub project**, specify your GitHub project URL.</span><span class="sxs-lookup"><span data-stu-id="42d1d-171">In the general section, under **GitHub project**, specify your GitHub project URL.</span></span> <span data-ttu-id="42d1d-172">This URL hosts the Service Fabric Java application that you want to integrate with the Jenkins continuous integration, continuous deployment (CI/CD) flow (for example, ``https://github.com/sayantancs/SFJenkins``).</span><span class="sxs-lookup"><span data-stu-id="42d1d-172">This URL hosts the Service Fabric Java application that you want to integrate with the Jenkins continuous integration, continuous deployment (CI/CD) flow (for example, ``https://github.com/sayantancs/SFJenkins``).</span></span>

   <span data-ttu-id="42d1d-173">b.</span><span class="sxs-lookup"><span data-stu-id="42d1d-173">b.</span></span> <span data-ttu-id="42d1d-174">Under the **Source Code Management** section, select **Git**.</span><span class="sxs-lookup"><span data-stu-id="42d1d-174">Under the **Source Code Management** section, select **Git**.</span></span> <span data-ttu-id="42d1d-175">Specify the repository URL that hosts the Service Fabric Java application that you want to integrate with the Jenkins CI/CD flow (for example, ``https://github.com/sayantancs/SFJenkins.git``).</span><span class="sxs-lookup"><span data-stu-id="42d1d-175">Specify the repository URL that hosts the Service Fabric Java application that you want to integrate with the Jenkins CI/CD flow (for example, ``https://github.com/sayantancs/SFJenkins.git``).</span></span> <span data-ttu-id="42d1d-176">Also, you can specify here which branch to build (for example, **/master**).</span><span class="sxs-lookup"><span data-stu-id="42d1d-176">Also, you can specify here which branch to build (for example, **/master**).</span></span>
4. <span data-ttu-id="42d1d-177">Configure your *GitHub* (which is hosting the repository) so that it is able to talk to Jenkins.</span><span class="sxs-lookup"><span data-stu-id="42d1d-177">Configure your *GitHub* (which is hosting the repository) so that it is able to talk to Jenkins.</span></span> <span data-ttu-id="42d1d-178">Use the following steps:</span><span class="sxs-lookup"><span data-stu-id="42d1d-178">Use the following steps:</span></span>

   <span data-ttu-id="42d1d-179">a.</span><span class="sxs-lookup"><span data-stu-id="42d1d-179">a.</span></span> <span data-ttu-id="42d1d-180">Go to your GitHub repository page.</span><span class="sxs-lookup"><span data-stu-id="42d1d-180">Go to your GitHub repository page.</span></span> <span data-ttu-id="42d1d-181">Go to **Settings** > **Integrations and Services**.</span><span class="sxs-lookup"><span data-stu-id="42d1d-181">Go to **Settings** > **Integrations and Services**.</span></span>

   <span data-ttu-id="42d1d-182">b.</span><span class="sxs-lookup"><span data-stu-id="42d1d-182">b.</span></span> <span data-ttu-id="42d1d-183">Select **Add Service**, type **Jenkins**, and select the **Jenkins-GitHub plugin**.</span><span class="sxs-lookup"><span data-stu-id="42d1d-183">Select **Add Service**, type **Jenkins**, and select the **Jenkins-GitHub plugin**.</span></span>

   <span data-ttu-id="42d1d-184">c.</span><span class="sxs-lookup"><span data-stu-id="42d1d-184">c.</span></span> <span data-ttu-id="42d1d-185">Enter your Jenkins webhook URL (by default, it should be ``http://<PublicIPorFQDN>:8081/github-webhook/``).</span><span class="sxs-lookup"><span data-stu-id="42d1d-185">Enter your Jenkins webhook URL (by default, it should be ``http://<PublicIPorFQDN>:8081/github-webhook/``).</span></span> <span data-ttu-id="42d1d-186">Click **add/update service**.</span><span class="sxs-lookup"><span data-stu-id="42d1d-186">Click **add/update service**.</span></span>

   <span data-ttu-id="42d1d-187">d.</span><span class="sxs-lookup"><span data-stu-id="42d1d-187">d.</span></span> <span data-ttu-id="42d1d-188">A test event is sent to your Jenkins instance.</span><span class="sxs-lookup"><span data-stu-id="42d1d-188">A test event is sent to your Jenkins instance.</span></span> <span data-ttu-id="42d1d-189">You should see a green check by the webhook in GitHub, and your project will build.</span><span class="sxs-lookup"><span data-stu-id="42d1d-189">You should see a green check by the webhook in GitHub, and your project will build.</span></span>

   <span data-ttu-id="42d1d-190">e.</span><span class="sxs-lookup"><span data-stu-id="42d1d-190">e.</span></span> <span data-ttu-id="42d1d-191">Under the **Build Triggers** section, select which build option you want.</span><span class="sxs-lookup"><span data-stu-id="42d1d-191">Under the **Build Triggers** section, select which build option you want.</span></span> <span data-ttu-id="42d1d-192">For this example, you want to trigger a build whenever some push to the repository happens.</span><span class="sxs-lookup"><span data-stu-id="42d1d-192">For this example, you want to trigger a build whenever some push to the repository happens.</span></span> <span data-ttu-id="42d1d-193">So you select **GitHub hook trigger for GITScm polling**.</span><span class="sxs-lookup"><span data-stu-id="42d1d-193">So you select **GitHub hook trigger for GITScm polling**.</span></span> <span data-ttu-id="42d1d-194">(Previously, this option was called **Build when a change is pushed to GitHub**.)</span><span class="sxs-lookup"><span data-stu-id="42d1d-194">(Previously, this option was called **Build when a change is pushed to GitHub**.)</span></span>

   <span data-ttu-id="42d1d-195">f.</span><span class="sxs-lookup"><span data-stu-id="42d1d-195">f.</span></span> <span data-ttu-id="42d1d-196">Under the **Build section**, from the drop-down **Add build step**, select the option **Invoke Gradle Script**.</span><span class="sxs-lookup"><span data-stu-id="42d1d-196">Under the **Build section**, from the drop-down **Add build step**, select the option **Invoke Gradle Script**.</span></span> <span data-ttu-id="42d1d-197">In the widget that comes, specify the path to **Root build script** for your application.</span><span class="sxs-lookup"><span data-stu-id="42d1d-197">In the widget that comes, specify the path to **Root build script** for your application.</span></span> <span data-ttu-id="42d1d-198">It picks up build.gradle from the path specified, and works accordingly.</span><span class="sxs-lookup"><span data-stu-id="42d1d-198">It picks up build.gradle from the path specified, and works accordingly.</span></span> <span data-ttu-id="42d1d-199">If you create a project named ``MyActor`` (using the Eclipse plug-in or Yeoman generator), the root build script should contain ``${WORKSPACE}/MyActor``.</span><span class="sxs-lookup"><span data-stu-id="42d1d-199">If you create a project named ``MyActor`` (using the Eclipse plug-in or Yeoman generator), the root build script should contain ``${WORKSPACE}/MyActor``.</span></span> <span data-ttu-id="42d1d-200">See the following screenshot for an example of what this looks like:</span><span class="sxs-lookup"><span data-stu-id="42d1d-200">See the following screenshot for an example of what this looks like:</span></span>

    ![Service Fabric Jenkins Build action][build-step]

   <span data-ttu-id="42d1d-202">g.</span><span class="sxs-lookup"><span data-stu-id="42d1d-202">g.</span></span> <span data-ttu-id="42d1d-203">From the **Post-Build Actions** drop-down, select **Deploy Service Fabric Project**.</span><span class="sxs-lookup"><span data-stu-id="42d1d-203">From the **Post-Build Actions** drop-down, select **Deploy Service Fabric Project**.</span></span> <span data-ttu-id="42d1d-204">Here you need to provide cluster details where the Jenkins compiled Service Fabric application would be deployed.</span><span class="sxs-lookup"><span data-stu-id="42d1d-204">Here you need to provide cluster details where the Jenkins compiled Service Fabric application would be deployed.</span></span> <span data-ttu-id="42d1d-205">You can also provide additional application details used to deploy the application.</span><span class="sxs-lookup"><span data-stu-id="42d1d-205">You can also provide additional application details used to deploy the application.</span></span> <span data-ttu-id="42d1d-206">See the following screenshot for an example of what this looks like:</span><span class="sxs-lookup"><span data-stu-id="42d1d-206">See the following screenshot for an example of what this looks like:</span></span>

    ![Service Fabric Jenkins Build action][post-build-step]

   > [!NOTE]
   > <span data-ttu-id="42d1d-208">The cluster here could be same as the one hosting the Jenkins container application, in case you are using Service Fabric to deploy the Jenkins container image.</span><span class="sxs-lookup"><span data-stu-id="42d1d-208">The cluster here could be same as the one hosting the Jenkins container application, in case you are using Service Fabric to deploy the Jenkins container image.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="42d1d-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="42d1d-209">Next steps</span></span>
<span data-ttu-id="42d1d-210">GitHub and Jenkins are now configured.</span><span class="sxs-lookup"><span data-stu-id="42d1d-210">GitHub and Jenkins are now configured.</span></span> <span data-ttu-id="42d1d-211">Consider making some sample change in your ``MyActor`` project in the repository example, https://github.com/sayantancs/SFJenkins.</span><span class="sxs-lookup"><span data-stu-id="42d1d-211">Consider making some sample change in your ``MyActor`` project in the repository example, https://github.com/sayantancs/SFJenkins.</span></span> <span data-ttu-id="42d1d-212">Push your changes to a remote ``master`` branch (or any branch that you have configured to work with).</span><span class="sxs-lookup"><span data-stu-id="42d1d-212">Push your changes to a remote ``master`` branch (or any branch that you have configured to work with).</span></span> <span data-ttu-id="42d1d-213">This triggers the Jenkins job, ``MyJob``, that you configured.</span><span class="sxs-lookup"><span data-stu-id="42d1d-213">This triggers the Jenkins job, ``MyJob``, that you configured.</span></span> <span data-ttu-id="42d1d-214">It fetches the changes from GitHub, builds them, and deploys the application to the cluster endpoint you specified in post-build actions.</span><span class="sxs-lookup"><span data-stu-id="42d1d-214">It fetches the changes from GitHub, builds them, and deploys the application to the cluster endpoint you specified in post-build actions.</span></span>  

  <!-- Images -->
  [build-step]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png


