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

