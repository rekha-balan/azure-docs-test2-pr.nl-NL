---
title: include file
description: include file
services: storage
author: tamram
ms.service: storage
ms.topic: include
ms.date: 04/04/2018
ms.author: tamram
ms.custom: include file
ms.openlocfilehash: bef314e60b962e39b3a55d0fb7acb40d4d1b4c32
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967336"
---
## <a name="copy-your-credentials-from-the-azure-portal"></a>Copy your credentials from the Azure portal

The sample application needs to authenticate access to your storage account. To authenticate, you provide the application with your storage account credentials in the form of a connection string. To view your storage account credentials:

1. Navigate to the [Azure portal](https://portal.azure.com).
2. Locate your storage account.
3. In the **Settings** section of the storage account overview, select **Access keys**. Your account access keys appear, as well as the complete connection string for each key.   
4. Find the **Connection string** value under **key1**, and click the **Copy** button to copy the connection string. You will add the connection string value to an environment variable in the next step.

    ![Screen shot showing how to copy a connection string from the Azure portal](media/storage-copy-connection-string-portal/portal-connection-string.png)
