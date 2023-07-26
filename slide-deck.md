---
marp: true
theme: gaia
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
$ gcc hello.c -o hello
$ ./hello.o
Hello, World!
```

---
# Hello, World!
<div class="columns">
<div class="columns-left">
Whats in the binary?

```
$ objdump -d hello
```

What is all this stuff!? I didn't write any of this!
</div>
<div class="columns-right">

```
0000000000001000 <_init>:
    1000:	f3 0f 1e fa          	endbr64
    1004:	48 83 ec 08          	sub    $0x8,%rsp
    1008:	48 8b 05 d9 2f 00 00 	mov    0x2fd9(%rip),%rax
    100f:	48 85 c0             	test   %rax,%rax
    ...
```

```
0000000000001060 <_start>:
    1060:	f3 0f 1e fa          	endbr64
    1064:	31 ed                	xor    %ebp,%ebp
    1066:	49 89 d1             	mov    %rdx,%r9
    ...

```

</div>
</div>


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

![center](assets/linker-order-matters/diagram.png)

</div>
</div>
