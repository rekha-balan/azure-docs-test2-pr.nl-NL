---
title: Migration of integration resources from Azure Germany to global Azure
description: This article provides help for migrating integration resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: 16e7ffa822f645c2a5a070ab3c693cef84a1a85c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871422"
---
# <a name="migration-of-integration-resources-from-azure-germany-to-global-azure"></a>Migration of integration resources from Azure Germany to global Azure

This article will provide you some help for the migration of Azure Integration resources from Azure Germany to global Azure.

## <a name="service-bus"></a>Service Bus

Service Bus services don't have data export or import capabilities. To migrate Service Bus from Azure Germany to global Azure, you can export the Service Bus resources [as a Resource Manager template](../azure-resource-manager/resource-manager-export-template-powershell.md). Then adopt the exported template for global Azure and recreate the resources.

> [!NOTE]
> This doesn't copy the data (for example messages), it's only recreating the metadata.


> [!IMPORTANT]
> Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.

### <a name="metadata-service-bus"></a>Metadata Service Bus

- Namespaces
- Queues
- Topics
- Subscriptions
- Rules
- AuthorizationRules (see also below)

### <a name="keys"></a>Keys

The Export/Recreate steps above won't copy the SAS keys associated with Authorization rules. If you need to preserve the SAS keys, use the `New-AzureRmServiceBuskey` cmdlet with the optional parameter `-Keyvalue` to accept the key as string. The updated cmdlet is available at [PowerShell Gallery release 6.4.0 (July 2018)](https://www.powershellgallery.com/packages/AzureRM/6.4.0) or at [GitHub](https://github.com/Azure/azure-powershell/releases/tag/v6.4.0-July2018).

### <a name="usage-example"></a>Usage example

```powershell
New-AzureRmServiceBuskey -ResourceGroupName <resourcegroupname> -Namespace <namespace> -Name <name of Authorization rule> -RegenerateKey <PrimaryKey/SecondaryKey> -KeyValue <string - key value>
```

```powershell
New-AzureRmServiceBuskey -ResourceGroupName <resourcegroupname> -Namespace <namespace> -Queue <queuename> -Name <name of Authorization rule> -RegenerateKey <PrimaryKey/SecondaryKey> -KeyValue <string - key value>
```

```powershell
New-AzureRmServiceBuskey -ResourceGroupName <resourcegroupname> -Namespace <namespace> -Topic <topicname> -Name <name of Authorization rule> -RegenerateKey <PrimaryKey/SecondaryKey> -KeyValue <string - key value>
```

> [!NOTE]
> You will need to update your applications to use a new connection string even if you preserve the keys because the DNS host names are different between Azure Germany and global Azure.

### <a name="sample-connection-strings"></a>Sample connection strings

**Azure Germany**

```cmd
Endpoint=sb://myBFProdnamespaceName.**servicebus.cloudapi.de**/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXx=
```

**Global Azure**

```cmd
Endpoint=sb://myProdnamespaceName.**servicebus.windows.net**/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=XXXXXXXXXXXXx=
```

### <a name="next-steps"></a>Next steps

- Refresh your knowledge about Service Bus by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/service-bus-messaging/#step-by-step-tutorials).
- Make yourself familiar how to [export an Azure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

### <a name="references"></a>References

- [Service Bus Overview](../service-bus-messaging/service-bus-messaging-overview.md)
- [Export a Resource Manager template using PowerShell](../azure-resource-manager/resource-manager-export-template-powershell.md#export-resource-group-as-template)







## <a name="logic-apps"></a>Logic Apps

Logic Apps service isn't available in Azure Germany. However, Azure Scheduler (which is available) is being deprecated. Use Azure Logic apps instead to create scheduling jobs.

### <a name="next-steps"></a>Next Steps

- Make yourself familiar with the features that [Azure Logic Apps provides by following the [Step-by-Step tutorials](https://docs.microsoft.com/azure/logic-apps/#step-by-step-tutorials).

### <a name="reference"></a>Reference

- [Azure Logic Apps overview](../logic-apps/logic-apps-overview.md) 