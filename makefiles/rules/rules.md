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
