---
title: Complete an access review for Azure resource roles in PIM | Microsoft Docs
description: Learn how to complete an access review for Azure resource roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 04/02/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: f998c509e9bea65980367690a5e9d03f579b8e98
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857827"
---
# <a name="complete-an-access-review-for-azure-resource-roles-in-pim"></a>Complete an access review for Azure resource roles in PIM
Privileged role administrators can review privileged access after an [access review has been started](pim-resource-roles-start-access-review.md). Privileged Identity Management (PIM) for Azure resources automatically sends an email that prompts users to review their access. If a user doesn't receive an email, you can send them the instructions for [how to perform an access review](pim-resource-roles-perform-access-review.md).

After the access review period is over, or after all the users have finished their self-review, follow the steps in this article to manage the review and see the results.

## <a name="manage-access-reviews"></a>Manage access reviews
1. Go to the [Azure portal](https://portal.azure.com/). Then, on the dashboard, select the **Azure resources** application.

2. Select your resource.

3. Select the **Access reviews** section of the dashboard.
![Access reviews](media/azure-pim-resource-rbac/rbac-access-review-home-list.png)

4. Select the access review that you want to manage.

On the detail blade of the access review, there are a number of options for managing that review. The options are as follows:

![Options for managing a review](media/azure-pim-resource-rbac/rbac-access-review-menu.png)

### <a name="stop"></a>Stop
All access reviews have an end date, but you can use the **Stop** button to finish it early. All users who haven't finished their review by this time won't be able to finish it after you stop the review. You can't restart a review after it's been stopped.

### <a name="reset"></a>Reset
You can reset an access review to remove all decisions that are made on it. After you've reset an access review, all users are marked as unreviewed again. 

### <a name="apply"></a>Apply
After an access review is complete, use the **Apply** button to implement the outcome of the review. If a user's access was denied in the review, this step removes their role assignment.  

### <a name="delete"></a>Delete
If you aren't interested in the review any more, delete it. The **Delete** button removes the review from the PIM application.

## <a name="results"></a>Results
On the **Results** tab, view and download a list of your review results. 
![Results tab](media/azure-pim-resource-rbac/rbac-access-review-results.png)

## <a name="reviewers"></a>Reviewers
View and add reviewers to your existing access review. Remind reviewers to complete their reviews.
![Add reviewers](media/azure-pim-resource-rbac/rbac-access-review-reviewers.png)

## <a name="next-steps"></a>Next steps

- [Start an access review for Azure resource roles in PIM](pim-resource-roles-start-access-review.md)
- [Perform an access review of my Azure resource roles in PIM](pim-resource-roles-perform-access-review.md)
