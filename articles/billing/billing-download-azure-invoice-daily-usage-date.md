---
title: Download Azure billing invoice and daily usage data | Microsoft Docs
description: Describes how to download or view your Azure billing invoice and daily usage data.
keywords: billing invoice,invoice download,azure invoice,azure usage
services: ''
documentationcenter: ''
author: genlin
manager: ruchic
editor: ''
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 69e2a882b14a8d16058ca7b747baa9e86297d733
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554555"
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>Download or view your Azure billing invoice and daily usage data
You can download your invoice from the [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) or have it sent in email. To download your daily usage, go to the [Azure Account Center](https://account.windowsazure.com). Only the Account Administrator has permission to get to the billing invoice and usage information. To find out who is the Account Administrator of the subscription, see the [Transferring ownership of an Azure subscription - FAQ](billing-subscription-transfer.md#faq).

## <a name="get-your-invoice-in-email-pdf"></a>Get your invoice in email (.pdf)
You can opt in and configure additional recipients to receive your Azure invoice in an email. This feature may not be available for certain subscriptions such as support offers, Enterprise Agreements, or Azure in Open.

1. Select your subscription from the [subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade). Opt-in for each subscription you own. Click **Invoices** then **Email my invoice**. 

    ![Screenshot that shows the opt-in flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. Click **Opt in** and accept the terms:

    ![Screenshot that shows the opt-in flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. Once you've accepted the agreement, you can configure additional recipients:

    ![Screenshot that shows the opt-in flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
If you don't get an email after following the steps, make sure your email address is correct in the [communication preferences on your profile](https://account.windowsazure.com/profile).


## <a name="download-invoice-from-azure-portal-pdf"></a>Download invoice from Azure portal (.pdf)

1. Sign in to the [Azure portal](https://portal.azure.com) as the Account Administrator. 
2. On the Hub menu, select **Subscriptions**. 

    ![Screenshot that shows the Subscription option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/submenu.png) 

3. In the **Subscriptions** blade, select the subscription that you want to view, and then select **Billing & usage**. 

    ![Screenshot that shows the Billing & usage option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

4. On the **Billing & usage** blade, click **Download Invoice** to view a copy of your pdf invoice. 

    ![Screenshot that shows billing periods, the download option, and total charges for each billing period](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/billing4.png)

5. You can view your daily usage by clicking the billing period. 

For more information about your invoice, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md). For help managing costs, see [Prevent unexpected costs with Azure billing and cost management](billing-getting-started.md).

## <a name="download-usage-from-the-account-center-csv"></a>Download usage from the Account Center (.csv)
1. Sign into the [Azure Account Center](https://account.windowsazure.com/subscriptions) as the Account Administrator.
2. Select the subscription for which you want the invoice and usage information.
3. Select **BILLING HISTORY**. 

    ![Screenshot that shows billing history option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. You can see your statements for the last six billing periods and the current unbilled period. 

    ![Screenshot that shows billing periods, options to download invoice and daily usage, and total charges for each billing period](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. Select **View Current Statement** to see an estimate of your charges at the time the estimate was generated. This information is only updated daily and may not include all your usage. Your monthly invoice may differ from this estimate.

    ![Screenshot that shows the View Current Statement option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Screenshot that shows the estimate of current charges](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. Select **Download Usage** to download the daily usage data as a CSV file. If you see two versions available, download version 2.

    ![Screenshot that shows the Download Usage option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

For more information about your daily usage, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md). For help managing costs, see [Prevent unexpected costs with Azure billing and cost management](billing-getting-started.md).

## <a name="noinvoice"></a> Why don't I see an invoice for the last billing period?
There could be several reasons that you don't see an invoice:
- You have a monthly credit amount with your subscription that you didn't exceed or you have a Free Trial. An invoice is only generated when you owe money.
- It's less than 30 days from the day you subscribed to Azure.
- The invoice isn't generated yet. Wait until the end of the billing period.

## <a name="need-help-contact-support"></a>Need help? Contact support.
If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.












