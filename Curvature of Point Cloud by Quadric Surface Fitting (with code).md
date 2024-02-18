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

