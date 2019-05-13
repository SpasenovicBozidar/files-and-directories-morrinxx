## 1. FAT Main Memory Requirements
### a) How many blocks does the disk have?
* 250.000.000
### b) How many entries must the FAT have?
* 250.000.000
### c) What size must be a table entry?
* It has to contain one integer which tells us what the next block of a file is, so 8 byte.
### d) Finally what size is the FAT now?
* 250.000.000 * 8 = 2.000.000.000 Byte = 2 gb

## 2. Random Access of Files
Random access to position 107.834.590 in
### a) UFS with blocksize 1 KB
First you have to find the I-Node from the file. Then we have to calculate, where the block is:
* First 10 Blocks are direct blocks:
* A single indirect block contains 1000/8 = 125 references to datablocks
* A double indirect block contains 1000*1000/8 = 125.000 references to datablocks
* A triple indirect block contains 1000*1000*1000/8 = 125.000.000 references to datablocks.

Now we calculate in which of the triple indirect
---TODO---- CALCULATION OF POSITION

### b) FAT32 with a block size of 1 KB
You get the first block-reference of the FAT by the file-name, then u have to jump 107.834.590 times within the FAT to get to the correct block.

## 3. UFS (i-node) File size
### a) 4 KB blocksize:
10 * 4kb      +       250 * 4kb      +      250 * 250 * 4kb     +     250 * 250 * 250 * 4kb = 62.751.040kb = 62.8gb

### b) 1 KB blocksize:
10 * 1kb      +       250 * 1kb      +      250 * 250 * 1kb     +     250 * 250 * 250 * 1kb = 15.687.760kb = 15.7gb

    The file size is four times smaller.

## 4. UFS File size
Maximum file size = 5gb

### a) Will it be sifficient to keep a block size of 512 or do you have to take 1024 bytes? Why?

We can stay with a block-size of 512 bytes, because the max file-size then would be 7.84gb.

### b) What would change if you estimate 12gb as a max. file size of your multi-media files? Why?

12gb is more than our max. file size, so we have to change to a block size of 1024 bytes. Then our max. file size will increace to 15.7gb.
