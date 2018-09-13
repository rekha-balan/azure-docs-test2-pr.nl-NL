---
title: Troubleshoot RemoteApp cloud collections - creation | Microsoft Docs
description: Learn how to troubleshoot RemoteApp cloud collection creation failures
services: remoteapp
documentationcenter: ''
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548909"
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>Troubleshoot creating RemoteApp cloud collections
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

If you are having problems creating a cloud collection, check out the following information.

## <a name="your-image-is-invalid"></a>Your image is invalid
If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md). So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.

## <a name="common-errors-seen-in-the-azure-management-portal"></a>Common errors seen in the Azure Management portal
    DNS server could not be reached
    ProvisioningTimeout

Cloud collections often fail during creation because of you are using custom images.  If you see one of the above errors and you are using a custom image to create the collection, please check the following things:

* Ensure that the custom image you uploaded meets image requirements.
* Most often the common problem is that the image was not properly syspreped.  
* Verify the image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using the image. If the VM fails to boot and not start, then this usually indicates that the custom image was not prepared correctly.  Verify the custom image was built following the How to create a custom template image for RemoteApp

If you are using one of the Microsoft images included with your subscription, try to create the collection again. If the issue persists then please contact Microsoft support.

    PlatformImageTrialModeOnly

If you see this error this usually means that you been upgraded to a paid account but you are trying to use a Microsoft provided image that is valid only during the trial mode of the service. In this case, try to create your cloud collection again, but be sure to specify the correct image.

