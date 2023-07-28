---
layout: two-cols
---

# Order Matters

```ld {all}
SECTIONS
{
  .text:
  {
    KEEP(*(.fixedVectors))
    *(.text*)
    *(.rodata*)
  } > FLASH
}
```

::right::

<img src="order-matters/assets/linker-order-matters/diagram.png" class="m-12 h-80" />

---
layout: two-cols
---

# Order Matters

```ld {3-4,8}
SECTIONS
{
  .text:
  {
    KEEP(*(.fixedVectors))
    *(.text*)
    *(.rodata*)
  } > FLASH
}
```

::right::

<img src="order-matters/assets/linker-order-matters/highlightFlashAddresses.png" class="m-12 h-80" />

---
layout: two-cols
---

# Order Matters

```ld {5-7}
SECTIONS
{
  .text:
  {
    KEEP(*(.fixedVectors))
    *(.text*)
    *(.rodata*)
  } > FLASH
}
```

::right::

<img src="order-matters/assets/linker-order-matters/diagram.png" class="m-12 h-80" />

---
layout: two-cols
---

# Order Matters

```ld {5-7}
SECTIONS
{
  .text:
  {
    *(.text*)
    KEEP(*(.fixedVectors))
    *(.rodata*)
  } > FLASH
}
```

::right::

<img src="order-matters/assets/linker-order-matters/fixedVectorsMiddle.png" class="m-12 h-80" />
