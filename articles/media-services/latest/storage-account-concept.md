---
title: Storage accounts in Azure Media Services | Microsoft Docs
description: This article discusses how Media Services uses storage accounts.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 03/19/2018
ms.author: juliako
ms.openlocfilehash: 6d4c21867b0b46508f348300ae2b9553a75d23b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865445"
---
# <a name="storage-accounts"></a>Storage accounts

When creating a Media Services account, you need to supply the name of an Azure Storage account resource. The specified storage account is attached to your Media Services account. 

You must have one **Primary** storage account and you can have any number of **Secondary** storage accounts associated with your Media Services account. Media Services supports **General-purpose v2** (GPv2) or **General-purpose v1** (GPv1) accounts. 

>[!NOTE]
> Blob only accounts are not allowed as **Primary**. 

We recommend that you use GPv2, so you can take advantage of choosing between hot and cool storage tiers. To learn more about storage accounts, see [Azure Storage account options](../../storage/common/storage-account-options.md). 

## <a name="assets-in-a-storage-account"></a>Assets in a storage account

In Media Services v3, the Storage APIs are used to upload files. To see how to use Storage APIs with Media Services to upload your input files, check out [Create a job input from a local file](job-input-from-local-file-how-to.md). 

> [!Note]
> You should not attempt to change the contents of blob containers that were generated by the Media Services SDK without using Media Services APIs.

## <a name="next-steps"></a>Next steps

To learn how to attach a storage account to your Media Services account, see [Create an account](create-account-cli-quickstart.md).