<script setup>
import { cn } from "@/lib/utils";

const props = defineProps({
  class: { type: null, required: false },
  variant: { type: String, default: 'default' }, // default, striped
});
</script>

<template>
  <tr
    :class="
      cn(
        'border-b transition-colors hover:bg-muted/50 data-[state=selected]:bg-muted',
        variant === 'striped' && 'odd:bg-gray-50',
        props.class,
      )
    "
  >
    <slot />
  </tr>
</template>
