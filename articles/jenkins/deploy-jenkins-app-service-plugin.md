---
title: Deploy to Azure App Service by using the Jenkins plugin
description: Learn how to use the Azure App Service Jenkins plugin to deploy a Java web app to Azure in Jenkins
ms.service: jenkins
keywords: jenkins, azure, devops, app service
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.topic: tutorial
ms.date: 07/31/2018
ms.openlocfilehash: a6ad40f90e12bbf4dd85c3cbd22839d39a734ca1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865268"
---
# <a name="deploy-to-azure-app-service-by-using-the-jenkins-plugin"></a><span data-ttu-id="151f6-104">Deploy to Azure App Service by using the Jenkins plugin</span><span class="sxs-lookup"><span data-stu-id="151f6-104">Deploy to Azure App Service by using the Jenkins plugin</span></span> 

<span data-ttu-id="151f6-105">To deploy a Java web app to Azure, you can use the Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can use the [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="151f6-105">To deploy a Java web app to Azure, you can use the Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can use the [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="151f6-106">The Jenkins plugin version 1.0 supports continuous deployment by using the Web Apps feature of Azure App Service through:</span><span class="sxs-lookup"><span data-stu-id="151f6-106">The Jenkins plugin version 1.0 supports continuous deployment by using the Web Apps feature of Azure App Service through:</span></span>
* <span data-ttu-id="151f6-107">File upload.</span><span class="sxs-lookup"><span data-stu-id="151f6-107">File upload.</span></span>
* <span data-ttu-id="151f6-108">Docker for Web Apps on Linux.</span><span class="sxs-lookup"><span data-stu-id="151f6-108">Docker for Web Apps on Linux.</span></span>

<span data-ttu-id="151f6-109">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="151f6-109">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="151f6-110">Configure Jenkins to deploy Web Apps through file upload.</span><span class="sxs-lookup"><span data-stu-id="151f6-110">Configure Jenkins to deploy Web Apps through file upload.</span></span>
> * <span data-ttu-id="151f6-111">Configure Jenkins to deploy Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="151f6-111">Configure Jenkins to deploy Web App for Containers.</span></span>

## <a name="create-and-configure-a-jenkins-instance"></a><span data-ttu-id="151f6-112">Create and configure a Jenkins instance</span><span class="sxs-lookup"><span data-stu-id="151f6-112">Create and configure a Jenkins instance</span></span>

<span data-ttu-id="151f6-113">If you don't already have a Jenkins Master, start with the [solution template](install-jenkins-solution-template.md), which includes the Java Development Kit (JDK) version 8 and the following required Jenkins plugins:</span><span class="sxs-lookup"><span data-stu-id="151f6-113">If you don't already have a Jenkins Master, start with the [solution template](install-jenkins-solution-template.md), which includes the Java Development Kit (JDK) version 8 and the following required Jenkins plugins:</span></span>

* <span data-ttu-id="151f6-114">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) version 2.4.6</span><span class="sxs-lookup"><span data-stu-id="151f6-114">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) version 2.4.6</span></span> 
* <span data-ttu-id="151f6-115">[Docker Commons plugin](https://plugins.jenkins.io/docker-commons) version 1.4.0</span><span class="sxs-lookup"><span data-stu-id="151f6-115">[Docker Commons plugin](https://plugins.jenkins.io/docker-commons) version 1.4.0</span></span>
* <span data-ttu-id="151f6-116">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) version 1.2</span><span class="sxs-lookup"><span data-stu-id="151f6-116">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) version 1.2</span></span>
* <span data-ttu-id="151f6-117">[Azure App Service](https://plugins.jenkins.io/azure-app-service) version 0.1</span><span class="sxs-lookup"><span data-stu-id="151f6-117">[Azure App Service](https://plugins.jenkins.io/azure-app-service) version 0.1</span></span>

<span data-ttu-id="151f6-118">You can use the Jenkins plugin to deploy a web app in any language that is supported by Web Apps, such as C#, PHP, Java, and Node.js.</span><span class="sxs-lookup"><span data-stu-id="151f6-118">You can use the Jenkins plugin to deploy a web app in any language that is supported by Web Apps, such as C#, PHP, Java, and Node.js.</span></span> <span data-ttu-id="151f6-119">In this tutorial, we use a [simple Java web app for Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="151f6-119">In this tutorial, we use a [simple Java web app for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="151f6-120">To fork the repo to your own GitHub account, select the **Fork** button in the upper right corner of the GitHub interface.</span><span class="sxs-lookup"><span data-stu-id="151f6-120">To fork the repo to your own GitHub account, select the **Fork** button in the upper right corner of the GitHub interface.</span></span>  
> [!NOTE]
> <span data-ttu-id="151f6-121">The Java JDK and Maven are required to build the Java project.</span><span class="sxs-lookup"><span data-stu-id="151f6-121">The Java JDK and Maven are required to build the Java project.</span></span> <span data-ttu-id="151f6-122">Install these components on the Jenkins Master, or on the VM agent if you use the agent for continuous integration.</span><span class="sxs-lookup"><span data-stu-id="151f6-122">Install these components on the Jenkins Master, or on the VM agent if you use the agent for continuous integration.</span></span> <span data-ttu-id="151f6-123">If you are deploying a Java SE application, ZIP is also needed on the build server.</span><span class="sxs-lookup"><span data-stu-id="151f6-123">If you are deploying a Java SE application, ZIP is also needed on the build server.</span></span>

<span data-ttu-id="151f6-124">To install the components, sign in to the Jenkins instance with SSH and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="151f6-124">To install the components, sign in to the Jenkins instance with SSH and run the following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="151f6-125">To deploy to Web App for Containers, install Docker on the Jenkins Master or on the VM agent that is used for the build.</span><span class="sxs-lookup"><span data-stu-id="151f6-125">To deploy to Web App for Containers, install Docker on the Jenkins Master or on the VM agent that is used for the build.</span></span> <span data-ttu-id="151f6-126">For instructions, see [Install Docker on Ubuntu](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="151f6-126">For instructions, see [Install Docker on Ubuntu](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>

##<a name="service-principal"></a> <span data-ttu-id="151f6-127">Add an Azure service principal to the Jenkins credentials</span><span class="sxs-lookup"><span data-stu-id="151f6-127">Add an Azure service principal to the Jenkins credentials</span></span>

<span data-ttu-id="151f6-128">You need an Azure service principal to deploy to Azure.</span><span class="sxs-lookup"><span data-stu-id="151f6-128">You need an Azure service principal to deploy to Azure.</span></span> 


1. <span data-ttu-id="151f6-129">To create an Azure service principal, use the [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or the [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal).</span><span class="sxs-lookup"><span data-stu-id="151f6-129">To create an Azure service principal, use the [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or the [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal).</span></span>
2. <span data-ttu-id="151f6-130">On the Jenkins dashboard, select **Credentials** > **System**.</span><span class="sxs-lookup"><span data-stu-id="151f6-130">On the Jenkins dashboard, select **Credentials** > **System**.</span></span> <span data-ttu-id="151f6-131">Then, select **Global credentials(unrestricted)**.</span><span class="sxs-lookup"><span data-stu-id="151f6-131">Then, select **Global credentials(unrestricted)**.</span></span>
3. <span data-ttu-id="151f6-132">To add a Microsoft Azure service principal, select **Add Credentials**.</span><span class="sxs-lookup"><span data-stu-id="151f6-132">To add a Microsoft Azure service principal, select **Add Credentials**.</span></span> <span data-ttu-id="151f6-133">Supply values for the **Subscription ID**, **Client ID**, **Client Secret**, and **OAuth 2.0 Token Endpoint** fields.</span><span class="sxs-lookup"><span data-stu-id="151f6-133">Supply values for the **Subscription ID**, **Client ID**, **Client Secret**, and **OAuth 2.0 Token Endpoint** fields.</span></span> <span data-ttu-id="151f6-134">Set the **ID** field to **mySp**.</span><span class="sxs-lookup"><span data-stu-id="151f6-134">Set the **ID** field to **mySp**.</span></span> <span data-ttu-id="151f6-135">We use this ID in subsequent steps in this article.</span><span class="sxs-lookup"><span data-stu-id="151f6-135">We use this ID in subsequent steps in this article.</span></span>


## <a name="configure-jenkins-to-deploy-web-apps-by-uploading-files"></a><span data-ttu-id="151f6-136">Configure Jenkins to deploy Web Apps by uploading files</span><span class="sxs-lookup"><span data-stu-id="151f6-136">Configure Jenkins to deploy Web Apps by uploading files</span></span>

<span data-ttu-id="151f6-137">To deploy your project to Web Apps, you can upload your build artifacts by file upload.</span><span class="sxs-lookup"><span data-stu-id="151f6-137">To deploy your project to Web Apps, you can upload your build artifacts by file upload.</span></span> <span data-ttu-id="151f6-138">Azure App Service supports multiple deployment options.</span><span class="sxs-lookup"><span data-stu-id="151f6-138">Azure App Service supports multiple deployment options.</span></span> <span data-ttu-id="151f6-139">The Azure App Service Jenkins plugin makes it simple for you and derives the deployment option based on the file type.</span><span class="sxs-lookup"><span data-stu-id="151f6-139">The Azure App Service Jenkins plugin makes it simple for you and derives the deployment option based on the file type.</span></span> 

* <span data-ttu-id="151f6-140">For Java EE applications, [WAR deployment](/azure/app-service/app-service-deploy-zip#deploy-war-file) is used.</span><span class="sxs-lookup"><span data-stu-id="151f6-140">For Java EE applications, [WAR deployment](/azure/app-service/app-service-deploy-zip#deploy-war-file) is used.</span></span>
* <span data-ttu-id="151f6-141">For Java SE applications, [ZIP deployment](/azure/app-service/app-service-deploy-zip#deploy-zip-file) is used.</span><span class="sxs-lookup"><span data-stu-id="151f6-141">For Java SE applications, [ZIP deployment](/azure/app-service/app-service-deploy-zip#deploy-zip-file) is used.</span></span>
* <span data-ttu-id="151f6-142">For other languages, [Git deployment](/azure/app-service/app-service-deploy-local-git) is used.</span><span class="sxs-lookup"><span data-stu-id="151f6-142">For other languages, [Git deployment](/azure/app-service/app-service-deploy-local-git) is used.</span></span>

<span data-ttu-id="151f6-143">Before you set up the job in Jenkins, you need an Azure App Service plan and a web app to run the Java app.</span><span class="sxs-lookup"><span data-stu-id="151f6-143">Before you set up the job in Jenkins, you need an Azure App Service plan and a web app to run the Java app.</span></span>


1. <span data-ttu-id="151f6-144">Create an Azure App Service plan with the **FREE** pricing tier by using the `az appservice plan create` [Azure CLI command](/cli/azure/appservice/plan#az-appservice-plan-create).</span><span class="sxs-lookup"><span data-stu-id="151f6-144">Create an Azure App Service plan with the **FREE** pricing tier by using the `az appservice plan create` [Azure CLI command](/cli/azure/appservice/plan#az-appservice-plan-create).</span></span> <span data-ttu-id="151f6-145">The App Service plan defines the physical resources that are used to host your apps.</span><span class="sxs-lookup"><span data-stu-id="151f6-145">The App Service plan defines the physical resources that are used to host your apps.</span></span> <span data-ttu-id="151f6-146">All applications that are assigned to an App Service plan share these resources.</span><span class="sxs-lookup"><span data-stu-id="151f6-146">All applications that are assigned to an App Service plan share these resources.</span></span> <span data-ttu-id="151f6-147">Shared resources help you to save on costs when hosting multiple apps.</span><span class="sxs-lookup"><span data-stu-id="151f6-147">Shared resources help you to save on costs when hosting multiple apps.</span></span>
2. <span data-ttu-id="151f6-148">Create a web app.</span><span class="sxs-lookup"><span data-stu-id="151f6-148">Create a web app.</span></span> <span data-ttu-id="151f6-149">You can use the [Azure portal](/azure/app-service-web/web-sites-configure) or the following `az` Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="151f6-149">You can use the [Azure portal](/azure/app-service-web/web-sites-configure) or the following `az` Azure CLI command:</span></span>
    ```azurecli-interactive 
    az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
    ```
    
3. <span data-ttu-id="151f6-150">Set up the Java runtime configuration that your app needs.</span><span class="sxs-lookup"><span data-stu-id="151f6-150">Set up the Java runtime configuration that your app needs.</span></span> <span data-ttu-id="151f6-151">The following Azure CLI command configures the web app to run on a recent JDK 8 and [Apache Tomcat](http://tomcat.apache.org/) version 8.0:</span><span class="sxs-lookup"><span data-stu-id="151f6-151">The following Azure CLI command configures the web app to run on a recent JDK 8 and [Apache Tomcat](http://tomcat.apache.org/) version 8.0:</span></span>
    ```azurecli-interactive
    az webapp config set \
    --name <myAppName> \
    --resource-group <myResourceGroup> \
    --java-version 1.8 \
    --java-container Tomcat \
    --java-container-version 8.0
    ```

### <a name="set-up-the-jenkins-job"></a><span data-ttu-id="151f6-152">Set up the Jenkins job</span><span class="sxs-lookup"><span data-stu-id="151f6-152">Set up the Jenkins job</span></span>

1. <span data-ttu-id="151f6-153">Create a new **freestyle** project on the Jenkins Dashboard.</span><span class="sxs-lookup"><span data-stu-id="151f6-153">Create a new **freestyle** project on the Jenkins Dashboard.</span></span>
2. <span data-ttu-id="151f6-154">Configure the **Source Code Management** field to use your local fork of the [simple Java web app for Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="151f6-154">Configure the **Source Code Management** field to use your local fork of the [simple Java web app for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="151f6-155">Provide the **Repository URL** value.</span><span class="sxs-lookup"><span data-stu-id="151f6-155">Provide the **Repository URL** value.</span></span> <span data-ttu-id="151f6-156">For example: http://github.com/&lt;your_ID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="151f6-156">For example: http://github.com/&lt;your_ID>/javawebappsample.</span></span>
3. <span data-ttu-id="151f6-157">Add a step to build the project by using Maven by adding the **Execute shell** command.</span><span class="sxs-lookup"><span data-stu-id="151f6-157">Add a step to build the project by using Maven by adding the **Execute shell** command.</span></span> <span data-ttu-id="151f6-158">For this example, we need an additional command to rename the \*.war file in the target folder to **ROOT.war**:</span><span class="sxs-lookup"><span data-stu-id="151f6-158">For this example, we need an additional command to rename the \*.war file in the target folder to **ROOT.war**:</span></span>   
    ```bash
    mvn clean package
    mv target/*.war target/ROOT.war
    ```

4. <span data-ttu-id="151f6-159">Add a post-build action by selecting **Publish an Azure Web App**.</span><span class="sxs-lookup"><span data-stu-id="151f6-159">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="151f6-160">Supply **mySp** as the Azure service principal.</span><span class="sxs-lookup"><span data-stu-id="151f6-160">Supply **mySp** as the Azure service principal.</span></span> <span data-ttu-id="151f6-161">This principal was stored as the [Azure Credentials](#service-principal) in a previous step.</span><span class="sxs-lookup"><span data-stu-id="151f6-161">This principal was stored as the [Azure Credentials](#service-principal) in a previous step.</span></span>
6. <span data-ttu-id="151f6-162">In the **App Configuration** section, choose the resource group and web app in your subscription.</span><span class="sxs-lookup"><span data-stu-id="151f6-162">In the **App Configuration** section, choose the resource group and web app in your subscription.</span></span> <span data-ttu-id="151f6-163">The Jenkins plugin automatically detects whether the web app is based on Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="151f6-163">The Jenkins plugin automatically detects whether the web app is based on Windows or Linux.</span></span> <span data-ttu-id="151f6-164">For a Windows web app, the **Publish Files** option is presented.</span><span class="sxs-lookup"><span data-stu-id="151f6-164">For a Windows web app, the **Publish Files** option is presented.</span></span>
7. <span data-ttu-id="151f6-165">Fill in the files that you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="151f6-165">Fill in the files that you want to deploy.</span></span> <span data-ttu-id="151f6-166">For example, specify the WAR package if you're using Java.</span><span class="sxs-lookup"><span data-stu-id="151f6-166">For example, specify the WAR package if you're using Java.</span></span> <span data-ttu-id="151f6-167">Use the optional **Source Directory** and **Target Directory** parameters to specify the source and target folders to use for file upload.</span><span class="sxs-lookup"><span data-stu-id="151f6-167">Use the optional **Source Directory** and **Target Directory** parameters to specify the source and target folders to use for file upload.</span></span> <span data-ttu-id="151f6-168">The Java web app on Azure is run in a Tomcat server.</span><span class="sxs-lookup"><span data-stu-id="151f6-168">The Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="151f6-169">So for Java, you upload your WAR package to the webapps folder.</span><span class="sxs-lookup"><span data-stu-id="151f6-169">So for Java, you upload your WAR package to the webapps folder.</span></span> <span data-ttu-id="151f6-170">For this example, set the **Source Directory** value to **target** and the **Target Directory** value to **webapps**.</span><span class="sxs-lookup"><span data-stu-id="151f6-170">For this example, set the **Source Directory** value to **target** and the **Target Directory** value to **webapps**.</span></span>
8. <span data-ttu-id="151f6-171">If you want to deploy to a slot other than production, you can also set the **Slot** name.</span><span class="sxs-lookup"><span data-stu-id="151f6-171">If you want to deploy to a slot other than production, you can also set the **Slot** name.</span></span>
9. <span data-ttu-id="151f6-172">Save the project and build it.</span><span class="sxs-lookup"><span data-stu-id="151f6-172">Save the project and build it.</span></span> <span data-ttu-id="151f6-173">Your web app is deployed to Azure when the build is complete.</span><span class="sxs-lookup"><span data-stu-id="151f6-173">Your web app is deployed to Azure when the build is complete.</span></span>

### <a name="deploy-web-apps-by-uploading-files-using-jenkins-pipeline"></a><span data-ttu-id="151f6-174">Deploy Web Apps by uploading files using Jenkins Pipeline</span><span class="sxs-lookup"><span data-stu-id="151f6-174">Deploy Web Apps by uploading files using Jenkins Pipeline</span></span>

<span data-ttu-id="151f6-175">The Azure App Service Jenkins plugin is pipeline-ready.</span><span class="sxs-lookup"><span data-stu-id="151f6-175">The Azure App Service Jenkins plugin is pipeline-ready.</span></span> <span data-ttu-id="151f6-176">You can refer to the following sample in the GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="151f6-176">You can refer to the following sample in the GitHub repo.</span></span>

1. <span data-ttu-id="151f6-177">In the GitHub interface, open the **Jenkinsfile_ftp_plugin** file.</span><span class="sxs-lookup"><span data-stu-id="151f6-177">In the GitHub interface, open the **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="151f6-178">To edit the file, select the pencil icon.</span><span class="sxs-lookup"><span data-stu-id="151f6-178">To edit the file, select the pencil icon.</span></span> <span data-ttu-id="151f6-179">Update the **resourceGroup** and **webAppName** definitions for your web app on lines 11 and 12, respectively:</span><span class="sxs-lookup"><span data-stu-id="151f6-179">Update the **resourceGroup** and **webAppName** definitions for your web app on lines 11 and 12, respectively:</span></span>
    ```java
    def resourceGroup = '<myResourceGroup>'
    def webAppName = '<myAppName>'
    ```

2. <span data-ttu-id="151f6-180">Set the **withCredentials** definition on line 14 to the credential ID in your Jenkins instance:</span><span class="sxs-lookup"><span data-stu-id="151f6-180">Set the **withCredentials** definition on line 14 to the credential ID in your Jenkins instance:</span></span>
    ```java
    withCredentials([azureServicePrincipal('<mySp>')]) {
    ```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="151f6-181">Create a Jenkins pipeline</span><span class="sxs-lookup"><span data-stu-id="151f6-181">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="151f6-182">Open Jenkins in a web browser.</span><span class="sxs-lookup"><span data-stu-id="151f6-182">Open Jenkins in a web browser.</span></span> <span data-ttu-id="151f6-183">Select **New Item**.</span><span class="sxs-lookup"><span data-stu-id="151f6-183">Select **New Item**.</span></span>
2. <span data-ttu-id="151f6-184">Provide a name for the job and select **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="151f6-184">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="151f6-185">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="151f6-185">Select **OK**.</span></span>
3. <span data-ttu-id="151f6-186">Select the **Pipeline** tab.</span><span class="sxs-lookup"><span data-stu-id="151f6-186">Select the **Pipeline** tab.</span></span>
4. <span data-ttu-id="151f6-187">For the **Definition** value, select **Pipeline script from SCM**.</span><span class="sxs-lookup"><span data-stu-id="151f6-187">For the **Definition** value, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="151f6-188">For the **SCM** value, select **Git**.</span><span class="sxs-lookup"><span data-stu-id="151f6-188">For the **SCM** value, select **Git**.</span></span> <span data-ttu-id="151f6-189">Enter the GitHub URL for your forked repo.</span><span class="sxs-lookup"><span data-stu-id="151f6-189">Enter the GitHub URL for your forked repo.</span></span> <span data-ttu-id="151f6-190">For example: https://&lt;your_forked_repo>.git.</span><span class="sxs-lookup"><span data-stu-id="151f6-190">For example: https://&lt;your_forked_repo>.git.</span></span>
6. <span data-ttu-id="151f6-191">Update the **Script Path** value to **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="151f6-191">Update the **Script Path** value to **Jenkinsfile_ftp_plugin**.</span></span>
7. <span data-ttu-id="151f6-192">Select **Save** and run the job.</span><span class="sxs-lookup"><span data-stu-id="151f6-192">Select **Save** and run the job.</span></span>

## <a name="configure-jenkins-to-deploy-web-app-for-containers"></a><span data-ttu-id="151f6-193">Configure Jenkins to deploy Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="151f6-193">Configure Jenkins to deploy Web App for Containers</span></span>

<span data-ttu-id="151f6-194">Web Apps on Linux supports deployment by using Docker.</span><span class="sxs-lookup"><span data-stu-id="151f6-194">Web Apps on Linux supports deployment by using Docker.</span></span> <span data-ttu-id="151f6-195">To deploy your web app by using Docker, you need to provide a Dockerfile that packages your web app with a service runtime into a Docker image.</span><span class="sxs-lookup"><span data-stu-id="151f6-195">To deploy your web app by using Docker, you need to provide a Dockerfile that packages your web app with a service runtime into a Docker image.</span></span> <span data-ttu-id="151f6-196">The Jenkins plugin then builds the image, pushes it to a Docker registry, and deploys the image to your web app.</span><span class="sxs-lookup"><span data-stu-id="151f6-196">The Jenkins plugin then builds the image, pushes it to a Docker registry, and deploys the image to your web app.</span></span>

<span data-ttu-id="151f6-197">Web Apps on Linux also supports traditional deployment methods, like Git and file upload, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span><span class="sxs-lookup"><span data-stu-id="151f6-197">Web Apps on Linux also supports traditional deployment methods, like Git and file upload, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="151f6-198">For other languages, you need to package your application code and service runtime together into a Docker image and use Docker to deploy.</span><span class="sxs-lookup"><span data-stu-id="151f6-198">For other languages, you need to package your application code and service runtime together into a Docker image and use Docker to deploy.</span></span>

<span data-ttu-id="151f6-199">Before setting up the job in Jenkins, you need a web app on Linux.</span><span class="sxs-lookup"><span data-stu-id="151f6-199">Before setting up the job in Jenkins, you need a web app on Linux.</span></span> <span data-ttu-id="151f6-200">You also need a container registry to store and manage your private Docker container images.</span><span class="sxs-lookup"><span data-stu-id="151f6-200">You also need a container registry to store and manage your private Docker container images.</span></span> <span data-ttu-id="151f6-201">You can use DockerHub to create the container registry.</span><span class="sxs-lookup"><span data-stu-id="151f6-201">You can use DockerHub to create the container registry.</span></span> <span data-ttu-id="151f6-202">In this example, we use Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="151f6-202">In this example, we use Azure Container Registry.</span></span>

* <span data-ttu-id="151f6-203">[Create your web app on Linux](../app-service/containers/quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="151f6-203">[Create your web app on Linux](../app-service/containers/quickstart-nodejs.md).</span></span>
* <span data-ttu-id="151f6-204">Azure Container Registry is a managed [Docker Registry](https://docs.docker.com/registry/) service that is based on the open-source Docker Registry version 2.0.</span><span class="sxs-lookup"><span data-stu-id="151f6-204">Azure Container Registry is a managed [Docker Registry](https://docs.docker.com/registry/) service that is based on the open-source Docker Registry version 2.0.</span></span> <span data-ttu-id="151f6-205">[Create an Azure container registry](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="151f6-205">[Create an Azure container registry](/azure/container-registry/container-registry-get-started-azure-cli).</span></span> <span data-ttu-id="151f6-206">You can also use DockerHub.</span><span class="sxs-lookup"><span data-stu-id="151f6-206">You can also use DockerHub.</span></span>

### <a name="set-up-the-jenkins-job-for-docker"></a><span data-ttu-id="151f6-207">Set up the Jenkins job for Docker</span><span class="sxs-lookup"><span data-stu-id="151f6-207">Set up the Jenkins job for Docker</span></span>

1. <span data-ttu-id="151f6-208">Create a new **freestyle** project on the Jenkins Dashboard.</span><span class="sxs-lookup"><span data-stu-id="151f6-208">Create a new **freestyle** project on the Jenkins Dashboard.</span></span>
2. <span data-ttu-id="151f6-209">Configure the **Source Code Management** field to use your local fork of the [simple Java web app for Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="151f6-209">Configure the **Source Code Management** field to use your local fork of the [simple Java web app for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="151f6-210">Provide the **Repository URL** value.</span><span class="sxs-lookup"><span data-stu-id="151f6-210">Provide the **Repository URL** value.</span></span> <span data-ttu-id="151f6-211">For example: http://github.com/&lt;your_ID>/javawebappsample.</span><span class="sxs-lookup"><span data-stu-id="151f6-211">For example: http://github.com/&lt;your_ID>/javawebappsample.</span></span>
3. <span data-ttu-id="151f6-212">Add a step to build the project by using Maven by adding an **Execute shell** command.</span><span class="sxs-lookup"><span data-stu-id="151f6-212">Add a step to build the project by using Maven by adding an **Execute shell** command.</span></span> <span data-ttu-id="151f6-213">Include the following line in the command:</span><span class="sxs-lookup"><span data-stu-id="151f6-213">Include the following line in the command:</span></span>
    ```bash
    mvn clean package
    ```

4. <span data-ttu-id="151f6-214">Add a post-build action by selecting **Publish an Azure Web App**.</span><span class="sxs-lookup"><span data-stu-id="151f6-214">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="151f6-215">Supply **mySp** as the Azure service principal.</span><span class="sxs-lookup"><span data-stu-id="151f6-215">Supply **mySp** as the Azure service principal.</span></span> <span data-ttu-id="151f6-216">This principal was stored as the [Azure Credentials](#service-principal) in a previous step.</span><span class="sxs-lookup"><span data-stu-id="151f6-216">This principal was stored as the [Azure Credentials](#service-principal) in a previous step.</span></span>
6. <span data-ttu-id="151f6-217">In the **App Configuration** section, choose the resource group and a Linux web app in your subscription.</span><span class="sxs-lookup"><span data-stu-id="151f6-217">In the **App Configuration** section, choose the resource group and a Linux web app in your subscription.</span></span>
7. <span data-ttu-id="151f6-218">Choose **Publish via Docker**.</span><span class="sxs-lookup"><span data-stu-id="151f6-218">Choose **Publish via Docker**.</span></span>
8. <span data-ttu-id="151f6-219">Fill in the **Dockerfile** path value.</span><span class="sxs-lookup"><span data-stu-id="151f6-219">Fill in the **Dockerfile** path value.</span></span> <span data-ttu-id="151f6-220">You can keep the default value /Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="151f6-220">You can keep the default value /Dockerfile.</span></span>
<span data-ttu-id="151f6-221">For the **Docker registry URL** value, supply the URL by using the format https://&lt;yourRegistry>.azurecr.io if you use Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="151f6-221">For the **Docker registry URL** value, supply the URL by using the format https://&lt;yourRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="151f6-222">If you use DockerHub, leave the value blank.</span><span class="sxs-lookup"><span data-stu-id="151f6-222">If you use DockerHub, leave the value blank.</span></span>
9. <span data-ttu-id="151f6-223">For the **Registry credentials** value, add the credential for the container registry.</span><span class="sxs-lookup"><span data-stu-id="151f6-223">For the **Registry credentials** value, add the credential for the container registry.</span></span> <span data-ttu-id="151f6-224">You can get the userid and password by running the following commands in the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="151f6-224">You can get the userid and password by running the following commands in the Azure CLI.</span></span> <span data-ttu-id="151f6-225">The first command enables the administrator account:</span><span class="sxs-lookup"><span data-stu-id="151f6-225">The first command enables the administrator account:</span></span>
    ```azurecli-interactive
    az acr update -n <yourRegistry> --admin-enabled true
    az acr credential show -n <yourRegistry>
    ```

10. <span data-ttu-id="151f6-226">The Docker image name and tag value in the **Advanced** tab are optional.</span><span class="sxs-lookup"><span data-stu-id="151f6-226">The Docker image name and tag value in the **Advanced** tab are optional.</span></span> <span data-ttu-id="151f6-227">By default, the value for the image name is obtained from the image name that you configured in the Azure portal in the **Docker Container** setting.</span><span class="sxs-lookup"><span data-stu-id="151f6-227">By default, the value for the image name is obtained from the image name that you configured in the Azure portal in the **Docker Container** setting.</span></span> <span data-ttu-id="151f6-228">The tag is generated from $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="151f6-228">The tag is generated from $BUILD_NUMBER.</span></span>
    > [!NOTE]
    > <span data-ttu-id="151f6-229">Be sure to specify the image name in the Azure portal or supply a **Docker Image** value in the **Advanced** tab. For this example, set the **Docker image** value to &lt;your_Registry>.azurecr.io/calculator and leave the **Docker Image Tag** value blank.</span><span class="sxs-lookup"><span data-stu-id="151f6-229">Be sure to specify the image name in the Azure portal or supply a **Docker Image** value in the **Advanced** tab. For this example, set the **Docker image** value to &lt;your_Registry>.azurecr.io/calculator and leave the **Docker Image Tag** value blank.</span></span>

11. <span data-ttu-id="151f6-230">The deploy fails if you use a built-in Docker image setting.</span><span class="sxs-lookup"><span data-stu-id="151f6-230">The deploy fails if you use a built-in Docker image setting.</span></span> <span data-ttu-id="151f6-231">Change the Docker configuration to use a custom image in the **Docker Container** setting in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="151f6-231">Change the Docker configuration to use a custom image in the **Docker Container** setting in the Azure portal.</span></span> <span data-ttu-id="151f6-232">For a built-in image, use the file upload approach to deploy.</span><span class="sxs-lookup"><span data-stu-id="151f6-232">For a built-in image, use the file upload approach to deploy.</span></span>
12. <span data-ttu-id="151f6-233">Similar to the file upload approach, you can choose a different **Slot** name other than **production**.</span><span class="sxs-lookup"><span data-stu-id="151f6-233">Similar to the file upload approach, you can choose a different **Slot** name other than **production**.</span></span>
13. <span data-ttu-id="151f6-234">Save and build the project.</span><span class="sxs-lookup"><span data-stu-id="151f6-234">Save and build the project.</span></span> <span data-ttu-id="151f6-235">Your container image is pushed to your registry and the web app is deployed.</span><span class="sxs-lookup"><span data-stu-id="151f6-235">Your container image is pushed to your registry and the web app is deployed.</span></span>

### <a name="deploy-web-app-for-containers-by-using-jenkins-pipeline"></a><span data-ttu-id="151f6-236">Deploy Web App for Containers by using Jenkins Pipeline</span><span class="sxs-lookup"><span data-stu-id="151f6-236">Deploy Web App for Containers by using Jenkins Pipeline</span></span>

1. <span data-ttu-id="151f6-237">In the GitHub interface, open the **Jenkinsfile_container_plugin** file.</span><span class="sxs-lookup"><span data-stu-id="151f6-237">In the GitHub interface, open the **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="151f6-238">To edit the file, select the pencil icon.</span><span class="sxs-lookup"><span data-stu-id="151f6-238">To edit the file, select the pencil icon.</span></span> <span data-ttu-id="151f6-239">Update the **resourceGroup** and **webAppName** definitions for your web app on lines 11 and 12, respectively:</span><span class="sxs-lookup"><span data-stu-id="151f6-239">Update the **resourceGroup** and **webAppName** definitions for your web app on lines 11 and 12, respectively:</span></span>
    ```java
    def resourceGroup = '<myResourceGroup>'
    def webAppName = '<myAppName>'
    ```

2. <span data-ttu-id="151f6-240">Change line 13 to your container registry server:</span><span class="sxs-lookup"><span data-stu-id="151f6-240">Change line 13 to your container registry server:</span></span>
    ```java
    def registryServer = '<registryURL>'
    ```

3. <span data-ttu-id="151f6-241">Change line 16 to use the credential ID in your Jenkins instance:</span><span class="sxs-lookup"><span data-stu-id="151f6-241">Change line 16 to use the credential ID in your Jenkins instance:</span></span>
    ```java
    azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
    ```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="151f6-242">Create a Jenkins pipeline</span><span class="sxs-lookup"><span data-stu-id="151f6-242">Create a Jenkins pipeline</span></span>    

1. <span data-ttu-id="151f6-243">Open Jenkins in a web browser.</span><span class="sxs-lookup"><span data-stu-id="151f6-243">Open Jenkins in a web browser.</span></span> <span data-ttu-id="151f6-244">Select **New Item**.</span><span class="sxs-lookup"><span data-stu-id="151f6-244">Select **New Item**.</span></span>
2. <span data-ttu-id="151f6-245">Provide a name for the job and select **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="151f6-245">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="151f6-246">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="151f6-246">Select **OK**.</span></span>
3. <span data-ttu-id="151f6-247">Select the **Pipeline** tab.</span><span class="sxs-lookup"><span data-stu-id="151f6-247">Select the **Pipeline** tab.</span></span>
4. <span data-ttu-id="151f6-248">For the **Definition** value, select **Pipeline script from SCM**.</span><span class="sxs-lookup"><span data-stu-id="151f6-248">For the **Definition** value, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="151f6-249">For the **SCM** value, select **Git**.</span><span class="sxs-lookup"><span data-stu-id="151f6-249">For the **SCM** value, select **Git**.</span></span> <span data-ttu-id="151f6-250">Enter the GitHub URL for your forked repo.</span><span class="sxs-lookup"><span data-stu-id="151f6-250">Enter the GitHub URL for your forked repo.</span></span> <span data-ttu-id="151f6-251">For example: https://&lt;your_forked_repo>.git.</span><span class="sxs-lookup"><span data-stu-id="151f6-251">For example: https://&lt;your_forked_repo>.git.</span></span>
7. <span data-ttu-id="151f6-252">Update the **Script Path** value to **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="151f6-252">Update the **Script Path** value to **Jenkinsfile_container_plugin**.</span></span>
8. <span data-ttu-id="151f6-253">Select **Save** and run the job.</span><span class="sxs-lookup"><span data-stu-id="151f6-253">Select **Save** and run the job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="151f6-254">Verify your web app</span><span class="sxs-lookup"><span data-stu-id="151f6-254">Verify your web app</span></span>

1. <span data-ttu-id="151f6-255">To verify that the WAR file is deployed successfully to your web app, open a web browser.</span><span class="sxs-lookup"><span data-stu-id="151f6-255">To verify that the WAR file is deployed successfully to your web app, open a web browser.</span></span>
2. <span data-ttu-id="151f6-256">Go to http://&lt;your_app_name>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="151f6-256">Go to http://&lt;your_app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="151f6-257">Replace &lt;your_app_name> with the name of your web app.</span><span class="sxs-lookup"><span data-stu-id="151f6-257">Replace &lt;your_app_name> with the name of your web app.</span></span> <span data-ttu-id="151f6-258">You see the message:</span><span class="sxs-lookup"><span data-stu-id="151f6-258">You see the message:</span></span>
    ```
    Welcome to Java Web App!!! This is updated!
    Sun Jun 17 16:39:10 UTC 2017
    ```

3. <span data-ttu-id="151f6-259">Go to http://&lt;your_app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y>.</span><span class="sxs-lookup"><span data-stu-id="151f6-259">Go to http://&lt;your_app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y>.</span></span> <span data-ttu-id="151f6-260">Replace &lt;x> and &lt;y> with any numbers to get the sum of x + y.</span><span class="sxs-lookup"><span data-stu-id="151f6-260">Replace &lt;x> and &lt;y> with any numbers to get the sum of x + y.</span></span> <span data-ttu-id="151f6-261">The calculator shows the sum: ![Calculator: add](./media/execute-cli-jenkins-pipeline/calculator-add.png)</span><span class="sxs-lookup"><span data-stu-id="151f6-261">The calculator shows the sum: ![Calculator: add](./media/execute-cli-jenkins-pipeline/calculator-add.png)</span></span>

### <a name="for-azure-app-service-on-linux"></a><span data-ttu-id="151f6-262">For Azure App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="151f6-262">For Azure App Service on Linux</span></span>

1. <span data-ttu-id="151f6-263">To verify your web app, run the following command in the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="151f6-263">To verify your web app, run the following command in the Azure CLI:</span></span>
    ```CLI
    az acr repository list -n <myRegistry> -o json
    ```
    <span data-ttu-id="151f6-264">The following message is displayed:</span><span class="sxs-lookup"><span data-stu-id="151f6-264">The following message is displayed:</span></span>
    ```CLI
    ["calculator"]
    ```
    
2. <span data-ttu-id="151f6-265">Go to http://&lt;your_app_name>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="151f6-265">Go to http://&lt;your_app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="151f6-266">Replace &lt;your_app_name> with the name of your web app.</span><span class="sxs-lookup"><span data-stu-id="151f6-266">Replace &lt;your_app_name> with the name of your web app.</span></span> <span data-ttu-id="151f6-267">You see the message:</span><span class="sxs-lookup"><span data-stu-id="151f6-267">You see the message:</span></span> 
    ```
    Welcome to Java Web App!!! This is updated!
    Sun Jul 09 16:39:10 UTC 2017
    ```

3. <span data-ttu-id="151f6-268">Go to http://&lt;your_app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y>.</span><span class="sxs-lookup"><span data-stu-id="151f6-268">Go to http://&lt;your_app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y>.</span></span> <span data-ttu-id="151f6-269">Replace &lt;x> and &lt;y> with any numbers to get the sum of x + y.</span><span class="sxs-lookup"><span data-stu-id="151f6-269">Replace &lt;x> and &lt;y> with any numbers to get the sum of x + y.</span></span>
    
## <a name="troubleshooting-the-jenkins-plugin"></a><span data-ttu-id="151f6-270">Troubleshooting the Jenkins plugin</span><span class="sxs-lookup"><span data-stu-id="151f6-270">Troubleshooting the Jenkins plugin</span></span>

<span data-ttu-id="151f6-271">If you encounter any bugs with the Jenkins plugins, file an issue in the [Jenkins JIRA](https://issues.jenkins-ci.org/) for the specific component.</span><span class="sxs-lookup"><span data-stu-id="151f6-271">If you encounter any bugs with the Jenkins plugins, file an issue in the [Jenkins JIRA](https://issues.jenkins-ci.org/) for the specific component.</span></span>

## <a name="next-steps"></a><span data-ttu-id="151f6-272">Next steps</span><span class="sxs-lookup"><span data-stu-id="151f6-272">Next steps</span></span>

<span data-ttu-id="151f6-273">In this tutorial, you used the Azure App Service Jenkins plugin to deploy to Azure.</span><span class="sxs-lookup"><span data-stu-id="151f6-273">In this tutorial, you used the Azure App Service Jenkins plugin to deploy to Azure.</span></span>

<span data-ttu-id="151f6-274">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="151f6-274">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="151f6-275">Configure Jenkins to deploy Azure App Service through file upload</span><span class="sxs-lookup"><span data-stu-id="151f6-275">Configure Jenkins to deploy Azure App Service through file upload</span></span> 
> * <span data-ttu-id="151f6-276">Configure Jenkins to deploy to Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="151f6-276">Configure Jenkins to deploy to Web App for Containers</span></span> 
