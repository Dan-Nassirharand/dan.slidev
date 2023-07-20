---
marp: true
theme: default
backgroundColor: white
style: |
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
---

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>

<!-- _class: lead -->

# Startup Code
Chris Beeler

---

# Hello, World!
This program starts at main, right? That’s what I was taught in school!

```
#include <stdio.h>

int main()
{
   printf("Hello, World!\n");
   return 0;
}
```

```
$ gcc hello.c -o hello.o
$ ./hello.o
Hello, World!
```

---
# Side Quest - Order Matters
<div class="columns">
<div class="columns-left">

```
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

</div>
<div class="columns-right">

![center](./assets/linker-order-matters/diagram.png)

</div>
</div>
