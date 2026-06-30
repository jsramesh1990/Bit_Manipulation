# Bitwise Operators in C - Complete Guide

## Table of Contents

1. [Introduction](#1-introduction)
2. [Definition](#2-definition)
3. [Why Bitwise Operators Are Important](#3-why-bitwise-operators-are-important)
4. [Binary Representation](#4-binary-representation)
5. [Bitwise Operators in C](#5-bitwise-operators-in-c)
6. [Bitwise AND (&)](#6-bitwise-and-)
7. [Bitwise OR (|)](#7-bitwise-or-)
8. [Bitwise XOR (^)](#8-bitwise-xor-)
9. [Bitwise NOT (~)](#9-bitwise-not-)
10. [Left Shift (<<)](#10-left-shift-)
11. [Right Shift (>>)](#11-right-shift-)
12. [Bit Manipulation Operations](#12-bit-manipulation-operations)
13. [Embedded Register Example](#13-embedded-register-example)
14. [Real Embedded Example - LED Control](#14-real-embedded-example---led-control)
15. [Bitwise vs Logical Operators](#15-bitwise-vs-logical-operators)
16. [Common Mistakes](#16-common-mistakes)
17. [Real-Time Examples](#17-real-time-examples)
18. [Advantages](#18-advantages)
19. [Quick Revision](#19-quick-revision)
20. [Interview Questions](#20-interview-questions)
21. [Conclusion](#21-conclusion)

---

## 1. Introduction

### What Are Bitwise Operators?

Bitwise operators in C are used to perform operations **directly on individual bits of data**. They work on the binary representation of integers, manipulating bits instead of values.

### Why They Matter

In embedded systems programming, bitwise operators are essential for:
- Register manipulation
- Peripheral control (GPIO, UART, SPI, I2C)
- Flag handling
- Performance optimization
- Memory-efficient programming

### Simple Example

```
Decimal: 5  → Binary: 0101
Decimal: 3  → Binary: 0011

Bitwise AND: 0101 & 0011 = 0001 (1)
Bitwise OR:  0101 | 0011 = 0111 (7)
Bitwise XOR: 0101 ^ 0011 = 0110 (6)
```

---

## 2. Definition

### Formal Definition

**Bitwise operators** operate on the binary representation of integers, performing operations bit by bit.

### Simple Definition

```
Bitwise Operators = Operations on individual bits
```

### Key Points

- Work on integer data types
- Operate at bit level
- Direct hardware manipulation
- Very fast execution
- Essential for embedded systems

### Visual Representation

```
Decimal: 5
Binary:  0 0 0 0 0 1 0 1
         ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑
         7 6 5 4 3 2 1 0  (Bit positions)
```

---

## 3. Why Bitwise Operators Are Important

### 1. Direct Hardware Control

Microcontrollers have registers where each bit controls a specific function.

```
GPIO Register:
Bit 0: Pin 0 direction
Bit 1: Pin 1 direction
Bit 2: Pin 2 direction
...
Bit 7: Pin 7 direction
```

### 2. Fast Execution

Bitwise operations are single CPU instructions.

```
C Code:    x & (1 << 3)
Assembly:  AND R0, R1
          → One instruction!
```

### 3. Memory-Efficient Flag Storage

Store 8 flags in 1 byte instead of 8 bytes.

```
Without Bitwise:
bool flag1, flag2, flag3, flag4, flag5, flag6, flag7, flag8;
// 8 bytes used

With Bitwise:
uint8_t flags;  // 8 flags in 1 byte!
```

### 4. No Function Overhead

Direct operations without function calls.

### 5. Essential for Embedded Systems

```
- GPIO Control
- Timer Configuration
- Interrupt Handling
- Communication Protocols
- ADC/DAC Control
```

---

## 4. Binary Representation

### Decimal to Binary

```
Decimal: 5
Binary:  00000101

Bit Positions:
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ 128 │ 64  │ 32  │ 16  │ 8   │ 4   │ 2   │ 1   │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  0  │  0  │  0  │  0  │  0  │  1  │  0  │  1  │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
       Bit 7 6 5 4 3 2 1 0
```

### Common Binary Patterns

```
Bit Pattern  | Decimal | Hex
00000001     | 1       | 0x01
00000010     | 2       | 0x02
00000100     | 4       | 0x04
00001000     | 8       | 0x08
00010000     | 16      | 0x10
00100000     | 32      | 0x20
01000000     | 64      | 0x40
10000000     | 128     | 0x80
```

### Bit Positions Visual

```
Byte: 0 1 0 1 0 0 1 1
      ↑ ↑ ↑ ↑ ↑ ↑ ↑ ↑
      │ │ │ │ │ │ │ │
      7 6 5 4 3 2 1 0 (Bit numbers)

Value = (bit7×128) + (bit6×64) + ... + (bit0×1)
```

---

## 5. Bitwise Operators in C

### Operators Table

| Operator | Name | Symbol | Example |
|----------|------|--------|---------|
| AND | Bitwise AND | `&` | `a & b` |
| OR | Bitwise OR | `|` | `a | b` |
| XOR | Exclusive OR | `^` | `a ^ b` |
| NOT | Complement | `~` | `~a` |
| Left Shift | Shift left | `<<` | `a << n` |
| Right Shift | Shift right | `>>` | `a >> n` |

### Quick Reference

```
┌─────────────────────────────────────────────────────────┐
│           BITWISE OPERATORS SUMMARY                     │
├──────────────┬────────────┬────────────────────────────┤
│ Operator     │ Symbol     │ Description                │
├──────────────┼────────────┼────────────────────────────┤
│ AND          │ &          │ 1 if both bits are 1      │
│ OR           │ |          │ 1 if at least one bit is 1│
│ XOR          │ ^          │ 1 if bits are different   │
│ NOT          │ ~          │ Inverts all bits          │
│ Left Shift   │ <<         │ Shifts left (×2)          │
│ Right Shift  │ >>         │ Shifts right (÷2)         │
└──────────────┴────────────┴────────────────────────────┘
```

---

## 6. Bitwise AND (&)

### Definition

**Bitwise AND** returns 1 only if **both** bits are 1.

### Truth Table

```
Bit A | Bit B | Result
------|-------|--------
  0   |   0   |   0
  0   |   1   |   0
  1   |   0   |   0
  1   |   1   |   1
```

### Example

```
a = 5  (0101)
b = 3  (0011)
result = a & b

  0101
& 0011
------
  0001  → 1
```

### Embedded Use Case: Checking Pin Status

```c
// Check if pin 2 is HIGH
if (PORT & (1 << 2)) {
    // Pin 2 is HIGH
}
```

### Common Uses

```
1. Check if a bit is set
   if (value & (1 << n))

2. Extract specific bits
   value & 0x0F  // Get lower 4 bits

3. Clear specific bits
   value = value & ~mask
```

---

## 7. Bitwise OR (|)

### Definition

**Bitwise OR** returns 1 if **at least one** bit is 1.

### Truth Table

```
Bit A | Bit B | Result
------|-------|--------
  0   |   0   |   0
  0   |   1   |   1
  1   |   0   |   1
  1   |   1   |   1
```

### Example

```
a = 5  (0101)
b = 3  (0011)
result = a | b

  0101
| 0011
------
  0111  → 7
```

### Embedded Use Case: Setting Pin HIGH

```c
// Set pin 3 HIGH
PORT |= (1 << 3);  // Set bit 3
```

### Common Uses

```
1. Set a bit
   value |= (1 << n)

2. Set multiple bits
   value |= (mask)

3. Combine values
   value = value | new_value
```

---

## 8. Bitwise XOR (^)

### Definition

**Bitwise XOR** returns 1 if bits are **different**.

### Truth Table

```
Bit A | Bit B | Result
------|-------|--------
  0   |   0   |   0
  0   |   1   |   1
  1   |   0   |   1
  1   |   1   |   0
```

### Example

```
a = 5  (0101)
b = 3  (0011)
result = a ^ b

  0101
^ 0011
------
  0110  → 6
```

### Embedded Use Case: Toggling Pin

```c
// Toggle pin 2
PORT ^= (1 << 2);
```

### Common Uses

```
1. Toggle a bit
   value ^= (1 << n)

2. Swap values without temp
   a = a ^ b;
   b = a ^ b;
   a = a ^ b;

3. Check if bits differ
   value = a ^ b  // Bits that differ
```

---

## 9. Bitwise NOT (~)

### Definition

**Bitwise NOT** inverts all bits (0→1, 1→0).

### Truth Table

```
Bit | Result
----|--------
 0  |   1
 1  |   0
```

### Example

```
a = 5  (00000101)
result = ~a

  00000101
  --------
  11111010  → 250 (for 8-bit)
```

### Embedded Use Case: Clearing Bits

```c
// Clear bit 3
PORT &= ~(1 << 3);
```

### Common Uses

```
1. Clear a bit
   value &= ~(1 << n)

2. Clear multiple bits
   value &= ~mask

3. Create inverted mask
   value = ~mask
```

---

## 10. Left Shift (<<)

### Definition

**Left Shift** shifts bits left by n positions, filling with 0s on right.

### Effect

```
x << n = x × 2^n
```

### Example

```
a = 3  (00000011)
result = a << 1

  00000011
  --------
  00000110  → 6

a << 2 = 12 (3 × 4)
```

### Embedded Use Case: Setting Bit Position

```c
// Activate pin 5
PORT = (1 << 5);
```

### Common Uses

```
1. Set bit at position n
   (1 << n)

2. Multiply by power of 2
   value << n  // value × 2^n

3. Create mask
   mask = 0xFF << 8
```

---

## 11. Right Shift (>>)

### Definition

**Right Shift** shifts bits right by n positions.

### Effect (Unsigned)

```
x >> n = x ÷ 2^n
```

### Example

```
a = 8  (00001000)
result = a >> 1

  00001000
  --------
  00000100  → 4

a >> 2 = 2 (8 ÷ 4)
```

### Embedded Use Case: Extracting Value

```c
// Extract bits 4-7
value = (PORT >> 4) & 0x0F;
```

### Common Uses

```
1. Divide by power of 2
   value >> n  // value ÷ 2^n

2. Extract bits
   (value >> n) & mask

3. Get high byte
   value >> 8
```

---

## 12. Bit Manipulation Operations

### 1. Set a Bit

```c
value |= (1 << n);
```

**Example:**
```
value = 0x00 (00000000)
Set bit 3:
value |= (1 << 3)  // 00001000
```

### 2. Clear a Bit

```c
value &= ~(1 << n);
```

**Example:**
```
value = 0x08 (00001000)
Clear bit 3:
value &= ~(1 << 3)  // 00000000
```

### 3. Toggle a Bit

```c
value ^= (1 << n);
```

**Example:**
```
value = 0x00 (00000000)
Toggle bit 3:
value ^= (1 << 3)  // 00001000
Toggle again:
value ^= (1 << 3)  // 00000000
```

### 4. Check a Bit

```c
if (value & (1 << n)) {
    // Bit is set
}
```

**Example:**
```
value = 0x08 (00001000)
if (value & (1 << 3)) {
    // Bit 3 is set (true)
}
if (value & (1 << 2)) {
    // Bit 2 is set (false)
}
```

### 5. Update a Bit

```c
value = (value & ~(1 << n)) | (bit << n);
```

**Example:**
```
value = 0x00
Set bit 3 to 1:
value = (value & ~(1 << 3)) | (1 << 3)  // 00001000
```

---

## 13. Embedded Register Example

### GPIO Register Control

```c
#define GPIO (*(volatile uint32_t*)0x40020000)

// Set bit 0 (enable output)
GPIO |= (1 << 0);

// Clear bit 0 (disable output)
GPIO &= ~(1 << 0);

// Toggle bit 0
GPIO ^= (1 << 0);

// Check bit 0
if (GPIO & (1 << 0)) {
    // Bit 0 is set
}
```

### Timer Configuration

```c
#define TIMER (*(volatile uint32_t*)0x40001000)

// Enable timer (bit 0)
TIMER |= (1 << 0);

// Set prescaler to 64 (bits 1-3)
TIMER |= (0b011 << 1);

// Set mode to PWM (bits 4-5)
TIMER |= (0b10 << 4);

// Check if timer is running
if (TIMER & (1 << 7)) {
    // Timer running
}
```

---

## 14. Real Embedded Example - LED Control

### LED Control Functions

```c
#define LED_PIN 2
#define PORT (*(volatile uint32_t*)0x40020000)

// Turn LED ON
void led_on() {
    PORT |= (1 << LED_PIN);
}

// Turn LED OFF
void led_off() {
    PORT &= ~(1 << LED_PIN);
}

// Toggle LED
void led_toggle() {
    PORT ^= (1 << LED_PIN);
}

// Check LED status
bool led_is_on() {
    return (PORT & (1 << LED_PIN)) ? true : false;
}
```

### Multiple LEDs Control

```c
#define LED1_PIN 0
#define LED2_PIN 1
#define LED3_PIN 2

#define LED1 (1 << LED1_PIN)
#define LED2 (1 << LED2_PIN)
#define LED3 (1 << LED3_PIN)

// Turn on all LEDs
PORT |= (LED1 | LED2 | LED3);

// Turn off all LEDs
PORT &= ~(LED1 | LED2 | LED3);

// Toggle LED1 and LED3
PORT ^= (LED1 | LED3);

// Check if any LED is on
if (PORT & (LED1 | LED2 | LED3)) {
    // Some LED is on
}
```

---

## 15. Bitwise vs Logical Operators

### Comparison Table

| Feature | Bitwise Operators | Logical Operators |
|---------|-------------------|-------------------|
| **Works on** | Bits | Boolean values |
| **Operators** | `&`, `|`, `^`, `~` | `&&`, `||`, `!` |
| **Result** | Integer | Boolean (0/1) |
| **Use Case** | Register manipulation | Conditions |
| **Short-circuit** | No | Yes |
| **Speed** | Very fast | Slower |
| **Example** | `x & 0x0F` | `x > 0 && x < 10` |

### Important Difference

```c
// Logical AND (short-circuit)
if (x && y) {  // y not evaluated if x is false
    // ...
}

// Bitwise AND (always evaluates)
if (x & y) {   // Both x and y are evaluated
    // ...
}
```

### When to Use Which

```
Use Bitwise Operators For:
- Register manipulation
- Flag handling
- Performance-critical code
- Embedded systems

Use Logical Operators For:
- Condition checking
- Control flow
- Boolean expressions
- General programming
```

---

## 16. Common Mistakes

### 1. Confusing OR and XOR

```c
// Wrong
PORT ^= (1 << 2);  // Toggle
PORT |= (1 << 2);  // Set

// If you meant set, use |
// If you meant toggle, use ^
```

### 2. Not Using Parentheses

```c
// Wrong - operator precedence issue
x & 1 << 2

// Correct
x & (1 << 2)
```

### 3. Shifting Beyond Data Type

```c
// Wrong - shifting 32-bit by 32
uint32_t x = 1 << 32;

// Correct - shift within range
uint32_t x = 1UL << 31;  // Max for 32-bit
```

### 4. Signed Shift Issues

```c
// Wrong - implementation-defined behavior
int x = -1 >> 2;

// Correct - use unsigned
unsigned int x = 0xFFFFFFFF >> 2;
```

### 5. Forgetting Mask

```c
// Wrong - may affect other bits
value = value & ~(1 << 3);  // Clears bit 3 only

// Correct - keep mask
value &= ~(1 << 3);
```

### 6. Confusing & and &&

```c
// Wrong - logical instead of bitwise
if (value && (1 << 3))

// Correct - bitwise
if (value & (1 << 3))
```

---

## 17. Real-Time Examples

### Example 1: UART Configuration

```c
#define UART_CR (*(volatile uint32_t*)0x40001000)
#define UART_BAUD (*(volatile uint32_t*)0x40001004)

// Configure UART
void uart_init(uint32_t baud) {
    // Enable UART (bit 0)
    UART_CR |= (1 << 0);
    
    // Set 8 data bits (bits 1-2)
    UART_CR |= (0b11 << 1);
    
    // Set 1 stop bit (bit 3 = 0)
    UART_CR &= ~(1 << 3);
    
    // No parity (bits 4-5 = 0)
    UART_CR &= ~(0b11 << 4);
    
    // Set baud rate
    UART_BAUD = baud;
}
```

### Example 2: Interrupt Handling

```c
#define IRQ_ENABLE (*(volatile uint32_t*)0x40002000)
#define IRQ_STATUS (*(volatile uint32_t*)0x40002004)
#define IRQ_CLEAR (*(volatile uint32_t*)0x40002008)

#define IRQ_TIMER   (1 << 0)
#define IRQ_UART    (1 << 1)
#define IRQ_GPIO    (1 << 2)

// Enable interrupts
IRQ_ENABLE |= (IRQ_TIMER | IRQ_UART);

// Check which interrupt occurred
if (IRQ_STATUS & IRQ_TIMER) {
    // Timer interrupt
    IRQ_CLEAR = IRQ_TIMER;  // Clear
}

if (IRQ_STATUS & IRQ_UART) {
    // UART interrupt
    IRQ_CLEAR = IRQ_UART;   // Clear
}
```

### Example 3: SPI Communication

```c
#define SPI_CR (*(volatile uint32_t*)0x40003000)
#define SPI_SR (*(volatile uint32_t*)0x40003004)
#define SPI_DR (*(volatile uint32_t*)0x40003008)

// SPI Configuration
void spi_init() {
    // Enable SPI (bit 0)
    SPI_CR |= (1 << 0);
    
    // Master mode (bit 1 = 1)
    SPI_CR |= (1 << 1);
    
    // Clock phase: data sampled on first edge (bit 2 = 0)
    SPI_CR &= ~(1 << 2);
    
    // Clock polarity: idle low (bit 3 = 0)
    SPI_CR &= ~(1 << 3);
    
    // Prescaler: 16 (bits 4-6 = 010)
    SPI_CR = (SPI_CR & ~(0b111 << 4)) | (0b010 << 4);
}

// SPI Send/Receive
uint8_t spi_xfer(uint8_t data) {
    // Wait for transmit ready
    while (!(SPI_SR & (1 << 0)));
    
    // Send data
    SPI_DR = data;
    
    // Wait for receive ready
    while (!(SPI_SR & (1 << 1)));
    
    // Return received data
    return SPI_DR;
}
```

---

## 18. Advantages

### 1. Very Fast Operations

```c
// Bitwise operation - one CPU instruction
x &= ~(1 << 3);

// Equivalent C - multiple instructions
if (x >= 8) {
    x -= 8;  // Actually multiple operations
}
```

### 2. Hardware-Level Control

```c
// Direct register access
PORT |= (1 << 5);  // Set pin 5

// Hardware interaction
// No function calls, no overhead
```

### 3. Memory Efficient

```c
// 8 flags in 1 byte
uint8_t status;
status |= (1 << 0);  // Flag 1
status |= (1 << 1);  // Flag 2
status |= (1 << 2);  // Flag 3

// vs 8 separate bools (8 bytes)
```

### 4. Essential for Embedded

```
✓ GPIO control
✓ Timer configuration
✓ Interrupt handling
✓ Communication protocols
✓ Power management
```

### 5. No Function Overhead

```
Direct operations
No function calls
No stack manipulation
No context switching
```

---

## 19. Quick Revision

### Bitwise Operators Summary

```
┌─────────────────────────────────────────────────────────┐
│           BITWISE OPERATORS CHEAT SHEET                 │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  AND (&):  1 if both bits are 1                        │
│  OR (|):   1 if at least one bit is 1                 │
│  XOR (^):  1 if bits are different                    │
│  NOT (~):  Inverts all bits                           │
│  << :      Shifts left (multiply by 2^n)              │
│  >> :      Shifts right (divide by 2^n)               │
│                                                         │
│  SET BIT:    x |= (1 << n)                            │
│  CLEAR BIT:  x &= ~(1 << n)                          │
│  TOGGLE BIT: x ^= (1 << n)                           │
│  CHECK BIT:  if (x & (1 << n))                       │
│                                                         │
│  COMMON PATTERNS:                                     │
│  0x01 = 1     │  0x0F = 15     │  0xFF = 255        │
│  0x02 = 2     │  0xF0 = 240                          │
│  0x04 = 4     │  0x0A = 10                           │
│  0x08 = 8     │  0x55 = 85                           │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Common Bit Patterns

```
Value  | Hex   | Binary
-------|-------|----------------
1      | 0x01  | 00000001
2      | 0x02  | 00000010
4      | 0x04  | 00000100
8      | 0x08  | 00001000
16     | 0x10  | 00010000
32     | 0x20  | 00100000
64     | 0x40  | 01000000
128    | 0x80  | 10000000
255    | 0xFF  | 11111111
```

---

## 20. Interview Questions

### Basic Questions

#### Q1: What are bitwise operators?
**Answer:** Bitwise operators perform operations on individual bits of integer data types.

#### Q2: List all bitwise operators in C.
**Answer:** `&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `<<` (Left Shift), `>>` (Right Shift).

#### Q3: What's the difference between `&` and `&&`?
**Answer:** `&` is bitwise AND (works on bits), `&&` is logical AND (works on boolean values).

#### Q4: How do you set a bit?
**Answer:** `x |= (1 << n);`

### Intermediate Questions

#### Q5: How do you clear a bit?
**Answer:** `x &= ~(1 << n);`

#### Q6: How do you toggle a bit?
**Answer:** `x ^= (1 << n);`

#### Q7: How do you check if a bit is set?
**Answer:** `if (x & (1 << n))`

#### Q8: What's the use of bitwise operators in embedded systems?
**Answer:** Register manipulation, GPIO control, timer configuration, flags handling.

### Advanced Questions

#### Q9: What's the difference between left shift and multiplication?
**Answer:** Left shift is a single CPU instruction and faster. Multiplication may be slower.

#### Q10: What happens when you shift a signed negative number?
**Answer:** Right shift of negative numbers is implementation-defined (compiler-dependent).

#### Q11: How do you extract specific bits?
**Answer:** `(x >> n) & mask`

#### Q12: What's a common use of XOR?
**Answer:** Toggling bits and swapping values without a temporary variable.

---

## 21. Conclusion

### Summary

Bitwise operators are fundamental tools in C programming, especially for embedded systems. They provide:

```
✓ Direct hardware control
✓ Fast execution
✓ Memory efficiency
✓ Simple flag handling
✓ Essential for embedded programming
```

### Key Takeaways

```
✓ AND (&):  Check bits
✓ OR (|):   Set bits
✓ XOR (^):  Toggle bits
✓ NOT (~):  Invert bits
✓ <<:       Multiply by 2^n
✓ >>:       Divide by 2^n
```

### When to Use

```
✓ GPIO control
✓ Register manipulation
✓ Flag handling
✓ Performance-critical code
✓ Embedded systems
✓ Hardware programming
```

### Final Thought

Bitwise operators are the **backbone of embedded systems programming**. Understanding them is essential for:

- Device driver development
- Microcontroller programming
- Real-time systems
- Performance optimization
- Memory-efficient code

**Master bitwise operators to unlock the true power of C programming in embedded systems.**

---

*End of Document*
