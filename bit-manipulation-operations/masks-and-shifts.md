# masks-and-shifts

---

#  Introduction

In embedded systems, **bit masks and shift operations** are used to manipulate specific bits inside registers or variables.

They are essential for:

* controlling hardware registers (GPIO, UART, SPI, I2C)
* extracting or setting specific fields
* memory-efficient flag handling
* low-level firmware development

---

#  Definition

* **Masking** → selecting or modifying specific bits using bitwise operations
* **Shifting** → moving bits left or right to position them correctly

---

#  Why Masks & Shifts Are Important

* direct hardware control
* fast execution (single CPU instructions)
* no extra memory usage
* precise bit-level manipulation
* widely used in microcontroller registers

---

#  Basic Concept

```text id="flow1"
Value (register)
     |
Apply mask
     |
Select specific bits
     |
Shift if needed
     |
Get or set target field
```

---

#  Bit Mask Example

```text id="bin1"
Value:  11010110
Mask:   00001111
Result: 00000110
```

---

#  1. What is a Mask?

A mask is a binary pattern used to **select or modify specific bits**.

---

## Example:

```c id="ex1"
int value = 0b11010110;
int mask  = 0b00001111;

int result = value & mask;
```

---

#  2. Setting Bits (Using OR)

## Turn ON specific bits

```c id="set1"
value |= (1 << n);
```

---

## Example:

```c id="ex2"
int value = 0;

value |= (1 << 3); // set bit 3
```

```text id="set2"
00000000 → 00001000
```

---

#  3. Clearing Bits (Using AND + NOT)

## Turn OFF specific bits

```c id="clear1"
value &= ~(1 << n);
```

---

## Example:

```c id="ex3"
int value = 0b11111111;

value &= ~(1 << 2);
```

```text id="clear2"
11111111 → 11111011
```

---

#  4. Toggling Bits (Using XOR)

## Flip bit state

```c id="toggle1"
value ^= (1 << n);
```

---

## Example:

```c id="ex4"
int value = 0b00001000;

value ^= (1 << 3);
```

```text id="toggle2"
00001000 → 00000000
```

---

#  5. Extracting Bits (Masking)

## Get specific field

```c id="extract1"
field = (value & mask);
```

---

## Example:

```c id="ex5"
int value = 0b11010110;
int mask  = 0b00001111;

int result = value & mask;
```

---

#  6. Shifting Bits (<< and >>)

---

## Left Shift (<<)

```text id="ls1"
Moves bits left → multiplies by 2
```

```c id="ex6"
int x = 1;
x = x << 3;
```

```text id="ls2"
00000001 → 00001000
```

---

## Right Shift (>>)

```text id="rs1"
Moves bits right → divides by 2
```

```c id="ex7"
int x = 8;
x = x >> 2;
```

```text id="rs2"
00001000 → 00000010
```

---

#  Mask + Shift Working Flow

```text id="flow2"
Raw Register Value
        |
Apply Mask
        |
Isolate Bits
        |
Shift to align
        |
Final Field Value
```

---

#  Embedded Register Example

```c id="reg1"
#define REGISTER (*(volatile int*)0x40020000)

// Set bit 5
REGISTER |= (1 << 5);

// Clear bit 5
REGISTER &= ~(1 << 5);

// Toggle bit 5
REGISTER ^= (1 << 5);
```

---

#  Real Embedded Example

## GPIO Control

```c id="gpio1"
#define LED_PIN (1 << 2)

PORT |= LED_PIN;   // LED ON
PORT &= ~LED_PIN;  // LED OFF
```

---

## Extract Status Bits

```c id="ex8"
int status = 0b10110100;

int errorCode = (status & 0b11110000) >> 4;
```

---

#  Bit Field Extraction Diagram

```text id="diag1"
Status:  10110100
Mask:    11110000
Result:   10110000 → shift → 00001011
```

---

#  Common Mask Patterns

---

## 1. Single Bit Mask

```c id="mask1"
1 << n
```

---

## 2. Multiple Bits Mask

```c id="mask2"
0b00001111
```

---

## 3. Clear Mask

```c id="mask3"
~(1 << n)
```

---

#  Key Concepts

---

## 1. Mask = Filter

Selects bits

---

## 2. Shift = Position adjuster

Moves bits into correct place

---

## 3. Combine both = Field extraction

---

# ⚠ Common Mistakes

---

## 1. Missing parentheses

```c id="m1"
x & 1 << 2   //  wrong
```

Correct:

```c id="m1fix"
x & (1 << 2)
```

---

## 2. Wrong mask value

---

## 3. Shifting beyond bit width

---

## 4. Signed shift issues

---

#  Mask vs Shift vs Bitwise Ops

| Concept     | Purpose     |
| ----------- | ----------- |
| Mask        | Select bits |
| Shift       | Move bits   |
| Bitwise ops | Modify bits |

---

