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

