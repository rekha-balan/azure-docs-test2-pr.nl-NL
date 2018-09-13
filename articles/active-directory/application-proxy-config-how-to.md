---
title: How to configure an Application Proxy application | Microsoft Docs
description: Learn how to create an configure an APplication Proxy application in a few simple steps
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: c1c026347d6b72ee255bb46b43566bcb9d266007
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556619"
---
# <a name="how-to-configure-an-application-proxy-application"></a>How to configure an Application Proxy application

This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.

## <a name="recommended-documents"></a>Recommended documents 

To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).

For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).

## <a name="create-the-applicationsetting-the-urls"></a>Create the Application/Setting the URLs

If you are following the steps in the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application. Most error messages include a suggested fix. To avoid common errors, verify:

-   You are an administrator with permission to create an Application Proxy application

-   The internal URL is unique

-   The external URL is unique

-   The URLs start with http or https, and end with a “/”

-   The URL should be a domain name, not an IP address

The error message should display in the top right corner when you create the application. You can also select the notification icon to see the error messages.

   ![Notification prompt](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>Configure connectors/connector groups

If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors. If you want to learn more about connectors, see the [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).

If your connectors are inactive, this means that they are unable to reach the service. This is often because all the required ports are not open. To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.

## <a name="upload-certificates-for-custom-domains"></a>Upload certificates for custom domains

Custom Domains allow you to specify the domain of your external URLs. To use custom domains, you need to upload the certificate for that domain. For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains). 

If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate. Common certificate problems include:

-   Expired certificate

-   Certificate is self-signed

-   Certificate is missing the private key

The error message display in the top right corner as you try to upload the certificate. You can also select the notification icon to see the error messages.

   ![Notification prompt](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>Next steps
[Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md)


