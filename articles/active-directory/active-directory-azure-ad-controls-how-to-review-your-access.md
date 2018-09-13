---
title: Review your access | Microsoft Docs
description: Review your access with Azure Active Directory
services: active-directory
author: rolyon
manager: mtillman
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: compliance
ms.date: 07/16/2018
ms.author: rolyon
ms.reviewer: mwahl
ms.openlocfilehash: f85f83ff103818b826ca2c61c41fbbef67e98c14
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869767"
---
# <a name="review-your-access"></a>Review your access

Azure Active Directory (Azure AD) simplifies how enterprises manage access to applications and members of groups in Azure AD and other Microsoft Online Services with a feature called access reviews. Perhaps you received an email from Microsoft that asks you to review access for members of a group or users with access to an application. 

## <a name="open-an-access-review"></a>Open an access review

To see the pending access reviews, click the review access link in the email. Starting in August 2018, the email notifications for Azure AD roles have an updated design. The following shows an example email that is sent when a user is invited to be a reviewer.

![Review access email](./media/active-directory-azure-ad-controls-how-to-review-your-access/new-ar-email.png)

If you don't have the email, you can locate the access reviews by following these steps:

1. Sign in on the [Azure AD access panel](https://myapps.microsoft.com).

2. Select the user symbol in the upper-right corner of the page, which displays your name and default organization. If more than one organization is listed, select the organization that requested an access review.

3. If a tile labeled **Access reviews** is on the right side of the page, select it. If the tile isn't visible, there are no access reviews to perform for that organization and no action is needed at this time.

## <a name="fill-out-an-access-review"></a>Fill out an access review

When you select an access review from the list, you can see your access. Select the row, and choose whether to approve or deny your need for continued access.

The reviewer might require that you supply a justification for approving continued access.

## <a name="next-steps"></a>Next steps

Denied access isn't removed immediately. If you want to change your answer and approve, reset the response and select a new response. You can do this step until the access review is finished.






