## 9432_Christos_Chrysikos
## Ergastirio Arxitektoniki 1o Gem 5
--------------------------------------------------------------------------------------------------
1.   
**[Info from starter_se.py, devices.py]**   
#### CPU:
* CPU Type = "Minor"  _//Decalred at the command_    
* self.clusters = []   _//line 90 starter_se.py_  
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

Voltage: "voltage_domain = VoltageDomain(voltage="3.3V")"  _//line 94 starter_se.py



---------------------------------------------------------------------------------------------

2. **[Info from config.ini]**
#### CPU:
	 CPU Type = "Minor"  //line 65 config.ini 
	 self.clusters = []  
	 self.num_cpus = 0    
	 Frequency = 1 Ghz  //line 8 config.ini  



#### Basic Units:
	devices.L1I, devices.L1D, devices.WalkCache, devices.L2


#### Caches:  
	"cache_line_size = 64" //line 15 config.ini


#### Memory:  
	membus = SystemXBar()   
	cpu_cluster.memoryMode() == "timing":  //line 20 config.ini
#### Voltage:  
	"voltage_domain = VoltageDomain(voltage="3.3V")"  //line 48 config.ini
a.  

	Number of Commited Instructions = 5028  
	
_The number differs because we use a different system than the one that was used to provide the statistics_

---------------------------------------------------------------------------------------------

3.  
#### IN-ORDER CPU's



