<script setup>
import { cn } from "@/lib/utils";

const props = defineProps({
  class: { type: null, required: false },
  align: { type: String, default: 'left' }, // left, center, right
  fixed: { type: String, required: false }, // left, right
  fixedOffset: { type: String, default: '0px' }, // offset from edge when fixed
});

const getFixedClasses = () => {
  if (!props.fixed) return '';

  const baseFixed = 'sticky z-10 bg-white/95 backdrop-blur-sm';

  if (props.fixed === 'left') {
    return `${baseFixed} border-r-2 border-gray-200 shadow-[4px_0_8px_-2px_rgba(0,0,0,0.15)] before:absolute before:inset-0 before:bg-white before:-z-10`;
  }
  if (props.fixed === 'right') {
    return `${baseFixed} border-l-2 border-gray-200 shadow-[-4px_0_8px_-2px_rgba(0,0,0,0.15)] before:absolute before:inset-0 before:bg-white before:-z-10`;
  }

  return '';
};

const getFixedStyle = () => {
  if (!props.fixed) return {};

  if (props.fixed === 'left') {
    return { left: props.fixedOffset };
  }
  if (props.fixed === 'right') {
    return { right: props.fixedOffset };
  }

  return {};
};
</script>

<template>
  <td
    :class="
      cn(
        'p-2 align-middle [&:has([role=checkbox])]:pr-0 [&>[role=checkbox]]:translate-y-0.5',
        props.align === 'center' && 'text-center',
        props.align === 'right' && 'text-right',
        getFixedClasses(),
        props.class,
      )
    "
    :style="getFixedStyle()"
  >
    <slot />
  </td>
</template>
