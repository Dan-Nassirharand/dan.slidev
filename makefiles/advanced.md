---
layout: section
---

# Advanced Make

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

# Recursive Make

- Using a make recipe to run a different makefile without including its contents within the calling makefile
- Used when sources need to be kept completely separate
- Example: An application builds it boot loader through recursive make. Since the boot loader has its own main and `applcommon`, they need to be kept separate otherwise the namespace would collide.

```makefile
.PHONY: boot-loader
boot-loader:
	$(MAKE) -C lib/boot-loader -f boot-loader.mk RELEASE=Y DEBUG=N build_all
```

No need to pass `-j` because using `$(MAKE)` uses the current process make and manages how many threads each `make` is using through a `jobserver`.

---
layout: applcommon-two-cols-header
---

# Non-Recursive Make

- Includes all the contents of the included makefile into the current makefile.
- The first rule encountered, included or not, is still the default rule
- Variables, rules and functions can conflict, so think carefully when designing makefiles.
- Including makefiles in different directories may not work if the included makefile is not designed for it.

::left::
```makefile
# target.mk
target: submodule
	@echo Target Complete using $(SUBMODULE)

include submodule.mk
```
```makefile
# submodule.mk
SUBMODULE:=applcommon
submodule:
	@echo $(SUBMODULE) complete
```

::right::
```bash
$ make
applcommon complete
Target Complete using applcommon
```

---

# Dependency Files

- Both GCC and Make are GNU products, which allow for the programs to have functionality to support each other
- The preprocessor can scan files and output their dependencies in Make format
- These files can be included into makefiles non-recursively to add the dependency to rules automatically and make incremental builds reliable

```makefile
# build/test/src/Alignment/AlignmentDetector.c.d in applcommon
build/test/./src/Alignment/AlignmentDetector.c.o: \
 src/Alignment/AlignmentDetector.c src/Alignment/AlignmentDetector.h \
 src/Utilities/utils.h
src/Alignment/AlignmentDetector.h:
src/Utilities/utils.h:

```

---

# Dependency Files

- Options to generate while compiling are:
  - `-MF "$(@:%.o=%.d)"` Outputs the dependency file to the same name as the `.o`, but instead swaps it to a `.d` extension
  - `-MT "$@"` This tells the compiler to keep directory components inside the generated rule
  - `-MP` Tells the compiler to add a phony target for each dependency other than the main file. Stops errors on incremental builds when removing header files
  - `-MMD` Only output dependencies for user files and not system files. If doing system development, `-MD` might be better

---

# Dependency Files

- The generated rules need to modify the existing rules in the makefile, so the files are included non-recursively.
- Since the dependency files do not exist on the first run, the `-` symbol must be used
  - `-` tells `make` to ignore errors, this can even be done in recipes but not recommended

```makefile
DEPS:=$(SRC:%=%.d) # Takes whatever is in SRC and adds a `.d` to it

-include $(DEPS)
```

---

# Debugging Make

- `make --dry-run`: Causes make to print the recipes that are needed to make the targets up to date, but not actually execute them. [1](https://www.gnu.org/software/make/manual/html_node/Instead-of-Execution.html#index-_002d_002djust_002dprint-1)
- `make --debug=[options]`: Prints debugging information along with doing the normal run. There are many options to help narrow the results. [2](https://www.gnu.org/software/make/manual/html_node/Options-Summary.html#index-_002d_002ddebug)
- `make --trace`: Show tracing information for make execution. Using `--trace` is shorthand for `--debug=print,why`. [3](https://www.gnu.org/software/make/manual/html_node/Options-Summary.html#index-_002d_002dtrace)

---

# Alternative Tools

- Make is awesome because its relatively simple, useful outside of C/C++, easy to run and easy to install

Other Options:
  - [meson](https://mesonbuild.com/): A very user friendly build system with lots of languages supported by default. This is the upcoming build system
  - [cmake](https://cmake.org/): Lots of built in functionality meant to make C/C++ easier, but it seems like it would be very difficult to teach a whole organization.
  - [Autotools](https://www.gnu.org/software/automake/manual/html_node/Autotools-Introduction.html): Meant to help generate makefiles so any user can compile on their system.
