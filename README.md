# Parallel Mandelbrot <br />

This code has been adapted from the rossetacode.com mandelbrot set implementation in c, which can be found here: https://rosettacode.org/wiki/Mandelbrot_set#C <by />

This parallelized code was tested with different configurations on the Bridges2 supercomputer to show how parallelization can be used to decrease the execution time of certain applications. <br /> 

The mandelbrot set is known to be "embarrassingly parallel", which means that every task can be completed independently from one another, making it a good candidate to be parallelized. <br />

# Serial Runtime
![unnamed](https://user-images.githubusercontent.com/54713482/145094837-16bcdd60-35f7-4c13-9275-9a41b5289ef0.png)

<br />Compiling the serial code with NVC provided an average run time of 282 seconds. <br />

# OpenMP Runtime
The code parallelized with with openMP was tested in 2,4,8, and 16 core configurations. The average times of each can be seen below. <br /> 
2 core:  <br />
![unnamed](https://user-images.githubusercontent.com/54713482/145094993-b7d68f2e-ed51-4be4-ad54-2f2954addde5.png)

<br />4 core: <br /> 
![unnamed (1)](https://user-images.githubusercontent.com/54713482/145095035-8c5c4267-494e-4a14-982c-9636dcf993bc.png)


<br />8 core: <br />
![unnamed (2)](https://user-images.githubusercontent.com/54713482/145095078-6f3243ca-2f93-4249-85ad-84851d9a819c.png)

<br />16 core: <br />
![unnamed (4)](https://user-images.githubusercontent.com/54713482/145095206-4caa2e31-0a2d-425c-b632-ddf4f09ce48b.png)


<br />This graph shows the performance of the OpenMP program as more cores are added. The lower the time, the better the performance. <br />
![unnamed (5)](https://user-images.githubusercontent.com/54713482/145095285-bf08d81e-65ae-4c58-bed8-34ba27299225.png)


# OpenACC Runtime
<br />The code parallelized with OpenACC was tested with 2, 4, 8, and 16 core configurations. The average times of each can be seen below. <br /> 

2 core: <br />
![unnamed (6)](https://user-images.githubusercontent.com/54713482/145095322-867e067a-c074-46f1-a9e7-95720b43f64a.png)

<br />4 core: <br />
![unnamed (7)](https://user-images.githubusercontent.com/54713482/145095460-eacaf7d7-187f-4d42-9775-910f4cc61f02.png)

<br />8 core:<br />
![unnamed (8)](https://user-images.githubusercontent.com/54713482/145095501-fbbac19c-0832-4a6f-8a51-7c41c82ba8cf.png)

<br />16 core:<br />
![unnamed (9)](https://user-images.githubusercontent.com/54713482/145095558-b74a0b28-b628-45fc-8918-8f7e4e29020e.png)



<br />This graph shows the performance of the OpenACC program as more cores are added. The lower the time, the better the performance.<br /> 
![unnamed (10)](https://user-images.githubusercontent.com/54713482/145095596-e4a1b755-50f2-40ec-a3b5-e31c7e76e7da.png)



