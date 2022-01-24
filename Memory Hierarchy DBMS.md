![image](https://user-images.githubusercontent.com/53339016/150761079-a9201c73-5e93-4b5f-aa68-2d35de1fff77.png)

**Primary storage:**
* **cache, main memory** - The memory storage that is directly accessible to the CPU comes under this category. CPU's internal memory (registers), fast memory (cache), and main memory (RAM) are directly accessible to the CPU, as they are all placed on the motherboard or CPU chipset
* **very fast access to data**
* **currently used data**
* **volatile** - Primary storage requires continuous power supply in order to maintain its state. In case of a power failure/or the system is restarted, all its data is lost. **Large amounts of data that shouldn't be discarded when the system is restarted => the need for DBMSs that bring data from disks into main memory for processing**


**Secondary storage:**
* **magnetic disks** - Secondary storage devices are used to store data for future use. Secondary storage includes memory devices that are not a part of the CPU chipset or motherboard, for example, magnetic disks.
* disks - sequential, direct access
* **slower storage devices**
* **nonvolatile**
* used as a **main database**
* disks - significantly cheaper than main memory

**Tertiary storage:** Tertiary storage is used to store huge volumes of data. Since such storage devices are external to the computer system, they are the slowest in speed. These storage devices are mostly used to take the back up of an entire system
* **tapes** 
* slowest storage devices
* nonvolatile
* only sequential access
* good for archives, backups
* unsuitable for data that is frequently accessed
* tapes - significantly cheaper than disks

## Magnetic Disks
![image](https://user-images.githubusercontent.com/53339016/150765227-f142a1bd-3dab-4d8e-87d1-3a34ed92cd8d.png)

* Direct access
* extremely used in database applications
* DBMSs - applications don't need to know whether the data is on disk or in main memory

It is composed of: 
* **disk block**
   * sequence of contiguous bytes
   * unit for data storage
   * unit for data transfer (reading data from disk / writing data to disk)
   * reading / writing a block - an input / output (I/O) operation
* **tracks**
   * concentric rings containing blocks, recorded on one or more platters
* **sectors**
   * arcs on tracks
* **platters**
   * single-sided, double-sided (data recorded on one / both surfaces)
* **cylinder**
   * set of all tracks with the same diameter
* **disk heads**
   * one per recorded surface
   * to read / write a block, a head must be on top of the block
   * all disk heads are moved as a unit
   * systems with one active head
* **sector size**
   * characteristic of the disk, cannot be modified
* **block size**
   * multiple of the sector size

DBMSs operate on data when it is in memory. A **block is a unit for data transfer between disk and main memory**. The time to access a desired location:
* main memory - approximately the same for any location
* disk - depends on where the data is stored
* **disk access time:**
   * seek time + rotational delay + transfer time
   * seek time: the time to move the disk head to the desired track (smaller platter size => decreased seek time)
   * rotational delay: the time for the block to get under the head
   * transfer time: the time to read / write the block, once the disk head is positioned over it

The time required for DB operations is dominated by the time taken to transfer blocks between disk and main memory. The goal is to minimize access time. For this purpose, data should be carefully placed on disk. **Records that are often used together should be close to each other**:
* same block
* same track
* same cylinder
* adjacent cylinder

Characteristics of Magnetic Disks:
* storage capacity (e.g., GB)
* platters (number, single-sided or double-sided)
* average / max seek time (ms)
* average rotational delay (ms)
* number of rotations / min
* data transfer rate (MB/s)
* ...
