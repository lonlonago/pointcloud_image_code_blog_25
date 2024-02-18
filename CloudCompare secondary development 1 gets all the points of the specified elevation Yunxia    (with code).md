#  First, source code compilation 

 [1] WIN10系统下VS2019编译CloudCompare2.12.4 

#  Production process 

 1. Find the plug-in example in the source code 

 ![avatar]( 03fbb88d2fad4a268f5d5135f3304090.png) 

>  Three main plug-ins are supported: GL plug-in for visual rendering, IO plug-in for data input and output, and ordinary plug-in for data processing. CloudCompare - 2.11.3 source code is perfectly compatible with PCL1.11.1. 

 ![avatar]( 71c1a76657794af19c0df52193e27930.png) 

 2. Copy the ordinary plugin. In order not to destroy the original example in CloudCompare, copy the ExamplePlugin and rename it to: ElevationPointsPlugin. Then modify the configuration file, CmakeLists.txt, .h and .cpp files in the folder.  

 ![avatar]( d259d5ee94184d248be417d35cae922a.png) 

 The specific modifications are as follows: 1. Images  

 2、CmakeLists.txt 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574113443
  ```  
 3、info.json 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574113443
  ```  
 ![avatar]( a6dba669e42e4b4b82b978d6724ebcff.png) 

 4, ElevationPointsPlugin and ElevationPointsPlugin first do not modify, to be compiled after modification in the VS compiler. 3. Modify the example directory CMakeLists.txt  

 Add your own plugin source directory in\ plugins\ example\ CMakeLists.txt 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574113443
  ```  
 ![avatar]( 758a67141ee4473497666bb9db0b1600.png) 

 4. After configuring and modifying, use the Cmake tool to generate the VS project and select the plug-in.  

 ![avatar]( dcfea180ce1a426e974efeb51bc713bf.png) 

 5. Select the plug-in and click the Configure button again. As shown in the figure below, it means that Configure is successful. Click Generate, and finally open the project.  

 6. Add the following code to the ElevationPointsPlugin file: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574113443
  ```  
 7. Add the following code to the ElevationPointsPlugin file: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574113443
  ```  
 ![avatar]( e6ea0991c0dc4b1aa2699025cba35cae.png) 

 8, ElevationPointsPlugin modify icons and .json files in .qrc  

#  III. Display of results 

 ![avatar]( a629ce1002844f56a399e98bf66f26e8.gif) 

