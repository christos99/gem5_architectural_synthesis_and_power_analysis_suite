# 9432_Christos_Chrysikos_Omada_B_7 
# Ergastirio 1o Arxitektoniki - LAB 1 Computer Architecture
# gem5
--------------------------------------------------------------------------------------------------
## 1.  

#### Information extracted from the first simulation
**cmd:**		
	
	$ ./build/ARM/gem5.opt -d hello_result configs/example/arm/starter_se.py --cpu="minor" "tests/test-progs/hello/bin/arm/linux/hello"
	
#### Extracting values from file [starter_se.py](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/hello%20Resluts/hello_result_MinorCPU_starter_se_py/starter_se.py)		

#### CPU:
* CPU Type = "Minor"  _//Decalred at the command_     
* self.num_cpus = 0    _//line 91 starter_se.py_  
* Frequency = 1 Ghz  _//line 95 starter_se.py_      

* **Basic Units =** 
	* L1Instruction Cache
	* L1Data Cache
	* Walk cache
	* L2 cache


#### **Cache:**

* **L1Instruction Cache:**
    * tag_latency = 1
    * data_latency = 1
    * response_latency = 1
    * mshrs = 4
    * tgts_per_mshr = 8
    * size = '48kB'
    * assoc = 3  
    
* **L1Data Cache:**
    * tag_latency = 2
    * data_latency = 2
    * response_latency = 1
    * mshrs = 16
    * tgts_per_mshr = 16
    * size = '32kB'
    * assoc = 2
    * write_buffers = 16  
    
* **Walk Cache:**
    * tag_latency = 4
    * data_latency = 4
    * response_latency = 4
    * mshrs = 6
    * tgts_per_mshr = 8
    * size = '1kB'
    * assoc = 8  
    * write_buffers = 16    
    
* **L2 Unified Cache:**
   * tag_latency = 12
   * data_latency = 12
   * response_latency = 5
   * mshrs = 32
   * tgts_per_mshr = 8
   * size = '1MB'
   * assoc = 16
   * write_buffers = 8
   * clusivity='mostly_excl'  
    
#### **Memory:**
  * membus = SystemXBar() 
  * memoryMode() == "timing"  _//line 116 starter_se.py_  

#### Voltage: 
  * voltage_domain = VoltageDomain(voltage="3.3V")"  _//line 94 starter_se.py_
  
  **[Info from [starter_se.py](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/hello%20Resluts/hello_result_MinorCPU_starter_se_py/starter_se.py), [devices.py](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/hello%20Resluts/hello_result_MinorCPU_starter_se_py/devices.py)]** 

**---------------------------------------------------------------------------------------------**

## 2 

### 2.a  

#### Extracting values from file [config.ini](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/hello%20Resluts/hello_result_MinorCPU_starter_se_py/config.ini)

#### CPU:
  * CPU Type = "Minor"  //line 65 config.ini   
  * self.num_cpus = 0    
  * Frequency = 1 Ghz  //line 8 config.ini  



#### Basic Units:
  * devices.L1I, devices.L1D, devices.WalkCache, devices.L2


#### Caches:  
  * cache_line_size = 64" //line 15 config.ini


#### Memory:  
  * membus = SystemXBar()   
  * cpu_cluster.memoryMode() == "timing":  //line 20 config.ini
#### Voltage:  
  * voltage_domain = VoltageDomain(voltage="3.3V")"  //line 48 config.ini
### 2.b  

 Number of Commited Instructions = 5028  
_The number differs because we use a different system than the one that was used to provide the statistics_
[**Reference File**](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/hello%20Resluts/hello_result_MinorCPU_starter_se_py/stats.txt)

### 2.c
_This is not finalized i would like to add more stuff and reference my answers if i had the time_


**Info from [config.ini](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/hello%20Resluts/hello_result_MinorCPU_starter_se_py/config.ini)** 

**---------------------------------------------------------------------------------------------**


## 3. IN-ORDER CPU's:
There are 4 differnet models of IN_ORDER CPU's in gem5:
 * SimpleCPU
 * 03CPU
 * TraceCPU
 * MinorCPU Model  
 ### SimpleCPU:  
 The SimpleCPU is a purely functional, in-order model that is suited for cases where a detailed model is not necessary. This can include warm-up 	periods, client systems that are driving a host, or just testing to make sure a program works.  
 
##### The Simple CPU can be broken up into three classes with different memory systems:**   
  * BaseSimpleCPU
  * AtomicSimpleCPU 
  * TimingSimpleCPU
 	
**BaseSimpleCPU**

The BaseSimpleCPU serves several purposes:
 * Holds architected state, stats common across the SimpleCPU models.
 * Defines functions for checking for interrupts, setting up a fetch request, handling pre-execute setup, handling post-execute actions, and advancing the PC to the next instruction. These functions are also common across the SimpleCPU models.
 * Implements the ExecContext interface. 
 
The BaseSimpleCPU can not be run on its own. You must use one of the classes that inherits from BaseSimpleCPU, either AtomicSimpleCPU or TimingSimpleCPU.

**AtomicSimpleCPU**

The AtomicSimpleCPU is the version of SimpleCPU that uses atomic memory accesses (see Memory systems for details). It uses the latency estimates from the atomic accesses to estimate overall cache access time. The AtomicSimpleCPU is derived from BaseSimpleCPU, and implements functions to read and write memory, and also to tick, which defines what happens every CPU cycle. It defines the port that is used to hook up to memory, and connects the CPU to the cache.

**TimingSimpleCPU**

The TimingSimpleCPU is the version of SimpleCPU that uses timing memory accesses (see Memory systems for details). It stalls on cache accesses and waits for the memory system to respond prior to proceeding. Like the AtomicSimpleCPU, the TimingSimpleCPU is also derived from BaseSimpleCPU, and implements the same set of functions. It defines the port that is used to hook up to memory, and connects the CPU to the cache. It also defines the necessary functions for handling the response from memory to the accesses sent out.

You can find reference [here](https://www.gem5.org/documentation/general_docs/cpu_models/SimpleCPU)

### O3CPU  

The O3CPU is our new detailed model for the v2.0 release. It is an out of order CPU model loosely based on the Alpha 21264. This page will give you a general overview of the O3CPU model, the pipeline stages and the pipeline resources. We have made efforts to keep the code well documented, so please browse the code for exact details on how each part of the O3CPU works

You can find reference [here](https://www.gem5.org/documentation/general_docs/cpu_models/O3CPU)

### TraceCPU

The Trace CPU model plays back elastic traces, which are dependency and timing annotated traces generated by the Elastic Trace Probe attached to the O3 CPU model. The focus of the Trace CPU model is to achieve memory-system (cache-hierarchy, interconnects and main memory) performance exploration in a fast and reasonably accurate way instead of using the detailed but slow O3 CPU model. The traces have been developed for single-threaded benchmarks simulating in both SE and FS mode. They have been correlated for 15 memory-sensitive SPEC 2006 benchmarks and a handful of HPC proxy apps by interfacing the Trace CPU with classic memory system and varying cache design parameters and DRAM memory type. In general, elastic traces can be ported to other simulation environments.

You can find reference [here](https://www.gem5.org/documentation/general_docs/cpu_models/TraceCPU)

### MinorCPU

Minor is an in-order processor model with a fixed pipeline but configurable data structures and execute behaviour. It is intended to be used to model processors with strict in-order execution behaviour and allows visualisation of an instruction’s position in the pipeline through the MinorTrace/minorview.py format/tool. The intention is to provide a framework for micro-architecturally correlating the model with a particular, chosen processor with similar capabilities.

You can find reference [here](https://www.gem5.org/documentation/general_docs/cpu_models/minor_cpu)

### 3.a
The program that I created and used for my simulations is [myprog.c](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/myprog.c) with then i compiled for arm into [myprog_arm](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/myprog_arm):
		 
		//A simple program that prints a "A sample C program" output
		#include<stdio.h>
		
		int main()
		{
			printf("\nA sample C program\n\n");
		return 0;
		
		}
		//end
		
Simulation done using different configuration file (Before = [starter_se.py](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/hello%20Resluts/hello_result_MinorCPU_starter_se_py/starter_se.py) -> Now = [se.py](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/se.py))

#### First Simulation Run:
 * CMD: 	
		
		build/ARM/gem5.opt configs/example/se.py --cmd=tests/test-progs/hello/bin/arm/linux/myprog_arm --cpu-type=MinorCPU --l1d_size=64kB --l1i_size=16kB --caches  
	
 * CPU TYPE = MinorCPU	
 * configuration file = [se.py](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/se.py)
 * program file = [myprog_arm](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/myprog_arm)
 * simulation seconds = 0.000033s  
 
 [Reference File](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/myprog_arm%20Results/my_prog_result_MinorCPU_se_py/stats.txt)
 
 #### Second Simulation Run:
 
 * CMD: 	
		
		build/ARM/gem5.opt configs/example/se.py --cmd=tests/test-progs/hello/bin/arm/linux/myprog_arm --cpu-type=TimingSimpleCPU --l1d_size=64kB --l1i_size=16kB --caches  
	
 * CPU TYPE = TimingSimpleCPU	
 * configuration file = [se.py](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/se.py)
 * program file = [myprog_arm](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/myprog_arm)
 * simulation seconds =  0.000037s  
 
[Reference File](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/myprog_arm%20Results/my_prog_result_TimingSimpleCPU_se_py/stats.txt)

### 3.b

Time difference between the 2 simulations  = 0.000037 - 0.000033 = 0.000004s
_This is not finalized i would like to add more stuff and reference my answers if i had the time_

>The TimingSimpleCPU is the version of SimpleCPU that uses timing memory accesses. It stalls on cache accesses and waits for the memory system to respond prior to proceeding. Regardless the time differnce is unsignificant and we can't run into any assumptions for the general performance difference of this 2 processors referring to this simulation.

### 3.c  

#### Third Simulation Run:
_Simulation run with change of cores value to 12_
 * CMD: 	
	
		build/ARM/gem5.opt configs/example/se.py --cmd=tests/test-progs/hello/bin/arm/linux/myprog_arm --cpu-type=MinorCPU --l1d_size=64kB --l1i_size=16kB --caches -n 12
	
		
 * CPU TYPE = MinorCPU	
 * configuration file = [se.py](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/se.py)
 * program file = [myprog_arm](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/myprog_arm)
 * simulation seconds =  0.000033s
 
 [Reference File](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/myprog_arm%20Results/my_prog_result_n%3D12_MinorCPU_se_py/stats.txt)
	
	
 #### Fourth Simulation Run:
 _Simulation run with change of cores value to 12_
 
 * CMD: 		
 	
		build/ARM/gem5.opt configs/example/se.py --cmd=tests/test-progs/hello/bin/arm/linux/myprog_arm --cpu-type=TimingSimpleCPU --l1d_size=64kB --	l1i_size=16kB --caches  -n 12
	
	
	
 * CPU TYPE = TimingSimpleCPU	
 * configuration file = [se.py](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/se.py)
 * program file = [myprog_arm](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/myprog_arm)
 * simulation seconds =   0.000037s

[Reference File](https://github.com/christos99/9432_Christos_Chrysikos/blob/main/Results%20Folder/myprog_arm%20Results/my_prog_result_n%3D12_TimingSimpleCPU_se_py/stats.txt)
	
	
		



**---------------------------------------------------------------------------------------------**


