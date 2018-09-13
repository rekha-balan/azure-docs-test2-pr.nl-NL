---
title: Sign-in activity reports in the Azure Active Directory portal - preview | Microsoft Docs
description: Introduction to sign-in activity reports in the Azure Active Directory portal - preview
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: 3fc69bd579a9c31cf45aebf640e500c01dde43b0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553876"
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal---preview"></a>Sign-in activity reports in the Azure Active Directory portal - preview

With reporting in the Azure Active Directory [preview](active-directory-preview-explainer.md), you get all the information you need to determine how your environment is doing.

The reporting architecture in Azure Active Directory consists of the following components:

- **Activity** 
    - **Sign-in activities** – Information about the usage of managed applications and user sign-in activities
    - **Audit logs** - System activity information about users and group management, your managed applications and directory activities.
- **Security** 
    - **Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account. For more details, see Risky sign-ins.
    - **Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised. For more details, see Users flagged for risk.

This topic gives you an overview of the sign-in activities.

## <a name="signs-in-activities"></a>Signs-in activities

With the information provided by the user sign-in report, you find answers to questions such as:

* What is the sign-in pattern of a user?
* How many users have users signed in over a week?
* What’s the status of these sign-ins?

Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**. Directory.


![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")


An audit log has a default list view that shows:

- the related user
- the application the user has signed-in to
- the sign-in status
- the sign-in time

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")

You can customize the list view by clicking **Columns** in the toolbar.

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")

This enables you to display additional fields or remove fields that are already displayed.

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")

By clicking an item in the list view, you get all available details about it.

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")


## <a name="filtering-sign-in-activities"></a>Filtering sign-in activities

To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:

- Time interval
- User
- Application
- Client
- Sign-in status

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")


The **time interval** filter enables to you to define a timeframe for the returned data.  
Possible values are:

- 1 month
- 7 days
- 24 hours
- Custom

When you select a custom timeframe, you can configure a start time and an end time.

The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.

The **application** filter enables you to specify the name of the application you care about.

The **client** filter enables you to specify information about the device you care about.

The **sign-in status** filter enables you to select one of the following filter:

- All
- Success
- Failure


## <a name="sign-in-activities-shortcuts"></a>Sign-in activities shortcuts

In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:

- Users and groups
- Enterprise applications


### <a name="users-and-groups-sign-ins-activities"></a>Users and groups sign-ins activities

With the information provided by the user sign-in report, you find answers to questions such as:

- What is the sign-in pattern of a user?
- How many users have users signed in over a week?
- What’s the status of these sign-ins?



Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")

The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period. The default for the time period is 30 days.

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")

When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")

Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:

* Who has signed in?
* What was the related UPN?
* What application was the target of the sign-in?
* What is the IP address of the sign-in?
* What was the status of the sign-in?

The **Sign-ins** option gives you a complete overview of all user sign-ins.

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")



## <a name="usage-of-managed-applications"></a>Usage of managed applications

With an application-centric view of your sign-in data, you can answer questions such as:

* Who is using my applications?
* What are the top 3 applications in your organization?
* I have recently rolled out an application. How is it doing?

Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")

The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period. The default for the time period is 30 days.

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")

If you want to, you can set the focus on a specific application.


![Reporting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")

When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.


![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")


The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.

![Sign-in activity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")



## <a name="next-steps"></a>Next steps
See the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).
















