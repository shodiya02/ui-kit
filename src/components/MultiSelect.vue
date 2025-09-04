<template>
  <Popover v-model:open="open">
    <!-- Trigger Button - This is what users click to open the dropdown -->
    <PopoverTrigger as-child>
      <Button
        variant="outline"
        role="combobox"
        :aria-expanded="open"
        :aria-label="ariaLabel"
        :class="cn(
          'w-full justify-between min-h-[40px] h-auto',
          triggerClasses
        )"
      >
        <!-- Selected items display -->
        <div class="flex flex-wrap gap-1 flex-1 text-left">
          <template v-if="selectedItems.length > 0">
            <!-- Show selected items as badges -->
            <Badge
              v-for="item in selectedItems"
              :key="item.value"
              :variant="getBadgeVariant()"
              class="text-xs"
            >
              {{ item.label }}
              <button
                @click.stop="removeItem(item)"
                class="ml-1 hover:text-destructive focus:outline-none focus:text-destructive"
                :aria-label="`Remove ${item.label}`"
              >
                <X class="h-3 w-3" />
              </button>
            </Badge>
          </template>
          <span v-else class="text-muted-foreground">
            {{ placeholder }}
          </span>
        </div>

        <!-- Icon for with-icon variant -->
        <component
          v-if="props.displayVariant === 'with-icon' && props.icon"
          :is="props.icon"
          class="absolute left-3 h-4 w-4 text-muted-foreground"
        />

        <!-- Static label for static-label variant -->
        <label
          v-if="props.displayVariant === 'static-label' && props.staticLabel"
          class="absolute top-2 left-3 text-xs text-muted-foreground bg-background px-1"
        >
          {{ props.staticLabel }}
        </label>

        <!-- Dropdown arrow -->
        <ChevronDown
          class="h-4 w-4 shrink-0 opacity-50 transition-transform duration-200"
          :class="{ 'rotate-180': open }"
        />
      </Button>
    </PopoverTrigger>

    <!-- Dropdown Content -->
    <PopoverContent class="w-full p-0" align="start">
      <Command>
        <!-- Search input -->
        <CommandInput
          :placeholder="searchPlaceholder"
          v-model:value="searchQuery"
        />

        <!-- No results message or empty state -->
        <CommandEmpty>
          <div v-if="props.displayVariant === 'empty-state'" class="flex flex-col items-center justify-center py-8 text-center">
            <div class="w-12 h-12 rounded-full bg-gray-100 flex items-center justify-center mb-4">
              <span class="text-gray-400 text-xl">!</span>
            </div>
            <p class="text-sm text-muted-foreground">{{ props.emptyStateMessage }}</p>
          </div>
          <span v-else>{{ emptyMessage }}</span>
        </CommandEmpty>

        <!-- Options list -->
        <CommandGroup class="max-h-64 overflow-auto">
          <CommandItem
            v-for="option in filteredOptions"
            :key="option.value"
            :value="option.value"
            @select="() => toggleOption(option)"
            class="flex items-center space-x-2 cursor-pointer"
          >
            <!-- Checkbox to show selection state (conditional) -->
            <Checkbox
              v-if="props.showCheckbox"
              :checked="isSelected(option)"
              class="pointer-events-none"
            />
            <!-- Radio button style for with-checkbox variant when showCheckbox is false -->
            <div
              v-else-if="props.displayVariant === 'with-checkbox'"
              class="w-4 h-4 rounded-full border-2 border-gray-300 flex items-center justify-center"
              :class="{ 'bg-blue-500 border-blue-500': isSelected(option) }"
            >
              <div v-if="isSelected(option)" class="w-2 h-2 rounded-full bg-white"></div>
            </div>
            <span class="flex-1" :class="{ 'text-sm': props.longText }">{{ option.label }}</span>
          </CommandItem>
        </CommandGroup>
      </Command>
    </PopoverContent>
  </Popover>
</template>

<script setup>
import { computed, ref, watch } from 'vue'
import { Button } from '@/components/ui/button'
import { Badge } from '@/components/ui/badge'
import { Popover, PopoverContent, PopoverTrigger } from '@/components/ui/popover'
import { Command, CommandEmpty, CommandGroup, CommandInput, CommandItem } from '@/components/ui/command'
import { Checkbox } from '@/components/ui/checkbox'
import { ChevronDown, X } from 'lucide-vue-next'
import { cn } from '@/lib/utils'

// Component Props - These control how the component behaves
const props = defineProps({
  // The list of available options
  options: {
    type: Array,
    required: true,
    validator: (options) => options.every(opt => opt.value && opt.label)
  },

  // Currently selected values
  modelValue: {
    type: Array,
    default: () => []
  },

  // Placeholder text when nothing is selected
  placeholder: {
    type: String,
    default: 'Select options...'
  },

  // Search placeholder text
  searchPlaceholder: {
    type: String,
    default: 'Search options...'
  },

  // Message when no options match search
  emptyMessage: {
    type: String,
    default: 'No options found.'
  },

  // Maximum number of selections allowed
  maxSelections: {
    type: Number,
    default: null
  },

  // Component variant for different states
  variant: {
    type: String,
    default: 'default',
    validator: (value) => ['default', 'error', 'success', 'warning', 'focus', 'hover', 'selected'].includes(value)
  },

  // Display variant for different layouts
  displayVariant: {
    type: String,
    default: 'default',
    validator: (value) => ['default', 'static-label', 'dynamic-height', 'with-icon', 'with-checkbox', 'long-text', 'empty-state'].includes(value)
  },

  // Tag variant for selected items
  tagVariant: {
    type: String,
    default: 'default',
    validator: (value) => ['default', 'error', 'warning', 'success'].includes(value)
  },

  // Static label for static-label variant
  staticLabel: {
    type: String,
    default: ''
  },

  // Icon for with-icon variant
  icon: {
    type: String,
    default: null
  },

  // Show checkbox in options (for with-checkbox variant)
  showCheckbox: {
    type: Boolean,
    default: true
  },

  // Enable long text display mode
  longText: {
    type: Boolean,
    default: false
  },

  // Empty state message
  emptyStateMessage: {
    type: String,
    default: 'Доступных опций для выбора нет'
  },

  // Readonly state
  readonly: {
    type: Boolean,
    default: false
  },

  // Disabled state
  disabled: {
    type: Boolean,
    default: false
  }
})

// Events that this component can emit
const emit = defineEmits(['update:modelValue', 'change'])

// Component state
const open = ref(false)
const searchQuery = ref('')

// Convert selected values to full objects for display
const selectedItems = computed(() => {
  return props.options.filter(option =>
    props.modelValue.includes(option.value)
  )
})

// Filter options based on search query
const filteredOptions = computed(() => {
  if (!searchQuery.value) return props.options

  const query = searchQuery.value.toLowerCase()
  return props.options.filter(option =>
    option.label.toLowerCase().includes(query)
  )
})

// Check if an option is currently selected
const isSelected = (option) => {
  return props.modelValue.includes(option.value)
}

// Toggle selection of an option
const toggleOption = (option) => {
  if (props.disabled || props.readonly) return

  const currentValues = [...props.modelValue]
  const isCurrentlySelected = currentValues.includes(option.value)

  if (isCurrentlySelected) {
    // Remove the option
    const newValues = currentValues.filter(value => value !== option.value)
    emit('update:modelValue', newValues)
    emit('change', newValues)
  } else {
    // Add the option (if under max limit)
    if (!props.maxSelections || currentValues.length < props.maxSelections) {
      const newValues = [...currentValues, option.value]
      emit('update:modelValue', newValues)
      emit('change', newValues)
    }
  }
}

// Get badge variant based on tagVariant prop
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

// Remove a selected item
const removeItem = (item) => {
  if (props.disabled || props.readonly) return

  const newValues = props.modelValue.filter(value => value !== item.value)
  emit('update:modelValue', newValues)
  emit('change', newValues)
}

// Computed classes for the trigger based on variant
const triggerClasses = computed(() => {
  const classes = []

  // State-based styling
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

  // Display variant styling
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

// Accessibility label
const ariaLabel = computed(() => {
  const count = selectedItems.value.length
  if (count === 0) return props.placeholder
  if (count === 1) return `1 option selected: ${selectedItems.value[0].label}`
  return `${count} options selected`
})

// Clear search when dropdown closes
watch(open, (isOpen) => {
  if (!isOpen) {
    searchQuery.value = ''
  }
})
</script>
