---
layout: two-cols
---

# Hello, World!

Whats in the binary?

```bash
$ objdump -d hello
```

What is all this stuff!? I didn't write any of this!

::right::

```ini {all|1,7|2|3}
0000000000001000 <_init>:
    1000:	f3 0f 1e fa          	endbr64
    1004:	48 83 ec 08          	sub    $0x8,%rsp
    1008:	48 8b 05 d9 2f 00 00 	mov    0x2fd9(%rip),%rax
    100f:	48 85 c0             	test   %rax,%rax
    ...
0000000000001060 <_start>:
    1060:	f3 0f 1e fa          	endbr64
    1064:	31 ed                	xor    %ebp,%ebp
    1066:	49 89 d1             	mov    %rdx,%r9
    ...
```

<!--
First Click:
This are the start addresses and names of the functions. See we have 2 functions here

Second Click:
address: machine code assembly representation

-->

---

# Hello, World!

The code written in the `main` of `hello.c` is a very small portion of the binary:

```ini {all|7|8-9}
0000000000001149 <main>:
    1149:	f3 0f 1e fa          	endbr64
    114d:	55                   	push   %rbp
    114e:	48 89 e5             	mov    %rsp,%rbp
    1151:	48 8d 05 ac 0e 00 00 	lea    0xeac(%rip),%rax        # 2004 <_IO_stdin_used+0x4>
    1158:	48 89 c7             	mov    %rax,%rdi
    115b:	e8 f0 fe ff ff       	call   1050 <puts@plt>
    1160:	b8 00 00 00 00       	mov    $0x0,%eax
    1165:	5d                   	pop    %rbp
    1166:	c3                   	ret
```
