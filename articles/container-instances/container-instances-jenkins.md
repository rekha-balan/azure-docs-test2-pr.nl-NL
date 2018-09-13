---
title: Use Azure Container Instances as a Jenkins build agent
description: Learn how to use Azure Container Instances as a Jenkins build agent.
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 08/31/2018
ms.author: marsma
ms.openlocfilehash: 9108d9e1b230fe2267f0195bd2c33c5a4c57d956
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856907"
---
# <a name="use-azure-container-instances-as-a-jenkins-build-agent"></a><span data-ttu-id="dc256-103">Use Azure Container Instances as a Jenkins build agent</span><span class="sxs-lookup"><span data-stu-id="dc256-103">Use Azure Container Instances as a Jenkins build agent</span></span>

<span data-ttu-id="dc256-104">Azure Container Instances (ACI) provides an on-demand, burstable, and isolated environment for running containerized workloads.</span><span class="sxs-lookup"><span data-stu-id="dc256-104">Azure Container Instances (ACI) provides an on-demand, burstable, and isolated environment for running containerized workloads.</span></span> <span data-ttu-id="dc256-105">Because of these attributes, ACI makes a great platform for running Jenkins build jobs at a large scale.</span><span class="sxs-lookup"><span data-stu-id="dc256-105">Because of these attributes, ACI makes a great platform for running Jenkins build jobs at a large scale.</span></span> <span data-ttu-id="dc256-106">This article walks through deploying and using a Jenkins server that's pre-configured with ACI as a build target.</span><span class="sxs-lookup"><span data-stu-id="dc256-106">This article walks through deploying and using a Jenkins server that's pre-configured with ACI as a build target.</span></span>

<span data-ttu-id="dc256-107">For more information on Azure Container Instances, see [About Azure Container Instances][about-aci].</span><span class="sxs-lookup"><span data-stu-id="dc256-107">For more information on Azure Container Instances, see [About Azure Container Instances][about-aci].</span></span>

## <a name="deploy-a-jenkins-server"></a><span data-ttu-id="dc256-108">Deploy a Jenkins server</span><span class="sxs-lookup"><span data-stu-id="dc256-108">Deploy a Jenkins server</span></span>

1. <span data-ttu-id="dc256-109">In the Azure portal, select **Create a resource** and search for **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="dc256-109">In the Azure portal, select **Create a resource** and search for **Jenkins**.</span></span> <span data-ttu-id="dc256-110">Select the Jenkins offering with a publisher of **Microsoft**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="dc256-110">Select the Jenkins offering with a publisher of **Microsoft**, and then select **Create**.</span></span>

2. <span data-ttu-id="dc256-111">Enter the following information on the **Basics** form, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc256-111">Enter the following information on the **Basics** form, and then select **OK**.</span></span>

   - <span data-ttu-id="dc256-112">**Name**: Enter a name for the Jenkins deployment.</span><span class="sxs-lookup"><span data-stu-id="dc256-112">**Name**: Enter a name for the Jenkins deployment.</span></span>
   - <span data-ttu-id="dc256-113">**User name**: Enter a name for the admin user of the Jenkins virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dc256-113">**User name**: Enter a name for the admin user of the Jenkins virtual machine.</span></span>
   - <span data-ttu-id="dc256-114">**Authentication type**: We recommend an SSH public key for authentication.</span><span class="sxs-lookup"><span data-stu-id="dc256-114">**Authentication type**: We recommend an SSH public key for authentication.</span></span> <span data-ttu-id="dc256-115">If you select this option, paste in an SSH public key to be used for logging in to the Jenkins virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dc256-115">If you select this option, paste in an SSH public key to be used for logging in to the Jenkins virtual machine.</span></span>
   - <span data-ttu-id="dc256-116">**Subscription**: Select an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="dc256-116">**Subscription**: Select an Azure subscription.</span></span>
   - <span data-ttu-id="dc256-117">**Resource group**: Create a resource group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="dc256-117">**Resource group**: Create a resource group or select an existing one.</span></span>
   - <span data-ttu-id="dc256-118">**Location**: Select a location for the Jenkins server.</span><span class="sxs-lookup"><span data-stu-id="dc256-118">**Location**: Select a location for the Jenkins server.</span></span>

   ![Basic settings for Jenkins portal deployment](./media/container-instances-jenkins/jenkins-portal-01.png)

3. <span data-ttu-id="dc256-120">On the **Additional Settings** form, complete the following items:</span><span class="sxs-lookup"><span data-stu-id="dc256-120">On the **Additional Settings** form, complete the following items:</span></span>

   - <span data-ttu-id="dc256-121">**Size**: Select the appropriate sizing option for your Jenkins virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dc256-121">**Size**: Select the appropriate sizing option for your Jenkins virtual machine.</span></span>
   - <span data-ttu-id="dc256-122">**VM disk type**: Specify either **HDD** (hard-disk drive) or **SSD** (solid-state drive) for the Jenkins server.</span><span class="sxs-lookup"><span data-stu-id="dc256-122">**VM disk type**: Specify either **HDD** (hard-disk drive) or **SSD** (solid-state drive) for the Jenkins server.</span></span>
   - <span data-ttu-id="dc256-123">**Virtual network**: Select the arrow if you want to modify the default settings.</span><span class="sxs-lookup"><span data-stu-id="dc256-123">**Virtual network**: Select the arrow if you want to modify the default settings.</span></span>
   - <span data-ttu-id="dc256-124">**Subnets**: Select the arrow, verify the information, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc256-124">**Subnets**: Select the arrow, verify the information, and select **OK**.</span></span>
   - <span data-ttu-id="dc256-125">**Public IP address**: Select the arrow to give the public IP address a custom name, configure the SKU, and set the assignment method.</span><span class="sxs-lookup"><span data-stu-id="dc256-125">**Public IP address**: Select the arrow to give the public IP address a custom name, configure the SKU, and set the assignment method.</span></span>
   - <span data-ttu-id="dc256-126">**Domain name label**: Specify a value to create a fully qualified URL to the Jenkins virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dc256-126">**Domain name label**: Specify a value to create a fully qualified URL to the Jenkins virtual machine.</span></span>
   - <span data-ttu-id="dc256-127">**Jenkins release type**: Select the desired release type from the options: **LTS**, **Weekly build**, or **Azure Verified**.</span><span class="sxs-lookup"><span data-stu-id="dc256-127">**Jenkins release type**: Select the desired release type from the options: **LTS**, **Weekly build**, or **Azure Verified**.</span></span>

   ![Additional settings for Jenkins portal deployment](./media/container-instances-jenkins/jenkins-portal-02.png)

4. <span data-ttu-id="dc256-129">For service principal integration, select **Auto(MSI)** to have [Azure Managed Service Identity][managed-identities-azure-resources] automatically create an authentication identity for the Jenkins instance.</span><span class="sxs-lookup"><span data-stu-id="dc256-129">For service principal integration, select **Auto(MSI)** to have [Azure Managed Service Identity][managed-identities-azure-resources] automatically create an authentication identity for the Jenkins instance.</span></span> <span data-ttu-id="dc256-130">Select **Manual** to provide your own service principal credentials.</span><span class="sxs-lookup"><span data-stu-id="dc256-130">Select **Manual** to provide your own service principal credentials.</span></span>

5. <span data-ttu-id="dc256-131">Cloud agents configure a cloud-based platform for Jenkins build jobs.</span><span class="sxs-lookup"><span data-stu-id="dc256-131">Cloud agents configure a cloud-based platform for Jenkins build jobs.</span></span> <span data-ttu-id="dc256-132">For the sake of this article, select **ACI**.</span><span class="sxs-lookup"><span data-stu-id="dc256-132">For the sake of this article, select **ACI**.</span></span> <span data-ttu-id="dc256-133">With the ACI cloud agent, each Jenkins build job is run in a container instance.</span><span class="sxs-lookup"><span data-stu-id="dc256-133">With the ACI cloud agent, each Jenkins build job is run in a container instance.</span></span>

   ![Cloud integration settings for Jenkins portal deployment](./media/container-instances-jenkins/jenkins-portal-03.png)

6. <span data-ttu-id="dc256-135">When you're done with the integration settings, select **OK**, and then select **OK** again on the validation summary.</span><span class="sxs-lookup"><span data-stu-id="dc256-135">When you're done with the integration settings, select **OK**, and then select **OK** again on the validation summary.</span></span> <span data-ttu-id="dc256-136">Select **Create** on the **Terms of use** summary.</span><span class="sxs-lookup"><span data-stu-id="dc256-136">Select **Create** on the **Terms of use** summary.</span></span> <span data-ttu-id="dc256-137">The Jenkins server takes a few minutes to deploy.</span><span class="sxs-lookup"><span data-stu-id="dc256-137">The Jenkins server takes a few minutes to deploy.</span></span>

## <a name="configure-jenkins"></a><span data-ttu-id="dc256-138">Configure Jenkins</span><span class="sxs-lookup"><span data-stu-id="dc256-138">Configure Jenkins</span></span>

1. <span data-ttu-id="dc256-139">In the Azure portal, browse to the Jenkins resource group, select the Jenkins virtual machine, and take note of the DNS name.</span><span class="sxs-lookup"><span data-stu-id="dc256-139">In the Azure portal, browse to the Jenkins resource group, select the Jenkins virtual machine, and take note of the DNS name.</span></span>

   ![DNS name in details about the Jenkins virtual machine](./media/container-instances-jenkins/jenkins-portal-fqdn.png)

2. <span data-ttu-id="dc256-141">Browse to the DNS name of the Jenkins VM and copy the returned SSH string.</span><span class="sxs-lookup"><span data-stu-id="dc256-141">Browse to the DNS name of the Jenkins VM and copy the returned SSH string.</span></span>

   ![Jenkins login instructions with SSH string](./media/container-instances-jenkins/jenkins-portal-04.png)

3. <span data-ttu-id="dc256-143">Open a terminal session on your development system, and paste in the SSH string from the last step.</span><span class="sxs-lookup"><span data-stu-id="dc256-143">Open a terminal session on your development system, and paste in the SSH string from the last step.</span></span> <span data-ttu-id="dc256-144">Update `username` to the username that you specified when you deployed the Jenkins server.</span><span class="sxs-lookup"><span data-stu-id="dc256-144">Update `username` to the username that you specified when you deployed the Jenkins server.</span></span>

4. <span data-ttu-id="dc256-145">After the session is connected, run the following command to retrieve the initial admin password:</span><span class="sxs-lookup"><span data-stu-id="dc256-145">After the session is connected, run the following command to retrieve the initial admin password:</span></span>

   ```
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```

5. <span data-ttu-id="dc256-146">Leave the SSH session and tunnel running, and go to http://localhost:8080 in a browser.</span><span class="sxs-lookup"><span data-stu-id="dc256-146">Leave the SSH session and tunnel running, and go to http://localhost:8080 in a browser.</span></span> <span data-ttu-id="dc256-147">Paste the initial admin password into the box, and then select **Continue**.</span><span class="sxs-lookup"><span data-stu-id="dc256-147">Paste the initial admin password into the box, and then select **Continue**.</span></span>

   !["Unlock Jenkins" screen with the box for the administrator password](./media/container-instances-jenkins/jenkins-portal-05.png)

6. <span data-ttu-id="dc256-149">Select **Install suggested plugins** to install all recommended Jenkins plugins.</span><span class="sxs-lookup"><span data-stu-id="dc256-149">Select **Install suggested plugins** to install all recommended Jenkins plugins.</span></span>

   !["Customize Jenkins" screen with "Install suggested plugins" selected](./media/container-instances-jenkins/jenkins-portal-06.png)

7. <span data-ttu-id="dc256-151">Create an admin user account.</span><span class="sxs-lookup"><span data-stu-id="dc256-151">Create an admin user account.</span></span> <span data-ttu-id="dc256-152">This account is used for logging in to and working with your Jenkins instance.</span><span class="sxs-lookup"><span data-stu-id="dc256-152">This account is used for logging in to and working with your Jenkins instance.</span></span>

   !["Create First Admin User" screen, with credentials filled in](./media/container-instances-jenkins/jenkins-portal-07.png)

8. <span data-ttu-id="dc256-154">Select **Save and Finish**, and then select **Start using Jenkins** to complete the configuration.</span><span class="sxs-lookup"><span data-stu-id="dc256-154">Select **Save and Finish**, and then select **Start using Jenkins** to complete the configuration.</span></span>

<span data-ttu-id="dc256-155">Jenkins is now configured and ready to build and deploy code.</span><span class="sxs-lookup"><span data-stu-id="dc256-155">Jenkins is now configured and ready to build and deploy code.</span></span> <span data-ttu-id="dc256-156">For this example, a simple Java application is used to demonstrate a Jenkins build on Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="dc256-156">For this example, a simple Java application is used to demonstrate a Jenkins build on Azure Container Instances.</span></span>

## <a name="create-a-build-job"></a><span data-ttu-id="dc256-157">Create a build job</span><span class="sxs-lookup"><span data-stu-id="dc256-157">Create a build job</span></span>

<span data-ttu-id="dc256-158">Now, a Jenkins build job is created to demonstrate Jenkins builds on an Azure container instance.</span><span class="sxs-lookup"><span data-stu-id="dc256-158">Now, a Jenkins build job is created to demonstrate Jenkins builds on an Azure container instance.</span></span>

1. <span data-ttu-id="dc256-159">Select **New Item**, give the build project a name such as **aci-demo**, select **Freestyle project**, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc256-159">Select **New Item**, give the build project a name such as **aci-demo**, select **Freestyle project**, and select **OK**.</span></span>

   ![Box for the name of the build job, and list of project types](./media/container-instances-jenkins/jenkins-new-job.png)

2. <span data-ttu-id="dc256-161">Under **General**, ensure that **Restrict where this project can be run** is selected.</span><span class="sxs-lookup"><span data-stu-id="dc256-161">Under **General**, ensure that **Restrict where this project can be run** is selected.</span></span> <span data-ttu-id="dc256-162">Enter **linux** for the label expression.</span><span class="sxs-lookup"><span data-stu-id="dc256-162">Enter **linux** for the label expression.</span></span> <span data-ttu-id="dc256-163">This configuration ensures that this build job runs on the ACI cloud.</span><span class="sxs-lookup"><span data-stu-id="dc256-163">This configuration ensures that this build job runs on the ACI cloud.</span></span>

   !["General" tab with configuration details](./media/container-instances-jenkins/jenkins-job-01.png)

3. <span data-ttu-id="dc256-165">Under **Build**, select **Add build step** and select **Execute Shell**.</span><span class="sxs-lookup"><span data-stu-id="dc256-165">Under **Build**, select **Add build step** and select **Execute Shell**.</span></span> <span data-ttu-id="dc256-166">Enter `echo "aci-demo"` as the command.</span><span class="sxs-lookup"><span data-stu-id="dc256-166">Enter `echo "aci-demo"` as the command.</span></span>

   !["Build" tab with selections for the build step](./media/container-instances-jenkins/jenkins-job-02.png)

5. <span data-ttu-id="dc256-168">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="dc256-168">Select **Save**.</span></span>

## <a name="run-the-build-job"></a><span data-ttu-id="dc256-169">Run the build job</span><span class="sxs-lookup"><span data-stu-id="dc256-169">Run the build job</span></span>

<span data-ttu-id="dc256-170">To test the build job and observe Azure Container Instances as the build platform, manually start a build.</span><span class="sxs-lookup"><span data-stu-id="dc256-170">To test the build job and observe Azure Container Instances as the build platform, manually start a build.</span></span>

1. <span data-ttu-id="dc256-171">Select **Build Now** to start a build job.</span><span class="sxs-lookup"><span data-stu-id="dc256-171">Select **Build Now** to start a build job.</span></span> <span data-ttu-id="dc256-172">It takes a few minutes for the job to start.</span><span class="sxs-lookup"><span data-stu-id="dc256-172">It takes a few minutes for the job to start.</span></span> <span data-ttu-id="dc256-173">You should see a status that's similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="dc256-173">You should see a status that's similar to the following image:</span></span>

   !["Build History" information with job status](./media/container-instances-jenkins/jenkins-job-status.png)

2. <span data-ttu-id="dc256-175">While the job is running, open the Azure portal and look at the Jenkins resource group.</span><span class="sxs-lookup"><span data-stu-id="dc256-175">While the job is running, open the Azure portal and look at the Jenkins resource group.</span></span> <span data-ttu-id="dc256-176">You should see that a container instance has been created.</span><span class="sxs-lookup"><span data-stu-id="dc256-176">You should see that a container instance has been created.</span></span> <span data-ttu-id="dc256-177">The Jenkins job is running inside this instance.</span><span class="sxs-lookup"><span data-stu-id="dc256-177">The Jenkins job is running inside this instance.</span></span>

   ![Container instance in the resource group](./media/container-instances-jenkins/jenkins-aci.png)

3. <span data-ttu-id="dc256-179">As Jenkins runs more jobs than the configured number of Jenkins executors (default 2), multiple container instances are created.</span><span class="sxs-lookup"><span data-stu-id="dc256-179">As Jenkins runs more jobs than the configured number of Jenkins executors (default 2), multiple container instances are created.</span></span>

   ![Newly created container instances](./media/container-instances-jenkins/jenkins-aci-multi.png)

4. <span data-ttu-id="dc256-181">After all build jobs have finished, the container instances are removed.</span><span class="sxs-lookup"><span data-stu-id="dc256-181">After all build jobs have finished, the container instances are removed.</span></span>

   ![Resource group with container instances removed](./media/container-instances-jenkins/jenkins-aci-none.png)

## <a name="troubleshooting-the-jenkins-plugin"></a><span data-ttu-id="dc256-183">Troubleshooting the Jenkins plugin</span><span class="sxs-lookup"><span data-stu-id="dc256-183">Troubleshooting the Jenkins plugin</span></span>

<span data-ttu-id="dc256-184">If you encounter any bugs with the Jenkins plugins, file an issue in the [Jenkins JIRA](https://issues.jenkins-ci.org/) for the specific component.</span><span class="sxs-lookup"><span data-stu-id="dc256-184">If you encounter any bugs with the Jenkins plugins, file an issue in the [Jenkins JIRA](https://issues.jenkins-ci.org/) for the specific component.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc256-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="dc256-185">Next steps</span></span>

<span data-ttu-id="dc256-186">To learn more about Jenkins on Azure, see [Azure and Jenkins][jenkins-azure].</span><span class="sxs-lookup"><span data-stu-id="dc256-186">To learn more about Jenkins on Azure, see [Azure and Jenkins][jenkins-azure].</span></span>

<!-- LINKS - internal -->
[about-aci]: ./container-instances-overview.md
[jenkins-azure]: ../jenkins/overview.md
[managed-service-identity]: ../active-directory/managed-service-identity/overview.md