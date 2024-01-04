# Conditionals

- Basic conditional is always terminated with a `endif`

```makefile
conditional-directive
text-if-true
endif
```

- else-if statements:

```makefile
conditional-directive-one
text-if-one-is-true
else conditional-directive-two
text-if-two-is-true
else
text-if-one-and-two-are-false
endif
```

---

# `ifeq`/`ifneq`

- `make` has lots of formatting options, but standard at GEA is to use `ifeq (arg1, arg2)`

```makefile
ifeq ($(JLINK), Y) # notice the variable is expanded
  FLASH_COMMAND=jlinkexe
else
  FLASH_COMMAND=rfp
endif
```

- Remember that variables can come in through the environment and mess with the logic!

---
layout: applcommon-two-cols-header
---


# `ifdef`/`ifndef`

- If the value of the variable is empty, `ifdef` returns `false`.

::left::

```makefile
hello=
foo=set

ifdef hello # notice hello is not expanded
$(info hello set)
else
$(info hello not set)
endif

ifdef foo
$(info foo set)
else
$(info foo not set)
endif
```

::right::

```bash
$ make
hello not set
foo set
make: *** No targets.  Stop.
```
