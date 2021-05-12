### **CMPE283 Assignment 4**

### **Goal**

To illustrate the difference in performance when using nested paging versus shadow paging, and to illustrate the different exit frequencies and types.

### **Team Members**

Self

### **Implementation Steps**

1. Have a working environment from Assignment3. If needed follow the steps to set it up from https://github.com/nakul32430/CMPE283_Assignments/tree/main/Assignment3
2. Boot the nested (inner) VM
3. Run the sequence of below statement with value of argument s from 0 to 68
    - cpuid -l 0x4FFFFFFE -s <exit number>
4. Record the frequency of exits for each exit number to a file using below command
    - dmesg | grep -i 'CPUID(0x4FFFFFFE)' > filename.txt
5. Shutdown the inner VM
6. On the running VM, navigate to the path /lib/modules/<version of the kernel>/kernel/arch/x86/kvm. In my case the version of the kernel was 5.12.0-rc8+
7. Remove the 'kvm-intel' module by executing the below command
    - sudo rmmod kvm-intel
8. Reload the kvm-intel module with the parameter ept=0 (this will disable nested paging and force KVM to use shadow paging instead). Run the below command
    - sudo insmod kvm-intel.ko ept=0
9. Repeat steps 2 to 4

### **What did you learn from the count of exits? Was the count what you expected? If not, why not?**


### **What changed between the two runs (ept vs no-ept)?**


### **Output File**


### **Issues faced**

None
