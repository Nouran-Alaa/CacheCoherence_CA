# CACHE COHERENCE SIMULATION

In this repository we are presenting the Cache Coherence MSI Protocol to analyze how would cache perform under various workloads.

We have studied about different snooping based Cache Coherence Protocols in class. Whenever a processor wants to read or write something, it tries to use its own cache to avoid having to go to the memory each time (as it’s very slow). But, when we have multiple processors, we need to synchronize the caches, so that all processors have a coherent view of memory. For this, one approach is to use a snooping cache, where each cache monitors the memory reads and writes done by other caches and takes some action based on those requests. MSI is one simple choice but there are other protocols too which offer different kinds of benefits under specific workloads - MESI, MOSI, MOESI, etc. 

To simulate the output we are using SMPCache simulator which comes with a pre-configured memory traces and different protocols configurations to be used for the simulation.

#### <ins>The following is the **State Transition Diagram** for MSI Protocol:</ins>

<img src="./assets/image9.png" alt="image-20220522074641709" style="zoom:67%;" />

**<ins>The basic MSI protocol with the Modified, Shared and Invalid states.</ins>**

<img src="./assets/MSI.png" alt="alt text" style="zoom:80%;" />

## Simulator Configuration

1. Open SMPCache simulator and choose `Load Configuration` from **file** menu.
2. On the opened window go to the following path `C:\PROGRAM FILES (X86)\ARCO\SMPCACHE\EXAMPLES\SMP\` and choose `ConfigMSI.cfg` to load the MSI protocol pre-configured files.

<img src="./assets/imag134.png" alt="image-20220522075527134" style="zoom:95%;" />

as seen on the right of this picture, this config contains 2 processes and cache of size 256 Bytes each with a block size of 16 Bytes.

3. Now from **file** menu choose `Open memory traces` and go to this path`C:\PROGRAM FILES (X86)\ARCO\SMPCACHE\EXAMPLES\SMP\` then on top right corner load P0 and P1 with `MSI1.prg`.

<img src="./assets/ima713.png" alt="image-20220522082418713" style="zoom:95%;" />

4. Now your program is ready for simulation and from **View**  menu choose `Cache Evolution` and make sure `Processor cache is 0`

## Simulation Results

> **Accesses number: 1**

<img src="./assets/image-20220522082637698.png" alt="image-20220522082637698" style="zoom:80%;" />

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

<img src="./assets/imag84.png" alt="image-20220522083307284" style="zoom:80%;" />

```
Node P[0] Seek block -> 273
	1.- Reading request (PrRd)
	2.- Hit in cache
```

**State Transition In Cache:**

```
SHARED ---> SHARED
```

------

> **Accesses number: 6**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%206.PNG?raw=true" style="zoom:80%;" /> 

 ```
Node P[0] Seek block -> 273
	1.- Writing request (PrWr)
	2.- Hit in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 273 from main memory
 ```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%206.PNG?raw=true" style="zoom:80%;" /> 

``` 
SHARED ---> MODIFIED
```

------

> **Accesses number: 7**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%207.PNG?raw=true" style="zoom:80%;" /> 

```
Node P[0] Seek block -> 273
	1.- Writing request (PrWr)
	2.- Hit in cache
```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%207.PNG?raw=true" style="zoom:80%;" />

``` 
MODIFIED ---> MODIFIED

MODIFIED ---> INVAILD
```

------

> **Accesses number: 8**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%208.PNG?raw=true" style="zoom:80%;" /> 

```
Node P[1] Seek block -> 273
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 273 from node P1
```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%208.PNG?raw=true" style="zoom:80%;" /> 

```
INVAILD ---> MODIFIED
```

------

> **Accesses number: 9** 

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%209.PNG?raw=true" style="zoom:80%;" /> 

```
Node P[0] Seek block -> 273
	1.- Writing request (PrWr)
	2.- Hit in cache 
```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%209.PNG?raw=true" style="zoom:80%;" />

```
MODIFIED ---> MODIFIED

MODIFIED ---> INVAILD
```

------

> **Accesses number: 10**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%2010.PNG?raw=true" style="zoom:80%;" /> 

```
Node P[1] Seek block -> 273
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 273 from node P1
```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%2010.PNG?raw=true" style="zoom:80%;" /> 

```
INVAILD ---> MODIFIED
```


------

> Accesses number: 11

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%2011.png?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 273
	1.- Reading request (PrRd)
	2.- Hit in cache
```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%2011.png?raw=true" style="zoom:80%;" />

```
MODIFIED ---> MODIFIED

MODIFIED ---> INVAILD
```

------

> **Accesses number: 12**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%2012.PNG?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 273
	1.- Reading request (PrRd)
	2.- Miss in cache
	3.- Bus reading request (BusRd)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 273 from node P1
	6.- Writeback in node P1 block 273
		6a.- Writeback request (BusWb)
		6b.- Transfer of block 273 to main memory
```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%2012.png?raw=true" style="zoom:80%;" />

```
INVAILD ---> SHARED
```

------

> **Accesses number: 13**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%2013.png?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 273
	1.- Reading request (PrRd)
	2.- Hit in cache
```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%2013.png?raw=true" style="zoom:80%;" />

```
SHARED ---> SHARED
```

------

> **Accesses number: 14**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%2014.png?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 273
	1.- Reading request (PrRd)
	2.- Hit in cache
```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%2014.png?raw=true" style="zoom:80%;" />

```
SHARED ---> SHARED
```

------

> **Accesses number: 15**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%2015.png?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 273
	1.- Reading request (PrRd)
	2.- Hit in cache
```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%2015.png?raw=true" style="zoom:80%;" />

```
SHARED ---> SHARED
```

---

> **Accesses number: 16**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/Access_Number%2016.png?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 546
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 546 from main memory
```

**State Transition In Cache:**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/State_Transition%2016.png?raw=true" style="zoom:80%;" />

```
INVAILD ---> MODIFIED
```

***
> **Accesses number: 17**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/17.PNG?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 546
	1.- Writing request (PrWr)
	2.- Hit in cache
```

**State Transition In Cache:**

```
P[0] : MODIFIED ---> MODIFIED
P[1] : MODIFIED ---> INVALID
```
***

> **Accesses number: 18**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/18.PNG?raw=true" style="zoom:80%;" />

```
Node P[1] Seek block -> 546
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P1
	5.- Transfer of block 546 from node P0
```

**State Transition In Cache:**

```
P[1] : INVALID ---> MODIFIED
```

***

> **Accesses number: 19**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/19.PNG?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 546
	1.- Writing request (PrWr)
	2.- Hit in cache
```

**State Transition In Cache:**

```
P[0] : MODIFIED ---> MODIFIED 
P[1] : MODIFIED ---> INVALID
```

***

> **Accesses number: 20**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/20.PNG?raw=true" style="zoom:80%;" />

```
Node P[1] Seek block -> 546
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P1
	5.- Transfer of block 546 from node P0
```

**State Transition In Cache:**

```
P[1] : INVALID ---> MODIFIED
```
***

> **Accesses number: 21**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/21.PNG?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 819
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 819 from main memory
```

**State Transition In Cache:**

```
P[0] : INVALID ---> MODIFIED
P[1] : MODIFIED ---> INVALID
```
***

> **Accesses number: 22**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/22.PNG?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 1092
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 1092 from main memory
```

**State Transition In Cache:**

```
P[0] : INVALID ---> MODIFIED
P[1] : MODIFIED ---> INVALID
```
***

> **Accesses number: 23**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/23.png?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 1365
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 1365 from main memory
```

**State Transition In Cache:**

```
INVALID ---> MODIFIED
MODIFIED ---> INVALID
```
***

> **Accesses number: 24**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/24.png?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 1638
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 1638 from main memory
```

**State Transition In Cache:**

```
INVALID ---> MODIFIED
MODIFIED ---> INVALID
```
***

> **Accesses number: 25**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/25.png?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 1911
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 1911 from main memory
```

**State Transition In Cache:**

```
INVALID ---> MODIFIED
MODIFIED ---> INVALID
```
***

> **Accesses number: 26**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/26.png?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 2184
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 2184 from main memory
```

**State Transition In Cache:**

```
INVALID ---> MODIFIED
MODIFIED ---> INVALID
```
***

> **Accesses number: 27**

<img src="https://github.com/Nouran-Alaa/CacheCoherence_CA/blob/main/assets/27.png?raw=true" style="zoom:80%;" />

```
Node P[0] Seek block -> 2457
	1.- Writing request (PrWr)
	2.- Miss in cache
	3.- Bus exclusive reading request (BusRdX)
	4.- The bus arbiter grants bus to node P0
	5.- Transfer of block 2457 from main memory
```

**State Transition In Cache:**

```
INVALID ---> MODIFIED
MODIFIED ---> INVALID
```
