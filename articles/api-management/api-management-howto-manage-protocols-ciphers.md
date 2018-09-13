---
title: Manage protocols and ciphers in Azure API Management | Microsoft Docs
description: Learn how to manage protocols (TLS, SSL) and ciphers (DES) in Azure API Management.
services: api-management
documentationcenter: ''
author: mikebudzynski
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2018
ms.author: apimpm
ms.openlocfilehash: 454ba5c42694581bfa8fb1ec69ce97ac906b53d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867192"
---
# <a name="manage-protocols-and-ciphers-in-azure-api-management"></a>Manage protocols and ciphers in Azure API Management

Azure API Management supports multiple versions of TLS protocol for both client and backend sides as well as the 3DES cipher.

This guide shows you how to manage protocols and ciphers configuration for an Azure API Management instance.

![Manage protocols and ciphers in APIM](./media/api-management-howto-manage-protocols-ciphers/api-management-protocols-ciphers.png)

## <a name="prerequisites"></a>Prerequisites

To follow the steps in this article, you must have:

* An API Management instance

## <a name="how-to-manage-tls-protocols-and-3des-cipher"></a>How to manage TLS protocols and 3DES cipher

1. Navigate to your **API Management instance** in the Azure portal.
2. Select **SSL** from the menu.  
    ![Manage protocols and ciphers in APIM - menu](./media/api-management-howto-manage-protocols-ciphers/api-management-menu.png)
3. Enable or disable desired protocols or ciphers.
4. Click **Save**. Changes will be applied within an hour.  
    ![Manage protocols and ciphers in APIM - save](./media/api-management-howto-manage-protocols-ciphers/api-management-protocols-ciphers-save.png)

## <a name="next-steps"></a>Next steps

* Learn more about [TLS (Transport Layer Security)](https://docs.microsoft.com/en-us/dotnet/framework/network-programming/tls).
* Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.