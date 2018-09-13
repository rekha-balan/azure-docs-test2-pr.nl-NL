---
title: Use Azure Kubernetes Service with Kafka on HDInsight
description: Learn how to use Kafka on HDInsight from container images hosted in Azure Kubernetes Service (AKS).
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/07/2018
ms.openlocfilehash: 5d855c2747194ccdeb9f5cdbe07e25c96dedc9b6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868282"
---
# <a name="use-azure-kubernetes-service-with-kafka-on-hdinsight"></a><span data-ttu-id="be451-103">Use Azure Kubernetes Service with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="be451-103">Use Azure Kubernetes Service with Kafka on HDInsight</span></span>

<span data-ttu-id="be451-104">Learn how to use Azure Kubernetes Service (AKS) with Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="be451-104">Learn how to use Azure Kubernetes Service (AKS) with Kafka on HDInsight cluster.</span></span> <span data-ttu-id="be451-105">The steps in this document use a Node.js application hosted in AKS to verify connectivity with Kafka.</span><span class="sxs-lookup"><span data-stu-id="be451-105">The steps in this document use a Node.js application hosted in AKS to verify connectivity with Kafka.</span></span> <span data-ttu-id="be451-106">This application uses the [kafka-node](https://www.npmjs.com/package/kafka-node) package to communicate with Kafka.</span><span class="sxs-lookup"><span data-stu-id="be451-106">This application uses the [kafka-node](https://www.npmjs.com/package/kafka-node) package to communicate with Kafka.</span></span> <span data-ttu-id="be451-107">It uses [Socket.io](https://socket.io/) for event driven messaging between the browser client and the back-end hosted in AKS.</span><span class="sxs-lookup"><span data-stu-id="be451-107">It uses [Socket.io](https://socket.io/) for event driven messaging between the browser client and the back-end hosted in AKS.</span></span>

<span data-ttu-id="be451-108">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span><span class="sxs-lookup"><span data-stu-id="be451-108">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="be451-109">Azure Kubernetes Service manages your hosted Kubernetes environment, and makes it quick and easy to deploy containerized applications.</span><span class="sxs-lookup"><span data-stu-id="be451-109">Azure Kubernetes Service manages your hosted Kubernetes environment, and makes it quick and easy to deploy containerized applications.</span></span> <span data-ttu-id="be451-110">Using an Azure Virtual Network, you can connect the two services.</span><span class="sxs-lookup"><span data-stu-id="be451-110">Using an Azure Virtual Network, you can connect the two services.</span></span>

> [!NOTE]
> <span data-ttu-id="be451-111">The focus of this document is on the steps required to enable Azure Kubernetes Service to communicate with Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be451-111">The focus of this document is on the steps required to enable Azure Kubernetes Service to communicate with Kafka on HDInsight.</span></span> <span data-ttu-id="be451-112">The example itself is just a basic Kafka client to demonstrate that the configuration works.</span><span class="sxs-lookup"><span data-stu-id="be451-112">The example itself is just a basic Kafka client to demonstrate that the configuration works.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be451-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="be451-113">Prerequisites</span></span>

* [<span data-ttu-id="be451-114">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be451-114">Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)
* <span data-ttu-id="be451-115">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="be451-115">An Azure subscription</span></span>

<span data-ttu-id="be451-116">This document assumes that you are familiar with creating and using the following Azure services:</span><span class="sxs-lookup"><span data-stu-id="be451-116">This document assumes that you are familiar with creating and using the following Azure services:</span></span>

* <span data-ttu-id="be451-117">Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="be451-117">Kafka on HDInsight</span></span>
* <span data-ttu-id="be451-118">Azure Kubernetes Service</span><span class="sxs-lookup"><span data-stu-id="be451-118">Azure Kubernetes Service</span></span>
* <span data-ttu-id="be451-119">Azure Virtual Networks</span><span class="sxs-lookup"><span data-stu-id="be451-119">Azure Virtual Networks</span></span>

<span data-ttu-id="be451-120">This document also assumes that you have walked through the [Azure Kubernetes Service tutorial](../../aks/tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="be451-120">This document also assumes that you have walked through the [Azure Kubernetes Service tutorial](../../aks/tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="be451-121">This tutorial creates a container service, creates a Kubernetes cluster, a container registry, and configures the `kubectl` utility.</span><span class="sxs-lookup"><span data-stu-id="be451-121">This tutorial creates a container service, creates a Kubernetes cluster, a container registry, and configures the `kubectl` utility.</span></span>

## <a name="architecture"></a><span data-ttu-id="be451-122">Architecture</span><span class="sxs-lookup"><span data-stu-id="be451-122">Architecture</span></span>

### <a name="network-topology"></a><span data-ttu-id="be451-123">Network topology</span><span class="sxs-lookup"><span data-stu-id="be451-123">Network topology</span></span>

<span data-ttu-id="be451-124">Both HDInsight and AKS use an Azure Virtual Network as a container for compute resources.</span><span class="sxs-lookup"><span data-stu-id="be451-124">Both HDInsight and AKS use an Azure Virtual Network as a container for compute resources.</span></span> <span data-ttu-id="be451-125">To enable communication between HDInsight and AKS, you must enable communication between their networks.</span><span class="sxs-lookup"><span data-stu-id="be451-125">To enable communication between HDInsight and AKS, you must enable communication between their networks.</span></span> <span data-ttu-id="be451-126">The steps in this document use Virtual Network Peering to the networks.</span><span class="sxs-lookup"><span data-stu-id="be451-126">The steps in this document use Virtual Network Peering to the networks.</span></span> <span data-ttu-id="be451-127">Other connections, such as VPN, should also work.</span><span class="sxs-lookup"><span data-stu-id="be451-127">Other connections, such as VPN, should also work.</span></span> <span data-ttu-id="be451-128">For more information on peering, see the [Virtual network peering](../../virtual-network/virtual-network-peering-overview.md) document.</span><span class="sxs-lookup"><span data-stu-id="be451-128">For more information on peering, see the [Virtual network peering](../../virtual-network/virtual-network-peering-overview.md) document.</span></span>


<span data-ttu-id="be451-129">The following diagram illustrates the network topology used in this document:</span><span class="sxs-lookup"><span data-stu-id="be451-129">The following diagram illustrates the network topology used in this document:</span></span>

![HDInsight in one virtual network, AKS in another, and the networks connected using peering](./media/apache-kafka-azure-container-services/kafka-aks-architecture.png)

> [!IMPORTANT]
> <span data-ttu-id="be451-131">Name resolution is not enabled between the peered networks, so IP addressing is used.</span><span class="sxs-lookup"><span data-stu-id="be451-131">Name resolution is not enabled between the peered networks, so IP addressing is used.</span></span> <span data-ttu-id="be451-132">By default, Kafka on HDInsight is configured to return host names instead of IP addresses when clients connect.</span><span class="sxs-lookup"><span data-stu-id="be451-132">By default, Kafka on HDInsight is configured to return host names instead of IP addresses when clients connect.</span></span> <span data-ttu-id="be451-133">The steps in this document modify Kafka to use IP advertising instead.</span><span class="sxs-lookup"><span data-stu-id="be451-133">The steps in this document modify Kafka to use IP advertising instead.</span></span>

## <a name="create-an-azure-kubernetes-service-aks"></a><span data-ttu-id="be451-134">Create an Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="be451-134">Create an Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="be451-135">If you do not already have an AKS cluster, use one of the following documents to learn how to create one:</span><span class="sxs-lookup"><span data-stu-id="be451-135">If you do not already have an AKS cluster, use one of the following documents to learn how to create one:</span></span>

* [<span data-ttu-id="be451-136">Deploy an Azure Kubernetes Service (AKS) cluster - Portal</span><span class="sxs-lookup"><span data-stu-id="be451-136">Deploy an Azure Kubernetes Service (AKS) cluster - Portal</span></span>](../../aks/kubernetes-walkthrough-portal.md)
* [<span data-ttu-id="be451-137">Deploy an Azure Kubernetes Service (AKS) cluster - CLI</span><span class="sxs-lookup"><span data-stu-id="be451-137">Deploy an Azure Kubernetes Service (AKS) cluster - CLI</span></span>](../../aks/kubernetes-walkthrough.md)

> [!NOTE]
> <span data-ttu-id="be451-138">AKS creates a virtual network during installation.</span><span class="sxs-lookup"><span data-stu-id="be451-138">AKS creates a virtual network during installation.</span></span> <span data-ttu-id="be451-139">This network is peered to the one created for HDInsight in the next section.</span><span class="sxs-lookup"><span data-stu-id="be451-139">This network is peered to the one created for HDInsight in the next section.</span></span>

## <a name="configure-virtual-network-peering"></a><span data-ttu-id="be451-140">Configure virtual network peering</span><span class="sxs-lookup"><span data-stu-id="be451-140">Configure virtual network peering</span></span>

1. <span data-ttu-id="be451-141">From the [Azure portal](https://portal.azure.com), select __Resource groups__, and then find the resource group that contains the virtual network for your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="be451-141">From the [Azure portal](https://portal.azure.com), select __Resource groups__, and then find the resource group that contains the virtual network for your AKS cluster.</span></span> <span data-ttu-id="be451-142">The resource group name is `MC_<resourcegroup>_<akscluster>_<location>`.</span><span class="sxs-lookup"><span data-stu-id="be451-142">The resource group name is `MC_<resourcegroup>_<akscluster>_<location>`.</span></span> <span data-ttu-id="be451-143">The `resourcegroup` and `akscluster` entries are the name of the resource group you created the cluster in, and the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="be451-143">The `resourcegroup` and `akscluster` entries are the name of the resource group you created the cluster in, and the name of the cluster.</span></span> <span data-ttu-id="be451-144">The `location` is the location that the cluster was created in.</span><span class="sxs-lookup"><span data-stu-id="be451-144">The `location` is the location that the cluster was created in.</span></span>

2. <span data-ttu-id="be451-145">In the resource group, select the __Virtual network__ resource.</span><span class="sxs-lookup"><span data-stu-id="be451-145">In the resource group, select the __Virtual network__ resource.</span></span>

3. <span data-ttu-id="be451-146">Select __Address space__.</span><span class="sxs-lookup"><span data-stu-id="be451-146">Select __Address space__.</span></span> <span data-ttu-id="be451-147">Note the address space listed.</span><span class="sxs-lookup"><span data-stu-id="be451-147">Note the address space listed.</span></span>

4. <span data-ttu-id="be451-148">To create a virtual network for HDInsight, select __+ Create a resource__, __Networking__, and then __Virtual network__.</span><span class="sxs-lookup"><span data-stu-id="be451-148">To create a virtual network for HDInsight, select __+ Create a resource__, __Networking__, and then __Virtual network__.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="be451-149">When entering the values for the new virtual network, you must use an address space that does not overlap the one used by the AKS cluster network.</span><span class="sxs-lookup"><span data-stu-id="be451-149">When entering the values for the new virtual network, you must use an address space that does not overlap the one used by the AKS cluster network.</span></span>

    <span data-ttu-id="be451-150">Use the same __Location__ for the virtual network that you used for the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="be451-150">Use the same __Location__ for the virtual network that you used for the AKS cluster.</span></span>

    <span data-ttu-id="be451-151">Wait until the virtual network has been created before going to the next step.</span><span class="sxs-lookup"><span data-stu-id="be451-151">Wait until the virtual network has been created before going to the next step.</span></span>

5. <span data-ttu-id="be451-152">To configure the peering between the HDInsight network and the AKS cluster network, select the virtual network and then select __Peerings__.</span><span class="sxs-lookup"><span data-stu-id="be451-152">To configure the peering between the HDInsight network and the AKS cluster network, select the virtual network and then select __Peerings__.</span></span> <span data-ttu-id="be451-153">Select __+ Add__ and use the following values to populate the form:</span><span class="sxs-lookup"><span data-stu-id="be451-153">Select __+ Add__ and use the following values to populate the form:</span></span>

    * <span data-ttu-id="be451-154">__Name__: Enter a unique name for this peering configuration.</span><span class="sxs-lookup"><span data-stu-id="be451-154">__Name__: Enter a unique name for this peering configuration.</span></span>
    * <span data-ttu-id="be451-155">__Virtual network__: Use this field to select the virtual network for the **AKS cluster**.</span><span class="sxs-lookup"><span data-stu-id="be451-155">__Virtual network__: Use this field to select the virtual network for the **AKS cluster**.</span></span>

    <span data-ttu-id="be451-156">Leave all other fields at the default value, then select __OK__ to configure the peering.</span><span class="sxs-lookup"><span data-stu-id="be451-156">Leave all other fields at the default value, then select __OK__ to configure the peering.</span></span>

6. <span data-ttu-id="be451-157">To configure the peering between the AKS cluster network and the HDInsight network, select the __AKS cluster virtual network__, and then select __Peerings__.</span><span class="sxs-lookup"><span data-stu-id="be451-157">To configure the peering between the AKS cluster network and the HDInsight network, select the __AKS cluster virtual network__, and then select __Peerings__.</span></span> <span data-ttu-id="be451-158">Select __+ Add__ and use the following values to populate the form:</span><span class="sxs-lookup"><span data-stu-id="be451-158">Select __+ Add__ and use the following values to populate the form:</span></span>

    * <span data-ttu-id="be451-159">__Name__: Enter a unique name for this peering configuration.</span><span class="sxs-lookup"><span data-stu-id="be451-159">__Name__: Enter a unique name for this peering configuration.</span></span>
    * <span data-ttu-id="be451-160">__Virtual network__: Use this field to select the virtual network for the __HDInsight cluster__.</span><span class="sxs-lookup"><span data-stu-id="be451-160">__Virtual network__: Use this field to select the virtual network for the __HDInsight cluster__.</span></span>

    <span data-ttu-id="be451-161">Leave all other fields at the default value, then select __OK__ to configure the peering.</span><span class="sxs-lookup"><span data-stu-id="be451-161">Leave all other fields at the default value, then select __OK__ to configure the peering.</span></span>

## <a name="install-kafka-on-hdinsight"></a><span data-ttu-id="be451-162">Install Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="be451-162">Install Kafka on HDInsight</span></span>

<span data-ttu-id="be451-163">When creating the Kafka on HDInsight cluster, you must join the virtual network created earlier for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be451-163">When creating the Kafka on HDInsight cluster, you must join the virtual network created earlier for HDInsight.</span></span> <span data-ttu-id="be451-164">For more information on creating a Kafka cluster, see the [Create a Kafka cluster](apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="be451-164">For more information on creating a Kafka cluster, see the [Create a Kafka cluster](apache-kafka-get-started.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be451-165">When creating the cluster, you must use the __Advanced settings__ to join the virtual network that you created for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be451-165">When creating the cluster, you must use the __Advanced settings__ to join the virtual network that you created for HDInsight.</span></span>

## <a name="configure-kafka-ip-advertising"></a><span data-ttu-id="be451-166">Configure Kafka IP Advertising</span><span class="sxs-lookup"><span data-stu-id="be451-166">Configure Kafka IP Advertising</span></span>

<span data-ttu-id="be451-167">Use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span><span class="sxs-lookup"><span data-stu-id="be451-167">Use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="be451-168">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="be451-168">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="be451-169">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="be451-169">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="be451-170">When prompted, use the HTTPS user name and password for the cluster.</span><span class="sxs-lookup"><span data-stu-id="be451-170">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="be451-171">The Ambari Web UI for the cluster is displayed.</span><span class="sxs-lookup"><span data-stu-id="be451-171">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="be451-172">To view information on Kafka, select __Kafka__ from the list on the left.</span><span class="sxs-lookup"><span data-stu-id="be451-172">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![Service list with Kafka highlighted](./media/apache-kafka-azure-container-services/select-kafka-service.png)

3. <span data-ttu-id="be451-174">To view Kafka configuration, select __Configs__ from the top middle.</span><span class="sxs-lookup"><span data-stu-id="be451-174">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Configs links for Kafka](./media/apache-kafka-azure-container-services/select-kafka-config.png)

4. <span data-ttu-id="be451-176">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span><span class="sxs-lookup"><span data-stu-id="be451-176">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Kafka configuration, for kafka-env](./media/apache-kafka-azure-container-services/search-for-kafka-env.png)

5. <span data-ttu-id="be451-178">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span><span class="sxs-lookup"><span data-stu-id="be451-178">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="be451-179">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span><span class="sxs-lookup"><span data-stu-id="be451-179">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="be451-180">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="be451-180">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="be451-181">To save the configuration changes, use the __Save__ button.</span><span class="sxs-lookup"><span data-stu-id="be451-181">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="be451-182">Enter a text message describing the changes.</span><span class="sxs-lookup"><span data-stu-id="be451-182">Enter a text message describing the changes.</span></span> <span data-ttu-id="be451-183">Select __OK__ once the changes have been saved.</span><span class="sxs-lookup"><span data-stu-id="be451-183">Select __OK__ once the changes have been saved.</span></span>

    ![Save configuration button](./media/apache-kafka-azure-container-services/save-button.png)

9. <span data-ttu-id="be451-185">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span><span class="sxs-lookup"><span data-stu-id="be451-185">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="be451-186">Select OK to complete this operation.</span><span class="sxs-lookup"><span data-stu-id="be451-186">Select OK to complete this operation.</span></span>

    ![Service actions, with turn on maintenance highlighted](./media/apache-kafka-azure-container-services/turn-on-maintenance-mode.png)

10. <span data-ttu-id="be451-188">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span><span class="sxs-lookup"><span data-stu-id="be451-188">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="be451-189">Confirm the restart, and then use the __OK__ button after the operation has completed.</span><span class="sxs-lookup"><span data-stu-id="be451-189">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![Restart button with restart all affected highlighted](./media/apache-kafka-azure-container-services/restart-button.png)

11. <span data-ttu-id="be451-191">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span><span class="sxs-lookup"><span data-stu-id="be451-191">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="be451-192">Select **OK** to complete this operation.</span><span class="sxs-lookup"><span data-stu-id="be451-192">Select **OK** to complete this operation.</span></span>

## <a name="test-the-configuration"></a><span data-ttu-id="be451-193">Test the configuration</span><span class="sxs-lookup"><span data-stu-id="be451-193">Test the configuration</span></span>

<span data-ttu-id="be451-194">At this point, Kafka and Azure Kubernetes Service are in communication through the peered virtual networks.</span><span class="sxs-lookup"><span data-stu-id="be451-194">At this point, Kafka and Azure Kubernetes Service are in communication through the peered virtual networks.</span></span> <span data-ttu-id="be451-195">To test this connection, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="be451-195">To test this connection, use the following steps:</span></span>

1. <span data-ttu-id="be451-196">Create a Kafka topic that is used by the test application.</span><span class="sxs-lookup"><span data-stu-id="be451-196">Create a Kafka topic that is used by the test application.</span></span> <span data-ttu-id="be451-197">For information on creating Kafka topics, see the [Create a Kafka cluster](apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="be451-197">For information on creating Kafka topics, see the [Create a Kafka cluster](apache-kafka-get-started.md) document.</span></span>

2. <span data-ttu-id="be451-198">Download the example application from [https://github.com/Blackmist/Kafka-AKS-Test](https://github.com/Blackmist/Kafka-AKS-Test).</span><span class="sxs-lookup"><span data-stu-id="be451-198">Download the example application from [https://github.com/Blackmist/Kafka-AKS-Test](https://github.com/Blackmist/Kafka-AKS-Test).</span></span>

3. <span data-ttu-id="be451-199">Edit the `index.js` file and change the following lines:</span><span class="sxs-lookup"><span data-stu-id="be451-199">Edit the `index.js` file and change the following lines:</span></span>

    * <span data-ttu-id="be451-200">`var topic = 'mytopic'`: Replace `mytopic` with the name of the Kafka topic used by this application.</span><span class="sxs-lookup"><span data-stu-id="be451-200">`var topic = 'mytopic'`: Replace `mytopic` with the name of the Kafka topic used by this application.</span></span>
    * <span data-ttu-id="be451-201">`var brokerHost = '176.16.0.13:9092`: Replace `176.16.0.13` with the internal IP address of one of the broker hosts for your cluster.</span><span class="sxs-lookup"><span data-stu-id="be451-201">`var brokerHost = '176.16.0.13:9092`: Replace `176.16.0.13` with the internal IP address of one of the broker hosts for your cluster.</span></span>

        <span data-ttu-id="be451-202">To find the internal IP address of the broker hosts (workernodes) in the cluster, see the [Ambari REST API](../hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-internal-ip-address-of-cluster-nodes) document.</span><span class="sxs-lookup"><span data-stu-id="be451-202">To find the internal IP address of the broker hosts (workernodes) in the cluster, see the [Ambari REST API](../hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-internal-ip-address-of-cluster-nodes) document.</span></span> <span data-ttu-id="be451-203">Pick IP address of one of the entries where the domain name begins with `wn`.</span><span class="sxs-lookup"><span data-stu-id="be451-203">Pick IP address of one of the entries where the domain name begins with `wn`.</span></span>

4. <span data-ttu-id="be451-204">From a command line in the `src` directory, install dependencies and use Docker to build an image for deployment:</span><span class="sxs-lookup"><span data-stu-id="be451-204">From a command line in the `src` directory, install dependencies and use Docker to build an image for deployment:</span></span>

    ```bash
    docker build -t kafka-aks-test .
    ```

    > [!NOTE]
    > <span data-ttu-id="be451-205">Packages required by this application are checked into the repository, so you do not need to use the `npm` utility to install them.</span><span class="sxs-lookup"><span data-stu-id="be451-205">Packages required by this application are checked into the repository, so you do not need to use the `npm` utility to install them.</span></span>

5. <span data-ttu-id="be451-206">Log in to your Azure Container Registry (ACR) and find the loginServer name:</span><span class="sxs-lookup"><span data-stu-id="be451-206">Log in to your Azure Container Registry (ACR) and find the loginServer name:</span></span>

    ```bash
    az acr login --name <acrName>
    az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
    ```

    > [!NOTE]
    > <span data-ttu-id="be451-207">If you don't know your Azure Container Registry name, or are unfamiliar with using the Azure CLI to work with the Azure Kubernetes Service, see the [AKS tutorials](../../aks/tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="be451-207">If you don't know your Azure Container Registry name, or are unfamiliar with using the Azure CLI to work with the Azure Kubernetes Service, see the [AKS tutorials](../../aks/tutorial-kubernetes-prepare-app.md).</span></span>

6. <span data-ttu-id="be451-208">Tag the local `kafka-aks-test` image with the loginServer of your ACR.</span><span class="sxs-lookup"><span data-stu-id="be451-208">Tag the local `kafka-aks-test` image with the loginServer of your ACR.</span></span> <span data-ttu-id="be451-209">Also add `:v1` to the end to indicate the image version:</span><span class="sxs-lookup"><span data-stu-id="be451-209">Also add `:v1` to the end to indicate the image version:</span></span>

    ```bash
    docker tag kafka-aks-test <acrLoginServer>/kafka-aks-test:v1
    ```

7. <span data-ttu-id="be451-210">Push the image to the registry:</span><span class="sxs-lookup"><span data-stu-id="be451-210">Push the image to the registry:</span></span>

    ```bash
    docker push <acrLoginServer>/kafka-aks-test:v1
    ```
    <span data-ttu-id="be451-211">This operation takes several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="be451-211">This operation takes several minutes to complete.</span></span>

8. <span data-ttu-id="be451-212">Edit the Kubernetes manifest file (`kafka-aks-test.yaml`) and replace `microsoft` with the ACR loginServer name retrieved in step 4.</span><span class="sxs-lookup"><span data-stu-id="be451-212">Edit the Kubernetes manifest file (`kafka-aks-test.yaml`) and replace `microsoft` with the ACR loginServer name retrieved in step 4.</span></span>

9. <span data-ttu-id="be451-213">Use the following command to deploy the application settings from the manifest:</span><span class="sxs-lookup"><span data-stu-id="be451-213">Use the following command to deploy the application settings from the manifest:</span></span>

    ```bash
    kubectl create -f kafka-aks-test.yaml
    ```

10. <span data-ttu-id="be451-214">Use the following command to watch for the `EXTERNAL-IP` of the application:</span><span class="sxs-lookup"><span data-stu-id="be451-214">Use the following command to watch for the `EXTERNAL-IP` of the application:</span></span>

    ```bash
    kubectl get service kafka-aks-test --watch
    ```

    <span data-ttu-id="be451-215">Once an external IP address is assigned, use __CTRL + C__ to exit the watch</span><span class="sxs-lookup"><span data-stu-id="be451-215">Once an external IP address is assigned, use __CTRL + C__ to exit the watch</span></span>

11. <span data-ttu-id="be451-216">Open a web browser and enter the external IP address for the service.</span><span class="sxs-lookup"><span data-stu-id="be451-216">Open a web browser and enter the external IP address for the service.</span></span> <span data-ttu-id="be451-217">You arrive at a page similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="be451-217">You arrive at a page similar to the following image:</span></span>

    ![Image of the web page](./media/apache-kafka-azure-container-services/test-web-page.png)

12. <span data-ttu-id="be451-219">Enter text into the field and then select the __Send__ button.</span><span class="sxs-lookup"><span data-stu-id="be451-219">Enter text into the field and then select the __Send__ button.</span></span> <span data-ttu-id="be451-220">The data is sent to Kafka.</span><span class="sxs-lookup"><span data-stu-id="be451-220">The data is sent to Kafka.</span></span> <span data-ttu-id="be451-221">Then the Kafka consumer in the application reads the message and adds it to the __Messages from Kafka__ section.</span><span class="sxs-lookup"><span data-stu-id="be451-221">Then the Kafka consumer in the application reads the message and adds it to the __Messages from Kafka__ section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="be451-222">You may receive multiple copies of a message.</span><span class="sxs-lookup"><span data-stu-id="be451-222">You may receive multiple copies of a message.</span></span> <span data-ttu-id="be451-223">This problem usually happens when you refresh your browser after connecting, or open multiple browser connections to the application.</span><span class="sxs-lookup"><span data-stu-id="be451-223">This problem usually happens when you refresh your browser after connecting, or open multiple browser connections to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be451-224">Next steps</span><span class="sxs-lookup"><span data-stu-id="be451-224">Next steps</span></span>

<span data-ttu-id="be451-225">Use the following links to learn how to use Apache Kafka on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="be451-225">Use the following links to learn how to use Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="be451-226">Get started with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="be451-226">Get started with Kafka on HDInsight</span></span>](apache-kafka-get-started.md)

* [<span data-ttu-id="be451-227">Use MirrorMaker to create a replica of Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="be451-227">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](apache-kafka-mirroring.md)

* [<span data-ttu-id="be451-228">Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="be451-228">Use Apache Storm with Kafka on HDInsight</span></span>](../hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="be451-229">Use Apache Spark with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="be451-229">Use Apache Spark with Kafka on HDInsight</span></span>](../hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="be451-230">Connect to Kafka through an Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="be451-230">Connect to Kafka through an Azure Virtual Network</span></span>](apache-kafka-connect-vpn-gateway.md)
