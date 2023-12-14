# SHADER-TOY PROJECT
In this project, I used two different methods to try different results.

# attempt-1
In the first attempt, I tried to divide the picture into four parts, and used cos and sin functions to try to create the effect of white flash in the picture.
  ![4470364f2bd1c0505fd2dbd60780940](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/e80405cf-9b3c-4e4d-967b-353b75932b51)
  ![c56a0c271d5ce9d383ede88dc8b0cb9](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/ea137007-208b-46dd-86f2-7f22ed0b3b7e)
  ![94f937c78002dac81cf3261289552e7](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/c620478c-10c9-4efc-8b76-3b9165587f5d)
  ![ef684c400bfc022243cf16b11e42e20](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/e1434f52-d0cb-4f35-ae55-c8a6120939ef)

#code
Steps are distinguished by comments (//1, //2)
  ```GLSL
  void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    // 1-2 Normalized pixel coordinates (from 0 to 1)
    vec2 normalizedCoord = fragCoord/iResolution.xy * 2.0 - 1.0;
    for (float i =0.0; i < 32.0; i += 1.0) 
    {
    
    //1
    normalizedCoord = abs(normalizedCoord);
    
    //2
    normalizedCoord -= 0.5;
    normalizedCoord *= 1.1;
    normalizedCoord *=mat2(
        cos(0.2), -sin(0.2),sin(0.2), cos(0.2)
        );
    }
    
    // Time varying pixel color
    //vec3 col = 0.5 + 0.5*cos(iTime+uv.xyx+vec3(0,2,4));

    //1-2 Output to screen
    fragColor = vec4(vec3(length(normalizedCoord)),1.0);
    
}

