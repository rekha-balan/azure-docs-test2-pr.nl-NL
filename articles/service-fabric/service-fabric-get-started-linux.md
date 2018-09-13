---
title: Set up your development environment on Linux | Microsoft Docs
description: Install the runtime and SDK and create a local development cluster on Linux. After completing this setup, you will be ready to build applications.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/23/2017
ms.author: subramar
ms.openlocfilehash: e3431fe327ede5f736de3e64d0d9819e684a9512
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551135"
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="3858b-104">Prepare your development environment on Linux</span><span class="sxs-lookup"><span data-stu-id="3858b-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

 <span data-ttu-id="3858b-108">To deploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install the runtime and common SDK.</span><span class="sxs-lookup"><span data-stu-id="3858b-108">To deploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install the runtime and common SDK.</span></span> <span data-ttu-id="3858b-109">You can also install optional SDKs for Java and .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3858b-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3858b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3858b-110">Prerequisites</span></span>

### <a name="supported-operating-system-versions"></a><span data-ttu-id="3858b-111">Supported operating system versions</span><span class="sxs-lookup"><span data-stu-id="3858b-111">Supported operating system versions</span></span>
<span data-ttu-id="3858b-112">The following operating system versions are supported for development:</span><span class="sxs-lookup"><span data-stu-id="3858b-112">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="3858b-113">Ubuntu 16.04 (i **"Xenial Xerus"**)</span><span class="sxs-lookup"><span data-stu-id="3858b-113">Ubuntu 16.04 (i **"Xenial Xerus"**)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="3858b-114">Update your apt sources</span><span class="sxs-lookup"><span data-stu-id="3858b-114">Update your apt sources</span></span>
<span data-ttu-id="3858b-115">To install the SDK and the associated runtime package via apt-get, you must first update your apt sources.</span><span class="sxs-lookup"><span data-stu-id="3858b-115">To install the SDK and the associated runtime package via apt-get, you must first update your apt sources.</span></span>

1. <span data-ttu-id="3858b-116">Open a terminal.</span><span class="sxs-lookup"><span data-stu-id="3858b-116">Open a terminal.</span></span>
2. <span data-ttu-id="3858b-117">Add the Service Fabric repo to your sources list.</span><span class="sxs-lookup"><span data-stu-id="3858b-117">Add the Service Fabric repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ trusty main" > /etc/apt/sources.list.d/servicefabric.list'
    ```
3. <span data-ttu-id="3858b-118">Add the **dotnet** repo to your sources list.</span><span class="sxs-lookup"><span data-stu-id="3858b-118">Add the **dotnet** repo to your sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```
4. <span data-ttu-id="3858b-119">Add the new GPG key to your apt keyring.</span><span class="sxs-lookup"><span data-stu-id="3858b-119">Add the new GPG key to your apt keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    ```
    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="3858b-120">Refresh your package lists based on the newly added repositories.</span><span class="sxs-lookup"><span data-stu-id="3858b-120">Refresh your package lists based on the newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```
## <a name="install-and-set-up-the-sdk-for-containers-and-guest-executables"></a><span data-ttu-id="3858b-121">Install and set up the SDK for containers and guest executables</span><span class="sxs-lookup"><span data-stu-id="3858b-121">Install and set up the SDK for containers and guest executables</span></span>
<span data-ttu-id="3858b-122">Once your sources are updated, you can install the SDK.</span><span class="sxs-lookup"><span data-stu-id="3858b-122">Once your sources are updated, you can install the SDK.</span></span>

1. <span data-ttu-id="3858b-123">Install the Service Fabric SDK package.</span><span class="sxs-lookup"><span data-stu-id="3858b-123">Install the Service Fabric SDK package.</span></span> <span data-ttu-id="3858b-124">You are asked to confirm the installation and to agree to a license agreement.</span><span class="sxs-lookup"><span data-stu-id="3858b-124">You are asked to confirm the installation and to agree to a license agreement.</span></span>

    ```bash
    sudo apt-get install servicefabricsdkcommon
    ```
2. <span data-ttu-id="3858b-125">Run the SDK setup script.</span><span class="sxs-lookup"><span data-stu-id="3858b-125">Run the SDK setup script.</span></span>

    ```bash
    sudo /opt/microsoft/sdk/servicefabric/common/sdkcommonsetup.sh
    ```

<span data-ttu-id="3858b-126">Once you have run the steps to install the Common SDK package, creation of apps with guest executable or container services should be possible by running `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="3858b-126">Once you have run the steps to install the Common SDK package, creation of apps with guest executable or container services should be possible by running `yo azuresfguest`.</span></span> <span data-ttu-id="3858b-127">You may need to set your **$NODE_PATH** environment variable to where the node modules are located.</span><span class="sxs-lookup"><span data-stu-id="3858b-127">You may need to set your **$NODE_PATH** environment variable to where the node modules are located.</span></span> 

    ```bash
    export NODE_PATH=$NODE_PATH:$HOME/.node/lib/node_modules 
    ```

<span data-ttu-id="3858b-128">If you are using the environment as root, you may need to set the variable with the following command:</span><span class="sxs-lookup"><span data-stu-id="3858b-128">If you are using the environment as root, you may need to set the variable with the following command:</span></span>

    ```bash
    export NODE_PATH=$NODE_PATH:/root/.node/lib/node_modules 
    ```

> [!TIP]
> You may want to add these commands into your ~/.bashrc file so that you don't have to set the environment variable at every login.
>

## <a name="set-up-the-azure-cross-platform-cli"></a><span data-ttu-id="3858b-130">Set up the Azure cross-platform CLI</span><span class="sxs-lookup"><span data-stu-id="3858b-130">Set up the Azure cross-platform CLI</span></span>
<span data-ttu-id="3858b-131">The [Azure cross-platform CLI][azure-xplat-cli-github] includes commands for interacting with Service Fabric entities, including clusters and applications.</span><span class="sxs-lookup"><span data-stu-id="3858b-131">The [Azure cross-platform CLI][azure-xplat-cli-github] includes commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="3858b-132">It is based on Node.js so [ensure that you have installed Node][install-node] before proceeding with the following instructions:</span><span class="sxs-lookup"><span data-stu-id="3858b-132">It is based on Node.js so [ensure that you have installed Node][install-node] before proceeding with the following instructions:</span></span>

1. <span data-ttu-id="3858b-133">Clone the github repo to your development machine.</span><span class="sxs-lookup"><span data-stu-id="3858b-133">Clone the github repo to your development machine.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-xplat-cli.git
    ```
2. <span data-ttu-id="3858b-134">Switch into the cloned repo and install the CLI's dependencies using the Node Package Manager (npm).</span><span class="sxs-lookup"><span data-stu-id="3858b-134">Switch into the cloned repo and install the CLI's dependencies using the Node Package Manager (npm).</span></span>

    ```bash
    cd azure-xplat-cli
    npm install
    ```
3. <span data-ttu-id="3858b-135">Create a symlink from the bin/azure folder of the cloned repo to /usr/bin/azure so that it's added to your path and commands are available from any directory.</span><span class="sxs-lookup"><span data-stu-id="3858b-135">Create a symlink from the bin/azure folder of the cloned repo to /usr/bin/azure so that it's added to your path and commands are available from any directory.</span></span>

    ```bash
    sudo ln -s $(pwd)/bin/azure /usr/bin/azure
    ```
4. <span data-ttu-id="3858b-136">Finally, enable auto-completion Service Fabric commands.</span><span class="sxs-lookup"><span data-stu-id="3858b-136">Finally, enable auto-completion Service Fabric commands.</span></span>

    ```bash
    azure --completion >> ~/azure.completion.sh
    echo 'source ~/azure.completion.sh' >> ~/.bash_profile
    source ~/azure.completion.sh
    ```

> [!NOTE]
> Service Fabric commands are not yet available in Azure CLI 2.0.


## <a name="set-up-a-local-cluster"></a><span data-ttu-id="3858b-138">Set up a local cluster</span><span class="sxs-lookup"><span data-stu-id="3858b-138">Set up a local cluster</span></span>
<span data-ttu-id="3858b-139">If everything has installed successfully, you should be able to start a local cluster.</span><span class="sxs-lookup"><span data-stu-id="3858b-139">If everything has installed successfully, you should be able to start a local cluster.</span></span>

1. <span data-ttu-id="3858b-140">Run the cluster setup script.</span><span class="sxs-lookup"><span data-stu-id="3858b-140">Run the cluster setup script.</span></span>

    ```bash
    sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
    ```
2. <span data-ttu-id="3858b-141">Open a web browser and navigate to http://localhost:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="3858b-141">Open a web browser and navigate to http://localhost:19080/Explorer.</span></span> <span data-ttu-id="3858b-142">If the cluster has started, you should see the Service Fabric Explorer dashboard.</span><span class="sxs-lookup"><span data-stu-id="3858b-142">If the cluster has started, you should see the Service Fabric Explorer dashboard.</span></span>

    ![Service Fabric Explorer on Linux][sfx-linux]

<span data-ttu-id="3858b-144">At this point, you are able to deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span><span class="sxs-lookup"><span data-stu-id="3858b-144">At this point, you are able to deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="3858b-145">To build new services using the Java or .NET Core SDKs, follow the optional setup steps provided in subsequent sections.</span><span class="sxs-lookup"><span data-stu-id="3858b-145">To build new services using the Java or .NET Core SDKs, follow the optional setup steps provided in subsequent sections.</span></span>


> [!NOTE]
> Stand alone clusters aren't supported in Linux - only one box and Azure Linux multi-machine clusters are supported in the preview.
>

## <a name="install-the-java-sdk-optional-if-you-wish-to-use-the-java-programming-models"></a><span data-ttu-id="3858b-147">Install the Java SDK (optional, if you wish to use the Java programming models)</span><span class="sxs-lookup"><span data-stu-id="3858b-147">Install the Java SDK (optional, if you wish to use the Java programming models)</span></span>
<span data-ttu-id="3858b-148">The Java SDK provides the libraries and templates required to build Service Fabric services using Java.</span><span class="sxs-lookup"><span data-stu-id="3858b-148">The Java SDK provides the libraries and templates required to build Service Fabric services using Java.</span></span>

1. <span data-ttu-id="3858b-149">Install the Java SDK package.</span><span class="sxs-lookup"><span data-stu-id="3858b-149">Install the Java SDK package.</span></span>

    ```bash
    sudo apt-get install servicefabricsdkjava
    ```
2. <span data-ttu-id="3858b-150">Run the SDK setup script.</span><span class="sxs-lookup"><span data-stu-id="3858b-150">Run the SDK setup script.</span></span>

    ```bash
    sudo /opt/microsoft/sdk/servicefabric/java/sdkjavasetup.sh
    ```
## <a name="install-the-eclipse-neon-plugin-optional"></a><span data-ttu-id="3858b-151">Install the Eclipse Neon plugin (optional)</span><span class="sxs-lookup"><span data-stu-id="3858b-151">Install the Eclipse Neon plugin (optional)</span></span>

<span data-ttu-id="3858b-152">You can install the Eclipse plugin for Service Fabric from within the **Eclipse IDE for Java Developers**.</span><span class="sxs-lookup"><span data-stu-id="3858b-152">You can install the Eclipse plugin for Service Fabric from within the **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="3858b-153">You can use Eclipse to create Service Fabric guest executable applications and container applications in addition to Service Fabric Java applications.</span><span class="sxs-lookup"><span data-stu-id="3858b-153">You can use Eclipse to create Service Fabric guest executable applications and container applications in addition to Service Fabric Java applications.</span></span>

> [!NOTE]
> Installing the Java SDK is a prerequisite to using the Eclipse plugin, even if you only use it to create and deploy guest executables and container applications.
>

1. <span data-ttu-id="3858b-155">In Eclipse, ensure that you have latest eclipse **Neon** and latest Buildship version (1.0.17 or later) installed.</span><span class="sxs-lookup"><span data-stu-id="3858b-155">In Eclipse, ensure that you have latest eclipse **Neon** and latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="3858b-156">You can check the versions of installed components by choosing **Help > Installation Details**.</span><span class="sxs-lookup"><span data-stu-id="3858b-156">You can check the versions of installed components by choosing **Help > Installation Details**.</span></span> <span data-ttu-id="3858b-157">You can update Buildship using the instructions [here][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="3858b-157">You can update Buildship using the instructions [here][buildship-update].</span></span>
2. <span data-ttu-id="3858b-158">To install the Service Fabric plugin, choose **Help > Install New Software...**</span><span class="sxs-lookup"><span data-stu-id="3858b-158">To install the Service Fabric plugin, choose **Help > Install New Software...**</span></span>
3. <span data-ttu-id="3858b-159">In the "Work with" textbox, enter: http://dl.windowsazure.com/eclipse/servicefabric</span><span class="sxs-lookup"><span data-stu-id="3858b-159">In the "Work with" textbox, enter: http://dl.windowsazure.com/eclipse/servicefabric</span></span>
4. <span data-ttu-id="3858b-160">Click Add.</span><span class="sxs-lookup"><span data-stu-id="3858b-160">Click Add.</span></span>
    <span data-ttu-id="3858b-161">![Eclipse plugin][sf-eclipse-plugin]</span><span class="sxs-lookup"><span data-stu-id="3858b-161">![Eclipse plugin][sf-eclipse-plugin]</span></span>
5. <span data-ttu-id="3858b-162">Choose the Service Fabric plugin and click next.</span><span class="sxs-lookup"><span data-stu-id="3858b-162">Choose the Service Fabric plugin and click next.</span></span>
6. <span data-ttu-id="3858b-163">Proceed through the installation and accept the end-user license agreement.</span><span class="sxs-lookup"><span data-stu-id="3858b-163">Proceed through the installation and accept the end-user license agreement.</span></span>

<span data-ttu-id="3858b-164">If you already have the Service Fabric Eclipse plugin installed, make sure you are on the latest version.</span><span class="sxs-lookup"><span data-stu-id="3858b-164">If you already have the Service Fabric Eclipse plugin installed, make sure you are on the latest version.</span></span> <span data-ttu-id="3858b-165">You can check by selecting ``Help => Installation Details`` and searching for Service Fabric in the list of installed plugins.</span><span class="sxs-lookup"><span data-stu-id="3858b-165">You can check by selecting ``Help => Installation Details`` and searching for Service Fabric in the list of installed plugins.</span></span> <span data-ttu-id="3858b-166">Select update if a newer version is available.</span><span class="sxs-lookup"><span data-stu-id="3858b-166">Select update if a newer version is available.</span></span> 

<span data-ttu-id="3858b-167">For more information, see [Service fabric getting started with eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="3858b-167">For more information, see [Service fabric getting started with eclipse](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-the-net-core-sdk-optional-if-you-wish-to-use-the-net-core-programming-models"></a><span data-ttu-id="3858b-168">Install the .NET Core SDK (optional, if you wish to use the .NET Core programming models)</span><span class="sxs-lookup"><span data-stu-id="3858b-168">Install the .NET Core SDK (optional, if you wish to use the .NET Core programming models)</span></span>
<span data-ttu-id="3858b-169">The .NET Core SDK provides the libraries and templates required to build Service Fabric services using cross-platform .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3858b-169">The .NET Core SDK provides the libraries and templates required to build Service Fabric services using cross-platform .NET Core.</span></span>

1. <span data-ttu-id="3858b-170">Install the .NET Core SDK package.</span><span class="sxs-lookup"><span data-stu-id="3858b-170">Install the .NET Core SDK package.</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

2. <span data-ttu-id="3858b-171">Run the SDK setup script.</span><span class="sxs-lookup"><span data-stu-id="3858b-171">Run the SDK setup script.</span></span>

   ```bash
   sudo /opt/microsoft/sdk/servicefabric/csharp/sdkcsharpsetup.sh
   ```

## <a name="updating-the-sdk-and-runtime"></a><span data-ttu-id="3858b-172">Updating the SDK and Runtime</span><span class="sxs-lookup"><span data-stu-id="3858b-172">Updating the SDK and Runtime</span></span>

<span data-ttu-id="3858b-173">To update to the latest version of the SDK and runtime, run the following steps (remove SDKs from the list that you don't want to update or install):</span><span class="sxs-lookup"><span data-stu-id="3858b-173">To update to the latest version of the SDK and runtime, run the following steps (remove SDKs from the list that you don't want to update or install):</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp servicefabricsdkjava
   ```

<span data-ttu-id="3858b-174">For updating the CLI, navigate to the directory where you cloned the CLI and run `git pull` for updating.</span><span class="sxs-lookup"><span data-stu-id="3858b-174">For updating the CLI, navigate to the directory where you cloned the CLI and run `git pull` for updating.</span></span>  <span data-ttu-id="3858b-175">If additional steps are needed for updating, the release notes will specify those steps.</span><span class="sxs-lookup"><span data-stu-id="3858b-175">If additional steps are needed for updating, the release notes will specify those steps.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="3858b-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="3858b-176">Next steps</span></span>
* [<span data-ttu-id="3858b-177">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span><span class="sxs-lookup"><span data-stu-id="3858b-177">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="3858b-178">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span><span class="sxs-lookup"><span data-stu-id="3858b-178">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="3858b-179">Create your first CSharp application on Linux</span><span class="sxs-lookup"><span data-stu-id="3858b-179">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="3858b-180">Prepare your development environment on OSX</span><span class="sxs-lookup"><span data-stu-id="3858b-180">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="3858b-181">Use the Azure CLI to manage your Service Fabric applications</span><span class="sxs-lookup"><span data-stu-id="3858b-181">Use the Azure CLI to manage your Service Fabric applications</span></span>](service-fabric-azure-cli.md)
* [<span data-ttu-id="3858b-182">Service Fabric Windows/Linux differences</span><span class="sxs-lookup"><span data-stu-id="3858b-182">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-linux/sfx-linux.png


