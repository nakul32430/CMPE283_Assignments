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

1. Have a working environment from Assignment2. If needed follow the steps to set it up from https://github.com/nakul32430/CMPE283_Assignments/tree/main/Assingment2
2. Made changes to the following files to modify CPUID emulation code in order to print the number of exits for the provided exit number. Special cases per the requirements are also handled
    - cpuid.c in linux/arch/x86/kvm
    - vmx.c in linux/arch/x86/kvm/vmx
3. In vmx.c, following changes were made
    - Declared an array to store exit counter for the corresponding exit type. Atomic variables were used to handle concurrency
    - The logic to increment the counter based on the basic exit reason is implemented inside the vmx_handle_exit() function
    - The actual implementation of the changes can be found at https://github.com/nakul32430/CMPE283_Assignments/blob/main/Assignment3/vmx.c
4. In cpuid.c, following changes were made
- Inside the function kvm_emulate_cpuid(), conditional statement is introduced when register eax has the value 0x4FFFFFFE with the following logic
    - if exit numbers are 35, 38, 42, 65 and outside the range of 0-68 in the ecx register that means they are not defined in the SDN. For such scenario, eax, ebx, ecx is set to 0 and edx to 0xFFFFFFF
    - if exit numbers are 3, 4, 5, 6, 11, 16, 17, 33, 34, 51, 63, 64, and 66 in the ecx register that means they are not enabled in the KVM. For such scenario, eax, ebx, ecx, and edx is set to 0
    - for all the exit numbers store the value of exit counter in eax
    - The actual implementation of the changes can be found at https://github.com/nakul32430/CMPE283_Assignments/blob/main/Assignment3/cpuid.c

### **Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?**

After the initial VM boot, the number of exits were increasing at a stable rate. There were around 2 million exits on the full VM boot.

### **Of the exit types defined in the SDM, which are the most frequent? Least?**

Based on the changes made, following was the observation.

- The most frequent exit types
    - External Interrupt
    - EPT Violation
    - HLT

- The least frequent exit types
    - MOV DR
    - WBINVD

### **Output File**

All the output files are located at https://github.com/nakul32430/CMPE283_Assignments/tree/main/Assignment3/Output%20files

### **Issues faced**

Initially faced issue in identifying the exits not enabled in KVM but was clarified by the Professor in a session
