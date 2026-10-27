---
banner: https://user-images.githubusercontent.com/1103897/34840206-e7adbb50-f6c9-11e7-84bc-08e4b7d9b661.png
---
The player is one of the most important parts in any game. It is the only way you are allowed to interact with the world the game shows you beyond simply watching it go by like a movie or cutscene.
- **Nodes** can be things like images, sounds, animations, etc...
- **Scenes** organise nodes by being a folder for the node. You can place scenes inside of other scenes.
	- For instance you may have a level scene and then a player scene

This document will note how to create a basic player node with full functionality and a projectile. These will work however, they are examples to teach GD Script, the coding language of Godot. [This](https://www.youtube.com/watch?v=q7wlSvt0JIc&list=PL4cUxeGkcC9iHCXBpxbdsOByZ55Ez4bgF) is the specific video we will be following.

![[Screenshot 2026-10-26 200414.png|wrap-right|gap-24|211]]The first things we want to look at is the ==Scene manager==. It controls everything in all of our scenes whether it be nodes like images or scenes containing those same nodes.

In this screenshots we have ==2D Scene and 3D Scene==. These would each create a unique dimensional environment where in which they would house a Node. Lets stick with 2D for now. This ==Node2D== will be placed at the universal middle of the scene. This will be 0, 0. A vertices with no physics.

What we want to do with this object is we want to add something we can see to it. We want to add some content that we can move, animate, control, etc...

Select the Node2D and do ==CTRL+A==. This will add a child node to the node you have selected. Since there are so many nodes we want to use the ==Search Bar== to find exactly what we want. Enter "==Sprite2D==". Change the name to "Player"

Now you will notice when you select Sprite2D we have a texture property. Add any you wish to visualise the Node. By default we have the icon.svg (a scalable vector image), drag that into the Sprite2D texture property.

![[Tutorial_Icon.png|wrap-left|207]] Your inspector of the player should look something like this now. But while this has given us some 