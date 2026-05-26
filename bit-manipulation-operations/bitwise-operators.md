# bitwise-operators

---

#  Introduction

Bitwise operators in C/C++ are used to perform operations **directly on individual bits of data**.

In embedded systems, they are heavily used for:

* register manipulation
* peripheral control (GPIO, UART, SPI, I2C)
* flag handling
* performance optimization
* memory-efficient programming

---

#  Definition

Bitwise operators operate on **binary representation of integers**, manipulating bits instead of values.

---

#  Why Bitwise Operators Are Important in Embedded

* direct hardware control
* fast execution (single CPU instruction)
* memory-efficient flag storage
* no function overhead
* used in microcontroller registers

---

#  Binary Representation Example

```text id="bin1"
Decimal: 5
Binary : 00000101

Decimal: 3
Binary : 00000011
```

---

#  Bitwise Operators in C/C++

| Operator    | Name         | Symbol |
| ----------- | ------------ | ------ |
| AND         | Bitwise AND  | &      |
| OR          | Bitwise OR   | |      |
| XOR         | Exclusive OR | ^      |
| NOT         | Complement   | ~      |
| Left Shift  | Shift left   | <<     |
| Right Shift | Shift right  | >>     |

---

#  1. Bitwise AND (&)

##  Definition:

Returns 1 only if both bits are 1.

---

## Example:

```c id="ex1"
int a = 5;   // 0101
int b = 3;   // 0011

int c = a & b;
```

```text id="and1"
0101
0011
----
0001  → 1
```

---

## Embedded Use Case:

* checking if a pin is HIGH

```c id="gpio1"
if (PORT & (1 << 2)) {
    // Pin 2 is HIGH
}
```

---

#  2. Bitwise OR (|)

##  Definition:

Returns 1 if at least one bit is 1.

---

## Example:

```c id="ex2"
int a = 5;  // 0101
int b = 3;  // 0011

int c = a | b;
```

```text id="or1"
0101
0011
----
0111 → 7
```

---

## Embedded Use Case:

* setting a bit (turn ON pin)

```c id="gpio2"
PORT |= (1 << 3); // Set pin 3
```

---

#  3. Bitwise XOR (^)

##  Definition:

Returns 1 if bits are different.

---

## Example:

```c id="ex3"
int a = 5; // 0101
int b = 3; // 0011

int c = a ^ b;
```

```text id="xor1"
0101
0011
----
0110 → 6
```

---

## Embedded Use Case:

* toggle a bit

```c id="gpio3"
PORT ^= (1 << 2); // Toggle pin 2
```

---

#  4. Bitwise NOT (~)

##  Definition:

Inverts all bits.

---

## Example:

```c id="ex4"
int a = 5; // 00000101
int c = ~a;
```

```text id="not1"
00000101
--------
11111010
```

---

## Embedded Use Case:

* clearing bits using mask logic

---

#  5. Left Shift (<<)

##  Definition:

Shifts bits left → multiplies by 2

---

## Example:

```c id="ex5"
int a = 3; // 00000011

int c = a << 1;
```

```text id="ls1"
00000011 → 00000110 = 6
```

---

## Embedded Use Case:

* setting bit position

```c id="gpio4"
PORT = (1 << 5); // activate pin 5
```

---

#  6. Right Shift (>>)

##  Definition:

Shifts bits right → divides by 2

---

## Example:

```c id="ex6"
int a = 8; // 00001000

int c = a >> 1;
```

```text id="rs1"
00001000 → 00000100 = 4
```

---

#  Bit Manipulation Diagram

```text id="diag1"
Bit position:
7 6 5 4 3 2 1 0
0 0 1 0 1 0 0 1
```

---

#  Embedded Register Example

```c id="reg1"
#define GPIO (*(volatile int*)0x40020000)

GPIO |= (1 << 0);  // Set bit 0
GPIO &= ~(1 << 0); // Clear bit 0
GPIO ^= (1 << 0);  // Toggle bit 0
```

---

# ⚙ Bit Manipulation Operations

---

## 1. Set Bit

```c id="set1"
x |= (1 << n);
```

---

## 2. Clear Bit

```c id="clear1"
x &= ~(1 << n);
```

---

## 3. Toggle Bit

```c id="toggle1"
x ^= (1 << n);
```

---

## 4. Check Bit

```c id="check1"
if (x & (1 << n)) {
    // bit is 1
}
```

---

#  Real Embedded Example

## LED Control

```c id="led1"
#define LED_PIN (1 << 2)

PORT |= LED_PIN;   // ON
PORT &= ~LED_PIN;  // OFF
```

---

#  Advantages

* very fast operations
* hardware-level control
* memory efficient
* no function overhead
* essential for embedded systems

---

#  Common Mistakes

---

## 1. Confusing OR and XOR

```text id="m1"
| vs ^
```

---

## 2. Not using parentheses

```c id="m2"
x & 1 << 2   //  wrong
```

Correct:

```c id="m2fix"
x & (1 << 2)
```

---

## 3. Shifting beyond size

---

## 4. Signed shift issues

---

#  Bitwise vs Logical Operators

| Feature   | Bitwise            | Logical    |     |   |   |
| --------- | ------------------ | ---------- | --- | - | - |
| Works on  | Bits               | Boolean    |     |   |   |
| Operators | &,                 | , ^        | &&, |   |   |
| Use case  | Embedded registers | Conditions |     |   |   |

---

