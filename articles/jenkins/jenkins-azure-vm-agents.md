---
title: Scale Jenkins deployments with Azure VM agents.
description: Add additional capacity to your Jenkins pipelines using Azure virtual machines with the Jenkins Azure VM Agent plug-in.
ms.service: jenkins
keywords: jenkins, azure, devops, virtual machine, agents
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.topic: tutorial
ms.date: 07/31/2018
ms.openlocfilehash: c11991aa0d487292eb044fde8436540fe2f34f9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855823"
---
# <a name="scale-your-jenkins-deployments-to-meet-demand-with-azure-vm-agents"></a><span data-ttu-id="a7f0d-104">Scale your Jenkins deployments to meet demand with Azure VM agents</span><span class="sxs-lookup"><span data-stu-id="a7f0d-104">Scale your Jenkins deployments to meet demand with Azure VM agents</span></span>

<span data-ttu-id="a7f0d-105">This tutorial shows how to use the Jenkins [Azure VM Agents plugin](https://plugins.jenkins.io/azure-vm-agents) to add on-demand capacity with Linux virtual machines running in Azure.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-105">This tutorial shows how to use the Jenkins [Azure VM Agents plugin](https://plugins.jenkins.io/azure-vm-agents) to add on-demand capacity with Linux virtual machines running in Azure.</span></span>

<span data-ttu-id="a7f0d-106">In this tutorial, you will:</span><span class="sxs-lookup"><span data-stu-id="a7f0d-106">In this tutorial, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7f0d-107">Install the Azure VM Agents plugin</span><span class="sxs-lookup"><span data-stu-id="a7f0d-107">Install the Azure VM Agents plugin</span></span>
> * <span data-ttu-id="a7f0d-108">Configure the plugin to create resources in your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a7f0d-108">Configure the plugin to create resources in your Azure subscription</span></span>
> * <span data-ttu-id="a7f0d-109">Set the compute resources available to each agent</span><span class="sxs-lookup"><span data-stu-id="a7f0d-109">Set the compute resources available to each agent</span></span>
> * <span data-ttu-id="a7f0d-110">Set the operating system and tools installed on each agent</span><span class="sxs-lookup"><span data-stu-id="a7f0d-110">Set the operating system and tools installed on each agent</span></span>
> * <span data-ttu-id="a7f0d-111">Create a new Jenkins freestyle job</span><span class="sxs-lookup"><span data-stu-id="a7f0d-111">Create a new Jenkins freestyle job</span></span>
> * <span data-ttu-id="a7f0d-112">Run the job on an Azure VM agent</span><span class="sxs-lookup"><span data-stu-id="a7f0d-112">Run the job on an Azure VM agent</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents/player]

## <a name="prerequisites"></a><span data-ttu-id="a7f0d-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a7f0d-113">Prerequisites</span></span>

* <span data-ttu-id="a7f0d-114">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="a7f0d-114">An Azure subscription</span></span>
* <span data-ttu-id="a7f0d-115">A Jenkins master server.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-115">A Jenkins master server.</span></span> <span data-ttu-id="a7f0d-116">If you don't have one, view the [quickstart](install-jenkins-solution-template.md) to set up one in Azure.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-116">If you don't have one, view the [quickstart](install-jenkins-solution-template.md) to set up one in Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="a7f0d-117">Install Azure VM Agents plugin</span><span class="sxs-lookup"><span data-stu-id="a7f0d-117">Install Azure VM Agents plugin</span></span>

> [!TIP]
> <span data-ttu-id="a7f0d-118">If you deployed Jenkins on Azure using the [solution template](install-jenkins-solution-template.md), the Azure VM Agent plugin is already installed.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-118">If you deployed Jenkins on Azure using the [solution template](install-jenkins-solution-template.md), the Azure VM Agent plugin is already installed.</span></span>

1. <span data-ttu-id="a7f0d-119">From the Jenkins dashboard, select **Manage Jenkins**, then select **Manage Plugins**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-119">From the Jenkins dashboard, select **Manage Jenkins**, then select **Manage Plugins**.</span></span>
1. <span data-ttu-id="a7f0d-120">Select the **Available** tab, then search for **Azure VM Agents**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-120">Select the **Available** tab, then search for **Azure VM Agents**.</span></span> <span data-ttu-id="a7f0d-121">Select the checkbox next to the entry for the plugin and select **Install without restart** from the bottom of the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-121">Select the checkbox next to the entry for the plugin and select **Install without restart** from the bottom of the dashboard.</span></span>

## <a name="configure-the-azure-vm-agents-plugin"></a><span data-ttu-id="a7f0d-122">Configure the Azure VM Agents plugin</span><span class="sxs-lookup"><span data-stu-id="a7f0d-122">Configure the Azure VM Agents plugin</span></span>

1. <span data-ttu-id="a7f0d-123">From the Jenkins dashboard, select **Manage Jenkins**, then **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-123">From the Jenkins dashboard, select **Manage Jenkins**, then **Configure System**.</span></span>
1. <span data-ttu-id="a7f0d-124">Scroll to the bottom of the page and find the **Cloud** section with the  **Add new cloud** dropdown and choose **Microsoft Azure VM Agents**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-124">Scroll to the bottom of the page and find the **Cloud** section with the  **Add new cloud** dropdown and choose **Microsoft Azure VM Agents**.</span></span>
1. <span data-ttu-id="a7f0d-125">Select an existing service principal from **Add** drop-down in the **Azure Credentials** section.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-125">Select an existing service principal from **Add** drop-down in the **Azure Credentials** section.</span></span> <span data-ttu-id="a7f0d-126">If none is listed, perform the following steps to [create a service principal](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager) for your Azure account and add it to your Jenkins configuration:</span><span class="sxs-lookup"><span data-stu-id="a7f0d-126">If none is listed, perform the following steps to [create a service principal](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager) for your Azure account and add it to your Jenkins configuration:</span></span>   

    <span data-ttu-id="a7f0d-127">a.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-127">a.</span></span> <span data-ttu-id="a7f0d-128">Select **Add** next to **Azure Credentials** and choose **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-128">Select **Add** next to **Azure Credentials** and choose **Jenkins**.</span></span>   
    <span data-ttu-id="a7f0d-129">b.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-129">b.</span></span> <span data-ttu-id="a7f0d-130">In the **Add Credentials** dialog, select **Microsoft Azure Service Principal** from the **Kind** drop-down.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-130">In the **Add Credentials** dialog, select **Microsoft Azure Service Principal** from the **Kind** drop-down.</span></span>   
    <span data-ttu-id="a7f0d-131">c.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-131">c.</span></span> <span data-ttu-id="a7f0d-132">Create an Active Directory Service principal from the Azure CLI or [Cloud Shell](/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="a7f0d-132">Create an Active Directory Service principal from the Azure CLI or [Cloud Shell](/azure/cloud-shell/overview).</span></span>
    
    ```azurecli-interactive
    az ad sp create-for-rbac --name jenkins_sp --password secure_password
    ```

    ```json
    {
        "appId": "BBBBBBBB-BBBB-BBBB-BBBB-BBBBBBBBBBB",
        "displayName": "jenkins_sp",
        "name": "http://jenkins_sp",
        "password": "secure_password",
        "tenant": "CCCCCCCC-CCCC-CCCC-CCCCCCCCCCC"
    }
    ```
    <span data-ttu-id="a7f0d-133">d.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-133">d.</span></span> <span data-ttu-id="a7f0d-134">Enter the credentials from the service principal into the **Add credentials** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-134">Enter the credentials from the service principal into the **Add credentials** dialog.</span></span> <span data-ttu-id="a7f0d-135">If you don't know your Azure subscription ID, you can query it from the CLI:</span><span class="sxs-lookup"><span data-stu-id="a7f0d-135">If you don't know your Azure subscription ID, you can query it from the CLI:</span></span>
     
     ```azurecli-interactive
     az account list
     ```

     ```json
        {
            "cloudName": "AzureCloud",
            "id": "AAAAAAAA-AAAA-AAAA-AAAA-AAAAAAAAAAAA",
            "isDefault": true,
            "name": "Visual Studio Enterprise",
            "state": "Enabled",
            "tenantId": "CCCCCCCC-CCCC-CCCC-CCCC-CCCCCCCCCCC",
            "user": {
            "name": "raisa@fabrikam.com",
            "type": "user"
            }
     ```

    <span data-ttu-id="a7f0d-136">The completed service principal should use the `id` field for **Subscription ID**, the `appId` value for **Client ID**, `password` for **Client Secret**, and `tenant` for **Tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-136">The completed service principal should use the `id` field for **Subscription ID**, the `appId` value for **Client ID**, `password` for **Client Secret**, and `tenant` for **Tenant ID**.</span></span> <span data-ttu-id="a7f0d-137">Select **Add** to add the service principal and then configure the plugin to use the newly created credential.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-137">Select **Add** to add the service principal and then configure the plugin to use the newly created credential.</span></span>

    ![Configure Azure Service Principal](./media/jenkins-azure-vm-agents/new-service-principal.png)

    

1. <span data-ttu-id="a7f0d-139">In the **Resource Group Name** section, leave **Create new** selected and enter `myJenkinsAgentGroup`.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-139">In the **Resource Group Name** section, leave **Create new** selected and enter `myJenkinsAgentGroup`.</span></span>
1. <span data-ttu-id="a7f0d-140">Select **Verify configuration** to connect to Azure to test the profile settings.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-140">Select **Verify configuration** to connect to Azure to test the profile settings.</span></span>
1. <span data-ttu-id="a7f0d-141">Select **Apply** to update the plugin configuration.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-141">Select **Apply** to update the plugin configuration.</span></span>

## <a name="configure-agent-resources"></a><span data-ttu-id="a7f0d-142">Configure agent resources</span><span class="sxs-lookup"><span data-stu-id="a7f0d-142">Configure agent resources</span></span>

<span data-ttu-id="a7f0d-143">Configure a template for use to define an Azure VM agent.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-143">Configure a template for use to define an Azure VM agent.</span></span> <span data-ttu-id="a7f0d-144">This template defines the compute resources each agent has when created.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-144">This template defines the compute resources each agent has when created.</span></span>

1. <span data-ttu-id="a7f0d-145">Select **Add** next to **Add Azure Virtual Machine Template**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-145">Select **Add** next to **Add Azure Virtual Machine Template**.</span></span>
1. <span data-ttu-id="a7f0d-146">Enter `defaulttemplate` for the **Name**</span><span class="sxs-lookup"><span data-stu-id="a7f0d-146">Enter `defaulttemplate` for the **Name**</span></span>
1. <span data-ttu-id="a7f0d-147">Enter `ubuntu` for the **Label**</span><span class="sxs-lookup"><span data-stu-id="a7f0d-147">Enter `ubuntu` for the **Label**</span></span>
1. <span data-ttu-id="a7f0d-148">Select the desired [Azure region](https://azure.microsoft.com/regions/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) from the combo box.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-148">Select the desired [Azure region](https://azure.microsoft.com/regions/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) from the combo box.</span></span>
1. <span data-ttu-id="a7f0d-149">Select a [VM size](/azure/virtual-machines/linux/sizes) from the drop-down under **Virtual Machine Size**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-149">Select a [VM size](/azure/virtual-machines/linux/sizes) from the drop-down under **Virtual Machine Size**.</span></span> <span data-ttu-id="a7f0d-150">A general-purpose `Standard_DS1_v2` size is fine for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-150">A general-purpose `Standard_DS1_v2` size is fine for this tutorial.</span></span>   
1. <span data-ttu-id="a7f0d-151">Leave the **Retention time** at `60`.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-151">Leave the **Retention time** at `60`.</span></span> <span data-ttu-id="a7f0d-152">This setting defines the number of minutes Jenkins can wait before it deallocated idle agents.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-152">This setting defines the number of minutes Jenkins can wait before it deallocated idle agents.</span></span> <span data-ttu-id="a7f0d-153">Specify 0 if you do not want idle agents to be removed automatically.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-153">Specify 0 if you do not want idle agents to be removed automatically.</span></span>

   ![General VM configuration](./media/jenkins-azure-vm-agents/general-config.png)

## <a name="configure-agent-operating-system-and-tools"></a><span data-ttu-id="a7f0d-155">Configure agent operating system and tools</span><span class="sxs-lookup"><span data-stu-id="a7f0d-155">Configure agent operating system and tools</span></span>

<span data-ttu-id="a7f0d-156">In the **Image Configuration** section of the plugin configuration, select **Ubuntu 16.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-156">In the **Image Configuration** section of the plugin configuration, select **Ubuntu 16.04 LTS**.</span></span> <span data-ttu-id="a7f0d-157">Check the boxes next to **Install Git (Latest)**, **Install Maven (V3.5.0)**, and **Install Docker** to install these tools on newly created agents.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-157">Check the boxes next to **Install Git (Latest)**, **Install Maven (V3.5.0)**, and **Install Docker** to install these tools on newly created agents.</span></span>

![Configure VM OS and tools](./media/jenkins-azure-vm-agents/jenkins-os-config.png)

<span data-ttu-id="a7f0d-159">Select **Add** next to **Admin Credentials**, then select **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-159">Select **Add** next to **Admin Credentials**, then select **Jenkins**.</span></span> <span data-ttu-id="a7f0d-160">Enter a username and password used to sign in to the agents, making sure they satisfy the [username and password policy](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm) for administrative accounts on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-160">Enter a username and password used to sign in to the agents, making sure they satisfy the [username and password policy](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm) for administrative accounts on Azure VMs.</span></span>

<span data-ttu-id="a7f0d-161">Select **Verify Template** to verify the configuration and then select **Save** to save your changes and return to the Jenkins dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-161">Select **Verify Template** to verify the configuration and then select **Save** to save your changes and return to the Jenkins dashboard.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="a7f0d-162">Create a job in Jenkins</span><span class="sxs-lookup"><span data-stu-id="a7f0d-162">Create a job in Jenkins</span></span>

1. <span data-ttu-id="a7f0d-163">Within the Jenkins dashboard, click **New Item**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-163">Within the Jenkins dashboard, click **New Item**.</span></span> 
1. <span data-ttu-id="a7f0d-164">Enter `demoproject1` for the name and select **Freestyle project**, then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-164">Enter `demoproject1` for the name and select **Freestyle project**, then select **OK**.</span></span>
1. <span data-ttu-id="a7f0d-165">In the **General** tab, choose **Restrict where project can be run** and type `ubuntu` in **Label Expression**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-165">In the **General** tab, choose **Restrict where project can be run** and type `ubuntu` in **Label Expression**.</span></span> <span data-ttu-id="a7f0d-166">You see a message confirming that the label is served by the cloud configuration created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-166">You see a message confirming that the label is served by the cloud configuration created in the previous step.</span></span> 
   <span data-ttu-id="a7f0d-167">![Set up job](./media/jenkins-azure-vm-agents/job-config.png)</span><span class="sxs-lookup"><span data-stu-id="a7f0d-167">![Set up job](./media/jenkins-azure-vm-agents/job-config.png)</span></span>
1. <span data-ttu-id="a7f0d-168">In the **Source Code Management** tab, select **Git** and add the following URL into the **Repository URL** field: `https://github.com/spring-projects/spring-petclinic.git`</span><span class="sxs-lookup"><span data-stu-id="a7f0d-168">In the **Source Code Management** tab, select **Git** and add the following URL into the **Repository URL** field: `https://github.com/spring-projects/spring-petclinic.git`</span></span>
1. <span data-ttu-id="a7f0d-169">In the **Build** tab, select **Add build step**, then **Invoke top-level Maven targets**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-169">In the **Build** tab, select **Add build step**, then **Invoke top-level Maven targets**.</span></span> <span data-ttu-id="a7f0d-170">Enter `package` in the **Goals** field.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-170">Enter `package` in the **Goals** field.</span></span>
1. <span data-ttu-id="a7f0d-171">Select **Save** to save the job definition.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-171">Select **Save** to save the job definition.</span></span>

## <a name="build-the-new-job-on-an-azure-vm-agent"></a><span data-ttu-id="a7f0d-172">Build the new job on an Azure VM agent</span><span class="sxs-lookup"><span data-stu-id="a7f0d-172">Build the new job on an Azure VM agent</span></span>

1. <span data-ttu-id="a7f0d-173">Go back to the Jenkins dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-173">Go back to the Jenkins dashboard.</span></span>
1. <span data-ttu-id="a7f0d-174">Select the job you created in the previous step, then click **Build now**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-174">Select the job you created in the previous step, then click **Build now**.</span></span> <span data-ttu-id="a7f0d-175">A new build is queued, but does not start until an agent VM is created in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-175">A new build is queued, but does not start until an agent VM is created in your Azure subscription.</span></span>
1. <span data-ttu-id="a7f0d-176">Once the build is complete, go to **Console output**.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-176">Once the build is complete, go to **Console output**.</span></span> <span data-ttu-id="a7f0d-177">You see that the build was performed remotely on an Azure agent.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-177">You see that the build was performed remotely on an Azure agent.</span></span>

![Console output](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="troubleshooting-the-jenkins-plugin"></a><span data-ttu-id="a7f0d-179">Troubleshooting the Jenkins plugin</span><span class="sxs-lookup"><span data-stu-id="a7f0d-179">Troubleshooting the Jenkins plugin</span></span>

<span data-ttu-id="a7f0d-180">If you encounter any bugs with the Jenkins plugins, file an issue in the [Jenkins JIRA](https://issues.jenkins-ci.org/) for the specific component.</span><span class="sxs-lookup"><span data-stu-id="a7f0d-180">If you encounter any bugs with the Jenkins plugins, file an issue in the [Jenkins JIRA](https://issues.jenkins-ci.org/) for the specific component.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7f0d-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7f0d-181">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7f0d-182">CI/CD to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a7f0d-182">CI/CD to Azure App Service</span></span>](java-deploy-webapp-tutorial.md)