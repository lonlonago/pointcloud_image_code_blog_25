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
