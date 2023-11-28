# Functions

- Make has many useful built-in functions
- Most of these revolve around text manipulation
- Not recommended to do complicated text manipulation inside make, most of these functions are intended for makefile tasks
- A complete list can be found in the [manual](https://www.gnu.org/software/make/manual/html_node/Functions.html).

## Making Calls

- Function calls look like variable expansion
- `$(function_name arg1,arg2,arg3,...)`
- Functions can be assigned to variables `time := $(shell date)`

---
layout: applcommon-four-grid-header
---

# Basic Output Functions

Useful for debugging or outputting variables from outside a recipe.

::topTitle::
`info` prints but does not error when used.

::topLeft::
```makefile
var:=testing output
$(info $(var))

.PHONY: all
all:
	@echo done
```

::bottomTitle::
`error` ends the program when reached and prints out the error message. Often used for required arguments.

::bottomLeft::
```makefile
var:=testing output
$(error $(var))

.PHONY: all
all:
  @echo done
```
::topRight::
```bash
$ make
testing output
done
$ echo $?
0
```

::bottomRight::
```bash
$ make
Makefile:2: *** testing output.  Stop.
$ echo $?
2
```

---

# Call function

- Write your own functions!

---

# defines

- the way we prefer to write functions

---

# eval

- generate makefile code

---

# gmsl

- Hopefully you never need to go this deep

---

# move onto conditionals in another file?
