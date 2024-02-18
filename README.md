#  First, the algorithm flow 

   This is a method I saw in the paper. It doesn't seem difficult to implement, so I tried to implement the following. 

>  The main process is: find the corresponding point pair of FPFH feature matching within a certain distance threshold range - > SVD calculation transformation matrix. Mainly used: pcl :: registration :: CorrespondenceEstimation class in PCL 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574036699
  ```  
#  III. Display of results 

 ![avatar]( 20201107164856123.png) 



--------------------------------------------------------------------------------

#  Point cloud compression 

   A point cloud consists of large datasets that describe three-dimensional points in space by distance, color, normals, and other additional information. In addition, point clouds can be created at very high rates, and therefore require considerable storage resources. Once a point cloud needs to be stored or transmitted over a rate-limited communication channel, it becomes very useful to provide a compression method for this data. PCL provides a point cloud compression function, which allows coding to compress all types of point clouds, including "disordered" point clouds, which have structural features such as no reference point and changing point size, resolution, distribution density, and point order. Furthermore, the underlying octree data structure allows point cloud data to be efficiently merged from several input sources. 

#  Second, parameter settings 

 1. Parameter setting instructions 

    The configuration files pre-define parameters for point cloud compression, which are optimized for point clouds obtained through the OpenNI fetcher. 

>  Note: It is not necessary for the decompressor to enter these parameters, as it can detect and adapt to the parameters used during compression. 

 2. Comes with parameter settings 

 Some compressed files that can be used: 

 3. Custom parameter settings 

 Select MANUAL_CONFIGURATION attribute in the OctreePointCloudCompression constructor to manually set all the parameters of the compression algorithm. There are six parameters entered, as follows: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574137414
  ```  
 4. Custom parameter description 

   PointResolution refers to the resolution of the point, which determines the degree to which the coordinates of the point can be accurately encoded, but this variable will only take effect when performing detail coding; octreeResolution refers to the smallest block when dividing the octree, that is, the side length of voxel; when the Boolean variable doVoxelGridDownSampling true, the point cloud file is downsampled, and the coordinates of the center point of the voxel are replaced by the coordinates of the point in the entire voxel, and the color is represented by the average color of all points in the voxel. At this time, pointResolution will not take effect; if the doVoxelGridDownSampling is false, the detail coding is carried out, that is, the specific coordinates and colors in a voxel are encoded. The implementation is to calculate the offset of each point in the voxel to the lower left corner of the voxel, and to obtain the integer coordinates by dividing pointResolution The color needs to encode the residual of the color of each point in the voxel relative to the average value. ColorResolution is used to represent the reserved significant digits of the RGB of the color. The iFrameRate is used to determine the frequency of I-frame encoding. If this value is 30, the I-frame encoding is performed every 30 frames, and the intermediate frame is encoded by P. doColorEncoding determines whether to perform color encoding. If the value is false, the color will not be encoded. If it is true but the input point cloud file has no color information, it will be given a default value when decoding. 5. Encoding Process 

 ![avatar]( 20210220080726921.png) 

    Before this flowchart, it is also necessary to determine whether the current frame is an I frame or a P frame. If it is an I frame, it is encoded normally according to this flowchart, and if it is a P frame, when encoding the octree placeholder code, the encoded is the difference after the exclusive OR of the previous frame. The structure coding of the octree is to encode the placeholder code of the voxel after the octree division. If the doVoxelGridDownSampling is true, the detail coding part is skipped. When decoding, the decoding end only needs to restore the octree structure according to the structure information of the octree, and its voxel center point is represented. The detail coding is the details in the encoded voxel. If the size of the voxels is large when the octree is divided, for example, in the ply file we input, the units of the points in the point cloud are millimeters, that is, each point corresponds to a cube with a side length of 1mm. If we set its value to 5mm when setting octreeResolution, the cube divided into a side length of 5mm when the octree is divided will stop, and there will be multiple points in a voxel. If we do not perform detail encoding, that is, when doVoxelGridDownSampling is true, only one point will be restored in the center of a voxel during decoding, and its properties will be the average of several points, which will lead to the loss of points. If we perform detail encoding, it will encode the details of a point in a voxel, that is, the specific position and properties of the encoded point. As shown in the figure:  

   First calculate the lower left corner coordinates of each voxel, then calculate the offset from each point to the lower left corner, and then divide it by pointResolution to obtain the final encoded information of integers diffX, diffY, and diffZ. Attribute coding is to calculate the mean of these points first, and then calculate the color offset of each point relative to the mean. The number of digits of each R, G, and B is determined by colorResolution. 

#  III. Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574137414
  ```  
#  IV. Display of results 

 ![avatar]( 2021022008231761.png) 

#  V. Reference links 

 [1] Point Cloud Compression [2] pcl::io::OctreePointCloudCompression [3] PCL学习八叉树 [4] （十二）OcTree教程四–OcTree在PCL中的应用-点云压缩 [5] PCL点云压缩总结 



--------------------------------------------------------------------------------

 + cloudA cloudB change area

#  First, the principle of the algorithm 

   Octree can be used to detect spatial variation between multiple disordered point clouds, which may differ in size, resolution, density, and point order. By recursively comparing the tree structures of octree, the spatial variation represented by the difference between the voxel compositions produced by octree can be identified. 

##  1. Core code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574195807
  ```  
>  PCL octree "double buffering" technology allows us to efficiently handle multiple point clouds over time. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574195807
  ```  
>  Find the difference between two point clouds in octree structure with minimum voxel resolution. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574195807
  ```  
>  The first time to find octree.getPointIndicesFromNewVoxels (newPointIdxVector); is in cloudB, not cloudA, the second time to find octree.getPointIndicesFromNewVoxels (newPointIdxVector); is to find in cloudA, not cloudB, is not the same, this operation does not meet the switching law; 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574195807
  ```  
>  The smaller the resolution, the tighter the constraint, that is, if only the number of points is different, that is, there is a change in the strict sense, then the resolution can be set to very small. 

##  2. Related references 

>  PCL :: octree :: OctreePointCloudChangeDetector class implements spatial change detection 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574195807
  ```  
#  III. Display of results 

##  cloudA 

 ![avatar]( ddb5578648504e08b93382fc13478d2c.png) 

##  cloudB 

 ![avatar]( 13205f2eacaa49e9b0a39c90334cb05d.png) 

##  change area 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574195807
  ```  
 ![avatar]( 665a9115b19a42a9851f1195fed9d62a.png) 



--------------------------------------------------------------------------------

1. Quaternion definition 1. Quaternion type 2. Quaternion assignment 3. Common functions 4. Quaternion conversion 5. Complete code 6. Results display 7. Reference link

##  First, the definition of quaternions 

>  A PDF about the explanation of quaternions An excellent blog about quaternions A quaternion derivation summarized by myself 

##  First, the quaternion type 

 Common quaternion formats include Quaternionf (float) and Quaterniond (double), and Scalar in the template class determines the data type. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
>  Note: The order of quaternions in Eigen is [w, x, y, z], with the real number w at the beginning; but in fact its internal storage order is [x y z w], and the output coefficients are also output in the internal storage order [x y z w]. 

##  Quaternion assignment 

 The official introduction has seven construction methods, but the commonly used ones are generally as follows: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
##  III. Common functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
>  Note: Both of the above outputs are output as vector vectors in Eigen 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
>  Note: Only unit quaternions represent rotation matrices, so you need to unify the quaternions first. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
>  Note: In general, inverse is not used. When representing rotation (the norm is 1), conjugate can represent the opposite rotation. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
##  Quaternion conversion 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
##  V. Complete Code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  
##  VI. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574166969
  ```  


--------------------------------------------------------------------------------

 + 1. Introduction to the concept of FitnessScore 2. References

 + 2. In PCL getFitnessScore () 

 + III. Improved MSE calculation 

#  FitnessScore 

##  1. Introduction to the concept 

 ![avatar]( 20210208114606755.png) 

   Due to the large difference in the spatial position of the point cloud of the wrong registration effect, the traditional root mean square error RMSE is used as the registration accuracy evaluation. Limiting the threshold of the closest point distance will lead to the rejection of the registration error points, resulting in a smaller RMSE. The RMSE value obtained by the rejection of the error points is small, but the registration effect is not ideal. This result can be avoided by using the sum of squares of the closest point distance corresponding to the point cloud after registration as the registration effect evaluation. The calculation source code of getFitnessScore () in PCL: 

   ![avatar]( 20200917200805816.png) 

   The units of the calculation result are the same as those of the input data. For example, the units of the input data are: meters, and the units of the output FitnessScore are: square meters 

    From the source code, it can be seen that the final result obtained by getFitnessScore () is the average of the sum of the squares of the distances between all corresponding points after the iteration, that is, MSE; the input in getFitnessScore () is the distance threshold between the corresponding points, that is, the MSE is calculated within a certain distance range. 

#  III. Improved MSE calculation 

   Although each registration can obtain a matching fitness score (ie mse), if you want to see the mse of the initial situation; that is, the MSE of the initial position of the source cloud and the target point cloud before icp.align (* cloud), an error will be reported. The reason is that some parameters in the source code require icp.align (* cloud) to provide. The mse of the initial position can be calculated by the following method 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574128796
  ```  
>  Note: This is the simplest point-to-point distance MSE calculation method. If different objective functions are used to measure the distance between the closest points, such as point-to-line, point-to-surface, etc., the distance measurement indicators obtained are different. Therefore, the above program cannot be used to calculate MSE. 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

#  I. Overview 

   For the algorithm principle of fast uniform sampling, see: PCL fast uniform sampling. Do not rely on any third-party library to directly use CLoudCompare implementation. 

#  Second, code integration 

 1. Add to the mainwindow.h file public: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574110046
  ```  
 2, mainwindow.cpp file void Main Window :: connect Actions () function to add: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574110046
  ```  
 Note: actionFastUniformSample the name of the new button on the interface, and set the button and name according to your own needs! 3. Add the implementation code in the mainwindow.cpp file: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574110046
  ```  
#  III. Display of results 

 ![avatar]( 06146644a5174c77ba8f4fa6b5e461fc.gif) 



--------------------------------------------------------------------------------

#  I. Overview 

   Without relying on any third-party point cloud related libraries, use ClopudCompare to calculate the point cloud centroid. 

#  Second, code integration 

 1. Add to the mainwindow.h file public: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574130574
  ```  
 2, mainwindow.cpp file void Main Window :: connect Actions () function to add: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574130574
  ```  
 Note: actioncomputeCenter is the name of the new button on the interface, and you can set the button and name according to your own needs! 3. Add the implementation code in the mainwindow.cpp file: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574130574
  ```  
#  III. Display of results 

 ![avatar]( ff7728051bce4838a8c35df4b4375546.gif) 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

#  I. Overview 

   See the algorithm principle of pass-through filtering: PCL pass-through filter. Based on PCL, pass-through filtering is integrated into CloudCompare software. 

#  Second, code integration 

 1. Add to the mainwindow.h file public: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574137085
  ```  
 2, mainwindow.cpp file void Main Window :: connect Actions () function to add: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574137085
  ```  
 Note: actionpassThrough is the name of the new button on the interface, and you can set the button and name according to your own needs! 3. Add the implementation code in the mainwindow.cpp file: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574137085
  ```  
#  III. Display of results 

 ![avatar]( 51e6528d5c3545faabdc77d81d1341de.gif) 



--------------------------------------------------------------------------------

#  I. Overview 

   Using CloudCompare and PCL joint programming to achieve the acquisition of the overlapping area of the two point clouds. For the specific calculation principle, see: PCL extracts the overlapping part of the two point clouds and saves it. 

#  Second, code integration 

 1. Add to the mainwindow.h file public: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574171010
  ```  
 2, mainwindow.cpp file void Main Window :: connect Actions () function to add: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574171010
  ```  
 Note: actionOverLap is the name of the new button on the interface, and you can set the button and name according to your own needs! 3. Add the implementation code in the mainwindow.cpp file: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574171010
  ```  
#  III. Display of results 

 ![avatar]( 27cdf2fa8caf48dc98f3884db6fa951b.gif) 



--------------------------------------------------------------------------------

 + Zero, save point cloud 

 + 1. Time calculation 

 + 2. Known to need to save the index of the point, copy the point from the origin cloud to the new point cloud 

 + 3. Delete invalid points 

 PCL :: Point Cloud :: Ptr and PCL :: Point Cloud 

 + 5. Compute point cloud center point 

 Convert Vector Indexes to PCL :: Indices Ptr 

 + 7. Get the point cloud format 

 + 8. Point clouds are saved in binary format 

 + 9. Generate a null point cloud 

 Delete and add points from the point cloud 

 + Eleven. Determine whether the point cloud is loaded successfully 

 + 12. Calculate the angle included in the vector 

 + 13. Count the number of occurrences of each element 

 + 14. Calculate the number located in the middle 

 + 15, keep n decimal places 

 + 16. Mode and its multiplicity 

 + 17. Find the y power of x 

 + 18. Assign the content of one vector to another vector 

#  Zero. Save the point cloud 

 1. Save in ASCII format 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
 2. Save in Binary format 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
 3. Save in compressed format 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  First, time calculation 

 There are many functions in PCL to calculate the running time of the program. 1. To use the time calculation of the console, you must first include the header file #include < pcl/console/time.h >. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
 2. Use the timer to calculate the time, you need to include the header file #include < ctime > 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Second, if you know the index of the points that need to be saved, copy the points from the origin cloud to the new point cloud 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  III. Delete invalid points 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  PCL :: Point Cloud :: Ptr and PCL :: Point Cloud 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Computing point cloud center point 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
 Reference link: PCL common tips 

#  Converting Vector Indexes to PCL :: Indices Ptr 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
 or 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
 Reference link: Point cloud extraction using PCL index 

#  Acquire the point cloud format 

 How to get the format of the point cloud in the pcd file, such as pcl :: Point XYZ or pcl :: Point XYZ RGB and other types? 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
 Reference link: Point cloud library PCL learning - common operations of point cloud 

#  Eight, point clouds are saved in binary format 

 Binary format PCD files take up less memory than ASCII files 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Generating a null point cloud 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Delete and add points from the point cloud 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Eleven. Determine whether the point cloud is loaded successfully 

   In point cloud registration, it is usually necessary to determine whether the source point cloud and the target point cloud are loaded successfully (of course, you don't want to judge or not, just be happy if you like to judge or not.) At present, the code version commonly circulated on the Internet is as follows: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
   Another way is to use the empty () function that comes with PCL to judge, the code is as follows: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Calculate the angle included in the vector 

 Refer to the link to find the angle between two vectors in space 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Thirteen, calculate the number of occurrences of each element 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Fourteen, calculate the number located in the middle 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Fifteen, keep n decimal places 

 Reference link: C/C++ keep two decimal places (summary of some usages of setprecision (n)) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Mode and its multiplicity 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  Seventeen, find the y power of x 

 In C ++, there is no operator to represent power. To find the Y power of X, you usually call the pow function in the mathematical function library, pow (X, Y). 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  
#  18. Assign the content of one vector to another vector 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574125906
  ```  


--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

 + 1. Original point cloud 2. Projected point cloud 3. Concave polygon boundary 4. Concave polygon contour

#  First, the code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574169505
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574169505
  ```  
##  1. Primitive point cloud 

 ![avatar]( df56f489d1fa4eeea70a29a7440d046f.png) 

##  2. Projection point cloud 

 ![avatar]( 72cd627813a0407ab1a7ec57d942f0f4.png) 

##  3. Concave polygon boundary 

 ![avatar]( be1d76dd6e574e4bad09b33275325cd4.png) 

##  4. Concave polygon contour 

 ![avatar]( 15c849a3a876466b9638244695bd6c72.png) 



--------------------------------------------------------------------------------

 + 1. Overview 

 + 2. VTK to PCD 

 + 3. PCD to VTK 

#  I. Overview 

 ![avatar]( 58d395d1c652463d868ce7599a503196.jpeg) 

   The polygon dataset vtkPolyData consists of vertices, polyvertices, lines, polylines, and triangular zones. Vertices, lines, and polygons form the smallest set of basic elements used to express geometric shapes in 0, 1, and 2 dimensions. .vtk to .pcd is to extract the vertices and polyvertices in vtkPolyData and save them as point clouds.  

#  VTK to PCD 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123395
  ```  
#  PCD to VTK 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123395
  ```  
#  IV. Experimental data 

 Vtk to pcd test data 



--------------------------------------------------------------------------------

#  First, the code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574119991
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574119991
  ```  
##  1. Primitive point cloud 

 ![avatar]( df56f489d1fa4eeea70a29a7440d046f.png) 

##  2. Projection point cloud 

 ![avatar]( 72cd627813a0407ab1a7ec57d942f0f4.png) 

##  3. Convex polygon boundary 

 ![avatar]( c620b5e9914f471c82e3395b9e810780.png) 

##  4. Convex polygon contour 

 ![avatar]( 47877f602d6249d4b92145e3041e8bcc.png) 



--------------------------------------------------------------------------------

##  Function prototype 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574270732
  ```  
 Main parameters: 

   Compute the 3x3 covariance matrix for a given set of points. Note: The covariance matrix is not normalized with the number of points. For the normalized covariance, please refer to: PCL calculates the normalized covariance matrix and three-dimensional centroid of a point cloud. The calculation formula is:  

##  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574270732
  ```  
##  III. Display of results 

 ![avatar]( 2021031720485862.png) 



--------------------------------------------------------------------------------

#   code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957412168
  ```  
#  III. Display of results 

 ![avatar]( 20201216210613879.png) 



--------------------------------------------------------------------------------

#  First, theoretical knowledge 

##  1. Principal curvature, mean curvature, and Gaussian curvature 

   Curvature is a measure of the degree of curvature of a curve. As an "external" bending measurement standard in differential geometry, the average curvature describes the curvature of a curved surface embedded in the surrounding space (such as a two-dimensional curved surface embedded in a three-dimensional Euclidean space). Gaussian curvature is a quantity that describes the concave-convex properties of a surface. When the degree of change of this quantity is large, the internal change of the surface surface is relatively large, which indicates that the smoothness of the surface is lower. There is a point cloud in the neighborhood of a surface approaching the point at any point in the point cloud, and the curvature at a point can be characterized by the local curvature of the surface fitted to the point and its neighborhood points. By least squares fitting, the quadric surface can be used to characterize the local area, and the principal curvature, average curvature, and Gaussian curvature at each point are calculated. In the formula: it is the partial differential of the surface, which is called the first fundamental invariant of the surface and the second fundamental invariant of the surface. 

##  2. Calculation of curvature 

   Take a data point in the scattered point cloud, and then take a point uniformly in the point cloud as the center. This point should cover the entire point cloud as much as possible. Through this point, the least squares method is used to fit the quadric surface. After solving the coefficients, the Gaussian curvature and average curvature of the data points are calculated according to the properties of the space surface curve. 

##  3. Type of local surface 

   According to the properties of differential geometry, the principal curvature is the embodiment of the local properties of the sampling point. Gaussian curvature is the product of the principal curvature. According to its sign, the properties of the point on the surface can be determined, indicating that the point is an ellipse point, a parabolic point, then, a hyperbolic point (K < O); the average curvature is the average value of the sum of the principal curvatures, which can indicate the convex and concave of the surface. Table 1 gives the average curvature and Gaussian curvature represented by different symbols. It can be seen from the table that the convex and concave information of the sampling point can be obtained from the symbol of the average curvature value. For sharp points with intense surface changes, there is no need to consider their specific convex and concave information when detecting. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574275597
  ```  
#  III. Display of results 

 ![avatar]( 20201029084020970.png) 



--------------------------------------------------------------------------------

