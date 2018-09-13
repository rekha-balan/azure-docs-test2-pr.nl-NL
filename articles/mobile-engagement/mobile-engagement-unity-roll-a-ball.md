---
title: Unity Roll a Ball tutorial
description: Steps to create the classic Unity Roll a Ball game which is a pre-requisite for all Mobile Engagement Unity tutorials
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fe3fc276a0f94ca4c9b1f9c06cb42ccdf58c74af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556539"
---
# <a id="unity-roll-a-ball"></a><span data-ttu-id="e6ab4-103">Create Unity Roll a Ball game</span><span class="sxs-lookup"><span data-stu-id="e6ab4-103">Create Unity Roll a Ball game</span></span>
<span data-ttu-id="e6ab4-104">This tutorial walks through the main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="e6ab4-104">This tutorial walks through the main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="e6ab4-105">This sample game consists of a spherical 'player' object which is controlled by the app user and the objective of the game is to 'collect' collectible objects by colliding the player object with these collectible objects.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-105">This sample game consists of a spherical 'player' object which is controlled by the app user and the objective of the game is to 'collect' collectible objects by colliding the player object with these collectible objects.</span></span> <span data-ttu-id="e6ab4-106">This assumes basic familiarity with Unity editor environment.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="e6ab4-107">If you run into any issues then you should refer to the full tutorial.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-107">If you run into any issues then you should refer to the full tutorial.</span></span> 

### <a name="setting-up-the-game"></a><span data-ttu-id="e6ab4-108">Setting up the game</span><span class="sxs-lookup"><span data-stu-id="e6ab4-108">Setting up the game</span></span>
<span data-ttu-id="e6ab4-109">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="e6ab4-109">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="e6ab4-110">Open **Unity Editor** and click **New**.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="e6ab4-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="e6ab4-112">Save the default scene just created as part of the new project as with the name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span><span class="sxs-lookup"><span data-stu-id="e6ab4-112">Save the default scene just created as part of the new project as with the name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="e6ab4-113">Create a **3D Object -> Plane** as the playing field and rename this plane object as **Ground**</span><span class="sxs-lookup"><span data-stu-id="e6ab4-113">Create a **3D Object -> Plane** as the playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="e6ab4-114">Reset the transform component for this **Ground** object so that it is at the Origin.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-114">Reset the transform component for this **Ground** object so that it is at the Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="e6ab4-115">Uncheck **Show Grid** from **Gizmos menu** for the **Ground** object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-115">Uncheck **Show Grid** from **Gizmos menu** for the **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="e6ab4-116">Update the **Scale** component for the **Ground** object to be [X = 2,Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="e6ab4-116">Update the **Scale** component for the **Ground** object to be [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="e6ab4-117">Add a new **3D Object -> Sphere** to the project and rename this sphere object as **Player**.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-117">Add a new **3D Object -> Sphere** to the project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="e6ab4-118">Select the **Player** object and click **Reset Transform** similar to the Plane object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-118">Select the **Player** object and click **Reset Transform** similar to the Plane object.</span></span> 
10. <span data-ttu-id="e6ab4-119">Update **Transform -> Position -> Y Coordinate** component for the Player Y as 0.5.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-119">Update **Transform -> Position -> Y Coordinate** component for the Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="e6ab4-120">Create a new folder called **Materials** in the project where we will create the material to color the player.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-120">Create a new folder called **Materials** in the project where we will create the material to color the player.</span></span> 
12. <span data-ttu-id="e6ab4-121">Create a new **Material** called **Background** in this folder.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="e6ab4-122">Update the color of the material by updating the **Albedo** property of it.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-122">Update the color of the material by updating the **Albedo** property of it.</span></span> <span data-ttu-id="e6ab4-123">You can select the RGB values of [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="e6ab4-123">You can select the RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="e6ab4-124">Drag this material into the scene view to apply color to the **Ground** object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-124">Drag this material into the scene view to apply color to the **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="e6ab4-125">Finally update the **Transform -> Rotation -> Y** to 60 on the Directional Light object for clarity.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-125">Finally update the **Transform -> Rotation -> Y** to 60 on the Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-the-player"></a><span data-ttu-id="e6ab4-126">Moving the player</span><span class="sxs-lookup"><span data-stu-id="e6ab4-126">Moving the player</span></span>
<span data-ttu-id="e6ab4-127">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="e6ab4-127">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="e6ab4-128">Add a **RigidBody** component to the **Player** object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-128">Add a **RigidBody** component to the **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="e6ab4-129">Create a new folder called **Scripts** in the Project.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-129">Create a new folder called **Scripts** in the Project.</span></span> 
3. <span data-ttu-id="e6ab4-130">Click **Add Component-> New Script -> C# Script**.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="e6ab4-131">Name it **PlayerController**, and click **Create and Add**.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="e6ab4-132">This will create and attach a script to the Player object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-132">This will create and attach a script to the Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="e6ab4-133">Move this script under the **Scripts** folder in the project.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-133">Move this script under the **Scripts** folder in the project.</span></span> 
5. <span data-ttu-id="e6ab4-134">Open the script for editing in your favorite script editor, update the script code with the following code and save it.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-134">Open the script for editing in your favorite script editor, update the script code with the following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="e6ab4-135">Note that the script above uses a **Speed** property.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-135">Note that the script above uses a **Speed** property.</span></span> <span data-ttu-id="e6ab4-136">In the Unity editor, update the speed property to 10.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-136">In the Unity editor, update the speed property to 10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="e6ab4-137">Hit **Play** in the Unity Editor.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-137">Hit **Play** in the Unity Editor.</span></span> <span data-ttu-id="e6ab4-138">Now you should be able to control the ball using the keyboard and it should rotate and move around.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-138">Now you should be able to control the ball using the keyboard and it should rotate and move around.</span></span> 

### <a name="moving-the-camera"></a><span data-ttu-id="e6ab4-139">Moving the camera</span><span class="sxs-lookup"><span data-stu-id="e6ab4-139">Moving the camera</span></span>
<span data-ttu-id="e6ab4-140">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie the **Main Camera** to the **Player** object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-140">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie the **Main Camera** to the **Player** object.</span></span> 

1. <span data-ttu-id="e6ab4-141">Update the **Transform.Position** to be X = 0,  Y = 10.5, Z=-10.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-141">Update the **Transform.Position** to be X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="e6ab4-142">Update the **Transform.Rotation** to be X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-142">Update the **Transform.Rotation** to be X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="e6ab4-143">Add a new script called **CameraController** to the **MainCamera** and move it under the Scripts folder.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-143">Add a new script called **CameraController** to the **MainCamera** and move it under the Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="e6ab4-144">Open up the script for editing and add the following code in it:</span><span class="sxs-lookup"><span data-stu-id="e6ab4-144">Open up the script for editing and add the following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="e6ab4-145">In Unity environment - drag the Player variable into the Player slot for the Main Camera object so that the two are associated with one another.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-145">In Unity environment - drag the Player variable into the Player slot for the Main Camera object so that the two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="e6ab4-146">Now if you hit Play in the Unity editor and rotate the Player Ball object then you will see the Camera following it in the movement.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-146">Now if you hit Play in the Unity editor and rotate the Player Ball object then you will see the Camera following it in the movement.</span></span>  

### <a name="setting-up-the-play-area"></a><span data-ttu-id="e6ab4-147">Setting up the Play area</span><span class="sxs-lookup"><span data-stu-id="e6ab4-147">Setting up the Play area</span></span>
<span data-ttu-id="e6ab4-148">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="e6ab4-148">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="e6ab4-149">We will create the Walls surrounding the Ground so that the Player Ball object doesn't drop off the play area in its movement.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-149">We will create the Walls surrounding the Ground so that the Player Ball object doesn't drop off the play area in its movement.</span></span> 

1. <span data-ttu-id="e6ab4-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span><span class="sxs-lookup"><span data-stu-id="e6ab4-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="e6ab4-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span><span class="sxs-lookup"><span data-stu-id="e6ab4-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="e6ab4-152">Update the **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-152">Update the **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="e6ab4-153">Duplicate the West wall to create an **East wall** with the updated transform position and scale.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-153">Duplicate the West wall to create an **East wall** with the updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="e6ab4-154">Duplicate the East wall to create a **North wall** with the updated transform position & scale.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-154">Duplicate the East wall to create a **North wall** with the updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="e6ab4-155">Duplicate the North wall and create a **South wall** with the updated transform position & scale.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-155">Duplicate the North wall and create a **South wall** with the updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="e6ab4-156">Creating Collectible objects</span><span class="sxs-lookup"><span data-stu-id="e6ab4-156">Creating Collectible objects</span></span>
<span data-ttu-id="e6ab4-157">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="e6ab4-157">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="e6ab4-158">We will create some attractive looking objects which will form the set of collectible objects which the Player Ball object needs to 'collect' by colliding with them.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-158">We will create some attractive looking objects which will form the set of collectible objects which the Player Ball object needs to 'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="e6ab4-159">Create a new **3D Cube object** and name it Pickup.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="e6ab4-160">Adjust the **Transform -> Rotation** & **Transform -> Scale** of the Pickup object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-160">Adjust the **Transform -> Rotation** & **Transform -> Scale** of the Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="e6ab4-161">Create and attach a **new C# Script** called **Rotator** to the Pickup object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-161">Create and attach a **new C# Script** called **Rotator** to the Pickup object.</span></span> <span data-ttu-id="e6ab4-162">Make sure to put the script under the Scripts folder.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-162">Make sure to put the script under the Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="e6ab4-163">Open this script for editing and update it to be the following:</span><span class="sxs-lookup"><span data-stu-id="e6ab4-163">Open this script for editing and update it to be the following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="e6ab4-164">Now hit the Play mode in the Unity Editor and your Pickup object show be rotating on its axis.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-164">Now hit the Play mode in the Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="e6ab4-165">Create a new folder called **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="e6ab4-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="e6ab4-166">Drag the **Pickup** object and put it in the Prefabs folder.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-166">Drag the **Pickup** object and put it in the Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="e6ab4-167">Create a new **Empty Game object** called **Pickups**.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="e6ab4-168">Reset its position to origin and then drag the Pickup object under this game object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-168">Reset its position to origin and then drag the Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="e6ab4-169">Duplicate the **Pickup** object and spread it on the **Ground** object around the **Player** object by updating the **Transform.Position's X & Z** values appropriately.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-169">Duplicate the **Pickup** object and spread it on the **Ground** object around the **Player** object by updating the **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="e6ab4-170">Create a **new material** called **Pickup** and update it to be Red in color by updating the **Albedo property** similar to what we did for updating the Ground object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-170">Create a **new material** called **Pickup** and update it to be Red in color by updating the **Albedo property** similar to what we did for updating the Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="e6ab4-171">Apply the material to all the 4 pickup objects.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-171">Apply the material to all the 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-the-pickup-objects"></a><span data-ttu-id="e6ab4-172">Collecting the Pickup objects</span><span class="sxs-lookup"><span data-stu-id="e6ab4-172">Collecting the Pickup objects</span></span>
<span data-ttu-id="e6ab4-173">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="e6ab4-173">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="e6ab4-174">We will update the Player so that it is able to 'collect' the pickup objects by colliding with them.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-174">We will update the Player so that it is able to 'collect' the pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="e6ab4-175">Open up the **PlayerController** script attached to the Player object for editing and update it to the following:</span><span class="sxs-lookup"><span data-stu-id="e6ab4-175">Open up the **PlayerController** script attached to the Player object for editing and update it to the following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="e6ab4-176">Create a new **Tag** called **Pick Up** (it must match what is in the script)</span><span class="sxs-lookup"><span data-stu-id="e6ab4-176">Create a new **Tag** called **Pick Up** (it must match what is in the script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="e6ab4-177">Apply this **Tag** to the Prefab Pickup object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-177">Apply this **Tag** to the Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="e6ab4-178">Enable **IsTrigger** checkbox for the Prefab object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-178">Enable **IsTrigger** checkbox for the Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="e6ab4-179">Add a Rigid body to Pickup Prefab object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-179">Add a Rigid body to Pickup Prefab object.</span></span> <span data-ttu-id="e6ab4-180">For performance optimization we will update the static collider that we used to a Dynamic collider.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-180">For performance optimization we will update the static collider that we used to a Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="e6ab4-181">Finally check the **IsKinematic** property for the prefab object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-181">Finally check the **IsKinematic** property for the prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="e6ab4-182">Hit **Play** in the Unity editor and you will be able to play this **Roll a Ball** game by moving the Player object using your keyboard keys for direction input.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-182">Hit **Play** in the Unity editor and you will be able to play this **Roll a Ball** game by moving the Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-the-game-for-mobile-play"></a><span data-ttu-id="e6ab4-183">Updating the game for mobile play</span><span class="sxs-lookup"><span data-stu-id="e6ab4-183">Updating the game for mobile play</span></span>
<span data-ttu-id="e6ab4-184">The sections above concluded the basic tutorial from Unity.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-184">The sections above concluded the basic tutorial from Unity.</span></span> <span data-ttu-id="e6ab4-185">Now we will modify the game to make it mobile device friendly.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-185">Now we will modify the game to make it mobile device friendly.</span></span> <span data-ttu-id="e6ab4-186">Note that we used keyboard input for the game so far for testing.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-186">Note that we used keyboard input for the game so far for testing.</span></span> <span data-ttu-id="e6ab4-187">Now we will modify it so that we can control the player by using the motion of the phone i.e. using Accelerometer as the input.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-187">Now we will modify it so that we can control the player by using the motion of the phone i.e. using Accelerometer as the input.</span></span> 

<span data-ttu-id="e6ab4-188">Open up the **PlayerController** script for editing and update the **FixedUpdate** method to use the motion from the accelerometer to move the Player object.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-188">Open up the **PlayerController** script for editing and update the **FixedUpdate** method to use the motion from the accelerometer to move the Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="e6ab4-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice to play the game.</span><span class="sxs-lookup"><span data-stu-id="e6ab4-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice to play the game.</span></span> 

<!-- Images -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/8.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/12.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/13.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/14.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/15.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/16.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/17.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/18.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-unity-roll-a-ball/save-scene.png






















































