

The secret of Blockmania's terrain.

---+ What is Perlin noise?

Imagine Perlin noise as a function that always provides the same value for a given pair of real numbers (x,y). But in comparison to the well known grainy noise, the values change very smoothly with increasing or decreasing x- and y-values. When one or both of the coordinates reaches an integer value, the noise function returns exactly zero. Both properties can be explained by the way Perlin noise is calculated. The following explanation is based on 2D Perlin noise, but can be easily transferred to 3D, 4D or 42D noise.
   * For any given pair of real number (x,y) four grid coordinates are determined. For (0.04, 0.01) this would be (0,0), (0,1), (1,0) and (1,1). For each of those grid coordinates a pseudo-random gradient vector is determined. This has to be the same vector for each unique grid coordinate point every time
   * Using the gradient vector and a sigmoid function, a smooth interpolated value for the given real numbers (x,y) is generated
   * The function is constructed to return zero at the grid vertices. This explains why any integer value forces the noise function to return zero
So using a noise function with an increment of one would return zero all the time (imagine calling noise(x,y) with x=1, x=2; x=3, x=4 and so on). Reducing the frequency e.g. to 1/100 would result in the well known basic shape of the noise function (imagine calling noise(x,y) with x=1/100, x=2/100, 3/100 and so on).
---+ Terrain generation basics

Blockmania uses a hybrid approach combining 2D and 3D noise functions to generate the terrain. On a very basic level, the combination of those noise functions returns a so called density value for any position in R^3. This final value is used to determine which block positions in a chunk get filled and which get treated as air.

But why a combination of 2D and 3D noise values? 2D noise functions can be used to generate a vast amount of different heightmaps. Just imagine a 2D grayscale image, where each color value represents a height. But a single noise function looks very boring (to say the least). But the combination of the same noise function at different frequencies (the change of the frequency can be compared to the usage of a simple Sinus function for example) with decreasing weight creates a multifractal noise function. Each of these layers is called an octave.

A 3D Perlin noise functions can be used the same way, but it has some other useful properties. At first glance the volumes generated by those functions look like some strange, wobbly thingies. But they provide a very important property in comparison to 3D noise: they allow the creation of concave structures and hence the generation of overhangs and caves.

Both approaches can be visualized using different techniques. Heightmaps are often visualized by manipulating the vertices of a plane mesh using the pre-calculated height values. 3D noise functions on the other hand can be used to fill volumes. So a volume (picture a 3D array) is filled with a noise value at each coordinate (x,y,z). In the final visualization step each value is analyzed and interpreted differently. A high value might be interpreted as solid mass and low values as air. This is how chunks in Blockmania are generated and filled. There are many complex algorithms available to generate meshes from volumes (a project of mine uses the marching cubes algorithm for example), but in Blockmania the density just determines if a block is generated or not.
---+ Generating the basic heightmap

The basic heightmap is generated by combining eight octaves of Perlin noise using fractional Brownian motion.
---+ Generating the mountains

Mountains are calculated in a second step by manually combining multiple octaves of Perlin noise at different frequencies. Additionally the input coordinates (x,y) are slightly offset using a additional Perlin noise function (this process is called perturbation).
---+ Calculating the final density value

Now we've got two separate noise values based on 2D and 3D Perlin noise. But how are both combined to generate the final density value? This is also the part where biomes come into play. The basic height level is not influenced by biomes, but the mountain density value. When generating a plain biome the amplitude of the mountain density function is reduced, whereas in a mountain biome the density value gets amplified. To keep the explanation simple, biomes a ignored in the following part.

Lets take a look at a pseudo version of the actual calculation
<verbatim>
calcDensity(x,y,z, ...) {
  return -y + (heightmapValue(x,z) * 64.0 + 32.0) + densityValue(x,y,z) * 128.0;
}</verbatim>

and how a chunk is filled with blocks:
<verbatim>
generateChunk(...) {
  foreach (int x,y,z) {
    if (calcDensity(x,y,z) >= 0.0 && calcDensity(x,y,z) < 64.0) {
      generateOuterLayer(...);
    } else {
      generateInnerLayer(...);}
    }
}
</verbatim>

Using the density value three different layers are generated: the air, outer and inner layer. This approach can be easily extended so support a vast amount of additional layers.
---+ Caves

Caves are generated using another combination of 3D Perlin noise functions. If this function returns a value in specified range, no block is set. It's as simple as that.
---+ Optimizing the generation using (tri)linear interpolation

Filling a volume in R^3 using solely the expensive Perlin noise functions can easily mess up the generation speed of chunks. Simply put, a chunk in Blockmania is filled with a reduced amount of actual noise values. All missing noise values are calculated subsequently using trilinear interpolation. Given the blocky nature of the world, this step is merely visible and adds a bit character to the world (more blocky shapes instead of surreal looking round shapes), but the calculation speedup is immense.