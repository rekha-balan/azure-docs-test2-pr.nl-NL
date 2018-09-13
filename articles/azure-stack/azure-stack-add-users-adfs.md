---
title: Add users for Azure Stack ADFS | Microsoft Docs
description: Learn how to add users for ADFS deployments of Azure Stack
services: azure-stack
documentationcenter: ''
author: HeathL17
manager: byronr
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/1/2017
ms.author: helaw
ms.openlocfilehash: 5f7febb10f776d6a314c98a2ec476725e7b07f6f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553065"
---
# <a name="add-users-in-the-azure-stack-poc"></a><span data-ttu-id="1552f-103">Add users in the Azure Stack POC</span><span class="sxs-lookup"><span data-stu-id="1552f-103">Add users in the Azure Stack POC</span></span>

<span data-ttu-id="1552f-104">To add more users in the POC deployment, you must add them to the Azure Stack POC AD using Microsoft Management Console from the Azure Stack host computer.</span><span class="sxs-lookup"><span data-stu-id="1552f-104">To add more users in the POC deployment, you must add them to the Azure Stack POC AD using Microsoft Management Console from the Azure Stack host computer.</span></span>
1.  <span data-ttu-id="1552f-105">On the Azure Stack host computer, open Microsoft Management Console.</span><span class="sxs-lookup"><span data-stu-id="1552f-105">On the Azure Stack host computer, open Microsoft Management Console.</span></span>
2.  <span data-ttu-id="1552f-106">Click **File > Add or remove snap-in**.</span><span class="sxs-lookup"><span data-stu-id="1552f-106">Click **File > Add or remove snap-in**.</span></span>
3.  <span data-ttu-id="1552f-107">Select **Active Directory Users and Computers** > **AzureStack.local** > **Users**.</span><span class="sxs-lookup"><span data-stu-id="1552f-107">Select **Active Directory Users and Computers** > **AzureStack.local** > **Users**.</span></span>
4.  <span data-ttu-id="1552f-108">Click **Action** > **New** > **User**.</span><span class="sxs-lookup"><span data-stu-id="1552f-108">Click **Action** > **New** > **User**.</span></span>
5.  <span data-ttu-id="1552f-109">In the New Object – User window, provide and confirm a password</span><span class="sxs-lookup"><span data-stu-id="1552f-109">In the New Object – User window, provide and confirm a password</span></span>
6.  <span data-ttu-id="1552f-110">To avoid requirements to change the password for the user you just created, uncheck **User must change password at next logon** and check **Password never expires**.</span><span class="sxs-lookup"><span data-stu-id="1552f-110">To avoid requirements to change the password for the user you just created, uncheck **User must change password at next logon** and check **Password never expires**.</span></span>
7.  <span data-ttu-id="1552f-111">Click **Next** to finalize the values and click Finish to create the user.</span><span class="sxs-lookup"><span data-stu-id="1552f-111">Click **Next** to finalize the values and click Finish to create the user.</span></span>


