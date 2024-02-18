#  First, source code download 

 [1]CloudCompare源码：https://github.com/CloudCompare/CloudCompare [2]CCCoreLib：https://github.com/CloudCompare/CCCoreLib 

#  Source code compilation 

##  1、CCCoreLib 

   CloudCompare 2.12.4 separates CCCorLib, so you need to copy and paste the contents of the CCCorLib folder into CloudCompare. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574275194
  ```  
 ![avatar]( 656445cc54624669809ee490b38d704d.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574275194
  ```  
 ![avatar]( 0b5b515871c547ea94f05b0815571d68.png) 

##  2. Cmake compilation 

 ![avatar]( c25773a6a31c461eb53c86eef27c4ed5.png) 

   2.1 Under the same path as the CloudCompare source code, create a new folder build (the folder name is random, try not to use Chinese) to place the compiled source code.  

 ![avatar]( 7cfa4b668a15484aa4535c2e95fb402b.png) 

   2.2 Set the source code path, compilation path, VS version, etc. in Cmake. As shown in the figure below: Click Finish - > then click "Configure" 

##  3. Set relevant options 

 ![avatar]( ff037172905d444192e4f3c700ac2b2b.png) 

 3.1 Create a new install folder in the build folder, and set the path in Cmake 3.2 OPTION, where GDAL is the library for reading the las point cloud, which is required. 3.3 OpenMP does not need to be set, the default is fine. 3.4 PLUGIN is compiled for plug-ins, the following are commonly used plug-ins. If you want to compile PCL plug-ins, you need to give the bin path in the environment variables of the computer (PCL1.11.1 is valid) 3.5 Generate the compilation project  

 ![avatar]( 3df33be3430044df9153538a477aecf5.png) 

 3.5 Compiling  

>  After success, set CloudCompare as the startup item, and at the path\ qCC\ Release, CloudCompare.exe. Path\ libs\ qCC_io\ Release QCC_IO_LIB path\ libs\ qCC_db\ Release QCC_DB_LIB path\ CC\ Release CC_CORE_LIB 

   Copy the above three dll files to the path\ qCC\ Release; if it prompts that the.dll is missing, copy it to the path\ qCC\ Release; double-click CloudCompare.exe to load a partial format point cloud to achieve basic functions. 

#  III. Error handling 

 ![avatar]( 17c8e56f91fe4733998b406d2f4750de.png) 

 ![avatar]( 9280660fdeae4579a6898b207cd22706.png) 

   The following error may occur: If this type of error occurs, simply delete the content in the CloudCompare property page - > Generate Events - > Command Line.  

#  IV. Use of plug-ins 

 ![avatar]( 0858140d2b9f45b7b5f0861bf9a0e45a.png) 

 Create a new plugins folder under the same directory folder as CloudCompare.exe  

 ![avatar]( ba23b6d731914e29b729b1cbc9566a49.png) 

 ![avatar]( 80937fe16ba64c638a0ddff30b7a6e69.png) 

 ![avatar]( 72491421b48e462e9fc1b28edeff3a19.png) 

 Open the pugins folder under the build folder, find the compiled plug-in, such as the PCL plug-in, copy and paste the .dll file into the pugins folder under the build, and then read the .pcd format point cloud with the plug-in  

>  This version of CloudCompare does not support the reading of point clouds in Chinese path pcd format, and there is no 2.11.2 easy to use!!!!. 

