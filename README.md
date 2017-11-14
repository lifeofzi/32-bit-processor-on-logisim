<span id="_Toc321147149" class="anchor"><span id="_Toc318188227"
class="anchor"><span id="_Toc318188327" class="anchor"><span
id="_Toc318189312" class="anchor"><span id="_Toc321147011"
class="anchor"></span></span></span></span></span><img src="./media/image1.JPG" width="432" height="448" />

32-bit Processor Design

Zaman Ishtiyaq | 15CS01043 | Autumn Semester 2017

*Contents*

[Overall Architecture](#overall-architecture)

[Instruction Format](#instruction-format)

[Instruction Set](#instruction-set)

[Components of Processor](#components-of-the-processor)

[Running an Example](#running-an-example)

Overall Architecture
====================

| 1.  General purpose registers    | 32                                  |
|----------------------------------|-------------------------------------|
| 1.  Clock cycles per instruction | 4                                   |
| 1.  Instructions                 | 8                                   |
| 1.  Memory                       | R.A.M (18-bit Address &32-bit Data) |
| 1.  Special Registers            | RA, RB, RC, RZ, RY                  |

Instruction Format
==================

> OOO AAAAA BBBBB XXXXXXXXXXXXXXXXXXX

| OOO                   | OP-CODE   |
|-----------------------|-----------|
| AAAAA                 | RA        |
| BBBBB                 | RB        |
| XXXXXXXXXXXXXXXXXXX   | IMMEDIATE |

Instruction Set
===============

| **OP-Code** | **Instruction**           | **RTN**                       |
|-------------|---------------------------|-------------------------------|
| 000         | LOAD RA, RB, IMMEDIATE    | RB \[ \[RA\]+IMMEDIATE \]     |
| 001         | STORE\* RA, RB, IMMEDIATE | \[RB\] \[ \[RA\] +IMMEDIATE\] |
| 010         | MOV RA, RB                | RB \[RA\]                     |
| 011         | JUMP RA, RB, IMMEDIATE    | PC IMMEDIATE                  |
| 100         | ADD RA, RB                | RB \[RA\] + \[RB\]            |
| 101         | SUBTRACT RA, RB           | RB \[RA\] - \[RB\]            |
| 110         | MULTIPLY RA, RB           | RB \[RA\] \* \[RB\]           |
| 111         | DIVIDE RA, RB             | RB \[RA\] / \[RB\]            |

\* STORE can only write to the RAM so the IMMEDTIATE value should be of
the form **1**XXXXXXXXXXXXXXXXXX as Chip-Select has to select RAM
otherwise it will try to write on to the ROM and it will have no effect.

Components of the Processor
===========================

Following are the components along with their figures:

1.  <img src="./media/image1.JPG" width="655" height="675" />***Processor
    Pipeline:***

2.  <img src="./media/image2.jpeg" width="488" height="554" />***Control
    Unit***

    <img src="./media/image3.JPG" width="348" height="289" />

3.  ***Fetch Unit:***

    <img src="./media/image4.JPG" width="499" height="253" />Fetch Unit
    increments the PC or jumps to a new address (Immediate Value) when
    JUMP command is given.

4.  ***Instruction Register and Instruction Decoder:***

    <img src="./media/image5.JPG" width="258" height="171" /><img src="./media/image6.JPG" width="510" height="222" />

5.  ***ALU:***

    Supports Addition, Subtraction, Multiplication and Division.

    <img src="./media/image7.jpg" width="458" height="241" />

6.  ***ROM-RAM:***

    We write our programs on ROM. ROM and RAM are selected based on Chip
    Select which changes on different operations.

    <img src="./media/image8.JPG" width="213" height="175" /><img src="./media/image9.JPG" width="169" height="145" /><img src="./media/image10.JPG" width="155" height="79" />

    <img src="./media/image11.JPG" width="239" height="186" />

<!-- -->

1.  ***Register File (Internal Circuit):***

    <img src="./media/image12.jpg" width="579" height="627" />

2.  3.  <img src="./media/image13.JPG" width="197" height="235" />9.
    ***Reset Button*** Resets Everything except ROM.

Running an Example
==================

Let us perform the following example:

Initially:

1.  Press the RED

2.  Change the Register Values in RF to:

**R0**: 1 **R1**: 3 **R2**: 7 **R3**: 6 **R4**: 2 **R5**: 1 **R6**: 2

1.  Let’s Load the ROM with the following values:

    00000 : 46280000

    00001 : 80080000

    00002 : a3200000

    00003 : c3280000

    00004 : e5080000

    00005 : 0008000a

    00006 : 202c0000

    00007 : 6000000f

    00008 : 00000000

    .

    .

    .

    0000b : 00000011

    .

    .

    .

    0000f : 80080000

    00010 : 80080000

When Executed following happens:

<img src="./media/image14.JPG" width="720" height="115" />Initially the
RF looks like :

**R0**: 1 **R1**: 3 **R2**: 7 **R3**: 6 **R4**: 2 **R5**: 1 **R6**: 2

1.  46280000 in binary is 01000110001010000000000000000000

    i.e. MOV R6, R5

    <img src="./media/image15.JPG" width="139" height="137" />

-   **Stage – 1: Fetch to IR**

    <img src="./media/image16.JPG" width="261" height="211" /><img src="./media/image17.JPG" width="157" height="93" />

-   **Stage – 2: RA gets value from R6**

    <img src="./media/image18.JPG" width="119" height="144" />

    <img src="./media/image19.JPG" width="179" height="184" />RA \[R6\]

-   **Stage – 3: RA gets value from R6**

    <img src="./media/image20.JPG" width="167" height="112" /><img src="./media/image21.JPG" width="129" height="126" />

    RA’s value passes unchanged through ALU to RZ

-   **Stage – 4: RY gets value from RZ**

    <img src="./media/image22.JPG" width="110" height="120" />

    <img src="./media/image23.JPG" width="195" height="88" />

    <img src="./media/image24.JPG" width="155" height="182" />

-   <img src="./media/image25.JPG" width="625" height="94" />**Stage –
    5: R5 gets value from RZ**

    Values Now:

    **R0**: 1 **R1**: 3 **R2**: 7 **R3**: 6 **R4**: 2 **R5**: 2 **R6**:
    2

    And PC is incremented to next instruction :

    <img src="./media/image26.JPG" width="176" height="108" />

1.  80080000 in binary is 100 00000 00001 0000000000000000000

    i.e. ADD R0, R1 or R1 \[R0\] + \[R1\]

-   **Stage – 1: Fetch to IR**

    <img src="./media/image27.JPG" width="235" height="355" />Similar to
    above

-   **Stage – 2: RA, RB get their values from RF**

-   **Stage – 3: ALU performs addition**

-   **Stage – 4: RY gets value from RZ**

-   **Stage -5: R1 gets value from RY and PC++**

    i.e. R1 1 + 3 (=4)

    <img src="./media/image28.JPG" width="497" height="76" />

    Values Now:

    **R0**: 1 **R1**: 4 **R2**: 7 **R3**: 6 **R4**: 2 **R5**: 2 **R6**:
    2

1.  a3200000 in binary is 101 00011 00010 0000000000000000000

    i.e. SUB R3, R4 or R4 \[R3\] - \[R4\]

-   **Stage – 1: Fetch to IR**

    <img src="./media/image29.JPG" width="235" height="335" />

-   **Stage – 2: RA, RB get their values from RF**

-   **Stage – 3: ALU performs Subtraction**

-   **Stage – 4: RY gets value from RZ**

-   **Stage -5: R4 gets value from RY and PC++**

    i.e. R4 6 - 2 (=4)

    <img src="./media/image30.JPG" width="497" height="76" />

Values Now:

**R0**: 1 **R1**: 4 **R2**: 7 **R3**: 6 **R4**: 4 **R5**: 2 **R6**: 2

1.  c3280000 in binary is 110 00011 00101 0000000000000000000

    i.e. MUL R3, R5 or R5 \[R3\] \* \[R5\]

-   **Stage – 1: Fetch to IR**

    <img src="./media/image31.JPG" width="235" height="334" />

-   **Stage – 2: RA, RB get their values from RF**

-   **Stage – 3: ALU performs Multiplication**

-   **Stage – 4: RY gets value from RZ**

-   **Stage -5: R5 gets value from RY and PC++**

    i.e. R5 6 \* 2 (=12)

    <img src="./media/image32.JPG" width="497" height="72" />

Values Now:

**R0**: 1 **R1**: 4 **R2**: 7 **R3**: 6 **R4**: 4 **R5**: 12 **R6**: 2

1.  e5080000 in binary is 111 00101 00001 0000000000000000000

    i.e. DIVIDE R5, R1 or R1 \[R5\] / \[R1\]

-   **Stage – 1: Fetch to IR**

-   **Stage – 2: RA, RB get their values from RF**

    <img src="./media/image33.JPG" width="231" height="268" />

-   **Stage – 3: ALU performs Division**

-   **Stage – 4: RY gets value from RZ**

-   **Stage -5: R1 gets value from RY and PC++**

    i.e. R5 12 / 4 (=3)

    <img src="./media/image34.JPG" width="524" height="81" />

Values Now:

**R0**: 1 **R1**: 3 **R2**: 7 **R3**: 6 **R4**: 4 **R5**: 12 **R6**: 2

1.  0008000a in binary is 000 00000 00001 0000000000000001010

    i.e. LOAD R0, R1, \#10 or R1 \[ \[R0\] + 10 \]

-   <img src="./media/image35.JPG" width="279" height="143" />**Stage –
    1: Fetch to IR**

-   **Stage – 2: RA get their values from RF, RB gets IMMEDIATE value**

-   **Stage – 3: ALU performs Addition, RY gets the address to be read
    from**

-   **Stage – 4: RY gets value from the ROM/RAM at address in RY**

-   **Stage -5: R0 gets value from RY and PC++**

    i.e. R0 \[ \[1 + 10\] \] which is 0000b location on ROM and the
    value there is

    <img src="./media/image36.JPG" width="593" height="94" />000000011 ,
    therefore R0 &lt;- 00000011 or 17

Values Now **R0**: 1 **R1**: 17 **R2**: 7 **R3**: 6 **R4**: 4 **R5**: 12
**R6**: 2

1.  202c0000 in binary is 001 00000 00010 1000000000000000000

    i.e. STORE R0, R5, \#0 or \[R0\] + 0 \[R5\] i.e. RAM gets written at
    this location by \[R5\]

-   <img src="./media/image37.JPG" width="211" height="173" />**Stage –
    1: Fetch to IR**

-   **Stage – 2: RA get their values from RF, RB gets IMMEDIATE value**

-   **Stage – 3: ALU performs Addition, RY gets the address to be write
    onto, RM gets value of R5  
    **

-   **Stage – 4: Value of RM is written on the address in RY**

-   <img src="./media/image38.JPG" width="303" height="197" />**Stage
    -5: PC++**

    <img src="./media/image39.JPG" width="156" height="101" /><img src="./media/image40.JPG" width="169" height="97" />

1.  6000000f in binary is 011 00000 00000 00000000000000001111

    i.e. JUMP IMMEDIATE or PC location 0000f on ROM

-   **Stage – 1: Fetch to IR**

    <img src="./media/image41.JPG" width="211" height="120" />

-   **Stage – 2: -**

-   **Stage – 3: MUX-PCSet is Enabled and IMMEDIATE is Selected  
    **

-   **Stage – 4: PC gets value of IMMEDIATE**

-   <img src="./media/image42.JPG" width="238" height="160" />**Stage
    -5: PC++**

    <img src="./media/image43.JPG" width="353" height="176" />

Now the further instructions are executed from this point onwards.
