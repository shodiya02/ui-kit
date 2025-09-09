<script setup>
import { cn } from "@/lib/utils";

const props = defineProps({
  class: { type: null, required: false },
  align: { type: String, default: 'left' }, // left, center, right
});
</script>

<template>
  <td
    :class="
      cn(
        'p-2 align-middle [&:has([role=checkbox])]:pr-0 [&>[role=checkbox]]:translate-y-0.5',
        align === 'center' && 'text-center',
        align === 'right' && 'text-right',
        props.class,
      )
    "
  >
    <slot />
  </td>
</template>
