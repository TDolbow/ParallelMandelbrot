# Parallel Mandelbrot <br />

This code has been adapted from the rossetacode.com mandelbrot set implementation in c, which can be found here: https://rosettacode.org/wiki/Mandelbrot_set#C <by />

This parallelized code was tested with different configurations on the Bridges2 supercomputer to show how parallelization can be used to decrease the execution time of certain applications. <br /> 

The mandelbrot set is known to be "embarrassingly parallel", which means that every task can be completed independently from one another, making it a good candidate to be parallelized. <br />


# Setup

All of the code used in this repository was tested using NVHPC on the Bridges 2 supercomputer. Because of this, the provided bash scripts may not work on on other systems. <br />

### Loading the NVHPC Module on Bridges 2
The NVHPC module must be loaded on Bridges 2 to compile the code. To load this module, the module load NVHPC/21.7 command can be used. <br />




### Compiling Code
To compile code, the following commands can be used: 
  - ```nvc mandelbrot.c -o mandelbrot --- For serial compilation```
  - ```nvc -acc -gpu=cc70 -Minfo=accel openACCMandelbrot.c -o openACCMandelbrotGPU --- For OpenACC on GPU```
  - ```nvc -acc -ta=multicore -Minfo=accel openACCMandelbrot.c -o openACCMandelbrot --- For OpenACC on CPU```
  - ```nvc -mp -Minfo=accel openMPMandelbrot.c -o openMPMandelbrot --- For OpenMP on CPU```

### Running Compiled Programs on Bridges 2
Compiled programs can not be run directly on Bridges 2, and need to be submitted to the Bridges 2 scheduler to be run. This can be done by creating a bash file that follows the following format: 
```
  #! /bin/bash
  #SBATCH -A see200002p # specify the project or allocation number
  #SBATCH -p GPU-shared
  #SBATCH --gpus=v100-32:1
  #SBATCH -J myjob
  #SBATCH --mail-user= EmailHere
  #SBATCH --mail-type=ALL
  
  #SBATCH -N 1 #The number of nodes, not cores (16 cores per node)
  #SBATCH -n 16 #The number of cores requested in total. 
  #SBATCH -t 00:30:00 #Set the maximum runtime to 30 minutes
    Any commands to run go here
```
To submit the batch file to the scheduler, type the command ```sbatch nameOfScript```<br />

The total number of cores can be set by modifying the ```#SBATCH -n 16``` command to the desired number of cores. If this number is greater than 16, the ```#SBATCH -N 1``` command will need to be modified to accomondate the desired number of cores. For every 16 cores, 1 should be added to the number in this command.  

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

# OpenACC GPU Runtime
![unnamed (11)](https://user-images.githubusercontent.com/54713482/145099865-af8600eb-81cb-4799-bbb7-c39b7eb83005.png)

<br /> Only one GPU  was tested, but as shown by the NSIGHT Compute graph below, there is performnace left on the table. <br />
![unnamed (12)](https://user-images.githubusercontent.com/54713482/145100087-9a881e7c-3551-44e8-b672-2e5b2ea7e27e.png)

# Parallelization Comparison
![unnamed (13)](https://user-images.githubusercontent.com/54713482/145100184-20b19262-d2e3-43e0-8699-d2a9bd8b8cc8.png)
<br />






