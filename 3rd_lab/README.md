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


