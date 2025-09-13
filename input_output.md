# I/O devices
**why I/O is important**
- A program without an input always produces the same input .
- A program without an output , what is the purpose of running it 
 
 ### Canonical Devices 
 A canonical device is a conceptual model used in operating systems to illustrate the standard components and interfaces of hardware devices. It consists of two key parts:

1. **Hardware Interface:** The standardized protocol and control registers that allow the operating system to interact with the device. This includes:

* Command registers :  to tell , the device to perform a certain tasks
* Status registers : which can read the current status of device
* Data registers or buffers : to pass data to the device or to get data from the device

By reading or writing this registers OS can control the device behavior 


2. **Internal Implementation:** The device-specific hardware and firmware that implements the actual functionality, which may include:

 * Specialized chips and circuits
 * Device firmware (software embedded in the hardware)
 * Internal processors and memory
 * Implementation-specific logic

 ### Steps in Protocol
 1. the OS waits until the device is ready to receive a command by repeatedly reading the status register;we call this polling the device (basically, just asking it what is going on)
 ```
 Wait for Readiness of device
 While (STATUS == BUSY)
  ; // Polling loop waiting until device is free
 ```
 2. the OS sends some data down to the data register; one can imagine that if this were a disk, for example, that multiple writes would need to take place to transfer a disk block (say 4KB) to the device.
 ```
Transfer Data:
Write data to DATA register
 ```
3. The OS writes a command to the command register; doing so implicitly lets the device know that
both the data is present and that it should begin working on the command
```
Issue Command:
Write command to COMMAND register
```
4. The OS waits for the device to finish by again polling it in a loop, waiting to see if it is finished (it may then get an error code to indicate success or failure).
```
Wait for Completion:
While (STATUS == BUSY); // Polling loop waiting until device finishes
```
**Key Limitations:**

* Polling Inefficiency: The CPU continuously checks device status, wasting processing time instead of doing useful work
* CPU-Intensive Data Transfer: Using the main CPU for data movement (programmed I/O) is inefficient for large transfers
* Blocking Operation: The entire process blocks while waiting for the device to complete