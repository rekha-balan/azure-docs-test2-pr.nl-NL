---
title: On-premises password writeback integration with Azure AD SSPR
description: Get cloud passwords written back to on-premises AD infratstructure
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: 4f4c2ada08c69b6602ff5a300a15c4ca57090a8e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868356"
---
# <a name="what-is-password-writeback"></a>What is password writeback?

Having a cloud based password reset utility is great but most companies still have an on-premises directory where their users exist. How does Microsoft support keeping traditional on-premises Active Directory (AD) in sync with password changes in the cloud? Password writeback is a feature enabled with [Azure AD Connect](./../connect/active-directory-aadconnect.md) that allows password changes in the cloud to be written back to an existing on-premises directory in real-time.

Password writeback is supported in environments that use:

* [Active Directory Federation Services](../connect/active-directory-aadconnect-federation-management.md)
* [Password hash synchronization](../connect/active-directory-aadconnectsync-implement-password-hash-synchronization.md)
* [Pass-through authentication](../connect/active-directory-aadconnect-pass-through-authentication.md)

Password writeback provides:

* **Enforcement of on-premises Active Directory password policies**: When a user resets their password, it is checked to ensure it meets your on-premises Active Directory policy before committing it to that directory. This review includes checking the history, complexity, age, password filters, and any other password restrictions that you have defined in local Active Directory.
* **Zero-delay feedback**: Password writeback is a synchronous operation. Your users are notified immediately if their password did not meet the policy or could not be reset or changed for any reason.
* **Supports password changes from the access panel and Office 365**: When federated or password hash synchronized users come to change their expired or non-expired passwords, those passwords are written back to your local Active Directory environment.
* **Supports password writeback when an admin resets them from the Azure portal**: Whenever an admin resets a user’s password in the [Azure portal](https://portal.azure.com), if that user is federated or password hash synchronized, the password is written back to on-premises. This functionality is currently not supported in the Office admin portal.
* **Doesn’t require any inbound firewall rules**: Password writeback uses an Azure Service Bus relay as an underlying communication channel. All communication is outbound over port 443.

> [!Note]
> User accounts that exist within protected groups in on-premises Active Directory cannot be used with password writeback. For more information about protected groups, see [Protected accounts and groups in Active Directory](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="licensing-requirements-for-password-writeback"></a>Licensing requirements for password writeback

**Self-Service Password Reset/Change/Unlock with on-premises writeback is a premium feature of Azure AD**. For more information about licensing, see the [Azure Active Directory pricing site](https://azure.microsoft.com/pricing/details/active-directory/).

To use password writeback, you must have one of the following licenses assigned on your tenant:

* Azure AD Premium P1
* Azure AD Premium P2
* Enterprise Mobility + Security E3 or A3
* Enterprise Mobility + Security E5 or A5
* Microsoft 365 E3 or A3
* Microsoft 365 E5 or A5
* Microsoft 365 F1

> [!WARNING]
> Standalone Office 365 licensing plans *don't support password writeback* and require that you have one of the preceding plans for this functionality to work.
>

## <a name="how-password-writeback-works"></a>How password writeback works

When a federated or password hash synchronized user attempts to reset or change their password in the cloud, the following actions occur:

1. A check is performed to see what type of password the user has. If the password is managed on-premises:
   * A check is performed to see if the writeback service is up and running. If it is, the user can proceed.
   * If the writeback service is down, the user is informed that their password can't be reset right now.
2. Next, the user passes the appropriate authentication gates and reaches the **Reset password** page.
3. The user selects a new password and confirms it.
4. When the user selects **Submit**, the plaintext password is encrypted with a symmetric key created during the writeback setup process.
5. The encrypted password is included in a payload that gets sent over an HTTPS channel to your tenant-specific service bus relay (that is set up for you during the writeback setup process). This relay is protected by a randomly generated password that only your on-premises installation knows.
6. After the message reaches the service bus, the password-reset endpoint automatically wakes up and sees that it has a reset request pending.
7. The service then looks for the user by using the cloud anchor attribute. For this lookup to succeed:

   * The user object must exist in the Active Directory connector space.
   * The user object must be linked to the corresponding metaverse (MV) object.
   * The user object must be linked to the corresponding Azure Active Directory connector object.
   * The link from the Active Directory connector object to the MV must have the synchronization rule `Microsoft.InfromADUserAccountEnabled.xxx` on the link. <br> <br>
   When the call comes in from the cloud, the synchronization engine uses the **cloudAnchor** attribute to look up the Azure Active Directory connector space object. It then follows the link back to the MV object, and then follows the link back to the Active Directory object. Because there can be multiple Active Directory objects (multi-forest) for the same user, the sync engine relies on the `Microsoft.InfromADUserAccountEnabled.xxx` link to pick the correct one.

   > [!Note]
   > As a result of this logic, for password writeback to work Azure AD Connect must be able to communicate with the primary domain controller (PDC) emulator. If you need to enable this manually, you can connect Azure AD Connect to the PDC emulator. Right-click the **properties** of the Active Directory synchronization connector, then select **configure directory partitions**. From there, look for the **domain controller connection settings** section and select the box titled **only use preferred domain controllers**. Even if the preferred domain controller is not a PDC emulator, Azure AD Connect attempts to connect to the PDC for password writeback.

8. After the user account is found, an attempt to reset the password directly in the appropriate Active Directory forest is made.
9. If the password set operation is successful, the user is told their password has been changed.
   > [!NOTE]
   > If the user's password hash is synchronized to Azure AD by using password hash synchronization, there is a chance that the on-premises password policy is weaker than the cloud password policy. In this case, the on-premises policy is enforced. This policy ensures that your on-premises policy is enforced in the cloud, no matter if you use password hash synchronization or federation to provide single sign-on.

10. If the password set operation fails, an error prompts the user to try again. The operation might fail because:
   * The service was down.
   * The password they selected did not meet the organization's policies.
   * Unable to find the user in local Active Directory.

    The error messages provide guidance to users so they can attempt to resolve without administrator intervention.

## <a name="password-writeback-security"></a>Password writeback security

Password writeback is a highly secure service. To ensure your information is protected, a four-tiered security model is enabled as the following describes:

* **Tenant-specific service-bus relay**
   * When you set up the service, a tenant-specific service bus relay is set up that's protected by a randomly generated strong password that Microsoft never has access to.
* **Locked down, cryptographically strong, password encryption key**
   * After the service bus relay is created, a strong symmetric key is created that is used to encrypt the password as it comes over the wire. This key only lives in your company's secret store in the cloud, which is heavily locked down and audited, just like any other password in the directory.
* **Industry standard Transport Layer Security (TLS)**
   1. When a password reset or change operation occurs in the cloud, the plaintext password is encrypted with your public key.
   2. The encrypted password is placed into an HTTPS message that is sent over an encrypted channel by using Microsoft SSL certs to your service bus relay.
   3. After the message arrives in the service bus, your on-premises agent wakes up and authenticates to the service bus by using the strong password that was previously generated.
   4. The on-premises agent picks up the encrypted message and decrypts it by using the private key.
   5. The on-premises agent attempts to set the password through the AD DS SetPassword API. This step is what allows enforcement of your Active Directory on-premises password policy (such as the complexity, age, history, and filters) in the cloud.
* **Message expiration policies**
   * If the message sits in service bus because your on-premises service is down, it times out and is removed after several minutes. The time-out and removal of the message increases security even further.

### <a name="password-writeback-encryption-details"></a>Password writeback encryption details

After a user submits a password reset, the reset request goes through several encryption steps before it arrives in your on-premises environment. These encryption steps ensure maximum service reliability and security. They are described as follows:

* **Step 1: Password encryption with 2048-bit RSA Key**: After a user submits a password to be written back to on-premises, the submitted password itself is encrypted with a 2048-bit RSA key.
* **Step 2: Package-level encryption with AES-GCM**: The entire package, the password plus the required metadata, is encrypted by using AES-GCM. This encryption prevents anyone with direct access to the underlying ServiceBus channel from viewing or tampering with the contents.
* **Step 3: All communication occurs over TLS/SSL**: All the communication with ServiceBus happens in an SSL/TLS channel. This encryption secures the contents from unauthorized third parties.
* **Automatic key roll over every six months**: All keys roll over every six months, or every time password writeback is disabled and then re-enabled on Azure AD Connect, to ensure maximum service security and safety.

### <a name="password-writeback-bandwidth-usage"></a>Password writeback bandwidth usage

Password writeback is a low-bandwidth service that only sends requests back to the on-premises agent under the following circumstances:

* Two messages are sent when the feature is enabled or disabled through Azure AD Connect.
* One message is sent once every five minutes as a service heartbeat for as long as the service is running.
* Two messages are sent each time a new password is submitted:
   * The first message is a request to perform the operation.
   * The second message contains the result of the operation, and is sent in the following circumstances:
      * Each time a new password is submitted during a user self-service password reset.
      * Each time a new password is submitted during a user password change operation.
      * Each time a new password is submitted during an admin-initiated user password reset (only from the Azure admin portals).

#### <a name="message-size-and-bandwidth-considerations"></a>Message size and bandwidth considerations

The size of each of the message described previously is typically under 1 KB. Even under extreme loads, the password writeback service itself is consuming a few kilobits per second of bandwidth. Because each message is sent in real time, only when required by a password update operation, and because the message size is so small, the bandwidth usage of the writeback capability is too small to have a measurable impact.

## <a name="supported-writeback-operations"></a>Supported writeback operations

Passwords are written back in all the following situations:

* **Supported end-user operations**
   * Any end-user self-service voluntary change password operation
   * Any end-user self-service force change password operation, for example, password expiration
   * Any end-user self-service password reset that originates from the [password reset portal](https://passwordreset.microsoftonline.com)
* **Supported administrator operations**
   * Any administrator self-service voluntary change password operation
   * Any administrator self-service force change password operation, for example, password expiration
   * Any administrator self-service password reset that originates from the [password reset portal](https://passwordreset.microsoftonline.com)
   * Any administrator-initiated end-user password reset from the [Azure portal](https://portal.azure.com)

## <a name="unsupported-writeback-operations"></a>Unsupported writeback operations

Passwords are *not* written back in any of the following situations:

* **Unsupported end-user operations**
   * Any end user resetting their own password by using PowerShell version 1, version 2, or the Azure AD Graph API
* **Unsupported administrator operations**
   * Any administrator-initiated end-user password reset from the [Office management portal](https://portal.office.com)
   * Any administrator-initiated end-user password reset from PowerShell version 1, version 2, or the Azure AD Graph API

## <a name="next-steps"></a>Next steps

Enable password writeback using the Tutorial: [Enabling password writeback](tutorial-enable-writeback.md)
