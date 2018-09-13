---
title: Sign ins after multiple failures
description: A report that indicates users who have successfully signed in after multiple consecutive failed sign in attempts.
services: active-directory
documentationcenter: ''
author: SSalahAhmed
manager: femila
editor: ''
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: e1645e0728011ee4de85eb89df4b5cb8599846ab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552605"
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="70df6-103">Sign-ins after multiple failures</span><span class="sxs-lookup"><span data-stu-id="70df6-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="70df6-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span><span class="sxs-lookup"><span data-stu-id="70df6-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="70df6-105">Possible causes include:</span><span class="sxs-lookup"><span data-stu-id="70df6-105">Possible causes include:</span></span>

* <span data-ttu-id="70df6-106">User had forgotten their password</span><span class="sxs-lookup"><span data-stu-id="70df6-106">User had forgotten their password</span></span></li><li><span data-ttu-id="70df6-107">User is the victim of a successful password guessing brute force attack</span><span class="sxs-lookup"><span data-stu-id="70df6-107">User is the victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="70df6-108">Results from this report will show you the number of consecutive failed sign-in attempts made prior to the successful sign-in and a timestamp associated with the first successful sign-in.</span><span class="sxs-lookup"><span data-stu-id="70df6-108">Results from this report will show you the number of consecutive failed sign-in attempts made prior to the successful sign-in and a timestamp associated with the first successful sign-in.</span></span>

<span data-ttu-id="70df6-109">**Report Settings**: You can configure the minimum number of consecutive failed sign in attempts that must occur before it can be displayed in the report.</span><span class="sxs-lookup"><span data-stu-id="70df6-109">**Report Settings**: You can configure the minimum number of consecutive failed sign in attempts that must occur before it can be displayed in the report.</span></span> <span data-ttu-id="70df6-110">When you make changes to this setting it is important to note that these changes will not be applied to any existing failed sign ins that currently show up in your existing report.</span><span class="sxs-lookup"><span data-stu-id="70df6-110">When you make changes to this setting it is important to note that these changes will not be applied to any existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="70df6-111">However, they will be applied to all future sign-ins. Changes to this report can only be made by licensed admins.</span><span class="sxs-lookup"><span data-stu-id="70df6-111">However, they will be applied to all future sign-ins. Changes to this report can only be made by licensed admins.</span></span>

![Sign ins after multiple failures](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)


