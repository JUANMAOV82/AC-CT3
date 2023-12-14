# SHADER-TOY PROJECT
In this project, I used two different methods to try different results.

# attempt-1
In the first attempt, I tried to divide the picture into four parts, and used cos and sin functions to try to create the effect of white flash in the picture. Coding steps are distinguished by comments (//1, //2)
  ![4470364f2bd1c0505fd2dbd60780940](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/e80405cf-9b3c-4e4d-967b-353b75932b51)
  ![c56a0c271d5ce9d383ede88dc8b0cb9](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/ea137007-208b-46dd-86f2-7f22ed0b3b7e)
  ![94f937c78002dac81cf3261289552e7](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/c620478c-10c9-4efc-8b76-3b9165587f5d)
  ![ef684c400bfc022243cf16b11e42e20](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/e1434f52-d0cb-4f35-ae55-c8a6120939ef)

#code
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
```

# attempt-2
In my second attempt, I tried dividing the image into multiple parts and using iTime, allowing the prototype halo in the image to shrink inwards. I used the palette function to make the halo shrink and change color at the same time.
  ![9e1dbdbaec203d0422d00aa7f2da003](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/c81bca10-6bff-40a4-bee2-21436a0f1eb0)
  ![148c22682a42db95f20457dde5159ca](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/ecddbdb0-3d92-4fa8-88d5-7a1a23f85b49)
  ![c9d36e3e6f403f8642af016b1219ba6](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/a58f4d36-9659-4014-be43-c4e0758ec738)
  ![94fdb5ec8139d6c740e7b908658eed7](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/7c84e300-eb7e-401d-a183-9b5a03497cc1)
  ![04649ab66214ca35c122f590239ca63](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/794e9bae-1ca3-4382-b921-f97f2fa46535)
Use the sin function to control the number of circles in a circle (the distance between circles)
  ![43ba2b4a2389d5eac9d98ca4be04abb](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/49cf12eb-d2b3-432f-90ae-55f9c3842963)
  ![390362b306a7566640d4ecde577c178](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/9353c807-584b-4710-b37e-e5880c62b91f)
  ![0af6e00938d4c26f781d1746a4fc7e6](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/f98a7149-fea0-416c-82ff-53b15023c476)
  ![8bc6c66d1eaf2a6c780ee27be51aa45](https://github.com/JUANMAOV82/AC-CT3/assets/113642935/c8f0ba91-7b16-4c74-9de6-06fd08f218f7)



