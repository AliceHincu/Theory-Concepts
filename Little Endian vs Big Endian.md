# What Is Little-Endian And Big-Endian Byte Ordering?
Computers store data in memory in binary. One thing that is often overlooked is the formatting at the byte level of this data. This is called endianness and it refers to the ordering of the bytes.

**Specifically, little-endian is when the least significant bytes are stored before the more significant bytes, and big-endian is when the most significant bytes are stored before the less significant bytes.**

When we write a number (in hex), i.e. 0x12345678, we write it with the most significant byte first (the 12 part). In a sense, big-endian is the “normal” way to write things down.

# Why This Is Important?
If we were to store ```0x12345678``` into memory (Note that each 2 hex letters represent 1 byte):
* using **little-endian** we would get the following. ```78 56 34 12```
* using **big-endian** we would get:  ```12 34 56 78```

In the end, that is why endianness is important; because not knowing how data is stored would lead to communicating different values.

**For example, all x86_64 processors (Intel/AMD) use little-endian while IP/TCP uses big-endian. This means that in order for you to use the Internet, your computer has to account for the difference in endianness.**


# So Why Does Everyone Have It Backwards?
However counter-intuitive it might seem at first, there are valid reasons why little-endian is used over big-endian. The reason for the widespread use of little-endian is not because of the ease of user understanding (as you might have figured out), but rather for ease of the computer. Let’s take a look at why. We will use this 8-byte value ```0x0000000000000042```. 
* When we store it in little-endian we have the following: ```0x00: 42 00 00 00 00 00 00 00```
* When we store it in in big-endian we would get: ```0x00: 00 00 00 00 00 00 00 42```

Now let’s say we were to run the following code:
```c
// In the case of 64 bit compilers, long long is the same size as long. They are both 8 bytes.
unsigned long long x = 0x0000000000000042;
unsigned long long * x_p = &x;
unsigned int * y_p = (unsigned int *)x_p;
unsigned int y = *y_p;
printf("y = %#.8x\n", y); // prints in hex with '0x' and with all leading zeros
```
We are doing something called a **pointer down cast**. We don’t change anything in memory, just how the processor reads from memory. An important thing to notice is that x_p and y_p will have the same value (they point to the same location). We will say they both point to 0x00.

When we run this, we will get two very different results depending on what endianness the processor uses. First, let’s assume that we are using an x86_64 processor (i.e. **little-endian**). We get exactly what you would expect to get: y = 0x00000042. This is because when we re-interpret the memory in 4-byte chunks and get the following:
```
0x00: 42 00 00 00
0x04: 00 00 00 00
```
Now, when we only grab 4 bytes at memory location 0x00 we get the 4 least significant bytes from the original 8-byte value. Feel free to try this out on your computer.

**Big-endian**, as you may expect, behaves very differently. Imagine that we ran this code on a big-endian processor instead. We would get: y = 0x00000000. Again, if we re-interpret the memory in 4-byte chunks we will see the reason why this is the case.
```
0x00: 00 00 00 00
0x04: 00 00 00 42
```
The y_p pointer (0x00 in our case) points to 0x00000000.

Getting code to run this in big-endian is hard because most processors are either little-endian or bi-endian. However, you can change the code by adding byte swaps to “emulate” big-endian.
