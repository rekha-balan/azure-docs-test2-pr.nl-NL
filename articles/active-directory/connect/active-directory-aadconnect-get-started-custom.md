---
title: 'Azure AD Connect: Custom installation | Microsoft Docs'
description: This document details the custom installation options for Azure AD Connect. Use these instructions to install Active Directory through Azure AD Connect.
services: active-directory
keywords: what is Azure AD Connect, install Active Directory, required components for Azure AD
documentationcenter: ''
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/30/2017
ms.author: billmath
ms.openlocfilehash: 320348fa74e500b2bfb7a596aaa05a4adc8ae0c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669522"
---
# <a name="custom-installation-of-azure-ad-connect"></a>Custom installation of Azure AD Connect
Azure AD Connect **Custom settings** is used when you want more options for the installation. It is used if you have multiple forests or if you want to configure optional features not covered in the express installation. It is used in all cases where the [**express installation**](active-directory-aadconnect-get-started-express.md) option does not satisfy your deployment or topology.

Before you start installing Azure AD Connect, make sure to [download Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) and complete the pre-requisite steps in [Azure AD Connect: Hardware and prerequisites](active-directory-aadconnect-prerequisites.md). Also make sure you have required accounts available as described in [Azure AD Connect accounts and permissions](active-directory-aadconnect-accounts-permissions.md).

If customized settings does not match your topology, for example to upgrade DirSync, see [related documentation](#related-documentation) for other scenarios.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Custom settings installation of Azure AD Connect
### <a name="express-settings"></a>Express Settings
On this page, click **Customize** to start a customized settings installation.

### <a name="install-required-components"></a>Install required components
When you install the synchronization services, you can leave the optional configuration section unchecked and Azure AD Connect sets up everything automatically. It sets up a SQL Server 2012 Express LocalDB instance, create the appropriate groups, and assign permissions. If you wish to change the defaults, you can use the following table to understand the optional configuration options that are available.

![Required Components](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| Optional Configuration | Description |
| --- | --- |
| Use an existing SQL Server |Allows you to specify the SQL Server name and the instance name. Choose this option if you already have a database server that you would like to use. Enter the instance name followed by a comma and port number in **Instance Name** if your SQL Server does not have browsing enabled. |
| Use an existing service account |By default Azure AD Connect uses a virtual service account for the synchronization services to use. If you use a remote SQL server or use a proxy that requires authentication, you need to use a **managed service account** or use a service account in the domain and know the password. In those cases, enter the account to use. Make sure the user running the installation is an SA in SQL so a login for the service account can be created. See [Azure AD Connect accounts and permissions](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| Specify custom sync groups |By default Azure AD Connect creates four groups local to the server when the synchronization services are installed. These groups are: Administrators group, Operators group, Browse group, and the Password Reset Group. You can specify your own groups here. The groups must be local on the server and cannot be located in the domain. |

### <a name="user-sign-in"></a>User sign-in
After installing the required components, you are asked to select your users single sign-on method. The following table provides a brief description of the available options. For a full description of the sign-in methods, see [User sign-in](active-directory-aadconnect-user-signin.md).

![User Sign in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| Single Sign On option | Description |
| --- | --- |
| Password Sync |Users are able to sign in to Microsoft cloud services, such as Office 365, using the same password they use in their on-premises network. The users passwords are synchronized to Azure AD as a password hash and authentication occurs in the cloud. See [Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) for more information. |
|Pass-through Authentication (Preview)|Users are able to sign in to Microsoft cloud services, such as Office 365, using the same password they use in their on-premises network.  The users password is passed through to the on-premises Active Directory controller to be validated.
| Federation with AD FS |Users are able to sign in to Microsoft cloud services, such as Office 365, using the same password they use in their on-premises network.  The users are redirected to their on-premises AD FS instance to sign in and authentication occurs on-premises. |
| Do not configure |Neither feature is installed and configured. Choose this option if you already have a 3rd party federation server or another existing solution in place. |
|Enable Single Sign on|This options is available with both password sync and Pass-through authentication and provides a single sign on experience for desktop users on the corporate network.  See [Single sign-on](active-directory-aadconnect-sso.md) for more information. </br>Note for AD FS customers this option is not available because AD FS already offers the same level of single sign on.</br>(if PTA is not released at the same time)
|Sign On Option|This options is available for password sync customers and provides a single sign on experience for desktop users on the corporate network.  </br>See [Single sign-on](active-directory-aadconnect-sso.md) for more information. </br>Note for AD FS customers this option is not available because AD FS already offers the same level of single sign on.


### <a name="connect-to-azure-ad"></a>Connect to Azure AD
On the Connect to Azure AD screen, enter a global admin account and password. If you selected **Federation with AD FS** on the previous page, do not sign in with an account in a domain you plan to enable for federation. A recommendation is to use an account in the default **onmicrosoft.com** domain, which comes with your Azure AD directory.

This account is only used to create a service account in Azure AD and is not used after the wizard has completed.  
![User Sign in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/connectaad.png)

If your global admin account has MFA enabled, then you need to provide the password again in the sign-in popup and complete the MFA challenge. The challenge could be a providing a verification code or a phone call.  
![User Sign in MFA](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

The global admin account can also have [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) enabled.

If you receive an error and have problems with connectivity, then see [Troubleshoot connectivity problems](active-directory-aadconnect-troubleshoot-connectivity.md).

## <a name="pages-under-the-section-sync"></a>Pages under the section Sync

### <a name="connect-your-directories"></a>Connect your directories
To connect to your Active Directory Domain Service, Azure AD Connect needs the credentials of an account with sufficient permissions. You can enter the domain part in either NetBios or FQDN format, that is, FABRIKAM\syncuser or fabrikam.com\syncuser. This account can be a regular user account because it only needs the default read permissions. However, depending on your scenario, you may need more permissions. For more information, see [Azure AD Connect Accounts and permissions](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account)

![Connect Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/connectdir.png)

### <a name="azure-ad-sign-in-configuration"></a>Azure AD sign-in configuration
This page allows you to review the UPN domains present in on-premises AD DS and which have been verified in Azure AD. This page also allows you to configure the attribute to use for the userPrincipalName.

![Unverified domains](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
Review every domain marked **Not Added** and **Not Verified**. Make sure those domains you use have been verified in Azure AD. Click the Refresh symbol when you have verified your domains. For more information, see [add and verify the domain](../active-directory-add-domain.md)

**UserPrincipalName** - The attribute userPrincipalName is the attribute users use when they sign in to Azure AD and Office 365. The domains used, also known as the UPN-suffix, should be verified in Azure AD before the users are synchronized. Microsoft recommends to keep the default attribute userPrincipalName. If this attribute is non-routable and cannot be verified, then it is possible to select another attribute. You can for example select email as the attribute holding the sign-in ID. Using another attribute than userPrincipalName is known as **Alternate ID**. The Alternate ID attribute value must follow the RFC822 standard. An Alternate ID can be used with both password sync and federation.

>[!NOTE]
> When you enable Pass-through Authentication you must have at least one verified domain in order to continue through the wizard.

> [!WARNING]
> Using an Alternate ID is not compatible with all Office 365 workloads. For more information, refer to [Configuring Alternate Login ID](https://technet.microsoft.com/library/dn659436.aspx).
>
>

### <a name="domain-and-ou-filtering"></a>Domain and OU filtering
By default all domains and OUs are synchronized. If there are some domains or OUs you do not want to synchronize to Azure AD, you can unselect these domains and OUs.  
![DomainOU filtering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
This page in the wizard is configuring domain-based and OU-based filtering. If you plan to make changes, then see [domain-based filtering](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) and [ou-based filtering](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) before you make these changes. Some OUs are essential for the functionality and should not be unselected.

If you use OU-based filtering, new OUs added later are synchronized by default. If you want the behavior that new OUs should not be synchronized, then you can configure it after the wizard has completed with [ou-based filtering](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering).

If you plan to use [group-based filtering](#sync-filtering-based-on-groups), then make sure the OU with the group is included and not filtered with OU-filtering. OU filtering is evaluated before group-based filtering.

It is also possible that some domains are not reachable due to firewall restrictions. These domains are unselected by default and have a warning.  
![Unreachable domains](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/unreachable.png)  
If you see this warning, make sure that these domains are indeed unreachable and the warning is expected.

### <a name="uniquely-identifying-your-users"></a>Uniquely identifying your users
The Matching across forests feature allows you to define how users from your AD DS forests are represented in Azure AD. A user might either be represented only once across all forests or have a combination of enabled and disabled accounts. The user might also be represented as a contact in some forests.

![Unique](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/unique.png)

| Setting | Description |
| --- | --- |
| [Users are only represented once across all forests](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |All users are created as individual objects in Azure AD. The objects are not joined in the metaverse. |
| [Mail attribute](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |This option joins users and contacts if the mail attribute has the same value in different forests. Use this option when your contacts have been created using GALSync. |
| [ObjectSID and msExchangeMasterAccountSID/ msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |This option joins an enabled user in an account forest with a disabled user in a resource forest. In Exchange, this configuration is known as a linked mailbox. This option can also be used if you only use Lync and Exchange is not present in the resource forest. |
| sAMAccountName and MailNickName |This option joins on attributes where it is expected the sign-in ID for the user can be found. |
| A specific attribute |This option allows you to select your own attribute. **Limitation:** Make sure to pick an attribute that already can be found in the metaverse. If you pick a custom attribute (not in the metaverse), the wizard cannot complete. |

**Source Anchor** - The attribute sourceAnchor is an attribute that is immutable during the lifetime of a user object. It is the primary key linking the on-premises user with the user in Azure AD. Since the attribute cannot be changed, you must plan for a good attribute to use. A good candidate is objectGUID. This attribute is not changed, unless the user account is moved between forests/domains. In a multi-forest environment where you move accounts between forests, another attribute must be used, such as an attribute with the employeeID. Avoid attributes that would change when a person marries or change assignments. You cannot use attributes with an @-sign, so email and userPrincipalName cannot be used. The attribute is also case-sensitive so when you move an object between forests, make sure to preserve the upper/lower case. Binary attributes are base64-encoded, but other attribute types remain in its unencoded state. In federation scenarios and some Azure AD interfaces, this attribute is also known as immutableID. More information about the source anchor can be found in the [design concepts](active-directory-aadconnect-design-concepts.md#sourceanchor).

### <a name="sync-filtering-based-on-groups"></a>Sync filtering based on groups
The filtering on groups feature allows you to sync only a small subset of objects for a pilot. To use this feature, create a group for this purpose in your on-premises Active Directory. Then add users and groups that should be synchronized to Azure AD as direct members. You can later add and remove users to this group to maintain the list of objects that should be present in Azure AD. All objects you want to synchronize must be a direct member of the group. Users, groups, contacts, and computers/devices must all be direct members. Nested group membership is not resolved. When you add a group as a member, only the group itself is added and not its members.

![Sync Filtering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> This feature is only intended to support a pilot deployment. Do not use it in a full-blown production deployment.
>
>

In a full-blown production deployment, it is going to be hard to maintain a single group with all objects to synchronize. Instead you should use one of the methods in [Configure filtering](active-directory-aadconnectsync-configure-filtering.md).

### <a name="optional-features"></a>Optional Features
This screen allows you to select the optional features for your specific scenarios.

![Optional features](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> If you currently have DirSync or Azure AD Sync active, do not activate any of the writeback features in Azure AD Connect.
>
>

| Optional Features | Description |
| --- | --- |
| Exchange Hybrid Deployment |The Exchange Hybrid Deployment feature allows for the co-existence of Exchange mailboxes both on-premises and in Office 365. Azure AD Connect is synchronizing a specific set of [attributes](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) from Azure AD back into your on-premises directory. |
| Azure AD app and attribute filtering |By enabling Azure AD app and attribute filtering, the set of synchronized attributes can be tailored. This option adds two more configuration pages to the wizard. For more information, see [Azure AD app and attribute filtering](#azure-ad-app-and-attribute-filtering). |
| Password synchronization |If you selected federation as the sign-in solution, then you can enable this option. Password synchronization can then be used as a backup option. For additional information, see [Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md). </br></br>If you selected Pass-through Authentication this option is enabled by default to ensure support for legacy clients and as a backup option. For additional information, see [Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md).|
| Password writeback |By enabling password writeback, password changes that originate in Azure AD is written back to your on-premises directory. For more information, see [Getting started with password management](../active-directory-passwords-getting-started.md). |
| Group writeback |If you use the **Office 365 Groups** feature, then you can have these groups represented in your on-premises Active Directory. This option is only available if you have Exchange present in your on-premises Active Directory. For more information, see [Group writeback](active-directory-aadconnect-feature-preview.md#group-writeback). |
| Device writeback |Allows you to writeback device objects in Azure AD to your on-premises Active Directory for conditional access scenarios. For more information, see [Enabling device writeback in Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md). |
| Directory extension attribute sync |By enabling directory extensions attribute sync, attributes specified are synced to Azure AD. For more information, see [Directory extensions](active-directory-aadconnectsync-feature-directory-extensions.md). |

### <a name="azure-ad-app-and-attribute-filtering"></a>Azure AD app and attribute filtering
If you want to limit which attributes to synchronize to Azure AD, then start by selecting which services you are using. If you make configuration changes on this page, a new service has to be selected explicitly by rerunning the installation wizard.

![Optional features Apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

Based on the services selected in the previous step, this page shows all attributes that are synchronized. This list is a combination of all object types being synchronized. If there are some particular attributes you need to not synchronize, you can unselect those attributes.

![Optional features Attributes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> Removing attributes can impact functionality. For best practices and recommendations, see [attributes synchronized](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize).
>
>

### <a name="directory-extension-attribute-sync"></a>Directory Extension attribute sync
You can extend the schema in Azure AD with custom attributes added by your organization or other attributes in Active Directory. To use this feature, select **Directory Extension attribute sync** on the **Optional Features** page. You can select more attributes to sync on this page.

![Directory extensions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/extension2.png)

For more information, see [Directory extensions](active-directory-aadconnectsync-feature-directory-extensions.md).

### <a name="enabling-single-sign-on-sso"></a>Enabling Single sign on (SSO)
Configuring single sign-on for use with Password Synchronization or Pass-through authentication is a simple process that you only need to complete once for each forest that is being synchronized to Azure AD. Configuration involves two steps as follows:

1.  Create the necessary computer account in your on-premises Active Directory.
2.  Configure the intranet zone of the client machines to support single sign on.

#### <a name="create-the-computer-account-in-active-directory"></a>Create the computer account in Active Directory
For each forest that has been added in Azure AD Connect, you will need to supply Domain Administrator credentials so that the computer account can be created in each forest. The credentials are only used to create the account and are not stored or used for any other operation. Simply add the credentials on the **Enable Single sign on** page of the Azure AD Connect wizard as shown:

![Enable Single sign on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/enablesso.PNG)

>[!NOTE]
>You can skip a particular forest if you do not wish to use Single sign on with that forest.

#### <a name="configure-the-intranet-zone-for-client-machines"></a>Configure the Intranet Zone for client machines
To ensure that the client sign-ins automatically in the intranet zone you need to ensure that two URLs are part of the intranet zone. This ensures that the domain joined computer automatically sends a Kerberos ticket to Azure AD when it is connected to the corporate network.
On a computer that has the Group Policy management tools.

1.  Open the Group Policy Management tools
2.  Edit the Group policy that will be applied to all users. For example, the Default Domain Policy.
3.  Navigate to **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site to Zone Assignment List** per the image below.
4.  Enable the policy, and enter the following two items in the dialog box.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  It should look similar to the following:  
![Intranet Zones](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  Click **Ok** twice.

## <a name="configuring-federation-with-ad-fs"></a>Configuring federation with AD FS
Configuring AD FS with Azure AD Connect is simple with just a few clicks. The following is required before the configuration.

* A Windows Server 2012 R2 server for the federation server with remote management enabled
* A Windows Server 2012 R2 server for the Web Application Proxy server with remote management enabled
* An SSL certificate for the federation service name you intend to use (for example sts.contoso.com)

### <a name="ad-fs-configuration-pre-requisites"></a>AD FS configuration pre-requisites
To configure your AD FS farm using Azure AD Connect, ensure WinRM is enabled on the remote servers. In addition, go through the ports requirement listed in [Table 3 - Azure AD Connect and Federation Servers/WAP](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap).

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>Create a new AD FS farm or use an existing AD FS farm
You can use an existing AD FS farm or you can choose to create a new AD FS farm. If you choose to create a new one, you are required to provide the SSL certificate. If the SSL certificate is protected by a password, you are prompted for the password.

![AD FS Farm](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/adfs1.png)

If you choose to use an existing AD FS farm, you are taken directly to the configuring the trust relationship between AD FS and Azure AD screen.

### <a name="specify-the-ad-fs-servers"></a>Specify the AD FS servers
Enter the servers that you want to install AD FS on. You can add one or more servers based on your capacity planning needs. Join all servers to Active Directory before you perform this configuration. Microsoft recommends installing a single AD FS server for test and pilot deployments. Then add and deploy more servers to meet your scaling needs by running Azure AD Connect again after initial configuration.

> [!NOTE]
> Ensure that all your servers are joined to an AD domain before you do this configuration.
>
>

![AD FS Servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-the-web-application-proxy-servers"></a>Specify the Web Application Proxy servers
Enter the servers that you want as your Web Application proxy servers. The web application proxy server is deployed in your DMZ (extranet facing) and supports authentication requests from the extranet. You can add one or more servers based on your capacity planning needs. Microsoft recommends installing a single Web application proxy server for test and pilot deployments. Then add and deploy more servers to meet your scaling needs by running Azure AD Connect again after initial configuration. We recommend having an equivalent number of proxy servers to satisfy authentication from the intranet.

> [!NOTE]
> <li> If the account you use is not a local admin on the AD FS servers, then you are prompted for admin credentials.</li>
> <li> Ensure that there is HTTP/HTTPS connectivity between the Azure AD Connect server and the Web Application Proxy server before you run this step.</li>
> <li> Ensure that there is HTTP/HTTPS connectivity between the Web Application Server and the AD FS server to allow authentication requests to flow through.</li>
>

![Web App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/adfs3.png)

You are prompted to enter credentials so that the web application server can establish a secure connection to the AD FS server. These credentials need to be a local administrator on the AD FS server.

![Proxy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-the-service-account-for-the-ad-fs-service"></a>Specify the service account for the AD FS service
The AD FS service requires a domain service account to authenticate users and lookup user information in Active Directory. It can support two types of service accounts:

* **Group Managed Service Account** - Introduced in Active Directory Domain Services with Windows Server 2012. This type of account provides services, such as AD FS, a single account without needing to update the account password regularly. Use this option if you already have Windows Server 2012 domain controllers in the domain that your AD FS servers belong to.
* **Domain User Account** - This type of account requires you to provide a password and regularly update the password when the password changes or expires. Use this option only when you do not have Windows Server 2012 domain controllers in the domain that your AD FS servers belong to.

If you selected Group Managed Service Account and this feature has never been used in Active Directory, you are prompted for Enterprise Admin credentials. These credentials are used to initiate the key store and enable the feature in Active Directory.

![AD FS Service Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-the-azure-ad-domain-that-you-wish-to-federate"></a>Select the Azure AD domain that you wish to federate
This configuration is used to setup the federation relationship between AD FS and Azure AD. It configures AD FS to issue security tokens to Azure AD and configures Azure AD to trust the tokens from this specific AD FS instance. This page only allows you to configure a single domain in the initial installation. You can configure more domains later by running Azure AD Connect again.

![Azure AD Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-the-azure-ad-domain-selected-for-federation"></a>Verify the Azure AD domain selected for federation
When you select the domain to be federated, Azure AD Connect provides you with necessary information to verify an unverified domain. See [Add and verify the domain](../active-directory-add-domain.md) for how to use this information.

![Azure AD Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> AD Connect tries to verify the domain during the configure stage. If you continue to configure without adding the necessary DNS records, the wizard is not able to complete the configuration.
>
>

## <a name="configure-and-verify-pages"></a>Configure and verify pages
The configuration happens on this page.

> [!NOTE]
> Before you continue installation and if you configured federation, make sure that you have configured [Name resolution for federation servers](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers).
>
>

![Ready to configure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>Staging mode
It is possible to setup a new sync server in parallel with staging mode. It is only supported to have one sync server exporting to one directory in the cloud. But if you want to move from another server, for example one running DirSync, then you can enable Azure AD Connect in staging mode. When enabled, the sync engine import and synchronize data as normal, but it does not export anything to Azure AD or AD. The features password sync and password writeback are disabled while in staging mode.

![Staging mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/stagingmode.png)

While in staging mode, it is possible to make required changes to the sync engine and review what is about to be exported. When the configuration looks good, run the installation wizard again and disable staging mode. Data is now exported to Azure AD from this server. Make sure to disable the other server at the same time so only one server is actively exporting.

For more information, see [Staging mode](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-your-federation-configuration"></a>Verify your federation configuration
Azure AD Connect verifies the DNS settings for you when you click the Verify button.

![Complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/completed.png)

![Verify](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-get-started-custom/adfs7.png)

In addition, perform the following verification steps:

* Validate that you can sign in from a browser from a domain joined machine on the intranet: Connect to https://myapps.microsoft.com and verify the sign-in with your logged in account. The built-in AD DS administrator account is not synchronized and cannot be used for verification.
* Validate that you can sign in from a device from the extranet. On a home machine or a mobile device, connect to https://myapps.microsoft.com and supply your credentials.
* Validate rich client sign-in. Connect to https://testconnectivity.microsoft.com, choose the **Office 365** tab and chose the **Office 365 Single Sign-On Test**.

## <a name="next-steps"></a>Next steps
After the installation has completed, sign out and sign in again to Windows before you use Synchronization Service Manager or Synchronization Rule Editor.

Now that you have Azure AD Connect installed you can [verify the installation and assign licenses](active-directory-aadconnect-whats-next.md).

Learn more about these features, which were enabled with the installation: [Prevent accidental deletes](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) and [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Learn more about these common topics: [scheduler and how to trigger sync](active-directory-aadconnectsync-feature-scheduler.md).

Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).



























