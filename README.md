# CACHE COHERENCE SIMULATIO

In this repository we are presenting the Cache Coherence MSI Protocol to analyze how would cache perform under various workloads.

We have studied about different snooping based Cache Coherence Protocols in class. Whenever a processor wants to read or write something, it tries to use its own cache to avoid having to go to the memory each time (as it’s very slow). But, when we have multiple processors, we need to synchronize the caches, so that all processors have a coherent view of memory. For this, one approach is to use a snooping cache, where each cache monitors the memory reads and writes done by other caches and takes some action based on those requests. MSI is one simple choice but there are other protocols too which offer different kinds of benefits under specific workloads - MESI, MOSI, MOESI, etc. 

To simulate the output we are using SMPCache simulator which comes with a pre-configured memory traces and different protocols configurations to be used for the simulation.

#### Following is the **State Transition Diagram** for MSI Protocol

<img src="H:\Colleage\3\Second Term\Computer Architecture\project\CacheCoherence_CA\assets\image9.png" alt="image-20220522074641709" style="zoom:67%;" />

**The basic MSI protocol with the Modified, Shared and Invalid states.**

<img src="H:\Colleage\3\Second Term\Computer Architecture\project\CacheCoherence_CA\assets\MSI.png" alt="alt text" style="zoom:80%;" />

## Simulator Configuration

1. Open SMPCache simulator and choose `Load Configuration` from **file** menu.
2. On the opened window go to the following path `C:\PROGRAM FILES (X86)\ARCO\SMPCACHE\EXAMPLES\SMP\` and choose `ConfigMSI.cfg` to load the MSI protocol pre-configured files.

<img src="H:\Colleage\3\Second Term\Computer Architecture\project\CacheCoherence_CA\assets\imag134.png" alt="image-20220522075527134" style="zoom:95%;" />

as seen on the right of this picture, this config contains 2 processes and cache of size 256 Bytes each with a bock size of 16 Bytes.

3. Now from **file** menu choose `Open memory traces` and go to this path`C:\PROGRAM FILES (X86)\ARCO\SMPCACHE\EXAMPLES\SMP\` then on top right corner load P0 and P1 with `MSI1.prg`.

<img src="H:\Colleage\3\Second Term\Computer Architecture\project\CacheCoherence_CA\assets\ima713.png" alt="image-20220522082418713" style="zoom:95%;" />

4. Now your program is ready for simulation and from **View**  menu choose `Cache Evolution` and make sure `Processor cache is 1`

## Simulation Results

> **Accesses number: 1**

<img src="H:\Colleage\3\Second Term\Computer Architecture\project\CacheCoherence_CA\assets\image-20220522082637698.png" alt="image-20220522082637698" style="zoom:80%;" />

```
Node P[0] Seek block -> 273
	1.- Reading request (PrRd)
	2.- Miss in cache
	3.- Bus reading request (BusRd)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 273 from main memory
```

**State Transition In Cache:**

```
INVALID ---> SHARED
```

>  **Accesses number: 2, 3, 4, 5**

<img src="H:\Colleage\3\Second Term\Computer Architecture\project\CacheCoherence_CA\assets\imag84.png" alt="image-20220522083307284" style="zoom:80%;" />

```
Node P[0] Seek block -> 273
	1.- Reading request (PrRd)
	2.- Hit in cache
```

**State Transition In Cache:**

```
SHARED ---> SHARED
```

