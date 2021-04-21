### **CMPE283 Assignment 1**

### **Goal**

Discover VMX features in our processor. The following is performed in the module’s main code:
- Read the VMX configuration MSRs to ascertain support capabilities/features
    - Entry / Exit / Procbased / Secondary Procbased / Pinbased controls
- For each group of controls above, interpret and output the values read from the MSR to the system
via printk(..), including if the value can be set or cleared.

### **Team Members**

Self

### **Implementation Steps**

1. Forked the https://github.com/torvalds/linux repo
2. The forked repo is at https://github.com/nakul32430/linux
3. Launched the VM
4. Opened a terminal and cloned the forked repo using "**git clone https://github.com/nakul32430/linux.git**"
5. In a separate terminal installed the necessary packages to build a kernel later on using the following command "**sudo apt-get install libncurses-dev gawk flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf**"
6. Created a new repo in GitHub for all the CMPE283 assignments (https://github.com/nakul32430/CMPE283_Assignments)
6a. Created a new folder "Assignment1" in the repo and added "**Makefile**" and "**cmpe283-1.c**" files provided for the assignment.
7. In a new terminal on the VM, cloned the CMPE283 assignments repo using "**git clone https://github.com/nakul32430/CMPE283_Assignments.git**"
8. This step is more of an explanation on what was done as part of the assignment and can be skipped while replicating the steps to run the program as the file would have all the changes in the repo. The original cmpe283-1.c file had the logic in place to read MSRs for Pin Based controls. Using the _Vol 3 Section 24.6.2_ of Intel SDM, the program was modified to read MSRs for Primary Processor Based and Secondary Processor Based execution control. Using _Vol 3. Section 24.7.1_ and _Section 24.8.1_, the code was modified to read MSRs for Exit Based and Entry Based execution controls respectively.
9. In the terminal under the "Assignment1" folder, ran the "make" command
10. It generated a bunch of files including cmpe283-1.ko
11. Inserted the module using "sudo insmod cmpe283-1.ko" (enter the password for the username when prompted)
12. Executed "dmesg" command on the terminal to see all the kernel outputs
13. In the end, unloaded the module by using "sudo rmmod cmpe283-1"

### **Output File**

https://raw.githubusercontent.com/nakul32430/CMPE283_Assignments/main/Assignment1/dmesg_log.txt

### **Issues faced**

While launching the Ubuntu 20.0.4 based VM using VMWare Workstation 16 Pro, ran into the following issue "VMWare Workstation and Device/Credential Guard are not compatible. VMWare Workstation can be run after disabling Device/Credential Guard". The issue was resolved by following the steps to disable Hyper-V at https://kb.vmware.com/s/article/2146361