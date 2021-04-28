### **CMPE283 Assignment 2**

### **Goal**

Modify the CPUID emulation code in KVM to report back additional information when a special CPUID “leaf function” is called
- For CPUID leaf function %eax=0x4FFFFFFF:
    - Return the total number of exits (all types) in %eax
    - Return the high 32 bits of the total time spent processing all exits in %ebx
    - Return the low 32 bits of the total time spent processing all exits in %ecx
        - %ebx and %ecx return values are measured in processor cycles

### **Team Members**

Self

### **Implementation Steps**

1. Forked the https://github.com/torvalds/linux repo
2. The forked repo is at https://github.com/nakul32430/linux
3. Launched the VM
4. Opened a terminal and cloned the forked repo using "**git clone https://github.com/nakul32430/linux.git**"
5. In a separate terminal installed the necessary packages to build a kernel later on using the following command "**sudo apt-get install libncurses-dev gawk flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf**"
6. Executed the below set of commands to build the kernel very first time (it took several hours to completely build it)
    a. sudo bash
    b. apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev
    c. uname -a (kernel version was “5.8.0-50-generic”)
    d. cp /boot/config-5.8.0-50-generic ./.config
    e. make oldconfig (and then just use the default for everything, don’t change anything – you can do this by holding down enter)
    f. make -j 2 && make -j 2 modules && make modules_install && make install (replace 2 with the number of cpus in your vm)
    g. reboot


### **Output File**

<<Output file link to go here>>

### **Issues faced**

<<Issues faced while performing the activities go here>>