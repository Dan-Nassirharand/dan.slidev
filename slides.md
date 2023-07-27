---
theme: apple-basic
layout: intro
colorSchema: light
---

# Startup Code
Chris Beeler

---
src: ./hello-world/hello-world.md
---

---
layout: two-cols
---

# Side Quest - Order Matters

```ld
SECTIONS
{
  .text :
  {
    KEEP(*(.fixedVectors))
    *(.text*)
    *(.rodata*)
  } > FLASH
}
```

::right::

![center](assets/linker-order-matters/diagram.png)
