<!--
  Usage:
```md
---
layout: two-cols-header
---
This spans both
::left::
# Left
This shows on the left
::right::
# Right
This shows on the right
```
-->

<script setup lang="ts">
const props = defineProps({
  class: {
    type: String,
  },
  layoutClass: {
    type: String,
  },
})
</script>

<template>
  <div class="slidev-layout two-cols-header-better w-full h-full" :class="layoutClass">
    <div class="col-header">
      <slot />
    </div>
    <div class="col-left" :class="props.class">
      <slot name="left" />
    </div>
    <div class="col-right" :class="props.class">
      <slot name="right" />
    </div>
  </div>
</template>

<style scoped>
.two-cols-header-better {
  display: grid;
  grid-template-columns: 1fr 2% 1fr;
  grid-template-rows: auto 2% 1fr;
}

.col-header { grid-area: 1 / 1 / 2 / 4; }
.col-left { grid-area: 3 / 1 / 3 / 2; }
.col-right { grid-area: 3 / 3 / 3 / 3; }
</style>
