#### Main computer hardware components
![[Screenshot 2026-09-04 at 13.02.28.png|467]]
e.g. `a = x + y`
1. Code instruction copied from RAM to a CPU register
2. Decodes as add instruction
3. Copies values of x and y from RAM into other CPU registers
4. Performs calculation, storing result in another CPU register
5. Copies value from that register to RAM

#### Operating system 
![[Screenshot 2026-09-04 at 13.06.33.png|660]]
e.g. Windows, Linux, MacOS
It manages the computer's resources, it handles the sharing of these resources
- Insulates applications both from the hardware and also from each other
- Components: kernel, the network stack, the filesystem, a hardware abstraction layer
- OS provides programmers with *system libraries* to perform OS-level operations, e.g. using network connection, allocating memory, managing files, using peripherals(USB, Bluetooth, etc.)

#### Linux
Kernel: core
- OS components are not part of the kernel. (e.g. shell命令行, GUI, Utilities命令行工具, bootloader(load the OS kernel into the RAM and initialize it))

Most Linux distributions are a combination of Linux kernel and utilities(tools) from the GNU project.

Libraries: common data and instructions shared.
Batch processing: multiple input at one time.
Multiprogramming: run multiple programs at the same time by switching between them.


#### File System (FS)

![[Screenshot 2026-09-05 at 10.49.26.png|354]]

![[Screenshot 2026-09-05 at 10.50.26.png|700]]
==*Note: dir can be leaves (the folders can be empty)*==

##### How to refer to a location in space
- Absolute path: full address 
	- starts from root file, includes "/"
- Relative path: directions from current location 
	- does not begin with '/'
	- .. --> *parent directory*

File/dir related command lines
```bash
touch #create file
mkdir #make a directory
rm    #remove file
rm -r #remove a directory
mv    #move a fily/directory
cp    #copy a file
cp -r #copy a directory
```



