---
title: Remote Monitoring access control - Azure | Microsoft Docs
description: This article provides information about how you can configure role-based access controls (RBAC) in the Remote Monitoring solution accelerator
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 08/06/2018
ms.topic: conceptual
ms.openlocfilehash: 956cb80ddbf96f23585dd52f3dc1013c7a665113
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871134"
---
# <a name="configure-role-based-access-controls-in-the-remote-monitoring-solution-accelerator"></a><span data-ttu-id="42b1f-103">Configure role-based access controls in the Remote Monitoring solution accelerator</span><span class="sxs-lookup"><span data-stu-id="42b1f-103">Configure role-based access controls in the Remote Monitoring solution accelerator</span></span>

<span data-ttu-id="42b1f-104">This article provides information about how to configure role-based access controls in the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="42b1f-104">This article provides information about how to configure role-based access controls in the Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="42b1f-105">Role-based access controls let you restrict access for individual users to specific features in the solution.</span><span class="sxs-lookup"><span data-stu-id="42b1f-105">Role-based access controls let you restrict access for individual users to specific features in the solution.</span></span>

## <a name="default-settings"></a><span data-ttu-id="42b1f-106">Default settings</span><span class="sxs-lookup"><span data-stu-id="42b1f-106">Default settings</span></span>

<span data-ttu-id="42b1f-107">When you first deploy the Remote Monitoring solution, there are two roles: **Admin** and **Read Only**.</span><span class="sxs-lookup"><span data-stu-id="42b1f-107">When you first deploy the Remote Monitoring solution, there are two roles: **Admin** and **Read Only**.</span></span>

<span data-ttu-id="42b1f-108">Any user in the **Admin** role has full access to the solution.</span><span class="sxs-lookup"><span data-stu-id="42b1f-108">Any user in the **Admin** role has full access to the solution.</span></span> <span data-ttu-id="42b1f-109">A user in the **Read Only** role can't do any of the following tasks:</span><span class="sxs-lookup"><span data-stu-id="42b1f-109">A user in the **Read Only** role can't do any of the following tasks:</span></span>

- <span data-ttu-id="42b1f-110">Update alarms</span><span class="sxs-lookup"><span data-stu-id="42b1f-110">Update alarms</span></span>
- <span data-ttu-id="42b1f-111">Delete alarms</span><span class="sxs-lookup"><span data-stu-id="42b1f-111">Delete alarms</span></span>
- <span data-ttu-id="42b1f-112">Create devices</span><span class="sxs-lookup"><span data-stu-id="42b1f-112">Create devices</span></span>
- <span data-ttu-id="42b1f-113">Update devices</span><span class="sxs-lookup"><span data-stu-id="42b1f-113">Update devices</span></span>
- <span data-ttu-id="42b1f-114">Delete devices</span><span class="sxs-lookup"><span data-stu-id="42b1f-114">Delete devices</span></span>
- <span data-ttu-id="42b1f-115">Create device groups</span><span class="sxs-lookup"><span data-stu-id="42b1f-115">Create device groups</span></span>
- <span data-ttu-id="42b1f-116">Update device groups</span><span class="sxs-lookup"><span data-stu-id="42b1f-116">Update device groups</span></span>
- <span data-ttu-id="42b1f-117">Delete device groups</span><span class="sxs-lookup"><span data-stu-id="42b1f-117">Delete device groups</span></span>
- <span data-ttu-id="42b1f-118">Create rules</span><span class="sxs-lookup"><span data-stu-id="42b1f-118">Create rules</span></span>
- <span data-ttu-id="42b1f-119">Update rules</span><span class="sxs-lookup"><span data-stu-id="42b1f-119">Update rules</span></span>
- <span data-ttu-id="42b1f-120">Delete rules</span><span class="sxs-lookup"><span data-stu-id="42b1f-120">Delete rules</span></span>
- <span data-ttu-id="42b1f-121">Create jobs</span><span class="sxs-lookup"><span data-stu-id="42b1f-121">Create jobs</span></span>
- <span data-ttu-id="42b1f-122">Update SIM management</span><span class="sxs-lookup"><span data-stu-id="42b1f-122">Update SIM management</span></span>

<span data-ttu-id="42b1f-123">The person who deploys the Remote Monitoring solution is automatically assigned to the **Admin** role and is an Azure Active Directory application owner.</span><span class="sxs-lookup"><span data-stu-id="42b1f-123">The person who deploys the Remote Monitoring solution is automatically assigned to the **Admin** role and is an Azure Active Directory application owner.</span></span> <span data-ttu-id="42b1f-124">As an application owner you can assign roles to other users in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42b1f-124">As an application owner you can assign roles to other users in the Azure portal.</span></span>

<span data-ttu-id="42b1f-125">If you want another user to assign roles in the solution, they must also be set as an application owner in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42b1f-125">If you want another user to assign roles in the solution, they must also be set as an application owner in the Azure portal.</span></span>

## <a name="add-or-remove-users"></a><span data-ttu-id="42b1f-126">Add or remove users</span><span class="sxs-lookup"><span data-stu-id="42b1f-126">Add or remove users</span></span>

<span data-ttu-id="42b1f-127">Use the Azure portal to add or remove a user from the Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="42b1f-127">Use the Azure portal to add or remove a user from the Remote Monitoring solution.</span></span> <span data-ttu-id="42b1f-128">The following steps use the [Azure Active Directory enterprise application](../active-directory/manage-apps/add-application-portal.md#find-your-azure-ad-tenant-application) that was created for you when you deployed the Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="42b1f-128">The following steps use the [Azure Active Directory enterprise application](../active-directory/manage-apps/add-application-portal.md#find-your-azure-ad-tenant-application) that was created for you when you deployed the Remote Monitoring solution.</span></span>

1. <span data-ttu-id="42b1f-129">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="42b1f-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="42b1f-130">Check the [user is in the directory](../active-directory/fundamentals/add-users-azure-active-directory.md) you're using.</span><span class="sxs-lookup"><span data-stu-id="42b1f-130">Check the [user is in the directory](../active-directory/fundamentals/add-users-azure-active-directory.md) you're using.</span></span> <span data-ttu-id="42b1f-131">You chose the directory to use when you signed in to the [Microsoft Azure IoT Solution Accelerators](https://www.azureiotsolutions.com/Accelerators) site.</span><span class="sxs-lookup"><span data-stu-id="42b1f-131">You chose the directory to use when you signed in to the [Microsoft Azure IoT Solution Accelerators](https://www.azureiotsolutions.com/Accelerators) site.</span></span> <span data-ttu-id="42b1f-132">The directory name is visible in the top-right corner of the [page](https://www.azureiotsolutions.com/Accelerators).</span><span class="sxs-lookup"><span data-stu-id="42b1f-132">The directory name is visible in the top-right corner of the [page](https://www.azureiotsolutions.com/Accelerators).</span></span>

1. <span data-ttu-id="42b1f-133">Find the **Enterprise application** for your solution in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42b1f-133">Find the **Enterprise application** for your solution in the Azure portal.</span></span> <span data-ttu-id="42b1f-134">Once there, filter the list by setting **Application Type** to **All Applications**.</span><span class="sxs-lookup"><span data-stu-id="42b1f-134">Once there, filter the list by setting **Application Type** to **All Applications**.</span></span> <span data-ttu-id="42b1f-135">Search for your application by application name.</span><span class="sxs-lookup"><span data-stu-id="42b1f-135">Search for your application by application name.</span></span> <span data-ttu-id="42b1f-136">The application name is the name of your Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="42b1f-136">The application name is the name of your Remote Monitoring solution.</span></span> <span data-ttu-id="42b1f-137">In the following screenshot, the solution and application display names are **contoso-rm4**.</span><span class="sxs-lookup"><span data-stu-id="42b1f-137">In the following screenshot, the solution and application display names are **contoso-rm4**.</span></span>

    ![Enterprise application](media/iot-accelerators-remote-monitoring-rbac/appregistration.png)

1. <span data-ttu-id="42b1f-139">Check you're an owner of the application by clicking the application and then clicking **Owners**.</span><span class="sxs-lookup"><span data-stu-id="42b1f-139">Check you're an owner of the application by clicking the application and then clicking **Owners**.</span></span> <span data-ttu-id="42b1f-140">In the following screenshot, **Contoso admin** is an owner of the **contoso-rm4** application:</span><span class="sxs-lookup"><span data-stu-id="42b1f-140">In the following screenshot, **Contoso admin** is an owner of the **contoso-rm4** application:</span></span>

    ![Owners](media/iot-accelerators-remote-monitoring-rbac/owners.png)

    <span data-ttu-id="42b1f-142">If you aren't an owner, you need to ask an existing owner to add you to the list.</span><span class="sxs-lookup"><span data-stu-id="42b1f-142">If you aren't an owner, you need to ask an existing owner to add you to the list.</span></span> <span data-ttu-id="42b1f-143">Only owners can assign application roles such as **Admin** or **Read Only** to other users.</span><span class="sxs-lookup"><span data-stu-id="42b1f-143">Only owners can assign application roles such as **Admin** or **Read Only** to other users.</span></span>

1. <span data-ttu-id="42b1f-144">To see the list of users assigned to roles in the application, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="42b1f-144">To see the list of users assigned to roles in the application, click **Users and groups**.</span></span>

1. <span data-ttu-id="42b1f-145">To add a user, click **+ Add user**, and then click **Users and groups, None Selected** to select a user from the directory.</span><span class="sxs-lookup"><span data-stu-id="42b1f-145">To add a user, click **+ Add user**, and then click **Users and groups, None Selected** to select a user from the directory.</span></span>

1. <span data-ttu-id="42b1f-146">To assign the user to a role, click **Select role, None Selected** and choose either the **Admin** or **Read Only** role for the user.</span><span class="sxs-lookup"><span data-stu-id="42b1f-146">To assign the user to a role, click **Select role, None Selected** and choose either the **Admin** or **Read Only** role for the user.</span></span> <span data-ttu-id="42b1f-147">Click **Select**, and then click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="42b1f-147">Click **Select**, and then click **Assign**.</span></span>

    ![Select role](media/iot-accelerators-remote-monitoring-rbac/selectrole.png)

1. <span data-ttu-id="42b1f-149">The user can now access the Remote Monitoring solution with the permissions defined by the role.</span><span class="sxs-lookup"><span data-stu-id="42b1f-149">The user can now access the Remote Monitoring solution with the permissions defined by the role.</span></span>

1. <span data-ttu-id="42b1f-150">You can delete users from the application on the **Users and groups** page in the portal.</span><span class="sxs-lookup"><span data-stu-id="42b1f-150">You can delete users from the application on the **Users and groups** page in the portal.</span></span>

## <a name="create-a-custom-role"></a><span data-ttu-id="42b1f-151">Create a custom role</span><span class="sxs-lookup"><span data-stu-id="42b1f-151">Create a custom role</span></span>

<span data-ttu-id="42b1f-152">The Remote Monitoring solution includes the **Admin** and **Read Only** roles when it's first deployed.</span><span class="sxs-lookup"><span data-stu-id="42b1f-152">The Remote Monitoring solution includes the **Admin** and **Read Only** roles when it's first deployed.</span></span> <span data-ttu-id="42b1f-153">You can add custom roles with different sets of permissions.</span><span class="sxs-lookup"><span data-stu-id="42b1f-153">You can add custom roles with different sets of permissions.</span></span> <span data-ttu-id="42b1f-154">To define a custom role, you need to:</span><span class="sxs-lookup"><span data-stu-id="42b1f-154">To define a custom role, you need to:</span></span>

- <span data-ttu-id="42b1f-155">Add a new role to the application in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42b1f-155">Add a new role to the application in the Azure portal.</span></span>
- <span data-ttu-id="42b1f-156">Define a policy for the new role in the Authentication and Authorization microservice.</span><span class="sxs-lookup"><span data-stu-id="42b1f-156">Define a policy for the new role in the Authentication and Authorization microservice.</span></span>
- <span data-ttu-id="42b1f-157">Update the solution's web UI.</span><span class="sxs-lookup"><span data-stu-id="42b1f-157">Update the solution's web UI.</span></span>

### <a name="define-a-custom-role-in-the-azure-portal"></a><span data-ttu-id="42b1f-158">Define a custom role in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="42b1f-158">Define a custom role in the Azure portal</span></span>

<span data-ttu-id="42b1f-159">The following steps describe how to add a role to an application in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="42b1f-159">The following steps describe how to add a role to an application in Azure Active Directory.</span></span> <span data-ttu-id="42b1f-160">In this example, you create a new role that allows members to create, update, and delete devices in the Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="42b1f-160">In this example, you create a new role that allows members to create, update, and delete devices in the Remote Monitoring solution.</span></span>

1. <span data-ttu-id="42b1f-161">Find the **App registration** for your solution in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="42b1f-161">Find the **App registration** for your solution in the Azure portal.</span></span> <span data-ttu-id="42b1f-162">The application name is the name of your Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="42b1f-162">The application name is the name of your Remote Monitoring solution.</span></span> <span data-ttu-id="42b1f-163">In the following screenshot, the solution and application display names are **contoso-rm4**.</span><span class="sxs-lookup"><span data-stu-id="42b1f-163">In the following screenshot, the solution and application display names are **contoso-rm4**.</span></span>

    ![App registration](media/iot-accelerators-remote-monitoring-rbac/appregistration2.png)

1. <span data-ttu-id="42b1f-165">Select your application and then click **Manifest**.</span><span class="sxs-lookup"><span data-stu-id="42b1f-165">Select your application and then click **Manifest**.</span></span> <span data-ttu-id="42b1f-166">You can see the two existing [app roles](https://docs.microsoft.com/azure/architecture/multitenant-identity/app-roles) defined for the application:</span><span class="sxs-lookup"><span data-stu-id="42b1f-166">You can see the two existing [app roles](https://docs.microsoft.com/azure/architecture/multitenant-identity/app-roles) defined for the application:</span></span>

    ![View manifest](media/iot-accelerators-remote-monitoring-rbac/viewmanifest.png)

1. <span data-ttu-id="42b1f-168">Edit the manifest to add a role called **ManageDevices** as shown in the following snippet.</span><span class="sxs-lookup"><span data-stu-id="42b1f-168">Edit the manifest to add a role called **ManageDevices** as shown in the following snippet.</span></span> <span data-ttu-id="42b1f-169">You need a unique string such as a GUID for the new role ID.</span><span class="sxs-lookup"><span data-stu-id="42b1f-169">You need a unique string such as a GUID for the new role ID.</span></span> <span data-ttu-id="42b1f-170">You can generate a new GUID using a service such as the [Online GUID Generator](https://www.guidgenerator.com/):</span><span class="sxs-lookup"><span data-stu-id="42b1f-170">You can generate a new GUID using a service such as the [Online GUID Generator](https://www.guidgenerator.com/):</span></span>

    ```json
    "appRoles": [
      {
        "allowedMemberTypes": [
          "User"
        ],
        "displayName": "Admin",
        "id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
        "isEnabled": true,
        "description": "Administrator access to the application",
        "value": "Admin"
      },
      {
        "allowedMemberTypes": [
          "User"
        ],
        "displayName": "Read Only",
        "id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
        "isEnabled": true,
        "description": "Read only access to device information",
        "value": "ReadOnly"
      },
      {
        "allowedMemberTypes": [
          "User"
        ],
        "displayName": "ManageDevices",
        "id": "ADD A NEW GUID HERE",
        "isEnabled": true,
        "description": "A new role for the application.",
        "value": "ManageDevices"
      }
    ],
    ```

    <span data-ttu-id="42b1f-171">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="42b1f-171">Save the changes.</span></span>

### <a name="define-a-policy-for-the-new-role"></a><span data-ttu-id="42b1f-172">Define a policy for the new role</span><span class="sxs-lookup"><span data-stu-id="42b1f-172">Define a policy for the new role</span></span>

<span data-ttu-id="42b1f-173">After to add the role to the app in the Azure portal, you need to define a policy in [roles.json](https://github.com/Azure/remote-monitoring-services-dotnet/blob/master/pcs-auth/Services/data/policies/roles.json) for the role that assigns the permissions needed to manage devices.</span><span class="sxs-lookup"><span data-stu-id="42b1f-173">After to add the role to the app in the Azure portal, you need to define a policy in [roles.json](https://github.com/Azure/remote-monitoring-services-dotnet/blob/master/pcs-auth/Services/data/policies/roles.json) for the role that assigns the permissions needed to manage devices.</span></span>

1. <span data-ttu-id="42b1f-174">Clone the [Authentication and Authorization microservice](https://github.com/Azure/pcs-auth-dotnet) repository from GitHub to your local machine.</span><span class="sxs-lookup"><span data-stu-id="42b1f-174">Clone the [Authentication and Authorization microservice](https://github.com/Azure/pcs-auth-dotnet) repository from GitHub to your local machine.</span></span>

1. <span data-ttu-id="42b1f-175">Edit the **Services/data/policies/roles.json** file to add the policy for the **ManageDevices** role as shown in the following snippet.</span><span class="sxs-lookup"><span data-stu-id="42b1f-175">Edit the **Services/data/policies/roles.json** file to add the policy for the **ManageDevices** role as shown in the following snippet.</span></span> <span data-ttu-id="42b1f-176">The **ID** and **Role** values must match the role definition in the app manifest from the previous section.</span><span class="sxs-lookup"><span data-stu-id="42b1f-176">The **ID** and **Role** values must match the role definition in the app manifest from the previous section.</span></span> <span data-ttu-id="42b1f-177">The list of allowed actions allows someone in the **ManageDevices** role to create, update, and delete devices connected to the solution:</span><span class="sxs-lookup"><span data-stu-id="42b1f-177">The list of allowed actions allows someone in the **ManageDevices** role to create, update, and delete devices connected to the solution:</span></span>

    ```json
    {
    "Items": [
      {
        "Id": "a400a00b-f67c-42b7-ba9a-f73d8c67e433",
        "Role": "admin",
        "AllowedActions": [
          "UpdateAlarms",
          "DeleteAlarms",
          "CreateDevices",
          "UpdateDevices",
          "DeleteDevices",
          "CreateDeviceGroups",
          "UpdateDeviceGroups",
          "DeleteDeviceGroups",
          "CreateRules",
          "UpdateRules",
          "DeleteRules",
          "CreateJobs",
          "UpdateSimManagement"
        ]
      },
      {
        "Id": "e5bbd0f5-128e-4362-9dd1-8f253c6082d7",
        "Role": "readOnly",
        "AllowedActions": []
      },
      {
        "Id": "GUID FROM APP MANIFEST",
        "Role": "ManageDevices",
        "AllowedActions": [
          "CreateDevices",
          "UpdateDevices",
          "DeleteDevices"
        ]
      }
    ]
    }
    ```

1. <span data-ttu-id="42b1f-178">When you have finished editing the **Services/data/policies/roles.json** file, rebuild and redeploy the Authentication and Authorization microservice to your solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="42b1f-178">When you have finished editing the **Services/data/policies/roles.json** file, rebuild and redeploy the Authentication and Authorization microservice to your solution accelerator.</span></span>

### <a name="how-the-web-ui-enforces-permissions"></a><span data-ttu-id="42b1f-179">How the web UI enforces permissions</span><span class="sxs-lookup"><span data-stu-id="42b1f-179">How the web UI enforces permissions</span></span>

<span data-ttu-id="42b1f-180">The web UI uses the [Authentication and Authorization microservice](https://github.com/Azure/pcs-auth-dotnet) to determine what actions a user is allowed to take and what controls are visible in the UI.</span><span class="sxs-lookup"><span data-stu-id="42b1f-180">The web UI uses the [Authentication and Authorization microservice](https://github.com/Azure/pcs-auth-dotnet) to determine what actions a user is allowed to take and what controls are visible in the UI.</span></span> <span data-ttu-id="42b1f-181">For example, if your solution is called **contoso-rm4**, the web UI retrieves a list of allowed actions for the current user by sending the following request:</span><span class="sxs-lookup"><span data-stu-id="42b1f-181">For example, if your solution is called **contoso-rm4**, the web UI retrieves a list of allowed actions for the current user by sending the following request:</span></span>

```http
http://contoso-rm4.azurewebsites.net/v1/users/current
headers:
X-Source: true
Authorization: Bearer <JWT Token from ADAL>
```

<span data-ttu-id="42b1f-182">For a user called **Device Manager** in the **ManageDevices** role, the response includes the following JSON in the body:</span><span class="sxs-lookup"><span data-stu-id="42b1f-182">For a user called **Device Manager** in the **ManageDevices** role, the response includes the following JSON in the body:</span></span>

```json
{
  "Id": "userIdExample",
  "Email": "devicemanager@contoso.com",
  "Name": "Device Manager",
  "AllowedActions": [
    "CreateDevices",
    "UpdateDevices",
    "DeleteDevices"
  ]
}
```

<span data-ttu-id="42b1f-183">The following snippet from [deviceDelete.js](https://github.com/Azure/pcs-remote-monitoring-webui/blob/master/src/components/pages/devices/flyouts/deviceDelete/deviceDelete.js) in the [web UI](https://github.com/Azure/pcs-remote-monitoring-webui/) shows how the permissions are enforced declaratively:</span><span class="sxs-lookup"><span data-stu-id="42b1f-183">The following snippet from [deviceDelete.js](https://github.com/Azure/pcs-remote-monitoring-webui/blob/master/src/components/pages/devices/flyouts/deviceDelete/deviceDelete.js) in the [web UI](https://github.com/Azure/pcs-remote-monitoring-webui/) shows how the permissions are enforced declaratively:</span></span>

```json
<FlyoutContent>
  <Protected permission={permissions.deleteDevices}>
    <form className="device-delete-container" onSubmit={this.deleteDevices}>
      ...
    </form>
  </Protected>
</FlyoutContent>
```

<span data-ttu-id="42b1f-184">For more information, see [Protected Components](https://github.com/Azure/pcs-remote-monitoring-webui/blob/master/src/components/shared/protected/README.md).</span><span class="sxs-lookup"><span data-stu-id="42b1f-184">For more information, see [Protected Components](https://github.com/Azure/pcs-remote-monitoring-webui/blob/master/src/components/shared/protected/README.md).</span></span> <span data-ttu-id="42b1f-185">You can define additional permissions in the [authModel.js](https://github.com/Azure/pcs-remote-monitoring-webui/blob/master/src/services/models/authModels.js) file.</span><span class="sxs-lookup"><span data-stu-id="42b1f-185">You can define additional permissions in the [authModel.js](https://github.com/Azure/pcs-remote-monitoring-webui/blob/master/src/services/models/authModels.js) file.</span></span>

### <a name="how-the-microservices-enforce-permissions"></a><span data-ttu-id="42b1f-186">How the microservices enforce permissions</span><span class="sxs-lookup"><span data-stu-id="42b1f-186">How the microservices enforce permissions</span></span>

<span data-ttu-id="42b1f-187">The microservices also check permissions to protect against unauthorized API requests.</span><span class="sxs-lookup"><span data-stu-id="42b1f-187">The microservices also check permissions to protect against unauthorized API requests.</span></span> <span data-ttu-id="42b1f-188">When a microservice receives an API request, it decodes and validates the JWT token to get the user ID and permissions associated with the user's role.</span><span class="sxs-lookup"><span data-stu-id="42b1f-188">When a microservice receives an API request, it decodes and validates the JWT token to get the user ID and permissions associated with the user's role.</span></span>

<span data-ttu-id="42b1f-189">The following snippet from the [DevicesController.cs](https://github.com/Azure/iothub-manager-dotnet/blob/master/WebService/v1/Controllers/DevicesController.cs) file in the [IoTHub Manager microservice](https://github.com/Azure/iothub-manager-dotnet), shows how the permissions are enforced:</span><span class="sxs-lookup"><span data-stu-id="42b1f-189">The following snippet from the [DevicesController.cs](https://github.com/Azure/iothub-manager-dotnet/blob/master/WebService/v1/Controllers/DevicesController.cs) file in the [IoTHub Manager microservice](https://github.com/Azure/iothub-manager-dotnet), shows how the permissions are enforced:</span></span>

```csharp
[HttpDelete("{id}")]
[Authorize("DeleteDevices")]
public async Task DeleteAsync(string id)
{
    await this.devices.DeleteAsync(id);
}
```

## <a name="next-steps"></a><span data-ttu-id="42b1f-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="42b1f-190">Next steps</span></span>

<span data-ttu-id="42b1f-191">In this article, you learned how role-based access controls are implemented in the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="42b1f-191">In this article, you learned how role-based access controls are implemented in the Remote Monitoring solution accelerator.</span></span>

<span data-ttu-id="42b1f-192">For more conceptual information about the Remote Monitoring solution accelerator, see [Remote Monitoring architecture](iot-accelerators-remote-monitoring-sample-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="42b1f-192">For more conceptual information about the Remote Monitoring solution accelerator, see [Remote Monitoring architecture](iot-accelerators-remote-monitoring-sample-walkthrough.md)</span></span>

<span data-ttu-id="42b1f-193">For more information about customizing the Remote Monitoring solution, see [Customize and redeploy a microservice](iot-accelerators-microservices-example.md)
<!-- Next tutorials in the sequence --></span><span class="sxs-lookup"><span data-stu-id="42b1f-193">For more information about customizing the Remote Monitoring solution, see [Customize and redeploy a microservice](iot-accelerators-microservices-example.md)
<!-- Next tutorials in the sequence --></span></span>