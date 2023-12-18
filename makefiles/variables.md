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
- Use `:=`, unless it is set using `?=` or recursive behavior is desired


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

---
layout: applcommon-two-cols-header
---

# Automatic Variables

::left::

- These variables are available in each target
- Allow for makefiles to become much more generic
- There are eight automatic variables

Here are the most useful:
- `$@`: The target of the rule
- `$<`: The first prerequisite
- `$^`: All the prerequisites

::right::
```makefile
.PHONY: all
all: foo bar
	@echo all rule
	@echo $@
	@echo $<
	@echo $^

.PHONY: foo
foo:
	@echo $@

.PHONY: bar
bar:
	@echo $@
```

```bash
$ make
foo
bar
all rule
all
foo
foo bar
```

<!--
https://www.gnu.org/software/make/manual/html_node/Automatic-Variables.html
-->

---

# "Arrays"

- Variables with spaces between values act like arrays.
  - All the functionality expected array functionality, such as easy indexing is missing.
- Operations to the "array" are easily add and apply a function to all values in the array

```makefile
SRC:=test.c main.c

SRC+=foo.c # results in SRC=test.c main.c foo.c
```

<!--
Will have a slide showing this in functions
-->

---

# Substitution References

- A quick way to modify the string inside a variable
- `$(var:a=b)`
  - `var`: the variable to modify
  - `a`: the text to replace
  - `b`: the text to replace to

```makefile
foo := a.o b.o l.a c.o
bar := $(foo:.o=.c)
```

Results in : `bar=a.c b.c l.a c.c`

This example comes directly from the [make manual](https://www.gnu.org/software/make/manual/html_node/Substitution-Refs.html).
