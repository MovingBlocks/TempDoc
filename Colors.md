# Player colors

Since commit 1da32259a225371496251e6ab804f4d0e6e8e2b2, Terasology uses a sample set of colors based the CIELch color space to define player colors. 

Subsequent colors should be distinguishable by 50% of the population. The number of colors is restricted to those that have almost identical chroma (think of it as color intensity) and luminosity (similar to brightness).

This has two advantages: 
* It's easier to choose: the player just needs to pick the hue of the color, the engine makes sure that it is recognizable on de-saturated (preferably dark) background.
* Bright/dark colors - in particular black and white - are reserved for other uses. This contrast allows for highlighting (system messages, admin users, etc).

As of 1da32259a225371496251e6ab804f4d0e6e8e2b2, there are two sets of colors. The first one preserves "perceived brightness" better while the second has a higher "colorfulness". The second one is currently in use as I thought that the number of distinguishable colors is more important for the use case.

![image](https://cloud.githubusercontent.com/assets/1820007/6076294/f0e77dfc-ade1-11e4-8a55-520830c94110.png)
