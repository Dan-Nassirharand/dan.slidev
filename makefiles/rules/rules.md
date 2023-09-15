---
layout: applcommon-two-cols-header
---

# Rules and Recipes

```makefile
target: prerequisites # Rule
	commands # Recipe
```

- Each recipe is run in its own subshell.
- When any of the prerequisites change, the target is rebuilt
- Make is whitespace sensitive and `Recipes` are preceded by a `tab` character.

::left::
```makefile
.PHONY: all
all:
	mkdir -p bar
	cd bar
	echo “put into file in bar” >> file.txt
```

::right::

Where will file.txt be placed and why?

<!--
Turning on render whitespace in VS Code by using `ctrl + shift + p` and `View: Toggle Render Whitespace`

Tabs look like a little arrow and it is almost impossible to work on Makefiles without rendering the whitespace.
-->

---
layout: applcommon-two-cols-header
---
# Echoing
- Each recipe will is printed on the command line when executed.
- Great for debugging, bad for normal use
- Using `@` at the start of a line will suppress the echoing.


::left::
```makefile
.PHONY: all
all:
	echo hello
```

```makefile
.PHONY: all
all:
	@echo hello
```

::right::
```bash
$ make
echo hello
hello
```

```bash
$ make
hello
```

<!--
Need to mention global silence after variables
-->

---

# Default Rule

---

# Specifying A Target

---

# Prerequisites

---

# Order Only Prerequisites

---

# Phony Targets
