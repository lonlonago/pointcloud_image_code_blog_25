#  I. Overview 

   When making the CloudCompare plug-in, PCL is required. The CloudCompare official website recommends that users use Cmake to configure the three-party library. Therefore, here we mainly record the use of Cmake to configure PCL in CloudCompare, and give the specific production process. 

#  II. CMakeLists.txt 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574164534
  ```  
#  Plug-in production 

 ![avatar]( f8faaccb8aac422099daff8693e04209.png) 

 1. Copy a copy of the ExamplePlugin in the source code and modify it to the plug-in name you want, such as GridMinimumPlugin. This is mainly based on PCL to realize grid lowest point filtering. For the specific principle of this algorithm, see: PCL GridMinimum gets the grid lowest point. Self-modify the configuration files, CmakeLists.txt, .h and .cpp files in the folder. 

 ![avatar]( 0024472ffec948fbbced1f6d1c6190c0.png) 

 2. Images folder - modify the picture to the icon you want 3. CMakeLists folder - add the PCL configuration environment, you need to pay attention to the following points: Attached: Complete Cmake configuration 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574164534
  ```  
 ![avatar]( 94fabd93c7a847a2a19338fd75fa6cbe.png) 

 4. H, cpp and qrc are all modified to plug-in names - the name does not matter, mainly for the unity of format 5. GridMinimumPlugin.cpp and GridMinimumPlugin.h are not modified first, and are modified in the VS compiler after compilation. For specific modifications, see: Plug-in code 6. Modify CMakeLists.txt in the example directory and add your own plug-in source code directory in\ plugins\ example\ CMakeLists.txt 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574164534
  ```  
 ![avatar]( 4ffc1d7e6e5e456194d61d68874136e5.png) 

 7. After configuring and modifying, use the Cmake tool to generate the VS project and select the plugin. 8. Modify the .json file. The core content is shown in the following figure:  

 Attached: Complete .json file 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574164534
  ```  
 ![avatar]( 322f002e3f8b477bb6a078516a587fd7.png) 

 9. Modify the icon and .json file in GridMinimumPlugin.qrc. 10. Compile GridMinimum. After compilation, copy and paste GridMinimum.dll into the plugins folder under the same path as CloudCompare.exe to complete the plug-in production. If you don't want to manually copy the .dll file every time, just configure the generation event path in the property table: specifically add content (write your own path) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574164534
  ```  
 auto copy 

 ![avatar]( 47f9f76790e5479c9afb47a75d834f04.png) 

#  IV. Plug-in code 

 GridMinimumPlugin.h 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574164534
  ```  
 GridMinimumPlugin.cpp 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574164534
  ```  
#  V. Display of results 

 ![avatar]( 81f3d94755c54a5bb10c2c137f896f8d.gif) 

