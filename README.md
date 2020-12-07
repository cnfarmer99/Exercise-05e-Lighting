

Godot, by default, creates a procedurally-generated skybox for 3D games with a blue, cloudless sky (which reflects on the meshes in the scene. The next step will be to replace this with a custom skybox and allow Godot to illuminate the cabin with indirect lighting.

Right click on the World node and Add Child Node. Select GIProbe. This will provide some constraints to Godot for precomputing the global illumination. Select the GIProbe node, and in the inspector, set the Extents to x=30, y=30, z=30. Immediately over the Viewport, you should see a button labeled Bake GIProbe. Press that now. Now, we would prefer to not have to look at the green cube, so we will hide it in the editor. To the left of the Bake GIProbe button is one labeled View. If you press that, you should see a Gizmos submenu. Select the eye next to GIProbe (so the eye is now closed).

Right click on the World node and Add Child Node. Select WorldEnvironment. Drag it to the top of the Scene panel, so it appears immediately under World. In the Inspector, select Environment and choose New Environment. After the new Environment has been created, select Environment again and Save it as res://Enironment.tres. Then select Environment once more and choose Edit.

Under Background->Mode, select Sky, and under Background->Sky, select New PanoramaSky. Edit the PanoramaSky, and drag the res://Assets/venice_sunset_1k.hd file (acquired [from HDRIHaven](https://hdrihaven.com/hdri/?h=venice_sunset)) into Panorama. The skybox should now appear as a boardwalk at sunset in Venice. Go back to editing the Environment. 

We actually only want the colors of the skybox reflecting on our model, so in Background->Mode, instead select Color+Sky. In Background->Color, type in R=68, G=68, B=68, A=255.

In Ambient Light->Color, type in R=95, G=33, B=217, A=255, set Ambient Light->Energy=0.2, and set Ambient Light->Sky Contribution=0.5

Set ToneMap->Mode to Aces and Ss Reflections->Enabled to On. There is a thorough discussion of ToneMap in the GDQuest video—it adjusts how the exposure and white balance are calculated. SS reflections allows metallic surfaces to be reflective.

We will now experiment with two different types of light sources. Back in the Scene panel, right-click on the World node and Add Child Node. Select DirectionalLight. In the Inspector, change Spatial->Transform->Translation: x=-15, y=10, z=20. Spatial->Rotation Degrees: x=-10, y=-40, z=-25. The arrow should be aligned with where the sun was in the Venice Sunset panorama (indicating where the directional light is coming from). To make it look more like a sunset, change Light->Light->Color: R=235, G=104, B=8, and change Light->Light->Energy=0.6

Right-click on the World node and Add Child Node. Select OmniLight. In the Inspector, change Spatial->Transform->Translation: x=1.711, y=4.333, z=0.268. Change Light->Light->Color: R=197, G=188, B=109. Change OmniLight->Omni->Attenuation=2 (drag down the line)

Finally, we will add a little dynamism to the camera. Right-click on the Pivot node, and Attach Script. Set the path to res://Pivot.gd with an Empty Template.

In the resulting Pivot.gd script, type the following:

```
extends Spatial

export var speed = 15
export var zoom_speed = 1.5
export var zoom_min = 5
export var zoom_max = 15

func _physics_process(delta):
	rotation_degrees.y += delta*speed
	$Camera.translation.z += delta*zoom_speed
	if $Camera.translation.z > zoom_max or $Camera.translation.z < zoom_min:
		zoom_speed *= -1
```

Run the scene. The result should look something like this: 

![Cabin example](https://github.com/BL-MSCH-C220-F20/Exercise-05e-Lighting/blob/master/cabin.gif)

Quit Godot. In GitHub desktop, add a summary message, commit your changes and push them back to GitHub. If you return to and refresh your GitHub repository page, you should now see your updated files with the time when they were changed.

Now edit the README.md file. When you have finished editing, commit your changes, and then turn in the URL of the main repository page (https://github.com/[username]/Exercise-05e-Lighting) on Canvas.

The final state of the file should be as follows (replacing the "Created by" information with your name):





```
# Exercise-05e-Lighting
Exercise for MSCH-C220, 3 November 2020

An exploration of 3D lighting and camera movement in Godot

## Implementation
Built using Godot 3.2.2

## References
[How to light a 3d scene in Godot (3d tutorial)](https://www.youtube.com/watch?v=iamttSmxA2I)

The model is [gr](https://sketchfab.com/3d-models/gr-5df64141235040749103749123e43010) created by luyssport and released under a CC Attribution-NonCommercial-ShareAlike license.

The HDRI Sky Box (Venice Sunset) was downloaded from [HDRIHaven](https://hdrihaven.com/hdri/?h=venice_sunset).

## Future Development
None

## Extra Credit
None

## Created by 
Jason Francis
```
