---
title: Post an announcment to a lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to add an announcement to a lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.assetid: 67a09946-4584-425e-a94c-abe57c9cbb82
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: ecfaf24d1122b711a93e1335b79acbbc4235bdae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855722"
---
# <a name="post-an-announcement-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="02d15-103">Post an announcement to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="02d15-103">Post an announcement to a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="02d15-104">As a lab administrator, you can post a custom announcement in an existing lab to notify users about recent changes or additions to the lab.</span><span class="sxs-lookup"><span data-stu-id="02d15-104">As a lab administrator, you can post a custom announcement in an existing lab to notify users about recent changes or additions to the lab.</span></span> <span data-ttu-id="02d15-105">For example, you might want to inform users about:</span><span class="sxs-lookup"><span data-stu-id="02d15-105">For example, you might want to inform users about:</span></span>

- <span data-ttu-id="02d15-106">New VM sizes that are available</span><span class="sxs-lookup"><span data-stu-id="02d15-106">New VM sizes that are available</span></span>
- <span data-ttu-id="02d15-107">Images that are currently unusable</span><span class="sxs-lookup"><span data-stu-id="02d15-107">Images that are currently unusable</span></span>
- <span data-ttu-id="02d15-108">Updates to lab policies</span><span class="sxs-lookup"><span data-stu-id="02d15-108">Updates to lab policies</span></span>

<span data-ttu-id="02d15-109">Once posted, the announcement is displayed on the lab's Overview page and the user can select it for more details.</span><span class="sxs-lookup"><span data-stu-id="02d15-109">Once posted, the announcement is displayed on the lab's Overview page and the user can select it for more details.</span></span>

<span data-ttu-id="02d15-110">The announcement feature is meant to be used for temporary notifications.</span><span class="sxs-lookup"><span data-stu-id="02d15-110">The announcement feature is meant to be used for temporary notifications.</span></span>  <span data-ttu-id="02d15-111">You can easily disable an announcement after it is no longer needed.</span><span class="sxs-lookup"><span data-stu-id="02d15-111">You can easily disable an announcement after it is no longer needed.</span></span>

## <a name="steps-to-post-an-announcement-in-an-existing-lab"></a><span data-ttu-id="02d15-112">Steps to post an announcement in an existing lab</span><span class="sxs-lookup"><span data-stu-id="02d15-112">Steps to post an announcement in an existing lab</span></span>

1. <span data-ttu-id="02d15-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="02d15-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="02d15-114">If necessary, select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="02d15-114">If necessary, select **All Services**, and then select **DevTest Labs** from the list.</span></span> <span data-ttu-id="02d15-115">(Your lab might already be shown on the Dashboard under **All Resources**).</span><span class="sxs-lookup"><span data-stu-id="02d15-115">(Your lab might already be shown on the Dashboard under **All Resources**).</span></span>
1. <span data-ttu-id="02d15-116">From the list of labs, select the lab in which you want to post an announcement.</span><span class="sxs-lookup"><span data-stu-id="02d15-116">From the list of labs, select the lab in which you want to post an announcement.</span></span>  
1. <span data-ttu-id="02d15-117">On the lab's **Overview** area, select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="02d15-117">On the lab's **Overview** area, select **Configuration and policies**.</span></span>  

    ![Configuration and policies button](./media/devtest-lab-announcements/devtestlab-config-and-policies.png)

1. <span data-ttu-id="02d15-119">On the left under **SETTINGS**, select **Lab announcement**.</span><span class="sxs-lookup"><span data-stu-id="02d15-119">On the left under **SETTINGS**, select **Lab announcement**.</span></span>

    ![Lab announcement button](./media/devtest-lab-announcements/devtestlab-announcements.png)

1. <span data-ttu-id="02d15-121">To create a message for the users in this lab, set **Enabled** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="02d15-121">To create a message for the users in this lab, set **Enabled** to **Yes**.</span></span>

1. <span data-ttu-id="02d15-122">You can enter an **Expiration date** to specify a date and time after which the announcement is no longer shown to users.</span><span class="sxs-lookup"><span data-stu-id="02d15-122">You can enter an **Expiration date** to specify a date and time after which the announcement is no longer shown to users.</span></span> <span data-ttu-id="02d15-123">If you don't enter an expiration date, the announcement remains until you disable it.</span><span class="sxs-lookup"><span data-stu-id="02d15-123">If you don't enter an expiration date, the announcement remains until you disable it.</span></span>

   > [!NOTE]
   > <span data-ttu-id="02d15-124">After the announcement expires, it is no longer shown to users, but still exists in the **Lab announcement** pane.</span><span class="sxs-lookup"><span data-stu-id="02d15-124">After the announcement expires, it is no longer shown to users, but still exists in the **Lab announcement** pane.</span></span> <span data-ttu-id="02d15-125">You can make edits to it and re-enable it to make it active again.</span><span class="sxs-lookup"><span data-stu-id="02d15-125">You can make edits to it and re-enable it to make it active again.</span></span>
   >
   >

1. <span data-ttu-id="02d15-126">Enter an **Announcement title** and the **Announcement text**.</span><span class="sxs-lookup"><span data-stu-id="02d15-126">Enter an **Announcement title** and the **Announcement text**.</span></span>

   <span data-ttu-id="02d15-127">The title can be up to 100 characters and is shown to the user on the lab's Overview page.</span><span class="sxs-lookup"><span data-stu-id="02d15-127">The title can be up to 100 characters and is shown to the user on the lab's Overview page.</span></span> <span data-ttu-id="02d15-128">If the user selects the title, the announcement text is displayed.</span><span class="sxs-lookup"><span data-stu-id="02d15-128">If the user selects the title, the announcement text is displayed.</span></span>

   <span data-ttu-id="02d15-129">The announcement text accepts markdown.</span><span class="sxs-lookup"><span data-stu-id="02d15-129">The announcement text accepts markdown.</span></span> <span data-ttu-id="02d15-130">As you enter the announcement text, you can view the message in the Preview area at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="02d15-130">As you enter the announcement text, you can view the message in the Preview area at the bottom of the screen.</span></span>

    ![Lab announcement screen to create the message.](./media/devtest-lab-announcements/devtestlab-post-announcement.png)


1. <span data-ttu-id="02d15-132">Select **Save** once your announcement is ready to post.</span><span class="sxs-lookup"><span data-stu-id="02d15-132">Select **Save** once your announcement is ready to post.</span></span>

<span data-ttu-id="02d15-133">When you no longer want to show this announcement to lab users, return to the **Lab announcement** page and set **Enabled** to **No**.</span><span class="sxs-lookup"><span data-stu-id="02d15-133">When you no longer want to show this announcement to lab users, return to the **Lab announcement** page and set **Enabled** to **No**.</span></span> <span data-ttu-id="02d15-134">If you specified an expiration date, the announcement is disabled automatically at that date and time.</span><span class="sxs-lookup"><span data-stu-id="02d15-134">If you specified an expiration date, the announcement is disabled automatically at that date and time.</span></span>

## <a name="steps-for-users-to-view-an-announcement"></a><span data-ttu-id="02d15-135">Steps for users to view an announcement</span><span class="sxs-lookup"><span data-stu-id="02d15-135">Steps for users to view an announcement</span></span>

1. <span data-ttu-id="02d15-136">From the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), select a lab.</span><span class="sxs-lookup"><span data-stu-id="02d15-136">From the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), select a lab.</span></span>

1. <span data-ttu-id="02d15-137">If the lab has an announcement posted for it, an information notice is shown at the top of the lab's Overview page.</span><span class="sxs-lookup"><span data-stu-id="02d15-137">If the lab has an announcement posted for it, an information notice is shown at the top of the lab's Overview page.</span></span> <span data-ttu-id="02d15-138">This information notice is the announcement title that was specified when the announcement was created.</span><span class="sxs-lookup"><span data-stu-id="02d15-138">This information notice is the announcement title that was specified when the announcement was created.</span></span>

    ![Lab announcement on Overview page](./media/devtest-lab-announcements/devtestlab-user-announcement.png)

1. <span data-ttu-id="02d15-140">The user can select the message to view the entire announcement.</span><span class="sxs-lookup"><span data-stu-id="02d15-140">The user can select the message to view the entire announcement.</span></span>

    ![More information for the lab announcement](./media/devtest-lab-announcements/devtestlab-user-announcement-text.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="azure-resource-manager-template"></a><span data-ttu-id="02d15-142">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="02d15-142">Azure Resource Manager template</span></span>
<span data-ttu-id="02d15-143">You can specify an announcement as part of an Azure Resource Manager template as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="02d15-143">You can specify an announcement as part of an Azure Resource Manager template as shown in the following example:</span></span> 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "name": {
            "type": "string",
            "defaultValue": "devtestlabfromarm"
        },
        "regionId": {
            "type": "string",
            "defaultValue": "eastus"
        }
    },
    "resources": [
        {
            "apiVersion": "2017-04-26-preview",
            "name": "[parameters('name')]",
            "type": "Microsoft.DevTestLab/labs",
            "location": "[parameters('regionId')]",
            "tags": {},
            "properties": {
                "labStorageType": "Premium",
                "announcement":
                {
                    "title": "Important! Three images are currently inaccessible. Click for more information.",
                    "markdown":"# Images are inaccessible\n\nThe following 3 images are currently not available for use: \n\n- image1\n- image2\n- image3\n\nI am working to fix the problem ASAP.",
                    "enabled": "Enabled",
                    "expirationDate":"2018-12-31T06:00:00+00:00",
                    "expired": "false"
                },
                "support": {
                    "markdown": "",
                    "enabled": "Enabled"
                }                
            },
            "resources": [
                {
                    "apiVersion": "2017-04-26-preview",
                    "name": "LabVmsShutdown",
                    "location": "[parameters('regionId')]",
                    "type": "schedules",
                    "dependsOn": [
                        "[resourceId('Microsoft.DevTestLab/labs', parameters('name'))]"
                    ],
                    "properties": {
                        "status": "Enabled",
                        "timeZoneId": "Eastern Standard Time",
                        "dailyRecurrence": {
                            "time": "1900"
                        },
                        "taskType": "LabVmsShutdownTask",
                        "notificationSettings": {
                            "status": "Disabled",
                            "timeInMinutes": 30
                        }
                    }
                },
                {
                    "apiVersion": "2017-04-26-preview",
                    "name": "[concat('Dtl', parameters('name'))]",
                    "type": "virtualNetworks",
                    "location": "[parameters('regionId')]",
                    "dependsOn": [
                        "[resourceId('Microsoft.DevTestLab/labs', parameters('name'))]"
                    ]
                }
            ]
        }
    ]
}
```

<span data-ttu-id="02d15-144">You can deploy an Azure Resource Manager template by using one of the following ways:</span><span class="sxs-lookup"><span data-stu-id="02d15-144">You can deploy an Azure Resource Manager template by using one of the following ways:</span></span>

- [<span data-ttu-id="02d15-145">Azure portal</span><span class="sxs-lookup"><span data-stu-id="02d15-145">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
- [<span data-ttu-id="02d15-146">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="02d15-146">Azure PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
- [<span data-ttu-id="02d15-147">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="02d15-147">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
- [<span data-ttu-id="02d15-148">REST API</span><span class="sxs-lookup"><span data-stu-id="02d15-148">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

## <a name="next-steps"></a><span data-ttu-id="02d15-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="02d15-149">Next steps</span></span>
* <span data-ttu-id="02d15-150">If you change or set a lab policy, you might want to post an announcement to inform users.</span><span class="sxs-lookup"><span data-stu-id="02d15-150">If you change or set a lab policy, you might want to post an announcement to inform users.</span></span> <span data-ttu-id="02d15-151">[Set policies and schedules](devtest-lab-set-lab-policy.md) provides information about applying restrictions and conventions across your subscription by using customized policies.</span><span class="sxs-lookup"><span data-stu-id="02d15-151">[Set policies and schedules](devtest-lab-set-lab-policy.md) provides information about applying restrictions and conventions across your subscription by using customized policies.</span></span>
* <span data-ttu-id="02d15-152">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="02d15-152">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
