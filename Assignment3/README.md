### **CMPE283 Assignment 3**

### **Goal**

Modify the CPUID emulation code in KVM to report back additional information when a special CPUID “leaf function” is called
- For CPUID leaf function %eax=0x4FFFFFFE:
    - Return the number of exits for the exit number provided (on input) in %ecx
        - This value should be returned in %eax
    - For leaf nodes 0x4FFFFFFE, if %ecx (on input) contains a value not defined by the SDM, return 0 in all %eax, %ebx, %ecx registers and return 0xFFFFFFFF in %edx. For exit types not enabled in KVM, return 0s in all four registers.

### **Team Members**

Self

### **Implementation Steps**

1. Have a working environment from Assignment 2. If needed follow the steps to set it up from https://github.com/nakul32430/CMPE283_Assignments/tree/main/Assingment2

### **Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?**



### **Output File**


### **Issues faced**
