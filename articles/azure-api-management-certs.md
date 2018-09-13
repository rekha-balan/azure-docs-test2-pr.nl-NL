---
title: Upload an Azure Management API Certificate | Microsoft Docs
description: Learn how to upload athe Management API certficate for the Azure Classic Portal.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: ''
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2016
ms.author: adegeo
ms.openlocfilehash: 7fcd383b25c54a7ddb9a45dabb45128523002010
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551647"
---
# <a name="upload-an-azure-management-api-management-certificate"></a>Upload an Azure Management API Management Certificate
Management certificates allow you to authenticate with the Service Management API provided by Azure. Many programs and tools (such as Visual Studio or the Azure SDK) will use these certficates to automate configuration and deployment of various Azure services. **This only applies to the Azure classic portal**.

> [!WARNING]
> Be careful! These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.
>
>

More information about Azure certificates (including creating a self-signed certificate) is [available](cloud-services/cloud-services-certs-create.md#what-are-management-certificates) to you if you need it.

You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) to authenticate client-code for automation purposes.

## <a name="upload-a-management-certificate"></a>Upload a management certificate
Once you have a management certficate created, (.cer file with only the public key) you can upload it into the portal. When the certificate is available in the portal, anyone with a matching certficiate (private key) can connect through the Management API and access the resources for the associated subscription.

1. Log into the [Azure classic portal](http://manage.windowsazure.com).
2. Make sure to select the correct subscription that you want to associate a certificate with. Press the **Subscriptions** text at the top-right of the portal.

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-api-management-certs/subscription.png)
3. After you have the correct subscription selected, press **Settings** on the left side of the portal (you may need to scroll down).

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-api-management-certs/settings.png)
4. Press the **Management Certificates** tab.

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-api-management-certs/certificates-tab.png)
5. Press the **Upload** button.

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-api-management-certs/upload.png)
6. Fill out the dialog information and press the done **Checkmark**.

    ![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-api-management-certs/upload-dialog.png)

## <a name="next-steps"></a>Next steps
Now that you have a management certificate associated with a subscription, you can (after you have installed the matching certificate locally) programmatically connect to the [Service Management REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate the various Azure resources that are also associated with that subscription.





