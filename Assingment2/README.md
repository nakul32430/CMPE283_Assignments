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
    - sudo bash
    - apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev
    - uname -a (kernel version was “5.8.0-50-generic”)
    - cp /boot/config-5.8.0-50-generic ./.config
    - make oldconfig (and then just use the default for everything, don’t change anything – you can do this by holding down enter)
    - make -j 2 && make -j 2 modules && make modules_install && make install (replace 2 with the number of cpus in your vm)
    - reboot
7. After reboot, verified the updated kernel version
    - uname -a (kernel version for my execution was "5.12.0-rc8")
8. Made changes to the following files to modify CPUID emulation code in order to print number of exits and elapsed time
    - cpuid.c in linux/arch/x86/kvm
    - vmx.c in linux/arch/x86/kvm/vmx
9. In vmx.c, following changes were made
    - Declared variables to store exit counter and time elapsed during each exit. Atomic variables were used to handle concurrency
    - The logic to increment the counter and calculate the elapsed time is implemented inside the vmx_handle_exit() function
10. In cpuid.c, following changes were made
    - Inside the function kvm_emulate_cpuid(), conditional statement is introduced when register eax has the value 0x4FFFFFF to store the exit counter, higher 32 bits of elapsed time, and lower 32 bits of elapsed time in registers eax, ebx, and ecx respectively.
11. Rebuilt the kernel using the same make statements as in step 6
12. Rebooted the VM
13. Inside the VM, installed the nested VM using the following steps
    - Ensure the nested virtualization is enabled in the outer VM by running the following command
        - cat /sys/module/kvm_intel/parameters/nested
    - Install virtual manager, qemu, and other dependencies
        - sudo apt install libvirt-clients libvirt-daemon-system ovmf virt-manager qemu-system-x86
    - Set up an inner VM using virtual manager and Ubuntu 20.0.4 ISO from assignment 1
    - Installed CPUID in the inner VM
        - sudo apt-get install cpuid
14. Tested the code using **cpuid -l 0x4FFFFFE** in inner VM

### **Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?**

After the initial VM boot, the number of exits were increasing at a stable rate. There were around 2 million exits on the full VM boot.

### **Output File**

Output file link to go here

### **Issues faced**

Issues faced while performing the activities go here