---
theme: apple-basic
layout: intro
colorSchema: dark
---

# Startup Code
Chris Beeler

---
src: ./hello-world/hello-world.md
---

---
layout: two-cols
---

# Order Matters

```ld
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

![center](assets/linker-order-matters/diagram.png)

---
layout: two-cols
---

# Order Matters

```ld
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

![center](assets/linker-order-matters/fixedVectorsMiddle.png)
