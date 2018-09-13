---
title: Getting started with Storage Explorer (Preview) | Microsoft Docs
description: Manage Azure storage resources with Storage Explorer (Preview)
services: storage
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: tarcher
ms.openlocfilehash: caad415589f6fb947c76da8df50dddfbe6570109
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550999"
---
# <a name="getting-started-with-storage-explorer-preview"></a>Getting started with Storage Explorer (Preview)
## <a name="overview"></a>Overview
Microsoft Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux. In this article, you learn the various ways of connecting to and managing your Azure storage accounts.

![Microsoft Azure Storage Explorer (Preview)][15]

## <a name="prerequisites"></a>Prerequisites
* [Download and install Storage Explorer (preview)](http://www.storageexplorer.com)

## <a name="connect-to-a-storage-account-or-service"></a>Connect to a storage account or service
Storage Explorer (Preview) provides a number of ways to connect to storage accounts. This includes connecting to storage accounts associated with your Azure subscriptions, connecting to storage accounts and services shared from other Azure subscriptions, and even connecting to and managing local storage using the Azure Storage Emulator. In addition, you can work with storage accounts in global and national Azure:

* [Connect to an Azure subscription](#connect-to-an-azure-subscription) - Manage storage resources belonging to your Azure subscription.
* [Work with local development storage](#work-with-local-development-storage) - Manage local storage using the Azure Storage Emulator.
* [Attach to external storage](#attach-or-detach-an-external-storage-account) - Manage storage resources belonging to another Azure subscription or under national Azure clouds using the storage account's name, key, and endpoints.
* [Attach storage account using SAS](#attach-storage-account-using-sas) - Manage storage resources belonging to another Azure subscription using a SAS.
* [Attach service using SAS](#attach-service-using-sas) - Manage a specific storage service (blob container, queue, or table) belonging to another Azure subscription using a SAS.

## <a name="connect-to-an-azure-subscription"></a>Connect to an Azure subscription
> [!NOTE]
> If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. In Storage Explorer (Preview), select **Azure Account settings**.

    ![Azure account settings][0]
2. The left pane displays all the Microsoft accounts you've logged in to. To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.
> [!NOTE]
>Connecting to national Azure such as Black Forest Azure, Fairfax Azure, and Mooncake Azure via sign-in is currently not supported. See **Attach or detach an external storage account** section for how to connect to national Azure storage accounts.

3. Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account. Select the Azure subscriptions with which you want to work, and then select **Apply**. (Selecting **All subscriptions** toggles selecting all or none of the listed Azure subscriptions.)

    ![Select Azure subscriptions][3]
4. The left pane displays the storage accounts associated with the selected Azure subscriptions.

    ![Selected Azure subscriptions][4]

## <a name="connect-to-an-azure-stack-subscription"></a>Connect to an Azure Stack subscription

1. VPN connection is needed for Storage Explorer to access Azure Stack subscription remotely. To learn about how to set up VPN connection to Azure Stack, refer to [Connect to Azure Stack with VPN](azure-stack/azure-stack-connect-azure-stack.md#connect-with-vpn)

2. For Azure Stack POC, you need to export Azure Stack authority root certificate. Open `mmc.exe` on MAS-CON01, Azure Stack host machine or local machine with VPN connection to Azure Stack. In **File**, select **Add/Remove Snap-in**, add **Certificates** to manage **Computer account** of **Local Computer**.

   ![Load the Azure stack root certificate through mmc.exe][25]   

   Find **AzureStackCertificationAuthority** under **Console Root\Certificated (Local Computer)\Trusted Root Certification Authorities\Certificates**. Right click on item, select **All Tasks -> Export**. Then follow the dialogs to export certificate with **Base-64 encoded X.509 (.CER)**. The exported certificate will be used in the next step.   

   ![Export the root Azure stack authority root certificate][26]   

3. In Storage Explorer (Preview), select the **Edit** menu, then **SSL Certificates**, then **Import Certificates**. Use the file picker dialog to find and open the certificate you explored in the previous step. After importing you will be prompted to restart Storage Explorer.

   ![Import the certificate into Storage Explorer (Preview)][27]

4. Once Storage Explorer (Preview) relaunches, select the **Edit** menu, and ensure **Target Azure Stack** is checked. If not, check it and restart Storage Explorer for the change to take effect. This configuration is required for  compatible with your Azure Stack environment.

   ![Ensure Target Azure Stack is selected][28]

5. On left side bar, select **Manage Accounts**. The left pane displays all the Microsoft accounts you are logged into. To connect to Azure Stack account, select **Add an account**.

   ![Add an Azure stack account][29]

6. Choose **Create Custom Environment** in under **Azure environment** in the **Add new account** dialog, then click **Next**.

7. Input all required information of Azure Stack custom environment, then click **Sign in**.  Fill in the **Sign in to a Custom Cloud environment** dialog to sign in with Azure Stack account that is associated with at least one active Azure Stack subscription. Details for each field on the dialog are as follows:

    * **Environment name** – The field can be customized by user.
    * **Authority** – The value should be https://login.windows.net. For Azure China (Mooncake), please use https://login.chinacloudapi.cn.
    * **Sign in resource id** – Retrieve the value by executing the following PowerShell:

    If you are Cloud Administrator:

    ```powershell
    PowerShell (Invoke-RestMethod -Uri https://adminmanagement.local.azurestack.external/metadata/endpoints?api-version=1.0 -Method Get).authentication.audiences[0]
    ```

    If you are Tenant:

    ```powershell
    PowerShell (Invoke-RestMethod -Uri https://management.local.azurestack.external/metadata/endpoints?api-version=1.0 -Method Get).authentication.audiences[0]
    ```

    * **Graph endpoint** – The value should be https://graph.windows.net. For Azure China (Mooncake), please use https://graph.chinacloudapi.cn.
    * **ARM resource id** – Use the same value as Sign in resource id.
    * **ARM resource endpoint** – The samples of ARM resource endpoint:

    For Cloud Administrator: https://adminmanagement.local.azurestack.external   
    For Tenant: https://management.local.azurestack.external
 
    * **Tenant Ids** – Optional. The value is given only when the directory must be specified.

8. Once you successfully sign in with an Azure Stack account, the left pane populates with the Azure Stack subscriptions associated with that account. Select the Azure Stack subscriptions with which you want to work, and then select **Apply**. (Selecting **All subscriptions** toggles selecting all or none of the listed Azure Stack subscriptions.)

   ![Select the Azure stack subscriptions after filling out the Custom Cloud Environment dialog][30]

9. The left pane displays the storage accounts associated with the selected Azure Stack subscriptions.

   ![List of storage accounts including Azure stack subscription accounts][31]

## <a name="work-with-local-development-storage"></a>Work with local development storage
Storage Explorer (Preview) enables you to work against local storage using the Azure Storage Emulator. This allows you to write code against and test storage without necessarily having a storage account deployed on Azure (since the storage account is being emulated by the Azure Storage Emulator).

> [!NOTE]
> The Azure Storage Emulator is currently supported only for Windows.
>
>

1. In the left pane of Storage Explorer (Preview), expand the **(Local and Attached** > **Storage Accounts** > **(Development)** node.

    ![Local development node][21]
2. If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an infobar. If the infobar is displayed, select **Download the latest version**, and install the emulator.

    ![Download Azure Storage Emulator prompt][22]
3. Once the emulator is installed, you have the ability to create and work with local blobs, queues, and tables. To learn how to work with each storage account type, select one of the following links:

   * [Manage Azure blob storage resources](vs-azure-tools-storage-explorer-blobs.md)
   * Manage Azure file share storage resources - *Coming soon*
   * Manage Azure queue storage resources - *Coming soon*
   * Manage Azure table storage resources - *Coming soon*

## <a name="attach-or-detach-an-external-storage-account"></a>Attach or detach an external storage account
Storage Explorer (Preview) provides the ability to attach to external storage accounts so that storage accounts can be easily shared. This section explains how to attach to (and detach from) external storage accounts.

### <a name="get-the-storage-account-credentials"></a>Get the storage account credentials
To share an external storage account, the owner of that account must first get the credentials - account name and key - for the account and then share that information with the person wanting to attach to that (external) account. Obtaining the storage account credentials can be done via the Azure portal by following these steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select **Browse**.
3. Select **Storage Accounts**.
4. In the **Storage Accounts** blade, select the desired storage account.
5. In the **Settings** blade for the selected storage account, select **Access keys**.

   ![Access Keys option][5]
6. In the **Access keys** blade, copy the **STORAGE ACCOUNT NAME** and **KEY 1** values for use when attaching to the storage account.

   ![Access keys][6]

### <a name="attach-to-an-external-storage-account"></a>Attach to an external storage account
To attach to an external storage account, you need the account's name and key. The section *Get the storage account credentials* explains how to obtain these values from the Azure portal. However, note that in the portal, the account key is called "key 1" so where the Storage Explorer (Preview) asks for an account key, you'll enter (or paste) the "key 1" value.

1. In Storage Explorer (Preview), select **Connect to Azure storage**.

   ![Connect to Azure storage option][23]
2. On the **Connect to Azure Storage** dialog, specify the account key ("key 1" value from the Azure portal), and then select **Next**.
> [!NOTE]
> You can enter Storage Connection string from a storage account on national Azure. For example, enter connection strings similar to the following to connect to Azure Black Forest storage accounts: DefaultEndpointsProtocol=https;AccountName=cawatest03;AccountKey=<storage_account_key>;EndpointSuffix=core.cloudapi.de; You can get the connection string from Azure portal in the same way as described in the **Get the storage account credentials** section

   ![Connect to Azure storage dialog][24]

3. In the **Attach External Storage** dialog, enter the storage account name in the **Account name** box, specify any other desired settings, and select **Next** when done.

   ![Attach external storage dialog][8]
4. In the **Connection Summary** dialog, verify the information. If you want to change anything, select **Back** and reenter the desired settings. Once finished, select **Connect**.
5. Once connected, the external storage account is displayed with the text **(External)** appended to the storage account name.

   ![Result of connecting to an external storage account][9]

### <a name="detach-from-an-external-storage-account"></a>Detach from an external storage account
1. Right-click the external storage account you want to detach, and - from the context menu - select **Detach**.

   ![Detach from storage option][10]
2. When the confirmation message box appears, select **Yes** to confirm the detachment from the external storage account.

## <a name="attach-storage-account-using-sas"></a>Attach storage account using SAS
A [SAS (Shared Access Signature)](storage/storage-dotnet-shared-access-signature-part-1.md) gives the admin of an Azure subscription the ability to grant access to a storage account on a temporary basis without having to provide their Azure subscription credentials.

To illustrate this, let's say UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:

1. UserA generates a SAS (consisting of the connection string for the storage account) for a specific time period and with the desired permissions.
2. UserA shares the SAS with the person wanting access to the storage account - UserB, in our example.  
3. UserB uses Storage Explorer (Preview) to attach to the account belonging to UserA using the supplied SAS.

### <a name="get-a-sas-for-the-account-you-want-to-share"></a>Get a SAS for the account you want to share
1. In Storage Explorer (Preview), right-click the storage account you want share, and - from the context menu - select **Get Shared Access Signature**.

   ![Get SAS context menu option][13]
2. On the **Shared Access Signature** dialog, specify the time frame and permissions you want for the account, and select **Create**.

    ![Get SAS dialog][14]
3. A second **Shared Access Signature** dialog displays the SAS. Select **Copy** next to the **Connection String** to copy it to the clipboard. Select **Close** to dismiss the dialog.

### <a name="attach-to-the-shared-account-using-the-sas"></a>Attach to the shared account using the SAS
1. In Storage Explorer (Preview), select **Connect to Azure storage**.

   ![Connect to Azure storage option][23]
2. On the **Connect to Azure Storage** dialog, specify the connection string, and then select **Next**.

   ![Connect to Azure storage dialog][24]
3. In the **Connection Summary** dialog, verify the information. If you want to change anything, select **Back** and reenter the desired settings. Once finished, select **Connect**.
4. Once attached, the storage account displays with the text (SAS) appended to the account name you supplied.

   ![Result of attached to an account using SAS][17]

## <a name="attach-service-using-sas"></a>Attach service using SAS
The section [Attach storage account using SAS](#attach-storage-account-using-sas) illustrates how an Azure subscription admin can grant temporary access to a storage account by generating (and sharing) a SAS for the storage account. Similarly, a SAS can be generated for a specific service (blob container, queue, or table) within a storage account.  

### <a name="generate-a-sas-for-the-service-you-want-to-share"></a>Generate a SAS for the service you want to share
In this context, a service can be a blob container, queue, or table. The following sections explain how to generate the SAS for the listed service:

* [Get the SAS for a blob container](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Get the SAS for a file share - *Coming soon*
* Get the SAS for a queue - *Coming soon*
* Get the SAS for a table - *Coming soon*

### <a name="attach-to-the-shared-account-service-using-the-sas"></a>Attach to the shared account service using the SAS
1. In Storage Explorer (Preview), select **Connect to Azure storage**.

   ![Connect to Azure storage option][23]
2. On the **Connect to Azure Storage** dialog, specify the SAS URI, and then select **Next**.

   ![Connect to Azure storage dialog][24]
3. In the **Connection Summary** dialog, verify the information. If you want to change anything, select **Back** and reenter the desired settings. Once finished, select **Connect**.
4. Once attached, the newly attached service displays under the **(Service SAS)** node.

   ![Result of attaching to a shared service using SAS][20]

## <a name="search-for-storage-accounts"></a>Search for storage accounts
If you have a long list of storage accounts, a quick way to locate a particular storage account is to use the search box at the top of the left pane.

As you are typing into the search box, the left pane displays only the storage accounts that match the search value you've entered up to that point. The following screen shot illustrates an example where I've searched for all storage accounts where the storage account name contains the text "tarcher".

![Storage account search][11]

To clear the search, select the **x** button in the search box.

## <a name="next-steps"></a>Next steps
* [Manage Azure blob storage resources with Storage Explorer (Preview)](vs-azure-tools-storage-explorer-blobs.md)

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png



























