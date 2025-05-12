# ee2003-assignment-7-solved
**TO GET THIS SOLUTION VISIT:** [EE2003 # Assignment 7 Solved](https://www.ankitcodinghub.com/product/ee2003-assignment-7-solved/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;90771&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;1&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (1 vote)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;EE2003 # Assignment 7 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (1 vote)    </div>
    </div>
# Assignment 7

IO interfacing

## Goals

– Implement aa simple output peripheral and use it to display text and numbers

## Given

– This builds on the single cycle peripheral you have already made for A6. Use your code for that

– The `compile` folder contains scripts and a sample C code that can print characters by calling the `outbyte` function

– You need to fill in the `outbyte` function appropriately so that your code will invoke your peripheral for display

## Details on the assignment

At this point (after A6) you should have a complete working single cycle peripheral that is capable of executing all the RV32I instructions (barring possibly the `fence` instructions). Now you need to create a simple peripheral, and memory map it to a suitable location.

Your peripheral will need to respond to read/write requests on specific addresses, and for this, you should choose addresses that are NOT part of the DMEM. The `biu` or *Bus Interface Unit* module is responsible for taking the addresses sent by the CPU and decoding whether they are meant for the DMEM or the peripheral. You can choose addresses as you like, but will need to update them in the C code as well as the Verilog.

### Memory Mapped Read/Write

The peripheral you will create will be *memory mapped* – this is done by part of the decoding in the BIU, so that the peripheral itself does not care at which address it is placed. Only the BIU and the C code need to be aware of this.

The C code itself can then directly read or write, but needs to know which address to deal with. An example is given in the `_outbyte` function in the sample code:

“`c

#define OUTPERIPH_BASE 0x34560

#define OUTPERIPH_WRITE_OFFSET 0x00

#define OUTPERIPH_READSTATUS_OFFSET 0x04

void _outbyte(int c)

{

int *p; // Pointer to integer

p = (OUTPERIPH_BASE + OUTPERIPH_WRITE_OFFSET); // Set pointer value directly

(*p) = c; // Write the value to the address

}

“`

The basic idea in the above code is that we make clever use of *pointers* in C: a pointer is just a regular integer-like value that contains an address. In our case, we directly store the address (`0x34560` in our case – this is a completely arbitrary choice – you just need to make sure it is outside the range of DMEM, otherwise the BIU may make parts of the DMEM inaccessible to the CPU, or the peripheral may not be accessible (memory shadowing)).

The generated code is:

“`asm

00000018 &lt;_outbyte&gt;:

18: fd010113 addi x2,x2,-48

1c: 02812623 sw x8,44(x2)

20: 03010413 addi x8,x2,48

24: fca42e23 sw x10,-36(x8)

28: 000347b7 lui x15,0x34

2c: 56078793 addi x15,x15,1376 # 34560 &lt;__global_pointer$+0x323ac&gt;

30: fef42623 sw x15,-20(x8)

34: fec42783 lw x15,-20(x8)

38: fdc42703 lw x14,-36(x8)

3c: 00e7a023 sw x14,0(x15)

40: 00000013 addi x0,x0,0

44: 02c12403 lw x8,44(x2)

48: 03010113 addi x2,x2,48

4c: 00008067 jalr x0,0(x1)

“`

As can be seen, the address (`0x34560`) gets loaded into `x15` through a combination of `lui` and `addi`. Once that is done, the `sw` instruction on line `3c` can be used to write the value into the peripheral. Similar code, but reading from the pointer, can be used to read back the status register.

### Test cases

For this example, you will need to also modify some of the code, so only a single test case has been given as a C file. Other tests will be generated and uses separately.

The code computes a Fibonacci series value, and prints an appropriate message if the value is correct. The test bench will need to run for enough cycles to complete the required functionality, but this will depend on the code itself, so cannot be known in advance.

Once you have filled in the following files:

– biu.v

– outperiph.v

– compile/outbyte.c

you should be able to use the `run.sh` script to compile and run your code through your CPU.

#
