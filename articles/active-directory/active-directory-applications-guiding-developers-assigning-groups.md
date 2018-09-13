---
title: Assign groups to Azure AD apps | Microsoft Docs'
description: How to implement group assignment for Azure applications.
services: active-directory
documentationcenter: ''
author: kgremban
manager: mtillman
editor: ''
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: 471099c58a7fc1dfd520e693873a76f64c0fbf0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44829192"
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="b1639-103">Assign Azure Active Directory groups to an application</span><span class="sxs-lookup"><span data-stu-id="b1639-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="b1639-104">Before you can assign users and groups to an application, you must require user assignment.</span><span class="sxs-lookup"><span data-stu-id="b1639-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="b1639-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span><span class="sxs-lookup"><span data-stu-id="b1639-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="b1639-106">This article assumes that you have already created groups in the active directory you are using for this application.</span><span class="sxs-lookup"><span data-stu-id="b1639-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="b1639-107">Assigning Groups to an Application</span><span class="sxs-lookup"><span data-stu-id="b1639-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="b1639-108">Log in to the Azure portal with an administrator account.</span><span class="sxs-lookup"><span data-stu-id="b1639-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="b1639-109">Click on the **All Items** item in the main menu.</span><span class="sxs-lookup"><span data-stu-id="b1639-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="b1639-110">Choose the directory you are using for the application.</span><span class="sxs-lookup"><span data-stu-id="b1639-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="b1639-111">Click on the **APPLICATIONS** tab.</span><span class="sxs-lookup"><span data-stu-id="b1639-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="b1639-112">Select the application from the list of applications associated with this directory.</span><span class="sxs-lookup"><span data-stu-id="b1639-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="b1639-113">Click the **USERS AND GROUPS** tab.</span><span class="sxs-lookup"><span data-stu-id="b1639-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="b1639-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span><span class="sxs-lookup"><span data-stu-id="b1639-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="b1639-115">Select the group.</span><span class="sxs-lookup"><span data-stu-id="b1639-115">Select the group.</span></span>
9. <span data-ttu-id="b1639-116">Click **ASSIGN**.</span><span class="sxs-lookup"><span data-stu-id="b1639-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="b1639-117">Click **yes** when prompted.</span><span class="sxs-lookup"><span data-stu-id="b1639-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1639-118">Next Steps</span><span class="sxs-lookup"><span data-stu-id="b1639-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
