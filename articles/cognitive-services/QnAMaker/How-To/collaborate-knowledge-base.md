---
title: Collaborating on your knowledge base - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: How to collaborate on your QnA Maker knowledge base
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: e18d656236276595fc5186a6656349bf28974ead
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870374"
---
# <a name="collaborate-on-your-knowledge-base"></a>Collaborate on your knowledge base

QnA Maker allows multiple people to collaborate on a knowledge base. This feature is provided with the Azure [Role-Based Access Control](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-configure). 

Perform the following steps to share your QnA Maker service with someone:

1. Log in to the Azure portal, and go to your QnA Maker resource.

    ![QnA Maker resource list](../media/qnamaker-how-to-collaborate-knowledge-base/qnamaker-resource-list.PNG)

2. Go to the **Access Control (IAM)** tab.

    ![QnA Maker IAM](../media/qnamaker-how-to-collaborate-knowledge-base/qnamaker-iam.PNG)

3. Select **Add**.

    ![QnA Maker IAM add](../media/qnamaker-how-to-collaborate-knowledge-base/qnamaker-iam-add.PNG)

4. Select the **Owner** or the **Contributor** role.

    ![QnA Maker IAM add role](../media/qnamaker-how-to-collaborate-knowledge-base/qnamaker-iam-add-role.PNG)

5. Enter the email you want to share with, and press save.

    ![QnA Maker IAM add email](../media/qnamaker-how-to-collaborate-knowledge-base/qnamaker-iam-add-email.PNG)

Now when the person you shared your QnA Maker service with, logs into the [QnA Maker portal](https://qnamaker.ai) they can see all the knowledge bases in that service.

Remember, you cannot share a particular knowledge base in a QnA Maker service. If you want more granular access control, consider distributing your knowledge bases across different QnA Maker services.

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Test a knowledge base](./test-knowledge-base.md)
