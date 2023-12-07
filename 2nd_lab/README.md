# 9432_Christos_Chrysikos_B
2nd Lab on gem-5 simulations Computer Architecture

--------------------------------------------------------------------------------------------------------------------------------------------------------------

## First Part


### 1.(Basic Paramters of the CPU):

#### Cache


* L1I:
  * Size = 32kB
  * Assoc = 2

* L1D:
  * Size = 64kB
  * Assoc = 2

* L2:
   * Size = 2MB
   * Assoc = 8

* Cache Line:
  * Size = 64


Options.py:[here](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/References/Options.py)

--------------------------------------------------------------------------------------------------------------------------------------------------------------


### 2. (SIM_SECONDS, CPI, MISS RATES):

#### specbzip

  * SIM_SECONDS = 0.160359s

  * CPI = 1.603595

  * MISS RATES
    * L1I = 0.000075
    * L1D = 0.014123
    * L2 = 0.295235

#### specmcf

* SIM_SECONDS = 0.123265s

* CPI = 1.232645

* MISS RATES
  * L1I = 0.019046
  * L1D = 0.002062
  * L2 = 0.067668

#### spechmmer

* SIM_SECONDS = 0.118517s

* CPI = 1.185174

* MISS RATES**
  * L1I = 0.000212
  * L1D = 0.001619
  * L2 = 0.078295

#### speclibm

* SIM_SECONDS = 0.262262s

* CPI = 2.622616

* MISS RATES 
  * L1I = 0.000095	
  * L1D =0.060972
  * L2 = 0.999978

#### specsjeng

* SIM_SECONDS = 0.705640s

* CPI = 7.0564

* MISS RATES
  * L1I = 	0.000020
  * L1D = 0.121831
  * L2 = 0.999940

Data gathered in a [file](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/CPI%20-%20Results-All/spec_results_1GHz-default.txt)
**GRAPHS:**
 * ![CPI GRAPH](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/CPI.jpg)  
 * ![SIM SECONDS GRAPH](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/SIM_SECONDS-page-001.jpg)  
 * ![L1I MISS GRAPH](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/L1I_Miss_Rate-page-001.jpg)  
 * ![L1D MISS GRAPH](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/L1D_Miss_Rate.jpg)  
 * ![L2 MISS GRAPH](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/L2_Miss_Rate-page-001.jpg)  
  
  Reference Files:
* [specbzip](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_1GHz-32kB-4-64kB-4-2048kB-16-64/specbzip)
* [spechmmer](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_1GHz-32kB-4-64kB-4-2048kB-16-64/spechmmer)
* [speclibm](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_1GHz-32kB-4-64kB-4-2048kB-16-64/speclibm)
* [specmcf](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_1GHz-32kB-4-64kB-4-2048kB-16-64/specmcf)
* [specsjeng](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_1GHz-32kB-4-64kB-4-2048kB-16-64/specsjeng)


--------------------------------------------------------------------------------------------------------------------------------------------------------------



### 3.(CPU CLOCK = 2GHz)

When we run the simualtion with cpu-clock = 2GHz we see that the system.clk_domain.clock = 1000 but the cpu_cluster.clk_domain.clock = 500. If we increase the cpu-clock=4GHz then cpu_cluster.clk_domain.clock= 250 so I suppose that whatever the CPU clock cycle is in GHz it is two or in the last case four times faster than the system clock. System clock is defined as the speed of the system that does not include the CPU such as the memory and the caches. 
* **SIM_SECONDS**
  * 1GHz(average) = 0.2740086s [spec_results_1GHz](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/CPI%20-%20Results-All/RESULTS_1_2_4_GHz/spec_results_1GHz-latest-all.txt)
  * 2GHz(average) = 0.1788366s [spec_results_2GHz](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/CPI%20-%20Results-All/RESULTS_1_2_4_GHz/spec_results_2GHz-default.txt)
  * 4GHz(average) = 0.1316488s [spec_results_4GHz](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/CPI%20-%20Results-All/RESULTS_1_2_4_GHz/spec_results_4GHz-default.txt)

As we review the sim_seconds for each individual simulation, we can easily extract that there is definetely increased performance as we increase the clock speeds .On the contrary we can't observe any type of scalabilty to the clock increase. For example for the first simulation we have a clock speed of 1GHz and the sim_seconds are 0.274s in average, as we double the clock speed we expect to see half the runntime but that it is not the case here. The sim_seconds for 2GHz are 0.1788s which is greater than 0.274/2 = 0.137s and we procceed with a greater clock increase such as 4GHz, the change in sim_seconds is even smaller sim seconds = 0.1316488s > 0.1788/2 = 0.0894s and even greater than 0.137/2 = 0.0685s which is the 1/4 of the 1GHz runtime.  As coclusion an increase in CPU clock will increase the performance but not proportionally to the clock increase.

In case we add another CPU the frequency is going to be 2GHz or what ever else we define as we run the simulation. 

Sources that say more about clock speed and general cpu performance increase:
[Factors affecting processor performance](https://isaaccomputerscience.org/concepts/sys_arch_performance)

**STATS:**
  * [stats.txt for the 2GHz](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_2GHz-32kB-4-64kB-4-2048kB-16-64)  
  * [stats.txt for the 4GHz](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Benchmarks/spec_results_4GHz-32kB-4-64kB-4-2048kB-16-64/specbzip/stats.txt) 

In case we add another CPU the frequency is going to be 2GHz or what ever else we define as we run the simulation. 



 
Benchmark Files for 2GHz:[specbzip](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_1GHz-32kB-4-64kB-4-2048kB-16-64/specbzip), [specmcf](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_1GHz-32kB-4-64kB-4-2048kB-16-64/specmcf), [spechmmer](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_1GHz-32kB-4-64kB-4-2048kB-16-64/spechmmer), [specsjeng](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_1GHz-32kB-4-64kB-4-2048kB-16-64/specsjeng), [speclibm](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_1GHz-32kB-4-64kB-4-2048kB-16-64/speclibm)  
Benchmark Files for 4GHz:[specbzip](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_4GHz-32kB-4-64kB-4-2048kB-16-64/specbzip), [specmcf](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_4GHz-32kB-4-64kB-4-2048kB-16-64/spechmmer), [spechmmer](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_4GHz-32kB-4-64kB-4-2048kB-16-64/speclibm), [specsjeng](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_4GHz-32kB-4-64kB-4-2048kB-16-64/specmcf), [speclibm](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/spec_results_4GHz-32kB-4-64kB-4-2048kB-16-64/specsjeng)


--------------------------------------------------------------------------------------------------------------------------------------------------------------



## Second Part

### All the different configurations I used.  
**(The list shows the different parameter that was changed while running the simulation, the other parameters do not vary from the default parameters used in the first simulation of this Lab above)**  

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


### 1. DIfferent Configurations:

**Configuring Only L1 Cache Size**  

**System 1: (L1i and L1d = 64kB)** 

* L1 instruction cache size = 64kB
* L1 instruction cache associativity = 2
* L1 data cache size = 64kB
* L1 data cache associativity = 2
* L2 cache size = 2048kB
* L2 cache associativity = 8
* cache line size = 64

CPI(average): 2.716  
SIM_SECONDS: 0.2716s

[BENCHMARKS](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/Latest%20Final%20Benchmarks/L1%20Cache/spec_results_default-64kB-64kB)

**System 2: (L1i and L1d = 128kB)** 

* L1 instruction cache size = 128kB
* L1 instruction cache associativity = 2
* L1 data cache size = 128kB
* L1 data cache associativity = 2
* L2 cache size = 2048kB
* L2 cache associativity = 8
* cache line size = 64

CPI(average): 2.710  
SIM_SECONDS: 0.271s

[BENCHMARKS](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/Latest%20Final%20Benchmarks/L1%20Cache/spec_results_default-128kB-128kB)


**System 3: (L1i and L1d = 256kB)** 

* L1 instruction cache size = 256kB
* L1 instruction cache associativity = 2
* L1 data cache size = 256kB
* L1 data cache associativity = 2
* L2 cache size = 2048kB
* L2 cache associativity = 8
* cache line size = 64

CPI(average): 2.704  
SIM_SECONDS: 0.2704s

[BENCHMARKS](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/Latest%20Final%20Benchmarks/L1%20Cache/spec_results_default-256kB-256kB)


**Configuring Only L2 Cache Size** 

**System 4: (L2 = 512kB)** 


* L1 instruction cache size = 32kB
* L1 instruction cache associativity = 2
* L1 data cache size = 64kB
* L1 data cache associativity = 2
* L2 cache size = 512kB
* L2 cache associativity = 8
* cache line size = 64

CPI(average): 2.750  
SIM_SECONDS: 0.2750s  

[BENCHMARKS](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/Latest%20Final%20Benchmarks/L2%20Cache/spec_results_default--512kB)

**System 5: (L2 = 1024kB)** 


* L1 instruction cache size = 32kB
* L1 instruction cache associativity = 2
* L1 data cache size = 64kB
* L1 data cache associativity = 2
* L2 cache size = 1024kB
* L2 cache associativity = 8
* cache line size = 64

CPI(average): 2.744  
SIM_SECONDS: 0.2744s
  

[BENCHMARKS](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/Latest%20Final%20Benchmarks/L2%20Cache/spec_results_default--1024kB)


**System 6: (L2 = 2048kB)** 


* L1 instruction cache size = 32kB
* L1 instruction cache associativity = 2
* L1 data cache size = 64kB
* L1 data cache associativity = 2
* L2 cache size = 2048kB
* L2 cache associativity = 8
* cache line size = 64

CPI(average): 2.740  
SIM_SECONDS: 0.274s

  

[BENCHMARKS](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/Latest%20Final%20Benchmarks/L2%20Cache/spec_results_default--2048kB)

**System 7: (L2 = 4096kB)** 


* L1 instruction cache size = 32kB
* L1 instruction cache associativity = 2
* L1 data cache size = 64kB
* L1 data cache associativity = 2
* L2 cache size = 4096kB
* L2 cache associativity = 8
* cache line size = 64

CPI(average): 2.735  
SIM_SECONDS: 0.2735s
  

[BENCHMARKS](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/Latest%20Final%20Benchmarks/L2%20Cache/spec_results_default--4096kB)

The remaining tests involve L1 and L2 cache association changes. After their completion I couldn't see any differences in CPI or SIM_SECONDS results. That's why I decided not to display them.

Average:(same everywhere)  
**L1 Association**  
* Different Assoc Values:6,8,10,12  
* L1 Assoc SIM_SECONDS: 0.2750s
* L1 Assoc CPI: 2.75  

[BENCHMARKS for L1 Association](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/Latest%20Final%20Benchmarks/L1%20Cache%20Assoc)

**L2 Association**  
Average:(same everywhere)
* Different Assoc Values:4,8,16,32
* L2 Assoc SIM_SECONDS: 0.2750s
* L2 Assoc CPI: 2.75


[BENCHMARKS for L2 Association](https://github.com/christos99/9432_Christos_Chrysikos_B/tree/main/Files/Benchmarks/Latest%20Final%20Benchmarks/L2%20Cache%20Assoc)


### 2. Graphs
 

* **L1 Size CPI:**
![L1 Size CPI](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/New%20Charts/CPI%20L1%20CACHE%20SIZE-page-001.jpg)
* **L2 Size CPI:**  
![L2 Size CPI](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/New%20Charts/L2%20CACHE%20SIZE%20CPI-page-001.jpg)  
* **L1 Size SIM SECONDS(average for all 5 test together):**  
![L1 Size SIM SECONDS](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/New%20Charts/L1%20SIze%20Sim%20Seconds.png)  
* **L2 Size SIM SECONDS(average for all 5 test together):**  
![L2 Size SIM SECONDS](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/New%20Charts/L2%20SIze%20Sim%20Seconds.png)  
* **L1 Assoc CPI(average for all 5 test together):**  
![L1 Assoc CPI](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/New%20Charts/L1%20Assoc%20CPI.png)  
* **L2 Assoc CPI(average for all 5 test together):**  
![L2 Assoc CPI](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/New%20Charts/L2%20Assoc%20CPI.png)  
* **L1 Assoc SIM SECONDS(average for all 5 test together):**  
![L1 Assoc SIM SECONDS](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/New%20Charts/L1%20Assoc%20Sim%20Seconds.png)  
* **L2 Assoc SIM SECONDS(average for all 5 test together)**  
![L2 Assoc SIM SECONDS](https://github.com/christos99/9432_Christos_Chrysikos_B/blob/main/Files/Graphs/New%20Charts/L2%20Assoc%20Sim%20Seconds.png)





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

