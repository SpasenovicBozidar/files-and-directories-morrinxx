## 1. FAT Main Memory Requirements
### a) How many blocks does the disk have?
* 262.144.000
### b) How many entries must the FAT have?
* 262.144.000
### c) What size must be a table entry?
* It has to contain reference which tells us what the next block of a file is. We calculate that with: log2(262.144.000)=27.966,
so one entry has to have a size of 32bits
### d) Finally what size is the FAT now?
* 262.144.000 * 32 / 8 = 1.048.576.000 Byte = 1.048gb

## 2. Random Access of Files
Random access to position 107.834.590 in
### a) UFS with blocksize 1 KB
First you have to find the I-Node from the file. Then we have to calculate, where the block is:
* First 10 Blocks are direct blocks:
* A single indirect block contains 1000/8 = 125 re ferences to datablocks
* A double indirect block contains 1000*1000/8 = 125.000 references to datablocks
* A triple indirect block contains 1000*1000*1000/8 = 125.000.000 references to datablocks.

Now we calculate in which of the triple indirect
---TODO---- CALCULATION OF POSITION

### b) FAT32 with a block size of 1 KB
You get the first block-reference of the FAT by the file-name, then u have to jump 107.834.590 times within the FAT to get to the correct block.

## 3. UFS (i-node) File size
### a) 4 KB blocksize:
one block = 4000/32/8 = 1000 block references  
10 * 4kb      +       1000 * 4kb      +      1000 * 1000 * 4kb     +     1000 * 1000 * 1000 * 4kb = 4.004.004.040kb = 4TB

### b) 1 KB blocksize:
one block = 1000/32/8 = 250 block references  
10 * 1kb      +       250 * 1kb      +      250 * 250 * 1kb     +     250 * 250 * 250 * 1kb = 15.687.760kb = 15.7gb

    The file size is four times smaller.

## 4. UFS File size
Maximum file size = 5gb

### a) Will it be sifficient to keep a block size of 512 or do you have to take 1024 bytes? Why?

512Byte = 512/32/8 = 128 references
1024Byte = 1024/32/4 = 256 references

10 x 512Bytes + 128 x 512 Bytes + 128^2 x 512 Bytes + 128^3 x 512 Bytes = 1.082.201.088 Bytes = 1GB

We can not stay with a block size of 512 Byte because the max file size is ~ 1GB

### b) What would change if you estimate 12gb as a max. file size of your multi-media files? Why?

10 * 1024Byte + 256 x 1024Byte + 256^2 x 1024Byte + 256^3 x 1024Byte = 17.247.250.430Bytes = 17.2GB

In bouth cases we need to take 1024Byte block size
