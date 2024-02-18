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

