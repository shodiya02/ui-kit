<script setup>
import { cn } from "@/lib/utils";

const props = defineProps({
  class: { type: null, required: false },
  sticky: { type: Boolean, default: false },
});
</script>

<template>
  <thead
    :class="cn(
      '[&_tr]:border-b',
      sticky && 'sticky top-0 z-10 bg-white shadow-sm',
      props.class
    )"
  >
    <slot />
  </thead>
</template>
