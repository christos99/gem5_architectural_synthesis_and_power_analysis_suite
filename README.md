# 9432_Christos_Chrysikos_Omada_B_7 
# Ergastirio 1o Arxitektoniki - LAB 1 Computer Architecture
# gem5
--------------------------------------------------------------------------------------------------
# Introduction to gem5

- ### Overview of gem5 simulator
- ### Importance in computer architecture research

# Project Setup

- ### Project repository and directory structure
- ### Introduction to ARM architecture and simulation environment

# gem5 Simulation Environment

- ### Command line for initiating simulations
- ### Understanding the starter_se.py configuration script

# CPU and Memory Configuration

- ### CPU types and configurations in gem5
- ### Memory hierarchy and cache configuration
- ### Voltage and frequency settings

# Simulation Results Analysis

- ### Analyzing the output of the initial simulation
- ### Interpreting config.ini and stats.txt files
- ### Comparing different CPU models (MinorCPU vs. TimingSimpleCPU)

# In-depth CPU Model Exploration

- ### SimpleCPU, AtomicSimpleCPU, TimingSimpleCPU
- ### MinorCPU, O3CPU, and TraceCPU model descriptions

# Custom Simulation

- ### Developing and compiling a custom program (myprog.c)
- ### Adjusting simulation parameters for custom program execution

# Comparative CPU Performance Analysis

- ### Comparing MinorCPU and TimingSimpleCPU performance
- ### Time difference analysis and impact on simulation

# Practical Implications

- ### Interpretation of simulation data
- ### Relevance to real-world processor performance and optimization

# Conclusion and Future Work

- ### Summary of findings from the gem5 simulations
- ### Potential for future research and exploration with gem5

# Appendices and References

- ### Code listings and simulation command references
- ### Links to relevant files and further reading materials
 
		
**---------------------------------------------------------------------------------------------**


## 2nd Lab on gem-5 simulations - Computer Architecture

## First Part

### 1. Basic Parameters of the CPU:

#### Cache
- **L1I**: Size = 32kB, Assoc = 2
- **L1D**: Size = 64kB, Assoc = 2
- **L2**: Size = 2MB, Assoc = 8
- **Cache Line**: Size = 64

[Options.py](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/References/Options.py)

### 2. SIM_SECONDS, CPI, MISS RATES:
- **specbzip**: SIM_SECONDS = 0.160359s, CPI = 1.603595, MISS RATES (L1I = 0.000075, L1D = 0.014123, L2 = 0.295235)
- **specmcf**: SIM_SECONDS = 0.123265s, CPI = 1.232645, MISS RATES (L1I = 0.019046, L1D = 0.002062, L2 = 0.067668)
- **spechmmer**: SIM_SECONDS = 0.118517s, CPI = 1.185174, MISS RATES (L1I = 0.000212, L1D = 0.001619, L2 = 0.078295)
- **speclibm**: SIM_SECONDS = 0.262262s, CPI = 2.622616, MISS RATES (L1I = 0.000095, L1D = 0.060972, L2 = 0.999978)
- **specsjeng**: SIM_SECONDS = 0.705640s, CPI = 7.0564, MISS RATES (L1I = 0.000020, L1D = 0.121831, L2 = 0.999940)

**GRAPHS:**
- ![CPI GRAPH](CPI.jpg)
- ![SIM SECONDS GRAPH](SIM_SECONDS.jpg)
- ![L1I MISS GRAPH](L1I_MISS.jpg)
- ![L1D MISS GRAPH](L1D_MISS.jpg)
- ![L2 MISS GRAPH](L2_MISS.jpg)

### 3. CPU CLOCK = 2GHz
- With increased CPU clock speed (up to 4GHz), performance improves but not proportionally.
- System clock remains at a lower frequency than CPU clock.
- **SIM_SECONDS** drops with higher CPU frequency but not by expected factor.

**STATS:**
- [2GHz stats](2GHz_stats.txt)
- [4GHz stats](4GHz_stats.txt)

## Second Part

### Different Configurations Tested
- Varied L1i/L1d cache size (64kB, 128kB, 256kB)
- Varied L2 cache size (512kB, 1024kB, 2048kB, 4096kB)
- Varied L1i/L1d cache associativity (6, 8, 10, 12)
- Varied L2 cache associativity (4, 8, 16, 32)

### 1. Different Configurations:
#### System 1: (L1i and L1d = 64kB)
- CPI(average): 2.716
- SIM_SECONDS: 0.2716s
#### System 2: (L1i and L1d = 128kB)
- CPI(average): 2.519
- SIM_SECONDS: 0.2519s

#### System 3: (L1i and L1d = 256kB)
- CPI(average): 2.307
- SIM_SECONDS: 0.2307s

### 2. Best Configuration:
- **Best L1 Config**: 256kB size with 6-way associativity
- **Best L2 Config**: 4096kB size with 8-way associativity
- Achieved **lowest CPI** of 2.1 and **SIM_SECONDS** of 0.21s

### 3. Observations:
- Increasing cache size and associativity usually improves performance but has diminishing returns.
- There's an optimal point for cost vs. performance trade-off.

## Conclusion

- Cache size and associativity significantly affect the performance of the CPU.
- Higher CPU frequencies improve performance but system clock can become a bottleneck.
- Optimal cache configuration depends on the specific workload and requirements.





**---------------------------------------------------------------------------------------------**

## Third Part

When we think of designing a CPU cache memmory hierarchy the first thing that comes to mind alogside with performance is the cost. Yes it is certain that we want to build the fastest and most powerfull CPU but we also want to make it as cheap as possible so it's easily distributed and used. With that in my mind through my reasearch I collected some information after runnning several simulations with different specifications for CPU Cache design and size. I 've listed them below from System 1-7 (I ran many different benchmarks but I chose those who had the most sagnificant differences).  

About the CPU Design, the L1I and L1D cache is the very fist level of cache memmory inside the CPU and therefore the fastest. The most commonly used size for those caches is 16-32-64 kB. There is a reason we won't make them bigger,first the cost as I mentioned before this SRAM type of memmory is very expensive and second the bigger the cache size the smaller the miss rate, that sounds good at first but it creates other kind of problems. There are 3 kinds of misses compulsory, capacity, and conflict. When we increase the size the conflict misses increase and when we decrease the size we more compulsory misses. It is therfore optimal to find  a sweet spot which in this case is 32-64kB and in some cases 128kB.  
For L2 Cache the things are a bit different we have a larger sized cache in general, ranged from 512kb to 2048 kb and in some cases even 4096kB or 8192kB. It is still fast SRAM but not as fast and expensive as the L1. We use L2 cache to reduce the penalty from going to the main memory. So it 's a Level between CPU - L1 Cache and main memory DRAM.  
Then last we consider the associativity between cache levels. Every cache level I reffered to has it's own level of assocaitivity, there are three types of associativity.

 * 1 - way associative or else direct mapped
 * N - way associative 
 * Fully associative
 
 Increasing the associativity increases the complexity of the CPU and therefore the cost.  
 There is more inforamtion about Caches to the links I 've used bellow. Those are the references I used, trying to make an estimate of what the prices of the caches are going to be.
 
 
Cost Estimates: 
* L1i and L1d = 5.000$ per GB (considering manufacture and design it is the most expensive SRAM)
* L2 = 2.500 per GB (easier and cheaper to make than L1 cache but still SRAM)
* Assocativity = for every multiplication by two the cost doubles(for example: assoc = 2, cost = 2 | assoc = 4, cost = 4 etc) 
  lets estimate that for assoc = 2 the cost = 0.5$ dollars 
* Cache line is not changed so I won't consider that in the cost.

Reference for Costs and Prices and CPU Architecture: 
* [University of NOTRE DAMNE](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/References/University%20of%20NOTREDAM%20Presentation.pdf) 
* [Caches and Memory Presentation](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/References/lecture_caches-handout.pdf)


With those values in mind we create a function that calculates the cost of our CPU:

Cost = L1 instruction cache size(in kB) * 0.005$ + L1 data cache size(in Kb) * 0.005$ + L1 instruction cache associativity * 0.25$ + L1 data cache associativity * 0.25$ + L2 cache size(in kB) * 0.0025$ + L2 data cache associativity * 0.25$
(I will consider making the L1 cache size more expensive or maybe the associativity and L2 cache cheaper because I think the prices are not proportianl and may give an inaccurate conclusion)  

**System 1: (L1i and L1d = 64kB):**

* L1 instruction cache size = 64kB : 0.32$
* L1 instruction cache associativity = 2 : 0.5$
* L1 data cache size = 64kB : 0.32$
* L1 data cache associativity = 2 : 0.5$
* L2 cache size = 2048kB : 10.24$
* L2 cache associativity = 8 : 2$

CPI(average): 2.716

Total Cost = 13.88$  

**System 2: (L1i and L1d = 128kB):**

* L1 instruction cache size = 128kB : 0.64$
* L1 instruction cache associativity = 2 : 0.5$
* L1 data cache size = 128kB : 0.64$
* L1 data cache associativity = 2 : 0.5$
* L2 cache size = 2048kB : 10.24$
* L2 cache associativity = 8 : 2$

CPI(average): 2.710

Total Cost = 14.52$

**System 3: (Li and L1d = 256kB):**

* L1 instruction cache size = 256kB : 1.28$
* L1 instruction cache associativity = 2 : 0.5$
* L1 data cache size = 256kB : 1.28$
* L1 data cache associativity = 2 : 0.5$
* L2 cache size = 2048kB : 10.24$
* L2 cache associativity = 8 : 2$

CPI(average): 2.704

Total Cost = 15.8$


**System 4: (L2 = 512kB):**

* L1 instruction cache size = 32kB : 0.16$
* L1 instruction cache associativity = 2 : 0.5$
* L1 data cache size = 64kB : 0.32$
* L1 data cache associativity 2 : 0.5$
* L2 cache size = 512kB : 2.56$
* L2 cache associativity = 8 : 2$

CPI(average): 2.750

Total cost = 6.04$

**System 5: (L2 = 1024kB):**  

* L1 instruction cache size = 32kB : 0.16$
* L1 instruction cache associativity = 2 : 0.5$
* L1 data cache size = 64kB : 0.32$
* L1 data cache associativity 2 : 0.5$
* L2 cache size = 1024kB : 5.12$
* L2 cache associativity = 8 : 2$

CPI(average): 2.744

Total cost = 8.6$


**System 6: (L2 = 2048kB):**  

* L1 instruction cache size = 32kB : 0.16$
* L1 instruction cache associativity = 2 : 0.5$
* L1 data cache size = 64kB : 0.32$
* L1 data cache associativity 2 : 0.5$
* L2 cache size = 2048kB : 5.12$
* L2 cache associativity = 8 : 2$

CPI(average): 2.740

Total cost = 13.72$

**System 7: (L2 = 4096kB):**  

* L1 instruction cache size = 32kB : 0.16$
* L1 instruction cache associativity = 2 : 0.5$
* L1 data cache size = 64kB : 0.32$
* L1 data cache associativity 2 : 0.5$
* L2 cache size = 4096kB : 5.12$
* L2 cache associativity = 8 : 2$

CPI(average): 2.735

Total cost = 18.84$


![COST-CPI GRAPH](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/New%20Charts/CPI-COST.jpg)

As a first conclusion we could say that the best CPU configuration was the System 3. The price was not so high but the CPI was the closer to 1.




Bibliography:
* [https://www.sciencedirect.com/topics/computer-science/set-associative-cache](https://www.sciencedirect.com/topics/computer-science/set-associative-cache)  
* [https://courses.cs.washington.edu/courses/cse378/09au/lectures/cse378au09-20.pdf](https://courses.cs.washington.edu/courses/cse378/09au/lectures/cse378au09-20.pdf)
* [Memory systems](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/References/memory-systems.pdf)
* [Caches and Memory](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/References/lecture_caches-handout.pdf)
* [Science Magazine](https://www.extremetech.com/extreme/188776-how-l1-and-l2-cpu-caches-work-and-why-theyre-an-essential-part-of-modern-chips)




# 9432_Christos_Chrysikos_C

2nd Lab on gem-5 simulations Computer Architecture


## <ins>Part 1: Getting to know McPAT</ins>


### 1.
[Output of Xeon](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Output%20Files/Xeon.txt)

#### Dynamic Power :
Circuits dissipate dynamic power when they charge and discharge the capacitive loads to switch states. Dynamic power is proportional to the total load capacitance, the supply voltage, the voltage swing during switching, the clock frequency, and the activity factor. Dynamic Power does  seem to be affected by the program that we run but not as much as of changing system paramateters.

Example using the same system running two different benchmarks:

* [specbzip](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Energy%20results/specbzip/L1_128_specbzip-energy.txt) 
  * dynamic power = 0.439631 W  
  * leakage = 2.129390 W 
  * runtime = 0.157622 s 
  
* [spechmmer](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Energy%20results/spechmmer/L1_128_spechmmer-energy.txt)
  * dynamic power = 0.491212 W  
  * leakage = 2.129390 W 
  * runtime = 0.118297 s 

We see that spechmmer has slighly greater dynamic power value than specbzip. Runtime does not affect the dynamic or static power but the energy consumtion of the system.



[McPAT 1.0: An Integrated Power, Area, and Timing Modeling Framework for
Multicore Architectures](https://www.hpl.hp.com/research/mcpat/McPATAlpha_TechRep.pdf)

#### Leakage :

Transistors in circuits leak, dissipating static power. Leakage current depends on the width of the transistors and the local state of the devices. There are two leakage mechanisms. Subthreshold leakage occurs because a small current passes between the source and drain of off-state transistors. Gate leakage is the current leaking through the gate terminal, and varies greatly with the state of the device. Leakage is not affected by the executable but from the characteristics of the system,same for all applications.

[McPAT 1.0: An Integrated Power, Area, and Timing Modeling Framework for
Multicore Architectures](https://www.hpl.hp.com/research/mcpat/McPATAlpha_TechRep.pdf)



### 2.

The proccessor with th 40 W is propably going to be faster and therefore finish an application in less time than thee 4W, which means that the system is going to require less energy. For a more accurate answer we whould need to know the leakge power of the proccessor because that is what consumes energy after the application is finshed. The dynamic power ,the leakage and the simulation time are data that are extracted both from McPAT and from gem5 and are vital for a more accurate answer.



### 3.  
The power that each proccessor consumes is a combination of dyanmic and static (leakage) power. We now that after the finalization of the program the system still runs and therefore we need to compare the static power of those 2 cpu's to find whick one is more efficient. Extracting from bibliography ARM have significantly smaller static power consumtion than x86 cpu's.

Let's assume that Xeon takes 10 seconds to run a program. Being 40 times faster than ARM, ARM A9 needs 40 seconds to run the same program.

**Runtime Dynamic** 

  * Xeon == 72.9199 W  
    EDP == (72.9199 + 36.8319) x 1 == 134.938 mJ
  * ARM A9  == 2.96053 W  
    EDP == (2.96053 + 0.108687) x 40 == 122.7652 mJ
    
 It is obvious that even though the ARM A9 runs for a longer period of time, but still is more energy efficient than the Xeon proccessor.
  
     
* [Output of Xeon](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Output%20Files/Xeon.txt)  
* [Output of ARM](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Output%20Files/ARM.txt)



## <ins>Part 2: gem5 and McPAT</ins>


### 1.

### 1. (Default Parameters of the CPU):
#### CPU
* cpu clock = 1GHz

#### Cache
|     CPU    | Clock |
|:----------:|:-----:|
|      1     |  1GHz |


|    Cache   |  Size | Assoc |
|:----------:|:-----:|:-----:|
|     L1I    |  32kB |   2   |
|     L1D    |  64kB |   2   |
|     L2     |  2MB  |   8   |
| Cache line |   64  |       |



Here are in categories the parameter changed in every simulation (ex. default_configuration_of_gem5_L1_Cache_64kB). The ending of the name shows the changed parameter compared to the default CPU.


### All the different configurations I used.  
**(The list shows the different parameter that was changed while running the simulation, the other parameters do not vary from the default parameters)**  

* L1i and L1d = 64kB
* L1i and L1d = 128kB
* L1i and L1d = 256kB
* L2 = 512kB
* L2 = 1024kB
* L2 = 2048kB
* L2 = 4096kB
* L1i and L1d Assoc= 6
* L1i and L1d Assoc= 8
* L1i and L1d Assoc= 10
* L1i and L1d Assoc= 12
* L2 Assoc= 4
* L2 Assoc= 8
* L2 Assoc= 16
* L2 Assoc= 32


#### L1 Cache

| Parameter Changed |       |  L1 Cache |                |            |
|:-----------------:|-------|:---------:|----------------|------------|
|     Sim Number    |  Size | Spec      | Energy         | Peak Power |
|         1         | 64 kB | specbzip  | 304.612318 mJ  | 3.079 W    |
|         2         | 64 kB | spechmmer | 230.257257 mJ  | 3.079 W    |
|         3         | 64 kB | specjeng  | 1225.410820 mJ | 3.089 W    |  
|         4         | 64 kB | speclibm  | 469.125388 mJ  | 3.088 W    |
|         5         | 64 kB | specmcf   | 214.602407 mJ  | 3.088 W    |
|         6         | 128kB | specbzip  | 404.934228 mJ  | 3.545 W    | 
|         7         | 128kB | spechmmer | 310.009355 mJ  | 3.545 W    |
|         8         | 128kB | specjeng  | 1660.129841 mJ | 3.545 W    |
|         9         | 128kB | speclibm  | 634.297256 mJ  | 3.545 W    | 
|         10        | 128kB | specmcf   | 289.067039 mJ  | 3.545 W    | 
|         11        | 256kB | specbzip  | 478.687097 mJ  | 3.86 W     | 
|         12        | 256kB | spechmmer | 487.544624 mJ  | 3.86 W     | 
|         13        | 256kB | specjeng  | 1995.164951 mJ | 3.86 W     |
|         14        | 256kB | speclibm  | 449.788309 mJ  | 3.86 W     |
|         15        | 256kB | specmcf   | 347.131705 mJ  | 3.86 W     |

#### L1 Cache Assoc

| Parameter Changed |               | L1 Cache  Assoc |               |            |
|:-----------------:|:-------------:|:---------------:|:-------------:|:----------:|
|     Sim Number    | Associativity |       Spec      | Energy        | Peak Power |
|         1         |       6       |     specbzip    | 239.703350 mJ |   2.48 W   |
|         2         |       6       |    spechmmer    | 182.315531 mJ |   2.48 W   |
|         3         |       6       |     specjeng    | 940.009153 mJ |   2.48 W   |
|         4         |       6       |     speclibm    | 362.957233 mJ |   2.485 W  |
|         5         |       6       |     specmcf     | 184.659352 mJ |   2.485 W  |
|         6         |       8       |     specbzip    | 239.703350 mJ |   2.48 W   |
|         7         |       8       |    spechmmer    | 182.315531 mJ |   2.48 W   |
|         8         |       8       |     specjeng    | 940.009153 mJ |   2.48 W   |
|         9         |       8       |     speclibm    | 362.957233 mJ |   2.485 W  |
|         10        |       8       |     specmcf     | 184.659352 mJ |   2.485 W  |
|         11        |       10      |     specbzip    | 239.703350 mJ |   2.48 W   |
|         12        |       10      |    spechmmer    | 182.315531 mJ |   2.48 W   |
|         13        |       10      |     specjeng    | 940.009153 mJ |   2.48 W   |
|         14        |       10      |     speclibm    | 362.957233 mJ |   2.485 W  |
|         15        |       10      |     specmcf     | 184.659352 mJ |   2.485 W  |
|         16        |       12      |     specbzip    | 239.703350 mJ |   2.48 W   |
|         17        |       12      |    spechmmer    | 182.315531 mJ |   2.48 W   |
|         18        |       12      |     specjeng    | 940.009153 mJ |   2.48 W   |
|         19        |       12      |     speclibm    | 362.957233 mJ |   2.485 W  |
|         20        |       12      |     specmcf     | 184.659352 mJ |   2.485 W  |





#### L2 Cache
    
| Parameter Changed |       |  L2 Cache |                |            |
|:-----------------:|-------|:---------:|----------------|------------|
|     Sim Number    |  Size | Spec      | Energy         | Peak Power |
|         1         | 64 kB | specbzip  | 2243.260147 mJ | 2.315 W    |
|         2         | 64 kB | spechmmer | 181.772249 mJ  | 2.31  W    |
|         3         | 64 kB | specjeng  | 932.459064 mJ  | 2.31  W    |
|         4         | 64 kB | speclibm  | 360.837240 mJ  | 2.315 W    |
|         5         | 64 kB | specmcf   | 183.856990 mJ  | 2.315 W    |
|         6         | 128kB | specbzip  | 240.673442 mJ  | 2.39 W     |
|         7         | 128kB | spechmmer | 181.995179 mJ  | 2.38 W     |
|         8         | 128kB | specjeng  | 935.426950 mJ  | 2.38 W     |
|         9         | 128kB | speclibm  | 361.694166 mJ  | 2.385 W    |
|         10        | 128kB | specmcf   | 184.121653 mJ  | 2.385 W    |
|         11        | 256kB | specbzip  | 239.703350 mJ  | 2.48 W     |
|         12        | 256kB | spechmmer | 182.315531 mJ  | 2.48 W     |
|         13        | 256kB | specjeng  | 940.009153 mJ  | 2.48 W     |
|         14        | 256kB | speclibm  | 362.957233 mJ  | 2.485 W    |
|         15        | 256kB | specmcf   | 184.659352 mJ  | 2.485 W    |
|         16        | 256kB | specbzip  | 239.557962 mJ  | 2.61 W     |
|         17        | 256kB | spechmmer | 182.978396 mJ  | 2.61 W     |
|         18        | 256kB | specjeng  | 946.424763 mJ  | 2.61 W     |
|         19        | 256kB | speclibm  | 364.911324 mJ  | 2.615 W    |
|         20        | 256kB | specmcf   | 185.915461 mJ  | 2.615 W    |


#### L2 Cache Assoc

| Parameter Changed |               | L2 Cache  Assoc |               |                        |
|:-----------------:|:-------------:|:---------------:|:-------------:|:----------------------:|
|     Sim Number    | Associativity |       Spec      | Energy        | Peak Power (Core +_L2) |
|         1         |       4       |     specbzip    | 239.703350 mJ |         2.48 W         |
|         2         |       4       |    spechmmer    | 182.315531 mJ |         2.48 W         |
|         3         |       4       |     specjeng    | 940.009153 mJ |         2.48 W         |
|         4         |       4       |     speclibm    | 362.957233 mJ |         2.485 W        |
|         5         |       4       |     specmcf     | 184.659352 mJ |         2.485 W        |
|         6         |       8       |     specbzip    | 239.703350 mJ |         2.48 W         |
|         7         |       8       |    spechmmer    | 182.315531 mJ |         2.48 W         |
|         8         |       8       |     specjeng    | 940.009153 mJ |         2.48 W         |
|         9         |       8       |     speclibm    | 362.957233 mJ |         2.485 W        |
|         10        |       8       |     specmcf     | 184.659352 mJ |         2.485 W        |
|         11        |       16      |     specbzip    | 239.703350 mJ |         2.48 W         |
|         12        |       16      |    spechmmer    | 182.315531 mJ |         2.48 W         |
|         13        |       16      |     specjeng    | 940.009153 mJ |         2.48 W         |
|         14        |       16      |     speclibm    | 362.957233 mJ |         2.485 W        |
|         15        |       16      |     specmcf     | 184.659352 mJ |         2.485 W        |
|         16        |       32      |     specbzip    | 239.703350 mJ |         2.48 W         |
|         17        |       32      |    spechmmer    | 182.315531 mJ |         2.48 W         |
|         18        |       32      |     specjeng    | 940.009153 mJ |         2.48 W         |
|         19        |       32      |     speclibm    | 362.957233 mJ |         2.485 W        |
|         20        |       32      |     specmcf     | 184.659352 mJ |         2.485 W        |
 
* [Energy Results Files-specbzip](https://github.com/christos99/9432_Christos_Chrysikos_C/tree/main/Energy%20results/specbzip) 
* [Energy Results Files-spechmmer](https://github.com/christos99/9432_Christos_Chrysikos_C/tree/main/Energy%20results/spechmmer)
* [Energy Results Files-specjeng](https://github.com/christos99/9432_Christos_Chrysikos_C/tree/main/Energy%20results/specjeng) 
* [Energy Results Files-speclibm](https://github.com/christos99/9432_Christos_Chrysikos_C/tree/main/Energy%20results/speclibm)
* [Energy Results Files-specbmcf](https://github.com/christos99/9432_Christos_Chrysikos_C/tree/main/Energy%20results/specmcf) 

* [McPAT results for Peak Power](https://github.com/christos99/9432_Christos_Chrysikos_C/tree/main/MC_PAT_RESULTS)


### 2.

### GRAPHS

### EDP

* specbzip - EDP

![specbzip](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Graphs/specbzip.png)

* spechmmer - EDP

![spechmmer](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Graphs/spechmmer.png)

* specjeng - EDP

![specjeng](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Graphs/specjeng.png)

* speclibm - EDP

![speclibm](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Graphs/speclibm.png)

* specmcf - EDP

![specmcf](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Graphs/specmcf.png)

### PeaK Power

* specbzip - Peak Power

![specbzip](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Graphs/specbzip_Peak_Power.png)

* spechmmer - Peak Power

![spechmmer](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Graphs/spechmmer_Peak_Power.png)

* specjeng - Peak Power

![specjeng](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Graphs/specjeng_Peak_Power.png)

* speclibm - Peak Power

![speclibm](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Graphs/speclibm_Peak_Power.png)

* specmcf - Peak Power

![specmcf](https://github.com/christos99/9432_Christos_Chrysikos_C/blob/main/Graphs/specmcf_Peak_Power.png)

## <ins>Conclussion</ins>

We can see from the above graphs that peak power is strictly correlated with L1 Cache size (L2 Cache also but it insignificant), the bigger the cache the greater the peak power and therefore the bigger the EDP.It is also important to say that there was no difference in Peak Power between different bechmarks running at the same system, which is very reasonable (we don't expect our proccessor to be faster depending on the program). 

We assume that every result we get can differ in some percentage from reality. This occurs because McPAT is a simulator and just like gem5 it simulates the reults based on the commercial product. These simulators are based on what we speculate the architecture is because we don't know the exact details of a commercial product such as an intel or amd processor. We speculate some values we think they are close to the real product and based on those we run a simulation. This has a huge impact in accuracy of the simulator because we may miss many micro details from the original product. The first level of speculation begins with gem5 and it is therefore transfered to McPAT which increases even more the accuracy of the result. These simulators are widely used around the industry and sometimes the results are really close to reality but we have to take into consideration the  possibility of an error in those simulation results.


[gem5, GPGPUSim, McPAT, GPUWattch, "Your favorite simulator here"
Considered Harmful](https://research.cs.wisc.edu/vertical/papers/2014/wddd-sim-harmful.pdf)



Ωραία εργασία, το αντικείμενο που ασχολήθηκαμε είναι αρκετά επίκαιρο και ενδιαφέρον.
Παρατηρήσεις:
* Δεν ηταν ευκόλη η κατανόηση των εξόδων από τον McPAT στην αρχη.
* Δεν διευκρινίζεται πουθένα στην βιβλιογραφία τι είναι ακριβώς το EDP και EDAP.
* Στην άρχη είχα θέμα με το να τρέξω τον McPAT έπρεπε να βάλω εξτρα python2 από μπρόστα για να τρέξει.
* Οι πρώτες θεωρητικές ερωτήσεις αδύνατον να απαντηθούν με σιγουριά στην φάση που ζητούνται. Ισως στο τελος θα ηταν πιο απλό (αφού δηλαδή έχουν γίνει οι προσωμοιώσεις)





