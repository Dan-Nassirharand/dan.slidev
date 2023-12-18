---
layout: section
---

# Make

---

# Make

- A GNU program that uses dependency tracking to execute the required commands necessary to create a target.
- `make` is normally associated with C and C++, but can be used anywhere.

---

# Make Principles

- Start by telling `make` what is desired and break it down into individual tasks.

<pre>

</pre>

```
Egg + Flour + Salt = Dough

Dough + Sauce + Cheese = Raw Pizza

Raw Pizza + Time + Heat = Pizza
```

- Then ask `make` for a specific target and it will use the dependencies to only execute what is needed.

<!--
Make sure to define all the steps so it is actually achievable

2 ways to approach:
- Write out exactly what to do in order for all steps
- Write out how to get from one step to another

Ponderings:
- How are you going to achieve parallelism?
- How are you going to achieve incrementalism (if I already have dough… do I need to make it?)
- How are you going to express options (I can either make dough from ingredients or I can go to the store)?
-->

---

# Running Make

- Typing `make` into the terminal will invoke the file `Makefile`.

- `make -f target.mk` will invoke the default rule in `target.mk` (more on this later)

- `make -j<n>` will allow `n` recipes to be run in parallel

---
src: ./rules.md
---

---
src: ./advanced.md
---
