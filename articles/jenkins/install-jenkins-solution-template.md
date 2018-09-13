---
title: Create a Jenkins server on Azure
description: Install Jenkins on an Azure Linux virtual machine from the Jenkins solution template and build a sample Java application.
ms.service: jenkins
keywords: jenkins, azure, devops, portal, virtual machine, solution template
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.topic: quickstart
ms.date: 6/7/2017
ms.openlocfilehash: 79132f23755f045b0a38ed932d91a41285daeea4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866478"
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-the-azure-portal"></a><span data-ttu-id="8cc3b-104">Create a Jenkins server on an Azure Linux VM from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8cc3b-104">Create a Jenkins server on an Azure Linux VM from the Azure portal</span></span>

<span data-ttu-id="8cc3b-105">This quickstart shows how to install [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with the tools and plug-ins configured to work with Azure.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-105">This quickstart shows how to install [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with the tools and plug-ins configured to work with Azure.</span></span> <span data-ttu-id="8cc3b-106">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="8cc3b-106">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cc3b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8cc3b-107">Prerequisites</span></span>

* <span data-ttu-id="8cc3b-108">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="8cc3b-108">An Azure subscription</span></span>
* <span data-ttu-id="8cc3b-109">Access to SSH on your computer's command line (such as the Bash shell or [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="8cc3b-109">Access to SSH on your computer's command line (such as the Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-jenkins-vm-from-the-solution-template"></a><span data-ttu-id="8cc3b-110">Create the Jenkins VM from the solution template</span><span class="sxs-lookup"><span data-stu-id="8cc3b-110">Create the Jenkins VM from the solution template</span></span>
<span data-ttu-id="8cc3b-111">Jenkins supports a model where the Jenkins server delegates work to one or more agents to allow a single Jenkins installation to host a large number of projects or to provide different environments needed for builds or tests.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-111">Jenkins supports a model where the Jenkins server delegates work to one or more agents to allow a single Jenkins installation to host a large number of projects or to provide different environments needed for builds or tests.</span></span> <span data-ttu-id="8cc3b-112">The steps in this section guide you through installing and configuring a Jenkins server on Azure.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-112">The steps in this section guide you through installing and configuring a Jenkins server on Azure.</span></span>

[!INCLUDE [jenkins-install-from-azure-marketplace-image](../../includes/jenkins-install-from-azure-marketplace-image.md)]

## <a name="connect-to-jenkins"></a><span data-ttu-id="8cc3b-113">Connect to Jenkins</span><span class="sxs-lookup"><span data-stu-id="8cc3b-113">Connect to Jenkins</span></span>

<span data-ttu-id="8cc3b-114">Navigate to your virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-114">Navigate to your virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="8cc3b-115">The Jenkins console is inaccessible through unsecured HTTP so instructions are provided on the page to access the Jenkins console securely from your computer using an SSH tunnel.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-115">The Jenkins console is inaccessible through unsecured HTTP so instructions are provided on the page to access the Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Unlock jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="8cc3b-117">Set up the tunnel using the `ssh` command on the page from the command line, replacing `username` with the name of the virtual machine admin user chosen earlier when setting up the virtual machine from the solution template.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-117">Set up the tunnel using the `ssh` command on the page from the command line, replacing `username` with the name of the virtual machine admin user chosen earlier when setting up the virtual machine from the solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="8cc3b-118">After you have started the tunnel, navigate to http://localhost:8080/ on your local machine.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-118">After you have started the tunnel, navigate to http://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="8cc3b-119">Get the initial password by running the following command in the command line while connected through SSH to the Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-119">Get the initial password by running the following command in the command line while connected through SSH to the Jenkins VM.</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="8cc3b-120">Unlock the Jenkins dashboard for the first time using this initial password.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-120">Unlock the Jenkins dashboard for the first time using this initial password.</span></span>

![Unlock jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="8cc3b-122">Select **Install suggested plugins** on the next page and then create a Jenkins admin user used to access the Jenkins dashboard.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-122">Select **Install suggested plugins** on the next page and then create a Jenkins admin user used to access the Jenkins dashboard.</span></span>

![Jenkins is ready!](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="8cc3b-124">The Jenkins server is now ready to build code.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-124">The Jenkins server is now ready to build code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="8cc3b-125">Create your first job</span><span class="sxs-lookup"><span data-stu-id="8cc3b-125">Create your first job</span></span>

<span data-ttu-id="8cc3b-126">Select **Create new jobs** from the Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-126">Select **Create new jobs** from the Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Create a new job](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="8cc3b-128">Select the **Source Code Management** tab, enable **Git**, and enter the following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="8cc3b-128">Select the **Source Code Management** tab, enable **Git**, and enter the following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Define the Git repo](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="8cc3b-130">Select the **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-130">Select the **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="8cc3b-131">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-131">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Use the Gradle wrapper to build](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="8cc3b-133">Select **Advanced** and then enter `complete` in the **Root Build script** field.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-133">Select **Advanced** and then enter `complete` in the **Root Build script** field.</span></span> <span data-ttu-id="8cc3b-134">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-134">Select **Save**.</span></span>

![Set advanced settings in the Gradle wrapper build step](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-the-code"></a><span data-ttu-id="8cc3b-136">Build the code</span><span class="sxs-lookup"><span data-stu-id="8cc3b-136">Build the code</span></span>

<span data-ttu-id="8cc3b-137">Select **Build Now** to compile the code and package the sample app.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-137">Select **Build Now** to compile the code and package the sample app.</span></span> <span data-ttu-id="8cc3b-138">When your build completes, select the **Workspace** link for the project.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-138">When your build completes, select the **Workspace** link for the project.</span></span>

![Browse to the workspace to get the JAR file from the build](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="8cc3b-140">Navigate to `complete/build/libs` and ensure the `gs-spring-boot-0.1.0.jar` is there to verify that your build was successful.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-140">Navigate to `complete/build/libs` and ensure the `gs-spring-boot-0.1.0.jar` is there to verify that your build was successful.</span></span> <span data-ttu-id="8cc3b-141">Your Jenkins server is now ready to build your own projects in Azure.</span><span class="sxs-lookup"><span data-stu-id="8cc3b-141">Your Jenkins server is now ready to build your own projects in Azure.</span></span>

## <a name="troubleshooting-the-jenkins-solution-template"></a><span data-ttu-id="8cc3b-142">Troubleshooting the Jenkins solution template</span><span class="sxs-lookup"><span data-stu-id="8cc3b-142">Troubleshooting the Jenkins solution template</span></span>

<span data-ttu-id="8cc3b-143">If you encounter any bugs with the Jenkins solution template, file an issue in the [Jenkins GitHub repo](https://github.com/azure/jenkins/issues).</span><span class="sxs-lookup"><span data-stu-id="8cc3b-143">If you encounter any bugs with the Jenkins solution template, file an issue in the [Jenkins GitHub repo](https://github.com/azure/jenkins/issues).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cc3b-144">Next Steps</span><span class="sxs-lookup"><span data-stu-id="8cc3b-144">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8cc3b-145">Add Azure VMs as Jenkins agents</span><span class="sxs-lookup"><span data-stu-id="8cc3b-145">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
