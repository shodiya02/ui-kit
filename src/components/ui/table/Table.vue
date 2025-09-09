<script setup>
import { cn } from "@/lib/utils";

const props = defineProps({
  class: { type: null, required: false },
  variant: { type: String, default: 'default' }, // default, fixed, scrollable
  height: { type: String, default: 'auto' },
  title: { type: String, required: false },
  horizontalScroll: { type: Boolean, default: false }, // Enable horizontal scroll for fixed columns
});

const getWrapperClasses = () => {
  const baseClasses = 'relative w-full';

  switch (props.variant) {
    case 'fixed':
      return cn(baseClasses, 'border rounded-lg shadow-sm bg-white overflow-hidden');
    case 'scrollable':
      return cn(baseClasses, 'border rounded-lg shadow-sm bg-white overflow-hidden');
    default:
      return cn(baseClasses, 'overflow-auto');
  }
};

const getTableClasses = () => {
  const baseClasses = 'caption-bottom text-sm';

  switch (props.variant) {
    case 'fixed':
    case 'scrollable':
      return cn(baseClasses, 'border-collapse');
    default:
      return cn(baseClasses, 'w-full');
  }
};

const getTableStyle = () => {
  const style = {};

  // Set minimum width for horizontal scroll when using fixed columns
  if (props.horizontalScroll) {
    style.minWidth = '100%';
    style.width = 'max-content';
  } else {
    style.width = '100%';
  }

  return style;
};

const getScrollContainerClasses = () => {
  const baseClasses = '';

  if (props.variant === 'scrollable' || props.variant === 'fixed') {
    return cn(baseClasses, 'overflow-auto');
  }

  if (props.horizontalScroll) {
    return cn(baseClasses, 'overflow-x-auto');
  }

  return baseClasses;
};

const getScrollContainerStyle = () => {
  const style = {};

  if (props.height !== 'auto' && (props.variant === 'scrollable' || props.variant === 'fixed')) {
    style.height = props.height;
    style.maxHeight = props.height;
  }

  return style;
};
</script>

<template>
  <div :class="getWrapperClasses()">
    <!-- Table Title -->
    <div v-if="title" class="px-4 py-3 border-b bg-gray-50 font-medium text-sm text-gray-900 flex-shrink-0">
      {{ title }}
    </div>

    <!-- Table Container -->
    <div
      :class="getScrollContainerClasses()"
      :style="getScrollContainerStyle()"
    >
      <table
        :class="cn(getTableClasses(), props.class)"
        :style="getTableStyle()"
      >
        <slot />
      </table>
    </div>
  </div>
</template>
