---
layout: applcommon-two-cols-header
---

# Variables

::left::

- Set a variable using the `=` operator (recursively expanded... more on this later)
- Single letter variables can be expanded using `$`, longer names need `$()`
- Invalid characters in a variable are `:`, `#` and `=`.

::right::
```makefile
var = test

.PHONY: print
print:
	echo $(var)
```

```bash
$ make
echo test
test
```

---
layout: applcommon-two-cols-header
---

# Passing in Variables

- Variables can be passed in from the command line or the environment
- Expecting variables from the environment is considered bad practice

::left::
```makefile
.PHONY: print
print:
	echo $(var)
```

::right::
```bash
$ make var=hello
echo hello
hello
```

---
layout: applcommon-two-cols-header
---

# Allowing Variable Overrides

- Use `?=` to set a default but allow others to override it


::left::
```makefile
var ?= default

.PHONY: print
print:
	echo $(var)
```

::right::

```bash
$ make var=hello
echo hello
hello
```

```bash
$ make
echo default
default
```

---
layout: applcommon-two-cols-header
---

# Recursively vs Non-Recursively Variable Expansion

- Setting a variable with `=` cause the variable to be evaluated at the time of expansion (use)

::left::
```makefile
time = $(shell date) # we will cover functions in a bit

.PHONY: all
all: some_task
	@echo $(time)

.PHONY: some_task
some_task:
	@date
	sleep 5
```

::right::
```bash
$ make
Fri Oct 20 11:31:51 AM EDT 2023
sleep 5
Fri Oct 20 11:31:56 AM EDT 2023
```

The time variable was expanded after `some_task` was completed!

<!--
Yes I know we haven't covered functions yet
-->

---
layout: applcommon-two-cols-header
---

# Recursively vs Non-Recursively Variable Expansion

- Recursively expanded variables can cause all sorts of headaches
- Use non-recursively expansion `:=` to avoid problems
- We recommend that variables are always set with `:=`, unless it is set using `?=`


::left::
```makefile
time := $(shell date) # we will cover functions in a bit

.PHONY: all
all: some_task
	@echo $(time)

.PHONY: some_task
some_task:
	@date
	sleep 5
```

::right::
```bash
$ make
Fri Oct 20 11:38:16 AM EDT 2023
sleep 5
Fri Oct 20 11:38:16 AM EDT 2023
```
