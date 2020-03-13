## Registers

### X

The **X** register is a general-purpose storage register and can store a number or a
keyword

### T

The **T** register is a general-purpose storage register and can store a number or a
keyword. It can also be the destination for **TEST** instructions, and is the criterion
for conditional jumps (**TJMP** and **FJMP**).

## Hardware Registers

Some hosts running the EXA-VM may provide access to connected hardware through
the use of hardware registers. Valid names for hardware registers are a pound sign ("#")
followed by four characters, such as **#POwR** or **#ENAB**. Depending on the
host's configuration hardware registers may be readable and writable, only readable,
or only writable.
