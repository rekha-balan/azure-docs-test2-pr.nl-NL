---
title: Configure CHAP for StorSimple 8000 series device | Microsoft Docs
description: Describes how to configure the Challenge Handshake Authentication Protocol (CHAP) on a StorSimple device.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 9ec81ec75f242940e1d49a605d65198dffe3c1e2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556485"
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="fc0bc-103">Configure CHAP for your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="fc0bc-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="fc0bc-104">This tutorial explains how to configure CHAP for your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="fc0bc-105">The procedure detailed in this article applies to StorSimple 8000 series as well as StorSimple 1200 devices.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-105">The procedure detailed in this article applies to StorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="fc0bc-106">CHAP stands for Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="fc0bc-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="fc0bc-108">The verification is based on a shared password or secret.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="fc0bc-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span><span class="sxs-lookup"><span data-stu-id="fc0bc-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="fc0bc-110">One-way CHAP is when the target authenticates an initiator.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-110">One-way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="fc0bc-111">Mutual or reverse CHAP, on the other hand, requires that the target authenticate the initiator and then the initiator authenticate the target.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-111">Mutual or reverse CHAP, on the other hand, requires that the target authenticate the initiator and then the initiator authenticate the target.</span></span> <span data-ttu-id="fc0bc-112">Initiator authentication can be implemented without target authentication.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="fc0bc-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="fc0bc-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="fc0bc-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="fc0bc-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span><span class="sxs-lookup"><span data-stu-id="fc0bc-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="fc0bc-117">Unidirectional or one-way authentication</span><span class="sxs-lookup"><span data-stu-id="fc0bc-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="fc0bc-118">Bidirectional or mutual or reverse authentication</span><span class="sxs-lookup"><span data-stu-id="fc0bc-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="fc0bc-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="fc0bc-120">The detailed steps for this configuration are described in the following tutorial.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="fc0bc-121">Unidirectional or one-way authentication</span><span class="sxs-lookup"><span data-stu-id="fc0bc-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="fc0bc-122">In unidirectional authentication, the target authenticates the initiator.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="fc0bc-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="fc0bc-124">The detailed procedures for your StorSimple device and Windows host are described next.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="fc0bc-125">To configure your device for one-way authentication</span><span class="sxs-lookup"><span data-stu-id="fc0bc-125">To configure your device for one-way authentication</span></span>
1. <span data-ttu-id="fc0bc-126">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-126">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![CHAP Initiator](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="fc0bc-128">Scroll down on this page, and in the **CHAP Initiator** section:</span><span class="sxs-lookup"><span data-stu-id="fc0bc-128">Scroll down on this page, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="fc0bc-129">Provide a user name for your CHAP initiator.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="fc0bc-130">Supply a password for your CHAP initiator.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="fc0bc-131">The CHAP user name must contain fewer than 233 characters.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-131">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="fc0bc-132">The CHAP password must be between 12 and 16 characters.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-132">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="fc0bc-133">A longer user name or password will result in an authentication failure on the Windows host.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-133">A longer user name or password will result in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="fc0bc-134">Confirm the password.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-134">Confirm the password.</span></span>
3. <span data-ttu-id="fc0bc-135">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-135">Click **Save**.</span></span> <span data-ttu-id="fc0bc-136">A confirmation message will be displayed.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="fc0bc-137">Click **OK** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-137">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="fc0bc-138">To configure one-way authentication on the Windows host server</span><span class="sxs-lookup"><span data-stu-id="fc0bc-138">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="fc0bc-139">On the Windows host server, start the iSCSI Initiator.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-139">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="fc0bc-140">In the **iSCSI Initiator Properties** window, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fc0bc-140">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="fc0bc-141">Click the **Discovery** tab.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-141">Click the **Discovery** tab.</span></span>
      
       ![iSCSI initiator properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="fc0bc-143">Click **Discover Portal**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="fc0bc-144">In the **Discover Target Portal** dialog box:</span><span class="sxs-lookup"><span data-stu-id="fc0bc-144">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="fc0bc-145">Specify the IP address of your device.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-145">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="fc0bc-146">Click **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-146">Click **Advanced**.</span></span>
      
       ![Discover target portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="fc0bc-148">In the **Advanced Settings** dialog box:</span><span class="sxs-lookup"><span data-stu-id="fc0bc-148">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="fc0bc-149">Select the **Enable CHAP log on** check box.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-149">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="fc0bc-150">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-150">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="fc0bc-151">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-151">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="fc0bc-152">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-152">Click **OK**.</span></span>
      
       ![Advanced settings general](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="fc0bc-154">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-154">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="fc0bc-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="fc0bc-156">Hence, steps  3-4 will need to be repeated for each volume.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-156">Hence, steps  3-4 will need to be repeated for each volume.</span></span>
   
    ![Volumes mounted as separate targets](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="fc0bc-158">If you change the iSCSI name, the new name will be used for new iSCSI sessions.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-158">If you change the iSCSI name, the new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="fc0bc-159">New settings are not used for existing sessions until you log off and log on again.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="fc0bc-160">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="fc0bc-160">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="fc0bc-161">Bidirectional or mutual authentication</span><span class="sxs-lookup"><span data-stu-id="fc0bc-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="fc0bc-162">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-162">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="fc0bc-163">This requires the user to configure the CHAP initiator settings, as well as the reverse CHAP settings on the device and iSCSI Initiator software on the host.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-163">This requires the user to configure the CHAP initiator settings, as well as the reverse CHAP settings on the device and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="fc0bc-164">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-164">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="fc0bc-165">To configure your device for mutual authentication</span><span class="sxs-lookup"><span data-stu-id="fc0bc-165">To configure your device for mutual authentication</span></span>
1. <span data-ttu-id="fc0bc-166">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-166">In the Azure classic portal, on the **Devices** page, click the **Configure** tab.</span></span>
   
    ![CHAP target](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="fc0bc-168">Scroll down on this page, and in the **CHAP Target** section:</span><span class="sxs-lookup"><span data-stu-id="fc0bc-168">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="fc0bc-169">Provide a **Reverse CHAP user name** for your device.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="fc0bc-170">Supply a **Reverse CHAP password** for your device.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="fc0bc-171">Confirm the password.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-171">Confirm the password.</span></span>
3. <span data-ttu-id="fc0bc-172">In the **CHAP Initiator** section:</span><span class="sxs-lookup"><span data-stu-id="fc0bc-172">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="fc0bc-173">Provide a **user name** for your device.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="fc0bc-174">Provide a **password** for your device.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="fc0bc-175">Confirm the password.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-175">Confirm the password.</span></span>
4. <span data-ttu-id="fc0bc-176">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-176">Click **Save**.</span></span> <span data-ttu-id="fc0bc-177">A confirmation message will be displayed.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="fc0bc-178">Click **OK** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-178">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="fc0bc-179">To configure bidirectional authentication on the Windows host server</span><span class="sxs-lookup"><span data-stu-id="fc0bc-179">To configure bidirectional authentication on the Windows host server</span></span>
1. <span data-ttu-id="fc0bc-180">On the Windows host server, start the iSCSI Initiator.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-180">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="fc0bc-181">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-181">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="fc0bc-182">Click **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="fc0bc-183">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span><span class="sxs-lookup"><span data-stu-id="fc0bc-183">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="fc0bc-184">Type the **Reverse CHAP Password** that you configured in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-184">Type the **Reverse CHAP Password** that you configured in the Azure classic portal.</span></span>
   2. <span data-ttu-id="fc0bc-185">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-185">Click **OK**.</span></span>
      
       ![iSCSI initiator mutual CHAP secret](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="fc0bc-187">Click the **Targets** tab.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-187">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="fc0bc-188">Click the **Connect** button.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-188">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="fc0bc-189">In the **Connect To Target** dialog box, click **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-189">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="fc0bc-190">In the **Advanced Properties** dialog box:</span><span class="sxs-lookup"><span data-stu-id="fc0bc-190">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="fc0bc-191">Select the **Enable CHAP log on** check box.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-191">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="fc0bc-192">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-192">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="fc0bc-193">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-193">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="fc0bc-194">Select the **Perform mutual authentication** check box.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-194">Select the **Perform mutual authentication** check box.</span></span>
      
       ![Advanced settings mutual authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="fc0bc-196">Click **OK** to complete the CHAP configuration</span><span class="sxs-lookup"><span data-stu-id="fc0bc-196">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="fc0bc-197">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="fc0bc-197">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="fc0bc-198">Additional considerations</span><span class="sxs-lookup"><span data-stu-id="fc0bc-198">Additional considerations</span></span>
<span data-ttu-id="fc0bc-199">The **Quick Connect** feature does not support connections that have CHAP enabled.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-199">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="fc0bc-200">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-200">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![Connect to target](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="fc0bc-202">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-202">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="fc0bc-203">This ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-203">This ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="fc0bc-204">Errors during configuration</span><span class="sxs-lookup"><span data-stu-id="fc0bc-204">Errors during configuration</span></span>
<span data-ttu-id="fc0bc-205">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-205">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="fc0bc-206">Verification of CHAP configuration</span><span class="sxs-lookup"><span data-stu-id="fc0bc-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="fc0bc-207">You can verify that CHAP is being used by completing the following steps.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-207">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="fc0bc-208">To verify your CHAP configuration</span><span class="sxs-lookup"><span data-stu-id="fc0bc-208">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="fc0bc-209">Click **Favorite Targets**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="fc0bc-210">Select the target for which you enabled authentication.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-210">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="fc0bc-211">Click **Details**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-211">Click **Details**.</span></span>
   
    ![iSCSI initiator properties favorite targets](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="fc0bc-213">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-213">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="fc0bc-214">If the configuration was successful, it should say **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="fc0bc-214">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![Favorite target details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="fc0bc-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc0bc-216">Next steps</span></span>
* <span data-ttu-id="fc0bc-217">Learn more about [StorSimple security](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="fc0bc-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="fc0bc-218">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="fc0bc-218">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>












