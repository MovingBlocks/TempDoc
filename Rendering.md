##RenderSystem interface
To get the engine to call your custom rendering functions, you need to have a System implementing the [RenderSystem](http://jenkins.terasology.org/job/Terasology/javadoc/index.html?org/terasology/entitySystem/systems/RenderSystem.html) interface. This interface contains a method for each rendering pass of the engine. Add your code to the method that best fits the type of rendering you want to do.
Usually this will be either renderOpaque or renderAlphaBlend, depending on whether or not you want to display transparent objects. The functions will be called automatically, while the system is registered to the engine.

##WorldRenderer
More often then not, you will need more information then just the description of the objects you want to render. It is likely that you also need to have access to the camera position. The [WorldRenderer](http://jenkins.terasology.org/job/Terasology/javadoc/index.html?org/terasology/rendering/world/WorldRenderer.html) can provide this amongst other useful stuff, such as block lighting information. To get access to the WorldRenderer, add a public WorldRenderer attribute to your system, with a @In annotation. The engine will assign an instance of WorldRenderer to this automatically.

    @RegisterSystem(RegisterMode.CLIENT)
    class MySystem implements WorldRenderer {
      @In
      public WorldRenderer worldRenderer;
      
      ... other code ...
 
      public void renderOpaque() {
        Camera camera = worldRenderer.getActiveCamera();
        ... rendering code ...
      }
    }

## OpenGL and GLSL
Terasology uses [OpenGL 2.1](https://www.opengl.org/sdk/docs/man2/) for all it's rendering. Shaders are written in the corresponding [GLSL version 1.2](https://www.opengl.org/registry/doc/GLSLangSpec.Full.1.20.8.pdf).

## Related Links
* [OpenGL 2.1 specification](https://www.opengl.org/sdk/docs/man2/)
* [GLSL 1.2 specification](https://www.opengl.org/registry/doc/GLSLangSpec.Full.1.20.8.pdf)
* [LWJGL OpenGL package documentation](http://javadoc.lwjgl.org/index.html?org/lwjgl/opengl/package-summary.html)