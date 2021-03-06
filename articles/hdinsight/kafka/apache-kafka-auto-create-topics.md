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
# <a name="how-to-configure-apache-kafka-on-hdinsight-to-automatically-create-topics"></a>How to configure Apache Kafka on HDInsight to automatically create topics

By default, Kafka on HDInsight does not enable automatic topic creation. You can enable auto topic creation for existing clusters using Ambari. You can also enable auto topic creation when creating a new Kafka cluster using an Azure Resource Manager template.

## <a name="ambari-web-ui"></a>Ambari Web UI

To enable automatic topic creation on an existing cluster through the Ambari Web UI, use the following steps:

1. From the [Azure portal](https://portal.azure.com), select the Kafka cluster.

2. From the __Cluster overview__, select __Cluster dashboard__. 

    ![Image of the portal with cluster dashboard selected](./media/apache-kafka-auto-create-topics/kafka-cluster-overview.png)

3. Then select __HDInsight cluster dashboard__. When prompted, authenticate using the login (admin) credentials for the cluster.

    ![Image of the HDInsight cluster dashboard entry](./media/apache-kafka-auto-create-topics/hdinsight-cluster-dashboard.png)

3. Select the Kafka service from the list on the left of the page.

    ![Service list](./media/apache-kafka-auto-create-topics/service-list.png)

4. Select Configs in the middle of the page.

    ![Service config tab](./media/apache-kafka-auto-create-topics/service-config.png)

5. In the Filter field, enter a value of `auto.create`. 

    ![Image of the filter field](./media/apache-kafka-auto-create-topics/filter.png)

    This filters the list of properties and displays the `auto.create.topics.enable` setting.

6. Change the value of `auto.create.topics.enable` to `true`, and then select Save. Add a note, and then select Save again.

    ![Image of the auto.create.topics.enable entry](./media/apache-kafka-auto-create-topics/auto-create-topics-enable.png)

7. Select the Kafka service, select __Restart__, and then select __Restart all affected__. When prompted, select __Confirm restart all__.

    ![Image of restart selection](./media/apache-kafka-auto-create-topics/restart-all-affected.png)

> [!NOTE]
> You can also set Ambari values through the Ambari REST API. This is generally more difficult, as you have to make multiple REST calls to retrieve the current configuration, modify it, etc. For more information, see the [Manage HDInsight clusters using the Ambari REST API](../hdinsight-hadoop-manage-ambari-rest-api.md) document.

## <a name="resource-manager-templates"></a>Resource Manager templates

When creating a Kafka cluster using an Azure Resource Manager template, you can directly set `auto.create.topics.enable` by adding it in a `kafka-broker`. The following JSON snippet demonstrates how to set this value to `true`:

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

## <a name="next-steps"></a>Next Steps

In this document, you learned how to enable automatic topic creation for Kafka on HDInsight. To learn more about working with Kafka, see the following links:

* [Analyze Kafka logs](apache-kafka-log-analytics-operations-management.md)
* [Replicate data between Kafka clusters](apache-kafka-mirroring.md)
