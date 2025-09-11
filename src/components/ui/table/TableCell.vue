<script setup>
import { cn } from "@/lib/utils";

const props = defineProps({
  class: { type: null, required: false },
  align: { type: String, default: 'left' }, // left, center, right
  fixedHorizontal: { type: String, required: false }, // left, right
  fixedVertical: { type: String, required: false }, // top, bottom
  fixedOffsetH: { type: String, default: '0px' }, // horizontal offset
  fixedOffsetV: { type: String, default: '0px' }, // vertical offset
});

const getFixedClasses = () => {
  if (!props.fixedHorizontal && !props.fixedVertical) return '';

  let classes = 'sticky bg-white';
  
  // Add shadows based on fixed directions
  if (props.fixedHorizontal === 'left') {
    classes += ' shadow-[2px_0_6px_-1px_rgba(0,0,0,0.1)]';
  }
  if (props.fixedHorizontal === 'right') {
    classes += ' shadow-[-2px_0_6px_-1px_rgba(0,0,0,0.1)]';
  }
  if (props.fixedVertical === 'top') {
    classes += ' shadow-[0_2px_6px_-1px_rgba(0,0,0,0.1)]';
  }
  if (props.fixedVertical === 'bottom') {
    classes += ' shadow-[0_-2px_6px_-1px_rgba(0,0,0,0.1)]';
  }

  return classes;
};

const getFixedStyle = () => {
  const style = {};

  if (!props.fixedHorizontal && !props.fixedVertical) return style;

  // Calculate z-index based on combined positioning
  let zIndex = 1;
  if (props.fixedVertical) zIndex += 10; // top/bottom gets +10
  if (props.fixedHorizontal) zIndex += 20; // left/right gets +20
  // Corner cells (both) get 30+ z-index
  
  style.zIndex = zIndex;

  // Apply horizontal positioning
  if (props.fixedHorizontal === 'left') {
    style.left = props.fixedOffsetH;
  }
  if (props.fixedHorizontal === 'right') {
    style.right = props.fixedOffsetH;
  }
  
  // Apply vertical positioning
  if (props.fixedVertical === 'top') {
    style.top = props.fixedOffsetV;
  }
  if (props.fixedVertical === 'bottom') {
    style.bottom = props.fixedOffsetV;
  }

  return style;
};
</script>

<template>
  <td
    v-bind="$attrs"
    :class="
      cn(
        'p-2 align-middle [&:has([role=checkbox])]:pr-0 [&>[role=checkbox]]:translate-y-0.5 border-r border-b border-gray-300',
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
