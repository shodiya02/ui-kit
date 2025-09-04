<template>
  <div class="min-h-screen bg-gray-50 p-8">
    <div class="max-w-2xl mx-auto space-y-8">
      <div>
        <h1 class="text-3xl font-bold text-gray-900 mb-4">
          Multi-Select Component Demo
        </h1>
        <p class="text-gray-600">
          Testing your custom multi-select component with shadcn-vue foundation
        </p>
      </div>

      <!-- Default Multi-Select -->
      <div class="space-y-2">
        <label class="text-sm font-medium text-gray-700">
          Default Multi-Select
        </label>
        <MultiSelect
          v-model="selectedRegions"
          :options="regionOptions"
          placeholder="Выберите область"
          @change="onSelectionChange"
        />
        <p class="text-xs text-gray-500">
          Selected: {{ selectedRegions.join(', ') || 'None' }}
        </p>
      </div>

      <!-- Error State -->
      <div class="space-y-2">
        <label class="text-sm font-medium text-gray-700">
          Error State
        </label>
        <MultiSelect
          v-model="selectedWithError"
          :options="regionOptions"
          placeholder="Выберите область"
          variant="error"
        />
        <p class="text-xs text-red-600">
          Количество не должно превышать 5т.
        </p>
      </div>

      <!-- Limited Selections -->
      <div class="space-y-2">
        <label class="text-sm font-medium text-gray-700">
          Maximum 3 Selections
        </label>
        <MultiSelect
          v-model="selectedLimited"
          :options="regionOptions"
          :max-selections="3"
          placeholder="Выберите до 3 областей"
        />
      </div>

      <!-- Disabled State -->
      <div class="space-y-2">
        <label class="text-sm font-medium text-gray-700">
          Disabled State
        </label>
        <MultiSelect
          :model-value="['tashkent']"
          :options="regionOptions"
          disabled
          placeholder="Disabled component"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import MultiSelect from './components/MultiSelect.vue'

// Sample data matching your Figma design
const regionOptions = [
  { value: 'tashkent', label: 'г. Ташкент' },
  { value: 'samarkand', label: 'г. Самарканд' },
  { value: 'navoi', label: 'г. Навоиган' },
  { value: 'andijan', label: 'г. Андижан' },
  { value: 'shahrisabz', label: 'г. Шахайбулак' },
  { value: 'ikra', label: 'г. Икра' },
  { value: 'kisto', label: 'г. Кисто' },
  { value: 'nukus', label: 'г. Нукус' },
  { value: 'dnisokchabloktrn', label: 'г. Днисокчаблоктрн' }
]

// Reactive state for different component instances
const selectedRegions = ref(['tashkent'])
const selectedWithError = ref([])
const selectedLimited = ref([])

// Event handler example
const onSelectionChange = (newValues) => {
  console.log('Selection changed:', newValues)
}
</script>
