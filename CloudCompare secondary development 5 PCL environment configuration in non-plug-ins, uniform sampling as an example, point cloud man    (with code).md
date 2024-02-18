#  I. Overview 

   During the secondary development of CloudCompare, you can directly add your own algorithms to the core functions of CloudCompare, which is much more convenient than plug-in algorithm integration. Therefore, this paper mainly records the configuration PCL of CloudCompare non-plug-in secondary development, and gives the specific development process. 

#  II. CMakeLists.txt 

 1. Modify the CMakeLists.txt in the E:\ CloudCompare\ CloudCompare-2.11.3\ CC directory. (Since CloudCompare 2.12.4 does not support the reading of .pcd files in the Chinese path, and has not found a solution to the problem for the time being, so fall back to CloudCompare 2.11.2 version) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574143267
  ```  
 ![avatar]( b9d3e93e3fbf44aea7aa7ff35356e8f8.png) 

 2. Modify the CMakeLists.txt file in the same directory as the CC folder  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574143267
  ```  
#  III. Source code compilation 

 ![avatar]( 71656307fb1b43d3b0a0c4e3ea765536.png) 

   Select COMPILE_CC_CORE_LIB_WITH_PCL compile in the COMPILE option of Cmake. After the compilation is successful, you can use PCL-related algorithms in the core functions of CloudCompare. You only need to add code to the project later, and you don't have to compile every time.  

#  IV. Code examples 

>  Give an example of adding uniform sampling to CLoudCompare 

 ![avatar]( f6af0118fc5c431fb1769f272d33fc79.png) 

 1. In the mainwindow.h file, add the declaration of the new algorithm in the public function.  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574143267
  ```  
 2. Add a uniformly sampled header file to the mainwindow.cpp file. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574143267
  ```  
 3. Add the implementation code of uniform sampling in the mainwindow.cpp file. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574143267
  ```  
 ![avatar]( d2dc699e249747529601a7b77dd7b10e.png) 

 4. The button of the design algorithm on the display interface in mainWindow.ui. The example is as follows, just design according to your own preferences. After the design is completed, you need to compile. 5. Add the signal connection slot function to the mainwindow.cpp file.  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574143267
  ```  
 So far, the new custom algorithm in CloudCompare is complete!!!! 

#  V. Display of results 

 ![avatar]( afe76cc594ab427089f552ed1d0f52de.gif) 

