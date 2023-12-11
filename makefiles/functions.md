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
layout: applcommon-two-cols-header
---

# Call function

- Write your own functions!
- `call` is the built-in function used to call a variable or define function
- Arguments are variables that start at 1 and count up. The same way that `bash` does it.

::left::

```makefile
say_hello=Gob is a co-op, $1

.PHONY: all
all:
	@echo $(call say_hello,dude)
```

::right::
```bash
$ make
Gob is a co-op, dude
```

---
layout: applcommon-two-cols-header
---


# defines

- The preferred to write functions because it makes it obvious what is a function and what is a variable
- Since functions can be hard to remember what the arguments are, comments are used to document


::left::

```makefile
# Returns a string of the obvious.
# $1 Who the sentence is directed at.
define say_hello
Gob is a co-op, $1
endef

.PHONY: all
all:
	@echo $(call say_hello,dude)

```

::right::
```bash
$ make
Gob is a co-op, dude
```

---
layout: applcommon-two-cols-header
---

# defines

- Multiple lines can be used to string together tasks.
- Remember each call still occurs within a subshell.

::left::

```makefile
# Creates a file with text and prints it out
# $1 file
# $2 contents
define create_file_with_text
echo Making File $1
echo $2 > file.txt
cat file.txt
endef

.PHONY: all
all:
	@$(call create_file_with_text,test.txt, file contents)

```

::right::
```bash
$ make
Making File test.txt
file contents
$ ls
file.txt

```

---

# eval

- Allows for the generation of makefile code that is not constant.
  - Variables, targets, rules can all be generated

```makefile
.PHONY: all
all: $(PRINTS)

# $1 Creates a rule with that name and prints it
define print =
.PHONY: $1
$1:
	@echo $1
endef

$(foreach string,$(PRINTS),$(eval $(call print,$(string))))
```

```bash
$ make PRINTS="test foo hello"
test
foo
hello
```

---

# GNU Make Standard Library (gmsl)

- [Adds a ton of additional functionally](https://gmsl.jgc.org/)
  - Integer Arithmetic and Logic
  - List Manipulation
- Generally recommended as a last resort

```makefile
xcode_version:=$(strip $(subst version:,,$(shell pkgutil --pkg-info=com.apple.pkg.CLTools_Executables | grep version)))
xcode_major_version:=$(firstword $(subst ., ,$(xcode_version)))

ifeq ($(call gte,$(xcode_major_version),15), $(true))
  LDFLAGS+=-Wl,-ld_cla
endif
```

A very annoying way to check if the XCode version is greater or equal to 15. If so, add an `LDFLAG`.

---
