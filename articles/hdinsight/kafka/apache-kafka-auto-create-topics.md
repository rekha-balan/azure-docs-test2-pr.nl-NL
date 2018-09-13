---
title: Enable automatic topic creation in Apache Kafka - Azure HDInsight
description: Learn how to configure Apache Kafka on HDInsight to automatically create topics. You can configure Kafka by setting auto.create.topics.enable to true through Ambari or during cluster creation through PowerShell or Resource Manager templates.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/18/2018
ms.openlocfilehash: f187991b1ff128a45845c2096928945722a9ae6a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855590"
---
# <a name="how-to-configure-apache-kafka-on-hdinsight-to-automatically-create-topics"></a><span data-ttu-id="70700-104">How to configure Apache Kafka on HDInsight to automatically create topics</span><span class="sxs-lookup"><span data-stu-id="70700-104">How to configure Apache Kafka on HDInsight to automatically create topics</span></span>

<span data-ttu-id="70700-105">By default, Kafka on HDInsight does not enable automatic topic creation.</span><span class="sxs-lookup"><span data-stu-id="70700-105">By default, Kafka on HDInsight does not enable automatic topic creation.</span></span> <span data-ttu-id="70700-106">You can enable auto topic creation for existing clusters using Ambari.</span><span class="sxs-lookup"><span data-stu-id="70700-106">You can enable auto topic creation for existing clusters using Ambari.</span></span> <span data-ttu-id="70700-107">You can also enable auto topic creation when creating a new Kafka cluster using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="70700-107">You can also enable auto topic creation when creating a new Kafka cluster using an Azure Resource Manager template.</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="70700-108">Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="70700-108">Ambari Web UI</span></span>

<span data-ttu-id="70700-109">To enable automatic topic creation on an existing cluster through the Ambari Web UI, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="70700-109">To enable automatic topic creation on an existing cluster through the Ambari Web UI, use the following steps:</span></span>

1. <span data-ttu-id="70700-110">From the [Azure portal](https://portal.azure.com), select the Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="70700-110">From the [Azure portal](https://portal.azure.com), select the Kafka cluster.</span></span>

2. <span data-ttu-id="70700-111">From the __Cluster overview__, select __Cluster dashboard__.</span><span class="sxs-lookup"><span data-stu-id="70700-111">From the __Cluster overview__, select __Cluster dashboard__.</span></span> 

    ![Image of the portal with cluster dashboard selected](./media/apache-kafka-auto-create-topics/kafka-cluster-overview.png)

3. <span data-ttu-id="70700-113">Then select __HDInsight cluster dashboard__.</span><span class="sxs-lookup"><span data-stu-id="70700-113">Then select __HDInsight cluster dashboard__.</span></span> <span data-ttu-id="70700-114">When prompted, authenticate using the login (admin) credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="70700-114">When prompted, authenticate using the login (admin) credentials for the cluster.</span></span>

    ![Image of the HDInsight cluster dashboard entry](./media/apache-kafka-auto-create-topics/hdinsight-cluster-dashboard.png)

3. <span data-ttu-id="70700-116">Select the Kafka service from the list on the left of the page.</span><span class="sxs-lookup"><span data-stu-id="70700-116">Select the Kafka service from the list on the left of the page.</span></span>

    ![Service list](./media/apache-kafka-auto-create-topics/service-list.png)

4. <span data-ttu-id="70700-118">Select Configs in the middle of the page.</span><span class="sxs-lookup"><span data-stu-id="70700-118">Select Configs in the middle of the page.</span></span>

    ![Service config tab](./media/apache-kafka-auto-create-topics/service-config.png)

5. <span data-ttu-id="70700-120">In the Filter field, enter a value of `auto.create`.</span><span class="sxs-lookup"><span data-stu-id="70700-120">In the Filter field, enter a value of `auto.create`.</span></span> 

    ![Image of the filter field](./media/apache-kafka-auto-create-topics/filter.png)

    <span data-ttu-id="70700-122">This filters the list of properties and displays the `auto.create.topics.enable` setting.</span><span class="sxs-lookup"><span data-stu-id="70700-122">This filters the list of properties and displays the `auto.create.topics.enable` setting.</span></span>

6. <span data-ttu-id="70700-123">Change the value of `auto.create.topics.enable` to `true`, and then select Save.</span><span class="sxs-lookup"><span data-stu-id="70700-123">Change the value of `auto.create.topics.enable` to `true`, and then select Save.</span></span> <span data-ttu-id="70700-124">Add a note, and then select Save again.</span><span class="sxs-lookup"><span data-stu-id="70700-124">Add a note, and then select Save again.</span></span>

    ![Image of the auto.create.topics.enable entry](./media/apache-kafka-auto-create-topics/auto-create-topics-enable.png)

7. <span data-ttu-id="70700-126">Select the Kafka service, select __Restart__, and then select __Restart all affected__.</span><span class="sxs-lookup"><span data-stu-id="70700-126">Select the Kafka service, select __Restart__, and then select __Restart all affected__.</span></span> <span data-ttu-id="70700-127">When prompted, select __Confirm restart all__.</span><span class="sxs-lookup"><span data-stu-id="70700-127">When prompted, select __Confirm restart all__.</span></span>

    ![Image of restart selection](./media/apache-kafka-auto-create-topics/restart-all-affected.png)

> [!NOTE]
> <span data-ttu-id="70700-129">You can also set Ambari values through the Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="70700-129">You can also set Ambari values through the Ambari REST API.</span></span> <span data-ttu-id="70700-130">This is generally more difficult, as you have to make multiple REST calls to retrieve the current configuration, modify it, etc. For more information, see the [Manage HDInsight clusters using the Ambari REST API](../hdinsight-hadoop-manage-ambari-rest-api.md) document.</span><span class="sxs-lookup"><span data-stu-id="70700-130">This is generally more difficult, as you have to make multiple REST calls to retrieve the current configuration, modify it, etc. For more information, see the [Manage HDInsight clusters using the Ambari REST API](../hdinsight-hadoop-manage-ambari-rest-api.md) document.</span></span>

## <a name="resource-manager-templates"></a><span data-ttu-id="70700-131">Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="70700-131">Resource Manager templates</span></span>

<span data-ttu-id="70700-132">When creating a Kafka cluster using an Azure Resource Manager template, you can directly set `auto.create.topics.enable` by adding it in a `kafka-broker`.</span><span class="sxs-lookup"><span data-stu-id="70700-132">When creating a Kafka cluster using an Azure Resource Manager template, you can directly set `auto.create.topics.enable` by adding it in a `kafka-broker`.</span></span> <span data-ttu-id="70700-133">The following JSON snippet demonstrates how to set this value to `true`:</span><span class="sxs-lookup"><span data-stu-id="70700-133">The following JSON snippet demonstrates how to set this value to `true`:</span></span>

```json
"clusterDefinition": {
    "kind": "kafka",
    "configurations": {
    "gateway": {
        "restAuthCredential.isEnabled": true,
        "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
        "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
    },
    "kafka-broker": {
        "auto.create.topics.enable": "true"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="70700-134">Next Steps</span><span class="sxs-lookup"><span data-stu-id="70700-134">Next Steps</span></span>

<span data-ttu-id="70700-135">In this document, you learned how to enable automatic topic creation for Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="70700-135">In this document, you learned how to enable automatic topic creation for Kafka on HDInsight.</span></span> <span data-ttu-id="70700-136">To learn more about working with Kafka, see the following links:</span><span class="sxs-lookup"><span data-stu-id="70700-136">To learn more about working with Kafka, see the following links:</span></span>

* [<span data-ttu-id="70700-137">Analyze Kafka logs</span><span class="sxs-lookup"><span data-stu-id="70700-137">Analyze Kafka logs</span></span>](apache-kafka-log-analytics-operations-management.md)
* [<span data-ttu-id="70700-138">Replicate data between Kafka clusters</span><span class="sxs-lookup"><span data-stu-id="70700-138">Replicate data between Kafka clusters</span></span>](apache-kafka-mirroring.md)
