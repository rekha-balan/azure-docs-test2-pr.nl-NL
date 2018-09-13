---
title: Add users for Azure Stack ADFS | Microsoft Docs
description: Learn how to add users for ADFS deployments of Azure Stack
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2018
ms.author: jeffgilb
ms.reviewer: unknown
ms.openlocfilehash: 5774750edc5b7380275d4f20aee3be47f2f62b4d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808020"
---
# <a name="add-users-in-the-azure-stack-development-kit"></a>Add users in the Azure Stack Development Kit

*Applies to: Azure Stack Development Kit*

To add additional users to the Development Kit deployment, you must add them to the Azure Stack Development Kit directory using Microsoft Management Console from the Azure Stack host computer.
1.  On the Azure Stack host computer, open Microsoft Management Console.
2.  Click **File > Add or remove snap-in**.
3.  Select **Active Directory Users and Computers** > **AzureStack.local** > **Users**.
4.  Click **Action** > **New** > **User**.
5.  In the New Object – User window, provide and confirm a password
6.  Click **Next** to finalize the values and click Finish to create the user.


