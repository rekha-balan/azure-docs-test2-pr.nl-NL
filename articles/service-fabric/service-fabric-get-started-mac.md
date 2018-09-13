---
title: Set up your development environment on Mac OS X | Microsoft Docs
description: Install the runtime, SDK, and tools and create a local development cluster. After completing this setup, you will be ready to build applications on Mac OS X.
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: ''
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/06/2017
ms.author: saysa
ms.openlocfilehash: bc24c1cb8ed47224615828f4a0ee3e849a29b1df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548767"
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="04321-104">Set up your development environment on Mac OS X</span><span class="sxs-lookup"><span data-stu-id="04321-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="04321-108">You can build Service Fabric applications to run on Linux clusters using Mac OS X. This article covers how to set up your Mac for development.</span><span class="sxs-lookup"><span data-stu-id="04321-108">You can build Service Fabric applications to run on Linux clusters using Mac OS X. This article covers how to set up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04321-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="04321-109">Prerequisites</span></span>
<span data-ttu-id="04321-110">Service Fabric does not run natively on OS X. To run a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="04321-110">Service Fabric does not run natively on OS X. To run a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="04321-111">Before you get started, you need:</span><span class="sxs-lookup"><span data-stu-id="04321-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="04321-112">Vagrant (v1.8.4 or later)</span><span class="sxs-lookup"><span data-stu-id="04321-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="04321-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="04321-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> You need to use mutually supported versions of Vagrant and VirtualBox. Vagrant might behave erratically on an unsupported VirtualBox version.
>

## <a name="create-the-local-vm"></a><span data-ttu-id="04321-116">Create the local VM</span><span class="sxs-lookup"><span data-stu-id="04321-116">Create the local VM</span></span>
<span data-ttu-id="04321-117">To create the local VM containing a 5-node Service Fabric cluster, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="04321-117">To create the local VM containing a 5-node Service Fabric cluster, perform the following steps:</span></span>

1. <span data-ttu-id="04321-118">Clone the `Vagrantfile` repo</span><span class="sxs-lookup"><span data-stu-id="04321-118">Clone the `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="04321-119">This steps bring downs the file `Vagrantfile` containing the VM configuration along with the location the VM is downloaded from.</span><span class="sxs-lookup"><span data-stu-id="04321-119">This steps bring downs the file `Vagrantfile` containing the VM configuration along with the location the VM is downloaded from.</span></span>


2. <span data-ttu-id="04321-120">Navigate to the local clone of the repo</span><span class="sxs-lookup"><span data-stu-id="04321-120">Navigate to the local clone of the repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="04321-121">(Optional) Modify the default VM settings</span><span class="sxs-lookup"><span data-stu-id="04321-121">(Optional) Modify the default VM settings</span></span>

    <span data-ttu-id="04321-122">By default, the local VM is configured as follows:</span><span class="sxs-lookup"><span data-stu-id="04321-122">By default, the local VM is configured as follows:</span></span>

   * <span data-ttu-id="04321-123">3 GB of memory allocated</span><span class="sxs-lookup"><span data-stu-id="04321-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="04321-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from the Mac host</span><span class="sxs-lookup"><span data-stu-id="04321-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from the Mac host</span></span>

     <span data-ttu-id="04321-125">You can change either of these settings or add other configuration to the VM in the `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="04321-125">You can change either of these settings or add other configuration to the VM in the `Vagrantfile`.</span></span> <span data-ttu-id="04321-126">See the [Vagrant documentation](http://www.vagrantup.com/docs) for the full list of configuration options.</span><span class="sxs-lookup"><span data-stu-id="04321-126">See the [Vagrant documentation](http://www.vagrantup.com/docs) for the full list of configuration options.</span></span>
4. <span data-ttu-id="04321-127">Create the VM</span><span class="sxs-lookup"><span data-stu-id="04321-127">Create the VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="04321-128">This step downloads the preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span><span class="sxs-lookup"><span data-stu-id="04321-128">This step downloads the preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="04321-129">You should expect it to take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="04321-129">You should expect it to take a few minutes.</span></span> <span data-ttu-id="04321-130">If setup completes successfully, you see a message in the output indicating that the cluster is starting up.</span><span class="sxs-lookup"><span data-stu-id="04321-130">If setup completes successfully, you see a message in the output indicating that the cluster is starting up.</span></span>

    ![Cluster setup starting following VM provisioning][cluster-setup-script]

>[!TIP]
> If the VM download is taking a long time, you can download it using wget or curl or through a browser by navigating to the link specified by **config.vm.box_url** in the file `Vagrantfile`. After downloading it locally, edit `Vagrantfile` to point to the local path where you downloaded the image. For example if you downloaded the image to /home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** to that path.
>

5. <span data-ttu-id="04321-135">Test that the cluster has been set up correctly by navigating to Service Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept the default private network IP).</span><span class="sxs-lookup"><span data-stu-id="04321-135">Test that the cluster has been set up correctly by navigating to Service Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept the default private network IP).</span></span>

    ![Service Fabric Explorer viewed from the host Mac][sfx-mac]

## <a name="install-the-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="04321-137">Install the Service Fabric plugin for Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="04321-137">Install the Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="04321-138">Service Fabric provides a plugin for the **Eclipse Neon for Java IDE** that can simplify the process of creating, building, and deploying Java services.</span><span class="sxs-lookup"><span data-stu-id="04321-138">Service Fabric provides a plugin for the **Eclipse Neon for Java IDE** that can simplify the process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="04321-139">You can follow the installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span><span class="sxs-lookup"><span data-stu-id="04321-139">You can follow the installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

## <a name="using-service-fabric-eclipse-plugin-on-mac"></a><span data-ttu-id="04321-140">Using Service Fabric Eclipse plugin on Mac</span><span class="sxs-lookup"><span data-stu-id="04321-140">Using Service Fabric Eclipse plugin on Mac</span></span>

<span data-ttu-id="04321-141">Ensure you have gone through the steps mentioned in the [Service Fabric Eclipse plugin documentation](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="04321-141">Ensure you have gone through the steps mentioned in the [Service Fabric Eclipse plugin documentation](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="04321-142">The steps for creating, building, and deploying Service Fabric Java application using vagrant-guest container on a Mac host, is mostly same as the general documentation, apart from the following items:</span><span class="sxs-lookup"><span data-stu-id="04321-142">The steps for creating, building, and deploying Service Fabric Java application using vagrant-guest container on a Mac host, is mostly same as the general documentation, apart from the following items:</span></span>

* <span data-ttu-id="04321-143">Since the Service Fabric libraries are required by your Service Fabric Java application, the eclipse project needs to be created in a shared path.</span><span class="sxs-lookup"><span data-stu-id="04321-143">Since the Service Fabric libraries are required by your Service Fabric Java application, the eclipse project needs to be created in a shared path.</span></span> <span data-ttu-id="04321-144">By default, the contents at the path on your host where the ``Vagrantfile`` exists, is shared with the ``/vagrant`` path on the guest.</span><span class="sxs-lookup"><span data-stu-id="04321-144">By default, the contents at the path on your host where the ``Vagrantfile`` exists, is shared with the ``/vagrant`` path on the guest.</span></span>
* <span data-ttu-id="04321-145">If you have the ``Vagrantfile`` in a path, say, ``~/home/john/allprojects/``, then you need to create your Service Fabric project ``MyActor`` in location ``~/home/john/allprojects/MyActor`` and the path to your eclipse workspace would be ``~/home/john/allprojects``.</span><span class="sxs-lookup"><span data-stu-id="04321-145">If you have the ``Vagrantfile`` in a path, say, ``~/home/john/allprojects/``, then you need to create your Service Fabric project ``MyActor`` in location ``~/home/john/allprojects/MyActor`` and the path to your eclipse workspace would be ``~/home/john/allprojects``.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04321-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="04321-146">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="04321-147">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span><span class="sxs-lookup"><span data-stu-id="04321-147">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="04321-148">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span><span class="sxs-lookup"><span data-stu-id="04321-148">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="04321-149">Create a Service Fabric cluster in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="04321-149">Create a Service Fabric cluster in the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="04321-150">Create a Service Fabric cluster using the Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="04321-150">Create a Service Fabric cluster using the Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="04321-151">Understand the Service Fabric application model</span><span class="sxs-lookup"><span data-stu-id="04321-151">Understand the Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship



