<template>
  <div class="space-y-2 relative">
    <Popover v-model:open="open">
      <!-- Trigger Button - This is what users click to open the dropdown -->
      <PopoverTrigger as-child>
        <Button
          ref="triggerRef"
          :aria-expanded="open"
          :aria-label="ariaLabel"
          :class="
            cn(
              'w-full justify-between min-h-[40px] h-auto px-3 py-2 text-left rounded-md transition-all duration-200',
              'hover:bg-muted/50',
              triggerClasses,
              label && (open || selectedItems.length > 0) ? 'pt-3 pb-2' : '',
            )
          "
          role="combobox"
          variant="outline"
        >
          <div class="flex flex-wrap gap-1 flex-1 text-left">
            <template v-if="selectedItems.length > 0">
              <Badge
                v-for="item in selectedItems"
                :key="item.value"
                :variant="getBadgeVariant()"
                class="text-sm bg-primary text-white hover:bg-[#0F5BA3]"
              >
                {{ item.label }}
                <button
                  :aria-label="`Remove ${item.label}`"
                  class="ml-1 hover:text-destructive focus:outline-none focus:text-destructive"
                  @click.stop="removeItem(item)"
                >
                  <X class="h-3 w-3" />
                </button>
              </Badge>
            </template>
          </div>

          <component
            :is="props.icon"
            v-if="props.displayVariant === 'with-icon' && props.icon"
            class="absolute left-3 h-4 w-4 text-muted-foreground"
          />

          <label
            v-if="props.displayVariant === 'static-label' && props.staticLabel"
            class="absolute top-2 left-3 text-xs text-muted-foreground bg-background px-1"
          >
            {{ props.staticLabel }}
          </label>

          <div class="flex items-center gap-2">
            <button
              v-if="selectedItems.length > 0 && !disabled && !readonly"
              :aria-label="'Clear all selections'"
              class="text-muted-foreground hover:text-foreground"
              @click.stop="clearAll"
            >
              <IconTrash class="!h-5 !w-5" />
            </button>

            <IconChevronDown
              :class="{ 'rotate-180': open }"
              class="h-4 w-4 shrink-0 opacity-50 transition-transform duration-200"
            />
          </div>
        </Button>
      </PopoverTrigger>

      <!-- Floating Label -->
      <label
        v-if="label"
        :class="
          cn(
            'absolute left-3 transition-all duration-200 pointer-events-none z-10',
            'ui-text-light bg-background px-1 hover:bg-muted/50',
            {
              '-top-4 text-xs': open || selectedItems.length > 0,
              'top-1/3 -translate-y-1/2 text-sm': !open && selectedItems.length === 0,
            },
          )
        "
      >
        {{ label }}
      </label>

      <PopoverContent
        :side-offset="4"
        :style="popoverStyle"
        align="start"
        class="ui-multiselect p-0 bg-background border border-border shadow-lg w-full"
      >
        <Command>
          <div class="p-2.5">
            <Input  v-model:value="searchQuery" :placeholder="searchPlaceholder" />
          </div>
          <CommandEmpty>
            <div
              v-if="props.displayVariant === 'empty-state'"
              class="flex flex-col items-center justify-center py-8 text-center"
            >
              <div class="w-12 h-12 rounded-full bg-gray-100 flex items-center justify-center mb-4">
                <span class="text-gray-400 text-xl">!</span>
              </div>
              <p class="text-sm text-muted-foreground">{{ props.emptyStateMessage }}</p>
            </div>
            <span v-else>{{ emptyMessage }}</span>
          </CommandEmpty>

          <CommandGroup class="max-h-64 overflow-auto p-0">
            <CommandItem
              v-for="option in filteredOptions"
              :key="option.value"
              :value="option.value"
              class="flex items-center  cursor-pointer hover:bg-primary/20 border-t p-3"
              @select="() => toggleOption(option)"
            >
              <Checkbox
                v-if="props.showCheckbox"
                :checked="!!isSelected(option)"
                :model-value="!!isSelected(option)"
                class="pointer-events-none"
                @update:checked="() => toggleOption(option)"
              />
              <span :class="{ 'text-sm': props.longText }" class="flex-1">{{ option.label }}</span>
            </CommandItem>
          </CommandGroup>
        </Command>
      </PopoverContent>
    </Popover>
  </div>
</template>

<script setup>
import { computed, nextTick, onMounted, onUnmounted, ref, watch } from 'vue'
import { Button } from '@/components/ui/button'
import { Badge } from '@/components/ui/badge'
import { Popover, PopoverContent, PopoverTrigger } from '@/components/ui/popover'
import { Command, CommandEmpty, CommandGroup, CommandItem } from '@/components/ui/command'
import { Checkbox } from '@/components/ui/checkbox'
import { X } from 'lucide-vue-next'
import { cn } from '@/lib/utils'
import IconTrash from '@/components/icons/IconTrash.vue'
import IconChevronDown from '@/components/icons/IconChevronDown.vue'
import { Input } from '@/components/ui/input/index.js'

const props = defineProps({
  options: {
    type: Array,
    required: true,
    validator: (options) => options.every((opt) => opt.value && opt.label),
  },

  modelValue: {
    type: Array,
    default: () => [],
  },

  placeholder: {
    type: String,
    default: 'Select options...',
  },

  searchPlaceholder: {
    type: String,
    default: 'Введите название города...',
  },

  emptyMessage: {
    type: String,
    default: 'No options found.',
  },

  maxSelections: {
    type: Number,
    default: null,
  },

  variant: {
    type: String,
    default: 'default',
    validator: (value) =>
      ['default', 'error', 'success', 'warning', 'focus', 'hover', 'selected'].includes(value),
  },

  displayVariant: {
    type: String,
    default: 'default',
    validator: (value) =>
      [
        'default',
        'static-label',
        'dynamic-height',
        'with-icon',
        'with-checkbox',
        'long-text',
        'empty-state',
      ].includes(value),
  },

  tagVariant: {
    type: String,
    default: 'default',
    validator: (value) => ['default', 'error', 'warning', 'success'].includes(value),
  },

  staticLabel: {
    type: String,
    default: '',
  },

  icon: {
    type: String,
    default: null,
  },

  showCheckbox: {
    type: Boolean,
    default: true,
  },

  longText: {
    type: Boolean,
    default: false,
  },

  emptyStateMessage: {
    type: String,
    default: 'Доступных опций для выбора нет',
  },

  readonly: {
    type: Boolean,
    default: false,
  },

  disabled: {
    type: Boolean,
    default: false,
  },
  label: {
    type: String,
    default: '',
  },
})

const emit = defineEmits(['update:modelValue', 'change'])

const triggerRef = ref(null)
const triggerWidth = ref(0)

const open = ref(false)
const searchQuery = ref('')

const updateTriggerWidth = () => {
  if (triggerRef.value?.$el) {
    triggerWidth.value = triggerRef.value.$el.offsetWidth
  }
}

onMounted(() => {
  updateTriggerWidth()
  window.addEventListener('resize', updateTriggerWidth)
})

watch(open, async (isOpen) => {
  if (isOpen) {
    await nextTick()
    updateTriggerWidth()
  }
})

const popoverStyle = computed(() => {
  return {
    width: `${triggerWidth.value}px`,
    minWidth: `${triggerWidth.value}px`,
    maxWidth: `${triggerWidth.value}px`,
  }
})

const selectedItems = computed(() => {
  return props.options.filter((option) => props.modelValue.includes(option.value))
})

const filteredOptions = computed(() => {
  if (!searchQuery.value) return props.options

  const query = searchQuery.value.toLowerCase()
  return props.options.filter((option) => option.label.toLowerCase().includes(query))
})

const isSelected = (option) => {
  return props.modelValue.includes(option.value)
}

const toggleOption = (option) => {
  if (props.disabled || props.readonly) return

  const currentValues = [...props.modelValue]
  const isCurrentlySelected = currentValues.includes(option.value)

  if (isCurrentlySelected) {
    const newValues = currentValues.filter((value) => value !== option.value)
    emit('update:modelValue', newValues)
    emit('change', newValues)
  } else {
    if (!props.maxSelections || currentValues.length < props.maxSelections) {
      const newValues = [...currentValues, option.value]
      emit('update:modelValue', newValues)
      emit('change', newValues)
    }
  }
}

const getBadgeVariant = () => {
  switch (props.tagVariant) {
    case 'error':
      return 'destructive'
    case 'warning':
      return 'outline'
    case 'success':
      return 'secondary'
    default:
      return 'secondary'
  }
}

const removeItem = (item) => {
  if (props.disabled || props.readonly) return

  const newValues = props.modelValue.filter((value) => value !== item.value)
  emit('update:modelValue', newValues)
  emit('change', newValues)
}

const clearAll = () => {
  if (props.disabled || props.readonly) return

  emit('update:modelValue', [])
  emit('change', [])
}

const triggerClasses = computed(() => {
  const classes = []

  switch (props.variant) {
    case 'error':
      classes.push('border-destructive focus-visible:ring-destructive text-destructive')
      break
    case 'success':
      classes.push('border-green-500 focus-visible:ring-green-500 text-green-700')
      break
    case 'warning':
      classes.push('border-yellow-500 focus-visible:ring-yellow-500 text-yellow-700')
      break
    case 'focus':
      classes.push('border-primary focus-visible:ring-primary ring-2')
      break
    case 'hover':
      classes.push('border-gray-400 bg-gray-50')
      break
    case 'selected':
      classes.push('border-primary bg-primary/5')
      break
    default:
      classes.push('border-input')
  }

  switch (props.displayVariant) {
    case 'static-label':
      classes.push('pt-6 relative')
      break
    case 'dynamic-height':
      classes.push('min-h-[60px] py-3')
      break
    case 'with-icon':
      classes.push('pl-10')
      break
  }

  if (props.disabled || props.readonly) {
    classes.push('opacity-50 cursor-not-allowed')
  }

  if (props.longText) {
    classes.push('h-auto min-h-[80px]')
  }

  return classes.join(' ')
})

const ariaLabel = computed(() => {
  const count = selectedItems.value.length
  if (count === 0) return props.placeholder
  if (count === 1) return `1 option selected: ${selectedItems.value[0].label}`
  return `${count} options selected`
})

watch(open, (isOpen) => {
  if (!isOpen) {
    searchQuery.value = ''
  }
})

onUnmounted(() => {
  window.removeEventListener('resize', updateTriggerWidth)
})
</script>
