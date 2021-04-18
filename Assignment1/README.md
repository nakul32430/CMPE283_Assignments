### **CMPE283 Assignment 1**

### **Goal**

Discover VMX features. The following is performed in the module’s main code:
- Read the VMX configuration MSRs to ascertain support capabilities/features
    - Entry / Exit / Procbased / Secondary Procbased / Pinbased controls
- For each group of controls above, interpret and output the values read from the MSR to the system
via printk(..), including if the value can be set or cleared.

### **Implementation Steps**

1. Fork the https://github.com/torvalds/linux
2. Ensure that the forked repo is public
