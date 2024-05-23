# Bigscreen Environment Setup
This document will go through the process of setting up your Unity scene to work in Bigscreen. If you have not already, extract the _BigscreenTemplate_v1.unitypackage_ file and put it somewhere accessible.

## 1) Unity Project
_If you already have a Unity project created with your environment, this section can be skipped._
You should have an app called _Unity Hub_ installed. Download here: https://unity.com/unity-hub

1. Under _Installs_, ensure a valid Unity installation is there. If not, install one using _Install Editor_. Unity version _2020.3.33f1_ or greater is recommended. We will use _2020.3.33f1_ for illustrations in this document. Note: Newer Unity versions may have different editor UI and layout from the snapshot figures in this document.

![image](https://github.com/assets/50002278/c45bb0f3-4877-4cdb-8eab-2251eec122ff)

2. In the _Projects_ tab, click _New project_. In _All templates_, look for _3D (Built-In Render Pipeline)_
3. Select this template and give it a project name, location, and your org. Finally, click _Create project_.

![image](https://github.com/assets/50002278/59cbba5a-14f8-4a2b-bbe7-deaeffdf7dca)



## 2) Project Preparation
In the created project from _section 1_, you will start in a _SampleScene_. In the _Project_ window, right click the _Scenes_ folder and delete it.
![image](https://github.com/assets/50002278/7cd8d998-fc8c-40e2-a549-ba00389a7d2f)

1. In the top bar of Unity, click _Assets_ > _Import Package_ > _Custom Package..._
2. Go to the _BigscreenTemplate_v1.unitypackage_ file you extracted earlier and open it.
3. An import window will appear in Unity. Make sure all the files are ticked then click _Import_.

![image](https://github.com/assets/50002278/47b3a55e-1036-4399-9a64-54c5ddae4852)

4. In the _Project_ window, expand _UserEnvironments_ and right click _Scenes_ then _Create_ > _Folder_. To avoid issues integrating your environment, give the folder the name of your environment followed by your Bigscreen username. Create new folders with the same name into the following folders:
  - _Audio_
  - _Lightbakes_
  - _Lightbakes_ > _ScreenLitVariants_
  - _Materials_
  - _Models_
  - _Scenes_

These folders will contain your environment's assets.

![image](https://github.com/assets/50002278/abd12cb5-30d5-42a8-bdc9-2352772ec6af)

5. Right click your unique folder in _Scenes_ from _step 4_ then click _Create_ > _Scene_. Give the scene your environment name.
6. Open your scene. _Don't save the SampleScene if that popup appears._
7. Delete _Main Camera_ and _Directional Light_ objects then in the _Project_ window under _TemplateAssets_ > _Prefabs_ > _Environments_, take the _SceneRoot_ prefab and drag it from the _Project_ window and into the _Hierarchy_ window in Unity. The template with required assets should appear in the _Scene_ view.

![image](https://github.com/assets/50002278/e409c287-2eab-43cf-aee9-1f52fe1aa003)
![image](https://github.com/assets/50002278/5deef6ef-6631-4496-b65b-efc915ba7847)



## 3) Integrating with the Template
The template has three root objects:
- _Areas_ -- this contains the seats, collisions, and screen placeholders for Bigscreen to use.
- _Environment_ -- this should house your environment's mesh GameObjects.
- _Lighting_ -- this will contain lighting objects for your environment including screen emissives. More on this in the _Lightbaking_ section.

In _TemplateAssets_ > _Prefabs_ > _Environments_, there is a _ScaleReferenceFigure_ asset that you can drag into your scene for referencing the scale of your environment and seating with a Bigscreen avatar. Note: This is not an asset to export with your environment.
![image](https://github.com/assets/50002278/720ec1b7-4857-44a9-b997-15b61ffcf34a)

Some objects in the template will have missing script components. **Do not remove these components as they hold important references and doing so will cause integration problems with your submission which will end up not being accepted.**

Let's explain what the objects in the template are for. Items with (*) are required setup for accepting environment submission.

### Seats*
There are two seat prefabs for use in Bigscreen:
- _Seat_ -- these are primarily used for the main viewing seats you want users at. The _bigscreen_ placeholder illustrates the direction the user will orient when teleporting to that seat and the default position a floating monitor will end up when resetting its position.
- _SeatTransitional_ -- these are the floor panels that are used for moving around the environment. They are typically used in flat open spaces with less suitable viewing spots. The _bigscreen_ placeholder illustrates the default position a floating monitor will end up when resetting its position.

- **Do not modify the seat prefabs nor unpack them as it can cause integration problems with your submission and will end up not being accepted. They are only meant for moving and rotating around in your environment. You can duplicate or remove the seat objects as you please.**
- **15 or more starting seats are required to work with a full room in Bigscreen.**
- **There should not be any seats that are set inactive. If you don't need a seat object, you must delete it.**
- **We recommend using Unity's snap settings for moving seats around in an even fashion. You can set the snap increment by going to _Edit_ > _Grid and Snap Settings..._ > _Increment Snap_**. **You hold _CTRL_ while moving an object to start snapping it in increments.**
  - **For _SeatTransitional_ objects, they use an increment of _0.8_ for forming a grid.**
  - **_Seat_ objects can be any spacing you want but it is recommended to have equal spacing when possible.**

![image](https://github.com/assets/50002278/04e8f5e6-3a06-49c4-8e4f-db728bedefa9)


The order that users spawn into their seats is sorted based on the upper-most seat in the hierarchy within the _Seats_ object. The first seat at the very top will be the default seat the host spawns at. The seat object below it will be the seat the first user that joins the host's room spawns at then so on and so forth.
![image](https://github.com/assets/50002278/ae095ba6-c9e6-4bf2-adc7-1820a6fa2bc6)

### Screens*
Provided are two screen objects under _Areas_:
- _ScreenPlaceholder_ -- this is where the primary screen will appear in your environment. You can adjust the position and rotation of this as you please. **There should only be one _ScreenPlaceholder_ in your environment.**
- _MirroredScreenContainer_ (optional) -- this has the mirrored screen which as the name suggests will mirror what the room host's primary screen is showing. This is optional and if you don't plan to use mirrored screens, it is recommended to delete it from the scene. You can adjust the size of the mirrored screen by changing the size of the inner _MirroredScreen_ object inside the container. Do not change the rotation or position of this object. Only do that on the _MirroredScreenContainer_ itself. You can duplicate the _MirroredScreenContainer_ to add more screens but at this time, we require that you only have 30 mirrored screens or less.

**The aspect ratio of the _ScreenPlaceholder_ and _MirroredScreen_ must stay as 16:9. You can scale the screens appropriately by enabling the _Scale Tool_ in Unity then dragging the center white cube of the scale tool to change the size of the screen.**
![image](https://github.com/assets/50002278/2d0bcded-d512-4d20-bc57-4e858c8eb16b)

### Colliders*
It's important to get your environment's collision setup. Otherwise toys will fall through geometry and will not make a good user experience. This is a required step to get your environment submission accepted.
Under _Colliders_, there are four _BoxCollider_ GameObjects representing the collision of the environment. You should add or remove any collider objects and adjust them to suit your environment's needs.
You can resize the _BoxCollider_ objects by using the bounding volume editor.
![image](https://github.com/assets/50002278/4967879a-e81a-417e-b347-9fa4db6b046e)

Optionally, you can attach _BoxCollider_ components to your mesh GameObjects and adjust the bounding size there. With that setup, however, you must make sure the Layer assigned to your mesh GameObjects are on _Ignore Raycast_.

**Mesh Colliders are permitted as long as they are used sparingly and are low poly. For example, using Mesh Colliders for flat flooring, flat walls, dectorative objects, or duplicated theater seats are not permitted use cases.**

### Camera Tool Angles
Under _Cameras_ there are three _CameraAnchor_ objects. These are used by the app's Camera tool's _2, 3, and 4_ angles. The arrows indicate where the camera will position and orient in your environment. You can move and rotate the camera anchors as you please. Avoid changing the inner _Indicator_ object though.
![image](https://github.com/assets/50002278/629e2152-b617-4e9c-8740-3cc622a9be30)

### MonitorOcclusionDetector
The bounding box collider of this object is used to tell when a user's floating monitor is outside the environment when switching environments. If a monitor is outside the bounds when entering the environment, the monitor resets to its default position in front of the user. It is recommended to set this BoxCollider boundary size to roughly fit your environment's geometry and just below your primary flooring.
![image](https://github.com/assets/50002278/25208af8-4bfc-4746-bb75-6c926828bb46)

Let's start integrating with the template. In this example, we will walk through making a simple environment with a giant donut and a big screen in front.
1. We first right click _SceneRoot_ in the _Hierarchy_ window then click _Prefab_ > _Unpack_ (avoid _Unpack Completely_).
2. We then remove the template's floor and table objects under _Environment_.
3. Next, let's add the donut mesh. We'll take a .fbx donut mesh for this example and copy it into _Models_ > _LargeDonut_Q_Q_ through File Explorer.
4. We will click the _Donut_ mesh and drag it into the _Environment_ object in the _Hierarchy_.

![image](https://github.com/assets/50002278/eb11c82e-c012-4a31-825a-523f464f6499)

5. The mesh will need its size and position adjusted.

![image](https://github.com/assets/50002278/2bff7634-4bdb-41fc-a31a-de4ef6837e1f)

6. Next, we add the materials and give it some color. The materials created will go in _Materials_ > _LargeDonut_Q_Q_

![image](https://github.com/assets/50002278/a3b1a4b0-7210-4cc6-917c-0895e01f5cd7)

7. Let's adjust the seating. We will keep the transitional seats and setup the diamond seats to be in two rows. The host entering this environment will appear at the selected seat which is the highest in the hierarchy.

![image](https://github.com/assets/50002278/a4b7fdf4-8c82-4a35-b537-e4db3e3b398d)

8. Next are screens. Let's resize the _ScreenPlaceholder_ to an appropriate size and delete the _MirroredScreenContainer_ as it is not needed for the environment.

![image](https://github.com/assets/50002278/1b3ab230-54a0-4d63-8b7f-41f8dccfabe9)

9. We will fit the MonitorOcclusionDetector to the environment's spec.

![image](https://github.com/assets/50002278/996e92fc-16cf-499c-b0cf-40288ebb5a73)

10. The CameraAnchors need to be adjusted. We will set them in three different angles pointing to where users sit.

![image](https://github.com/assets/50002278/18de48ae-3d43-409e-a202-2f590e03e679)

11. Finally, colliders are setup. To help aid collision setup, let's enable collider visuals in the scene by going to _Window_ > _Analysis_ > _Physics Debugger_ then enable _Gizmos_ and _Collision Geometry_ in the scene view.
12. Because of the unique shape, we start with a collision segment using the provided _Collider_ objects in the template then duplicate and rotate the segments around the torus shape.

![image](https://github.com/assets/50002278/c75deaac-8ca4-4922-b636-38baf6c016df)
![image](https://github.com/assets/50002278/2d85c515-15b4-459f-8309-ec48c507ebb6)

🎉The scene setup is now done! Next we will look at lightbaking in the next section to get screen lights to work in the environment.



## 4) Lightbaking
Bigscreen uses lightbaking to emit screen lighting while being performant on PC and Quest. There are two variations: _lights up_ and _screen lit_. Both of these are used when dimming the lights in your environment. When no content is on-screen, the app will fade to your _lights up_ lightmap.

It is important to assign your meshes with a simple material that's either assigned its texture assets or opaque with color. We recommend using the _Standard_ shader for your materials. When importing your environment into Bigscreen, we will assign the right shaders to the materials so screen lighting can work. **We do not accept having any realtime lighting setups nor complex shaders.** If there is a use case for a unique material or shader for object(s) in your environment, let us know about it in your submission ticket.

**You must ensure that all of your mesh objects you intend to lightbake with your environment have non-overlapping UV maps. If you lightbake otherwise, you end up with artifacts and screen lighting will not work appropriate.**

There are scenarios where a screen lit lightbake of your environment is not needed. Any environments you intend to be fairly lit at all times will not need _screen lit_ lightmap(s) but only the _lights up_ lightmap(s). Screen lighting will not be active in this scenario.

### Setup
For this example, we will use the native Unity lightbaking system but any other baking asset you use would work granted that it does not produce separate direction lightmaps. Additionally, we will use the same environment that we have setup in _section 3_. Note: Your editor UI pertaining to lightbakes may differ in newer Unity versions from the below figure snapshots.

1. We first need to set all of the environment's mesh GameObjects to _Static_ for lightbakes to use their surfaces.

![image](https://github.com/assets/50002278/ea545fc8-6862-44b0-a7e5-a5872964eeb4)

2. Now we make the _Lighting_ object under _SceneRoot_ active. This contains the screen emissive objects that will emit the lighting for the _screen lit_ lightmap(s).

![image](https://github.com/assets/50002278/485c8cf6-68b2-41e4-96fd-7ca99ee71ecf)

3. Since we are not using any mirrored screens in this environment, we will remove the screen emissive included in the template that was representing the _MirroredScreenContainer_ object. Optionally, you can duplicate the _ScreenEmissive_ and resize/position it to fit over any mirrored screens your environment contains.

4. We will position then resize the _ScreenEmissive_ to represent the _ScreenPlaceholder_ object in our environment. This is for the _screen lit_ lightmap.

![image](https://github.com/assets/50002278/70cc5291-0ff9-4ebe-a1fa-a82bb8001764)

5. The environment needs a some lighting for the _lights up_ lightmap. To do this, we add a _Directional Light_ to the scene under _Lighting_ then adjust the position and color. You can use any of the Unity lighting effects in your environment for lightbaking the _lights up_ lightmap. All Unity lighting objects need to have their _Mode_ set to _Baked_. Depending on your scene, you may need to adjust any light object's _Intensity_ to get the desired lightbake output if you find the default value is too dim. Keep in mind if you use a third party lightbake solution, it may have its own objects for emitting light onto a scene.

![image](https://github.com/assets/50002278/7e7caf69-8127-44d7-b1e3-2ddfae8a699b)
![image](https://github.com/assets/50002278/c542b076-bd7f-4fed-b182-c15bcd6211da)

6. With the _lights up_ and _screen lit_ setup done, we hide the _Areas_ object under _SceneRoot_ as we do not want its objects influencing the lighting in the environment.

7. First we start with the _screen lit_ lightbake. **If your enviroment is intended to be screen lit, you must run the _screen lit_ lightbake first then do _lights up_.** We need to set the lights that were setup in _step 5_ as inactive and leave only _ScreenEmissive_ objects active.

![image](https://github.com/assets/50002278/fd0d9096-8904-42f2-ab93-0ce0b891e7ed)

8. Now open the _Lighting_ window by going to _Window_ > _Rendering_ > _Lighting_.

![image](https://github.com/assets/50002278/215496f2-7149-4edb-9b7d-c5b7d1be2f81)

9. With the _Scene_ tab active, click on _New Lighting Settings_. This will save a lighting asset to the current folder the _Project_ window has selected. It is recommended to select your lightbake folder under _Lightbakes_ in the _Project_ window so that the file ends up there.

![image](https://github.com/assets/50002278/615e3300-acb3-4196-a594-e090eeb636e0)
![image](https://github.com/assets/50002278/5064f6a1-3c39-4fd3-9204-696a971f278b)

10. For _screen lit_, we will need to bake with lighting mode set to _Shadowmask_ and Global Illumination enabled. Additionally, we need to set _Directional Mode_ to _Non-Directional_ so the appropriate lightmap files are produced.

![image](https://github.com/assets/50002278/c2ef8a0d-60b2-471c-915b-38b431dfbc3c)
![image](https://github.com/assets/50002278/2db56736-4ff9-4200-9f81-0c6f513a60b6)

11. We will keep the other settings as default but you may have to tune some numeric values under _Lightmapper_ to suit your environment's needs. You can view more info on these settings here: https://docs.unity3d.com/Manual/progressive-lightmapper.html

12. Now we click _Generate Lighting_ and wait for the process to finish.

13. This is our result for the _screen lit_ lightmap. It seems a little too dim, so let's adjust the _ScreenEmissive_ intensity to emit more light. You may have to adjust this too depending on your environment and lightbake output.

![image](https://github.com/assets/50002278/8b03b3d1-7654-438f-b195-b91c853efcd0)

14. We will select the _ScreenEmissive_ object then scroll down to its material at the bottom of the _Inspector_ window.

![image](https://github.com/assets/50002278/96e9e406-aeb3-481e-a256-6ade26a400d2)

15. From here we select the _HDR_ button under _Emission_ to change the _Intensity_. We will assign its _Intensity_ to 1.25. **For screen lighting to work appropriate in Bigsreen, the color of the _ScreenEmissive_ must stay white.**

![image](https://github.com/assets/50002278/e6b45e16-1097-49d0-9cb0-ab077e48caab)

16. Now we open the _Lighting_ window again and rebake similar to _step 11_. The _screen lit_ bake now looks better. It's best to not make your _screen lit_ lighting too bright that there is little falloff as it can produce unrealistic screen lighting in your environment.

![image](https://github.com/assets/50002278/5f582018-108f-40a8-8446-b75fd909bc83)

17. With the _screen lit_ lightbake finished, we need to take the produced lightmap files and copy them over to _Lightbakes_ > _ScreenLitVariants_ > _LargeDonut_Q_Q_. You can find the lightmap file location by clicking on a mesh GameObject in your environment, then selecting the _Baked Lightmap_ image in _Inspector_.

![image](https://github.com/assets/50002278/65223b58-51f4-4ecd-8e5f-4b2113d91ac9)

18. Right click the lightmap file and _Show in Explorer_.
19. The lightbake produced two lightmap files. We will highlight those including its _.meta_ files then copy them.

![image](https://github.com/assets/50002278/b73b6fd1-1d13-4eea-98a0-4beb9ae203fb)

21. Next we paste those files into the location using File Explorer: _Lightbakes_ > _ScreenLitVariants_ > _LargeDonut_Q_Q_. Unity will show them in the Project window.

![image](https://github.com/assets/50002278/5158b37d-874b-4576-9558-43ca1a9f375e)

21. Now we move on to lightbaking the _lights up_ lightmap. This is a similar process to _screen lit_.
22. In the _Hierarchy_ window in Unity, set the _ScreenEmissive_ objects to inactive and set all of your lighting objects active.

![image](https://github.com/assets/50002278/ab9db348-a7c7-4622-90d2-059727cf6a4c)

23. Now open the _Lighting_ window in Unity and set _Lighting Mode_ to _Baked Indirect_

![image](https://github.com/assets/50002278/7fe6918d-9fdf-44b8-8b45-f50e135e9972)

24. Now click _Generate Lighting_. After it finishes, we now have our _lights up_ lightmap.

![image](https://github.com/assets/50002278/69c5b08e-6e2a-4643-a4d7-b5e518255a53)

25. We will need to find the lightmap file again. You can find the lightmap file location by clicking on a mesh GameObject in your environment, then selecting the _Baked Lightmap_ image in _Inspector_.

![image](https://github.com/assets/50002278/a35e36db-a10d-4713-9eaf-6f12b9c221c3)

26. This time we will not copy the files but instead move them into _Lightbakes_ > _LargeDonut_Q_Q_.

![image](https://github.com/assets/50002278/a57227af-b60a-404f-9772-1c3644b4321c)

🎉Lightbaking is now done! Next we will go over exporting your environment so it can integrate into Bigscreen smoothly.



## 5) Exporting your Environment
When exporting your environment, you need to make sure all of your environment's assets are under _UserEnvironments_ and under the subfolders you created from _section 2_. Failure to do so will cause missing assets to occur when integrating your environment into Bigscreen. You must also export assets that are **only used in your environment** and no extra assets left over from other environment projects or what you no longer require.

1. In the scene _Hierarchy_, we need to set the _Lighting_ object to inactive as it is only meant for lightbaking.
2. Then we make the _Areas_ object active again. Its child objects such as _Seats_ must all be active as well. The _Areas_ object only needs to be inactive during lightbakes.
3. Save your Unity scene by using _CTRL + S_ or other means.
4. In the _Project_ window, select _UserEnvironments_ under _Assets_ and right click it.
5. Click _Export Package..._

![image](https://github.com/assets/50002278/33fc7a92-becc-477c-a1a2-eb46f701b4ef)

6. In the _Exporting package_ window, the _TemplateAssets_ folder should be unticked and all of your assets under _UserEnvironments_ should be ticked. If a folder stays unticked, it means no files are in it. You can proceed.

![image](https://github.com/assets/50002278/53df0516-9f2b-497a-bde0-7bf493572ee3)

7. Click _Export..._ and give the package a file name. _Your environment is now ready for submission!_

![image](https://github.com/assets/50002278/4f21d9a0-4bb6-46fd-b250-b58619f8f8ec)
