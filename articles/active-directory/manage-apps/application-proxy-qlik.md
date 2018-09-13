---
title: Azure AD App Proxy and Qlik Sense| Microsoft Docs
description: Turn on Application Proxy in the Azure  portal, and install the Connectors for the reverse proxy.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.topic: article
ms.date: 09/06/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5f103e9fe410374a551eb43d456d5993bdd36627
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855566"
---
# <a name="application-proxy-and-qlik-sense"></a>Application Proxy and Qlik Sense 
Azure Active Directory Application Proxy and Qlik Sense have partnered together to ensure you are easily able to use Application Proxy to provide remote access for your Qlik Sense deployment.  

## <a name="prerequisites"></a>Prerequisites 
The remainder of this scenario assumes you done the following:
 
- Configured [Qlik Sense](https://community.qlik.com/docs/DOC-19822). 
- [Installed an Application Proxy connector](application-proxy-enable.md#install-and-register-a-connector) 
 
## <a name="publish-your-applications-in-azure"></a>Publish your applications in Azure 
To publish QlikSense, you will need to publish two applications in Azure.  

### <a name="application-1"></a>Application #1: 
Follow these steps to publish your app. For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md). 


1. Sign in to the Azure portal as a global administrator. 
2. Select **Azure Active Directory** > **Enterprise applications**. 
3. Select **Add** at the top of the blade. 
4. Select **On-premises application**. 
5.       Fill out the required fields with information about your new app. Use the following guidance for the settings: 
    - **Internal URL**: This application should have an internal URL that is the QlikSense URL itself. For example, **https&#58;//demo.qlikemm.com:4244** 
    - **Pre-authentication method**: Azure Active Directory (Recommended but not required) 
1.       Select **Add** at the bottom of the blade. Your application is added, and the quick start menu opens. 
2.       In the quick start menu, select **Assign a user for testing**, and add at least one user to the application. Make sure this test account has access to the on-premises application. 
3.       Select **Assign** to save the test user assignment. 
4.       (Optional) On the app management blade, select Single sign-on. Choose **Kerberos Constrained Delegation** from the drop-down menu, and fill out the required fields based on your Qlik configuration. Select **Save**. 

### <a name="application-2"></a>Application #2: 
Follow the same steps as for Application #1, with the following exceptions: 

**Step #5**: The Internal URL should now be the QlikSense URL with the authentication port used by the application. The default is **4244** for HTTPS, and 4248 for HTTP. Ex: **https&#58;//demo.qlik.com:4244**</br></br> 
**Step #10:** Don’t set up SSO, and leave the **Single sign-on disabled**
 
 
## <a name="testing"></a>Testing 
Your application is now ready to test. Access the external URL you used to publish QlikSense in Application #1, and login as a user assigned to both applications.  

## <a name="next-steps"></a>Next Steps

- [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md)
- [Working with Application Proxy connectors](application-proxy-connector-groups.md).
